---

copyright:
  years: 2020, 2025
lastupdated: "2025-04-17"

keywords: dns-svcs, DNS Services, Private DNS, dns support script, dns backup script

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Exporting your {{site.data.keyword.dns_short}} configuration
{: #writing-dns-svcs-config-to-file}

This section describes how to run a script to copy your {{site.data.keyword.dns_full}} instance configuration. The example script writes the following information to a file.

* The specified instance itself.
* Custom resolvers in the instance.
* GLB pools in this instance.
* GLB monitors in this instance.
* Cross account linked zone whose accesses was requested by this instance.
* Permitted networks for each of the linked zones.
* All DNS zones and DNS zone data for an instance.
* All resource record data for each DNS zone.
* All permitted network data for each DNS zone.
* Cross account linked zones access requests to any DNS zones on this instance.

This data can be helpful in debugging issues and can be provided to the Support team (if configuration data is not considered private) if you have a Support issue. The data can also serve as a backup.

This data is "export only" and does not work to import a configuration.
{: note}

## Script usage
{: #script-usage}

The basic script is used in the following example.

```console
$ ./copy_dns_config.sh <instance ID, NAME, or CRN> [path/to/output-file]
#   Required: <instance ID, NAME, or CRN>
#   Optional: [path/to/output-file]
```
{: codeblock}

Where `<instance ID, NAME, or CRN>` is replaced by the relevant {{site.data.keyword.dns_short}} instance ID, NAME, or CRN. Optionally, pass a path to an output file as the second argument. If no output file argument is given, the output is written to a file in the current directory.

Example usage:

```console
./copy_dns_config.sh my-instance1
./copy_dns_config.sh my-instance2 ~/dns-output.txt
```
{: pre}

## Script requirements
{: #script-requirements}

To run the script, you need the following prequisites.

* [IBM Cloud CLI](/docs/cli?topic=cli-getting-started)
    * You must be logged in to your {{site.data.keyword.cloud_notm}} account.
    * Use `ibmcloud login` to log in.
* [jq](https://stedolan.github.io/jq/), a command line JSON processor.
    * `$ brew install jq # macOS`
    * `$ apt-get install jq # Ubuntu`

## The script
{: #the-script}

```bash
#!/usr/bin/env bash
#
# copy_dns_config.sh
#
# This script will write to a file all the zones, resource records,
# and permitted networks within an IBM Cloud DNS Services instance.
#
# This script requires jq to be installed: https://stedolan.github.io/jq/
#
# Usage:
#   ./copy_dns_config.sh <instance ID, NAME, or CRN> [path/to/output-file]
#
#   Required: <instance ID, NAME, or CRN>
#   Optional: [path/to/output-file]
#
# Examples:
#   ./copy_dns_config.sh my-instance1
#   ./copy_dns_config.sh my-instance2 ~/dns-output.txt
#

# $1 is the DNS Services instance NAME, ID, or CRN
instance="$1"
# $2 is the output file path
file="$2"

if [ -z "$instance" ]; then
    echo "[ERROR]: DNS Services ID, NAME, or CRN is required."
    echo "Usage:"
    printf "\t./copy_dns_config.sh <instance ID, NAME, or CRN> [path/to/output-file]\n"

    echo ""
    echo "Use one of the following DNS Services instances when running the script:"
    ibmcloud dns instances
    exit 1
fi

# jq is required
command -v jq >/dev/null 2>&1 ||  { echo >&2 \
    "[ERROR]: jq (https://stedolan.github.io/jq/) is not installed."; \
    exit 1; }

if [[ "$instance" == crn* ]]; then
    # CRN passed as arg, extract the Instance ID
    parts=($(echo $instance | tr ":" "\n"))
    instance="${parts[7]}"
fi

timestamp="$(date +'%F')"

# determine output file
if [ -z "$file" ]; then
    file="dns_svcs_${instance}_${timestamp}.txt"
fi
echo ""
echo "Saving output to file: $file"
echo ""

printf "# Timestamp\n\n" >> "$file"
echo "${timestamp}" >> "$file"
echo "" >> "$file"

# set DNS Services instance context
ibmcloud dns instance-target "$instance"

if [ $? -eq 1 ]
then
    echo "[ERROR]: Failed to set instance. Aborting."
    exit 1
fi

# list the target instance
printf "# Instance\n\n" >> "$file"
ibmcloud dns instance "$instance" --output JSON >> "$file"
echo "" >> "$file"

# list all custom resolvers for the instance
printf "# Custom resolvers in the instance\n\n" >> "$file"
custom_resolvers="$(ibmcloud dns custom-resolvers --output JSON | jq -n 'try input // ["none"]')"
echo "$custom_resolvers" >> "$file"
echo "" >> "$file"

if [[ "$(echo "$custom_resolvers" | jq -r '.[0]')" != "none" ]]; then
    custom_resolver_ids="$(echo $custom_resolvers | jq '[.[].id]')"
    for custom_resolver_id in $(echo "${custom_resolver_ids}" | jq -r '.[]'); do
        # list all custom resolver forwarding rules for the custom resolver
        printf "# Custom resolvers forwarding rules in custom resolver with ID ${custom_resolver_id}\n\n" >> "$file"
        ibmcloud dns custom-resolver-forwarding-rules "$custom_resolver_id" --output JSON \
            | jq -n 'try input // ["none"]' \
            >> "$file"
        echo "" >> "$file"

        # list all secondary zones for the custom resolver
        printf "# Secondary zones for custom resolver with ID ${custom_resolver_id}\n\n" >> "$file"
        ibmcloud dns secondary-zones "$custom_resolver_id" --output JSON \
            | jq -n 'try input // ["none"]' \
            >> "$file"
        echo "" >> "$file"
    done
fi

# list glb pools for the instance
printf "# GLB pools in this instance ${instance}\n\n" >> "$file"
ibmcloud dns glb-pools --output JSON | jq -n 'try input // ["none"]' >> "$file"
echo "" >> "$file"

# list glb monitors for the instance
printf "# GLB monitors in this instance ${instance}\n\n" >> "$file"
ibmcloud dns glb-monitors --output JSON | jq -n 'try input // ["none"]' >> "$file"
echo "" >> "$file"

# list all cross account linked zones whose access was requested by this instance to another instance
printf "# Cross account linked zones whose access was requested by this instance ${instance}\n\n" >> "$file"
linked_zones="$(ibmcloud dns cross-account linked-zones --output JSON | jq -n 'try input // ["none"]')"
echo "$linked_zones" >> "$file"
echo "" >> "$file"

# for each linked zone requested by this instance
if [[ "$(echo "$linked_zones" | jq -r '.[0]')" != "none" ]]; then 
    linked_zone_ids="$(echo $linked_zones | jq '[.[].id]')"

    for linked_zone_id in $(echo "${linked_zone_ids}" | jq -r '.[]'); do
        printf "# Cross account linked zones permitted networks for linked zone with ID ${linked_zone_id}\n\n" >> "$file"
        ibmcloud dns cross-account linked-zone-permitted-networks "$linked_zone_id" \
            | jq -n 'try input // ["none"]' \
            >> "$file"
        echo "" >> "$file"
    done
fi

# list all DNS Services zones for the instance
zones="$(ibmcloud dns zones --output JSON | jq -n 'try input // ["none"]')"
printf "# Zones in this instance ${instance}\n\n" >> "$file"
echo "${zones}" >> "$file"
echo "" >> "$file"

# for each zone
if [[ "$(echo "$zones" | jq -r '.[0]')" != "none" ]]; then 
    zone_ids="$(echo $zones | jq '[.[].id]')"

    for zone_id in $(echo "${zone_ids}" | jq -r '.[]'); do
        printf "# Resource records in zone with ID ${zone_id}\n\n" >> "$file"

        # list all resource records for the zone
        first_page=""
        for i in {1..4}
        do
            if [[ $i -eq 1 ]]; then
                first_page="$(ibmcloud dns resource-records "$zone_id" --per-page 1000 --page $i --output JSON | jq -n 'try input // ["none"]')"
                echo "$first_page" >> "$file"

                if [[ "$(echo "$first_page" | jq -r 'if type == "array" then .[0] else . end')" != "none" ]]; then 
                    break
                fi
            else
                ibmcloud dns resource-records "$zone_id" --per-page 1000 --page $i --output JSON >> "$file"
            fi
        done
        echo "" >> "$file"

        # list all permitted networks for the zone
        printf "# Permitted networks in zone with ID ${zone_id}\n\n" >> "$file"
        ibmcloud dns permitted-networks "$zone_id" --output JSON \
            | jq -n 'try input // ["none"]' \
            >> "$file"
        echo "" >> "$file"

        # list cross account linked zone requests made from another instance to this instance
        printf "# Cross account linked zones access requests to this zone with ID ${zone_id}\n\n" >> "$file"
        ibmcloud dns cross-account access-requests "$zone_id" --output JSON \
            | jq -n 'try input // ["none"]' \
            >> "$file"
        echo "" >> "$file"
    done
fi

```
{: codeblock}

## Script alternatives
{: #script-alternatives}

* This example script uses the outputs of the plugin and commands related to this service through the CLI.
* A full list of {{site.data.keyword.dns_full_notm}} CLI commands are available in the [documentation](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands).
* APIs that are noted in the [API documentation](/apidocs/dns-svcs) can also produce similar outputs.
* A different script can export different resources under {{site.data.keyword.dns_short}} in different formats, as needed.

## Alternatives to a script
{: #alternatives-to-a-script}

* A more portable alternative is to use an Infrastructure as Code tool such as Terraform for {{site.data.keyword.dns_short}} [as documented](/docs/dns-svcs?topic=dns-svcs-terraform-setup-dns-svcs).
* Compared to custom scripts that only export, tools like Terraform allow for easier export, import, and other operations needed to manage configurations in a more uniform manner.

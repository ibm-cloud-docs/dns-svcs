---

copyright:
  years: 2020
lastupdated: "2020-04-06"

keywords: dns-svcs, DNS Services, Private DNS, dns support script, dns backup script

subcollection: dns-svcs

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Exporting your {{site.data.keyword.dns_short}} configuration
{: #writing-dns-svcs-config-to-file}

This section describes how to run a script to copy your {{site.data.keyword.dns_full}} instance configuration. It writes the following to a file:
* All DNS zones and DNS zone data for an instance.
* All resource record data for each DNS zone.
* All permitted network data for each DNS zone.

This data can be helpful in debugging issues and can be provided to the support team (if configuration data is not considered private) in the case of a support issue. The data can also serve as a backup.  

This data is "export only" and does not work to import a configuration.
{: note}

## Usage
{: #usage}

The basic usage is as follows:

```console
$ ./copy_dns_config.sh <instance ID, NAME, or CRN> [path/to/output-file]
#   Required: <instance ID, NAME, or CRN>
#   Optional: [path/to/output-file]
```
{: #codeblock}

Where `<instance ID, NAME, or CRN>` is replaced by the relevant {{site.data.keyword.dns_short}} instance ID, NAME, or CRN. Optionally, pass a path to an output file as the second argument. If no output file argument is given the output is written to a file in the current directory.

Example usage:

```console
$ ./copy_dns_config.sh my-instance1
$ ./copy_dns_config.sh my-instance2 ~/dns-output.txt
```
{: pre}

## Script requirements
{: #script-requirements}

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
instance=$1
# $2 is the output file path
file=$2

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
    parts=($(echo $CRN | tr ":" "\n"))
    instance="${parts[7]}"
fi

timestamp=$(date +"%F")

# determine output file
if [ -z "$file" ]; then
    file="dns_svcs_${instance}_${timestamp}.txt"
fi
echo ""
echo "Saving output to file: $file"

printf "$timestamp\n\n" >> $file

# set DNS Services instance context
ibmcloud dns instance-target $instance >> $file

if [ $? -eq 1 ]
then
    echo "[ERROR]: Failed to set instance. Aborting."
    exit 1
fi

# list all DNS Services zones
zones=$(ibmcloud dns zones --output JSON)
printf "\nZones for service instance $instance:\n$zones\n" >> $file

zone_ids=$(echo $zones | jq '[.[].id]')
printf "\nZone IDs:\n$zone_ids\n" >> $file

# get details for each zone
for zone_id in $(echo "${zone_ids}" | jq -r '.[]'); do
    printf "\n==================================================================" >> $file
    printf "\nZone ID: $zone_id\nInstance: $instance\n\nResource records:\n" >> $file

    # list all resource records for the zone
    for i in {1..4}
    do
        ibmcloud dns resource-records $zone_id --per-page 1000 --page $i --output JSON >> $file
    done

    printf "\nPermitted networks:\n" >> $file
    # list all permitted networks for the zone
    ibmcloud dns permitted-networks $zone_id --output JSON >> $file
done
```
{: codeblock}

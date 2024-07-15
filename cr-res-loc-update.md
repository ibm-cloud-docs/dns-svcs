---

copyright:
  years: 2021, 2024
lastupdated: "2024-07-15"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Updating custom resolver locations
{: #cr-res-loc-update}

You can update custom resolver locations in {{site.data.keyword.dns_full}} by using the UI, CLI, or API.
{: shortdesc}

## Updating a resolver location using the UI
{: #ui-update-res-loc}
{: ui}

From the custom resolver details page, select the **Resolver locations** tab. Here you can enable or disable your custom resolver by setting the toggle switch. Change the priority of your resolver location by clicking the up or down arrows to alter the priority order of the list.

When the resolver location is disabled, the **Subnet** column changes to a list menu from which you can select a different subnet for your resolver location. When the resolver location is enabled, the **Subnets** column becomes static.

## Updating a resolver location using the CLI
{: #cli-update-res-loc}
{: cli}

To update a resolver location using the CLI, run the following command:

`ibmcloud dns custom-resolver-location-update RESOLVER_ID LOCATION_ID [--subnet SUBNET_CRN] [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **LOCATION_ID** is the ID of the custom resolver location.
- **--subnet** is the CRN of the subnet.
- **--enabled** determines whether to enable the custom resolver location.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used instead.
- **--output** specifies output format. Currently, JSON is the only supported format.

## Adding a resolver location using the API
{: #api-update-res-loc}
{: api}

To update a custom resolver location using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `location_id`, which is the custom resolver location ID.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, get the details of your custom resolver:

    ```sh
    {
      "enabled": false,
      "subnet_crn": "crn:v1:bluemix:public:is:us-south-1:a/01652b251c3ae2787110a995d8db0135::subnet:0716-b49ef064-0f89-4fb1-8212-135b12568f04"
    }
    ```
    {: codeblock}

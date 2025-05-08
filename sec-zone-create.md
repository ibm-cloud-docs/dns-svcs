---

copyright:
  years: 2022, 2025
lastupdated: "2025-05-08"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a secondary zone
{: #create-secondary-zone}

Create a secondary zone by using the UI, CLI, or API.
{: shortdesc}

## Creating a secondary zone in the console
{: #ui-create-secondary-zone}
{: ui}

To create a secondary zone using the UI, take the following steps:

1. Navigate to the **Custom resolver** section of your DNS Services instance, and select the custom resolver where you want to create a secondary zone.
1. In the **Custom resolver details** page, select the **Secondary zone** tab.
1. Click **Create secondary zone**.
1. Enter a name for the secondary zone.
1. Optionally, enter a description for the secondary zone.
1. Enter up to two IP addresses of your IXFR-capable or AXFR-capable DNS servers, separated by a comma.
1. Click **Create**.

The new secondary zone now appears in the list of secondary zones in the **Custom resolver details** page, and is enabled by default.

## Creating a secondary zone from the CLI
{: #cli-create-secondary-zone}
{: cli}

To create a secondary zone using the CLI, run the following command:

```sh
ibmcloud dns secondary-zone-create RESOLVER_ID --name NAME --transfer-from ADDRESS1,ADDRESS2 [--description DESCRIPTION] [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **RESOLVER_ID** is the ID of the custom resolver. Required.
* **--name value** is the name of the secondary zone.
* **--transfer-from value** is the addresses of the DNS servers from where the secondary zone data is transferred.
* **--description value** is the description of the secondary zone.
* **--enabled value** specifies whether the secondary zone is enabled.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by `ibmcloud dns instance-target INSTANCE` is used.
* **--output value** specifies the output format. Currently, JSON is the only supported format.

## Creating a secondary zone with the API
{: #api-create-secondary-zone}
{: api}

To create a secondary zone using the API, follow these steps:

1. Set up your [API environment](/apidocs/dns-svcs#authentication) with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `INSTANCE_ID`, which is the unique identifier of a service instance.
    * `RESOLVER_ID`, which is the unique identifier of a custom resolver.
    * `X-Correlation-ID` (optional), which uniquely identifies a request.
1. When all variables are initiated, create a secondary zone:

```sh
curl -X POST   https://api.dns-svcs.cloud.ibm.com/v1/instances/2be5d4a7-78f0-4c62-a957-41dc15342777/custom_resolvers/ddbe7a53-7971-46dc-b021-420335c31562/secondary_zones   -H 'Content-Type: application/json'   -H 'Authorization: Bearer xxxxxx'   -d '{
  "description": "secondary zone",
  "zone": "example.com",
  "enabled": false,
  "transfer_from": [
    "10.0.0.7"
  ]
}'
```
{: codeblock}

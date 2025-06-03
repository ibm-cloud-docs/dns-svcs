---

copyright:
  years: 2022, 2025
lastupdated: "2025-06-03"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Editing a secondary zone
{: #edit-secondary-zone}

Edit a secondary zone by using the UI, CLI, or API.
{: shortdesc}

## Editing a secondary zone in the console
{: #ui-edit-secondary-zone}
{: ui}

To edit a secondary zone using the UI, take the following steps:

1. Navigate to the **Custom resolver** section of your DNS Services instance, and select the custom resolver in which you want to edit a secondary zone.
1. In the **Custom resolver details** page, select the **Secondary zone** tab.
1. Select the secondary zone that you want to edit.
1. Enter the changes for the secondary zone. Only the description and IP address fields can be edited.
1. Click **Save**.

To change the zone name, delete the secondary zone rule and create the rule again with the new name.
{: tip}

## Editing a secondary zone from the CLI
{: #cli-edit-secondary-zone}
{: cli}

To edit a secondary zone using the CLI, run the following command:

```sh
ibmcloud dns secondary-zone-update RESOLVER_ID SECONDARY_ZONE_ID [--transfer-from ADDRESS1,ADDRESS2] [--description DESCRIPTION] [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **RESOLVER_ID** is the ID of the custom resolver. Required.
* **SECONDARY_ZONE_ID** is the ID of the secondary zone. Required.
* **--transfer-from value** is the addresses of the DNS servers from where the secondary zone data is transferred.
* **--description value** is the description of the secondary zone.
* **--enabled value** is whether the secondary zone is enabled.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by ibmcloud dns instance-target INSTANCE is used.
* **--output value** specifies output format. Currently, `json` is the only supported format.


## Editing a secondary zone with the API
{: #api-edit-secondary-zone}
{: api}

To edit a secondary zone using the API, follow these steps:

1. Set up your [API environment](/apidocs/dns-svcs#authentication) with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `INSTANCE_ID`, which is the unique identifier of a service instance.
    * `RESOLVER_ID`, which is the unique identifier of a custom resolver.
    * `SECONDARY_ZONE_ID` is the unique identifier of a secondary zone.
    * `X-Correlation-ID` (optional), which uniquely identifies a request.
1. When all variables are initiated, edit the secondary zone:

```sh
curl -X PATCH   https://api.dns-svcs.cloud.ibm.com/v1/instances/2be5d4a7-78f0-4c62-a957-41dc15342777/custom_resolvers/ddbe7a53-7971-46dc-b021-420335c31562/secondary_zones/f97ef698-d5fa-4f91-bc5a-33f17d143b7d   -H 'Content-Type: application/json'   -H 'Authorization: Bearer xxxxxx'   -d '{
    "description": "secondary zone",
    "enabled": false,
    "transfer_from": [
      "10.0.0.7"
    ]
}'
```
{: codeblock}

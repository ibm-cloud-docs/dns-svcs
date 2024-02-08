---

copyright:
  years: 2022
lastupdated: "2022-06-24"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Listing and getting details of a linked zone
{: #list-linked-zone}

List all linked zones and get the details of a linked zone by using the UI, CLI, or API.
{: shortdesc}

## Listing a linked zone using the UI
{: #ui-list-linked-zone}
{: ui}

To list all linked zones using the UI, navigate to the **Zones** section of your {{site.data.keyword.dns_short}} instance, then select the **Linked zones** tab.

## Getting the details of a linked zone using the UI
{: #ui-get-details}
{: ui}

To get the details of a linked zone using the UI, take the following steps:

1. Navigate to the **Zones** section of your {{site.data.keyword.dns_short}} instance, then select the **Linked zones** tab.
1. Click the link in the **Zone name** column of the linked zone you want to view.

The **Linked zone details** page appears, where you can edit the linked zone details, [delete the linked zone](/docs/dns-svcs?topic=dns-svcs-update-linked-zone), and manage permitted networks. For more information, see [Add a permitted network](/docs/dns-svcs?topic=dns-svcs-add-permit-network-linked).

## Listing a linked zone using the CLI
{: #cli-list-linked-zone}
{: cli}

To list a linked zone using the CLI, run the following command:

```sh
ibmcloud dns cross-account linked-zones [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by `ibmcloud dns instance-target INSTANCE` is used.
* **--output value** specifies the output format. Currently, `json` is the only supported format.

## Getting the details of a linked zone using the CLI
{: #cli-get-details}
{: cli}

To get the details of a linked zone using the API, run the following command:

```sh
ibmcloud dns cross-account linked-zone LINKED_ZONE_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **LINKED_ZONE_ID** is the ID of linked zone.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by `ibmcloud dns instance-target INSTANCE` is used.
* **--output value** specifies the output format. Currently, `json` is the only supported format.

## Listing all linked zones using the API
{: #api-list-linked-zone}
{: api}

To list all linked zones using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `linked_dnszone_id` which is the unique identifier of a linked zone.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, list the linked zones:

    ```sh
    {
      "description": "linked zone example",
      "label": "dev"
    }
    ```
    {: codeblock}


## Getting the details of a linked zone using the API
{: #api-get-details}
{: api}

To get the details of a linked zone using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `linked_dnszone_id` which is the unique identifier of a linked zone.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, get the details of the linked zone:

    ```sh
    curl -X GET "https://api.dns-svcs.cloud.ibm.com/v1/instances/test/linked_dnszones/example" -H  "accept: application/json" -H  "X-Correlation-ID: property"
    ```
    {: codeblock}

---

copyright:
  years: 2022
lastupdated: "2022-06-24"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Listing and getting details of permitted networks
{: #list-perm-nets}

List all permitted networks and get the details of a permitted network in your linked zone by using the UI, CLI, or API.
{: shortdesc}

## Getting the details of a permitted network using the UI
{: #ui-get-details-perm-nets}
{: ui}

To get the details of a permitted network using the UI, take the following steps:

1. Navigate to the **Zones** section of your {{site.data.keyword.dns_short}} instance, then select the **Linked zones** tab.
1. Click the link in the **Zone name** column of the linked zone you want to view.

In the **Linked zone details** page, the **Permitted networks** tab lists the details of the permitted network.

## Listing all permitted networks using the CLI
{: #cli-list-perm-nets}
{: cli}

To list a permitted network using the CLI, run the following command:

```sh
ibmcloud dns cross-account linked-zones [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by `ibmcloud dns instance-target INSTANCE` is used.
* **--output value** specifies the output format. Currently, `json` is the only supported format.

## Getting the details of a permitted network using the CLI
{: #cli-get-details-perm-nets}

To get the details of a permitted network using the API, run the following command:

```sh
ibmcloud dns cross-account linked-zone LINKED_ZONE_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **LINKED_ZONE_ID** is the ID of permitted network.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by `ibmcloud dns instance-target INSTANCE` is used.
* **--output value** specifies the output format. Currently, `json` is the only supported format.

## Listing a permitted network using the API
{: #api-list-perm-nets}
{: api}

To list all linked zones using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `INSTANCE_ID`, which is the unique identifier of a service instance.
    * `LINKED_DNSZONE_ID` which is the unique identifier of a linked zone.
    * `IAM_TOKEN`, which is the IAM authorization token.
1. When all variables are initiated, list the linked zones:

    ```sh
    curl -X GET \
        https://api.dns-svcs.cloud.ibm.com/v1/instances/$INSTANCE_ID/linked_dnszones/$LINKED_DNSZONE_ID/permitted_networks \
        -H "Authorization: $IAM_TOKEN"
    ```
    {: codeblock}


## Getting the details of a permitted network using the API
{: #api-get-details-perm-nets}

To get the details of a permitted network using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `INSTANCE_ID`, which is the unique identifier of a service instance.
    * `LINKED_DNSZONE_ID` which is the unique identifier of a linked zone.
    * `PERMITTED_NETWORK_ID` which is the unique identifier of a permitted network
    * `IAM_TOKEN`, which is the IAM authorization token.
1. When all variables are initiated, get the details of the permitted network:

    ```sh
    curl -X GET \
        https://api.dns-svcs.cloud.ibm.com/v1/instances/$INSTANCE_ID/linked_dnszones/$LINKED_DNSZONE_ID/permitted_networks/$PERMITTED_NETWORK_ID \
        -H "Authorization: $IAM_TOKEN"
    ```
    {: codeblock}

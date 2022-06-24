---

copyright:
  years: 2022
lastupdated: "2022-06-24"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Removing a permitted network from a linked zone
{: #remove-permit-network-linked}

Remove a permitted network from your linked zone by using the UI, CLI, or API.
{: shortdesc}

## Removing a permitted network using the UI
{: #ui-remove-permit-network}
{: ui}

To remove a permitted network using the UI, take the following steps:

1. Navigate to the **Zones** section of your {{site.data.keyword.dns_short}} instance, then select the **Linked zones** tab.
1. Click the link in the **Zone name** column of the linked zone you want to view the **Linked zone details** page.
1. In the **Permitted networks** tab, click the overflow menu ![Overflow menu icon](images/overflow-icon.png "Overflow menu icon") of the permitted network you want to delete, and select **Delete**.

## Removing a permitted network using the CLI
{: #cli-remove-permit-network}
{: cli}

To remove a permitted network from your linked zone using the CLI, run the following command:

```sh
ibmcloud dns cross-account linked-zone-permitted-network-remove LINKED_ZONE_ID PERMITTED_NETWORK_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **LINKED_ZONE_ID** is the ID of the linked zone.
* **PERMITTED_NETWORK_ID** is the ID of the permitted network.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by `ibmcloud dns instance-target INSTANCE` is used.
* **--output value** specifies the output format. Currently, `json` is the only supported format.

## Removing a permitted network using the API
{: #api-remove-permit-network}
{: api}

To remove a permitted network from your linked zone using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `INSTANCE_ID`, which is the unique identifier of a service instance.
    * `LINKED_DNSZONE_ID` which is the unique identifier of a linked zone.
    * `PERMITTED_NETWORK_ID` which is the unique identifier of a permitted network
    * `IAM_TOKEN`, which is the IAM authorization token.
1. When all variables are initiated, remove the permitted network:

    ```sh
    curl -X DELETE \
        https://api.dns-svcs.cloud.ibm.com/v1/instances/$INSTANCE_ID/linked_dnszones/$LINKED_DNSZONE_ID/permitted_networks/$PERMITTED_NETWORK_ID \
        -H "Authorization: $IAM_TOKEN"
    ```
    {: codeblock}



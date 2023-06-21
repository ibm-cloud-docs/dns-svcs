---

copyright:
  years: 2022
lastupdated: "2022-06-24"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Updating a linked zone
{: #update-linked-zone}

Update the properties of a linked zone by using the UI, CLI, or API.

## Updating a linked zone using the UI
{: #ui-update-linked-zone}
{: ui}

To update the properties of a linked zone using the UI, take the following steps:

1. Navigate to the **Zones** section of your {{site.data.keyword.dns_short}} instance, then select the **Linked zones** tab.
1. Click the link in the **Zone name** column of the linked zone you want to update.
1. Click **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit icon") of the linked zone you want to update.
1. Enter your changes and click **Save**.

## Updating a linked zone using the CLI
{: #cli-update-linked-zone}
{: cli}

To update a linked zone using the CLI, run the following command:

```sh
ibmcloud dns cross-account linked-zone-update LINKED_ZONE_ID [--label LABEL] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **LINKED_ZONE_ID** is the ID of linked zone.
* **--label value** is the label of linked zone.
* **--description value** is the description of the linked zone.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by `ibmcloud dns instance-target INSTANCE` is used.
* **--output value** specifies the output format. Currently, `json` is the only supported format.

## Updating a linked zone using the API
{: #api-update-linked-zone}
{: api}

To update the properties of a linked zone using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `INSTANCE_ID`, which is the unique identifier of a service instance.
    * `LINKED_DNSZONE_ID` which is the unique identifier of a linked zone.
    * `IAM_TOKEN`, which is the IAM authorization token.
1. When all variables are initiated, update the properties of the linked zone:

    ```sh
    curl -X PATCH \
        https://api.dns-svcs.cloud.ibm.com/v1/instances/$INSTANCE_ID/linked_dnszones/$LINKED_DNSZONE_ID \
        -H "Authorization: $IAM_TOKEN" \
        -H "Content-Type: application/json" \
        -d '{
          "description": "linked zone desc",
          "label": "linked-zone-lable"
        }'
    ```
    {: codeblock}

When the linked zone is updated successfully, the updated information is returned, similar to the following response:

```sh
{
  "id": "5365b73c-ce6f-4d6f-ad9f-d9c131b26370",
  "instance_id": "5cbc3c1b-021c-4ad7-b9e4-a5dfefdecf85",
  "name": "example.com",
  "description": "linked zone example",
  "linked_to": {
    "instance_crn": "crn:v1:staging:public:pdnsdev:global:a/01652b251c3ae2787110a995d8db0135:abe30019-1c08-42dc-9ad9-a0682af70054::",
    "zone_id": "05855abe-3908-4cdc-bf0d-063e0b1c296d"
  },
  "state": "PENDING_APPROVAL",
  "label": "dev",
  "approval_required_before": "2022-03-16T07:23:25Z",
  "created_on": "2022-03-09T07:23:25Z",
  "modified_on": "2022-03-09T07:23:25Z"
}
```
{: screen}

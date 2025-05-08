---

copyright:
  years: 2022, 2025
lastupdated: "2025-05-08"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Creating a linked zone
{: #create-linked-zone}

Create a linked zone from your DNS Services instance to a DNS zone in another account by using the UI, CLI, or API.
{: shortdesc}

The following table shows the possible states your linked zone might be in as the access request progresses.

| Requestor State | Description |
|-----------------|-------------|
|Approval pending|Waiting on approval from account owner|
|Pending network add|Account owner approved cross-account access, but no permitted networks have been added to the linked zone|
|Active|Permitted networks have been added to the linked zone|
|Approval rejected|Account owner rejected the cross-account access request|
|Approval timed out|Account owner did not respond to the request for over 7 days|
|Approval revoked|Account owner has revoked the cross-account access|
{: caption="Requestor states" caption-side="bottom"}

## Creating a linked zone in the console
{: #ui-create-linked-zone}
{: ui}

To create a linked zone using the UI, gather the following information from the owner of the account to which you are linking:
* Zone ID
* DNS services instance ID

After you have the required information, take the following steps to create a linked zone:

1. Navigate to the **Zones** section of your DNS Services instance, then select the **Linked zones** tab.
1. Click **Request linked zones**.
1. Enter the Zone ID of the zone to which you are requesting access.
1. Enter the DNS services instance ID to which you are requesting access.
1. Optionally, give the connection a label and description.
1. Click **Submit**.

The status column changes to "Request pending", and your request is sent to the owner of the account you're establishing a link to. The owner has 7 days to respond before the request times out.

If the request times out, you must create a new request to establish a linked zone.
{: tip}

After the request is approved, the status changes to "Pending network add". For more information, see [Adding a permitted network to a linked zone](/docs/dns-svcs?topic=dns-svcs-add-permit-network-linked).

## Creating a linked zone from the CLI
{: #cli-create-linked-zone}
{: cli}

To create a linked zone using the CLI, run the following command:

```sh
ibmcloud dns cross-account linked-zone-create --owner-instance-id OWNER_INSTANCE_ID --owner-zone-id OWNER_ZONE_ID [--label LABEL] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--owner-instance-id value** is the ID of owner's instance.
* **--owner-zone-id value** is the ID of owner's zone.
* **--label value** is the label of linked zone.
* **--description value** is the description of the linked zone.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by `ibmcloud dns instance-target INSTANCE` is used.
* **--output value** specifies the output format. Currently, `json` is the only supported format.

## Creating a linked zone with the API
{: #api-create-linked-zone}
{: api}

To create a linked zone using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `INSTANCE_ID`, which is the unique identifier of a service instance.
    * `IAM_TOKEN`, which is the IAM authorization token.
1. When all variables are initiated, create a linked zone:

    ```sh
    curl -X POST \
         https://api.dns-svcs.cloud.ibm.com/v1/instances/$INSTANCE_ID/linked_dnszones \
         -H "Authorization: $IAM_TOKEN" \
         -H "Content-Type: application/json" \
         -d '{
           "owner_instance_id": "c60c8beb-e291-4207-93e0-38e31744bbff",
           "owner_zone_id": "1a5acfd7-6283-49a4-ae5e-0ca19209406e",
           "description": "linked zone test",
           "label": "dev"
         }'
    ```
    {: codeblock}

When the linked zone is created successfully, a cross account request is sent to the account owner. The following response shows an example.

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

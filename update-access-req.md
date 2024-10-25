---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-25"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Updating an access request
{: #update-access-req}

As the owner of the account the access request comes to, you can update the properties of an access request by using the UI, CLI, or API.
{: shortdesc}

The following table describes the actions you can take as the account owner.

|Action|Description|
|------|-----------|
|Approve|Grants access to establish a linked zone. |
|Reject|Denies the access request. |
|Revoke|Removes access requests that were granted previously. |
|No action | The request times out if you take no action after 7 days elapse.|
{: caption="Owner states" caption-side="bottom"}

## Updating an access request in the UI
{: #ui-update-access-req}
{: ui}

To update an access request using the UI, take the following steps:

1. Navigate to the **Zones** section of your {{site.data.keyword.dns_short}} instance.
1. Click the link in the **Name** column of the request you want to review.
1. Select the  **Cross-account ACL** tab.
1. Click overflow menu ![Overflow menu icon](images/overflow-icon.png "Overflow menu icon") of the linked zone for which you want to manage an access request.
1. Select **Review request**.
1. Select **Reject** or **Approve** to complete the request, or click the `X` at the top right of the side panel to close the request and take no action.


## Updating an access request from the CLI
{: #cli-update-access-req}
{: cli}

To update an access request using the CLI, run the following command:

```sh
ibmcloud dns cross-account access-request-update ZONE_ID REQUEST_ID --action ACTION [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **ZONE_ID** is the ID of the owner's zone.
* **REQUEST_ID** is the ID of the access request.
* **--action value** is the action applied to the access request. Valid values: "APPROVE", "REJECT", "REVOKE".
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by `ibmcloud dns instance-target INSTANCE` is used.
* **--output value** specifies the output format. Currently, `json` is the only supported format.

## Updating an access request with the API
{: #api-update-access-req}
{: api}

To update the properties of an access request using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `INSTANCE_ID`, which is the unique identifier of a service instance.
    * `DNSZONE_ID` which is the unique identifier of a DNS zone.
    * `ACCESS_REQUEST_ID` which is the  unique identifier of an access request.
    * `IAM_TOKEN`, which is the IAM authorization token.
1. When all variables are initiated, update the properties of the access request:

    ```sh
    curl -X PATCH \
        https://api.dns-svcs.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/access_requests/$ACCESS_REQUEST_ID \
        -H "Authorization: $IAM_TOKEN" \
        -H "Content-Type: application/json" \
        -d '{"action": "APPROVE"}
    ```
    {: codeblock}

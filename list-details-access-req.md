---

copyright:
  years: 2022, 2025
lastupdated: "2025-05-08"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Listing and getting details of access requests
{: #list-access-req}

List all access requests and get the details of an access request in your linked zone by using the UI, CLI, or API.
{: shortdesc}

## Listing all access requests in the console
{: #ui-list-access-req}
{: ui}

To list all access requests using the UI, take the following steps:

1. Navigate to the **Zones** section of your {{site.data.keyword.dns_short}} instance, then select the **DNS zones** tab, which shows a list of all zones.
1. Check the **Status** column for pending requests.

## Getting the details of an access request in the console
{: #ui-get-details-access-req}

To get the details of an access request using the UI, take the following steps:

1. Navigate to the **Zones** section of your {{site.data.keyword.dns_short}} instance, then select the **DNS zones** tab.
1. Click the link in the **Zone name** column of the linked zone you want to view.

## Listing all access requests from the CLI
{: #cli-list-access-req}
{: cli}

To list an access request using the CLI, run the following command:

```sh
ibmcloud dns cross-account access-request ZONE_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **ZONE_ID** is the ID of the owner's zone.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by `ibmcloud dns instance-target INSTANCE` is used.
* **--output value** specifies the output format. Currently, `json` is the only supported format.

## Getting the details of an access request from the CLI
{: #cli-get-details-access-req}

To get the details of an access request using the API, run the following command:

```sh
ibmcloud dns cross-account access-request ZONE_ID REQUEST_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **ZONE_ID** is the ID of the owner's zone.
* **REQUEST_ID** is the ID of the access request.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by `ibmcloud dns instance-target INSTANCE` is used.
* **--output value** specifies the output format. Currently, `json` is the only supported format.

## Listing access requests with the API
{: #api-list-access-req}
{: api}

To list all access requests using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `INSTANCE_ID`, which is the unique identifier of a service instance.
    * `DNSZONE_ID` which is the unique identifier of a linked zone.
    * `IAM_TOKEN`, which is the IAM authorization token.
1. When all variables are initiated, list the access requests:

    ```sh
    curl -X GET \
        https://api.dns-svcs.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/access_requests \
        -H "Authorization: $IAM_TOKEN"
    ```
    {: codeblock}


## Getting the details of an access request with the API
{: #api-get-details-access-req}

To get the details of an access request using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `INSTANCE_ID`, which is the unique identifier of a service instance.
    * `DNSZONE_ID` which is the unique identifier of a linked zone.
    * `ACCESS_REQUEST_ID` which is the  unique identifier of an access request.
    * `IAM_TOKEN`, which is the IAM authorization token.
1. When all variables are initiated, get the details of the the access request:

    ```sh
    curl -X GET \
        https://api.dns-svcs.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/access_requests/$ACCESS_REQUEST_ID \
        -H "Authorization: $IAM_TOKEN"
    ```
    {: codeblock}

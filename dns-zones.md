---

copyright:
  years: 2019
lastupdated: "2019-11-25"

keywords: dns-svcs, DNS Services, Private DNS

subcollection: dns-svcs

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:tip: .tip}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:download: .download}


# Managing DNS zones
{:#managing-dns-zones}

You must have an {{site.data.keyword.dns_full}} instance before managing DNS zones. Refer to [Create a {{site.data.keyword.dns_short}} instance](/docs/dns-svcs?topic=dns-svcs-getting-started#step-1-create-dns-services-instance) for more information.

## Using the {{site.data.keyword.cloud_notm}} console
{: #managing-dns-zones-ui}
DNS zones can be managed through the {{site.data.keyword.cloud}} console, or the API. The following sections cover the console usage.
{:shortdesc}

### Creating a DNS zone
{:#create-dns-zone-ui}

  1. From the Resource page, select the desired {{site.data.keyword.dns_short}} instance.
  2. Click the **Create Zone** button on the **DNS Zones** page.
  3. In the panel that appears, enter your zone name in the **Name** field. Optionally, enter **Label** and **Description** fields.
  5. Click **Create Zone**.

If the zone creation is successful, you are directed to the Zone Details page.

If the zone creation is unsuccessful, an error notification appears with information about what caused the error.

### Editing a DNS zone
{:#edit-dns-zone-ui}

  1. From the **DNS Zones** page, select your zone. **Label** and **Description** options appear.
  2. Click the edit icon for **Label**, then enter the label and click **Save**.
  3. Click the edit icon for **Description**, then enter the description and click **Save**.

### Deleting a DNS zone
{:#delete-dns-zone-ui}

  1. From the **DNS Zones** page, click the delete icon from the row for the zone you wish to delete. A confirmation dialog appears.
  2. Click **Delete** button.

## Using the API
{: #managing-dns-zones-api}

First store the API endpoint in a variable so you can use it in API requests without having to type the full URL. For example, to store the production endpoint in a variable, run this command:

```bash
dnssvcs_endpoint=https://api.dns-svcs.cloud.ibm.com
```
{:pre}

To verify that this variable was saved, run `echo $DNSSVCS_ENDPOINT` and make sure the response is not empty.

### Creating a DNS zone
{: #create-dns-zone-api}

Create a new zone by using the following `curl` command:

**Request**

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones \
  -H "Authorization: $TOKEN" \
  -d '{
	"name": "example.com",
	"description": "Example zone"
}'
```
{:pre}

**Response**

```json
{
    "success": true,
    "result": {
        "id": "ed10e4b2-8a64-4afa-a4e2-9e60a766d079",
        "created_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
        "modified_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
        "instance_id": "1a34bda8-9c94-4232-bea7-7df163b21d23",
        "name": "example.com",
        "description": "Example zone",
        "state": "PENDING_NETWORK_ADD",
        "tag": "example.com:ed10e4b2-8a64-4afa-a4e2-9e60a766d079"
    },
    "errors": [],
    "messages": []
}
```
{:screen}

For future reference, the "id" in response is used as `DNSZONE_ID`. 
{:note}

### Getting a DNS zone
{: #get-dns-zone-api}

Use the following command to get an existing zone. 

**Request**

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID \
  -H "Authorization: $TOKEN"
```
{:pre}

**Response**

```json
{
    "success": true,
    "result": {
        "id": "ed10e4b2-8a64-4afa-a4e2-9e60a766d079",
        "created_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
        "modified_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
        "instance_id": "1a34bda8-9c94-4232-bea7-7df163b21d23",
        "name": "example.com",
        "description": "Example zone",
        "state": "PENDING_NETWORK_ADD",
        "tag": "example.com:ed10e4b2-8a64-4afa-a4e2-9e60a766d079"
    },
    "errors": [],
    "messages": []
}
```
{:screen}

### Updating a DNS zone
{: #update-dns-zone-api}

Use the following command to update an existing zone. You can update the description and label fields. All other fields are read-only.

**Request**

```bash
curl -X PATCH \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID \
  -H 'Content-Type: application/json' \
  -H "Authorization: $TOKEN" \
  -d '{
	  "description": "The DNS zone is used for VPCs in us-east region",
	  "label": "us-east"
}'

```
{:pre}

**Response**

```json
{
  "created_on": "2019-01-01T05:20:00.12345Z",
  "description": "The DNS zone is used for VPCs in us-east region",
  "id": "example.com:2d0f862b-67cc-41f3-b6a2-59860d0aa90e",
  "instance_id": "1407a753-a93f-4bb0-9784-bcfc269ee1b3",
  "label": "us-east",
  "modified_on": "2019-01-01T05:20:00.12345Z",
  "name": "example.com",
  "state": "PENDING_NETWORK_ADD"
}
```
{:screen}


### Listing DNS zones
{: #list-dns-zones-api}

List one or more zones in your domain by using the following `curl` command: 

**Request**

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones \
  -H "Authorization: $TOKEN"
```
{:pre}

**Response**

```json
{
    "success": true,
    "result": [
        {
            "id": "ed10e4b2-8a64-4afa-a4e2-9e60a766d079",
            "created_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
            "modified_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
            "instance_id": "1a34bda8-9c94-4232-bea7-7df163b21d23",
            "name": "example.com",
            "description": "Example zone",
            "state": "PENDING_NETWORK_ADD",
            "tag": "example.com:ed10e4b2-8a64-4afa-a4e2-9e60a766d079"
        }
    ],
    "errors": [],
    "messages": []
}
```
{:screen}

### Deleting a DNS zone
{: #delete-dns-zone-api}

**Request**

```bash
curl -X DELETE \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID \
  -H "Authorization: $TOKEN"
```
{:pre}

**Response**

```json
{
    "success": true,
    "result": {
        "id": "ed10e4b2-8a64-4afa-a4e2-9e60a766d079"
    },
    "errors": [],
    "messages": []
}
```
{:screen}

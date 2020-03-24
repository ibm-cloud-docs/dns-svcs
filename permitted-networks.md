---

copyright:
  years: 2019, 2020
lastupdated: "2020-02-10"

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

# Managing permitted networks
{: #managing-permitted-networks}

This section describes how to manage permitted networks for your {{site.data.keyword.dns_full}} instance.
{:shortdesc}

## Using the IBM Cloud console
{: #managing-permitted-networks-ui}

### Adding permitted networks
{: #adding-permitted-networks-ui}

DNS Services is a global service, therefore you may add permitted networks (for example, a VPC) from any {{site.data.keyword.cloud}} region. This request adds the network to the DNS zone, thereby giving the network access to the zone. You may add up to 10 permitted networks to a DNS zone.

1. Select the desired zone from the table on the DNS Zones page.
1. Select the **Permitted Networks** tab.
1. Click the **Add Network** button.
1. In the panel that appears, select the region of your network from the **Network Region** list menu.
1. Select the desired network from the **Network** list menu that appears.
1. Click **Add Network**.

Adding the same VPC to two DNS zones of the same name is not allowed.
{:note}

### Removing a permitted network
{: #removing-permitted-networks-ui}

From the permitted networks table, click the **Delete** icon. Confirm the delete process in the dialog box that appears.

If a network exists in a zone, you cannot delete the zone until the permitted network is deleted.
{:note}

## Using the API
{: #managing-permitted-networks-api}

First store the API endpoint in a variable so you can use it in API requests without having to type the full URL. For example, to store the production endpoint in a variable, run this command:

```bash
dnssvcs_endpoint=https://api.dns-svcs.cloud.ibm.com
```
{:pre}

To verify that this variable was saved, run **`echo $DNSSVCS_ENDPOINT`** and make sure the response is not empty.

### Adding permitted networks
{: #adding-permitted-networks-api}

A DNS zone's initial state is `PENDING_NETWORK_ADD`, because its permitted network list is empty when the DNS zone is created. When a permitted network is added to the DNS zone's permitted networks, the state changes to `ACTIVE`.

**Parameters**

* DNSZONE_ID: When you create a zone, the DNSZONE_ID is returned in the response as **`id`**.

**Request**

```bash
curl -X POST \
         $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/permitted_networks \
         -H "Authorization: $TOKEN" \
         -d '{
             "type": "vpc",
             "permitted_network":{
                 "vpc_crn":"crn:v1:staging:public:is:us-east:a/0821fa9f9ebcc7b7c9a0d6e9bf9442a4::vpc:b7246cdf-892a-4a6c-8fa9-491a5f585bd0"
             }
         }'
```
{:pre}


**Response**

```json
{
    "id": "b7246cdf-892a-4a6c-8fa9-491a5f585bd0",
    "created_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
    "modified_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
    "permitted_network": {
        "vpc_crn": "crn:v1:staging:public:is:us-east:a/0821fa9f9ebcc7b7c9a0d6e9bf9442a4::vpc:b7246cdf-892a-4a6c-8fa9-491a5f585bd0"
    },
    "type": "vpc",
    "state": "ACTIVE"
}
```
{:pre}

For future requests, the ID in the response is referenced as **`PERMITTED_NETWORK_ID`**.
{:note}

### Retrieve a permitted network
{: #get-permitted-network-api}

Retrieve a specific permitted network from your instance using the permitted network ID.

**Request**

```bash
curl -X GET \
         $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/permitted_networks/$PERMITTED_NETWORK_ID \
         -H "Authorization: $TOKEN"
```
{:pre}

**Response**

```json
{
    "id": "b7246cdf-892a-4a6c-8fa9-491a5f585bd0",
    "created_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
    "modified_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
    "permitted_network": {
        "vpc_crn": "crn:v1:staging:public:is:us-east:a/0821fa9f9ebcc7b7c9a0d6e9bf9442a4::vpc:b7246cdf-892a-4a6c-8fa9-491a5f585bd0"
    },
    "type": "vpc",
    "state": "ACTIVE"
}
```
{:screen}

### Listing permitted networks
{: #list-permitted-networks-api}

List all permitted networks for your DNS zone.

**Request**

```bash
curl -X GET \
         $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/permitted_networks \
         -H "Authorization: $TOKEN"
```
{:pre}

**Response**

```json
{
    "permitted_networks": [
        {
            "id": "b7246cdf-892a-4a6c-8fa9-491a5f585bd0",
            "created_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
            "modified_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
            "permitted_network": {
                "vpc_crn": "crn:v1:staging:public:is:us-east:a/0821fa9f9ebcc7b7c9a0d6e9bf9442a4::vpc:b7246cdf-892a-4a6c-8fa9-491a5f585bd0"
            },
            "type": "vpc",
            "state": "ACTIVE"
        }
    ]
}
```
{:screen}

### Removing a permitted network
{: #removing-permitted-networks-api}

Delete a specific permitted network from your instance, and unlink VPC from a zone.

**Request**

```bash
curl -X DELETE \
         $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/permitted_networks/$PERMITTED_NETWORK_ID \
         -H "Authorization: $TOKEN"
```
{:pre}

**Response**
```json
{
    "id": "b7246cdf-892a-4a6c-8fa9-491a5f585bd0",
    "created_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
    "modified_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
    "permitted_network": {
        "vpc_crn": "crn:v1:staging:public:is:us-east:a/0821fa9f9ebcc7b7c9a0d6e9bf9442a4::vpc:b7246cdf-892a-4a6c-8fa9-491a5f585bd0"
    },
    "type": "vpc",
    "state": "REMOVAL_IN_PROGRESS"
}
```
{:pre}

Removing a permitted network can take up to 5 minutes. You cannot add the VPC back to the DNS zone's permitted network until the removal operation is complete.
{:note}

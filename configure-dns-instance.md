---

copyright:
  years: 2019
lastupdated: "2019-12-12"

keywords: dns, dns-svcs, DNS Services, Private DNS, dns vpc

subcollection: dns-svcs

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Setting up your DNS instance
{: #setting-up-your-dns-instance}

This section describes how to set up a DNS instance, DNS zones, permitted networks, and resource records.
{:shortdesc}

## Using the {{site.data.keyword.cloud_notm}} console
{: #setting-up-your-dns-instance-ui}

### Creating a DNS instance
{: #creating-a-dns-instance}

  1. Open the {{site.data.keyword.cloud_notm}} **Catalog** page.
  2. Select the **Networking** category.
  3. Click the **{{site.data.keyword.dns_short}}** tile.  
     Currently, the default and only available plan is free.
  4. Enter **Service name** and click **Create**.

   You are redirected to the {{site.data.keyword.dns_short}} instance page showing **DNS Zones** information.

### Creating a DNS zone
{: #creating-a-dns-zone}

  1. Navigate to the Resource page and select your {{site.data.keyword.dns_short}} instance.
  2. On the DNS Zones page, click **Create Zone**.
  3. In the Create Zone panel, enter your zone name. Optionally, enter a label and description.
  4. Click **Create Zone** in the panel.

     If the zone is created successfully, you are redirected to the Zone Details page.

### Creating a permitted network
{: #creating-a-dns-permitted-network}

  1. Navigate to the Resource page and select your {{site.data.keyword.dns_short}} instance. Then select your zone.
  2. Click the **Permitted Networks** tab.
  3. Click **Add Network**.
  4. In the Add Network panel, select the region of your VPC from the **Network Region** menu.
  5. Select the VPC from the **Network** menu that appears.
  6. Click **Add Network**.

  This request adds the VPC network to your zone, thereby giving the network access to the zone.

### Creating an "A" resource record
{: #creating-an-a-resource-record}

  1. Navigate to the Resource page and select your {{site.data.keyword.dns_short}} instance. Then select your zone.
  2. On the DNS Details page, click the **DNS Records** tab.
  3. Click **Add Record**.
  4. In the Add Record panel, select the type of DNS record that you want to add from the **Type** menu.

     In this case, select the type **A**.
  5. Enter the required data for the type of DNS record you selected.

     In this case, for type **A**, enter **Name** and **IPv4 Address**.
  6. Click **Add Record** in the panel.

### Verifying the setup
{: #verifying-the-setup}

To verify that your instance, zone, and record are performing correctly, run the following **dig** command:

```dig @161.26.0.7 <Record type> <record name>
```
{:pre}

Example:

```dig @161.26.0.7 A xyz.example.com
```
{:pre}

## Using the API
{: #setting-up-your-dns-instance-api}

### Creating a DNS instance
{: #creating-dns-instance-api}

If your account is enabled for the experimental {{site.data.keyword.dns_short}}, it appears in the [experimental catalog](https://{DomainName}/catalog/labs). You can also navigate directly to the {{site.data.keyword.dns_short}} instance creation by going to the [{{site.data.keyword.dns_short}} catalog entry](https://{DomainName}/catalog/services/dns-services).

See the [{{site.data.keyword.dns_short}} API reference](/docs/dns-svcs?topic=dns-svcs-dns-svcs-api) documentation for more information on using the API.

### Creating a DNS zone
{: #creating-dns-zone-api}

You must create a VPC so that you can link your DNS zone to the VPC.

Store the API endpoint in a variable so you can use it in API requests without having to type the full URL. For example, to store the endpoint in a variable, run this command:

```bash
DNSSVCS_ENDPOINT=https://api.dns-svcs.cloud.ibm.com
```
{:pre}

To verify that this variable is saved, run `echo $DNSSVCS_ENDPOINT` and ensure the response is not empty.

After you gather details about your instance, run the following `curl` command to create a DNS zone:

**Request**

* INSTANCE_ID: GUID of the instance
* TOKEN: IAM OAUTH token

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones \
  -H "Authorization: $TOKEN" \
  -d '{
        "name": "example.com",
        "description": "The DNS zone is used for VPCs in the us-east region",
        "label": "us-east"
  }'
```
{:pre}


**Response**
```json
{
  "id": "example.com:2d0f862b-67cc-41f3-b6a2-59860d0aa90e",
  "created_on": "2019-01-01T05:20:00.12345Z",
  "modified_on": "2019-01-01T05:20:00.12345Z",
  "instance_id": "1407a753-a93f-4bb0-9784-bcfc269ee1b3",
  "name": "example.com",
  "description": "The DNS zone is used for VPCs in the us-east region",
  "state": "pending_network_add",
  "label": "us-east"
}
```
{:screen}

### Creating a permitted network
{: #creating-permitted-network-api}

Private DNS allows name resolution only from a VPC that was added to the DNS zone.

When a DNS zone gets created, its Status is `PENDING_NETWORK_ADD`. To move the zone to `ACTIVE` state, add an entry for your VPC to the zone's permitted network.

By adding your VPC to your zone's permitted network, compute instances on your VPC can access these resource records.

**Request**
```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/acls \
  -H "Authorization: $TOKEN" \
  -d '{
        "type": "vpc",
        "acl_data": {
            "vpc_crn": "crn:v1:staging:public:is:us-east:a/40705ee14536813e2385f26c20be24a5::vpc:ed5e3cdd-8a4f-45ce-bae4-2774cb028caf"
        }
  }'
```
{:pre}

**Response**
```json
{
  "id": "fecd0173-3919-456b-b202-3029dfa1b0f7",
  "created_on": "2019-01-01T05:20:00.12345Z",
  "modified_on": "2019-01-01T05:20:00.12345Z",
  "acl_data": {
    "vpc_crn": "crn:v1:staging:public:is:us-east:a/40705ee14536813e2385f26c20be24a5::vpc:ed5e3cdd-8a4f-45ce-bae4-2774cb028caf"
  },
  "type": "vpc"
}
```
{:screen}

### Creating an "A" resource record
{: #creating-resource-records}

An A Record (Address Record) is a DNS resource record that associates a domain or subdomain to an IPv4 address.

**Request**

* `name`: FQDN, such as `www.example.com` or the host, such as `www`.
* `type`: Type of Record - A, AAAA, SRV, and so on.
* `ip`: IP address for the name.
* `ttl`: Time to live for the resource record.

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
        "name":"www.example.com",
        "type":"A",
        "rdata": {
            "ip":"1.2.6.7"
        },
        "ttl":300
  }'
```
{:pre}

**Response**

```json
{
   "created_on":"2019-09-13 19:56:42.484382585 +0000 UTC",
   "modified_on":"2019-09-13 19:56:42.484382585 +0000 UTC",
   "rtype":"A",
   "ttl":300,
   "name":"www.example.com.testZone.com",
   "id":"A:786c07c7-173e-473b-aa09-c186601a5709",
   "rdata":{
      "ip":"1.2.6.7"
   }
}
```
{:screen}

### Verifying the setup
{: #verifying-the-setup-api}

To verify that your instance, zone, and record are performing correctly, run the following **dig** command:

```dig @161.26.0.7 <Record type> <record name>
```
{:pre}

Example:

```dig @161.26.0.7 A xyz.example.com
```
{:pre}

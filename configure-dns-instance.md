---

copyright:
  years: 2019, 2025
lastupdated: "2025-05-08"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Setting up your {{site.data.keyword.dns_short}} instance
{: #setting-up-your-dns-instance}

Set up a {{site.data.keyword.dns_full}} instance, DNS zones, permitted networks, and resource records by using the UI or API.
{: shortdesc}

## Creating a {{site.data.keyword.dns_short}} instance in the console
{: #creating-a-dns-instance}
{: ui}

1. Open the [{{site.data.keyword.cloud_notm}} **Catalog**](https://{DomainName}/catalog/) page.
1. Select the **Networking** category.
1. Click the **{{site.data.keyword.dns_short}}** tile.
1. Choose a plan.
1. Enter **Service name** and click **Create**.

   You are redirected to the {{site.data.keyword.dns_short}} instance page showing **DNS Zones** information.

You can also navigate directly to the {{site.data.keyword.dns_short}} instance creation by going to the [{{site.data.keyword.dns_short}} catalog entry](https://{DomainName}/catalog/services/dns-services).

## Creating a DNS zone in the console
{: #creating-a-dns-zone}
{: ui}

1. Navigate to the Resource page and select your {{site.data.keyword.dns_short}} instance.
1. On the DNS Zones page, click **Create zone**.
1. In the Create Zone panel, enter your zone name. Optionally, enter a label and description.
1. Click **Create zone** in the panel.
   If the zone is created successfully, you are redirected to the Zone Details page.

## Creating an "A" resource record in the console
{: #creating-an-a-resource-record}
{: ui}

1. Navigate to the Resource page and select your {{site.data.keyword.dns_short}} instance. Then select your zone.
1. On the DNS Details page, click the **DNS Records** tab.
1. Click **Select record action**, and select **Add record** from the list menu.
1. In the Add Record panel, select the type of DNS record that you want to add from the **Type** menu.
   In this case, select the type **A**.
1. Enter the required data for the type of DNS record you selected.
   In this case, for type **A**, enter **Name** and **IPv4 Address**.
1. Click **Add record** in the panel.

## Creating a permitted network in the console
{: #creating-a-dns-permitted-network}
{: ui}

1. Navigate to the Resource page and select your {{site.data.keyword.dns_short}} instance. Then select your zone.
1. Click the **Permitted Networks** tab.
1. Click **Add network**.
1. In the Add Network panel, select the region of your VPC from the **Network Region** menu.
1. Select the VPC from the **Network** menu that appears.
1. Click **Add network**.

   This request adds the VPC network to your zone, thereby giving the network access to the zone.

## Verifying the setup
{: #verifying-the-setup}

To verify that your instance, zone, and record are performing correctly, run the following **dig** command:

```sh
dig @161.26.0.7 <Record type> <record name>
```
{: pre}

Example:

```sh
dig @161.26.0.7 A xyz.example.com
```
{: codeblock}

## Creating a {{site.data.keyword.dns_short}} instance with the API
{: #creating-dns-instance-api}
{: api}

See the [create a new resource instance](/apidocs/resource-controller/resource-controller#create-resource-instance) documentation for the Resource Controller API. Note that the `resource_group` and `resource_plan_id` must be set. Each account can have multiple resource groups, and each resource group has a unique ID.

Set the variables as follows to create an instance of the standard plan:

```sh
"resource_plan_id": "2c8fa097-d7c2-4df2-b53e-2efb7874cdf7",
```
{: codeblock}

See the [Resource Controller API reference](/apidocs/resource-controller/resource-controller) documentation for more information on using the API.

Command lines for instances are using resource controller API, not DNS APIs. These commands are equivalent to commands `ibmcloud resource service-instance`, which provide convenience for DNS users to manage {{site.data.keyword.dns_short}} instances.
{: note}

## Creating a DNS zone with the API
{: #creating-dns-zone-api}
{: api}

You must create a VPC so that you can link your DNS zone to the VPC.

Store the API endpoint in a variable so you can use it in API requests without having to type the full URL. For example, to store the endpoint in a variable, run this command:

```bash
DNSSVCS_ENDPOINT=https://api.dns-svcs.cloud.ibm.com
```
{: pre}

To verify that this variable is saved, run `echo $DNSSVCS_ENDPOINT` and ensure the response is not empty.

After you gather details about your instance, run the following `curl` command to create a DNS zone:

### Request
{: #api-create-dns-zone-request}
{: api}

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
{: pre}


### Response
{: #api-create-dns-zone-response}
{: api}

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
{: codeblock}

## Creating a permitted network with the API
{: #creating-permitted-network-api}
{: api}

{{site.data.keyword.dns_short}} allows name resolution only from a VPC that was added to the DNS zone.

When a DNS zone gets created, its Status is `PENDING_NETWORK_ADD`. To move the zone to `ACTIVE` state, add an entry for your VPC to the zone's permitted network.

By adding your VPC to your zone's permitted network, compute instances on your VPC can access these resource records.

### Request
{: #api-create-pm-request}
{: api}

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
{: pre}

### Response
{: #api-create-pm-response}
{: api}

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
{: codeblock}

## Creating an "A" resource record with the API
{: #creating-resource-records}
{: api}

An A Record (Address Record) is a DNS resource record that associates a domain or subdomain to an IPv4 address.

### Request
{: #create-resource-records-request}
{: api}

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
{: pre}

### Response
{: #create-resource-records-response}
{: api}

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
{: codeblock}

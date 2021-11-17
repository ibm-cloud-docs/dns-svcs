---
copyright:
  years: 2019, 2021
lastupdated: "2021-03-03"

keywords: dns-svcs, DNS Services, Private DNS

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with {{site.data.keyword.dns_full_notm}}
{: #getting-started}

{{site.data.keyword.dns_full}} provides private DNS to Virtual Private Cloud (VPC) users. Private DNS zones are resolvable only on {{site.data.keyword.cloud_notm}}, and only from explicitly [permitted networks](/docs/dns-svcs?topic=dns-svcs-dns-concepts#permitted-networks) in an account. To get started, create a {{site.data.keyword.dns_short}} instance using the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

## Before you begin
{: #before-you-begin-getting-started}

To use {{site.data.keyword.dns_short}}, you must have at least one virtual server instance (VSI) in a VPC in the {{site.data.keyword.cloud_notm}}. If you do not have one, learn how to [get started with Virtual Private Cloud](/docs/vpc?topic=vpc-getting-started).

While the private DNS resolvers are required to resolve private DNS names, they also resolve public DNS names if the request is for a name that is not defined to be in a private DNS zone.
{: note}

## Step 1: Create a {{site.data.keyword.dns_short}} instance
{: #step-1-create-dns-services-instance}

1. Open the {{site.data.keyword.cloud_notm}} catalog page and select **Networking**.
1. Click the **{{site.data.keyword.dns_short}}** tile.
1. In the **Create** tab, select a pricing plan and optionally update the default the service name and resource group.
1. Click **Create**.

## Step 2: Add a DNS zone
{: #step-2-add-dns-zone}

1. From the resource page, select the {{site.data.keyword.dns_short}} instance.
1. Click the **Create zone** button on the DNS Zones page.
1. Enter a fully qualified domain name for the zone and optionally add a label and description. The maximum number of levels a domain name can have is 5. You can define subdomains within the zone later.
1. Click **Create zone**.
1. If the zone creation is successful, you are directed to the zone details page.


## Step 3: Add a VPC as a permitted network to the DNS zone
{: #step-3-add-vpc-as-permitted-network-to-dns-zone}

1. Select the zone from the table on the DNS Zones page.
1. Select the **Permitted networks** tab.
1. Click **Add network**.
1. Select the region from the **Region** drop-down menu to see the list of networks in that region.
1. Select the network from the list and click **Add network**.

Resources in the VPC can resolve records associated with the DNS zone (see [Step 4](#step-4-add-dns-resource-records) to add records to the DNS zone). The DHCP server returns the DNS servers (`161.26.0.7` and `161.26.0.8`) provided by {{site.data.keyword.dns_short}} in its responses. If you have DHCP disabled on a server in the VPC, it is your responsibility to configure the DNS server IP addresses statically on that server, according to your operating system's documentation.

## Step 4: Add DNS resource records
{: #step-4-add-dns-resource-records}

1. Select the zone from the table on the DNS Zones page.
1. Select the **DNS records** tab.
1. Click **Add record**.
1. In the panel that appears, select the type of DNS record you are adding from the **Type** menu.
1. Input the required data for the type of DNS record selected.
1. Click **Add record**.

## Step 5: Verify that DNS name resolution works from the VPC
{: #step-5-test-if-the-dns-name-resolution-works}

Test whether the zone resolution works using a **`dig`** from the VSI on your VPC. The following command should yield a resolution as the result.

```shell
dig www.example.com
```
{: pre}

## Next Steps
{: #getting-started-api}

Follow the steps in these detailed guides to use the API for:
- [Creating a DNS zone](/docs/dns-svcs?topic=dns-svcs-managing-dns-zones#create-dns-zone-api)
- [Managing permitted networks](/docs/dns-svcs?topic=dns-svcs-managing-permitted-networks#managing-permitted-networks-api)
- [Import a DNS zone file](/docs/dns-svcs?topic=dns-svcs-managing-dns-zones#import-resource-records-api)
- [Managing DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records#managing-dns-records-api)

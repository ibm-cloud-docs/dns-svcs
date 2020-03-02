---
copyright:
  years: 2019, 2020
lastupdated: "2020-2-24"

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

# Getting started with {{site.data.keyword.dns_full_notm}}
{: #getting-started}

{{site.data.keyword.dns_full}} (currently in Beta release) provides private DNS to Virtual Private Cloud (VPC) users. Private DNS zones are resolvable only on {{site.data.keyword.cloud_notm}}, and only from explicitly permitted networks such as VPCs in an account.

Create a {{site.data.keyword.dns_short}} instance using the {{site.data.keyword.cloud_notm}} console.
{:shortdesc}

To get started:

1. Create a {{site.data.keyword.dns_short}} instance.
1. Add a DNS zone.
1. Add VPC as a permitted network to the DNS zone.
1. Add DNS resource records to the DNS zone.
1. Ensure that virtual server instances in the VPC use the private DNS resolvers.
1. Test if the DNS name resolution works from the VPC.

These steps enable you to query any record added to the zone from the permitted VPC network.

## Before you begin
{:#before-you-begin-getting-started}

1. To use {{site.data.keyword.dns_short}}, you must have a VPC in the {{site.data.keyword.cloud_notm}}. Follow this link to [Create a VPC](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console) using the {{site.data.keyword.cloud_notm}} console, or [create a VPC using the CLI](/docs/vpc?topic=vpc-creating-a-vpc-using-cli).
1. Create a virtual server instance (VSI) within the VPC.
1. The VSI on the VPC must be configured to use the private DNS resolvers (161.26.0.7, 161.26.0.8). For example, on some Linux distributions, this is done by editing the file `/etc/resolv.conf`. It may also be possible to override the default DNS resolvers using `cloud-init` during server boot up. Consult your operating system manuals for more information. When editing configuration files, ensure that you keep a backup copy of the existing configuration in case it needs to be restored.

While the private DNS resolvers are required to resolve private DNS names, they also resolve public DNS names if the request is for a name that is not defined to be in a private DNS zone for the originating network/VPC.
{:note}

## Using the {{site.data.keyword.cloud_notm}} console

### Creating a {{site.data.keyword.dns_short}} instance
{: #step-1-create-dns-services-instance}

1. Open the {{site.data.keyword.cloud_notm}} Catalog page and select **Networking**.
1. Click the **{{site.data.keyword.dns_short}}** tile to create a **{{site.data.keyword.dns_short}}** instance.

Currently, the default and only available plan is free.
{: note}

### Adding a DNS zone
{: #step-2-add-dns-zone}

1. From the resource page, select the desired {{site.data.keyword.dns_short}} instance.
1. Click the **Create Zone** button on the DNS Zones page.
1. The label and description are optional fields.
1. Click **Create Zone**.
1. If the zone creation is successful, you will be directed to the Zone Details page.

   For example, a zone name could be `example.com`. Note that only 2-level zones are supported as zone names (for example, `example.com` is permitted, but `subdomain.example.com` is not. You can define subdomains within the zone after creation).

## Adding VPC as a permitted network to the DNS zone
{:#step-3-add-vpc-as-permitted-network-to-dns-zone}

1. Select the desired zone from the table on the DNS Zones page.
1. Select the **Permitted Networks** tab.
1. Click **Add Network**.
1. Select the VPC from the **Network** menu.
1. Click **Add Network**.

This request adds the VPC network to the zone, which gives the network access to the zone.

## Adding DNS resource records
{:#step-4-add-dns-resource-records}

1. Select the zone from the table on the DNS Zones page.
1. Select the **DNS Records** tab.
1. Click **Add Record**.
1. In the panel that appears, select the type of DNS record you are adding add from the **Type** menu.
1. Input the required data for the type of DNS record selected.
1. Click **Add Record**.

## Testing if the DNS name resolution works from the VPC
{:#step-5-test-if-the-dns-name-resolution-works}

Test whether the zone resolution works using a **`dig`** from the VSI on your VPC. The following command should yield a resolution as the result.

```shell
dig www.example.com
```
{:pre}

## Using the API
{: #getting-started-api}

Follow the steps in these detailed guides to use the API for:
- [Creating a zone](/docs/dns-svcs?topic=dns-svcs-managing-dns-zones-api#managing-dns-zones-api).
- [Managing permitted networks](/docs/dns-svcs?topic=dns-svcs-managing-permitted-networks-api#managing-permitted-networks-api).
- [Managing DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records-api#managing-dns-records-api).

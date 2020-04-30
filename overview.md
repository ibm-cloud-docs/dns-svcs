---

copyright:
  years: 2019, 2020
lastupdated: "2020-04-17"

keywords: dns-svcs, DNS Services, Private DNS, split horizons

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

# About {{site.data.keyword.dns_short}}
{: #about-dns-services}

To better understand {{site.data.keyword.dns_full}}, it helps to know more about DNS in general.
{:shortdesc}

## DNS overview
{: #dns-overview}

Computers on a network can find one another by IP addresses. To make it easier to work within a computer network, people can use a Domain Name System (DNS) to associate human-friendly domain names with IP addresses, similar to a phonebook. A DNS can also associate other information beyond just computer network addresses to domain names.

That way, people can use human friendly domain names instead of obscure, hard-to-remember, machine-oriented data.

## {{site.data.keyword.dns_short}} overview
{: dns-services-overview}

{{site.data.keyword.dns_short}} allow you to
  * Create private DNS zones that are collections for holding domain names.
  * Create DNS resource records under these DNS zones.
  * Specify access controls used for the DNS resolution of resource records on a zone-wide level.

{{site.data.keyword.dns_short}} also maintains its own worldwide set of DNS resolvers. Instances that are provisioned under {{site.data.keyword.cloud_notm}} on an {{site.data.keyword.cloud_notm}} network can use resource records that are configured through
{{site.data.keyword.dns_full_notm}} by querying {{site.data.keyword.dns_short}} resolvers.

Resource records and zones that are configured through {{site.data.keyword.dns_short}} are
  * Separated from the wider, public DNS and their publicly accessible records.
  * Hidden from machines outside of and not part of the {{site.data.keyword.cloud_notm}} private network.
  * Accessible only from machines that you authorize on the {{site.data.keyword.cloud_notm}} private network.
  * Resolvable only via the resolvers provided by the service.



## Resolving DNS names with {{site.data.keyword.dns_short}}
{: #resolving-dns-names-with-dns-services}

![Diagram of DNS services overview](images/dns-svcs-overview.png "Diagram of {{site.data.keyword.dns_short}} overview"){: caption="Figure 1. A diagram of {{site.data.keyword.dns_short}} workflow" caption-side="bottom"}


As an example, consider that a DNS zone `example.com` is created in your DNS instance, and a resource record for `www` has been defined as shown in Figure 1. Also consider that a VPC 1 has been added to the DNS zone as a permitted network.

When the {{site.data.keyword.dns_short}} server receives a name resolution request for `www.example.com` from a client in VPC 1, the {{site.data.keyword.dns_short}} resolver determines that the request originated from a VPC that is a permitted network for the `example.com` DNS zone, and resolves the name `www.example.com` to the IP `10.0.0.1`.

If the name resolution request for `www.example.com` originated from a client in VPC 2 that is _not_ added as a permitted network to `example.com`, the request is forwarded to a public DNS server, and the response from public DNS server is returned to the VPC client. The scenario is referred to as a Split Horizon, where the same hostname, which is defined in both a private DNS zone and a public DNS zone, can be resolved to different IPs depending on where the DNS name resolution request originated.

{{site.data.keyword.dns_short}} ensures a level of privacy for information that is specified in your zones and resource records.

{{site.data.keyword.dns_short}} is private only. For provisioning and configuring DNS records for public DNS resolution, refer to [{{site.data.keyword.cis_full_notm}}](/docs/cis?topic=cis-about-ibm-cloud-internet-services-cis) ({{site.data.keyword.cis_short_notm}}).
{: note}

## Limits
{: #limits}

{{site.data.keyword.dns_short}} has limits in some areas, which are noted in the following table.

|Item| Limitation|
|----|-----------|
|DNS zones |10 per service instance|
|DNS records| 3500 per DNS zone|
|Permitted networks| 10 per DNS zone|

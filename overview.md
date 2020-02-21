---

copyright:
  years: 2019, 2020
lastupdated: "2020-02-21"

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

# About {{site.data.keyword.dns_short}}
{: #about-dns-services}

To better understand {{site.data.keyword.dns_full}}, it helps to know more about DNS in general.
{:shortdesc}

## DNS overview
{: #dns-overview}

Computers on a network can find one another by IP addresses. To make it easier to work within a computer network, people can use a Domain Name System (DNS) to associate human-friendly domain names with IP addresses, similar to a phonebook. A DNS can also associate other information beyond just computer network addresses to domain names.

That way, people can use human friendly domain names instead of obscure, hard-to-remember, machine-oriented data.

## {{site.data.keyword.dns_short}}
{: dns-services-overview}

{{site.data.keyword.dns_short}} allow you to:
  * Create DNS zones that are collections for holding domain names.
  * Create DNS resource records under these zones.
  * Specify access controls used for the DNS resolution of resource records on a zone-wide level.

{{site.data.keyword.dns_short}} also maintains its own worldwide set of DNS resolvers. Computer machines provisioned under {{site.data.keyword.cloud_notm}} on an {{site.data.keyword.cloud_notm}} network can use resource records configured through IBM Cloud DNS Services by querying {{site.data.keyword.dns_short}} resolvers.

Resource records and zones configured through {{site.data.keyword.dns_short}} are:
  * Separated from the wider, public DNS and their publicly accessible records.
  * Hidden from machines outside of and not part of the {{site.data.keyword.cloud_notm}} network.
  * Accessible only from machines that you authorize on the {{site.data.keyword.cloud_notm}} network.
  * Resolvable only via the resolvers provided by the service.


![Diagram of DNS services overview](images/dns-svcs-overview.png "Diagram of {{site.data.keyword.dns_short}} overview"){: caption="Figure 1. A diagram of {{site.data.keyword.dns_short}} workflow" caption-side="bottom"}


{{site.data.keyword.dns_short}} ensures a level of privacy for information specified in your zones and resource records.

{{site.data.keyword.dns_short}} is private only. For provisioning and configuring DNS records for public DNS resolution, refer to [{{site.data.keyword.cis_full_notm}}](/docs/cis?topic=cis-about-ibm-cloud-internet-services-cis) ({{site.data.keyword.cis_short_notm}}).
{: note}

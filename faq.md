---

copyright:
  years: 2020
lastupdated: "2020-03-10"

keywords: dns-svcs, DNS Services, Private DNS, FAQ, frequently asked questions

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
{:faq: data-hd-content-type='faq'}
{:generic: data-hd-programlang="generic"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:download: .download}

# FAQs
{: #frequently-asked-questions}

Have a question about {{site.data.keyword.dns_full}}? Review frequently asked questions, which provide answers to provisioning concerns, application access, and other common inquiries.
{:shortdesc}

## How is private DNS different from public DNS?
{: faq}

Private DNS permits name resolution only from permitted VPCs within your {{site.data.keyword.cloud}} account. The DNS zone is not resolvable on the internet.

## Can I manage publicly available DNS records with this service?
{: faq}

No, {{site.data.keyword.dns_short}} only offers private DNS at the moment. Use [{{site.data.keyword.cis_short_notm}}](/docs/cis?topic=cis-getting-started#getting-started) for public DNS.

## Is DNSSec supported with zones managed by {{site.data.keyword.dns_short}}?
{: faq}

DNSSec allows resolvers to cryptographically verify the data received from authoritative servers. {{site.data.keyword.dns_short}} resolvers support DNSSec for public domains, for which requests are forwarded to public resolvers that support DNSSec. For private zones, since the authority is within {{site.data.keyword.cloud_notm}}, records are fetched using secure protocols, and are guaranteed to have the same level of privacy and security that DNSSec provides for public zones.

## Is {{site.data.keyword.dns_short}} regional or global?
{: faq}

{{site.data.keyword.dns_short}} is a global service and can be used from permitted networks in any {{site.data.keyword.cloud_notm}} region.

## How do I update my Virtual Server Instance to use Private DNS for name resolution?
{: faq}

This is operating system specific. For example, on some Linux distributions the `/etc/resolv.conf` file contains the IP address of the DNS resolver. This file should be updated with the IP address of the Private DNS name servers, `161.26.0.7` and `161.26.0.8`. The configuration can also be updated through Cloud Init, where supported. Consult your operating system manuals for instructions on how to update DNS resolvers. See [Detailed steps](/docs/dns-svcs?topic=dns-svcs-updating-dns-resolver) to learn how to update configuration to use Private DNS Resolvers, for different distros.

## When creating a DNS zone, what is the purpose of the `Label` field?
{: faq}

A given instance can have multiple DNS zones with the same name. The label helps to differentiate zones with name collisions.

## How many private zones are supported?
{: faq}

{{site.data.keyword.dns_short}} supports 10 private zones per service instance.

## How many permitted networks are supported?
{: faq}

{{site.data.keyword.dns_short}} supports 10 permitted networks per DNS zone.

## How many DNS records are supported?
{: faq}

{{site.data.keyword.dns_short}} supports 3500 DNS records per DNS zone.

## How do I delete my {{site.data.keyword.dns_short}} instance?
{: faq}

To delete a {{site.data.keyword.dns_short}} instance, 
  - Navigate to the Resource List in the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}/){: new_window}.
  - Click the "overflow" menu ![overflow menu icon](../../icons/actions-icon-vertical.svg "Overflow menu icon") in the final column and select "Delete".

## Why can't I delete a {{site.data.keyword.dns_short}} instance?
{: faq}

If a DNS zone has been added to the {{site.data.keyword.dns_short}} instance, the instance cannot be deleted.

## Why can't I delete a DNS zone?
{: faq}

If a network has been added to a zone, the zone cannot be deleted until the permitted network is deleted from the zone.

## What happens if I delete my VPC?
{: faq}

If the VPC is deleted, the corresponding permitted network will also be deleted from the DNS zones of your instance.


## What do the different zone states mean?
{: faq}

The zone states definitions are as follows.
* **Pending**: When a DNS zone is added to the instance it will be in `Pending`. In this state Resource Records can be added, deleted or updated. Since the zone does not have any permitted networks, the zone will not be served by the resolvers in any region.
  * **Active**: When a domain has one or more permitted networks added then the domain state changes to `ACTIVE` and the domain will be served by the resolver from all the regions.
  * **Disabled**: In this state the zone will not be served and all control path operations will be disabled except deleting the zone.

## Can I use any name for the zone?
{: faq}

In general, yes, you can use any name for the zone. Certain IBM-owned or IBM-specific DNS zone names are restricted, in other words, they can't be created in Private DNS. See [Restricted DNS zone names](/docs/dns-svcs?topic=dns-svcs-managing-dns-zones#restricted-dns-zone-names) for the complete list. The zone names must be 2-level deep (for example, `example.com`). After the zone has been added, hostnames within the zone can be multiple levels deep, depending on your needs (for example, you can add records for `hostname.example.com`, or `hostname.subdomain.example.com`, and so on).

## Can I create two DNS zones with the same name?
{: faq}

Creating two DNS Zones with the same name is allowed. Use label and description to differentiate between the two.

## Can I add the same permitted network (for example, a VPC) to two DNS zones of the same name?
{: faq}

No, adding the same permitted network (for example, a VPC) to two DNS zones of the same name is not allowed.


## What are the authoritative servers for the private DNS zones? Can I resolve the private DNS zones iteratively?
{: faq}

Unlike public DNS zones, {{site.data.keyword.dns_short}} does not expose authoritative servers for private DNS zones. Clients must send their recursive DNS queries to the DNS resolvers provided by the service. The service does not allow iterative resolution of private DNS zones.

## Can I create a DNS zone with same name as a Public DNS zone?
{: faq}

{{site.data.keyword.dns_short}} allows creating a private DNS zone that can have the same name as the public DNS zone. See a [detailed explanation](/docs/dns-svcs?topic=dns-svcs-use-cases#using-dns-services-with-split-horizon-capabilities) of this scenario, referred to as Split Horizon.

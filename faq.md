---

copyright:
  years: 2020
lastupdated: "2020-11-16"

keywords: 

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
{:support: data-reuse='support'}
{:generic: data-hd-programlang="generic"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:download: .download}

# FAQs
{: #frequently-asked-questions}

Have a question about {{site.data.keyword.dns_full}}? Review frequently asked questions, which provide answers to provisioning concerns, application access, and other common inquiries.
{:shortdesc}

## How do I create my own private DNS zone using {{site.data.keyword.dns_short}}?
{:#private-zone} {: faq} 

To create your own private DNS zone using {{site.data.keyword.dns_short}}, take the following steps.
  1. Create a VPC instance.
  1. Create a {{site.data.keyword.dns_short}} instance.
  1. Add a DNS zone to the {{site.data.keyword.dns_short}} instance.
  1. Designate the VPC instance as a permitted network for the DNS zone.
  1. Add a DNS Resource Record to the DNS zone.
  1. Verify name resolution of the DNS Resource Record works from within the VPC.

## How is {{site.data.keyword.dns_short}} different from public DNS?
{:#not-for-public} {: faq}

{{site.data.keyword.dns_short}} permits name resolution only from permitted VPCs within your {{site.data.keyword.cloud}} account. The DNS zone is not resolvable from the internet.

## Can I manage publicly available DNS records with this service?
{: faq}

No, {{site.data.keyword.dns_short}} only offers private DNS at the moment. Use [{{site.data.keyword.cis_short_notm}}](/docs/cis?topic=cis-getting-started#getting-started) for public DNS.

## Is DNSSec supported with zones managed by {{site.data.keyword.dns_short}}?
{: faq}

DNSSec allows resolvers to cryptographically verify the data received from authoritative servers. {{site.data.keyword.dns_short}} resolvers support DNSSec for public domains, for which requests are forwarded to public resolvers that support DNSSec. For private zones, since the authority is within {{site.data.keyword.cloud_notm}}, records are fetched using secure protocols, and are guaranteed to have the same level of privacy and security that DNSSec provides for public zones.

## Is {{site.data.keyword.dns_short}} regional or global?
{: faq}

{{site.data.keyword.dns_short}} is a global service and can be used from permitted networks in any {{site.data.keyword.cloud_notm}} region.

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
{: support}

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
{: support}

In general, yes, you can use any name for the zone. Certain IBM-owned or IBM-specific DNS zone names are restricted, in other words, they can't be created in {{site.data.keyword.dns_short}}. See [Restricted DNS zone names](/docs/dns-svcs?topic=dns-svcs-managing-dns-zones#restricted-dns-zone-names) for the complete list.

## Can I create two DNS zones with the same name?
{: faq}

Creating two DNS Zones with the same name is allowed. Use label and description as described in the following steps to differentiate between the two.
 1. Create an instance of {{site.data.keyword.dns_short}}.
 2. Create a DNS zone for each environment (for example, production, staging, development, testing). When creating the zone, be sure to include a description indicating what environment the zone is for. The zone name is the same for each zone (for example, `testing.com`).
    A single {{site.data.keyword.dns_short}} instance can only contain 10 zones.
    {: note}
 3. Add a zone to the instance of {{site.data.keyword.dns_short}}.
 4. In each respective zone, add specific VPCs as permitted networks. For example, for a development VPC, create a permitted network with the development VPC ID in the DNS zone for the development environment.
    While duplicate zone names are allowed in an account, duplicate zones cannot be associated with a single permitted network.
    {: note}
 5. The result is that traffic from the development VPC only sees records from the development DNS zone and similarly for all the other environments. This way, you can use the same zone name in all environments, with the results tailored to each respective environment.


## Can I add the same permitted network (for example, a VPC) to two DNS zones of the same name?
{: faq}

No, adding the same permitted network (for example, a VPC) to two DNS zones of the same name is not allowed.


## What are the authoritative servers for the {{site.data.keyword.dns_short}} zones? Can I resolve the private DNS zones iteratively?
{: faq}

Unlike public DNS zones, {{site.data.keyword.dns_short}} does not expose authoritative servers for private DNS zones. Clients must send their recursive DNS queries to the DNS resolvers provided by the service. {{site.data.keyword.dns_short}} does not allow iterative resolution of private DNS zones.

## Can I create a DNS zone with same name as a Public DNS zone?
{: faq}
{: support}

{{site.data.keyword.dns_short}} allows creating a private DNS zone that can have the same name as the public DNS zone. See a [detailed explanation](/docs/dns-svcs?topic=dns-svcs-about-dns-services#resolving-dns-names-with-dns-services) of this scenario, referred to as Split Horizon.


## Are there any limits on global load balancer usage?
{:#load-balancer} {:faq}

See [Global load balancers limitations](/docs/dns-svcs?topic=dns-svcs-global-load-balancers#glb-ki) for more information on global load balancer usage.

## What types of health checks are supported?
{:faq}

HTTP and HTTPS health checks are currently supported.

## What regions can I use for health check monitoring?
{:faq}

Health checks are currently supported in the following regions:
* Dallas
* Washington, D.C.
* Frankfurt
* London
* Tokyo

## How can I disable health check monitoring to the origins? 
{:faq}

You can disable health check monitoring by disabling the origin.

## How do I upgrade my plan from free to standard?
{: faq}

 1. Navigate to the Resource List in the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}/){: new_window}.
 1. Select the instance of {{site.data.keyword.dns_short}} you want to upgrade.
 1. Select **Plan** from the navigation menu.
 1. Select **Standard DNS** from the plan table.
 1. Click **Save** and then click **OK** when prompted to verify 'Are you sure that you want to change plans?'.

See [Update DNS Services instances](/docs/dns-svcs?topic=dns-svcs-cli-plugin-dns-services-cli-commands#update-DNS-services-instance) to update to the standard plan using the command-line interface.

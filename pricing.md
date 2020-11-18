---

copyright:
  years: 2020
lastupdated: "2020-11-18"

keywords: 

subcollection: dns-svcs

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# {{site.data.keyword.dns_short}} pricing
{: #pricing}

Pricing for {{site.data.keyword.dns_full}} follows.
{:shortdesc}

## Standard
{: #standard-plan}
  * One DNS zone and one million DNS queries are included in an account.
  * Each instance can have up to 10 DNS zones.
  * Each DNS zone can have up to 10 VPC networks.
  * Each DNS zone can have up to 3500 DNS records.
  * Multi-tiered

### DNS Zones
{: #zones-pricing}

The standard price is $0.50 USD/month per DNS zone. If an instance does not have the zone for the whole month, the price of the instance's zone is prorated for the portion of the month a zone exists. Zone costs follow the prorated metering model based on usage for the month.

### Tiers
{: #tiers-pricing}

  * For up to 1 billion DNS queries, the price is $0.60 USD per million DNS queries.
  * For over 1 billion DNS queries, the price is $0.30 USD per million DNS queries.

### Global load balancers
{: #glb-pricing}

Global load balancers are billed monthly. If an instance does not have the global load balancer for the whole month, the price of the instance's load balancer is prorated for the portion of the month a load balancer exists. Global load balancer costs follow the prorated metering model based on usage for the month.
  * $25 per global load balancer
  * $25 per origin pool
  * $1 per health check

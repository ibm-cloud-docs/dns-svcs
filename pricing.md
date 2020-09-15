---

copyright:
  years: 2020
lastupdated: "2020-09-11"

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

# {{site.data.keyword.dns_full_notm}} pricing
{: #pricing}

Pricing for {{site.data.keyword.dns_full}} follows.

## Free
{: #free-plan}

One DNS zone and one million DNS queries are free for an account.

## Standard
{: #standard-plan}

  * Each instance can have up to 10 DNS zones.
  * Each DNS zone can have up to 10 VPC networks.
  * Each DNS zone can have up to 3500 DNS records.
  * Multi-tiered

### DNS Zones
{: #zones-pricing}

The standard price is $0.50 USD/month per DNS zone. If an instance does not have the zone for the whole month, the price of the instance's zone is prorated for the portion of the month a zone exists. Zone costs follow the [**dailyproration_avg**](/docs/get-coding?topic=get-coding-meteringintera#metermodel) metering model.

### Tiers
{: #tiers-pricing}

  * For up to 1 billion DNS queries, the price is $0.60 USD per million DNS queries.
  * For over 1 billion DNS queries, the price is $0.30 USD per million DNS queries.

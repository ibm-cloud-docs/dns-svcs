---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-26"

keywords: 

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.dns_short}} pricing
{: #pricing}

Pricing for {{site.data.keyword.dns_full}} follows. For more information, see the [{{site.data.keyword.dns_full}} catalog entry](/catalog/services/dns-services). All prices are in USD.
{: shortdesc}

## Standard
{: #standard-plan}

* One DNS zone and one million DNS queries are included in an account.
* Each instance can have up to 10 DNS zones.
* Each DNS zone can have up to 10 VPC networks.
* Each DNS zone can have up to 3500 DNS records.
* Multi-tiered

### DNS Zones
{: #zones-pricing}

The standard price is $0.50 per month, per DNS zone. If an instance does not have the zone for the whole month, the price of the instance's zone is prorated for the portion of the month a zone exists. Zone costs follow the prorated metering model based on usage for the month.

### Tiers
{: #tiers-pricing}

* For up to 1 billion DNS queries, the price is $0.60 USD per million DNS queries.
* For over 1 billion DNS queries, the price is $0.30 USD per million DNS queries.

### Global load balancers
{: #glb-pricing}

Global load balancers are billed monthly. If an instance does not have the global load balancer for the whole month, the price of the instance's load balancer is prorated for the portion of the month a load balancer exists. Global load balancer costs follow the prorated metering model based on usage for the month. 

* $0.0342 for each global load balancer instance, per hour
* $0.0342 for each pool, per hour 
* $1 per health check

For more information, see [Global load balancer limits](/docs/dns-svcs?topic=dns-svcs-global-load-balancers#glb-ki).

### Custom resolvers
{: #cr-pricing}

Custom resolvers are billed hourly at a rate of $0.125 per resolver location. The price is based on the number of hours the custom resolver exists within the billing cycle. If a custom resolver is removed before a full hour has elapsed, there is no charge for that hour. 

For more information, see [Custom resolver limits](/docs/dns-svcs?topic=dns-svcs-custom-resolver#cr-limits).

#### Custom resolver tiers
{: #cr-tiers}

* For 1-10 external queries, the price is $0.40 per million DNS queries.
* For over 10 external queries, the price is $0.20 per million DNS queries.

---

copyright:
  years: 2020, 2026
lastupdated: "2026-07-02"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for DNS Services
{: #frequently-asked-questions}

Have a question about {{site.data.keyword.dns_full}}? Review frequently asked questions, which provide answers to provisioning concerns, pricing, and other common inquiries.
{: shortdesc}

## Pricing FAQ for DNS Services
{: #frequently-asked-questions-pricing}

### Where do I find cost estimates for {{site.data.keyword.dns_short}}?
{: #where-do-i-find-cost-estimates-for-dns-svcs}
{: faq}
{: support}

You can estimate the cost of a service by using the cost estimator on the provisioning pages for {{site.data.keyword.dns_short}} offerings. For example, log in to the [{{site.data.keyword.dns_short}}](/catalog/services/dns-services) console and click **Estimate costs** in the Summary panel. As you complete the form, cost estimates appear in the Summary side panel.

### What does "Million DNS Queries" refer to?
{: #what-are-million-dns-queries}
{: faq}
{: support}

- "Million DNS Queries" refers to DNS queries answered by the Private DNS Service back-end resolvers (`161.26.0.7`, `161.26.0.8`).
- Private DNS Service back-end resolvers (`161.26.0.7`, `161.26.0.8`) only charge for private zone queries, meaning zones defined and allowed to a VPC by a DNS Service instance. Any queries that are forwarded to public resolvers (`161.26.0.10`, `161.26.0.11`) are not charged.
- By default, a virtual server instance in a VPC without a DNS Service points to public resolvers (`161.26.0.10` and `161.26.0.11`) and is not charged.

### When creating DNS Services from the IBM Cloud Catalog, does a custom resolver location correspond to a single IP on a custom resolver, and does the cost increase if deployed across multiple subnets or zones?
{: #create-dns-cost-per-subnet-zone}
{: faq}

The listed price in the [{{site.data.keyword.cloud_notm}} Catalog](https://{DomainName}/catalog/) is per `Custom Resolver Location`, where location is equivalent to being deployed to a subnet. For example, a custom resolver that is deployed across three subnets would cost three times the rate that is listed in the catalog.

Billing continues even if a custom resolver or its locations are in the `disabled` state because each custom resolver location is a managed appliance that is provisioned for you.
{: note}

### When creating DNS Services from the IBM Cloud Catalog, what does the option Million Custom Resolver External Queries refer to, and are these DNS queries forwarded by forwarding rules?
{: #create-dns-million-custom-resolver-external-queries}
{: faq}

The option **Million Custom Resolver External Queries** refers to queries that result in a cache miss. These queries are not forwarded to the Private DNS resolvers (`161.26.0.7`, `161.26.0.8`).

### Am I charged when queries are sent through a custom resolver and when they are forwarded to on-premises DNS servers by forwarding rules?
{: #dns-charge-per-query}
{: faq}

Yes, you are charged for queries that result in a cache miss and which are not forwarded to the Private DNS resolvers (`161.26.0.7`, `161.26.0.8`).

## General FAQ for DNS Services
{: #frequently-asked-questions-general}

### How do I create my own private DNS zone using {{site.data.keyword.dns_short}}?
{: #private-zone}
{: faq}

To create your own private DNS zone using {{site.data.keyword.dns_short}}, follow these steps:

1. Create a VPC instance.
1. Create a {{site.data.keyword.dns_short}} instance.
1. Add a DNS zone to the {{site.data.keyword.dns_short}} instance.
1. Designate the VPC instance as a permitted network for the DNS zone.
1. Add a DNS resource record to the DNS zone.
1. Verify that that name resolution of the DNS resource record works from within the VPC.

### How is {{site.data.keyword.dns_short}} different from public DNS?
{: #not-for-public}
{: faq}

{{site.data.keyword.dns_short}} allows name resolution only from permitted VPCs within your {{site.data.keyword.cloud}} account. DNS zones are not resolvable from the internet.

### Can I manage publicly available DNS records with this service?
{: #publicly-available-dns-records}
{: faq}

No, {{site.data.keyword.dns_short}} currently offers only private DNS. Use [{{site.data.keyword.cis_short_notm}}](/docs/cis?topic=cis-getting-started#getting-started) for public DNS.

### Is DNSSec supported with zones managed by {{site.data.keyword.dns_short}}?
{: #dnssec-supported-with-zones}
{: faq}

DNSSec allows resolvers to cryptographically verify the data received from authoritative servers. {{site.data.keyword.dns_short}} resolvers support DNSSec for public domains, for which requests are forwarded to public resolvers that support DNSSec. For private zones, since the authority is within {{site.data.keyword.cloud_notm}}, records are fetched by using secure protocols and provide the same level of privacy and security as DNSSec provides for public zones.

### Is {{site.data.keyword.dns_short}} regional or global?
{: #is-dns-svcs-global}
{: faq}

{{site.data.keyword.dns_short}} is a global service and can be used from permitted networks in any {{site.data.keyword.cloud_notm}} region.

### How do I delete my {{site.data.keyword.dns_short}} instance?
{: #delete-dns-svcs-instance}
{: faq}

To delete a {{site.data.keyword.dns_short}} instance, follow these steps:
1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login) and log in to your account.
1. Select the **Navigation Menu** ![Menu icon](../icons/icon_hamburger.svg), then click **Resource list > Networking**.
1. Click the **Actions** menu ![Actions icon](../icons/action-menu-icon.svg "Actions") next to the instance that you want to delete, then select **Delete**.

### Why can't I delete a {{site.data.keyword.dns_short}} instance?
{: #why-cant-i-delete-an-instance}
{: faq}
{: support}

If a DNS zone is added to the {{site.data.keyword.dns_short}} instance, the instance cannot be deleted.

### Why am I getting timeout errors for DNS queries from my VPC?
{: #dns-query-rate-limit}
{: faq}

The DNS queries per second per availability zone [limit](/docs/dns-svcs?topic=dns-svcs-about-dns-services#limits) is an approximate value. Depending on how traffic is routed, what protocols the queries use, and other factors, the actual rate limit might vary. After a DNS query rate exceeds this rate limit, {{site.data.keyword.dns_short}} resolvers no longer respond to the excess DNS queries.

## DNS zones
{: #frequently-asked-questions-zones}

### When creating a DNS zone, what is the purpose of the **Label** field?
{: #purpose-of-label}
{: faq}

An instance can have multiple DNS zones with the same name. The label helps differentiate between zones that share the same name.

### How many private zones are supported?
{: #how-many-private-zones-supported}
{: faq}

{{site.data.keyword.dns_short}} supports 10 private zones per service instance.

### What do the different zone states mean?
{: #zone-states-definitions}
{: faq}

The zone state definitions are as follows.
* **Pending**: When a DNS zone is added to the instance, it is in `Pending` state. In this state, resource records can be added, deleted, or updated. Because the zone does not have any permitted networks, the zone is not served by the resolvers in any region.
* **Active**: When a domain has one or more permitted networks added, the domain state changes to `ACTIVE` and the domain is served by the resolver from all regions.
* **Disabled**: In this state, the zone is not served and all control path operations are disabled except for deleting the zone.

### Can I use any name for the zone?
{: #can-i-use-any-name-for-zone}
{: faq}
{: support}

In general, yes, you can use any name for the zone. Certain IBM-owned or IBM-specific DNS zone names are restricted, in other words, they cannot be created in {{site.data.keyword.dns_short}}. For a complete list of restricted zone names, see [Restricted DNS zone names](/docs/dns-svcs?topic=dns-svcs-managing-dns-zones#restricted-dns-zone-names).

### Can I create two DNS zones with the same name?
{: #can-i-create-2-zones-with-same-name}
{: faq}

Creating two DNS zones with the same name is allowed. Use the **label** and **description** fields as described in the following steps to differentiate between the two zones.
1. Create an instance of {{site.data.keyword.dns_short}}.
1. Create a DNS zone for each environment (for example, production, staging, development, testing). When creating the zone, make sure to include a description indicating what environment the zone is for. The zone name is the same for each zone (for example, `testing.com`).

    A single {{site.data.keyword.dns_short}} instance can contain only 10 zones.
    {: note}

1. Add a zone to the instance of {{site.data.keyword.dns_short}}.
1. In each respective zone, add specific VPCs as permitted networks. For example, for a development VPC, create a permitted network with the development VPC ID in the DNS zone for the development environment.

    While duplicate zone names are allowed in an account, duplicate zones cannot be associated with a single permitted network.
    {: note}

1. The result is that traffic from the development VPC sees records only from the development DNS zone, and similarly for all other environments. This way, you can use the same zone name in all environments, with the results tailored to each respective environment.

### Can I add the same permitted network (for example, a VPC) to two DNS zones of the same name?
{: #can-i-add-same-permitted-network-to-two-dns-zones-same-name}
{: faq}

No, adding the same permitted network (for example, a VPC) to two DNS zones of the same name is not allowed.

### What are the authoritative servers for the {{site.data.keyword.dns_short}} zones? Can I resolve the private DNS zones iteratively?
{: #authoritative-servers-for-dns-zones}
{: faq}

Unlike public DNS zones, {{site.data.keyword.dns_short}} does not expose authoritative servers for private DNS zones. Clients must send their recursive DNS queries to the DNS resolvers provided by the service. {{site.data.keyword.dns_short}} does not allow iterative resolution of private DNS zones.

### Can I create a DNS zone with the same name as a public DNS zone?
{: #create-dns-zone-same-name-public-dns-zone}
{: faq}
{: support}

{{site.data.keyword.dns_short}} allows you to create a private DNS zone that can have the same name as a public DNS zone. This scenario is referred to as Split Horizon. For more information, see, [Resolving DNS names with DNS Services](/docs/dns-svcs?topic=dns-svcs-about-dns-services#resolving-dns-names-with-dns-services).

### Why can't I delete a DNS zone?
{: #why-cant-i-delete-a-zone}
{: faq}

If a network is added to a zone, the zone cannot be deleted until the permitted network is deleted from the zone.

## DNS records
{: #frequently-asked-questions-records}

### How many DNS records are supported?
{: #how-many-dns-records-supported}
{: faq}

{{site.data.keyword.dns_short}} supports 3500 DNS records per DNS zone.

## Permitted networks
{: #frequently-asked-questions-permitted-networks}

### How many permitted networks are supported?
{: #how-many-permitted-networks-supported}
{: faq}

{{site.data.keyword.dns_short}} supports 10 permitted networks per DNS zone.

### What happens if I delete my VPC?
{: #what-if-i-delete-vpc}
{: faq}

If the VPC is deleted, the corresponding permitted network is also deleted from the DNS zones of your instance.

### Why can I still resolve my resource records after deleting its associated zone or permitted network?
{: #why-can-i-resolve-resource-records-after-delete}
{: faq}

To maintain a level of performance while resolving DNS queries, DNS Services resolvers cache data related to permitted networks for a period of time. Changes made to a permitted network might not have propagated until the previously cached data expires. For more details, see [Known issues and limitations](/docs/dns-svcs?topic=dns-svcs-limitations-known-issues).

## Custom resolvers
{: #frequently-asked-questions-custom-resolvers}

### Why am I still being charged for a disabled custom resolver or location?
{: #disabled-custom-resolver-charge}
{: faq}

When you disable a custom resolver or a custom resolver location, the underlying appliance is still provisioned and subjected to billing. To prevent unwanted charges, delete the custom resolver and custom resolver locations.

### How do I upgrade my plan from free to standard?
{: #upgrade-plan-free-standard}
{: faq}

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login) and log in to your account.
1. Select the **Navigation Menu** ![Menu icon](../icons/icon_hamburger.svg), then click **Resource list > Networking**.
1. Select the instance of {{site.data.keyword.dns_short}} you want to upgrade.
1. Select **Plan** from the navigation menu.
1. Select **Standard DNS** from the plan table.
1. Click **Save** and then click **OK** when prompted to verify "Are you sure that you want to change plans?"

To update to the standard plan from the command-line interface, see [Update DNS Services instances](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#update-DNS-services-instance).

### Why is my custom resolver request count so low?
{: #why-custom-resolver-request-response-count-low}
{: faq}

DNS Services platform metrics count DNS queries to custom resolvers in two ways: DNS requests, and cache hits and misses. When a DNS query is first received by the custom resolver location, it counts that query towards the DNS requests total. Subsequent queries made before the TTL is reached are counted towards the cache hits and misses total. For example, if 100 queries are made in rapid succession for a given domain, the DNS requests count would be 1 and the cache hits count would be 99.

If you want to view the total request count, you can do one of the following:
* Combine the DNS requests and cache hits.
* Combine the cache hits and misses.
* View the cache requests metric.

### Why do my custom resolver metrics show a `.` instead of my requested zone name?
{: #why-custom-resolver-metrics-show-period}
{: faq}

The custom resolver metric shows the zone name only for queries to zones that have forwarding rules configured. Queries for any other zones result in a zone name of `.`.

## Global load balancers
{: #frequently-asked-questions-glb}

### Are there any limits on global load balancer usage?
{: #load-balancer}
{: faq}

For more information on global load balancer usage, see [Global load balancers limitations](/docs/dns-svcs?topic=dns-svcs-global-load-balancers#glb-ki).

### What types of health checks are supported?
{: #health-check-types-supported}
{: faq}

HTTP and HTTPS health checks are currently supported.

### What regions can I use for health check monitoring?
{: #what-regions-health-check-monitoring}
{: faq}

For an updated list of regions where health checks are currently supported, see [DNS Services supported regions](/docs/dns-svcs?topic=dns-svcs-about-dns-services#supported-regions).

### How can I disable health check monitoring for an origin?
{: #disable-health-check-monitoring-to-origin}
{: faq}

You can disable health check monitoring for an origin by disabling it.

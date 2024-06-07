---

copyright:
  years: 2020, 2023
lastupdated: "2023-07-07"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# FAQs
{: #frequently-asked-questions}

Have a question about {{site.data.keyword.dns_full}}? Review frequently asked questions, which provide answers to provisioning concerns, application access, and other common inquiries.
{: shortdesc}

## How do I create my own private DNS zone using {{site.data.keyword.dns_short}}?
{: #private-zone}
{: faq}

To create your own private DNS zone using {{site.data.keyword.dns_short}}, take the following steps.
1. Create a VPC instance.
1. Create a {{site.data.keyword.dns_short}} instance.
1. Add a DNS zone to the {{site.data.keyword.dns_short}} instance.
1. Designate the VPC instance as a permitted network for the DNS zone.
1. Add a DNS Resource Record to the DNS zone.
1. Verify name resolution of the DNS Resource Record works from within the VPC.

## How is {{site.data.keyword.dns_short}} different from public DNS?
{: #not-for-public}
{: faq}

{{site.data.keyword.dns_short}} permits name resolution only from permitted VPCs within your {{site.data.keyword.cloud}} account. The DNS zone is not resolvable from the internet.

## Can I manage publicly available DNS records with this service?
{: #publicly-available-dns-records}
{: faq}

No, {{site.data.keyword.dns_short}} only offers private DNS at the moment. Use [{{site.data.keyword.cis_short_notm}}](/docs/cis?topic=cis-getting-started#getting-started) for public DNS.

## Is DNSSec supported with zones managed by {{site.data.keyword.dns_short}}?
{: #dnssec-supported-with-zones}
{: faq}

DNSSec allows resolvers to cryptographically verify the data received from authoritative servers. {{site.data.keyword.dns_short}} resolvers support DNSSec for public domains, for which requests are forwarded to public resolvers that support DNSSec. For private zones, since the authority is within {{site.data.keyword.cloud_notm}}, records are fetched using secure protocols, and are guaranteed to have the same level of privacy and security that DNSSec provides for public zones.

## Is {{site.data.keyword.dns_short}} regional or global?
{: #is-dns-svcs-global}
{: faq}

{{site.data.keyword.dns_short}} is a global service and can be used from permitted networks in any {{site.data.keyword.cloud_notm}} region.

## When creating a DNS zone, what is the purpose of the `Label` field?
{: #purpose-of-label}
{: faq}

A given instance can have multiple DNS zones with the same name. The label helps to differentiate zones with name collisions.

## How many private zones are supported?
{: #how-many-private-zones-supported}
{: faq}

{{site.data.keyword.dns_short}} supports 10 private zones per service instance.

## How many permitted networks are supported?
{: #how-many-permitted-networks-supported}
{: faq}

{{site.data.keyword.dns_short}} supports 10 permitted networks per DNS zone.

## How many DNS records are supported?
{: #how-many-dns-records-supported}
{: faq}

{{site.data.keyword.dns_short}} supports 3500 DNS records per DNS zone.

## How do I delete my {{site.data.keyword.dns_short}} instance?
{: #delete-dns-svcs-instance}
{: faq}

To delete a {{site.data.keyword.dns_short}} instance,
- Navigate to the Resource List in the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}/).
- Click the "overflow" menu ![overflow menu icon](../icons/actions-icon-vertical.svg "Overflow menu icon") in the final column and select "Delete".

## Why can't I delete a {{site.data.keyword.dns_short}} instance?
{: #why-cant-i-delete-an-instance}
{: faq}
{: support}

If a DNS zone has been added to the {{site.data.keyword.dns_short}} instance, the instance cannot be deleted.

## Why can't I delete a DNS zone?
{: #why-cant-i-delete-a-zone}
{: faq}

If a network has been added to a zone, the zone cannot be deleted until the permitted network is deleted from the zone.

## What happens if I delete my VPC?
{: #what-if-i-delete-vpc}
{: faq}

If the VPC is deleted, the corresponding permitted network will also be deleted from the DNS zones of your instance.


## Why can I still resolve my resource records after I deleted its associated zone or permitted network?
{: #why-can-i-resolve-resource-records-after-delete}
{: faq}

To maintain a level of performance while resolving DNS queries, DNS Services resolvers cache data related to permitted networks for a period of time. Changes made to a permitted network might not have propagated until the previously cached data expires. See [Known limitations](/docs/dns-svcs?topic=dns-svcs-known-limitations) for more details.

## Why am I still being charged for a disabled custom resolver or location?
{: #disabled-custom-resolver-charge}
{: faq}

When you disable a custom resolver or a custom resolver location, the underlying appliance is still provisioned and subject to billing. To prevent unwanted charges, delete the custom resolver and custom resolver locations.

## What do the different zone states mean?
{: #zone-states-definitions}
{: faq}

The zone states definitions are as follows.
* **Pending**: When a DNS zone is added to the instance it will be in `Pending`. In this state Resource Records can be added, deleted or updated. Since the zone does not have any permitted networks, the zone will not be served by the resolvers in any region.
* **Active**: When a domain has one or more permitted networks added then the domain state changes to `ACTIVE` and the domain will be served by the resolver from all the regions.
* **Disabled**: In this state the zone will not be served and all control path operations will be disabled except deleting the zone.

## Can I use any name for the zone?
{: #can-i-use-any-name-for-zone}
{: faq}
{: support}

In general, yes, you can use any name for the zone. Certain IBM-owned or IBM-specific DNS zone names are restricted, in other words, they can't be created in {{site.data.keyword.dns_short}}. See [Restricted DNS zone names](/docs/dns-svcs?topic=dns-svcs-managing-dns-zones#restricted-dns-zone-names) for the complete list.

## Can I create two DNS zones with the same name?
{: #can-i-create-2-zones-with-same-name}
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
{: #can-i-add-same-permitted-network-to-two-dns-zones-same-name}
{: faq}

No, adding the same permitted network (for example, a VPC) to two DNS zones of the same name is not allowed.


## What are the authoritative servers for the {{site.data.keyword.dns_short}} zones? Can I resolve the private DNS zones iteratively?
{: #authoritative-servers-for-dns-zones}
{: faq}

Unlike public DNS zones, {{site.data.keyword.dns_short}} does not expose authoritative servers for private DNS zones. Clients must send their recursive DNS queries to the DNS resolvers provided by the service. {{site.data.keyword.dns_short}} does not allow iterative resolution of private DNS zones.

## Can I create a DNS zone with same name as a Public DNS zone?
{: #create-dns-zone-same-name-public-dns-zone}
{: faq}
{: support}

{{site.data.keyword.dns_short}} allows creating a private DNS zone that can have the same name as the public DNS zone. See a [detailed explanation](/docs/dns-svcs?topic=dns-svcs-about-dns-services#resolving-dns-names-with-dns-services) of this scenario, referred to as Split Horizon.


## Are there any limits on global load balancer usage?
{: #load-balancer}
{: faq}

See [Global load balancers limitations](/docs/dns-svcs?topic=dns-svcs-global-load-balancers#glb-ki) for more information on global load balancer usage.

## What types of health checks are supported?
{: #health-check-types-supported}
{: faq}

HTTP and HTTPS health checks are currently supported.

## What regions can I use for health check monitoring?
{: #what-regions-health-check-monitoring}
{: faq}

Health checks are currently supported in the following regions:
* Dallas (us-south)
* Washington, D.C. (us-east)
* London (eu-gb)
* Frankfurt (eu-de)
* Osaka (jp-osa)
* Tokyo (jp-tok)
* Toronto (ca-tor)
* Sydney (au-syd)
* Sao Paulo (br-sao)

## How can I disable health check monitoring to the origins?
{: #disable-health-check-monitoring-to-origin}
{: faq}

You can disable health check monitoring by disabling the origin.

## How do I upgrade my plan from free to standard?
{: #upgrade-plan-free-standard}
{: faq}

1. Navigate to the Resource List in the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}/).
1. Select the instance of {{site.data.keyword.dns_short}} you want to upgrade.
1. Select **Plan** from the navigation menu.
1. Select **Standard DNS** from the plan table.
1. Click **Save** and then click **OK** when prompted to verify 'Are you sure that you want to change plans?'.

See [Update DNS Services instances](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#update-DNS-services-instance) to update to the standard plan using the command-line interface.

## Where do I find cost estimates for {{site.data.keyword.dns_short}}?
{: #where-do-i-find-cost-estimates-for-dns-svcs}
{: faq}
{: support}

You can estimate the cost of a service using the cost estimator on the provisioning pages for {{site.data.keyword.dns_short}} offerings. For example, log in to the [{{site.data.keyword.dns_short}}](/catalog/services/dns-services) console and click **Estimate costs** in the Summary panel. As you complete the form, cost estimates appear in the Summary side panel.

## Why am I getting timeout errors for my DNS queries from my VPC when my query rate is more or less than the noted rate limit?
{: #dns-query-rate-limit}
{: faq}

The noted DNS queries per second per availability zone rate [limit](/docs/dns-svcs?topic=dns-svcs-about-dns-services#limits) is currently the typical amount when using {{site.data.keyword.dns_short}} resolvers from a VPC. Depending on how traffic is actually routed, what protocols the queries use, and other factors, the actual rate limit might vary around this number. After a DNS query rate exceeds this rate limit, {{site.data.keyword.dns_short}} resolvers no longer respond to the excess DNS queries.

## Why is my custom resolver request and response count so low?
{: #why-custom-resolver-request-response-count-low}

DNS Services platform metrics counts DNS queries to custom resolvers in two ways: DNS requests, and cache hits and misses. When a DNS query is first received by the custom resolver location it counts that query towards the DNS requests total. Subsequent queries made before the TTL is reached are counted towards the cache hits and misses total. For example if 100 queries are made in rapid succession for a given domain, the DNS requests count would be 1 and the cache hits count would be at 99.

If you want view the total request count you can do one of the following:
* Combine the DNS requests and cache hits
* Combine the cache hits and misses
* View the cache requests metric

## Why is my custom resolver metrics showing a `.` instead of my requested zone name?
{: #why-custom-resolver-metrics-show-period}

The custom resolver metric only shows the zone name for queries that are made for zones that have forwarding rules established. Queries for any other zones result in a zone name of `.`

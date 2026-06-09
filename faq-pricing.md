---

copyright:
  years: 2020, 2026
lastupdated: "2026-06-09"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for DNS Services Pricing
{: #frequently-asked-questions}

Have a question about {{site.data.keyword.dns_full}} Pricing? Review frequently asked questions, which provide answers to provisioning concerns, application access, and other common inquiries.
{: shortdesc}

## Where do I find cost estimates for {{site.data.keyword.dns_short}}?
{: #where-do-i-find-cost-estimates-for-dns-svcs}
{: faq}
{: support}

You can estimate the cost of a service using the cost estimator on the provisioning pages for {{site.data.keyword.dns_short}} offerings. For example, log in to the [{{site.data.keyword.dns_short}}](/catalog/services/dns-services) console and click **Estimate costs** in the Summary panel. As you complete the form, cost estimates appear in the Summary side panel.

## What does “Million DNS Queries” refer to?
{: #what-are-million-dns-queries}
{: faq}
{: support}

- “Million DNS Queries” refers to DNS queries answered by the Private DNS Service backend resolvers (161.26.0.7, 161.26.0.8).
- Private DNS Service backend resolvers (161.26.0.7, 161.26.0.8) only charge for private zones queries, meaning zones defined and permitted to VPC by a given DNS Service Instance. Any queries forwarded to public resolvers (161.26.0.10, 161.26.0.11) are not charged.
- A Virtual Server Instance in a VPC without a DNS Service by default will point to public resolvers (161.26.0.10 and 161.26.0.11) and is not charged.

## When creating DNS Services from the IBM Cloud Catalog, does a Custom Resolver Location correspond to a single IP on a Custom Resolver, and does the cost increase if deployed across multiple subnets or zones?
{: #create-dns-cost-per-subnet-zone}

The listed price in the [{{site.data.keyword.cloud_notm}} **Catalog**](https://{DomainName}/catalog/) is per `Custom Resolver Location`, where location is equivalent to being deployed to a subnet. For example, a custom resolver deployed across three subnets would cost three times the rate listed in the Catalog. 

Billing continues even if a Custom Resolver or its locations are in the `disabled` state, since each custom resolver location is a managed appliance provisioned for you.
{: note}

## When creating DNS Services from the IBM Cloud Catalog, what does the option Million Custom Resolver External Queries refer to, and are these DNS queries sent via forwarding rules?
{: #create-dns-million-custom-resolver-external-queries}

The option **Million Custom Resolver External Queries** refers to queries that result in a cache miss and are not forwarded to our Private DNS resolvers (`161.26.0.7`, `161.26.0.8`).

## Am I charged when queries are sent through a Custom Resolver and when they are forwarded to on-premises DNS servers by forwarding rules? 
{: #dns-charge-per-query}

Yes, you are charged for queries that result in a cache miss and are not forwarded to our Private DNS resolvers (161.26.0.7, 161.26.0.8).


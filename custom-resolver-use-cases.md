---

copyright:
  years: 2021
lastupdated: "2021-07-12"

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
{:beta: .beta}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Custom resolvers use cases (Beta)
{: #custom-resolvers-use-case}

The custom resolver feature is available to {{site.data.keyword.dns_short}} users with a Standard plan. 
{: beta}

{{site.data.keyword.dns_full}} provides custom resolvers as a service that offers the ability to customize the hostname resolving rules for different hostnames. The custom resolver feature offers fine-grained control of name resolution and forwarding of DNS Queries to and from on-premises DNS resolvers.
{: shortdesc}

In this example scenario, financial data is in the on-premises instance and you manage this data access under the DNS zone `fin.example.com` which is managed by your on-premises DNS servers. Your applications running in IBM Cloud VPC need to access financial data with hostnames under this DNS zone. 

In this case, you can create custom resolvers to forward the DNS queries on this DNS zone to your on-premises DNS servers. The custom resolvers also allow you to customize rules to forward DNS queries to {{site.data.keyword.dns_short}} servers, public resolvers, or even custom resolvers launched in other IBM Cloud VPCs.

## Concepts
{: #cr-concepts}

A custom resolver is a logical object created for an IBM Cloud VPC in a {{site.data.keyword.dns_short}} instance. Within the custom resolver, you can specify which locations you want to launch the underlying DNS forwarders for the custom resolver. The custom resolver location is equivalent to the subnet in the IBM Cloud VPC. You can create a custom resolver by specifying only one location, or two locations in different subnets in the same VPC. 

A custom resolver can have multiple forwarding rules to customize where the DNS queries on what DNS zones should be forwarded to. A default forwarding rule is automatically created along with the custom resolver to forward DNS queries to {{site.data.keyword.dns_short}} servers.


## Use cases and workflows
{: #cr-use-cases}

The most common use cases of custom resolvers are: 

- Forwarding DNS queries from an IBM Cloud VPC to your on-premises DNS servers, or the reverse.
- Forwarding DNS queries from an IBM Cloud VPC to public resolvers.
- Forwarding DNS queries from one IBM Cloud VPC to another.

The following workflows are performed from the {{site.data.keyword.dns_short}} dashboard. Navigate to the **Custom resolver** tab to view your custom resolvers.
{: note}

### Creating a custom resolver with forwarding rules
{: #create-cr}

Follow this workflow to create a custom resolver with forwarding rules:

1. Create a custom resolver by selecting the region, VPC, and adding one or two subnets.
1. The default forwarding rule is automatically created to forward all DNS queries to {{site.data.keyword.dns_short}} servers.
1. Create a forwarding rule to specify DNS queries on what DNS zones should be forwarded to what DNS servers.
1. Enable the custom resolver.

The default forwarding rule is always used last if the query name doesn't match any of the preceding forwarding rules.
{: note}

### Forwarding DNS queries to {{site.data.keyword.dns_short}} servers
{: #fwd-dns-svcs}

To forward DNS queries on a specific DNS zone to {{site.data.keyword.dns_short}} servers, enter the forwarding IP addresses `161.26.0.7` and `161.26.0.8`. 

### Forwarding DNS queries to public resolver
{: #fwd-public-resolver}

To forward DNS queries on a specific DNS zone to public resolvers on the internet, create a public gateway and attach it to the subnet used for the custom resolver location before entering the public resolver IP addresses as the forwarding IP. 

See the [External connectivity](/docs/vpc?topic=vpc-about-networking-for-vpc#external-connectivity) documentation for more information on connecting to external networks.
{: note}

### Forwarding DNS queries across VPCs
{: #fwd-across-vpcs}

You might want to create custom resolvers on multiple VPCs and use these custom resolvers to follow the spoke-and-hub paradigm. In this configuration, you must interconnect the VPCs through a transit gateway in advance.

See the [Managing transit gateway](/docs/transit-gateway?topic=transit-gateway-adding-connections) documentation for interconnecting VPCs using a transit gateway.

To form the spoke-and-hub topology for custom resolvers across different VPCs, choose one custom resolver as the hub and manage its forwarding rules in the hub custom resolver. You must also edit the default forwarding rule in each spoke custom resolver to forward DNS queries to the hub custom resolver.

---

copyright:
  years: 2022
lastupdated: "2022-07-20"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Understanding secondary zones
{: #sec-zones-about}

## Secondary zone definition
{: #secondary-zone-term}

A secondary zone is a read-only copy of the primary DNS zone. Instead of getting information from local files, secondary zones receive pertinent information from a primary server in a communication process known as a zone transfer.
{: shortdesc}

With secondary zones, you can duplicate records from your on-premises DNS server to your DNS Services custom resolver. The custom resolver gives fine-grain control of name resolution and also enables forwarding DNS queries to and from on-premises DNS servers. You can make DNS queries for transferred zones within your VPC and receive the same records as if the query was made to your on-premises DNS server.

Existing custom resolvers automatically support the secondary zone feature, but you will have to create a secondary zone manually.
{: tip}

## Configuring secondary zones
{: #sec-zone-config}

When configuring secondary zones, take the following into consideration:

* Server must have the zone configured
* Server must enable DNS transfer to all custom resolver locations
* Currently, custom resolver only perform AXFR, and not IXFR
* Custom resolver uses port 53 to communicate with DNS server
* Each custom resolver can have a maximum of 5 secondary zones

## Example for secondary zone
{: #secondary-zone-example}

In this example, a customer has a zone `onprem.customer.com` which is managed by the DNS server `10.230.9.2`. In IBM Cloud, the customer has workloads running in VPCs which need to resolve resource record `database.onprem.customer.com`. Using custom resolvers and forwarding rules the customer can resolve the name by forwarding the query to DNS server `10.230.9.2`, but if the DNS server is down or has connectivity issues, the name resolution fails. To avoid this, instead of a forwarding rule the customer can configure a secondary zone rule in their custom resolver and on-premises DNS server. Then, even if there are intermittent connectivity issues reaching the on-premises DNS server, the custom resolver locations can resolve the resource record requests.

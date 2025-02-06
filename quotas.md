---

copyright:
  years: 2019, 2025
lastupdated: "2025-02-06"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Quotas and service limits for DNS services
{: #dns-quotas-service-limits}

This section details some of the quotas and service limits of DNS services.
{: shortdesc}

## Quotas for DNS services
{: #dns-quotas}

### Quotas for Custom Resolvers
{: #custom-resolver-quotas}

| Resource | Quota |
|--------|-----|
| Secondary zones | 100 |
| Forwarding rules | 100 |
| View Limits per forwarding rule | 5 |
{: caption="Quotas for DNS services" caption-side="bottom"}

For more information, see [Custom resolver profiles overview](https://cloud.ibm.com/docs/dns-svcs?topic=dns-svcs-custom-resolver#cr-profiles).

## Service limits for DNS services
{: #dns-service-limits}

* Resolvers cache permitted network details for a zone. The TTL for these cached details is typically 1 hour.
* In custom resolvers, disabling both custom resolver locations at the same time may be possible, but is _not recommended_ when the custom resolver is enabled.
* {{site.data.keyword.dns_short}} custom resolver platform metrics do not track secondary zone usage. This means that DNS queries made to a configured custom resolver for a secondary zone will not be counted in the reported metrics.
* Each VPC can have a maximum of one custom resolver.
* Each custom resolver can have a maximum of 3 locations, either within the same subnet or in different subnets.
* You cannot delete the subnet that is used for the custom resolver.
* You must manually add rules to your security groups to allow traffic from your virtual server instance to the resolver location's virtual server instance.

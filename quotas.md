---

copyright:
  years: 2019, 2025
lastupdated: "2025-02-20"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Quotas and service limits for DNS services
{: #dns-quotas-service-limits}

This section lists the quotas and service limits for DNS services.
{: shortdesc}

## Quotas for DNS services
{: #dns-quotas}

These quotas list the maximum limit for DNS Services resources. If the default limit of resources is not suitable for your business needs, you can [create a support case](/unifiedsupport/cases/add){: external} to request an increase of your resource quota values.

### Quotas for custom resolver profiles
{: #custom-resolver-quotas}

You can use custom resolver profiles to increase the limits on how many forwarding rules, secondary zones, or DNS views can be configured. Additionally, if you want to configure many DNS records for their secondary zones, a larger profile prevents performance bottlenecks.

Quotas vary based on the custom resolver profile you select. 

|                              | Essential | Advanced | Premier   |
|------------------------------|-----------|----------|-----------|
| Forwarding rules             | 10        | 50       | 100       |
| Secondary zones              | 10        | 50       | 100       |
| Total recommended number of DNS records | 100,000   | 500,000  | 6,000,000 |
| DNS view per forwarding rule | 1         | 3        |  5        |
{: caption="Comparison of custom resolver profiles by plan" caption-side="bottom"}

Larger custom resolver profiles result in an increased usage cost per location configured.
{: note}

## Service limits for DNS Services
{: #dns-service-limits}

* Each VPC can have a maximum of one custom resolver configured on it. This means that if a custom resolver is configured in one DNS Services instance for a given VPC it will not be allowed to be configured for that VPC again even if it is within a different DNS Services instance.
* Each custom resolver can have a maximum of 3 locations, either within the same subnet or in different subnets.
* You cannot delete the subnet that is used for the custom resolver.
* You must manually add rules to your security groups to allow traffic from your virtual server instance to the resolver location's virtual server instance.

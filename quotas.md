---

copyright:
  years: 2019, 2025
lastupdated: "2025-02-17"

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

[Note]{: tag-red} _Are there other quotas for DNS Services besides custom resolvers?  Need to list here._

These headings require a short description or sentence before list items. Are these the quotas when not using a profile? Need to state that the quotas differ depending on the profile being used. These quotas aren't quotas for profiles. (example, Advanced profile you are only allowed up to 50 forwarding rules).

_Not sure if you can increase quotas but here's a typical intro to this section._

_These quotas list the maximum limit for DNS Services resources. If the default limit of resources is not suitable for your business needs, you can [create a support case](/unifiedsupport/cases/add){: external} to request an increase of your resource quota values._

### Quotas for custom resolver profiles
{: #custom-resolver-quotas}

Quotas vary based on the custom resolver profile you select. For more information, see [Custom resolver profiles overview](https://cloud.ibm.com/docs/dns-svcs?topic=dns-svcs-custom-resolver#cr-profiles).

[Note]{: tag-red} _Are these service limits or limitations? Most repos require a separate topic in Help subsection titled "Known issues and limitations. Need to identify what are service limits vs limitations vs planning considerations._

## Service limits for DNS Services
{: #dns-service-limits}

* Each VPC can have a maximum of one custom resolver.
* Each custom resolver can have a maximum of 3 locations, either within the same subnet or in different subnets.
* You cannot delete the subnet that is used for the custom resolver.
* You must manually add rules to your security groups to allow traffic from your virtual server instance to the resolver location's virtual server instance.

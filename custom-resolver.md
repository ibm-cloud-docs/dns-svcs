---

copyright:
  years: 2021, 2022
lastupdated: "2022-07-08"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Working with custom resolvers
{: #custom-resolver}

A private DNS custom resolver extends {{site.data.keyword.dns_full}}'s capability to meet the needs of a hybrid cloud environment by enabling resolution of the {{site.data.keyword.cloud_notm}} VPC hostnames from on-premises DNS resolvers, and also enables the  resolution of on-premises hostnames from the {{site.data.keyword.cloud_notm}}. 
{: shortdesc}

Key features of the custom resolver:

* Extends DNS resolutions to resolvers residing on-premises
* Allows for resolution fallback to a secondary resolver location (if one is configured) when the primary resolver location is not available

## Custom resolver overview
{: #custom-resolver-overview}

To get started using a custom resolver, you must create a custom resolver and then add forwarding rules to it. 

It is expected that the custom resolver will be configured for High Availability by default. Follow the steps in [Creating a custom resolver without high availability](/docs/dns-svcs?topic=dns-svcs-ui-create-cr&interface=ui#cr-add-no-ha) if you do not want a highly available configuration.
{: important}

After you create the custom resolver and configure its forwarding rules, the resolver can be enabled for the VPC. This results in the DHCP option for the resolver changing to the custom resolver IP addresses.

## Custom resolver status
{: #cr-statuses}

The status of a newly-created custom resolver is initially `Critical` because the resolver location is not yet enabled. The status changes to `Healthy` after the resolver location changes to `Up`.
{: note}

The following status definitions apply to the resolver locations:
* **Up** - when the resolver location is functioning.
* **Down** - when the resolver location is not functioning.

The following status definitions apply to the custom resolver:
* **Healthy** - when all resolver locations are `Up`, the status is `Healthy`.
* **Degraded** - when there is more than one resolver location, and one is `Up` but another is `Down`, then the status changes to `Degraded`.
* **Critical** - when all resolver locations are `Down`, the status changes to `Critical`.

## Custom resolvers limits
{: #cr-limits}

The following limits exist for the custom resolvers feature:

* Each VPC can have a maximum of one custom resolver.
* Each custom resolver can have a maximum of three locations, either within the same subnet or in different subnets.
* Each custom resolver can have a maximum of 10 forwarding rules.
* You cannot delete the subnet used for the custom resolver.
* You must manually add rules to your security groups to allow traffic from your virtual server instance to the resolver location virtual server instance.

For more information, see [{{site.data.keyword.dns_short}}'s pricing page](/docs/dns-svcs?topic=dns-svcs-pricing).

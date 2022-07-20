---

copyright:
  years: 2020, 2022
lastupdated: "2022-07-13"

keywords: 

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Auditing events for {{site.data.keyword.dns_short}}
{: #at_events}

As a security officer, auditor, or manager, you can use the Activity Tracker service to track how users and applications interact with the {{site.data.keyword.dns_full}} service in {{site.data.keyword.cloud}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the [getting started tutorial for {{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

## DNS zone events
{: #events_dns_zones}

The following table lists the actions that are related to DNS zones and generate an event.

|Action |Description|
|---|---|  
|`dns-svcs.zones.read`  |Get or list DNS zones. |
|`dns-svcs.zones.create`|Create a DNS zone.     |
|`dns-svcs.zones.update`|Update a DNS zone.     |
|`dns-svcs.zones.delete`|Delete a DNS zone.     |
{: caption="Table 1. DNS zones" caption-side="bottom"}

## Resource records events
{: #events_resource_record}

The following table lists the actions that are related to resource records and generate an event.

|Action |Description|
|---|---|
|`dns-svcs.resource-records.read`  |Get or list resource records. |
|`dns-svcs.resource-records.create`|Create a resource record.     |
|`dns-svcs.resource-records.update`|Update a resource record.     |
|`dns-svcs.resource-records.delete`|Delete a resource record.     |
{: caption="Table 2. Resource records" caption-side="bottom"}


## Permitted networks events
{: #events_permitted_networks}

The following table lists the actions that are related to permitted networks and generate an event.

|Action |Description|
|---|---|  
|`dns-svcs.permitted-networks.read`  |Get or list permitted networks from DNS zone. |
|`dns-svcs.permitted-networks.create`|Add a permitted network to DNS zone.          |
|`dns-svcs.permitted-networks.delete`|Remove a permitted network from DNS zone.     |
{: caption="Table 3. Permitted networks" caption-side="bottom"}


## Global balancer events
{: #events_global_load_balancers}

The following table lists the actions that are related to global load balancers and generate an event.

|Action |Description|
|---|---|
|`dns-svcs.monitors.read`        |Get or list health monitors. |
|`dns-svcs.monitors.create`      |Create a health monitor.     |
|`dns-svcs.monitors.update`      |Update a health monitor.     |
|`dns-svcs.monitors.delete`      |Delete a health monitor.     |
|`dns-svcs.pools.read`           |Get or list origin pools.    |
|`dns-svcs.pools.create`         |Create an origin pool.       |
|`dns-svcs.pools.update`         |Update an origin pool.       |
|`dns-svcs.pools.delete`         |Delete an origin pool.       |
|`dns-svcs.load-balancers.read`  |Get or list load balancers.  |
|`dns-svcs.load-balancers.create`|Create a load balancer.     |
|`dns-svcs.load-balancers.update`|Update a load balancer.     |
|`dns-svcs.load-balancers.delete`|Delete a load balancer.     |
{: caption="Table 4. Global load balancers" caption-side="bottom"}

## Custom resolvers
{: #events_custom_resolver}

The following table lists the actions that are related to custom resolvers and generate an event.

|Action |Description|
|---|---|
|`dns-svcs.custom-resolvers.read`  |Get or list custom resolvers.     |
|`dns-svcs.custom-resolvers.create`|Create a custom resolver.         |
|`dns-svcs.custom-resolvers.update`|Update a custom resolver.         |
|`dns-svcs.custom-resolvers.delete`|Delete a custom resolver.         |
|`dns-svcs.locations.create`       |Add a custom resolver location.   |
|`dns-svcs.locations.update`       |Update a custom resolver location.|
|`dns-svcs.locations.delete`       |Delete a custom resolver location.|
|`dns-svcs.forwarding-rules.read`  |Get or list forwarding rules.     |
|`dns-svcs.forwarding-rules.create`|Create a forwarding rule.         |
|`dns-svcs.forwarding-rules.update`|Update a forwarding rule.         |
|`dns-svcs.forwarding-rules.delete`|Delete a forwarding rule.         |
|`dns-svcs.secondary-zones.read`   |Get or list secondary zones.      |
|`dns-svcs.secondary-zones.create` |Create a secondary zone.          |
|`dns-svcs.secondary-zones.update` |Update a secondary zone.          |
|`dns-svcs.secondary-zones.delete` |Delete a secondary zone.          |
{: caption="Table 5. Custom resolvers" caption-side="bottom"}

## Cross-account zone access events
{: #events_cross_account_zone_access}

The following table lists the actions that are related to cross-account zone access and generate an event.

|Action |Description|
|---|---|
|`dns-svcs.linked-dnszone.create`                   |Requestor creates a linked zone.                          |
|`dns-svcs.linked-dnszone.update`                   |Requestor updates a linked zone.                          |
|`dns-svcs.linked-dnszone.delete`                   |Requestor deletes a linked zone.                          |
|`dns-svcs.linked-dnszone.read`                     |Requestor get or list linked zones.                       |
|`dns-svcs.linked-dnszone-access-request.approve`   |Owner approves a access request.                          |
|`dns-svcs.linked-dnszone-access-request.reject`    |Owner rejects a access request.                           |
|`dns-svcs.linked-dnszone-access-request.revoke`    |Owner revokes a access request.                           |
|`dns-svcs.linked-dnszone-access-request.read`      |Owner get or list access requests.                        |
|`dns-svcs.linked-dnszone-permitted-networks.create`|Requestor adds a permitted network in a linked zone.      |
|`dns-svcs.linked-dnszone-permitted-networks.delete`|Requestor removes a permitted network from a linked zone. |
|`dns-svcs.linked-dnszone-permitted-networks.read`  |Requestor get or list permitted networks in a linked zone.|
{: caption="Table 6. Cross-account zone access" caption-side="bottom"}


## Viewing events
{: #ui}

The {{site.data.keyword.dns_short}} {{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} instance in the {{site.data.keyword.cloud_notm}} **Frankfurt** region.

## Requesting additional information for an event
{: #info}

While monitoring {{site.data.keyword.cloudaccesstrailshort}} events that are generated by the {{site.data.keyword.dns_full_notm}}, if you identify an API request for which you need additional information, then check the `requestData` field in the event. Open an IBM Support case and include the value of the field **requestId** that is available in `requestData`.

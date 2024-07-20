---

copyright:
  years: 2020, 2024
lastupdated: "2024-07-20"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracking events for {{site.data.keyword.dns_short}}
{: #at_events}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.dns_short}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

As of 28 March 2024, the {{site.data.keyword.at_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.at_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Activity tracking events are the same for both services. For information about migrating from {{site.data.keyword.at_full_notm}} to {{site.data.keyword.logs_full_notm}} and running the services in parallel, see [migration planning](/docs/cloud-logs?topic=cloud-logs-migration-intro).
{: important}

## Locations where activity tracking events are generated
{: #at-locations}

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`)| Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #at-table-1a}
{: tab-title="Americas"}
{: tab-group="ata"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #at-table-2a}
{: tab-title="Asia Pacific"}
{: tab-group="ata"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #at-table-3a}
{: tab-title="Europe"}
{: tab-group="ata"}
{: class="simple-tab-table"}
{: row-headers}

## Locations where activity tracking events are sent to {{site.data.keyword.at_full_notm}} hosted event search
{: #at-legacy-locations}



{{site.data.keyword.dns_short}} sends activity tracking events to {{site.data.keyword.at_full_notm}} hosted event search in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`)| Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #at-table-1}
{: tab-title="Americas"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #at-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #at-table-3}
{: tab-title="Europe"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

## Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}



{{site.data.keyword.dns_short}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

## Viewing activity tracking events for {{site.data.keyword.dns_short}}
{: #at-viewing}

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #at-log-launch-standalone}

For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)


## List of platform events
{: #at_actions_platform}



The following table lists the activity tracking event actions that the {{site.data.keyword.cloud_notm}} platform generates {{site.data.keyword.dns_short}} instances are processed.

| Action                                   | Description |
|------------------------------------------|---------|
| `{{site.data.keyword.dns_short}}.instance.create`           | An event is generated when you provision a service instance. |
| `{{site.data.keyword.dns_short}}.instance.update`           | An event is generated when you rename a service instance or when you change the service plan. |
| `{{site.data.keyword.dns_short}}.instance.delete`           | An event is generated when a service instance is deleted. |
| `{{site.data.keyword.dns_short}}.instance.schedule_reclaim` | An event is generated when a service instance is pending_reclamation. |
| `{{site.data.keyword.dns_short}}.instance.restore`          | An event is generated when a service instance is restored. |
{: caption="Actions that generate platform events" caption-side="bottom"}

## Events for DNS zones
{: #at_actions_dns-zones}

The following table lists the actions that are related to DNS zones and generate an event.

| Action                           | Description                        |
|----------------------------------|------------------------------------|
|`dns-svcs.zones.read`             |Get or list DNS zones. |
|`dns-svcs.zones.create`           |Create a DNS zone.     |
|`dns-svcs.zones.update`           |Update a DNS zone.     |
|`dns-svcs.zones.delete`           |Delete a DNS zone.     |
{: caption="DNS zones events" caption-side="bottom"}


## Events for resource records
{: #events_resource_record}

The following table lists the actions that are related to resource records and generate an event.

|Action |Description|
|---|---|
|`dns-svcs.resource-records.read`  |Get or list resource records. |
|`dns-svcs.resource-records.create`|Create a resource record.     |
|`dns-svcs.resource-records.update`|Update a resource record.     |
|`dns-svcs.resource-records.delete`|Delete a resource record.     |
{: caption="Resource records" caption-side="bottom"}


## Events for permitted networks
{: #events_permitted_networks}

The following table lists the actions that are related to permitted networks and generate an event.

|Action |Description|
|---|---|
|`dns-svcs.permitted-networks.read`  |Get or list permitted networks from DNS zone. |
|`dns-svcs.permitted-networks.create`|Add a permitted network to DNS zone.          |
|`dns-svcs.permitted-networks.delete`|Remove a permitted network from DNS zone.     |
{: caption="Permitted networks" caption-side="bottom"}


## Events for global balancers
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
{: caption="Global load balancers" caption-side="bottom"}

## Events for custom resolvers
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
{: caption="Custom resolvers" caption-side="bottom"}

## Events for cross-account zone access
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
{: caption="Cross-account zone access" caption-side="bottom"}

## Analyzing {{site.data.keyword.dns_short}} activity tracking events
{: #at_events_iam_analyze}

Refer to the following information when you are analyzing events:

- Filter for the `dns-svcs` action to see all {{site.data.keyword.dns_short}} events in your account.
- Activity Tracker actions are set to `read` for both the GET and LIST calls, for example, `dns-svcs.zones.read`.
    - LIST calls set the `target.name` field to empty.
    - GET calls set the `target.name` field to the name of the resource.
- The event's `correlationId` field contains a unique ID to identify the request transaction.
- The event's `initiator` field contains information about the person who initiated each request.
- All events that are issued for failed actions display `failure` in the `outcome` field, and provide more details as part of the `reason` field. Note that the `reason.reasonForFailure` field might be especially helpful, because it contains the details of the failure.
- You can find the detailed information and fields included in the `requestData` and `responseData` for the {{site.data.keyword.dns_short}} AT events in the [API documentation](/apidocs/dns-svcs).


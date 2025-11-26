---

copyright:
  years: 2018, 2025
lastupdated: "2025-11-26"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Logging for {{site.data.keyword.dns_short}}
{: #logging}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.dns_short}}, generate platform logs that you can use to investigate abnormal activity and critical actions in your account, and troubleshoot problems.
{: shortdesc}

You can use {{site.data.keyword.logs_routing_full_notm}}, a platform service, to route platform logs in your account to a destination of your choice by configuring a tenant that defines where platform logs are sent. For more information, see [About Logs Routing](/docs/logs-router?topic=logs-router-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on platform logs that are generated in your account and routed by {{site.data.keyword.logs_routing_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

## Locations where platform logs are generated
{: #log-locations}


{{site.data.keyword.dns_short}} generates platform logs to {{site.data.keyword.la_full_notm}} in the regions indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where platform logs are generated in Americas locations" caption-side="top"}
{: tab-title="Americas"}
{: tab-group="pl"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where platform logs are generated in Asia Pacific locations" caption-side="top"}
{: tab-title="Asia Pacific"}
{: tab-group="pl"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where platform logs are generated in Europe locations" caption-side="top"}
{: tab-title="Europe"}
{: tab-group="pl"}
{: class="simple-tab-table"}
{: row-headers}

## Locations where logs are sent by {{site.data.keyword.logs_routing_full_notm}}
{: #lr-locations}



{{site.data.keyword.dns_short}} sends logs by {{site.data.keyword.logs_routing_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where logs are sent in Americas locations" caption-side="top"}
{: tab-title="Americas"}
{: tab-group="lr"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where logs are sent in Asia Pacific locations" caption-side="top"}
{: tab-title="Asia Pacific"}
{: tab-group="lr"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where logs are sent in Europe locations" caption-side="top"}
{: tab-title="Europe"}
{: tab-group="lr"}
{: class="simple-tab-table"}
{: row-headers}

## Platform logs that are generated
{: #log-platform}

The following three types of platform logs are generated for DNS services:

`link_zone_action` 
:   Logs are created during key steps of the process of linking a zone between DNS Services instances. This includes when a request to link is created, and when the link is granted access. Learn more about [cross-account access](/docs/dns-svcs?topic=dns-svcs-cross-account-about&interface=ui).

`health_check_event`
:   Logs are created when there is critical activity regarding a healthcheck appliance. These logs can be related to the status of the appliance VSI itself, or to any of the origins that the healthcheck is monitoring. Learn more about [creating a health check](/docs/dns-svcs?topic=dns-svcs-global-load-balancers&interface=ui#add-a-health-check).

`custom_resolver_event` 
:   Logs are created when there is critical activity regarding custom resolvers. Activities such as create and delete events for custom resolver locations and status updates of the locations all fall under this category.Learn more about [working with custom resolvers](/docs/dns-svcs?topic=dns-svcs-custom-resolver).

## Viewing logs
{: #log-viewing}



### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}



For more information about launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## Fields by log type
{: #log-fields}

For information about fields included in every platform log, see [Fields for platform logs](/docs/logs-router?topic=logs-router-about-platform-logs#platform_reqd).

| Field             | Type       | Description             |
|-------------------|------------|-------------------------|
| `logSourceCRN`    | Required   | Defines the account and {{site.data.keyword.dns_short}} instance where the log is published. |
| `saveServiceCopy` | Required   | Defines whether IBM saves a copy of the record for operational purposes. |
| `message`         | Required   | Description of the log that is generated. |
| `messageID`       | Required   | ID of the log that is generated. |
| `msg_timestamp`   | Required   | The timestamps when the log is generated. |
| `resolution`      | Optional   | Guidance on how to proceed if you receive this log record. |
| `documentsURL`    | Optional   | More information on how to proceed if you receive this log record. |
{: caption="Log record fields" caption-side="bottom"}

## Analyzing {{site.data.keyword.dns_short}} logs
{: #cloud-logs}

### linked_zones_action logs
{: #analyzing-linked-zone-action-logs}

Notable fields:

`permitted_network`
:   Identifies the permitted network that is being granted access to the linked zone.

`requestor_info` 
:   Contains the account, instance, and zone information of the requestor.

Common messages to look for:

- `"Linked DNS zone <zone ID> under instance <instance ID> is approved by zone owner"` - indicates that a request to link a zone was approved.

- `"The permitted network <VPC ID> on linked dns zone <zone ID> under instance <instance ID>"' is removed by zone owner` - indicates that a previously allowed linked zone has been revoked.

### health_check_event logs
{: #analyzing-health-check-event-logs}

Notable fields:

`pool:healthy`
:   The overall health status of the pool being monitored. 

`origins:health_status_code`
:   The health status of each origin configured in the pool. 

Common messages to look for:

- `"The healthy status of origin <origin name> is changed to <UP/DOWN>"` - This indicates that the healthcheck for a given pool has identified a change in response from a given origin. Health status changes to the **DOWN** state should be monitored as they can indicate issues with either a configured network or origin.

### custom_resolver_event logs
{: #analyzing-custom-resolver-event-logs}

Notable fields:

`id`
:   An identifier for the custom resolver.

`healthy`
:   Overall health status of the custom resolver.

`locations:healthy`
:   Health status of individual custom resolver locations.

Common messages to look for:

- `"The status of custom resolver location <id> is changed from <up/down> to <up/down>"` - This message indicates that a custom resolver appliance has changed health status. This can be due a planned maintenance/update or from a unexpected outage.

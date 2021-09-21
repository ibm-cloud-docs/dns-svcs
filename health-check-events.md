---

copyright:
  years: 2020
lastupdated: "2020-11-18"

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
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Viewing health check events
{: #health-check-events}

When using global load balancing, you can create a health check to specify how the origin's health is monitored. Health check events are status changes from monitored origin pools and their associated origin servers. If an origin's status changes, a new event is recorded with the event's description.
{: shortdesc}

{{site.data.keyword.loganalysisfull}} manages system and application logs in the IBM Cloud. You can use this service to access health check events for your origin pools and origin servers. For more information, see the [Getting started tutorial](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-getting-started) for {{site.data.keyword.loganalysislong_notm}}.

## Before you begin
{: #loganalysis-preparation}

To view health check events in {{site.data.keyword.loganalysisshort}}, make sure that you create an {{site.data.keyword.loganalysislong_notm}} instance in the Frankfurt region in the account.

## Adding {{site.data.keyword.loganalysisshort}}
{: #loganalysis-nav}

From the UI, follow these steps to navigate to the {{site.data.keyword.loganalysisshort}} service:

1. From the {{site.data.keyword.dns_short}} navigation menu, click **Global load balancers**, then select the **Health checks** tab. 
1. For new logging, click **Add logging** to start creating a new {{site.data.keyword.loganalysisshort}} instance. 
1. To view existing {{site.data.keyword.loganalysisshort}} instances, click **Launch logging**.

{{site.data.keyword.loganalysislong_notm}} opens in a new tab.

## Receiving health check events with the {{site.data.keyword.loganalysisshort}} instance
{: #receiving-health-check-events-loganalysis}

To view health check events in a {{site.data.keyword.loganalysisshort}} instance, you must configure the {{site.data.keyword.loganalysisshort}} instance to receive platform logs with the following steps:

1. In the {{site.data.keyword.cloud_notm}} UI, click the menu icon ![menu icon](../icons/icon_hamburger.svg) and select **Observability**. The Observability dashboard appears.
1. Select **Logging**. The list of logging instances appears.
1. Click **Configure platform logs**.
1. Select the `Frankfurt` region, then select one {{site.data.keyword.loganalysisshort}} instance where you want to receive the platform logs.
1. Click **Save**.

### Viewing health check events in the {{site.data.keyword.loganalysisshort}} instance
{: #viewing-healtch-check-events-loganalysis}

To view health check events, use the UI of the {{site.data.keyword.loganalysisshort}} instance that you configured to receive the platform logs in the previous steps.

For more information, see [Launching the {{site.data.keyword.loganalysisshort}} web UI through the IBM Cloud UI](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-launch#launch_cloud_ui).

To search health check events from within the logging instance, enter the health check event type `health_check_event` in the **Search** field.

![{{site.data.keyword.loganalysisshort}} source search](images/health-check-type-filter.png)

You can also search for the events you want by combining other event fields. For example:

- Search health check events for a specific {{site.data.keyword.dns_short}} instance.
![search events by CRN](images/health-check-type-filter-crn.png)

- Search health check events for a pool by specifying its `name` and its {{site.data.keyword.dns_short}} instance.
![search events by CRN and pool name](images/health-check-type-filter-crn-pool.png)

- Search health check events for an origin by specifying its `name` and its {{site.data.keyword.dns_short}} instance.
![search events by CRN and origin name](images/health-check-type-filter-crn-origin.png)

- Search health check events for an origin when its status becomes healthy by specifying its `name` and `overall_health` fields and also its {{site.data.keyword.dns_short}} instance.
![search events by CRN, origin name and health](images/health-check-type-filter-crn-origin-health.png)

- Search health check events for a pool when its status becomes DEGRADED by specifying its `name` and `healthy` fields and also its {{site.data.keyword.dns_short}} instance.
![search events by CRN, pool name and health](images/health-check-type-filter-crn-pool-health.png)

## Health check event properties
{: #health-check-event-properties}

Health check event records have the following properties:

- `event_time`: The time at which the event was recorded. For example, `2020-10-28T15:04:05.00+0000`.
- `logSourceCRN`: CRN of the {{site.data.keyword.dns_short}} instance in which the origin pools and origin servers were created.
    For example: `crn:v1:bluemix:public:dns-svcs:global:a/bcf1865e99742d38d2d5fc3fb80a5496:85ed7b9d-cd48-4881-b354-52eb1d8e9011::`
- `type`: The value of this property is `health_check_event` for health check events.
- `origins`: An array of objects representing the origin servers associated with the origin pool. For example: 

    ```
    [
         {
             "name": "web-server1",
             "address": "10.240.0.4",
             "enabled": true,
             "healthy": true,
             "overall_health": true,
             "health_failure_reason": "SUCCESS",
             "changed": true
         },
         {
             "name": "web-server2",
             "address": "10.240.100.4",
             "enabled": true,
             "overall_health": false,
             "health_failure_reason": "CONNECTION_ERROR",
             "changed": false
         }
     ]
    ```
    {: codeblock}

- `pool`: An object that represents the origin pool for which the health check event was generated. For example:

    ```
    {
        "id": "987f3f96-c077-4124-87eb-846dc026e383",
        "name": "us-south-pool",
        "healthy_origins_threshold": 1,
        "enabled": true,
        "healthy": "DEGRADED",
        "changed": false
    }
    ```
    {: codeblock}

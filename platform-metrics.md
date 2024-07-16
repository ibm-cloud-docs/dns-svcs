---

copyright:
  years: 2023, 2024
lastupdated: "2024-07-16"

keywords: cloud monitoring, monitoring, platform metrics, observability page, enable platform metrics, view metrics, launch monitoring

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.mon_full_notm}} integration
{: #monitor-ibm-cloud-pm}

{{site.data.keyword.mon_full}} is a cloud-native and container-intelligent management system that you can include as part of your {{site.data.keyword.cloud}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full-stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.
{: shortdesc}

Currently, {{site.data.keyword.mon_full_notm}} integration is available for {{site.data.keyword.dns_short}} deployments according to the following table:

| Deployment Region | {{site.data.keyword.mon_full_notm}} Region |
|----------|-----------|
| `Dallas`        | `Dallas` |
| `Frankfurt`     | `Frankfurt` |
| `London`        | `London` |
| `Madrid`        | `Madrid`|
| `Osaka`         | `Osaka` |
| `Paris`         | `Paris` |
| `São Paulo`     | `São Paulo` |
| `Sydney`        | `Sydney` |
| `Tokyo`         | `Tokyo` |
| `Toronto`       | `Toronto` |
| `Washington DC` | `Washington DC` |
{: caption="Table 1. {{site.data.keyword.mon_full_notm}} regions" caption-side="bottom"}

## Platform metrics overview
{: #platform_metrics-pm}

You can configure only one instance of the {{site.data.keyword.mon_full}} service per region to collect platform metrics. Platform metrics are enabled by default in all instances, and cannot be disabled.

- Provision an instance of the {{site.data.keyword.mon_full_notm}} service. After you provision the Monitoring instance, the *Observability* page opens. To continue working with {{site.data.keyword.cloud_notm}}, go back to the {{site.data.keyword.cloud_notm}} UI.
- To configure the Monitoring instance, you must turn on the *platform metrics* configuration setting.
- If a Monitoring instance in a region is already enabled to collect platform metrics, metrics from enabled-monitoring services are collected automatically and available for monitoring through this instance. For more information about enabled-monitoring services, see [{{site.data.keyword.cloud}} services](https://www.ibm.com/consulting/cloud).
- Use the Metrics Router to allow customers to configure which Sysdig instance their platform metrics flows to. To learn more about Metrics Router, see [IBM Cloud Metrics Routing](/docs/metrics-router).

To monitor platform metrics, check that the Monitoring instance is provisioned in the same region where the {{site.data.keyword.cloud_notm}} instance is provisioned.
{: important}

## Viewing metrics
{: #view_metrics}

To monitor {{site.data.keyword.dns_short}} metrics, you must launch the {{site.data.keyword.mon_full_notm}} web UI instance that is enabled for platform metrics in the region where your {{site.data.keyword.cloud_notm}} instance is available.
{: note}

You can use different options to launch the {{site.data.keyword.mon_full_notm}} web UI and monitor metrics that are described in the following section.

### Launching {{site.data.keyword.mon_full_notm}} web UI from the Observability page
{: #view_metrics_opt2}

Complete the following steps to launch the {{site.data.keyword.mon_full_notm}} web UI from the *Observability* page:

1. [Launch the {{site.data.keyword.mon_full_notm}} web UI](/docs/monitoring?topic=monitoring-launch).
2. Click **DASHBOARDS**.
3. In the **Default Dashboards** section, expand **{{site.data.keyword.IBM_notm}}**.
4. Choose the {{site.data.keyword.dns_short}} Dashboard from the list.

    You can also reach your deployment's {{site.data.keyword.mon_full_notm}} Dashboard from {{site.data.keyword.mon_full_notm}} in the sidebar, under {{site.data.keyword.IBM_notm}}.

    Next, change the scope or make a copy of the *Default* dashboard to monitor an {{site.data.keyword.dns_short}} instance.

## {{site.data.keyword.dns_short}} metrics dictionary
{: #metrics_dictionary-pm}

DNS Services collects two levels of platform metrics from two locations within the data path; the data path and custom resolvers. By default, you'll receive only the summary of metrics which gives a minimum amount of information about DNS query requests, DNS query results, and custom resolver location health.

Open a Network Support case to enable the total metrics set.

Platform metrics are priced per usage.

Enabling the total metrics set increases the amount of metrics you receive, and can incur a greater cost depending on your usage.
{: note}

### Data path summary metrics
{: #datapath-summary-metrics}

The data path summary metrics provide the request count and response count with the corresponding response codes.

|Metric name | Labels |
|----------|-------------|
|`ibm_dns_svcs_dns_requests_summary` | not available |
|`ibm_dns_svcs_dns_responses_summary` | rtype |
{: caption="Table 2. Data path metrics summary" caption-side="bottom"}

The labels correspond to the following definitions:

* **rtype** - Response type: NOERROR, SERVFAIL, and so on

### Data path total platform metrics
{: #datapath-total-metrics}

Data path total platform metrics collect the following set of metrics in a {{site.data.keyword.dns_short}} instance:

|Metric name | Labels |
|----------|-------------|
| `ibm_dns_svcs_dns_requests_total`|qtype, proto, family, accountid, zoneid, zonename, instanceid, vpcid, mtype |
| `ibm_dns_svcs_dns_responses_total`|rtype, accountid, zoneid, zonename, instanceid, vpcid, mtype, cachehit|
{: caption="Table 3. Total DNS requests" caption-side="bottom"}

The labels correspond to the following definitions:

* **qtype** - Resource records type: A, AAAA, CNAME, NS, MX, TXT, and so on
* **rtype** - Response type: NOERROR, SERVFAIL, and so on
* **proto** - Protocol type: UDP or TCP
* **family** - Transport family: IPv4 or IPv6
* **accountid** - ID of the account which owns the DNS Service instance configured for this query
* **zoneid** - ID of the zone for which the DNS query is configured for
* **zonename** - Name of the zone for which the DNS query is configured for
* **instanceid** - ID of the DNS Service instance configured for this query
* **vpcid** - ID of the VPC from which this query originates from
* **mtype** - Metric type: public or private
* **cachehit** - True or false depending on if the response was served from cache

### Custom resolver summary metrics
{: #custom-resolver-summary}

The custom resolver summary provides custom resolver location health.

|Metric name | Labels |
|----------|-------------|
|`ibm_dns_svcs_cr_location_health` | crid, accountid, instanceid, locationip|
|`ibm_dns_svcs_cr_dp_health`|crid, accountid, instanceid, locationip|
{: caption="Table 4. Custom resolver summary metrics" caption-side="bottom"}

Where:
* `ibm_dns_svcs_cr_location_health` is a metric that helps determine the health of critical applications in a custom resolver location. The values are 0 for unhealthy and 1 for healthy.
* `ibm_dns_svcs_cr_dp_health` is a metric that shows the connectivity to the configured default forwarding rule IPs in the custom resolver location. This metric is marked 1 (healthy) when any one of the IPs in the default forwarding rule has connectivity. A 0 (unhealthy) means that none of the IPs in the default forwarding rule have connectivity.

The labels correspond to the following definitions:

* **crid** - The ID of the custom resolver
* **accountid** - The ID of the account which owns the DNS Service instance
* **instanceid** - The ID of the DNS Service instance
* **locationip** - The IP address of the virtual server instance appliance acting as a custom resolver location

### Custom resolver total platform metrics
{: #custom-resolver-total}

The set of metrics associates with DNS resolution through custom resolvers:

| Metric Name | Label |
|----------|-------------|
|`ibm_dns_svcs_cr_dns_requests_total` | server, zone, proto, family, type, crid, accountid, instanceid |
|`ibm_dns_svcs_cr_dns_responses_total` |server, zone, rcode, crid, accountid, instanceid |
|`ibm_dns_svcs_cr_cache_requests_total` | server, crid, accountid, instanceid |
|`ibm_dns_svcs_cr_cache_hits_total` | server, type, crid, accountid, instanceid |
|`ibm_dns_svcs_cr_cache_misses_total` | server, crid, accountid, instanceid |
|`ibm_dns_svcs_cr_forward_requests_total` | to, crid, accountid, instanceid |
|`ibm_dns_svcs_cr_forward_responses_total` | to, rcode, crid, accountid, instanceid |
|`ibm_dns_svcs_cr_location_health` | crid, accountid, instanceid, locationip |
{: caption="Table 5. Custom resolver platform metrics" caption-side="bottom"}

The labels correspond to the following definitions:

* **server** - The forwarding rule that handled this query
* **zone** – The zone the query is for
* **type** - Resource records type: A, AAAA, CNAME, NS, MX, TXT, and so on
* **proto** - Protocol type: UDP or TCP
* **family** - Transport family: IPv4 or IPv6
* **to** – IP of the resolver the request is forwarded to
* **rcode** – Response code of the forwarded query
* **crid** - The ID of the custom resolver the query was handled by
* **accountid** - The ID of the account which owns the DNS Service instance configured for this query
* **instanceid** - The ID of the DNS Service instance configured for this query
* **locationip** – The IP address of the virtual server instance appliance acting as a custom resolver location

## {{site.data.keyword.dns_short}} Dashboard's dictionary
{: #dashboards_dictionary-pm}

The following table outlines the pre-defined dashboards that you can use to monitor {{site.data.keyword.dns_short}} metrics:

| Dashboard name        | Description    |
|-----------------------|----------------|
| **`DNS Services - Metrics Summary`**|The default summary dashboard that opens when you launch {{site.data.keyword.mon_full_notm}} web UI from your service instance UI. |
| **`DNS Services - DP Metrics`**| The default data path dashboard that opens when you launch {{site.data.keyword.mon_full_notm}} web UI from your service instance UI. |
| **`DNS Services - Custom Resolver (CR) Metrics`** |The default custom resolver dashboard that opens when you launch {{site.data.keyword.mon_full_notm}} web UI from your service instance UI.|
{: caption="Table 6. Pre-defined dashboard" caption-side="bottom"}

The *Default* dashboard cannot be changed.
{: important}


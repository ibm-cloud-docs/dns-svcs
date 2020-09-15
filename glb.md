---

copyright:
  years: 2020
lastupdated: "2020-09-15"

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
{:beta: .beta}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Working with global load balancers (Beta)
{: #global-load-balancers}

{{site.data.keyword.dns_full}} provides global load balancing as a service that offers you high availability and geographical distribution of your traffic, based on the health of your origin servers and the geographical region where the user request originates.
{:shortdesc}

For example, in a DNS zone `example.com`, a DNS hostname of `api.example.com` is created as a global load balancer. The hostname `api.example.com` can resolve to different IP addresses based on the location of the requester and the health of the origins. If any or all of the origins (based on policy) are not available in one region, then healthy origins from different regions are returned in response to the DNS query. This ensures a high degree of availability of the hostname `api.example.com`. It also ensures that the load is geographically distributed among different origins and routed regionally.

The open beta version of the global load balancer feature offers limited capabilities so that you can evaluate its functionality. Your assessment helps IBM make beneficial changes before releasing this feature as a GA service.
{:beta}  

## Global load balancers limitations
{: #glb-ki}

The following limitations exist during the Beta period of the global load balancing feature:

* The origins must be on the same subnet as the health monitoring subnet.
* The origin address must be specified by using an IP address and not the hostname.
* One global load balancer, three health checks, and three origin pools per {{site.data.keyword.dns_short}} instance are allowed.
* The origin pools can use no more than two subnets for health monitoring per {{site.data.keyword.dns_short}} instance. 
* Currently, the only health check method that is supported is `GET`.

## Use cases and workflows
{: #glb-use-cases}

The most common use of global load balancers is to direct traffic to healthy origins and distribute loads.

The following workflows are performed from the {{site.data.keyword.dns_short}} zone dashboard. Navigate to the **Global load balancers** tab to view your [load balancers](#x2788902){: term}, origin pools, and [health checks](#x4571658){: term}. 
{: note}

### Creating a global load balancer with origin health monitoring
{: #use-case-no-monitoring}

Creating a global load balancer with origin health monitoring combines high availability with geographic load balancing for mission-critical applications. This workflow ensures that traffic is routed only to healthy origins.

Follow this workflow to create a global load balancer with origin health monitoring:

1. Create a health check.
1. Create an origin pool.
1. Create a global load balancer. 

### Creating a global load balancer without origin health monitoring
{: #use-case-no-monitoring}

In this configuration, {{site.data.keyword.dns_short}} provides geographical load balancing based on the configured policy, but not high availability features. 

After you create a DNS zone and add a permitted network to it, follow this workflow to create a global load balancer:

1. Create an origin pool.
1. Create the global load balancer.

## Creating a health check
{: #add-a-health-check}

Create a health check to specify how the origin health is monitored. {{site.data.keyword.dns_short}} supports HTTP and HTTPS monitoring types. After you create a health check, you can add it to a new or existing origin pool. Health checks exist at the instance level, and can be used by any pool in the instance. 

Follow these steps to create a health check:

1. From the {{site.data.keyword.dns_short}} zone page, click **Global load balancers**, then click **Health checks**. 
1. Click **Create health check** to start.
1. In the **Health check name** field, give your health check a name.
1. Optionally, enter a **Description** for the health check to help you understand what it is monitoring.
1. Select the **Monitor type**. Choose the protocol to use for the health check. Supported monitor types are HTTP and HTTPS. The default value is `HTTP`.
   If **HTTPS** is selected, the **Don't validate certificate** checkbox appears after the **Advanced options** section. Select this box when the HTTPS certificate on the origin is not signed by a certificate authority (for instance, a self-signed certificate).
1. Enter the endpoint **Path** against which to perform the health check. The default value is `/`.
1. Optionally, enter the **Port** number that you want to use.
   For the health check to succeed, a relevant application must be running on the origin that responds to the health monitoring requests.  
   {: note}
1. In the **Advanced settings** section, select a **Test interval** (in seconds) between each health check. Shorter intervals can improve failover time, but increase load on the origins, as checks come from multiple locations. The default value is `60`.
1. Choose a **Method** to use for the health check from the list. The default value is `GET`.
1. Select a **Timeout** interval (in seconds) for how long to wait before the health check is marked as failed. The default value is `5`.
1. Select the **Number of retries** to attempt in case there is a timeout before the origin is marked as unhealthy. Retries are attempted immediately. The default value is `1`.
1. Enter the **Expected response codes**, which are the HTTP response codes or code range of the health check. This value must be between `200-299` with wildcards denoted by an `x`.
1. Optionally, enter a **Response body** which is a case-insensitive substring to match against in the response body. If this string is not found, the origin is marked as unhealthy.
1. In the optional **Request headers** section, you can add and configure HTTP request headers to send in the health check. Enter a header name and value in the fields provided. Click **Add request header** to configure additional headers.
1. Click **Create** to save your changes and create the health check.
 
## Adding an origin pool
{: #add-a-pool}

Origin pools group your origins for the load balancer to use. Decide whether you want to create a monitored or unmonitored origin pool. For monitored pools, you must specify the health check to use, and from which subnet the health is monitored. Origin pools exist at the instance level, and can be used by any global load balancer in any DNS zone that is configured in the instance. 

Before you begin, keep the following considerations in mind when working with origin pools: 

* At least one origin pool is required for each provisioned load balancer. 
* Origins must be on the same subnet as the subnet specified for health monitoring. 
* Only origins with IP addresses can be specified.
* Origin health monitoring continues even when an origin pool is disabled. To disable health monitoring on an origin, you can disable the origin.
* When creating an origin pool, it can take 1 - 10 minutes for the health check to get initiated, during which time the pool appears in a `Critical` state.

You must update your VPC security group to allow traffic from the health monitoring subnet. See [Security groups](#security-groups-glb) for more information.
{:important}
 
To create an origin pool, follow these steps:

1. From the {{site.data.keyword.dns_short}} zone page, click **Global load balancers**, then click **Origin pools**. 
1. Click **Create origin pool**. Pools are enabled by default. 

   Disabling a pool causes any load balancer that uses it to fail over to the next pool, if any. Disabled pools do not receive traffic. 
   {: note}
1. Enter a **Name** for the pool. Only alphanumeric characters, hyphens, and underscores are allowed.
1. Optionally, enter a **Description** for the origin pool.
1. Enable **Origins** to add to the list of origins within this pool. 
1. Give the origin a **Name** and **Address**. Click **Add** to add more pools, and move the toggle to switch the pool off or on. Traffic that is directed at this pool is balanced across all currently healthy origins, provided that the pool itself is healthy. Health checks exclude disabled origins.
1. Select the **Healthy origin threshold**, which is the minimum number of origins that must be healthy for this pool to serve traffic. If the number of healthy origins falls below this number, the pool is marked unhealthy and fails over to the next available pool. The default value is `1`.
1. In the **Health monitoring** section, select a **Health check** to determine what method the health check uses, as well as the health check to use for checking origins within this pool. The default value is no health check.
1. Select a **Health check region** from which the health check performs monitoring. Options are **Dallas**, **WDC**, **Frankfurt**, **London**, and **Tokyo**.
1. Select the **VPC** that contains the subnet from where the health check originates.
1. Choose a **Subnet (Location)**. Select a subnet and location from the list menu. This defines from which subnet the health check is running.
   
   The subnet must be from VPC Gen 2.
   {:note}

1. Click **Create** to save your changes and create your origin pool.
   
When you first create an origin pool, its status is `Critical` and the origin's status is `Down` because the initial health check has not completed yet. The status updates after the health check for the origin completes successfully.
{:note}

### Status definitions
{: #status-definitions}

The following table describes the possible statuses that you might see in your origins, origin pools, and global load balancers. 

|Feature|Status|Definition|
|:------|:-----|:---------|
|Origin| `up` `down`|**Up**: The origin is functioning normally. <br/> **Down**: The origin is down. |
|Origin pool|`healthy` `degraded` `critical` | **Healthy**: All of the origins in the pool are up. <br/>**Degraded**: At least one origin status is down.<br/>**Critical**: The number of healthy origins is less than the healthy origin threshold. For example, if your threshold is `2`, and only one origin is up, the pool status is **Critical**. |
|Global load balancer|`healthy` `degraded` `critical` |**Healthy**: All the origin pools that are associated with the global load balancer are healthy. <br/>**Degraded**: At least one of the origin pools is in degraded status.<br/> **Critical**: The global load balancer status is critical when all of the origin pools associated with the global load balancer are critical.|
{: caption="Table 1. Status definitions for origins, origin pools, and global load balancers" caption-side="top"}

The fallback pool status is not taken into account for assessing the health of the global load balancer. 
{:note}

### Security groups
{: #security-groups-glb}

Update the security group of the VPC to allow incoming health check traffic from the IP address that the health checker on the health monitoring subnet is using. Currently, this can be done by allowing traffic for the whole subnet CIDR.

## Creating a global load balancer
{: #add-a-load-balancer}

Load balancers help to distribute your proxied traffic across multiple origin pools.

Follow these steps to create a load balancer:

To set up a global load balancer, you must first create an origin pool.
{:important}

1. From the {{site.data.keyword.dns_short}} zone page, click **Global load balancers**, then click **Load balancers**.  
1. Click **Create load balancer**.
1. Enter the DNS **Balancer hostname** to associate it with your load balancer. 
1. Optionally, enter a **Description** for the global load balancer.
1. Select the **TTL** (time-to-live) of the DNS entry for the IP address returned by this load balancer. 
1. Add or select a **Default policy**. A default policy specifies which origin pools are used for all availability zones (AZ) for which a location-based policy is not specified. When multiple pools are selected within a policy, you can change their priority by using the arrow keys in the **Priority** column.
1. Add or select a **Fallback policy**. A fallback policy specifies the origin pool to use when all other origin pools in the default or location policy are in a critical state. There can be only one origin pool in the fallback policy.
1. Optionally, add or select a **Location policy**. The location policy allows you to associate one or more origin pools for a specific AZ. Any AZ that is not explicitly defined as a location policy uses the default policy.

## Viewing, editing, or deleting components of a global load balancer
{: #edit-delete-load-balancer}

To view, edit or delete a load balancer, or one of its components, click an action from the overflow menu ![overflow icon](images/horizontal-overflow-icon.png) on the table row of the load balancer.

The following options are provided for each list.

* Health Checks
  * **View health check** - Shows a short summary of the health check with a link that takes you to the edit flow.
  * **Edit health check** - Redirects to the edit flow.
  * **Delete health check** - Shows the confirmation dialog box for the deletion flow.

* Origin Pools
  * **View pool details** - Shows a modal dialog box with information about the pool.
  * **Edit pool** - Redirects to the edit flow.
  * **Delete pool** - Shows the confirmation dialog box for the deletion flow.

* Load Balancers
  * **View load balancer** - Shows all the pools, the pool's priority, and status.
  * **Edit load balancer** - Redirects to the edit flow.
  * **Delete load balancer** - Shows the confirmation dialog box for the deletion flow.
  

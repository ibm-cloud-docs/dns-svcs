---

copyright:
  years: 2025
lastupdated: "2025-10-23"

keywords: HA for dns services, DR for dns-svcs, dns-svcs recovery time objective, dns-svcs recovery point objective

subcollection: content-kit

---

{{site.data.keyword.attribute-definition-list}}

# Understanding high availability and disaster recovery for DNS Services
{: #dns-svcs-ha-dr}



[High availability](#x2284708){: term} (HA) is the ability for a service to remain operational and accessible in the presence of unexpected failures. The main purpose of high availability is to eliminate potential points of failures in an IT infrastructure. [Disaster recovery](#x2113280){: term} is the process of recovering the service instance to a working state. It includes procedures for copying and storing an installed system's essential data in a secure location, and for recovering that data to restore normal operation.
{: shortdesc} 

DNS Services is designed to meet the [Service Level Objectives (SLO)](/docs/resiliency?topic=resiliency-slo#slo-high-network-services) with the Standard plan. DNS Services is a highly available global service, architected with separate failure domains to enhance resilience. The control plane is resilient to both zonal and regional failures, and its failure does not affect the data plane. The data plane is resilient to at least zonal failures, and its failure doesn't affect the control plane.

For more information about the deployment regions and data center locations for DNS Services, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

## High availability architecture
{: #ha-architecture}

### Control plane
{: #ha-control-plane}

{{site.data.keyword.dns_full}} is a globally available (GA) service. Its public API endpoints for DNS configuration are available through a global load balancer deplyed in two [multizone regions](#x9774820){: term} (MZRs) of {{site.data.keyword.cloud_notm}}, ensuring high availability. These regions are Dallas and Washington, DC. If one region experiences an outage, the global load balancer automatically routes API traffic to the other region. For example, if the Dallas region is unavailable, requests are redirected to other available geographic regions—in this case, Washington, DC.

In the event of a global failure, the control plane is restored with a focus on reducing data loss for resources. Therefore, customers should also plan for disaster recovery.

A control plane handles user-initiated DNS configuration requests, whereas a data plane handles name resolution requests from the Virtual Private Cloud (VPC).
{: note}


### Data plane DNS servers
{: #data-plane-dns-server}

The [DNS servers](/docs/dns-svcs?topic=dns-svcs-service-connection) are distributed globally across multiple MZRs and use anycast IP addresses to optimize latency and ensure high availability. If an availability zone or a entire region experiences an outage, DNS queries are automatically routed to nearest availability zone or region. DNS data is replicated across the following regions to support both latency optimization and high availability:

- Dallas (us-south)
- Washington, D.C. (us-east)
- London (eu-gb)
- Madrid (eu-es)
- Frankfurt (eu-de)
- Osaka (jp-osa)
- Tokyo (jp-tok)
- Toronto (ca-tor)
- Sydney (au-syd)
- Sao Paulo (br-sao)

### Data plane custom resolvers
{: #data-plane-custom-resolvers}

A custom resolver is a regional object composed of zonal objects (custom resolver locations) configured on subnets across zones. A best practice is to deploy custom resolvers to more than one subnet to ensure high availability. It is recommended that you deploy in all three availability zones.

When there is a regional failure, this aspect of the data plane is restored to the state of the resources as represented and persisted in the control plane.

### High availability features
{: #ha-features}

DNS Services supports the following high availability features:

| Feature | Description | Consideration |
| ------- | ----------- | ------------- |
| [Custom resolver locations](/docs/dns-svcs?topic=dns-svcs-cr-res-loc-add) | Manage where your custom resolver deploys. | Only adds resilience to zonal failures. |
{: caption="HA features for DNS Services" caption-side="bottom"}

You can achieve high availability at various levels within your IT infrastructure and across different components of your DNS cluster. The level of availability that is right for you depends on several factors, including your business requirements, the Service Level Agreements (SLAs) that you have with your customers, and the resources that you are willing to expend.

The level of availability that you set up for your cluster impacts your coverage under the [IBM Cloud high availability SLA terms](/docs/overview?topic=overview-slas#slas).

Service Level Objectives (SLOs) define the design points that the {{site.data.keyword.cloud_notm}} services are engineered to meet. {{site.data.keyword.dns_full}} is designed to meet the following availability target.

| Availability target | Target Value   |
| ------------------- | -------------- |
|  Availability % | 99.999% |
{: caption="SLO for DNS Services" caption-side="bottom"}

The SLO is not a warranty and {{site.data.keyword.IBM_notm}} will not issue credits for failure to meet an objective. Refer to the [SLAs for commitments and credits](/docs/overview?topic=overview-slas#slas) that are issued for failure to meet any committed SLAs. For a summary of all SLOs, see [{{site.data.keyword.cloud_notm}} service level objectives](//docs/resiliency?topic=resiliency-slo#slo-high-network-services).

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

See [How IBM Cloud ensures high availability and disaster recovery](/docs/overview?topic=overview-zero-downtime#zero-downtime) to learn more about the high availability and disaster recovery standards in {{site.data.keyword.cloud_notm}}.

## Disaster recovery architecture
{: #disaster-recovery-intro}

Maintaining an external record of your DNS configuration is important for recovering DNS Services in the event of a disaster. Both the backup and restore process can be automated using scripting and the export and import processes in the [Disaster recovery features](/docs/dns-svcs?topic=dns-svcs-dns-svcs-ha-dr#dr-features) table. DNS Services supports Terraform and it can be used to define workloads with parameterized locations and performance. Customers can use IBM Cloud Schematics to build and manage Terraform scripts, which in turn can be used to recover resources in an available location during a disaster.

### Disaster recovery features
{: #dr-features}

{{site.data.keyword.dns_full}} supports the following disaster recovery features:



| Feature | Description | Consideration |
| ------- | ----------- | ------------- |
| [Export DNS resource records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records&interface=ui#ui-export-records) | Export DNS records for a zone to a text file through the dashboard. | Exports only [DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records) for one zone at a time. Does not export load balancer or other non-DNS-record data. |
| [Import DNS resource records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records&interface=ui#ui-import-records)  | Import DNS records on a text file into a zone through the dashboard. | Need to recreate the zone before importing DNS records. |
| External source of truth | DNS zones, permitted networks, DNS resource records, custom resolvers, custom resolver forwarding rules, and more captured in a customer managed configuration files like Terraform scripts, shell scripts or programs. | Customer must create the script or program, and persist the configuration where it can be used during disaster. |
| [Backup and restore](/docs/dns-svcs?topic=dns-svcs-writing-dns-svcs-config-to-file) | Backup a service instance by using customer written script. | Customer must create the script and persist the backup copy where it can be used during recovery. |

### Planning for DR
{: #features-for-disaster-recovery}

As a customer, you are responsible for recovering your DNS Server configuration data in the event of a disaster. You should ensure that you build a disaster recovery plan and consider the following failure scenarios and solutions:



| Failure | Resolution |
| ------- | ---------- |
| Zonal failure | Mitigated for custom resolvers by deploying to multiple locations <BR> Mitigated for DNS Servers by queries answered by the nearest available availability zone. |
| Regional failure | Outage for custom resolvers until one availability zone is restored. <BR>  Mitigated for DNS Servers by queries answered by the nearest available region. |
| Data corruption | Restore service configurations from an external source of truth. |
{: caption="DR scenarios for DNS Services" caption-side="bottom"}

## Your responsibilities for HA and DR
{: #feature-responsibilities}



It is your responsibility to continuously test your plan for HA and DR.

Interruptions in network connectivity and short periods of unavailability of a service might occur. It is your responsibility to make sure that application source code includes [client availability retry logic](/docs/resiliency?topic=resiliency-high-availability-design#client-retry-logic-for-ha) to maintain high availability of the application.
{: note}

Use the following checklists associated with each feature to help you create and practice your plan.

- Custom resolver
   - [ ] Ensure that DNS zones and resource records data is correct and accurate.
   - [ ] Take periodic [backups](/docs/dns-svcs?topic=dns-svcs-writing-dns-svcs-config-to-file) of your DNS zones and resource records.
   - [ ] To achieve high availability, configure custom resolvers with a minimum of two resolver locations. The best practice is to establish one location in each availability zone.
   - [ ] To ensure correct high availability of secondary zones with multiple custom resolver locations, configure your on-prem resolver to allow zone transfers to all custom resolver locations that have been created.

For more information about responsibility ownership between you and {{site.data.keyword.cloud_notm}} for IBM Cloud DNS Services, see [Understanding your responsibilities when using IBM Cloud DNS Services](/docs/dns-svcs?topic=dns-svcs-responsibilities-dns-svcs).

## Change management
{: #dns-services-change-management}

Change management includes tasks, such as configuration changes and deletion.

Grant users and processes the Identity and Access Management (IAM) roles and actions with the least privilege that is required for their work. For more information, see [How can I prevent accidental deletion of services?](/docs/resiliency?topic=resiliency-dr-faq#prevent-accidental-deletion).
{: tip} 

Best practices for managing change also include:
 
* Plan and document changes by maintaining a change log for any modifications that are made to your DNS Services configuration. 
* Create a backup of critical configurations before performing major changes.
* Schedule high-impact changes during low-traffic windows and notify impacted teams.
* Monitor your DNS Services health and metrics to ensure that everything is performing as expected. 

## How IBM helps ensure disaster recovery
{: #ibm-disaster-recovery}

{{site.data.keyword.IBM}} takes specific recovery actions for {{site.data.keyword.dns_full}}, if a disaster occurs.

### How IBM recovers from regional failures
{: #ibm-regional-failure}





{{site.data.keyword.cloud_notm}} has [business continuity](#x3026801){: term} plans in place to provide for the recovery of services within hours, if a disaster occurs. You are responsible for your data backup and associated recovery of your content.

DNS Services provide mechanisms to protect your data and restore service functions. Business continuity plans are in place to achieve targeted [recovery point objective](#x3429911){: term} (RPO) and [recovery time objective](#x3167918){: term} (RTO) for the service. The following table outlines the targets for DNS Services.

| Element of service | RPO | RTO |
| --------------------------- | -------------- | -------------- |
|  Control Plane | 0 | < 60 secs |
|  Data Plane | 0 | < 60 secs |
|  Custom Resolver | 0 | < 60 secs |
|  Database Recovery | 24 hrs | 8 hrs |
{: caption="RPO and RTO for DNS Services" caption-side="bottom"}

If {{site.data.keyword.IBM_notm}} can’t restore the service instance, then you must restore the service as described in the [Disaster recovery architecture](#disaster-recovery-intro).

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region). 

## How IBM maintains services
{: #ibm-service-maintenance}

All upgrades follow {{site.data.keyword.IBM_notm}} service best practices, including recovery plans and rollback processes. Regular maintenance might cause short interruptions, mitigated by [client availability retry logic](/docs/resiliency?topic=resiliency-high-availability-design#client-retry-logic-for-ha). Changes are rolled out sequentially, region by region, and zone by zone within a region. {{site.data.keyword.IBM_notm}} reverts updates at the first sign of a defect. 

IBM provides advance notice for all planned maintenance activities. If a change is expected to affect your workloads, IBM communicates this through official notifications. To stay updated on maintenance, service announcements, and other updates, see the [Monitoring notifications and status](/docs/account?topic=account-viewing-cloud-status) page.

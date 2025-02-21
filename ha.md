---

copyright:
  years: 2021
lastupdated: "2025-02-21"

keywords:

subcollection: repo-name

---

{{site.data.keyword.attribute-definition-list}}

# Understanding high availability for DNS Services
{: #ha}

[High availability](#x2284708){: term} (HA) is a core discipline in an IT infrastructure to keep your apps up and running, even after a partial or full site failure. The main purpose of high availability is to eliminate potential points of failures in an IT infrastructure.
{: shortdesc}

## Responsibilities
{: #ha-responsibilities}

To find out more about responsibility ownership for using IBM Cloud DNS Services, see [Understanding your responsibilities when using IBM Cloud DNS Services](/docs/dns-svcs?topic=dns-svcs-responsibilities-dns-svcs).

## What level of availability do I need?
{: #ha-level}

You can achieve high availability on different levels in your IT infrastructure and within different components of your cluster. The level of availability that is right for you depends on several factors, such as your business requirements, the service level agreements (SLAs) that you have with your customers, and the resources that you want to expend.

{{site.data.keyword.dns_full}} is a GA service that is offered globally. The public API endpoints for DNS configuration are available globally through a global load balancer in two MZRs (Multi Zone Regions) of {{site.data.keyword.cloud_notm}}, providing high availability. The regions are Dallas and Washington, DC. If one region experiences an outage, the global load balancer ensures that the API traffic gets routed to another region. For instance, if the Dallas region experiences an outage, requests get routed to the geographically nearest region, in this case, Washington, DC.

The DNS resolvers are distributed around the world in multiple MZRs with any cast IP addresses for optimizing latencies and providing high availability. If one region experiences an outage, the DNS queries are routed to another region. The data is replicated to the following regions for latency optimization and high availability:

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

A best practice is to deploy custom resolvers to more than one subnet to ensure high availability. It is recommended that you deploy in all three availability zones.

## What level of availability does {{site.data.keyword.cloud_notm}} offer?
{: #ha-service}

The level of availability that you set up for your cluster impacts your coverage under the {{site.data.keyword.cloud_notm}} high availability service level agreement terms.

Service level objectives (SLOs) describe the design points that the {{site.data.keyword.cloud_notm}} services are engineered to meet. _service-name_ is designed to achieve the following availability target.

| Availability target | Target Value   |
|---|---|
|  Availability % | 99.999% |
{: caption="SLO for _service-name_" caption-side="bottom"}

The SLO is not a warranty and {{site.data.keyword.IBM_notm}} will not issue credits for failure to meet an objective. Refer to the SLAs for commitments and credits that are issued for failure to meet any committed SLAs. For a summary of all SLOs, see [{{site.data.keyword.cloud_notm}} service level objectives](/docs/overview?topic=overview-slo).


## Locations
{: #ha-locations}

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

See [How IBM Cloud ensures high availability and disaster recovery](/docs/overview?topic=overview-zero-downtime#zero-downtime) to learn more about the high availability and disaster recovery standards in {{site.data.keyword.cloud_notm}}. You can also find information about [Service Level Agreements](/docs/overview?topic=overview-slas#slas).

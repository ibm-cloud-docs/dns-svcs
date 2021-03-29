---

copyright:
  years: 2020
lastupdated: "2020-07-23"

keywords: HA for DNS Services, DR for DNS Services, high availability for DNS Services, disaster recovery for DNS Services, failover for DNS Services

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


# Understanding high availability and disaster recovery for {{site.data.keyword.dns_short}}
{: #ha-dr}

All {{site.data.keyword.cloud}} general availability (GA) offerings have a Service Level Agreement of 99.99% availability. {{site.data.keyword.dns_full}} is a GA service that is offered globally. The public API endpoints for DNS configuration are available globally through a global load balancer in three MZRs (Multi Zone Regions) of {{site.data.keyword.cloud_notm}}, providing high availability. The regions are **Dallas**, **WDC**, and **Frankfurt**. If one region experiences an outage, the global load balancer ensures that the API traffic gets routed to another region. For instance, if the **Dallas** region experiences an outage, requests get routed to the geographically nearest region, in this case, **WDC**.


The DNS resolvers are distributed around the world in multiple MZRs for optimizing latencies and providing high availability. If one region experiences an outage, the DNS resolvers route DNS requests to another region.
The data is replicated to the following regions for latency optimization and high availability:

* Dallas
* Washington, DC
* London
* Frankfurt
* Osaka
* Tokyo
* Sydney

See [How do I ensure zero downtime?](/docs/overview?topic=overview-zero-downtime#zero-downtime) to learn more about the high availability and disaster recovery standards in {{site.data.keyword.Bluemix_notm}}. You can also find information about [Service Level Agreements](/docs/overview?topic=overview-slas#avail-downtime).

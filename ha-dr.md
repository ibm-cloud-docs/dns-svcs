---

copyright:
  years: 2020, 2021
lastupdated: "2021-10-25"

keywords: HA for DNS Services, DR for DNS Services, high availability for DNS Services, disaster recovery for DNS Services, failover for DNS Services

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}


# Understanding high availability and disaster recovery for {{site.data.keyword.dns_short}}
{: #ha-dr}

All {{site.data.keyword.cloud}} general availability (GA) offerings have a Service Level Agreement of 99.99% availability. {{site.data.keyword.dns_full}} is a GA service that is offered globally. The public API endpoints for DNS configuration are available globally through a global load balancer in two MZRs (Multi Zone Regions) of {{site.data.keyword.cloud_notm}}, providing high availability. The regions are **Dallas** and **Washington, DC**. If one region experiences an outage, the global load balancer ensures that the API traffic gets routed to another region. For instance, if the **Dallas** region experiences an outage, requests get routed to the geographically nearest region, in this case, **Washington, DC**.


The DNS resolvers are distributed around the world in multiple MZRs for optimizing latencies and providing high availability. If one region experiences an outage, the DNS resolvers route DNS requests to another region. The data is replicated to the following regions for latency optimization and high availability:

* Dallas
* Washington, DC
* London
* Frankfurt
* Osaka
* Tokyo
* Sydney

Custom resolvers are deployed to two locations by default, to ensure high availability.

See [How do I ensure zero downtime?](/docs/overview?topic=overview-zero-downtime#zero-downtime) to learn more about the high availability and disaster recovery standards in {{site.data.keyword.Bluemix_notm}}. You can also find information about [Service Level Agreements](/docs/overview?topic=overview-slas#slas).

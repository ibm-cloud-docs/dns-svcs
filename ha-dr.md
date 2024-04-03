---

copyright:
  years: 2020, 2024
lastupdated: "2024-03-21"

keywords: HA for DNS Services, DR for DNS Services, high availability for DNS Services, disaster recovery for DNS Services, failover for DNS Services

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}


# Understanding high availability and disaster recovery for {{site.data.keyword.dns_short}}
{: #ha-dr}

All {{site.data.keyword.cloud}} general availability (GA) offerings have a Service Level Agreement of 99.99% availability. {{site.data.keyword.dns_full}} is a GA service that is offered globally. The public API endpoints for DNS configuration are available globally through a global load balancer in two MZRs (Multi Zone Regions) of {{site.data.keyword.cloud_notm}}, providing high availability. The regions are **Dallas** and **Washington, DC**. If one region experiences an outage, the global load balancer ensures that the API traffic gets routed to another region. For instance, if the **Dallas** region experiences an outage, requests get routed to the geographically nearest region, in this case, **Washington, DC**.

The DNS resolvers are distributed around the world in multiple MZRs with any cast IP addresses for optimizing latencies and providing high availability. If one region experiences an outage, the DNS queries are routed to another region. The data is replicated to the following regions for latency optimization and high availability:

* Dallas (us-south)
* Washington, D.C. (us-east)
* London (eu-gb)
* Madrid (eu-es)
* Frankfurt (eu-de)
* Osaka (jp-osa)
* Tokyo (jp-tok)
* Toronto (ca-tor)
* Sydney (au-syd)
* Sao Paulo (br-sao)

A best practice is to deploy custom resolvers to more than one location to ensure high availability. It is recommended that you deploy in all three availability zones.

See [How do I ensure zero downtime?](/docs/overview?topic=overview-zero-downtime#zero-downtime) to learn more about the high availability and disaster recovery standards in {{site.data.keyword.Bluemix_notm}}. You can also find information about [Service Level Agreements](/docs/overview?topic=overview-slas#slas).

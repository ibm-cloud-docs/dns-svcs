---

copyright:
  years: 2020
lastupdated: "2020-04-10"

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

All {{site.data.keyword.cloud}} general availability (GA) offerings have a Service Level Agreement of 99.99% availability. {{site.data.keyword.dns_full}} is a GA service that is offered globally. The public API endpoints for DNS configuration are available globally through a global load balancer in three MZRs (Multi Zone Regions) of {{site.data.keyword.cloud_notm}}, providing high availability. If one region experiences an outage, then this will ensure that the API traffic gets routed to another region.

The DNS resolvers are distributed around the world in six MZRs for optimizing latencies and providing high availability. If one region experiences an outage, then this will route DNS requests to another region.

See [How do I ensure zero downtime?](/docs/overview?topic=overview-zero-downtime#zero-downtime) to learn more about the high availability and disaster recovery standards in {{site.data.keyword.Bluemix_notm}}. You can also find information about [Service Level Agreements](/docs/overview?topic=overview-slas#avail-downtime).

## Restoring a deleted service instance
{:#restoring-a-deleted-service-instance}

After you delete an instance of {{site.data.keyword.dns_short}}, you can restore the deleted service instance within the data retention period of seven days. After the seven-day period expires, the service instance is permanently deleted.

To view which service instances are available for restoration, use the `ibmcloud resource reclamations` command. To restore a deleted service instance, use the `ibmcloud resource reclamation-restore` command.

Learn more about [managing resources](/docs/resources?topic=resources-manage_resource).
{: note}

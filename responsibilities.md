---

copyright:
  years: 2020, 2024
lastupdated: "2024-03-21"

keywords: responsibilities, ha, high availability, disaster recovery

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Understanding your responsibilities when using {{site.data.keyword.dns_full_notm}}
{: #responsibilities-dns-svcs}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.dns_full}}. For a high-level view of the service types in {{site.data.keyword.Bluemix}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.dns_short}}. For the overall terms of use, see [{{site.data.keyword.cloud_notm}} Terms of Use](/docs/overview?topic=overview-terms).

## IBM's responsibilities
{: #ibm-responsibilities}

- Fulfill requests for {{site.data.keyword.dns_short}} configurations, including DNS zones and resource records.
- Keep your {{site.data.keyword.dns_short}} configuration, including DNS zones and resource records, secure.
- Ensure only permitted VPCs have access to the DNS zone information.
- Provide high availability of DNS zone and resource records configuration data.
- Ensure redundancy of data, enabling Disaster Recovery.
- Provide DNS resolvers for DNS resolution.
- Provide updates of appliance for global load balancer and custom resolvers.

## Customer responsibilities
{: #customer-responsibilities}

- Ensure that DNS zones and resource records data is correct and accurate.
- Take periodic [backups](/docs/dns-svcs?topic=dns-svcs-writing-dns-svcs-config-to-file) of your DNS zones and resource records.
- To achieve high availability, configure custom resolvers with a minimum of two resolver locations. The best practice is to establish one location in each availability zone.
- To ensure correct high availability of secondary zones with multiple custom resolver locations, configure your on-prem resolver to allow zone transfers to all custom resolver locations that have been created.

## Abuse of {{site.data.keyword.dns_full_notm}}
{: #abuse-of-dns-svcs}

Clients must not misuse {{site.data.keyword.cloud}} infrastructure.

Misuse includes:
- Any illegal activity
- Distribution or execution of malware
- Harming {{site.data.keyword.cloud_notm}} infrastructure or interfering with the use of {{site.data.keyword.cloud_notm}} infrastructure
- Harming or interfering with the use of any other service or system
- Unauthorized access to any service or system
- Unauthorized modification of any service or system
- Violation of the personal rights of others

See [{{site.data.keyword.cloud_notm}} Terms of Use](/docs/overview?topic=overview-terms) for overall terms of use.

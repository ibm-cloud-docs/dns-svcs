---

copyright:
  years: 2020
lastupdated: "2020-03-16"

keywords: DNS Services, responsibilities, ha, high availability, disaster recovery

subcollection: dns-svcs

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:term: .term}  
{:generic: data-hd-programlang="generic"}
{:download: .download}  

# Understanding your responsibilities when using {{site.data.keyword.dns_full_notm}}
{: #responsibilities-dns-svcs}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.dns_full}}. For a high-level view of the service types in {{site.data.keyword.Bluemix}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.dns_short}}. For the overall terms of use, see [{{site.data.keyword.Bluemix}} Terms and Notices](/docs/overview/terms-of-use?topic=overview-terms)

## IBM's responsibilities
{: #ibm-responsibilities}

- Fulfill requests for {{site.data.keyword.dns_short}} configurations, including DNS zones and resource records.
- Keep your {{site.data.keyword.dns_short}} configuration, including DNS zones and resource records, secure.
- Ensure only permitted VPCs have access to the DNS zone information.
- Provide high availability of DNS zone and resource records configuration data.
- Ensure redundancy of data, enabling Disaster Recovery.
- Provide DNS resolvers for DNS resolution.

## Customer responsibilities
{: #customer-responsibilities}

- Ensure that DNS zones and resource records data is correct and accurate.
- Take periodic [backups](/docs/dns-svcs?topic=dns-svcs-writing-dns-svcs-config-to-file) of your DNS zones and resource records.

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

See [Cloud Services terms](/docs/overview/terms-of-use?topic=overview-terms) for overall terms of use.

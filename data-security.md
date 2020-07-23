---

copyright:
  years: 2020
lastupdated: "2020-07-21"

keywords: data encryption in dns services, data storage for dns services, bring your own keys for dns services, BYOK for dns services, key management for dns services, key encryption for dns services, personal data in dns services, data deletion for dns services, data in dns services, data security in dns services

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



# Securing your data in {{site.data.keyword.dns_short}}
{: #mng-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.dns_full}}, it is important to know exactly what data is stored and encrypted and how you can delete any stored personal data.
{: shortdesc}

## How your data is stored and encrypted in {{site.data.keyword.dns_short}}
{: #data-storage}

The {{site.data.keyword.dns_short}} data which includes {{site.data.keyword.dns_short}} instance, DNS zone, permitted networks and DNS resource records is encrypted at rest in a Cloudant database. The data is also encrypted in transit using SSL.

## Deleting your data in {{site.data.keyword.dns_short}}
{: #data-delete}

After DNS records are deleted from a DNS zone, they are deleted immediately from the database. The DNS zone itself is retained for seven days from deletion.

### Deleting {{site.data.keyword.dns_short}} instances
{: #service-delete}

{{site.data.keyword.dns_short}} instance data is retained for seven days from deletion.

The {{site.data.keyword.dns_short}} data retention policy describes how long your data is stored after you delete the service. The data retention policy is included in the {{site.data.keyword.dns_short}} service description, which you can find in the [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).

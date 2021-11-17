---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: isolation for dns services, service endpoints for dns services, private network for dns services, network isolation in dns services, non-public routes for dns services, private connection for dns services

subcollection: dns-svcs
---

{{site.data.keyword.attribute-definition-list}}

# Securing your connection to {{site.data.keyword.dns_short}}
{: #service-connection}

The control plane of {{site.data.keyword.dns_full}} is accessed by all customer environments through public endpoints behind {{site.data.keyword.cis_full}}.
Because {{site.data.keyword.dns_short}} is a global service, the service endpoints are not limited to {{site.data.keyword.cloud_notm}} private networks. 
{: shortdesc}


The data plane DNS servers are only accessible on the {{site.data.keyword.cloud_notm}} private network through the IPs `161.26.0.7` and `161.26.0.8`.
 

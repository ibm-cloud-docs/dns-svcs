---

copyright:
  years: 2020
lastupdated: "2020-09-18"

keywords: 

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}


# Why did I get an error when adding a permitted network to a VPC?
{: #troubleshoot-cse-enabled}
{: troubleshoot}
{: support}

You tried to add a permitted network, but got an error that the VPC does not have Cloud Service Endpoint (CSE) enabled.
{: shortdesc}

You are unable to add a permitted network to a VPC.
{: tsSymptoms}

By default, only VPCs created on or after 10/09/2019 are enabled to use DNS Services.
{: tsCauses}

For VPCs created as a permitted network before that date, review [Enabling Cloud Service Endpoints](/support/pages/node/1086243) to contact IBM Support and get the VPC CSE enabled. You are then able to add this VPC for your DNS zone.
{: tsResolve}

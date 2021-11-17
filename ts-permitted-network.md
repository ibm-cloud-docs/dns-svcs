---

copyright:
  years: 2020
lastupdated: "2020-09-18"

keywords: 

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I add a permitted network?
{: #troubleshoot-add-permitted-network}
{: troubleshoot}
{: support} 

You tried to add a permitted network, and couldn't.
{: shortdesc}

You are unable to add a permitted network.
{: tsSymptoms}

You cannot add duplicate zone and networks combinations.
{: tsCauses}

Verify that you are trying to add unique zone and networks combinations.
{: tsResolve}

For example:

- Create zone1.com with network-1
    - Create zone1.com is successful
    - Add network-1 is successful

- Create duplicate zone1.com with network-1
    - Create zone1.com is successful
    - Add network-1 fails

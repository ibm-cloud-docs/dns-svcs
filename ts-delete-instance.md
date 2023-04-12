---

copyright:
  years: 2023
lastupdated: "2023-04-06"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I delete my {{site.data.keyword.dns_short}} instance?
{: #troubleshoot-delete-instance}
{: troubleshoot}
{: support}

You attempted to delete your {{site.data.keyword.dns_short}} instance, but received an error.
{: shortdesc}

You received an error when you tried to delete your {{site.data.keyword.dns_short}} instance. It might be for the following reason.
{: tsSymptoms}

## A permitted network is still in the zone
{: #permitted-network-still-in-zone}

To delete a service instance, you must first remove all permitted networks from zones within the service instance.

Remove all permitted networks in the zone's instance again.
{: tsResolve}

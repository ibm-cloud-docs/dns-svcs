---

copyright:
  years: 2024
lastupdated: "2024-09-12"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Why is my customer resolver DNS view not working?
{: #troubleshoot-dns-view}
{: troubleshoot}
{: support}

You tried to use a DNS view, but it didn't work.
{: shortdesc}

A custom resolver that has a forwarding rule with a DNS view configured is not forwarding or resolving a DNS query properly.
{: tsSymptoms}

[Need content]{: tag-red}
{: tsCauses}

To get the DNS view working properly, take the following steps.
{: tsResolve}

* Check that the DNS view expression is configured correctly
* Verify that the source IP for the DNS query matches the view expression for which it is configured
* Verify that each of the  DNS servers that the view is configured to forward the query to are:
  * reachable from the CR locations
  * setup with the zone information

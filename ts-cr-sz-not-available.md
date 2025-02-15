---

copyright:
  years: 2024
lastupdated: "2025-01-30"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Why are my custom resolver secondary zone records not available in the custom resolver location?
{: #troubleshoot-cr-sz-records-not-in-cr}
{: troubleshoot}
{: support}

You tried to query a custom resolver's secondary zone records, but it doesn't respond.
{: shortdesc}

A custom resolver that has a secondary zone configured is not responding to DNS queries for the configured zone.
{: tsSymptoms}

This issue can occur when there is a misconfiguration in either the on-prem resolver or in the DNS Services instance.
{: tsCauses}

To make the custom resolver secondary zone records available for the configured zones, take the following steps.
{: tsResolve}

* Check that the on-prem DNS server is configured to allow transfers to all custom resolver locations
* Check that the secondary zone in their custom resolver is configured to make the transfer from the correct IP
* Check that the on-prem DNS server can be reached by the custom resolver locations

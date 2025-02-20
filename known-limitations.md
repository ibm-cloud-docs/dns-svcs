---

copyright:
  years: 2019, 2025
lastupdated: "2025-02-20"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Known issues and limitations
{: #limitations-known-issues}

This section details some of the limitations and known issues of {{site.data.keyword.dns_short}}.
{: shortdesc}

* Resolvers cache permitted network details for a zone. The TTL for these cached details is typically 1 hour.
* A zone can have an arbitrary number of levels, but not fewer than two. For example, `ibm.austin.texas.example.com` is a valid zone name, but com is not.
* When creating a DNS zone it is not allowed to have numbers in the top level domain (TLD). This means a zone such as `example.com1` is not valid
* In custom resolvers, disabling all custom resolver locations at the same time may be possible, but is _not recommended_ when the custom resolver is enabled.
* {{site.data.keyword.dns_short}} custom resolver platform metrics do not track secondary zone usage. This means that DNS queries made to a configured custom resolver for a secondary zone will not be counted in the reported metrics. 
* The DNS resolver always looks for a record from the longest matching zone, even though the record might not exist in the longest matching zone but does exist in another non-longest matching zone.

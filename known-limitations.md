---

copyright:
  years: 2019, 2023
lastupdated: "2023-06-07"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Known limitations
{: #known-limitations}

This section details some of the known limitations of {{site.data.keyword.dns_short}}.
{: shortdesc}

* Resolvers cache permitted network details for a zone. The TTL for these cached details is typically 1 hour.
* In custom resolvers, disabling both custom resolver locations at the same time may be possible, but is _not recommended_ when the custom resolver is enabled.
* {{site.data.keyword.dns_short}} custom resolver platform metrics do not track secondary zone usage. This means that DNS queries made to a configured custom resolver for a secondary zone will not be counted in the reported metrics.


---

copyright:
  years: 2019, 2022
lastupdated: "2022-03-21"

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


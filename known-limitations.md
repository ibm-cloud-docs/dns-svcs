---

copyright:
  years: 2019, 2021
lastupdated: "2021-07-14"

keywords:

subcollection: dns-svcs

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}
{:external: target="_blank" .external}

# Known limitations
{: #known-limitations}

This section details some of the known limitations of {{site.data.keyword.dns_short}}.
{:shortdesc}

 * This service is supported for VPCs (Gen1) that are created after 10/8/2019. To use the service for VPCs created before then, [open a Support case](https://www.ibm.com/support/pages/node/1086243).
 * The UI can display a maximum of 1000 resource records. If you have more than 1000, use the [API](https://{DomainName}/apidocs/dns-svcs/records#list-resource-records) or [CLI](/docs/dns-svcs?topic=dns-svcs-cli-plugin-dns-services-cli-commands#list-resource-rec-pagination-example) to get all resource records.
 * Resolvers cache permitted network details for a zone.  The TTL for these cached details is typically 1 hour.
 * In custom resolvers, disabling both custom resolver locations at the same time may be possible, but is _not recommended_ when the custom resolver is enabled.
 * Custom resolvers are supported in following regions:
   * Dallas
   * Washington
   * London
   * Frankfurt
   * Osaka
   * Tokyo
   * Sydney

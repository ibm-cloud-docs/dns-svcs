---

copyright:
  years: 2019, 2020
lastupdated: "2020-06-18"

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

 * When editing a health check in the UI to remove headers, the final remaining header cannot be removed. If you need to remove this header, there are 3 workarounds:
   * From the UI, delete the health check and recreate it without the header.
   * Use the [API](https://{DomainName}/apidocs/dns-svcs/#update-monitor) to remove the headers by sending an empty headers array in the PUT request.
   * Use the [CLI](/docs/dns-svcs?topic=dns-svcs-cli-plugin-dns-services-cli-commands#update-glb-monitor).

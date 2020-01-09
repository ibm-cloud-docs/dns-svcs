---

copyright:
  years: 2019
lastupdated: "2019-12-19"

keywords: known issues, DNS Services

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

 * This service is supported for VPCs (Gen1) that are created after 10/8/2019. To use the service for VPCs created prior to that, follow [this process](https://www.ibm.com/support/pages/node/1086243) to open a support case.
 * When adding a VPC to a permitted network through the UI, you cannot add a VPC from a region that contains more than 8 VPCs. Use the API or CLI to add the VPC directly to the permitted network call using its CRN.

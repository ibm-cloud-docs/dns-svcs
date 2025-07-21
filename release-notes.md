---

copyright:
  years: 2021, 2025
lastupdated: "2025-07-21"

keywords:

subcollection: dns-svcs

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}


# Release notes for {{site.data.keyword.dns_short}}
{: #release-notes}

Use these release notes to learn about the latest updates to {{site.data.keyword.dns_full}} that are grouped by date.
{: shortdesc}

## 13 March 2025
{: #dns-svcs-mar1325}

Montreal region now available
:    Montreal is now a supported region for DNS Services. For more information, see [IBM Cloud region and data center locations for resource deployment](/docs/overview?topic=overview-locations).

## 30 January 2025
{: #dns-svcs-jan3025}
{: release-note}

Profiles for custom resolvers
:   You can now provision [custom resolvers with different profiles](/docs/dns-svcs?topic=dns-svcs-custom-resolver#cr-profile-capabilities).

Custom resolver capacity
:   [Increased limits](/docs/dns-svcs?topic=dns-svcs-custom-resolver#cr-limits) on forwarding rules, secondary zones, and the number of supported DNS records per secondary zone.

View feature for forwarding rules
:   The [view feature](/docs/dns-svcs?topic=dns-svcs-custom-resolver#cr-forwarding-rule-view) enables advanced server block routing functions, such as split DNS.

IXFR for secondary zone transfers
:   Now supports both [IXFR and AXFR transfers](/docs/dns-svcs?topic=dns-svcs-sec-zones-about&interface=ui#sec-zone-config). IXFR incremental zone transfers increase efficiency by only sending the changed zone data instead of the entire set of zone data.

## 21 June 2023
{: #dns-svcs-jun2123}
{: release-note}

Platform metrics feature enabled
:   Added support for platform metrics to DNS Services.

Madrid region support added
:   Added Madrid multi-zone region support.

## 24 August 2022
{: #dns-svcs-aug2422}
{: release-note}

Resolver locations
:   Added UI feature to the custom resolver location settings. You can now change resolver location priority by clicking up or down arrows to reorder the list.

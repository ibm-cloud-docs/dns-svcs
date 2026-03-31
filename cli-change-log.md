---

copyright:
  years: 2022, 2026
lastupdated: "2026-03-13"

keywords: change log for dns services cli, updates to cli

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.dns_short}} CLI change log
{: #cli-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.dns_short}} CLI.
{: shortdesc}

## 06 March 2026
{: #cli-mar2026}

On 6 March 2026, the following features changed in the {{site.data.keyword.dns_short}} CLI:

- Fixed an issue where enabling or disabling GLB origins using [update-glb-pool](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#update-glb-pool) failed with "Access to the subnet is forbidden" when the user did not have VPC permissions.
- Fixed an issue where [dns glbs](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#list-glb) returned an empty list when using certain --per-page values.

## 16 September 2025
{: #cli-sept2025}

On 16 September 2025, the following features changed in the {{site.data.keyword.dns_short}} CLI:

Pagination support has been added to the following DNS Services CLI commands:

- [list-glbs](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#list-glb)
- [list-glb-pools](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#list-glb-pools)
- [list-glb-monitors](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#list-glb-monitors)
        
As part of this update (available in version 0.8.4), the JSON response structure has changed. Users should update their jq filters accordingly:

- list-glb:
   - From: `jq '.[] | .name'`
   - To: `jq '.load_balancers[] | .name'`

- list-glb-pools:
   - From: `jq '.[] | .name'`
   - To: `jq '.pools[] | .name'`

- list-glb-monitors:
   - From: `jq '.[] | .name'`
   - To: `jq '.monitors[] | .name'`
   
- Fixed issues and improved pagination handling for GLB-related commands.

## 06 March 2025
{: #cli-mar2025}

On 6 March 2025, the following features changed in the {{site.data.keyword.dns_short}} CLI:

- Added support for 3xx, 4xx, and 5xx response codes for GLB monitors.
  
  This update allows GLB monitors to accept a wider range of HTTP response codes beyond 2xx.

## 12 October 2022
{: #cli-oct2022}

On 12 October 2022, the following features changed in the {{site.data.keyword.dns_short}} CLI:
- Added IBM Power and Z binary support
- Adopt service context-based restrictions

## 20 July 2022
{: #cli-jul2022}

[Secondary zones](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#secondary-zones) support added.

## 14 April 2022
{: #cli-apr1422}

The minimum interval for `glb-monitor-update` has been updated to from 5 seconds to 60 seconds.

## 07 June 2021
{: #cli-jun0721}

All references to the variable `INSTANCE_NAME` have been changed to `INSTANCE`.

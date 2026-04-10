---

copyright:
  years: 2022, 2026
lastupdated: "2026-04-10"

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

- Enabled support for managing GLB origins using [update-glb-pool](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#update-glb-pool) without requiring VPC permissions.
- Fixed an issue where [dns glbs](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#list-glb) could return an empty list when using specific `--per-page` values.

## 16 September 2025
{: #cli-sept2025}

Added pagination support to the following DNS Services CLI commands:

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

## 06 March 2025
{: #cli-mar2025}

- Added support for 3xx, 4xx, and 5xx response codes for GLB monitors.

## 11 December 2024
{: #cli-dec2024}

- Added support for managing views in forwarding rules. You can now add, update, remove, and reorder views when working with forwarding rules.
- Added support for custom resolver profiles.
- Fixed an issue where forwarding rules failed when the forward_to value was empty.
- Improved CLI behavior with fixes to error messages, PTR handling, and lifecycle attributes.

## 30 May 2023
{: #cli-may2023}

- Added pagination support for forwarding rules. For more information, see [forwarding rules CLI command](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#list-custom-resolver-forwarding-rules).
- Added support for filtering resource records by name or type when listing records. For more information, see [resource records CLI command](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#list-resource-record).

## 12 October 2022
{: #cli-oct2022}

- Added IBM Power and Z binary support.
- Adopted service context-based restrictions. For more information, see [Protecting DNS Services resources with context-based restrictions](/docs/dns-svcs?topic=dns-svcs-cbr).

## 20 July 2022
{: #cli-jul2022}

- Added [Secondary zones](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#secondary-zones) support.
- Added support for cross-account operations, allowing resources such as VPCs to be managed across different accounts.

## 14 April 2022
{: #cli-apr1422}

- Updated the minimum interval for `glb-monitor-update` from 5 seconds to 60 seconds.

## 07 June 2021
{: #cli-jun0721}

- Changed all references to the variable `INSTANCE_NAME` to `INSTANCE`.
- Added support for custom resolver CLI commands.

## 25 August 2020
{: #cli-aug2020}

- Added support for Global Load Balancer (GLB), including load balancer and pool management capabilities.
- Added support for specifying a resource group during instance creation using the CLI.

## 27 December 2019
{: #cli-dec2019}

- Introduced initial CLI support, including commands for managing instances, zones, and access control lists (ACLs).
- Added support for managing resource records, with additional options for record operations.
- Added support for VPC-related operations, including displaying VPC information.

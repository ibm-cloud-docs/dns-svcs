---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-12"

keywords: change log for dns services cli, updates to cli

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.dns_short}} CLI change log
{: #cli-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.dns_short}} CLI.
{: shortdesc}

## 16 September 2025
{: #cli-sept2025}

On 16 September 2025, the following features changed in the {{site.data.keyword.dns_short}} CLI:

Pagination support has been added to the following DNS Services CLI commands:

- [list-glbs](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#list-glb)
- [list-glb-pools](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#list-glb-pools)
- [list-glb-monitors](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#list-glb-monitors)
        
As part of this update (available in version 0.8.4), the JSON response structure has changed. Users should update their jq filters accordingly:

- list-glb:
   - From: jq '.[] | .name'
   - To: jq '.load_balancers[] | .name'

- list-glb-pools:
   - From: jq '.[] | .name'
   - To: jq '.pools[] | .name'

- list-glb-monitors:
   - From: jq '.[] | .name'
   - To: jq '.monitors[] | .name'

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

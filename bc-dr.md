---

copyright:
  years: 2021
lastupdated: "2025-02-21"

keywords:

subcollection: repo-name

---

{{site.data.keyword.attribute-definition-list}}

# Understanding business continuity and disaster recovery for DNS Services
{: #bc-dr}

[Disaster recovery](#x2113280){: term} involves a set of policies, tools, and procedures for returning a system, an application, or an entire data center to full operation after a catastrophic interruption. It includes procedures for copying and storing an installed system's essential data in a secure location, and for recovering that data to restore normalcy of operation.
{: shortdesc}

## Responsibilities
{: #bc-dr-responsibilities}

To find out more about responsibility ownership for using IBM Cloud DNS Services, see [Understanding your responsibilities when using IBM Cloud DNS Services](/docs/dns-svcs?topic=dns-svcs-responsibilities-dns-svcs).

## Disaster recovery strategy
{: #bc-dr-strategy}

{{site.data.keyword.cloud_notm}} has [business continuity](#x3026801){: term} plans in place to provide for the recovery of services within hours if a disaster occurs. You are responsible for your data backup and associated recovery of your content.

DNS Services provide mechanisms to protect your data and restore service functions. Business continuity plans are in place to achieve targeted [recovery point objective](#x3429911){: term} (RPO) and [recovery time objective](#x3167918){: term} (RTO) for the service. The following table outlines the targets for DNS Services.

| Disaster recovery objective | Target Value   |
|---|---|
|  RPO | 1 hour   |
|  RTO | 24 hours  |
{: caption="RPO and RTO for DNS Services" caption-side="bottom"}

## Locations
{: #ha-locations}

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

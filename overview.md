---

copyright:
  years: 2019, 2025
lastupdated: "2025-03-13"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# About {{site.data.keyword.dns_short}}
{: #about-dns-services}

To better understand {{site.data.keyword.dns_full}}, it helps to know more about DNS in general.
{: shortdesc}

## DNS overview
{: #dns-overview}

Computers on a network can find one another by IP addresses. To make it easier to work within a computer network, people can use a Domain Name System (DNS) to associate human-friendly domain names with IP addresses, similar to a phonebook. A DNS can also associate other information beyond just computer network addresses to domain names.

That way, people can use human friendly domain names instead of obscure, hard-to-remember, machine-oriented data.

## {{site.data.keyword.dns_short}} overview
{: #dns-services-overview}

{{site.data.keyword.dns_short}} allow you to
* Create private DNS zones that are collections for holding domain names.
* Create DNS resource records under these DNS zones.
* Specify access controls used for the DNS resolution of resource records on a zone-wide level.

{{site.data.keyword.dns_short}} also maintains its own worldwide set of DNS resolvers. Instances that are provisioned under {{site.data.keyword.cloud_notm}} on an {{site.data.keyword.cloud_notm}} network can use resource records that are configured through
{{site.data.keyword.dns_full_notm}} by querying {{site.data.keyword.dns_short}} resolvers.

Resource records and zones that are configured through {{site.data.keyword.dns_short}} are
* Separated from the wider, public DNS and their publicly accessible records.
* Hidden from machines outside of and not part of the {{site.data.keyword.cloud_notm}} private network.
* Accessible only from machines that you authorize on the {{site.data.keyword.cloud_notm}} private network.
* Resolvable only via the resolvers provided by the service.

## Clock synchronization
{: #clock-sync}

ISO 27001 requires that clocks of all relevant information processing systems within an organization or security domain must be synchronized with a single reference time source. {{site.data.keyword.dns_short}} synchronizes the systems with Network Time Protocol (NTP) servers to ensure that all time-based activities occur synchronously everywhere on the network.

IBM {{site.data.keyword.dns_short}} uses the following internal NTP servers:
* `time.adn.networklayer.com`
* `systemd-timesyncd.service`

## Resolving DNS names with {{site.data.keyword.dns_short}}
{: #resolving-dns-names-with-dns-services}

![Diagram of DNS services overview](images/dns-svcs-overview.png "Diagram of {{site.data.keyword.dns_short}} overview"){: caption="A diagram of {{site.data.keyword.dns_short}} workflow" caption-side="bottom"}


As an example, consider that a DNS zone `example.com` is created in your DNS instance, and a resource record for `www` has been defined as shown in Figure 1. Also consider that a VPC 1 has been added to the DNS zone as a permitted network.

When the {{site.data.keyword.dns_short}} server receives a name resolution request for `www.example.com` from a client in VPC 1, the {{site.data.keyword.dns_short}} resolver determines that the request originated from a VPC that is a permitted network for the `example.com` DNS zone, and resolves the name `www.example.com` to the IP `10.0.0.1`.

If the name resolution request for `www.example.com` originated from a client in VPC 2 that is _not_ added as a permitted network to `example.com`, the request is forwarded to a public DNS server, and the response from public DNS server is returned to the VPC client. The scenario is referred to as a Split Horizon, where the same hostname, which is defined in both a private DNS zone and a public DNS zone, can be resolved to different IPs depending on where the DNS name resolution request originated.

{{site.data.keyword.dns_short}} ensures a level of privacy for information that is specified in your zones and resource records.

{{site.data.keyword.dns_short}} is private only. For provisioning and configuring DNS records for public DNS resolution, refer to [{{site.data.keyword.cis_full_notm}}](/docs/cis?topic=cis-about-ibm-cloud-internet-services-cis) ({{site.data.keyword.cis_short_notm}}).
{: note}

## Limits
{: #limits}

{{site.data.keyword.dns_short}} has limits in some areas, which are noted in the following table.

|Item| Limitation|
|----|-----------|
|DNS zones |10 per service instance|
|DNS records| 3500 per DNS zone|
|Permitted networks| 10 per DNS zone|
|Global load balancers| 25 per DNS zone|
|DNS queries per second| 1000 per availability zone|
{: caption="DNS Services limitations" caption-side="bottom"}

## DNS Services supported regions
{: #supported-regions}

| Region | Data replication region | [Health check region](/docs/dns-svcs?topic=dns-svcs-global-load-balancers#add-a-pool) | Permitted networks |
| ------ | ------------- | --- |-------------------|
| Dallas (us-south) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) |
| Washington, D.C. (us-east) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) |
| London (eu-gb) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) |
| Frankfurt (eu-de) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) |
| Madrid (eu-es) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) | 
| Montreal (ca-mon) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) |
| Osaka (jp-osa) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) |
| Tokyo (jp-tok) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) |
| Toronto (ca-tor) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) |
| Sydney (au-syd) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) |
| Sao Paulo (br-sao) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) | ![check icon](../icons/checkmark-icon.svg) |
{: caption="Regions supported by DNS Services" caption-side="bottom"}

---

copyright:
  years: 2020
lastupdated: "2020-09-18"

keywords: 

subcollection: dns-svcs

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:support: data-reuse='support'}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}
{:troubleshoot: data-hd-content-type='troubleshoot'}


# Why did I get an NXDOMAIN error on name resolution?
{: #troubleshoot-nxdomain}
{: troubleshoot}
{: support} 

You tried to perform a domain name resolution, but it didn't work.
{:shortdesc}

You receive an NXDOMAIN error when performing domain name resolution.
{: tsSymptoms}
  
NXDDOMAIN errors happen when a request to resolve a domain is sent to the DNS and the request can't be resolved to an IP address. An NXDOMAIN error message means that the domain does not exist.
{: tsCauses}
 
* Verify {{site.data.keyword.dns_short}} is configured correctly and that access to `161.26.0.7` and `161.26.0.8` is available from within the virtual server instance using the following `dig` command: `$ dig @161.26.0.7 yourzone.com`.
* Verify the server you are sending the request from is configured to use one of these DNS resolvers: `161.26.0.7` or `161.26.0.8`.
* Verify the server you are sending the request from is part of a VPC that has been added as a permitted network to the DNS zone.
* Verify the FQDN for which name resolution is attempted has a resource record in the DNS zone.
* Verify the DNS request is using the correct resource record type in the query.
{: tsResolve}



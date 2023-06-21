---

copyright:
  years: 2020, 2023
lastupdated: "2023-02-02"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Why did I get an NXDOMAIN error on name resolution?
{: #troubleshoot-nxdomain}
{: troubleshoot}
{: support}

You tried to perform a domain name resolution, but it didn't work. Your response can vary depending on whether the domain name resolution is the first query attempt, or across multiple query attempts.
{: shortdesc}

## NXDOMAIN error on the first query
{: #first-query}

You tried to perform a domain name resolution for the first time, but you receive an NXDOMAIN error.
{: tsSymptoms}

NXDDOMAIN errors happen when a request to resolve a domain is sent to the DNS and the request can't be resolved to an IP address. An NXDOMAIN error message means that the domain does not exist.
{: tsCauses}

* Verify {{site.data.keyword.dns_short}} is configured correctly and that access to `161.26.0.7` and `161.26.0.8` is available from within the virtual server instance by using the following `dig` command: `$ dig @161.26.0.7 yourzone.com`.
* Verify the server that you are sending the request from is configured to use one of these DNS resolvers: `161.26.0.7` or `161.26.0.8`.
* Verify the server that you are sending the request from is part of a VPC that has been added as a permitted network to the DNS zone.
* Verify the FQDN for which name resolution is attempted has a resource record in the DNS zone.
* Verify that the DNS request is using the correct resource record type in the query.
{: tsResolve}

## NXDOMAIN error across multiple query attempts for the same name with custom resolver
{: #multiple-queries}

You tried to perform a domain name resolution multiple times for a given name using a custom resolver, but none of the attempts worked.
{: tsSymptoms}

* You received an NXDOMAIN error across multiple domain name resolution attempts.
* The error persists for many minutes, but less than an hour.
* The first attempt at DNS resolution takes the longest, typically. Most attempts for the same query after the first one take less time to resolve.

For example, an application in your VPC had attempted a domain name resolution to your custom resolver. Your custom resolver responded with an NXODMAIN response from an upstream DNS resolver and had cached that response. Then for subsequent queries, your custom resolver responded with that cached response. Because resolving from cache is faster, subsequent DNS queries that were resolved through the custom resolver's cache took less time. The TTL has a 30-minute maximum for the negative cache for the custom resolver, which is currently not a configuration parameter.
{: tsCauses}

Avoid caching a negative DNS response in the resolver for that query before the period in which applications expect to intentionally make queries and get good responses. For example:
{: tsResolve}

* Add the DNS resource record that is associated with the queried name _before_ the applications make that first DNS query.
* Add the DNS resource record that is associated with the queried name, then wait until the negative cache entry on the custom resolver expires. Resume DNS queries, and maintain access to resource records for that DNS name.


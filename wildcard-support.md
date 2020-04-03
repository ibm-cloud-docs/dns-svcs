---

copyright:
  years: 2020
lastupdated: "2020-03-16"

keywords: dns-svcs, DNS Services, Private DNS, wildcard, wildcard records

subcollection: dns-svcs

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:tip: .tip}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:download: .download}

# Working with wildcard records
{: #what-are-wildcard-records}

A wildcard DNS record helps match non-existent domain names within a particular DNS Zone. Wildcard domain names always contain an asterisk label, which is the `*` character only. In order for a domain name to be considered a wildcard domain name, the asterisk label must be the lowest (or first) label. An asterisk in any other place is not treated as a wildcard.

* Wildcard record format
  * `<*>.<hostname.zone | zone>`

* Valid wildcard record examples 
  * `*.example.com 900 IN A 20.20.20.20`
  * `*.foo.example.com 900 MX mailserver.example.com`

* Invalid wildcard record examples
  * `foo.*.example.com 900 IN A 20.20.20.20`
  * `foo*.example.com 900 MX mailserver.example.com`
  * `*foo.example.com 900 IN A 1.2.3.4`

## How wildcard records work
{: #how-wildcard-records-work}

Only use wildcard data if no other resource records match the qname. Similarly, do not use wildcard data if the record type does not match the qtype, even if the resource record matches the qname.

For example, a type `A` query for the name `www.example.com` is made with wildcard: `*.example.com  900 IN A 20.20.20.20`. 
  * If there is no resource record of the name `www.example.com`, it matches with the wildcard record. 
  * The wildcard is matched only if the domain does not exist. 

## Limitations
{: #wildcard-limitations}

* A zone cannot contain more than 5 wildcard records.
* Only the following wildcard record following types are allowed:
  * `A` 
  * `AAAA` 
  * `MX`
* PTR records are not supported for `A` and `AAAA` type wildcard records. 

## Managing wildcard DNS records
{: #managing-wildcard-records}

You can manage a wildcard record the same way as any other record. Refer to [Managing DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records) for more information on creating, reading, updating, and deleting wildcard records. 

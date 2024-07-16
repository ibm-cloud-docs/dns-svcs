---

copyright:
  years: 2020, 2024
lastupdated: "2024-07-16"

keywords: wildcard records

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

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

Use wildcard data only if no other resource records match the Qname. Similarly, do not use wildcard data if the record type does not match the Qtype, even if the resource record matches the Qname.

For example, a type `A` query for the name `www.example.com` is made with wildcard: `*.example.com  900 IN A 20.20.20.20`.
* If there is no resource record of the name `www.example.com`, it matches with the wildcard record.
* The wildcard is matched only if the domain does not exist.

## Limitations
{: #wildcard-limitations}

* A zone cannot contain more than five wildcard records.
* Wildcard records are only allowed for the following record types.
    * `A`
    * `AAAA`
    * `CNAME`
    * `MX`
* PTR records are not supported for `A` and `AAAA` type wildcard records.
* [Importing DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records&interface=api#import-resource-records-api) does not support wildcard records.
* To avoid causing conflicts when importing a DNS zone file, do not create or delete DNS records until the import is complete.
* When importing a DNS zone file, ensure that no other import operations occur that might cause a conflict.

## Managing wildcard DNS records
{: #managing-wildcard-records}

You can manage a wildcard record the same way as any other record. Refer to [Managing DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records) to learn more about creating, reading, updating, and deleting wildcard records.

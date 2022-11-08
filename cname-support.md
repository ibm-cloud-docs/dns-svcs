---

copyright:
  years: 2022
lastupdated: "2022-11-04"

keywords: cname records

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Working with CNAME records
{: #what-are-cname-records}

A Canonical Name record (CNAME), is a record that points to another domain address rather than an IP address. A CNAME record points to another DNS record which, in turn, points to an A record which points to an IP address. Then, if the IP address ever changes, you only have to record the change in one place within the network.

* Valid CNAME record examples:
    * `ftp.example.com 900 IN CNAME example.com`
    * `sftp.example.com 900 IN CNAME example.com`

* Invalid CNAME record examples (MX record should not point to another CNAME record):
   * `example.com.      MX     0   foo.example.com.`
   * `foo.example.com.  CNAME  host.example.com.`

## How CNAME records work
{: #how-CNAME-records-work}

A CNAME is an alias. It allows one domain to point to another domain which, if you follow the CNAME chain, eventually resolves to an A record and IP address.
Pointing a CNAME record to another CNAME record is inefficient (but possible) because it requires multiple DNS lookups before the domain can be loaded, negatively impacting the speed of the user experience. 

Each resource record in the CNAME chain is considered as a separate DNS query, which slows down the resolution time.

For example, use CNAME records to point `ftp.example.com` and `sftp.example.com` to the DNS entry for `example.com`, which in turn has an A record that points to the IP address:

```sh
ftp.example.com CNAME example.com
example.com A 10.1.1.10
```
{: codeblock}

The following is an example of a long CNAME chain that is a combination of private zones and public zones.

* Private zones
    * `foo.com`
    * `bar.com`
* Public zones
    * `prod.com`
    * `containers.appdomain.cloud`

```sh
abc.foo.com CNAME abc.bar.com
abc.bar.com CNAME new.prod.com
new.prod.com CNAME 1234.containers.appdomain.cloud
1234.containers.appdomain.cloud A 10.10.24.4
```
{: codeblock}

Longer CNAME chains, with or without global load balancers, increase the DNS response times. Typically, DNS clients have a 2-second default query timeout, so the client will timeout and will retry the query when resolution takes longer than 2 seconds.

## Limitations
{: #cname-limitations}

* MX and NS records can't point to a CNAME record; they must point to an A record (for IPv4) or an AAAA record (for IPv6).
* The CNAME chain length should not be greater than 5.
* The CNAME can’t share the same name as another record type for a single domain.
* You can't have mulitple CNAME records with the same name in the same domain.

## Managing CNAME DNS records
{: #managing-CNAME-records}

You can manage a CNAME record in the same way as you manage any other record. To learn more about creating, reading, updating, and deleting CNAME records, see [Managing DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records). 

---

copyright:
  years: 2019, 2025
lastupdated: "2025-05-08"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Managing DNS records
{: #managing-dns-records}

DNS records make the connection between human-readable names and IP addresses. We cover how to manage DNS records in the following sections. Manage DNS records by using the UI, CLI, or API.
{: shortdesc}

## Adding DNS records in the console
{: #adding-dns-records}
{: ui}

1. From the DNS zones table, click the zone name to which you want to add record(s). More details about the selected zone appear.
2. Click **Add Record** to display a panel where you can create a record.

You can use the **Type** menu to select the type of record that you want to create. Each DNS record type has a Name and Time-To-Live (TTL) associated with it.

When you enter a name in the Name field, a domain name is automatically appended if you did not add one manually. For example, if you type `www` or `www.example.com` in the Name field, the API handles both entries as `www.example.com`. If you enter the exact domain name into the name field, then it won't append to itself (for example, `example.com` is handled as `example.com`). However, the list of DNS records shows only the names, without the domain name added on. As a result, `www.example.com` displays as `www` and `example.com` as `example.com`.

The minimum supported TTL value is `1 min` and the maximum is `12 hours`. The default value of TTL is `15 min`, but users can change it.
{: note}

### Add an A type record in the console
{: #a-record}
{: ui}

To add this record type, valid values must exist in the **Name** and **IPv4 Address** fields. Specify a **TTL** value from the list menu, with a default value of `15 min`.

Required fields
* Name
* IPv4 Address
* TTL (Default value is 15 min)

### Add an AAAA type record in the console
{: #aaaa-record}
{: ui}

To add this record type, valid values must exist in the **Name** and **IPv6 Address** fields. Specify a **TTL** value from the list menu, with a default value of `15 min`.

Required fields
* Name
* IPv6 Address
* TTL (Default value is 15 min)

### Add an CNAME type record in the console
{: #cname-record}
{: ui}

To add this record type, a valid value must exist in the **Name** field and a fully qualified domain name must be in the **Target** (FQDN) field. A **TTL** can also be specified from the list menu, with the default value of `15 min`.

Required fields
* Name
* Target (for CNAME)
* TTL (Default value is 15 min)

### Add an MX Type record in the console
{: #mx-record}
{: ui}

To add this record type, a valid value must exist in the **Name** field, a fully qualified domain name must be in the **Mail Server** (FQDN) field, and a valid number must exist in the **Priority** field. Specify a **TTL** value from the list menu, with a default value of `15 min`.

Required fields
* Name
* Mail Server
* TTL (Default value is 15 min)
* Priority (Default value is 1)

### Add an PTR type record in the console
{: #ptr-record}
{: ui}

To add this record type, you must have an existing A or AAAA record that is not already associated with another PTR record. Select an existing record from the list menu. Specify a **TTL** value from the list menu, with a default value of `15 min`.

Required fields
* Select existing record
* TTL (Default value is 15 min)

### Add an SRV type record in the console
{: #srv-record}
{: ui}

To add this record type, valid values must exist in the **Name**, **Service Name**, and **Target** fields. Use the list menu to select a **protocol**, which defaults to the UDP protocol. Additionally, you can specify **Priority**, **Weight**, and **Port**. These three fields default to a value of `1`. Specify a **TTL** value from the list menu, with a default value of `15 min`.

Required fields
* Name
* Service Name
* Target
* TTL (Default value is 15 min)
* Protocol (Default value is UDP)
* Priority (Default value is 1)
* Weight (Default value is 1)
* Port (Default value is 1)

### Add an TXT type record in the console
{: #txt-record}
{: ui}

To add this record type, valid values must exist in the **Name** and **Content** fields. Specify a **TTL** value from the list menu, with a default value of `15 min`.

For security and privacy reasons, it is recommended that you not use TXT type records for sensitive and confidential data.
{: important}

Required fields
* Name
* Content
* TTL (Default value is 15 min)

## Update DNS records in the console
{: #updating-dns-records}
{: ui}

In each record row, click the **Edit** icon to open a panel where you can update the record.

## Delete DNS records in the console
{: #deleting-dns-records}

In each record row, click the **Delete** icon to open a panel where you can confirm the delete process.

## Import resource records in the console
{: #ui-import-records}
{: ui}

To import resource records, take the following steps:

1. From your DNS Services instance, select the zone to which you want to import records
1. Click **Select record action** in the zone details section and choose **Import records**
1. You can drag and drop the import file into the panel that appears, or click the link to upload from your computer

    Import files must be plain text format, and cannot exceed 8 MB
    {: note}

1. Click **Import records**

Your import file should follow this sample format:

```sh
www.test.com.  900 IN  A   127.0.0.1
www.test.com.  900 IN  AAAA    ::1
w3.test.com.   900 IN  CNAME   mydomain.com.
www.test.com.  900 IN  MX  1 mail.example.com.
_service._tcp.www.sample.com.   900 IN  SRV 1 1 1 mydomain.com.
www.test.com.  900 IN  TXT "my content"
```
{: codeblock}

After the records are imported, you can review the details of the import status, including the number of files that successfully uploaded and which records could not be uploaded. If you need to upload additional files, click **Upload more files** and repeat the import steps. Click the **X** icon in the top right of the panel to close the import panel.

## Export resource records in the console
{: #ui-export-records}
{: ui}

To export resource records, take the following steps:

1. From your DNS Services instance, select the zone from which you want to export records
1. Click **Select record action** in the zone details section and choose **Export records**
1. Enter a name for your exported file, or accept the default name of `records.txt`
1. Click **Download**

The exported file is downloaded to the default download location specified by your browser.

## Managing DNS reconrds from the CLI
{: #managing-dns-records-cli}
{: cli}

First use the `ibmcloud dns instance-target` command to set the target operating DNS Services instance.

```bash
$ ibmcloud dns instances
Retrieving service instances for service 'dns-svcs' ...
OK

Name                 ID                                     Location   State    Service Name
DNS Services-km      ffffffff-b042-41fd-885e-000000000000   global     active   dns-svcs

$ ibmcloud dns instance-target "DNS Services-km"
```

Store the zone ID in a variable so you can use it in following commands without having to type it every time. For example, to store the zone ID in a variable, run this command:

```bash
DNS_ZONE_ID="example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae"
```
{: pre}

## Create a type `A` resource record from the CLI
{: #create-resource-record-cli}
{: cli}

Use the `ibmcloud dns resource-record-create` command with `--type A` option to create a type `A` resource record. `--name`, and `--ipv4` are the mandatory options.

```bash
$ ibmcloud dns resource-record-create $DNS_ZONE_ID --type A --name www --ipv4 192.168.1.100
Creating resource record in zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK

ID            A:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6
Name          www.example.com
Type          A
Created On    2020-04-10 09:12:07.858707275 +0000 UTC
Modified On   2020-04-10 09:12:07.858707275 +0000 UTC
TTL           900
Data
    ip        192.168.1.100
```
{: pre}

## Create a type 'SRV' resource record from the CLI
{: #create-srv-resource-record-cli}
{: cli}

Use the `ibmcloud dns resource-record-create` command with `--type SRV` option to create a type `SRV` resource record. `--name`, `--service`, `--protocol`, and `--target` are the mandatory options.

```bash
$ ibmcloud dns resource-record-create $DNS_ZONE_ID --type SRV --name video --service _sip --protocol tcp --priority 10 --weight 10 --port 953 --target media.example.com
Creating resource record in zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK

ID             SRV:c7c8938b-87c7-4aee-95fa-63f28452c8d4
Name           _sip._tcp.video.example.com
Type           SRV
Created On     2020-04-10 09:15:56.940189115 +0000 UTC
Modified On    2020-04-10 09:15:56.940189115 +0000 UTC
TTL            900
Data
    port       953
    priority   10
    target     media.example.com
    weight     10
```
{: pre}

## Create a type 'TXT' resource record from the CLI
{: #create-txt-resource-record-cli}
{: cli}

Use the `ibmcloud dns resource-record-create` command with `--type TXT` option to create a type `TXT` resource record. `--name` and `--text` are mandatory options.

```bash
$ ibmcloud dns resource-record-create $DNS_ZONE_ID --type TXT --name text --text "This is a text record."
Creating resource record in zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK

ID            TXT:92648285-c7e5-49ef-bf8b-a5be91d5c5d3
Name          text.example.com
Type          TXT
Created On    2020-04-10 09:16:50.169135062 +0000 UTC
Modified On   2020-04-10 09:16:50.169135062 +0000 UTC
TTL           900
Data
    text      This is a text record.
```
{: pre}

## Create a type 'MX' resource record from the CLI
{: #create-amx-resource-record-cli}
{: cli}

Use `ibmcloud dns resource-record-create` command with `--type MX` option to create a type `MX` resource record. `--name` and `--exchange` are the mandatory options.

```bash
$ ibmcloud dns resource-record-create $DNS_ZONE_ID --type MX --name mail --preference 10 --exchange exchange.example.com
Creating resource record in zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK

ID               MX:900750bf-881d-402f-a482-20447f2e64a2
Name             mail.example.com
Type             MX
Created On       2020-04-10 09:18:08.299278244 +0000 UTC
Modified On      2020-04-10 09:18:08.299278244 +0000 UTC
TTL              900
Data
    preference   10
    exchange     exchange.example.com
```
{: pre}

## Create a type 'PTR' resource record from the CLI
{: #create-ptr-resource-record-cli}
{: cli}

Use `ibmcloud dns resource-record-create` command with `--type PTR` option to create a type `PTR` resource record. `--name` and `--ptrdname` are the mandatory options.

```bash
$ ibmcloud dns resource-record-create $DNS_ZONE_ID --type PTR --name 192.168.1.100 --ptrdname www.example.com
Creating resource record in zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK

ID             PTR:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6
Name           192.168.1.100
Type           PTR
Created On     2020-04-10 09:34:49.722454606 +0000 UTC
Modified On    2020-04-10 09:34:49.722454606 +0000 UTC
TTL            900
Data
    ptrdname   www.example.com
```
{: pre}


## Create a type 'CNAME' resource record from the CLI
{: #create-cname-resource-record-cli}
{: cli}

Use `ibmcloud dns resource-record-create` command with `--type CNAME` option to create a type `CNAME` resource record. `--name` and `--cname` are mandatory options.

```bash
$ ibmcloud dns resource-record-create $DNS_ZONE_ID --type CNAME --name web --cname www.example.com
Creating resource record in zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK

ID            CNAME:6e80f079-effd-409a-a520-b8c1b10f6e6e
Name          web.example.com
Type          CNAME
Created On    2020-04-10 09:36:13.186040793 +0000 UTC
Modified On   2020-04-10 09:36:13.186040793 +0000 UTC
TTL           900
Data
    cname     www.example.com
```
{: pre}

## Create a type 'AAAA' resource record from the CLI
{: #create-aaaa-resource-record-cli}
{: cli}

Use `ibmcloud dns resource-record-create` command with `--type AAAA` option to create a type `AAAA` resource record. `--name` and `--ipv6` are mandatory options.

```bash
$ ibmcloud dns resource-record-create $DNS_ZONE_ID --type AAAA --name www --ipv6 2019::2020
Creating resource record in zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK

ID            AAAA:37e1e701-e549-4ca1-8c22-86574bf4aaed
Name          www.example.com
Type          AAAA
Created On    2020-04-10 09:37:15.063814601 +0000 UTC
Modified On   2020-04-10 09:37:15.063814601 +0000 UTC
TTL           900
Data
    ip        2019::2020
```
{: pre}

## Get a resource record from the CLI
{: #get-resource-record-cli}
{: cli}

Use `ibmcloud dns resource-record` command followed by the zone ID and resource record ID to get details of a resource record.

```bash
$ ibmcloud dns resource-record $DNS_ZONE_ID A:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6
Getting resource record 'A:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6' in zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK

ID            A:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6
Name          www.example.com
Type          A
Created On    2020-04-10 09:12:07.858707275 +0000 UTC
Modified On   2020-04-10 09:34:49.986883927 +0000 UTC
TTL           900
Data
    ip        192.168.1.100
```
{: pre}

## List resource records from the CLI
{: #list-resource-records-cli}
{: cli}

Use `ibmcloud dns resource-records` command followed by the zone ID to list all resource records.

```bash
$ ibmcloud dns resource-records $DNS_ZONE_ID
Listing resource records in zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK
ID                                           Name                          Type    TTL
AAAA:37e1e701-e549-4ca1-8c22-86574bf4aaed    www.example.com               AAAA    900
CNAME:6e80f079-effd-409a-a520-b8c1b10f6e6e   web.example.com               CNAME   900
MX:900750bf-881d-402f-a482-20447f2e64a2      mail.example.com              MX      900
TXT:92648285-c7e5-49ef-bf8b-a5be91d5c5d3     text.example.com              TXT     900
SRV:c7c8938b-87c7-4aee-95fa-63f28452c8d4     _sip._tcp.video.example.com   SRV     900
A:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6       www.example.com               A       900
PTR:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6     192.168.1.100                 PTR     900
```
{: pre}


## Update a resource record from the CLI
{: #update-resource-record-cli}
{: cli}

Use `ibmcloud dns resource-record-update` command followed by the zone ID and resource record ID to update a resource record.

```bash
$ ibmcloud dns resource-record-update $DNS_ZONE_ID A:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6 --name www --ipv4 10.10.1.1
Updating resource record 'A:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6' in zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK

ID            A:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6
Name          www.example.com
Type          A
Created On    2020-04-10 09:12:07.858707275 +0000 UTC
Modified On   2020-04-10 09:40:55.204076727 +0000 UTC
TTL           900
Data
    ip        10.10.1.1
```
{: pre}


## Delete a resource record from the CLI
{: #delete-resource-record-cli}
{: cli}

Use `ibmcloud dns resource-record-delete` command followed by the zone ID and resource record ID to delete a resource record.

```bash
$ ibmcloud dns resource-record-delete $DNS_ZONE_ID PTR:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6
Really delete resource record 'PTR:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6' in zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km'? [y/N]> y
Deleting resource record 'PTR:f20cfe91-b936-4bad-a8d1-f7afa4ac32a6' in zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK
```
{: pre}

## Manage DNS Records with the API
{: #managing-dns-records-api}
{: api}

First store the API endpoint in a variable so you can use it in API requests without having to type the full URL. For example, to store the production endpoint in a variable, run this command:

```bash
DNSSVCS_ENDPOINT=https://api.dns-svcs.cloud.ibm.com
```
{: pre}

To verify that this variable was saved, run `echo $DNSSVCS_ENDPOINT` and ensure that the response is not empty.

## Create a type `A` resource record with the API
{: #create-resource-record-api}
{: api}

### Request
{: #create-a-request}
{: api}

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
    "name":"www.example.com",
    "type":"A",
    "rdata": {
            "ip":"1.2.6.7"
        },
    "ttl":300
}'
```
{: pre}

### Response
{: #create-a-response}

```json
{
    "id": "fa57d5d0-7729-4770-af27-6d7f8dce860c",
    "created_on": "2019-08-12 08:03:03.910471016 +0000 UTC",
    "modified_on": "2019-08-12 08:03:03.910471016 +0000 UTC",
    "rtype": "A",
    "ttl": 300,
    "name": "www.example.com",
    "id": "A:fa57d5d0-7729-4770-af27-6d7f8dce860c",
    "rdata": {
        "ip": "1.2.6.7"
    }
}
```
{: codeblock}

## Create a type 'SRV' resource record with the API
{: #create-srv-resource-record-api}
{: api}

### Request
{: #create-srv-request}
{: api}

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
    "type": "SRV",
    "name": "example.com",
    "service": "srv",
    "protocol": "udp",
    "rdata": {
        "priority": 100,
        "weight": 100,
        "port": 8000,
        "target": "siphost.com"
    }
}'
```
{: pre}

### Response
{: #create-srv-response}
{: api}

```json
{
    "created_on": "2019-08-16 08:07:41.113606 +0000 UTC",
    "modified_on": "2019-08-16 08:07:41.113606 +0000 UTC",
    "rtype": "SRV",
    "ttl": 60,
    "name": "example.com",
    "id": "SRV:7562b1f9-1a6a-4189-b794-dd84c91d6a28",
    "rdata": {
        "priority": 100,
        "weight": 100,
        "port": 8000,
        "target": "siphost.com"
    },
    "service": "srv",
    "protocol": "udp"
}
```
{: codeblock}

## Create a type 'TXT' resource record with the API
{: #create-txt-resource-record-api}
{: api}

### Request
{: #create-txt-request}

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
    "type": "TXT",
    "name": "txt.example.com",
    "rdata": {
        "txtdata": "txt strings"
    }
}'
```
{: pre}

### Response
{: #create-txt-response}
{: api}

```json
{
    "created_on": "2019-08-16 08:15:53.360664 +0000 UTC",
    "modified_on": "2019-08-16 08:15:53.360664 +0000 UTC",
    "rtype": "TXT",
    "ttl": 60,
    "name": "txt.example.com",
    "id": "TXT:c6221d5f-69d7-4717-9951-4f69b2680fd4",
    "rdata": {
        "txtdata": "txt strings"
    }
}
```
{: codeblock}

### Create a type 'MX' resource record with the API
{: #create-amx-resource-record-api}
{: api}

### Request
{: #create-mx-request}
{: api}

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
    "type": "MX",
    "name": "mx1.example.com",
    "rdata": {
        "exchange": "mailserver.example.com",
        "preference": 10
    }
}'
```
{: pre}

### Response
{: #create-mx-response}
{: api}

```json
{
    "created_on": "2019-08-16 08:21:20.308716 +0000 UTC",
    "modified_on": "2019-08-16 08:21:20.308716 +0000 UTC",
    "rtype": "MX",
    "ttl": 60,
    "name": "mx1.example.com",
    "id": "MX:8e1b201e-00dd-46a0-a3ec-46573f908870",
    "rdata": {
        "preference": 10,
        "exchange": "mailserver.example.com"
    }
}
```
{: codeblock}

## Create a type 'PTR' resource record with the API
{: #create-ptr-resource-record-api}
{: api}

### Request
{: #create-ptr-request}

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
    "type": "PTR",
    "name": "192.168.10.100",
    "rdata": {
       "ptrdname": "www1.example.com"
    }
}'
```
{: pre}

### Response
{: #create-ptr-response}

```json
{
    "created_on": "2019-08-30 06:48:16.971764628 +0000 UTC",
    "modified_on": "2019-08-30 06:48:16.971764628 +0000 UTC",
    "rtype": "PTR",
    "ttl": 60,
    "name": "100.10.168.192.in-addr.arpa",
    "id": "PTR:a47dd63a-e65a-4280-8f53-3cdb433cc78a",
    "rdata": {
        "ptrdname": "www1.example.com"
    }
}
```
{: codeblock}

## Create a type 'CNAME' resource record with the API
{: #create-cname-resource-record-api}
{: api}

### Request
{: #create-cname-request}

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
    "type": "CNAME",
    "name": "cname.example.com",
    "rdata": {
       "cname": "clientinterface.com"
    }
}'
```
{: pre}

### Response
{: #create-cname-response}
{: api}

```json
{
    "created_on": "2019-08-16 08:29:36.710416 +0000 UTC",
    "modified_on": "2019-08-16 08:29:36.710416 +0000 UTC",
    "rtype": "CNAME",
    "ttl": 60,
    "name": "cname.example.com",
    "id": "CNAME:c95916ba-5504-499a-943a-21f5befe92b5",
    "rdata": {
        "cname": "clientinterface.com"
    }
}
```
{: codeblock}


## Creating a type 'AAAA' resource record with the API
{: #create-aaaa-resource-record-api}
{: api}

### Request
{: #create-aaaa-request}
{: api}

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
    "type": "AAAA",
    "name": "test.example.com",
    "rdata": {
       "ip": "8000::2000"
    }
}'
```
{: pre}

### Response
{: #create-aaaa-response}
{: api}

```json
{
    "created_on": "2019-08-16 08:34:38.311539 +0000 UTC",
    "modified_on": "2019-08-16 08:34:38.311539 +0000 UTC",
    "rtype": "AAAA",
    "ttl": 60,
    "name": "test.example.com",
    "id": "AAAA:894e165b-f066-434d-9b58-4afc2dca62c9",
    "rdata": {
        "ip": "8000::2000"
    }
}
```
{: codeblock}

## Get a resource record with the API
{: #get-resource-record-api}
{: api}

### Request
{: #get-rec-request}
{: api}

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records/$RECORD_ID \
  -H "Authorization: $TOKEN"
```
{: pre}

### Response
{: #get-rec-response}
{: api}

```json
{
    "created_on": "2019-08-12 08:03:03.910471016 +0000 UTC",
    "modified_on": "2019-08-12 08:03:32.875065176 +0000 UTC",
    "rtype": "A",
    "ttl": 300,
    "name": "www.example.com",
    "id": "A:fa57d5d0-7729-4770-af27-6d7f8dce860c",
    "rdata": {
        "ip": "9.4.6.7"
    }
}
```
{: codeblock}

## List resource records with the API
{: #list-resource-records-api}
{: api}

### Request
{: #list-rec-request}
{: api}

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records?limit=50&offset=0 \
  -H "Authorization: $TOKEN"
```
{: pre}

### Response
{: #list-rec-response}
{: api}

```json
{
    "offset": 0,
    "limit": 50,
    "total_count": 1,
    "first": {
      "href": "https://api.dns-svcs.cloud.ibm.com/v1/instances/ec0c4ee2-5d1f-4066-bcf2-dc9f3122c638/dnszones/example.com:4759caa4-d4fa-4fb9-7848-f463de19b392/resource_records?limit=50"
    },
    "resource_records": [
        {
            "created_on": "2019-08-30 04:10:25.092468565 +0000 UTC",
            "modified_on": "2019-08-30 04:10:25.092468565 +0000 UTC",
            "rtype": "A",
            "ttl": 60,
            "name": "www.example.com",
            "id": "A:ec0c4ee2-5d1f-4066-bcf2-dc9f3122c639",
            "rdata": {
                "ip": "192.168.10.100"
            }
        }
    ]
}
```
{: codeblock}

## Update a resource record with the API
{: #update-resource-record-api}
{: api}

### Request
{: #update-rec-request}
{: api}

```bash
curl -X PUT \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records/$RECORD_ID \
  -H "Authorization: $TOKEN" \
  -d '{
    "name":"www",
    "rdata": {
            "ip":"7.7.7.7"
        },
    "ttl":300
}'
```
{: pre}

### Response
{: #update-rec-response}
{: api}

```json
{
    "created_on":"2019-09-10 20:03:25.249355942 +0000 UTC",
    "modified_on":"2019-09-11 16:13:17.350043736 +0000 UTC",
    "rtype":"A",
    "ttl":300,
    "name":"www",
    "id":"A:139eb9f3-c646-4eb6-92fa-3ddabfb1b84f",
    "rdata":{
        "ip":"7.7.7.7"
    }
}
```
{: codeblock}

## Delete a resource record with the API
{: #delete-resource-record-api}
{: api}

### Request
{: #delete-rec-request}
{: api}

```bash
curl -X DELETE \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records/$RECORD_ID \
  -H "Authorization: $TOKEN"
```
{: pre}

### Response
{: #delete-rec-response}
{: api}

```json
HTTP 204 is returned, no content in response.
```
{: codeblock}

## Import bulk resource records from a DNS zone file with the API
{: #import-resource-records-api}
{: api}

### Request
{: #import-bulk-request}
{: api}

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/import_resource_records --form "file=@./bind.cfg" \
  -H "Authorization: $TOKEN"
```
{: pre}

### Response
{: #import-bulk-response}
{: api}

```json
{
    "total_records_parsed": 17,
    "records_added": 17,
    "records_failed": 0,
    "records_added_by_type": {
        "A": 10,
        "AAAA": 2,
        "CNAME": 4,
        "SRV": 0,
        "TXT": 0,
        "MX": 0,
        "PTR": 1
    },
    "records_failed_by_type": {
        "A": 0,
        "AAAA": 0,
        "CNAME": 0,
        "SRV": 0,
        "TXT": 0,
        "MX": 0,
        "PTR": 0
    },
    "message": null,
    "errors": null
}
```
{: codeblock}

## Export bulk resource records to a DNS zone file with the API
{: #export-resource-records-api}
{: api}

### Request
{: #export-bulk-request}
{: api}

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/export_resource_records -o dns_records.cfg \
  -H "Authorization: $TOKEN"
```
{: pre}

#### Response
{: #export-bulk-response}
{: api}

```json
HTTP 200 is returned with zone file content in byte format
```
{: codeblock}

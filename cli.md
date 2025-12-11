---

copyright:
  years: 2019, 2025
lastupdated: "2025-12-11"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.dns_short}} CLI reference
{: #dns-services-cli-commands}

Follow these instructions to use the {{site.data.keyword.dns_full}} command line interface (CLI).
{: shortdesc}

## Before you begin
{: #cli-ref-prereqs}

Complete these steps to use the {{site.data.keyword.dns_short}} CLI, which is implemented as an {{site.data.keyword.cloud_notm}} CLI plug-in. This plug-in provides you with the means to manage your service instance and its associated resources through a command line user interface. 

1. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli#install-ibmcloud-cli){: external}.
1. Install or update the `cloud-dns-services` plug-in to the {{site.data.keyword.cloud_notm}} CLI.

    To install the plug-in, enter the following command.

    ```sh
    ibmcloud plugin install cloud-dns-services
    ```
    {: pre}

    To update:

    ```sh
    ibmcloud plugin update cloud-dns-services
    ```
    {: pre}

    To view installed plug-ins and versions

    ```sh
    ibmcloud plugin list
    ```
    {: pre}



## Instances
{: #resource-instance}

Manage DNS Services instances by using the following `instance` commands.

### `ibmcloud dns instances`
{: #list-dns-services-instances}

List all DNS Services instances.

```sh
   ibmcloud dns instances [--output FORMAT]
```
{: pre}

#### Command option
{: #command-options-list-dns-services-instances}

`--output`
:   Specify the output format. Currently, `json` is the only supported format.

### `ibmcloud dns instance-target`
{: #set-context-DNS-service-instance}

Set the context service instance to operate.

```sh
   ibmcloud dns instance-target [INSTANCE] [--unset]
```
{: pre}

#### Command options
{: #command-options-set-context-dns-service-instance}

INSTANCE
:   The name or ID of a DNS Services instance. If it is present, set the context instance to `operate`; if not, show the current context instance.

--unset
:   Unset context instance.


### `ibmcloud dns instance-create`
{: #create-DNS-services-instance}

Create a DNS Services instance.

   Use `ibmcloud target -g RESOURCE_GROUP` to set the target resource group before you create a DNS Services instance. Use `ibmcloud resource groups` to view the list of available resource groups.
   {: note}


```sh
   ibmcloud dns instance-create INSTANCE_NAME PLAN [-g, --resource-group RESOURCE_GROUP] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-create-dns-svcs-instance}

INSTANCE_NAME
:   The name of the DNS Services instance.

PLAN
:   The name or ID of a service plan.

-g, --resource-group
:   The name or ID of a resource group.

--output
:   Specify the output format. Currently, `json` is the only supported format.

### `ibmcloud dns instance-update`
{: #update-DNS-services-instance}

Update a DNS Services instance.

```sh
   ibmcloud dns instance-update INSTANCE [--name NAME] [--plan PLAN] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-update-dns-svcs-instance}

INSTANCE
:   The name or ID of a DNS Services instance.

--name
:   The DNS Services instance name.

--plan
:   The name or ID of a DNS Services plan. Use `ibmcloud dns plans` to get available plans.

--output
:   Specify the output format. Currently, `json` is the only supported format.


### `ibmcloud dns instance-delete`
{: #delete-DNS-services-instance}

Delete a DNS Services instance.

```sh
   ibmcloud dns instance-delete INSTANCE [--force] 
```
{: pre}

#### Command options
{: #command-options-delete-dns-svcs-instance}

INSTANCE
:   The name or ID of a DNS Services instance.

--force
:   Delete an instance without prompting for confirmation.


### `ibmcloud dns instance`
{: #get-DNS-service-instance}

Show details of a DNS Services instance.

```sh
   ibmcloud dns instance INSTANCE [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-get-dns-svcs-instance}

INSTANCE
:   The name or ID of a DNS Services instance.

--output
:   Specify output format, only JSON is supported.


### `ibmcloud dns plans`
{: #list-DNS-services-plans}

List all DNS Services instances.

```sh
   ibmcloud dns plans
```
{: pre}

## Zones
{: #zone}

Manage DNS zones by using the following `zone` commands.

### `ibmcloud dns zone-create`
{: #create-zone}

Create a DNS zone.

```sh
   ibmcloud dns zone-create ZONE_NAME [-d, --description DESC] [-l, --label LABEL] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #options-create-dns-svcs-zone}

ZONE_NAME
:   The name of the DNS zone.

-d, --description
:   The text that describes the purpose of a DNS zone.

-l, --label
:   The label of a DNS zone.

-i, --instance INSTANCE
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output FORMAT
:   Specify the output format. Currently, `json` is the only supported format.

### `ibmcloud dns zone`
{: #get-zone}

Get the DNS zone details.

```sh
   ibmcloud dns zone ZONE_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #options-get-zone}

ZONE_ID
:   The ID of the DNS zone.

-i, --instance INSTANCE
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output FORMAT
:   Specify the output format. Currently, `json` is the only supported format.
  
### `ibmcloud dns zone-update`
{: #update-zone}

Update a DNS zone's description and label.

```sh
   ibmcloud dns zone-update ZONE_ID [-d, --description DESC] [-l, --label LABEL] [--instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #options-update-zone}

ZONE_ID
:   The ID of the DNS zone.

-d, --description
:   The text that describes the purpose of a DNS zone.

-l, --label
:   The label of a DNS zone.

-i, --instance INSTANCE
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output FORMAT
:   Specify the output format. Currently, `json` is the only supported format.

### `ibmcloud dns zone-delete`
{: #delete-zone}

Delete a DNS zone.

```sh
   ibmcloud dns zone-delete ZONE_ID [-i, --instance INSTANCE] [-f,--force]
```
{: pre}

#### Command options
{: #options-delete-zone}

ZONE_ID
:   The ID of the DNS zone.

-i, --instance INSTANCE
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

-f, --force
:   Delete a zone without prompting for confirmation.

### `ibmcloud dns zones`
{: #list-zones}

List all DNS zones for a service instance.

```sh
   ibmcloud dns zones [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #options-list-zones}

-i, --instance INSTANCE
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output FORMAT
:   Specify the output format. Currently, `json` is the only supported format.

## Permitted networks
{: #permitted-network}

Manage permitted networks by using the following `permitted-network` commands.

### `ibmcloud dns permitted-network-add`
{: #add-permitted-network}

Add a permitted network for a DNS zone.

```sh
   ibmcloud dns permitted-network-add ZONE_ID --vpc-crn VPC_CRN [--type TYPE] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #options-add-permitted-network}

ZONE_ID
:   The ID of the DNS zone.

--type
:   The permitted network type. Valid values: `vpc`.

--vpc-crn
:   The CRN of the VPC instance.

-i, --instance INSTANCE
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output FORMAT
:   Specify the output format. Currently, `json` is the only supported format.

### `ibmcloud dns permitted-network`
{: #get-permitted-network}

Get the permitted network details.

```sh
   ibmcloud dns permitted-network ZONE_ID PERMITTED_NETWORK_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #options-get-permitted-network}

ZONE_ID
:   The ID of the DNS zone.

PERMITTED_NETWORK_ID
:   The ID of the permitted network.

-i, --instance INSTANCE
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output FORMAT
:   Specify the output format. Currently, `json` is the only supported format.


### `ibmcloud dns permitted-network-remove`
{: #Remove-permitted-network}

Remove a permitted network.

```sh
   ibmcloud dns permitted-network-remove ZONE_ID PERMITTED_NETWORK_ID [-i, --instance INSTANCE] [-f,--force]
```
{: pre}

#### Command options
{: #options-remove-permitted-network}

ZONE_ID
:   The ID of the DNS zone.

PERMITTED_NETWORK_ID
:   The ID of the permitted network.

--instance INSTANCE
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

-f, --force
:   Remove a permitted network without prompting for confirmation.


### `ibmcloud dns permitted-networks`
{: #cli-list-permitted-networks}

List permitted networks for a zone.

```sh
   ibmcloud dns permitted-networks ZONE_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #options-list-permitted-networks}

ZONE_ID
:   The ID of the DNS zone.

-i, --instance INSTANCE
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output FORMAT
:   Specify the output format. Currently, `json` is the only supported format.

## Resource records
{: #resource-record}

Manage how the resource record performs using the following `resource-record` commands.

### `ibmcloud dns resource-record-create`
{: #create-resource-record}

Create a resource record for a DNS zone.

```sh
   ibmcloud dns resource-record-create DNS_ZONE_ID (-r, --record-content @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

```sh
   ibmcloud dns resource-record-create DNS_ZONE_ID --type A --name NAME --ipv4 IP_ADDRESS [--ttl TTL]
   ibmcloud dns resource-record-create DNS_ZONE_ID --type AAAA --name NAME --ipv6 IP_ADDRESS [--ttl TTL]
   ibmcloud dns resource-record-create DNS_ZONE_ID --type CNAME --name NAME --cname CNAME [--ttl TTL]
   ibmcloud dns resource-record-create DNS_ZONE_ID --type PTR --name NAME --ptrdname PTRDNAME [--ttl TTL]
   ibmcloud dns resource-record-create DNS_ZONE_ID --type TXT --name NAME --text TEXT [--ttl TTL]
   ibmcloud dns resource-record-create DNS_ZONE_ID --type MX --name NAME --exchange EXCHANGE --preference PREFERENCE [--ttl TTL]
   ibmcloud dns resource-record-create DNS_ZONE_ID --type SRV --name NAME --service SERVICE --protocol PROTOCOL --priority PRIORITY --weight WEIGHT --port PORT --target TARGET  [--ttl TTL]
```
{: codeblock}

#### Command options
{: #options-create-resource-record}

ZONE_ID
:   The ID of the DNS zone.

--name
:   Resource record name.

--type
:   Resource record type.

--ipv4
:   IPv4 address.

--ipv6
:   IPv6 address.

--cname
:   Canonical name.

--ptrdname
:   Hostname of the relevant A or AAAA record.

--text
:   Human readable text.

--exchange
:   Hostname of Exchange server.

--preference
:   Preference of the MX record.

--service
:   The symbolic name of the wanted service, beginning with an underscore `_`.

--protocol
:   The symbolic name of the wanted protocol.

--port
:   Port number of the target server.

--weight
:   Weight of distributing queries among multiple target servers.

--priority
:   Priority of the SRV record.

--target
:   Hostname of the target server.

--ttl
:   Time to live, in seconds. The default value is 900. Valid values: 60, 120, 300, 600, 900, 1800, 3600, 7200, 18000, 43200.

-r, --record-content
:   The JSON file or JSON string that is used to describe a DNS Resource Record. See [Required fields for `-r --record-content`](#required-fields-r-record-content) for more detail.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Required fields for `-r --record-content`
{: #required-fields-r-record-content}

The required field in JSON data is `type`.

Resource record type. Valid values: `A`, `AAAA`, `CNAME`, `PTR`, `TXT`, `MX`, `SRV`.
* For type A, AAAA: Extra required fields are `name`, `rdata`.
    * `name`: Resource record name.
    * `rdata`: Content of the resource record.
      * `ip`: IPv4/IPv6 address
*  Extra optional fields are `ttl`.
    * `ttl`: Time to live in seconds. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

Sample JSON data:

```json
        {
             "name": "testA",
             "type": "A",
             "rdata": {
                 "ip": "1.2.3.4"
                }
        }
```
{: codeblock}

```json
        {
            "name": "testAAAA",
            "type": "AAAA",
            "rdata": {
                "ip": "2001:0db8:0012:0001:3c5e:7354:0000:5db1"
            }
        }
```
{: codeblock}

* For type CNAME: Extra required fields are `name`, `rdata`.
    * `name`: Resource record name.
    * `rdata`: The content of the type-CNAME resource record.
        * `cname`: Canonical name.
* Extra optional fields are `ttl`.
    * `ttl`: Time to live in second. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

Sample JSON data:

```json
        {
            "name": "testCNAME",
            "type": "CNAME",
            "rdata": {
                "cname": "example.com"
            }
        }
```
{: codeblock}

* For type PTR: Extra required fields are `name`, `rdata`.
    * `name`: Resource record name.
    * `rdata`: The content of type-PTR resource record.
        * `ptrdname`: Hostname of the relevant A or AAAA record.
* Extra option fields are `ttl`.
    * `ttl`: Time to live in second. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

Sample JSON data:

```json
        {
            "name": "1.2.3.4",
            "type": "PTR",
            "rdata": {
                "ptrdname": "testA.example.com"
            }
        }
```
{: codeblock}

* For type TXT: Extra required fields are `name`, `rdata`.
    * `name`: Resource record name.
    * `rdata`: The content of type-TXT resource record.
        * `text`: Human readable text.
* Extra optional fields are `ttl`.
    * `ttl`: Time to live in seconds. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

Sample JSON data:

```json
        {
            "name": "testTXT",
            "type":"TXT",
            "rdata": {
                "text": "text information"
            }
        }
```
{: codeblock}


* For type MX: Extra required fields are `name`, `rdata`.
    * `name`: Resource record name.
    * `rdata`: The content of type-MX resource record.
        * `exchange`: Hostname of Exchange server.
        * `preference`: Preference of the MX record
* Extra optional fields are `ttl`.
    * `ttl`: Time to live in seconds. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

Sample JSON data:

```json
        {
           "name": "testMX",
           "type": "MX",
           "rdata": {
                "preference": 10,
                "exchange": "mailserver.example.com"
            }
        }
```
{: codeblock}

* For type SRV: Extra required fields are `name`, `rdata`, `service`, `protocol`.
    * `name`: Resource record name.
    * `rdata`: The content of type-SRV resource record.
        * `priority`: Priority of the SRV record.
        * `weight`: Weight of distributing queries among multiple target servers.
        * `port`: Port number of the target server.
        * `target`: Hostname of the target server.
    * `service`: The symbolic name of the wanted service, starting with an underscore `_`.
    * `protocol`: The symbolic name of the wanted protocol.
* Extra option fields are `ttl`.
    * `ttl`: Time to live in seconds. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

Sample JSON data:

```json
        {
            "type": "SRV",
            "name": "testSRV",
            "rdata": {
                "priority": 100,
                "weight": 100,
                "port": 8000,
                "target": "siphost.com"
            },
            "service": "_sip",
            "protocol": "udp"
        }
```
{: codeblock}

### `ibmcloud dns resource-record-update`
{: #update-resource-record}

Update a resource record for a DNS zone.


```sh
   dns resource-record-update DNS_ZONE_ID RESOURCE_RECORD_ID (-r, --record-content @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

```sh
   ibmcloud dns resource-record-update DNS_ZONE_ID RESOURCE_RECORD_ID --name NAME --ipv4 IP_ADDRESS [--ttl TTL]
   ibmcloud dns resource-record-update DNS_ZONE_ID RESOURCE_RECORD_ID --name NAME --ipv6 IP_ADDRESS [--ttl TTL]
   ibmcloud dns resource-record-update DNS_ZONE_ID RESOURCE_RECORD_ID --name NAME --cname CNAME [--ttl TTL]
   ibmcloud dns resource-record-update DNS_ZONE_ID RESOURCE_RECORD_ID [--ttl TTL]
   ibmcloud dns resource-record-update DNS_ZONE_ID RESOURCE_RECORD_ID --name NAME --text TEXT [--ttl TTL]
   ibmcloud dns resource-record-update DNS_ZONE_ID RESOURCE_RECORD_ID --name NAME --exchange EXCHANGE --preference PREFERENCE [--ttl TTL]
   ibmcloud dns resource-record-update DNS_ZONE_ID RESOURCE_RECORD_ID --name NAME --priority PRIORITY --weight WEIGHT --port PORT --target TARGET  [--service SERVICE] [--protocol PROTOCOL] [--ttl TTL]
```
{: codeblock}

#### Command options
{: #options-update-resource-record}

ZONE_ID
:   The ID of the DNS zone.

RECORD_ID
:   The ID of the record.

--name
:   Resource record name.

--type
:   Resource record type.

--ipv4
:   IPv4 address.

--ipv6
:   IPv6 address.

--cname
:   Canonical name.

--ptrdname
:   Hostname of the relevant A or AAAA record.

--text
:   Human readable text.

--exchange
:   Hostname of Exchange server.

--preference
:   Preference of the MX record.

--service
:   The symbolic name of the wanted service, starting with an underscore `_`.

--protocol
:   The symbolic name of the wanted protocol.

--port
:   Port number of the target server.

--weight
:   Weight of distributing queries among multiple target servers.

--priority
:   Priority of the SRV record.

--target
:   Hostname of the target server.

--ttl
:   Time to live, in seconds. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

-r, --record-content
:   The JSON file or JSON string that is used to describe a DNS Resource Record. See [Required fields for -r, --record-content](#r-record-details) for more detail.

-i, --instance INSTANCE
:   Instance name or ID. If the name is not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output FORMAT
:   Specify output format, only JSON is supported.

#### Required fields for -r, --record-content
{: #r-record-details}

The required field in JSON data is `name`. Resource record name.

PTR records _do not_ need this field.
{: note}

* For type A, AAAA: Extra required fields are `rdata`.
    * `rdata`: Content of the resource record.
        * `ip`: IPv4/IPv6 address
* Extra option fields are `ttl`.
    * `ttl`: Time to live, in seconds. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

Sample JSON data:

```json
        {
             "name": "testA",
             "rdata": {
                 "ip": "1.2.3.4"
            }
        }
```
{: codeblock}

```json
        {
            "name": "testAAAA",
            "rdata": {
                "ip": "2001:0db8:0012:0001:3c5e:7354:0000:5db1"
            }
        }
```
{: codeblock}

* For type CNAME: Extra required fields are `rdata`.
    * `rdata`: The content of type-PTR resource record.
    * `cname`: Canonical name
* Extra option fields are `ttl`.
    * `ttl`: Time to live, in seconds. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

Sample JSON data:

```json
        {
            "name": "testCNAME",
            "rdata": {
                "cname": "example.com"
            }
        }
```
{: codeblock}

* For type PTR: Extra option fields are `ttl`.
    * `ttl`: Time to live, in seconds. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

Sample JSON data:

```json
        {
            "ttl": 360,
        }
```
{: codeblock}

* For type TXT: Extra required fields are `rdata`.
    * `rdata`: The content of type-TXT resource record.
    * `text`: Human readable text.
* Extra optional fields are `ttl`.
    * `ttl`: Time to live, in seconds. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

Sample JSON data:

```json
        {
            "name": "testTXT",
            "rdata": {
                "text": "text information"
            }
        }
```
{: codeblock}

* For type MX: Extra required fields are `rdata`.
    * `rdata`: The content of type-MX resource record.
        * `exchange`: Hostname of Exchange server.
        * `preference`: Preference of the MX record
* Extra optional fields are `ttl`.
    * `ttl`: Time to live, in seconds. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

Sample JSON data:

```json
        {
            "name": "testMX",
            "content": "smtp.example.com",
            "priority": 10
        }
```
{: codeblock}

* For type SRV: Extra required fields are `rdata`, `service`, `protocol`.
    * `rdata`: The content of type-SRV resource record.
        * `priority`: Priority of the SRV record
        * `weight`: Weight of distributing queries among multiple target servers.
        * `port`: Port number of the target server.
        * `target`: Hostname of the target server.
    * `service`: The symbolic name of the wanted service, start with an underscore `_`.
    * `protocol`: The symbolic name of the wanted protocol.
* Extra option fields are `ttl`.
    * `ttl`: Time to live, in seconds. The default value is `900`. Valid values: `60`, `120`, `300`, `600`, `900`, `1800`, `3600`, `7200`, `18000`, `43200`.

Sample JSON data:

```json
        {
            "name": "testSRV"
            "rdata": {
                "priority": 100,
                "weight": 100,
                "port": 8000,
                "target": "siphost.com"
            },
            "service": "_sip",
            "protocol": "udp"
        }
```
{: codeblock}


### `ibmcloud dns resource-record`
{: #get-resource-record}

Get a resource record details for a DNS zone.

```sh
   ibmcloud dns resource-record ZONE_ID RECORD_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #options-get-resource-records}

ZONE_ID
:   The ID of the DNS zone.

RECORD_ID
:   The ID of resource record.

-i, --instance INSTANCE
:   Instance name or ID. If the name is not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output FORMAT
:   Specify the output format. Currently, `json` is the only supported format.

### `ibmcloud dns resource-record-delete`
{: #delete-resource-record}

Delete a resource record for a DNS zone.

```sh
   ibmcloud dns resource-record-delete ZONE_ID RECORD_ID [-i, --instance INSTANCE] [-f,--force]
```
{: pre}

#### Command options
{: #options-delete-resource-records}
  
ZONE_ID
:   The ID of the DNS zone.

RECORD_ID
:   The ID of resource record.

-i, --instance INSTANCE
:   Instance name or ID. If the name is not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

-f, --force
:   Delete resource record without prompting for confirmation.

### `ibmcloud dns resource-records`
{: #list-resource-record}

List all resource records for a DNS zone.

```sh
   ibmcloud dns resource-records ZONE_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #options-list-resource-records}

ZONE_ID
:   The ID of the DNS zone.

--page
:   Page number of paginated results (default 1).

--per-page
:   Number of resource records per page. Min: 50. Max: 1000 (default 200).

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Example command to list resource records with pagination
{: #list-resource-rec-pagination-example}

List all resource records with pagination.

 ```sh
 ibmcloud dns resource-records ZONE_ID --per-page 1000 --page 1
 ```
{: pre}

### `ibmcloud dns resource-records-import`
{: #import-resource-records}

Import resource records from BIND zone file.

```sh
ibmcloud dns resource-records-import DNS_ZONE_ID (--file FILE) [-i, --instance INSTANCE_NAME | INSTANCE_ID] [--output FORMAT]
```
{: pre}

#### Command options
{: #import-resource-records-options}

DNS_ZONE_ID
:   The ID of the DNS zone.

--file
:   BIND zone file to import. Support type: A, AAAA, CNAME, MX, PTR, SRV, TXT.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #import-resource-records-examples}

Import resource records from BIND zone file `dns_records.cfg` in zone `f1d596fc-7e86-4b99-b912-9508167e9e56` for instance `dns-demo`.

```sh
ibmcloud dns resource-records-import f1d596fc-7e86-4b99-b912-9508167e9e56 --file dns_records.cfg -i "dns-demo"
```
{: pre}

### `ibmcloud dns resource-records-export`
{: #export-resource-records}

Export resource records to BIND zone file.

```sh
ibmcloud dns resource-records-export DNS_ZONE_ID [--file FILE] [-i, --instance INSTANCE_NAME | INSTANCE_ID] [--output FORMAT]
```
{: pre}

#### Command options
{: #export-resource-records-options}

DNS_ZONE_ID
:   The ID of the DNS zone.

--file
:   The BIND zone file that saves the exported resource records.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #export-resource-records-examples}

Export resource records in zone `f1d596fc-7e86-4b99-b912-9508167e9e56` to zone file `dns_records.cfg` for instance `dns-demo`.

```sh
ibmcloud dns resource-records-export f1d596fc-7e86-4b99-b912-9508167e9e56 --file dns_records.cfg -i "dns-demo"
```
{: pre}

## Global load balancer
{: #glb}

Manage global load balancers by using the following `glb` commands.

### `ibmcloud dns glb-create`
{: #create-glb}

Create a global load balancer in a zone.

```sh
ibmcloud dns glb-create DNS_ZONE_ID --name NAME --default-pools POOL_LIST --fallback-pool POOL_ID [--description DESCRIPTION] [--enabled true|false] [--ttl TTL] [--az-pools AZPOOLS1 --az-pools AZPOOLS2] [-i, --instance INSTANCE] [--output FORMAT]

ibmcloud dns glb-create DNS_ZONE_ID (-j, --json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #create-glb-options}

DNS_DOMAIN_ID
:   The ID of the DNS zone. Required.

--json
:   The JSON file or JSON string that is used to describe a global load balancer. Required.
    - The required fields in JSON data are `name`, `fallback_pool`, `default_pools`:
      - `name`: The DNS hostname to associate with your load balancer.
      - `fallback_pool`: The pool ID to use when all other pools are detected as unhealthy.
      - `default_pools`: A list of pool IDs ordered by their failover priority.
    - The optional fields are `description`, `ttl`, `az_pools`, `enabled`:
      - `description`: The descriptive text of the load balancer.
      - `ttl`: Time to live (TTL) of the DNS entry for the IP address returned by this load balancer.
      - `az_pools`: A mapping of region and country codes to a list of pool IDs (ordered by their failover priority) for the region.
      - `enabled`: Determines whether or not the load balancer pool is enabled. Valid values: `true`, `false`. The values `on` and `off` are deprecated.

    Sample JSON data:

    ```json
    {
      "name": "glb01",
      "description": "Global load balancer 01",
      "enabled": false,
      "ttl": 300,
      "default_pools": ["cc1deb57-0eb4-45cb-94ce-a3c71c189d12"],
      "fallback_pool": "cc1deb57-0eb4-45cb-94ce-a3c71c189d12",
      "az_pools": [
        {
          "availability_zone": "us-south-1",
          "pools": [
            "0fc0bb7c-2fab-476e-8b9b-40fa14bf8e3d"
          ]
        },
        {
          "availability_zone": "us-south-2",
          "pools": [
            "f46eba57-f08e-4e38-a76c-f3370d457bd2"
          ]
        }
      ]
    }
    ```
    {: codeblock}

--name
:   The DNS hostname to associate with your load balancer.

--fallback-pool
:   The pool ID to use when all other pools are detected as unhealthy.

--default-pools
:   A list of pool IDs ordered by their failover priority.

--description
:   The descriptive text of the load balancer.

--ttl
:   Time to live (TTL) of the DNS entry for the IP address returned by this load balancer.

--az-pools
:   A mapping of region and country codes to a list of pool IDs (ordered by their failover priority) for the region.

--enabled
:   Determines whether or not the load balancer pool is enabled. Valid values: `true`, `false`.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #create-glb-examples}

Create a global load balancer in the zone `demo.com:31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud dns glb-create demo.com:31984fea73a15b45779fa0df4ef62f9b --json @glb.json -i "dns-demo"
```
{: pre}

### `ibmcloud dns glb-update`
{: #update-glb}

Update a global load balancer in a zone.

```sh
ibmcloud dns glb-update DNS_ZONE_ID GLB_ID (-j, --json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]

ibmcloud dns glb-update DNS_ZONE_ID GLB_ID [--name NAME] [--default-pools POOL_LIST] [--fallback-pool POOL_ID] [--description DESCRIPTION] [--enabled true|false] [--ttl TTL] [--az-pools AZPOOLS1 --az-pools AZPOOLS2] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #update-glb-options}

DNS_DOMAIN_ID
:   The ID of the DNS zone. Required.

GLB_ID
:   The ID of the global load balancer. Required.

--json
:   The JSON file or JSON string that is used to describe a global load balancer. Required.
    - The optional fields are `name`, `fallback_pool`, `default_pools`, `description`, `ttl`, `az_pools`, `enabled`:
      - `name`: The DNS hostname to associate with your load balancer.
      - `fallback_pool`: The pool ID to use when all other pools are detected as unhealthy.
      - `default_pools`: A list of pool IDs ordered by their failover priority.
      - `description`: The descriptive text of the load balancer.
      - `ttl`: Time to live (TTL) of the DNS entry for the IP address returned by this load balancer.
      - `az_pools`: A mapping of region and country codes to a list of pool IDs (ordered by their failover priority) for the region.
      - `enabled`: Determines whether or not the load balancer pool is enabled. Valid values: `true`, `false`. The values `on`, `off` are deprecated.

    Sample JSON data:

    ```json
    {
      "name": "glb01",
      "description": "Global load balancer 01",
      "enabled": false,
      "ttl": 300,
      "default_pools": ["cc1deb57-0eb4-45cb-94ce-a3c71c189d12"],
      "fallback_pool": "cc1deb57-0eb4-45cb-94ce-a3c71c189d12",
      "az_pools": [
        {
          "availability_zone": "us-south-1",
          "pools": [
            "0fc0bb7c-2fab-476e-8b9b-40fa14bf8e3d"
          ]
        },
        {
          "availability_zone": "us-south-2",
          "pools": [
            "f46eba57-f08e-4e38-a76c-f3370d457bd2"
          ]
        }
      ]
    }
    ```
    {: codeblock}

--name
:   The DNS hostname to associate with your load balancer.

--fallback-pool
:   The pool ID to use when all other pools are detected as unhealthy.

--default-pools
:   A list of pool IDs ordered by their failover priority.

--description
:   The descriptive text of the load balancer.

--ttl
:   Time to live (TTL) of the DNS entry for the IP address returned by this load balancer.

--az-pools
:   A mapping of region and country codes to a list of pool IDs (ordered by their failover priority) for the region.

--enabled
:   Determines whether or not the load balancer pool is enabled. Valid values: `true`, `false`.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #update-glb-examples}

Update global load balancer `699d98642c564d2e855e9661899b7252` in zone `demo.com:31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud dns glb-update demo.com:31984fea73a15b45779fa0df4ef62f9b 699d98642c564d2e855e9661899b7252 --json @glb.json -i "dns-demo"
```
{: pre}

### `ibmcloud dns glb`
{: #show-glb}

Show a global load balancer in a zone.

```sh
ibmcloud dns glb DNS_DOMAIN_ID GLB_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #show-glb-options}

DNS_DOMAIN_ID
:   The ID of the DNS zone. Required.

GLB_ID
:   The ID of a global load balancer. Required.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #show-glb-examples}

Show global load balancer `699d98642c564d2e855e9661899b7252` in zone `demo.com:31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud dns glb demo.com:31984fea73a15b45779fa0df4ef62f9b 699d98642c564d2e855e9661899b7252 -i "dns-demo"
```
{: pre}

### `ibmcloud dns glb-delete`
{: #delete-glb}

Delete a global load balancer in a DNS domain.

```sh
ibmcloud dns glb-delete DNS_DOMAIN_ID GLB_ID [-i, --instance INSTANCE] [-f,--force]
```
{: pre}

#### Command options
{: #delete-glb-options}

DNS_DOMAIN_ID
:   The ID of the DNS zone. Required.

GLB_ID
:   The ID of a global load balancer. Required.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

-f, --force
:   Delete load balancer without prompting for confirmation.

#### Examples
{: #delete-glb-examples}

Delete global load balancer `699d98642c564d2e855e9661899b7252` in zone `demo.com:31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud dns glb-delete demo.com:31984fea73a15b45779fa0df4ef62f9b 699d98642c564d2e855e9661899b7252 -f -i "dns-demo"
```
{: pre}

### `ibmcloud dns glbs`
{: #list-glb}

List all load balancers for the zone.

```sh
ibmcloud dns glbs DNS_ZONE_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #list-glb-options}

DNS_DOMAIN_ID
:   The ID of the DNS zone. Required.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

--page
:   Page number of paginated results (default 1).

--per-page
:   Number of resource records per page. Min: 50. Max: 1000 (default 200).

#### Example command to list load balancers
{: #list-glb-examples}

List load balancers for zone `demo.com:31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud dns glbs demo.com:31984fea73a15b45779fa0df4ef62f9b -i "dns-demo"
```
{: pre}

#### Example command to list load balancers with pagination
{: #list-glb-pagination-example}

List load balancers for zone "dns-demo" with pagination.

 ```sh
ibmcloud dns glbs demo.com:31984fea73a15b45779fa0df4ef62f9b -i "dns-demo" --output json --per-page 1000 --page 1
 ```
{: pre}

### `ibmcloud dns glb-pool-create`
{: #create-glb-pool}

Create a GLB pool for a service instance.

```sh
ibmcloud dns glb-pool-create (-j, --json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]

ibmcloud dns glb-pool-create --name NAME --origins ORIGIN1 --origins ORIGIN2 [--description DESCRIPTION] [--enabled true|false] [--healthy-origins-threshold THRESHOLD] [--monitor MONITOR_ID] [--notification-channel CHANNEL] [--healthcheck-region REGION] [--healthcheck-subnets SUBNETS] [-i, --instance INSTANCE] [--output FORMAT]

```
{: pre}

#### Command options
{: #create-glb-pool-options}

--json
:   The JSON file or JSON string that is used to describe a global load balancer pool. Required.
    - The required fields in JSON data are `name`, `origins`:
        - `name`: The name of the load balancer pool.
        - `origins`: The list of origins within this pool.
    - The optional fields are `description`, `healthy_origins_threshold`, `enabled`, `monitor`, `notification_channel`, `healthcheck_region`, `healthcheck_subnets`:
        - `description`: The descriptive text of the load balancer pool.
        - `healthy_origins_threshold`: The minimum number of origins that must be healthy for this pool to serve traffic.
        - `enabled`: Determines whether or not the load balancer pool is enabled. Valid values: `true`, `false`.
        - `monitor`: The ID of the load balancer monitor that is to be associated to this pool.
        - `notification_channel`: The notification channel.
        - `healthcheck_region`: Health check region of VSIs. Valid values: `us-south`, `us-east`, `eu-gb`, `eu-du`, `au-syd`, `jp-tok`, `br-sao`, `ca-tor`.
        - `healthcheck_subnets`: A list of health check subnet IDs of VSIs.

        When you create a pool by attaching a monitor, DNS Services takes one address from the health check subnet. Ensure that this health check subnet has sufficient IP addresses available.
        {: note}

    Sample JSON data:

    ```json
    {
      "name": "us-pool",
      "description": "application server pool in US",
      "origins": [
        {
          "name": "us-app-dal10",
          "description": "dallas origin 10",
          "address": "1.1.1.1",
          "enabled": true
        },
        {
          "name": "us-app-dal12",
          "description": "dallas origin 12",
          "address": "2.2.2.2",
          "enabled": true
        }
      ],
      "healthy_origins_threshold": 1,
      "monitor": "f1aba936b94213e5b8dca0c0dbf1f9cc",
      "enabled": true,
      "notification_channel": "https://mywebsite.com/dns/webhook",
      "healthcheck_region": "us-south",
      "healthcheck_subnets": ["0716-a4c0c123-594c-4ef4-ace3-a08858540b5e"]
    }
    ```
    {: codeblock}

--name
:   The name of the load balancer pool.

--description
:   The descriptive text of the load balancer pool.

--healthy-origins-threshold
:   The minimum number of origins that must be healthy for this pool to serve traffic.

--enabled
:   Determines whether or not the load balancer pool is enabled. Valid values: `true`, `false`.

--monitor
:   The ID of the load balancer monitor that is to be associated to this pool.

--notification-channel
:   The notification channel.

healthcheck-region
:   Health check region of VSIs. Valid values: `us-south`, `us-east`, `eu-gb`, `eu-du`, `au-syd`, `jp-tok`.

healthcheck-subnets
:   A list of health check subnet IDs of VSIs.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #create-glb-pool-examples}

Create a GLB pool for instance `dns-demo`.

```sh
ibmcloud dns glb-pool-create --json @glb-pool.json -i "dns-demo"
```
{: pre}

### `ibmcloud dns glb-pool-update`
{: #update-glb-pool}

Update the details of a GLB pool.

```sh
ibmcloud dns glb-pool-update GLB_POOL_ID [--name NAME] [--enable-origin ORIGIN_NAME --enable-origin ORIGIN_NAME ...] [--disable-origin ORIGIN_NAME --disable-origin ORIGIN_NAME ...] [--add-origin ORIGIN_PARAMETER --add-origin ORIGIN_PARAMETER ...] [--remove-origin ORIGIN_NAME --remove-origin ORIGIN_NAME ...]  [--description DESCRIPTION] [--enabled true|false] [--healthy-origins-threshold THRESHOLD] [-detach-monitor] [--attach-monitor MONITOR_ID] [--healthcheck-region REGION] [--healthcheck-subnets SUBNETS] [-i, --instance INSTANCE] [--output FORMAT]

ibmcloud dns glb-pool-update GLB_POOL_ID (-j, --json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #update-glb-pool-options}

GLB_POOL_ID
:   The ID of the global load balancer pool. Required.

--json
:   The JSON file or JSON string that is used to describe a GLB pool. Required.
    - The optional fields are `name`, `origins`, `description`, `healthy_origins_threshold`, `enabled`, `monitor`, `notification_channel`, `healthcheck_region`, `healthcheck_subnets`:
        - `name`: The name of the load balancer pool.
        - `origins`: The list of origins within this pool.
        - `description`: The descriptive text of the load balancer pool.
        - `healthy_origins_threshold`: The minimum number of origins that must be healthy for this pool to serve traffic.
        - `enabled`: Determines whether or not the load balancer pool is enabled. Valid values: `true`, `false`.
        - `monitor`: The ID of the load balancer monitor that is to be associated to this pool.
        - `notification_channel`: The notification channel.
        - `healthcheck_region`: Health check region of VSIs. Valid values: `us-south`, `us-east`, `eu-gb`, `eu-du`, `au-syd`, `jp-tok`, `br-sao`, `ca-tor`.
        - `healthcheck_subnets`: A list of health check subnet IDs of VSIs.

    Sample JSON data:

    ```json
    {
      "name": "us-pool",
      "description": "application server pool in US",
      "origins": [
        {
          "name": "us-app-dal10",
          "description": "dallas origin 10",
          "address": "1.1.1.1",
          "enabled": true
        },
        {
          "name": "us-app-dal12",
          "description": "dallas origin 12",
          "address": "2.2.2.2",
          "enabled": true
        }
      ],
      "healthy_origins_threshold": 1,
      "monitor": "f1aba936b94213e5b8dca0c0dbf1f9cc",
      "enabled": true,
      "notification_channel": "https://mywebsite.com/dns/webhook",
      "healthcheck_region": "us-south",
      "healthcheck_subnets": ["0716-a4c0c123-594c-4ef4-ace3-a08858540b5e"]
    }
    ```
    {: codeblock}

--name
:   The name of the load balancer pool.

--description
:   The descriptive text of the load balancer pool.

--enable-origin
:   Enable the origin within the pool. The value can be ORIGIN_NAME or ORIGIN_ADDRESS.

--disable-origin
:   Disable the origin within the pool. The value can be ORIGIN_NAME or ORIGIN_ADDRESS.

--add-origin
:   Add an origin into the pool. ORIGIN_NAME and ORIGIN_ADDRESS are required.
    For example, `--add-origin name=example,address=1.2.3.4,enabled=true,description=origin_description`.

--remove-origin
:   Remove an origin from the Pool. The value can be ORIGIN_NAME or ORIGIN_ADDRESS.

--detach-monitor
:   Detach monitor from origin pool.

--attach-monitor
:   Attach monitor to origin pool.

--healthy-origins-threshold
:   The minimum number of origins that must be healthy for this pool to serve traffic.

--enabled
:   Determines whether or not the load balancer pool is enabled. Valid values: `true`, `false`.

healthcheck-region
:   Health check region of VSIs. Valid values: `us-south`, `us-east`, `eu-gb`, `eu-du`, `au-syd`, `jp-tok`, `br-sao`, `ca-tor`.

healthcheck-subnets
:   A list of health check subnet IDs of VSIs.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #update-glb-pool-examples}

Update a GLB pool `17b5962d775c646f3f9725cbc7a53df4` for instance `dns-demo`.

```sh
ibmcloud dns glb-pool-update 17b5962d775c646f3f9725cbc7a53df4 --json @glb-pool.json -i "dns-demo"
```
{: pre}

### `ibmcloud dns glb-pool`
{: #show-glb-pool}

Show the details of a GLB pool.

```sh
ibmcloud dns glb-pool GLB_POOL_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #show-glb-pool-options}

GLB_POOL_ID
:   The ID of the global load balancer pool. Required.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #show-glb-pool-examples}

Show the details of the GLB pool `17b5962d775c646f3f9725cbc7a53df4`.

```sh
ibmcloud dns glb-pool 17b5962d775c646f3f9725cbc7a53df4 -i "dns-demo"
```
{: pre}

### `ibmcloud dns glb-pool-delete`
{: #delete-glb-pool}

Delete a GLB pool.

```sh
ibmcloud dns glb-pool-delete GLB_POOL_ID [-i, --instance INSTANCE] [-f,--force]
```
{: pre}

#### Command options
{: #delete-glb-pool-options}

GLB_POOL_ID
:   The ID of the global load balancer pool. Required.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

-f, --force
:   Delete load balancer pool without prompting for confirmation.

#### Examples
{: #delete-glb-pool-examples}

Delete GLB pool `17b5962d775c646f3f9725cbc7a53df4`.

```sh
ibmcloud dns glb-pool-delete 17b5962d775c646f3f9725cbc7a53df4 -f -i "dns-demo"
```
{: pre}

### `ibmcloud dns glb-pools`
{: #list-glb-pools}

List all GLB pools for a service instance.

```sh
ibmcloud dns glb-pools [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #list-glb-pools-options}

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

--page
:   Page number of paginated results (default 1).

--per-page
:   Number of resource records per page. Min: 50. Max: 1000 (default 200).

#### Example command to list load balancer pools
{: #list-glb-pools-examples}

List all load balancer pools for instance `dns-demo`.

```sh
ibmcloud dns glb-pools -i "dns-demo"
```
{: pre}

#### Example command to list load balancer pools with pagination
{: #list-glb-pools-pagination-example}

List all load balancer pools with pagination for instance `dns-demo`.

 ```sh
ibmcloud dns glb-pools -i "dns-demo" --output json --per-page 1000 --page 1
 ```
{: pre}

### `ibmcloud dns glb-monitor-create`
{: #create-glb-monitor}

Create a GLB monitor for a service instance.

```sh
ibmcloud dns glb-monitor-create (-j, --json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]

ibmcloud dns glb-monitor-create --name NAME --type TCP [--port PORT] [--description DESCRIPTION] [--interval INTERVAL] [--retries RETRY] [--timeout TIMEOUT] [-i, --instance INSTANCE] [--output FORMAT]

ibmcloud dns glb-monitor-create --name NAME --type (HTTP|HTTPS) --path PATH [--port PORT] [--description DESCRIPTION] [--method GET|HEAD] [--headers HEADER1 --headers HEADER2...] [--interval INTERVAL] [--retries RETRY] [--timeout TIMEOUT] [--allow-insecure true|false] [--expected-body BODY] [--expected-codes CODE] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #create-glb-monitor-options}

--json
:   The JSON file or JSON string that is used to describe a GLB monitor. Required.
    - The required fields in JSON data are `name`, `type`.
        - `name`: The name of the load balancer monitor.
        - `type`: The protocol to use for the health check. Valid values: `HTTP`, `HTTPS`, `TCP`.
    - The optional fields are `description`, `timeout`, `retries`, `interval`.
        - `description`: The descriptive text of the load balancer monitor.
        - `timeout`: The timeout (in seconds) before the health check is marked as failed. Valid values: `1-10`.
        - `retries`: The number of retries to attempt when a timeout occurs before the origin is marked as unhealthy. Valid values: `0-3`.
        - `interval`: The interval between each health check. Valid values: `60-3600`.
    - For `TCP`-type health checks. Extra required fields are `port`.
        - `port`: The TCP port to use for the health check.
    - For `HTTP/HTTPS`-type health checks. Extra required fields are `expected_codes`.
        - `expected_codes`: The expected HTTP response code or code range of the health checks. Valid values: `200`, `201`, `202`, `203`, `204`, `205`, `206`, `207`, `208`, `226`, `2xx`, `3xx`, `4xx`, `5xx`.
    - Extra option fields are `port`, `expected_body`, `method`, `path`, `header`, `allow_insecure`.
        - `port`: The port number that the health check connects to.
        - `expected_body`: A case-insensitive substring to look for in the response body.
        - `method`: The method to use for the health check that is applicable to HTTP/HTTPS based checks. Valid values: `GET`, `HEAD`.
        - `path`: The endpoint path to health check against.
        - `header`: The HTTP request headers to send in the health check.
        - `allow_insecure`: Do not validate the certificate when monitor use HTTPS. Valid values: `true`, `false`.

    Sample JSON data:

    For HTTP/HTTPS:

    ```json
    {
      "name": "glbmonitor",
      "description": "Health monitor of web service",
      "type": "HTTPS",
      "method": "GET",
      "path": "/health",
      "headers": [
        {
          "name": "Host",
          "value": ["glb.example.com"]
        },
        {
          "name": "X-App-ID",
          "value":["abc123"]
        }
      ],
      "port": 443,
      "timeout": 5,
      "retries": 2,
      "interval": 90,
      "allow_insecure": false,
      "expected_codes": "2xx",
      "expected_body": "alive"
    }
    ```
    {: codeblock}

    For TCP:

    ```sh
    {
      "name": "glbmonitor",
      "description": "Health monitor of TCP",
      "type": "TCP",
      "port": 80,
      "timeout": 5,
      "retries": 2,
      "interval": 90
    }
    ```
    {: codeblock}

--name
:   The name of the load balancer monitor.

--type
:   The protocol to use for the health check. Valid values: `HTTP`, `HTTPS`, `TCP`.

--description
:   The descriptive text of the load balancer monitor.

--timeout
:   The timeout (in seconds) before the health check is marked as failed. Valid values: `1-10`.

--retries
:   The number of retries to attempt when a timeout occurs before the origin is marked as unhealthy. Valid values: `0-3`.

--interval
:   The interval between each health check. Valid values: `60-3600`.

--port
:   The port number that the health check connects to.

--expected-codes
:   The expected HTTP response code or code range of the health check. Valid values: `200`, `201`, `202`, `203`, `204`, `205`, `206`, `207`, `208`, `226`, `2xx`, `3xx`, `4xx`, `5xx`.

--expected-body
:   A case-insensitive substring to look for in the response body.

--method
:   The method to use for the health check that is applicable to HTTP/HTTPS-based checks. Valid values: `GET`, `HEAD`.

--path
:   The endpoint path to health check against.

--headers
:   The HTTP request headers to send in the health check.

--allow-insecure
:   Do not validate the certificate when monitor uses HTTPS. Valid values: `on`, `off`.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #create-glb-monitor-examples}

Create a GLB monitors in instance `dns-demo`.

```sh
ibmcloud dns glb-monitor-create --json @glb-monitor.json -i "dns-demo"
```
{: pre}

### `ibmcloud dns glb-monitor-update`
{: #update-glb-monitor}

Update a GLB monitor for a service instance.

```sh
ibmcloud dns glb-monitor-update GLB_MON_ID (-j, --json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]

ibmcloud dns glb-monitor-update GLB_MON_ID [--name NAME] [--type TCP] [--port PORT] [--description DESCRIPTION] [--interval INTERVAL] [--retries RETRY] [--timeout TIMEOUT] [-i, --instance INSTANCE] [--output FORMAT]

ibmcloud dns glb-monitor-update GLB_MON_ID [--name NAME] [--type HTTP|HTTPS] [--expected-codes CODE] [--path PATH] [--port PORT] [--description DESCRIPTION] [--method GET|HEAD] [--headers HEADER1 --headers HEADER2...] [--interval INTERVAL] [--retries RETRY] [--timeout TIMEOUT] [--allow-insecure true|false] [--expected-body BODY] [--expected-codes CODE] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #update-glb-monitor-options}

GLB_MON_ID
:   The ID of a global load balancer monitor. Required.
--json
:   The JSON file or JSON string that is used to describe a GLB monitor. Required.
    - The optional fields are `name`, `type`, `description`, `timeout`, `retries`, `interval`.
        - `name`: The name of the load balancer monitor.
        - `type`: The protocol to use for the health check. Valid values: `HTTP`, `HTTPS`, `TCP`.
        - `description`: The descriptive text of the load balancer monitor.
        - `timeout`: The timeout (in seconds) before the health check is marked as failed. Valid values: `1-10`.
        - `retries`: The number of retries to attempt when a timeout occurs before the origin is marked as unhealthy. Valid values: `0-3`.
        - `interval`: The interval between each health check. Valid values: `60-3600`.
    - For `TCP`-type health check. Extra option fields are `port`.
        - `port`: The TCP port to use for the health check.
    - For `HTTP/HTTPS`-type health check. Extra option fields are `expected_codes`, `port`, `expected_body`, `method`, `path`, `header`, `allow_insecure`.
        - `expected_codes`: The expected HTTP response code or code range of the health check. Valid values: `200`, `201`, `202`, `203`, `204`, `205`, `206`, `207`, `208`, `226`, `2xx`, `3xx`, `4xx`, `5xx`.
        - `port`: The port number that the health check connects to.
        - `expected_body`: A case-insensitive substring to look for in the response body.
        - `method`: The method to use for the health check that is applicable to HTTP/HTTPS-based checks. Valid values: `GET`, `HEAD`.
        - `path`: The endpoint path to health check against.
        - `header`: The HTTP request headers to send in the health check.
        - `allow_insecure`: Do not validate the certificate when monitor use HTTPS. Valid values: `on`, `off`.

    Sample JSON data:

    For HTTP/HTTPS:

    ```json
    {
      "name": "glbmonitor",
      "description": "Health monitor of web service",
      "type": "HTTPS",
      "method": "GET",
      "path": "/health",
      "headers": [
        {
          "name": "Host",
          "value": ["glb.example.com"]
        },
        {
          "name": "X-App-ID",
          "value":["abc123"]
        }
      ],
      "port": 443,
      "timeout": 5,
      "retries": 2,
      "interval": 90,
      "allow_insecure": false,
      "expected_codes": "2xx",
      "expected_body": "alive"
    }
    ```
    {: codeblock}

    For TCP:

    ```sh
    {
      "name": "glbmonitor",
      "description": "Health monitor of TCP",
      "type": "TCP",
      "port": 80,
      "timeout": 5,
      "retries": 2,
      "interval": 90
    }
    ```
    {: codeblock}

--name
:   The name of the load balancer monitor.

--type
:   The protocol to use for the health check. Valid values: `HTTP`, `HTTPS`, `TCP`.

--description
:   The descriptive text of the load balancer monitor.

--timeout
:   The timeout (in seconds) before the health check is marked as failed. Valid values: `1-10`.

--retries
:   The number of retries to attempt when a timeout occurs before the origin is marked as unhealthy. Valid values: `0-3`.

--interval
:   The interval between each health check. Valid values: `60-3600`.

--port
:   The port number that the health check connects to.

--expected-codes
:   The expected HTTP response code or code range of the health check. Valid values: `200`, `201`, `202`, `203`, `204`, `205`, `206`, `207`, `208`, `226`, `2xx`, `3xx`, `4xx`, `5xx`.

--expected-body
:   A case-insensitive substring to look for in the response body.

--method
:   The method to use for the health check that is applicable to HTTP/HTTPS-based checks. Valid values: `GET`, `HEAD`.

--path
:   The endpoint path to health check against.

--headers
:   The HTTP request headers to send in the health check.

--allow-insecure
:   Do not validate the certificate when monitor uses HTTPS. Valid values: `on`, `off`.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #update-glb-monitor-examples}

Update GLB monitors `f1aba936b94213e5b8dca0c0dbf1f9cc` in instance `dns-demo`.

```sh
ibmcloud dns glb-monitor-update f1aba936b94213e5b8dca0c0dbf1f9cc --json @glb-monitor.json -i "dns-demo"
```
{: pre}

### `ibmcloud dns glb-monitor`
{: #show-glb-monitor}

Show the details of a global load balancer monitor.

```sh
ibmcloud dns glb-monitor GLB_MON_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #show-glb-monitor-options}

GLB_MON_ID
:   The ID of a global load balancer monitor. Required.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #show-glb-monitor-examples}

Show the details of the GLB monitor `f1aba936b94213e5b8dca0c0dbf1f9cc`.

```sh
ibmcloud dns glb-monitor f1aba936b94213e5b8dca0c0dbf1f9cc -i "dns-demo"
```
{: pre}


### `ibmcloud dns glb-monitor-delete`
{: #delete-glb-monitor}

Delete the GLB monitor for a service instance.

```sh
ibmcloud dns glb-monitor-delete GLB_MON_ID [-i, --instance INSTANCE] [-f,--force]
```
{: pre}

#### Command options
{: #delete-glb-monitor-options}

GLB_MON_ID
:   The ID of a global load balancer monitor. Required.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

-f, --force
:   Delete load balancer monitor without prompting for confirmation.

#### Examples
{: #delete-glb-monitor-examples}

Delete the GLB monitor `f1aba936b94213e5b8dca0c0dbf1f9cc`.

```sh
ibmcloud dns glb-monitor-delete f1aba936b94213e5b8dca0c0dbf1f9cc -f -i "dns-demo"
```
{: pre}

### `ibmcloud dns glb-monitors`
{: #list-glb-monitors}

List GLB monitors for a service instance.

```sh
ibmcloud dns glb-monitors [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #list-glb-monitors-options}

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

--page
:   Page number of paginated results (default 1).

--per-page
:   Number of resource records per page. Min: 50. Max: 1000 (default 200).

#### Example commands
{: #list-glb-monitors-examples}

List all load balancer monitors for instance `dns-demo`.

```sh
ibmcloud dns glb-monitors -i "dns-demo"
```
{: pre}

#### Example command to list load balancer pools with pagination
{: #list-glb-monitors-pagination-example}

List all load balancer monitors with pagination for instance `dns-demo`.

 ```sh
ibmcloud dns glb-monitors -i "dns-demo" --output json --per-page 1000 --page 1
 ```
{: pre}

## Custom resolver
{: #custom-resolvers}

Manage custom resolvers by using the following custom resolver commands.

### `ibmcloud dns custom-resolver-create`
{: #create-custom-resolver}

Create a custom resolver for a service instance.

```sh
ibmcloud dns custom-resolver-create --name NAME [--location LOCATION1] [--location LOCATION2] [-description DESCRIPTION] [-f, --force] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #create-custom-resolver-options}

-n, --name
:   The name of the custom resolver.

-d, --description
:   The descriptive text of the custom resolver.

-f, --force
:   Allow creating custom resolver with fewer than 2 locations.

--location
:   The locations on which the custom resolver runs. The location subnet CRN is required.
    For example, `--location subnet1,enable  --location subnet2,disable`.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #create-custom-resolver-examples}

Create a custom resolver for instance `dns-demo`.

```sh
ibmcloud dns custom-resolver-create --name "example" --location crn:v1:bluemix:public:is:us-south-1:a/01652b251c3ae2787110a995d8db0135::subnet:0716-b49ef064-0f89-4fb1-8212-135b12568f04,enable --description "demo" -i "dns-demo"
```
{: pre}

### `ibmcloud dns custom-resolver-update`
{: #update-custom-resolver}

Update a custom resolver for a service instance.

```sh
ibmcloud dns custom-resolver-update RESOLVER_ID [--name NAME] [--enabled true|false] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #update-custom-resolver-options}

RESOLVER_ID
:   The ID of the custom resolver.

-n, --name
:   The name of the custom resolver.

-d, --description
:   The descriptive text of the custom resolver.

--enabled
:   Determines whether or not to enable the custom resolver.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #update-custom-resolver-examples}

Update a custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc` for instance `dns-demo`.

```sh
ibmcloud dns custom-resolver-update f1aba936b94213e5b8dca0c0dbf1f9cc --name "example" --enabled true -description "demo" -i "dns-demo"
```
{: pre}

### `ibmcloud dns custom-resolver`
{: #get-custom-resolver}

Get the custom resolver details for a service instance.

```sh
ibmcloud dns custom-resolver RESOLVER_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #get-custom-resolver-options}

RESOLVER_ID
:   The ID of the custom resolver.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #get-custom-resolver-examples}

Get a custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc` for instance `dns-demo`.

```sh
ibmcloud dns custom-resolver f1aba936b94213e5b8dca0c0dbf1f9cc -i "dns-demo"
```
{: pre}

### `ibmcloud dns custom-resolvers`
{: #list-custom-resolvers}

List custom resolvers for a service instance.

```sh
ibmcloud dns custom-resolvers [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #list-custom-resolvers-options}

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #list-custom-resolvers-examples}

List custom resolvers for instance `dns-demo`.

```sh
ibmcloud dns custom-resolvers -i "dns-demo"
```
{: pre}

### `ibmcloud dns custom-resolver-delete`
{: #delete-custom-resolver}

Delete a custom resolver for a service instance.

```sh
ibmcloud dns custom-resolver-delete RESOLVER_ID [-i, --instance INSTANCE] [-f, --force]
```
{: pre}

#### Command options
{: #delete-custom-resolver-options}

RESOLVER_ID
:   The ID of the custom resolver.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--f, --force
:   Delete custom resolver without prompting for confirmation.

#### Examples
{: #delete-custom-resolver-examples}

Delete a custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc` for instance `dns-demo`.

```sh
ibmcloud dns custom-resolver-delete f1aba936b94213e5b8dca0c0dbf1f9cc -i "dns-demo"
```
{: pre}

### `ibmcloud dns custom-resolver-location-add`
{: #add-custom-resolver-location}

Add a custom resolver location for a service instance.

```sh
ibmcloud dns custom-resolver-location-add RESOLVER_ID --subnet SUBNET_CRN [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #add-custom-resolver-location-options}

RESOLVER_ID
:   The ID of the custom resolver.

--subnet
:   The CRN of the subnet.

--enabled
:   Determines whether or not to enable the custom resolver location.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #add-custom-resolver-location-examples}

Add a location in the custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc` for instance `dns-demo`.

```sh
ibmcloud dns custom-resolver-location-add f1aba936b94213e5b8dca0c0dbf1f9cc --subnet crn:v1:bluemix:public:is:us-south-1:a/01652b251c3ae2787110a995d8db0135::subnet:0716-b49ef064-0f89-4fb1-8212-135b12568f04 --enabled true -i "dns-demo"
```
{: pre}

### `ibmcloud dns custom-resolver-location-update`
{: #update-custom-resolver-location}

Update the custom resolver location for a service instance.

```sh
ibmcloud dns custom-resolver-location-update RESOLVER_ID LOCATION_ID [--subnet SUBNET_CRN] [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #update-custom-resolver-location-options}

RESOLVER_ID
:   The ID of the custom resolver.

LOCATION_ID
:   The ID of the custom resolver location.

--subnet
:   The CRN of the subnet.

--enabled
:   Determines whether or not to enable the custom resolver location.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #update-custom-resolver-location-examples}

Update the location `9a234ede-c2b6-4c39-bc27-d39ec139ecdb` in custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc` for instance `dns-demo`.

```sh
ibmcloud dns custom-resolver-location-update f1aba936b94213e5b8dca0c0dbf1f9cc 9a234ede-c2b6-4c39-bc27-d39ec139ecdb --subnet crn:v1:bluemix:public:is:us-south-1:a/01652b251c3ae2787110a995d8db0135::subnet:0716-b49ef064-0f89-4fb1-8212-135b12568f04 --enabled true -i "dns-demo"
```
{: pre}

### `ibmcloud dns custom-resolver-location-delete`
{: #delete-custom-resolver-location}

Delete the custom resolver location for a service instance.

```sh
ibmcloud dns custom-resolver-location-delete RESOLVER_ID LOCATION_ID [-i, --instance INSTANCE] [-f, --force]
```
{: pre}

#### Command options
{: #delete-custom-resolver-location-options}

RESOLVER_ID
:   The ID of the custom resolver.

LOCATION_ID
:   The ID of the custom resolver location.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--f, --force
:   Delete the custom resolver location without prompting for confirmation.

#### Examples
{: #delete-custom-resolver-location-examples}

Delete the location `9a234ede-c2b6-4c39-bc27-d39ec139ecdb` in custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc` for instance `dns-demo`.

```sh
ibmcloud dns custom-resolver-location-delete f1aba936b94213e5b8dca0c0dbf1f9cc 9a234ede-c2b6-4c39-bc27-d39ec139ecdb -i "dns-demo"
```
{: pre}

### `ibmcloud dns custom-resolver-forwarding-rule-create`
{: #create-custom-resolver-forwarding-rule}

Create a custom resolver forwarding rule for a service instance.

```sh
ibmcloud dns custom-resolver-forwarding-rule-create RESOLVER_ID --type TYPE --match HOSTNAME --dns-svcs IPs [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #create-custom-resolver-forwarding-rule-options}

RESOLVER_ID
:   The ID of the custom resolver.

-t, --type
:   The type of the forwarding rule. Valid values: "zone".

-d, --description
:   The descriptive text of the custom resolver forwarding rule.

--match
:   The matching zone or hostname.

--dns-svcs
:   The upstream DNS servers are forwarded to, for example: `ip1`, `ip2`.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #create-custom-resolver-forwarding-rule-examples}

Create a forwarding rule in a custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc` for instance `dns-demo`.

```sh
ibmcloud dns custom-resolver-forwarding-rule-create f1aba936b94213e5b8dca0c0dbf1f9cc --type zone --match "example.com" --dns-svcs 192.168.0.1,192.168.0.2 --description "demo" -i "dns-demo"
```
{: pre}

### `ibmcloud dns custom-resolver-forwarding-rule-update`
{: #update-custom-resolver-forwarding-rule}

Update a custom resolver forwarding rule for a service instance.

```sh
ibmcloud dns custom-resolver-forwarding-rule-update RESOLVER_ID RULE_ID [--match HOSTNAME] [--dns-svcs IPs] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #update-custom-resolver-forwarding-rule-options}

RESOLVER_ID
:   The ID of the custom resolver.

RULE_ID
:   The ID of custom resolver forwarding rule.

-d, --description
:   The descriptive text of the custom resolver forwarding rule.

--match
:   The matching zone or hostname.

--dns-svcs
:   The upstream DNS servers are forwarded to, for example: `ip1`,`ip2`.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #update-custom-resolver-forwarding-rule-examples}

Update the forwarding rule `9a234ede-c2b6-4c39-bc27-d39ec139ecdb` in custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc` for instance `dns-demo`.

```sh
ibmcloud dns custom-resolver-forwarding-rule-update f1aba936b94213e5b8dca0c0dbf1f9cc 9a234ede-c2b6-4c39-bc27-d39ec139ecdb --type zone --match "example.com" --dns-svcs 192.168.0.1,192.168.0.2 --description "demo" -i "dns-demo"
```
{: pre}

### `ibmcloud dns custom-resolver-forwarding-rule`
{: #get-custom-resolver-forwarding-rule}

Get the custom resolver forwarding rule details for a service instance.

```sh
ibmcloud dns custom-resolver-forwarding-rule RESOLVER_ID RULE_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #get-custom-resolver-forwarding-rule-options}

RESOLVER_ID
:   The ID of the custom resolver.

RULE_ID
:   The ID of custom resolver forwarding rule.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #get-custom-resolver-forwarding-rule-examples}

Get the forwarding rule `9a234ede-c2b6-4c39-bc27-d39ec139ecdb` in custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc` for instance `dns-demo`.

```sh
ibmcloud dns custom-resolver-forwarding-rule f1aba936b94213e5b8dca0c0dbf1f9cc 9a234ede-c2b6-4c39-bc27-d39ec139ecdb -i "dns-demo"
```
{: pre}

### `ibmcloud dns custom-resolver-forwarding-rules`
{: #list-custom-resolver-forwarding-rules}

List custom resolver forwarding rules for a service instance.

```sh
ibmcloud dns custom-resolver-forwarding-rules RESOLVER_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #list-custom-resolver-forwarding-rules-options}

RESOLVER_ID
:   The ID of the custom resolver.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output
:   Specify the output format. Currently, `json` is the only supported format.

--page
:   Page number of paginated results (default 1).

--per-page
:   Number of resource records per page. Min: 50. Max: 1000 (default 200).

#### Example command to list forwarding rules
{: #list-custom-resolver-forwarding-rules-examples}

List forwarding rules in a custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc` for instance `dns-demo`.

```sh
ibmcloud dns custom-resolver-forwarding-rules f1aba936b94213e5b8dca0c0dbf1f9cc -i "dns-demo"
```
{: pre}

#### Example command to list forwarding rules with pagination
{: #list-forwarding-rules-pagination-example}

List all forwarding rules in a custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc` with pagination for instance `dns-demo`.

 ```sh
ibmcloud dns custom-resolver-forwarding-rules f1aba936b94213e5b8dca0c0dbf1f9cc -i "dns-demo" --output json --per-page 1000 --page 1
 ```
{: pre}

### `ibmcloud dns custom-resolver-forwarding-rule-delete`
{: #delete-custom-resolver-forwarding-rule}

Delete a custom resolver forwarding rule for a service instance.

```sh
ibmcloud dns custom-resolver-forwarding-rule-delete RESOLVER_ID RULE_ID [-i, --instance INSTANCE] [-f, --force]
```
{: pre}

#### Command options
{: #delete-custom-resolver-forwarding-rule-options}

RESOLVER_ID
:   The ID of the custom resolver.

RULE_ID
:   The ID of the custom resolver forwarding rule.

-i, --instance
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

-f, --force
:   Delete the custom resolver forwarding rule without prompting for confirmation.

#### Examples
{: #delete-custom-resolver-forwarding-rule-examples}

Delete the forwarding rule `9a234ede-c2b6-4c39-bc27-d39ec139ecdb` in custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc` for instance `dns-demo`.

```sh
ibmcloud dns custom-resolver-forwarding-rule-delete f1aba936b94213e5b8dca0c0dbf1f9cc 9a234ede-c2b6-4c39-bc27-d39ec139ecdb -i "dns-demo"
```
{: pre}

## Secondary zones
{: #secondary-zones}

Manage secondary zones by using the following secondary zone commands.

### `ibmcloud dns secondary-zone-create`
{: #create-secondary-zones}

Create a secondary zone for given custom resolver.

```sh
ibmcloud dns secondary-zone-create RESOLVER_ID --name NAME --transfer-from ADDRESS1,ADDRESS2 [--description DESCRIPTION] [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #create-secondary-zone-options}

RESOLVER_ID
:   The ID of the custom resolver. Required.

--name value
:   The domain name of the secondary zone.

--transfer-from value
:   The source addresses of the secondary zone.

--description value
:   The description of the secondary zone.

--enabled value
:   Determines whether or not the secondary zone is enabled.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target INSTANCE` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #create-secondary-zone-examples}

Create a secondary zone for custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc`.

```sh
ibmcloud dns secondary-zone-create f1aba936b94213e5b8dca0c0dbf1f9cc --name "test.com" --transfer-from 169.13.12.10 -i "dns-demo"
```
{: pre}

### `ibmcloud dns secondary-zone-update`
{: #update-secondary-zone}

Update a secondary zone.

```sh
ibmcloud dns secondary-zone-update RESOLVER_ID SECONDARY_ZONE_ID [--transfer-from ADDRESS1,ADDRESS2] [--description DESCRIPTION] [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #update-secondary-zone-options}

RESOLVER_ID
:   The ID of the custom resolver. Required.

SECONDARY_ZONE_ID
:   The ID of the secondary zone. Required.

--transfer-from value
:   The source addresses of the secondary zone.

--description value
:   The description of the secondary zone.

--enabled value
:   Determines whether or not the secondary zone is enabled.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target INSTANCE` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #update-secondary-zone-examples}

Update a secondary zone `e2aba136a93212e5a8dce0c2dbf6f2ee` for custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc`.

```sh
ibmcloud dns secondary-zone-update f1aba936b94213e5b8dca0c0dbf1f9cc e2aba136a93212e5a8dce0c2dbf6f2ee --transfer-from 169.13.12.10:53 -i "dns-demo"
```
{: pre}

### `ibmcloud dns secondary-zone`
{: #secondary-zone}

Get the details of a secondary zone.

```sh
ibmcloud dns secondary-zone RESOLVER_ID SECONDARY_ZONE_ID [-i, --instance INSTANCE_NAME] [--output FORMAT]
```
{: pre}

#### Command options
{: #get-secondary-zone-options}

RESOLVER_ID
:   The ID of the custom resolver. Required.

SECONDARY_ZONE_ID
:   The ID of the secondary zone. Required.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #get-secondary-zone-examples}

Get a secondary zone `e2aba136a93212e5a8dce0c2dbf6f2ee` for custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc`.

```sh
ibmcloud dns secondary-zone f1aba936b94213e5b8dca0c0dbf1f9cc e2aba136a93212e5a8dce0c2dbf6f2ee -i "dns-demo"
```
{: pre}

### `ibmcloud dns secondary-zones`
{: #list-secondary-zones}

List all secondary zones.

```sh
ibmcloud dns secondary-zones RESOLVER_ID [-i, --instance INSTANCE_NAME] [--output FORMAT]
```
{: pre}

#### Command options
{: #list-secondary-zones-options}

RESOLVER_ID
:   The ID of the custom resolver. Required.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #list-custom-resolver-examples}

List all secondary zones for a custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc`.

```sh
ibmcloud dns secondary-zones f1aba936b94213e5b8dca0c0dbf1f9cc -i "dns-demo"
```
{: pre}   


### `ibmcloud dns secondary-zone-delete`
{: #secondary-zones-delete}

Delete a secondary zone.

```sh
ibmcloud dns secondary-zone-delete RESOLVER_ID SECONDARY_ZONE_ID [-i, --instance INSTANCE_NAME] [--output FORMAT]
```
{: pre}

#### Command options
{: #delete-secondary-zone-options}

RESOLVER_ID
:   The ID of the custom resolver. Required.

SECONDARY_ZONE_ID
:   The ID of the secondary zone. Required.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `dns instance-target INSTANCE` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #delete-secondary-zone-examples}

Delete a secondary zone `e2aba136a93212e5a8dce0c2dbf6f2ee` for a custom resolver `f1aba936b94213e5b8dca0c0dbf1f9cc`.

```sh
ibmcloud dns secondary-zone-delete f1aba936b94213e5b8dca0c0dbf1f9cc e2aba136a93212e5a8dce0c2dbf6f2ee -i "dns-demo"
```
{: pre}   

## Cross-account access
{: #cross-account}

Manage cross accounts by using the following cross-account access commands.

### `ibmcloud dns cross-account linked-zone-create`
{: #linked-zone-create}

Create a linked zone.

```sh
ibmcloud dns cross-account linked-zone-create --owner-instance-id OWNER_INSTANCE_ID --owner-zone-id OWNER_ZONE_ID [--label LABEL] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #linked-zone-create-options}

--owner-instance-id value
:   The ID of the owner's instance.

--owner-zone-id value
:   The ID of the owner's zone.

--label value
:   The label of the linked zone.

--description value
:    The description of the linked zone.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target INSTANCE` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #linked-zone-create-examples}

```sh
ibmcloud dns cross-account linked-zone-create --owner-instance-id abe30019-1c08-42dc-9ad9-a0682af70054 --owner-zone-id 05855abe-3908-4cdc-bf0d-063e0b1c296d --description "linked zone example" --label "dev" -i "dns-demo"
```
{: pre}   

### `ibmcloud dns cross-account linked-zone-update`
{: #update-linked-zones}

Update a linked zone.

```sh
ibmcloud dns cross-account linked-zone-update LINKED_ZONE_ID [--label LABEL] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #update-linked-zone-options}

LINKED_ZONE_ID
:   The ID of the linked zone.

--label value
:   The label of the linked zone.

--description value
:   The description of the linked zone.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target INSTANCE` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #update-linked-zone-examples}

```sh
ibmcloud dns cross-account linked-zone-update 5365b73c-ce6f-4d6f-ad9f-d9c131b26370 --description "linked zone example" --label "dev" -i "dns-demo"
```
{: pre}   

### `ibmcloud dns cross-account linked-zones`
{: #list-linked-zones}

List all linked zones.

```sh
ibmcloud dns cross-account linked-zones [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #list-linked-zones-options}

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target INSTANCE` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #list-linked-zone-examples}

```sh
ibmcloud dns cross-account linked-zones -i "dns-demo"
```
{: pre}   

### `ibmcloud dns cross-account linked-zone`
{: #get-linked-zone}

Get details of the linked zone.

```sh
ibmcloud dns cross-account linked-zone LINKED_ZONE_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #get-linked-zone-options}

LINKED_ZONE_ID
:   The ID of the linked zone.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target INSTANCE` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #get-linked-zone-examples}

```sh
ibmcloud dns cross-account linked-zone 5365b73c-ce6f-4d6f-ad9f-d9c131b26370 -i "dns-demo"
```
{: pre}   

### `ibmcloud dns cross-account linked-zone-delete`
{: #delete-linked-zone}

Delete a linked zone.

```sh
ibmcloud dns cross-account linked-zone-delete LINKED_ZONE_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #delete-linked-zone-options}

LINKED_ZONE_ID
:   The ID of the linked zone.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target INSTANCE` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #delete-linked-zone-examples}

```sh
ibmcloud dns cross-account linked-zone-delete 5365b73c-ce6f-4d6f-ad9f-d9c131b26370 -i "dns-demo"
```
{: pre}  

### `ibmcloud dns cross-account linked-zone-permitted-network-add`
{: #add-permitted-network-for-lined-zone}

Create a permitted network for a linked zone

```sh
   ibmcloud dns cross-account linked-zone-permitted-network-add LINKED_ZONE_ID --vpc-crn VPC_CRN [--type TYPE] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #options-add-permitted-network-for-linked-zone}

LINKED_ZONE_ID
:   The ID of the linked zone.

--type value
:   The permitted network type. Valid values: `vpc`.

--vpc-crn value
:   The CRN of the VPC instance.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #add-linked-zone-permitted-network-examples}

```sh
ibmcloud dns cross-account linked-zone-permitted-network-add 5365b73c-ce6f-4d6f-ad9f-d9c131b26370 --vpc-crn  "crn:v1:bluemix:public:is:eu-de:a/bcf1865e99742d38d2d5fc3fb80a5496::vpc:6e6cc326-04d1-4c99-a289-efb3ae4193d6" --i "dns-demo"
```
{: pre}    

### `ibmcloud dns cross-account linked-zone-permitted-network`
{: #get-linked-zone-permitted-network}

Get a permitted network for a linked zone

```sh
   ibmcloud dns cross-account linked-zone-permitted-network LINKED_ZONE_ID PERMITTED_NETWORK_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #options-get-permitted-network-for-linked-zone}

LINKED_ZONE_ID
:   The ID of the linked zone.

PERMITTED_NETWORK_ID
:   The ID of the permitted network.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #get-linked-zone-permitted-network-examples}

```sh
ibmcloud dns cross-account linked-zone-permitted-network 5365b73c-ce6f-4d6f-ad9f-d9c131b26370 6e6cc326-04d1-4c99-a289-efb3ae4193d6  --i "dns-demo"
```
{: pre}    

### `ibmcloud dns cross-account linked-zone-permitted-network-remove`
{: #remove-linked-zone-permitted-network}

Remove a permitted network for a linked zone

```sh
   ibmcloud dns cross-account linked-zone-permitted-network-remove LINKED_ZONE_ID PERMITTED_NETWORK_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #options-remove-permitted-network-for-linked-zone}

LINKED_ZONE_ID
:   The ID of the linked zone.

PERMITTED_NETWORK_ID
:   The ID of the permitted network.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #remove-linked-zone-permitted-network-examples}

```sh
ibmcloud dns cross-account linked-zone-permitted-network-remove 5365b73c-ce6f-4d6f-ad9f-d9c131b26370 6e6cc326-04d1-4c99-a289-efb3ae4193d6  --i "dns-demo"
```
{: pre} 

### `ibmcloud dns cross-account linked-zone-permitted-networks`
{: #list-linked-zone-permitted-networks}

List the permitted networks for a linked zone

```sh
   ibmcloud dns cross-account linked-zone-permitted-networks LINKED_ZONE_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #options-list-permitted-networks-for-linked-zone}

LINKED_ZONE_ID
:   The ID of the linked zone.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #list-linked-zone-permitted-networks-examples}

```sh
ibmcloud dns cross-account linked-zone-permitted-networks 5365b73c-ce6f-4d6f-ad9f-d9c131b26370 --i "dns-demo"
```
{: pre} 

### `ibmcloud dns cross-account access-request-update`
{: #update-access-request}

Update the state of an access request.

```sh
   ibmcloud dns cross-account access-request-update ZONE_ID REQUEST_ID --action ACTION [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #options-update-access-request}

ZONE_ID
:   The ID of the owner's zone.

REQUEST_ID
:   The ID of the access request.

--action value
:   The action applies to the access request. Valid values: "APPROVE", "REJECT", "REVOKE".

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #update-access-request-examples}

```sh
ibmcloud dns cross-account access-request-update 05855abe-3908-4cdc-bf0d-063e0b1c296d 9a234ede-c2b6-4c39-bc27-d39ec139ecdb --action "APPROVE" --i "dns-demo"
```
{: pre} 

### `ibmcloud dns cross-account access-request`
{: #get-access-request}

Get details of an access request.

```sh
   ibmcloud dns cross-account access-request ZONE_ID REQUEST_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #options-get-access-request}

ZONE_ID
:   The ID of the owner's zone.

REQUEST_ID
:   The ID of the access request.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #get-access-request-examples}

```sh
ibmcloud dns cross-account access-request 05855abe-3908-4cdc-bf0d-063e0b1c296d 9a234ede-c2b6-4c39-bc27-d39ec139ecdb --i "dns-demo"
```
{: pre} 

### `ibmcloud dns cross-account access-requests`
{: #list-access-request}

List access requests in the owner's instance.

```sh
   ibmcloud dns cross-account access-requests ZONE_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #options-list-access-requests}

ZONE_ID
:   The ID of the owner's zone.

-i, --instance value
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud dns instance-target` is used.

--output value
:   Specify the output format. Currently, `json` is the only supported format.

#### Examples
{: #list-access-request-examples}

```sh
ibmcloud dns cross-account access-requests 05855abe-3908-4cdc-bf0d-063e0b1c296d --i "dns-demo"
```
{: pre} 

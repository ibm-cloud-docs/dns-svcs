---

copyright:
  years: 2019, 2024
lastupdated: "2024-10-25"

keywords: restricted zones

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Managing DNS zones
{: #managing-dns-zones}

Manage DNS zones by using the UI, CLI, or API.
{: shortdesc}

You must have an {{site.data.keyword.dns_full}} instance before managing DNS zones. Refer to [Create a {{site.data.keyword.dns_short}} instance](/docs/dns-svcs?topic=dns-svcs-getting-started#step-1-create-dns-services-instance) for more information.

A zone can have an arbitrary number of levels, but not fewer than two. For example, `ibm.austin.texas.example.com` is a valid zone name, but `com` is not.

You can have multiple zones where one is a suffix to another. For example, `sub.domain.example.com` and `domain.example.com` can co-exist.

You can also define subdomains within an added zone. For example, the following are all valid names within the zone `domain.example.com`.
* `subdomain.domain.example.com`
* `hostname.domain.example.com`
* `hostname.subdomain.domain.example.com`

The name `host.sub.domain.example.com` might be `host.sub` within the zone `domain.example.com`. It might also be `host.sub.domain` within the zone `example.com`. Both can exist at the same time, and are separate.

## Known limitations
{: #multi-level-limitations}

The DNS resolver always looks for a record from the longest matching zone, even though the record might not exist in the longest matching zone but does exist in another non-longest matching zone.

Let's say we have two zones, `domain.example.com` and `example.com`.

Records for `example.com`

```bash
 {
      myhost.domain.example.com A 1.1.1.1
      me.domain.example.com A 8.8.8.8
  }
```
{: screen}

Records for `domain.example.com`

```bash
  {
      myhost.domain.example.com A 2.2.2.2
  }
```
{: screen}

If a user queries for `myhost.domain.example.com`, the expected result (which is 2.2.2.2) should come from `domain.example.com`, because `domain.example.com` is the longest match with the user query.

If they queried for `me.domain.example.com` instead, the resolver searches only the longest matching zone. Because `me.domain.example.com` does not exist in `domain.example.com`, the result is an `NXDOMAIN`. 

## Creating a DNS zone in the UI
{: #create-dns-zone-ui}
{: ui}

1. From the Resource page, select the desired {{site.data.keyword.dns_short}} instance.
1. Click the **Create Zone** button on the **DNS Zones** page.
1. In the panel that appears, enter your zone name in the **Name** field. Optionally, enter **Label** and **Description** fields. See [Restricted DNS zone names(#restricted-dns-zone-names) for information about what names are not permitted.
1. Click **Create Zone**.

If the zone creation is successful, you are directed to the Zone Details page.

Newly added zones have a pending state until you add permitted networks to the zone. The zone becomes active after permitted networks are added.
{: note}

If the zone creation is unsuccessful, an error notification appears with information about what caused the error.

### Restricted DNS zone names
{: #restricted-dns-zone-names}
{: ui}

Subdomains to any of the restricted 2-level zones are not permitted. For example, `my.host.ibm.com` is a subdomain to `ibm.com`. Therefore, `my.host.ibm.com` is also a restricted zone.

The following DNS zone names are not permitted.
* `ibm.com`
* `softlayer.com`
* `bluemix.net`
* `softlayer.local`
* `mybluemix.net`
* `networklayer.com`
* `ibmcloud.com`
* `pdnsibm.net`
* `appdomain.cloud`
* `compass.cobaltiron.com`

## Edit a DNS zone in the UI
{: #edit-dns-zone-ui}
{: ui}

1. From the DNS Zones page, select your zone. **Label** and **Description** options appear.
2. Click the edit icon for **Label**, then enter the label and click **Save**.
3. Click the edit icon for **Description**, then enter the description and click **Save**.

## Delete a DNS zone in the UI
{: #delete-dns-zone-ui}
{: ui}

1. From the DNS Zones page, click the delete icon from the row for the zone you wish to delete. A confirmation dialog appears.
2. Click **Delete** button.

# Manage DNS zones from the CLI
{: #managing-dns-zones-cli}
{: cli}

Follow these [instructions](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands#cli-ref-prereqs) to install DNS Services CLI plugin.

First use `ibmcloud dns instances` command to list the DNS Services instances and then use the `ibmcloud dns instance-target` command to set the target operating DNS Services instance.

```bash
$ ibmcloud dns instances
Retrieving service instances for service 'dns-svcs' ...
OK

Name                 ID                                     Location   State    Service Name
DNS Services-km      ffffffff-b042-41fd-885e-000000000000   global     active   dns-svcs

$ ibmcloud dns instance-target "DNS Services-km"
```
{: pre}

## Create a DNS zone from the CLI
{: #create-dns-zone-cli}
{: cli}

Use the `ibmcloud dns zone-create` command followed by the zone name to create a zone.

```bash
$ ibmcloud dns zone-create example.com
Creating zone 'example.com' for service instance 'DNS Services-km' ...
OK

ID            example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae
Name          example.com
Description
Label
State         PENDING_NETWORK_ADD
Created On    2020-04-10 07:21:51.774444868 +0000 UTC
Modified On   2020-04-10 07:21:51.774444868 +0000 UTC
```
{: pre}

For future reference, the "ID" in output is used as variable `DNS_ZONE_ID`. Run this command to store it in variable `DNS_ZONE_ID`:

```bash
DNS_ZONE_ID="example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae"
```
{: codeblock}


## Get a DNS zone from the CLI
{: #get-dns-zone-cli}
{: cli}

Use the `ibmcloud dns zone` command followed by the zone ID to get details of an existing zone. 

```bash
$ ibmcloud dns zone $DNS_ZONE_ID
Getting zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK

ID            example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae
Name          example.com
Description
Label
State         PENDING_NETWORK_ADD
Created On    2020-04-10 07:21:51.774444868 +0000 UTC
Modified On   2020-04-10 07:21:51.774444868 +0000 UTC
```
{: pre}

## Update a DNS zone from the CLI
{: #update-dns-zone-cli}
{: cli}

Use the `ibmcloud dns zone-update` command followed by the zone ID to update a zone. Specify `-d, --description` to update the description and/or `-l, --label` to update the label of a zone.

```bash
$ ibmcloud dns zone-update $DNS_ZONE_ID -d "example zone" -l "us-south"
Updating zone 'example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae' for service instance 'DNS Services-km' ...
OK

ID            example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae
Name          example.com
Description   example zone
Label         us-south
State         PENDING_NETWORK_ADD
Created On    2020-04-10 07:21:51.774444868 +0000 UTC
Modified On   2020-04-10 07:38:36.712131819 +0000 UTC
```
{: pre}

## List DNS zones from the CLI
{: #list-dns-zones-cli}
{: cli}

Use the `ibmcloud dns zones` command to list all zones.

```bash
$ ibmcloud dns zones
Listing zones for service instance 'DNS Services-km' ...
OK

ID                                                      Name               Status
example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae        example.com        PENDING_NETWORK_ADD
```
{: pre}


## Delete a DNS zone from the CLI
{: #delete-dns-zone-cli}
{: cli}

Use the `ibmcloud dns zone-delete` followed by the zone ID to delete a zone.

```bash
ibmcloud dns zone-delete  $DNS_ZONE_ID
```
{: pre}

## Manage DNS zones with the API
{: #managing-dns-zones-api}
{: api}

First store the API endpoint in a variable so you can use it in API requests without having to type the full URL. For example, to store the production endpoint in a variable, run this command:

```bash
DNSSVCS_ENDPOINT=https://api.dns-svcs.cloud.ibm.com
```
{: pre}

To verify that this variable was saved, run `echo $DNSSVCS_ENDPOINT` and make sure the response is not empty.

## Authentication
{: #iam-authentication}
{: api}

The Authorization header is required for each API call. This header is the bearer token for the user, which can be retrieved from IAM (for example, using the `ibmcloud iam oauth-tokens` command).

You must obtain an IAM token and export it into the `$TOKEN` for {{site.data.keyword.dns_short}}.

## Create a DNS zone with the API
{: #create-dns-zone-api}
{: api}

Create a new zone by using the following `curl` command:

### Request
{: #create-dns-zone-request}
{: api}

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones \
  -H "Authorization: $TOKEN" \
  -d '{
  "name": "example.com",
  "description": "Example zone"
}'
```
{: pre}

### Response 
{: #create-dns-zone-response}
{: api}

```json
{
    "success": true,
    "result": {
        "id": "ed10e4b2-8a64-4afa-a4e2-9e60a766d079",
        "created_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
        "modified_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
        "instance_id": "1a34bda8-9c94-4232-bea7-7df163b21d23",
        "name": "example.com",
        "description": "Example zone",
        "state": "PENDING_NETWORK_ADD",
        "tag": "example.com:ed10e4b2-8a64-4afa-a4e2-9e60a766d079"
    },
    "errors": [],
    "messages": []
}
```
{: codeblock}

For future reference, the "id" in response is used as `DNSZONE_ID`. 
{: note}

## Get a DNS zone with the API
{: #get-dns-zone-api}
{: api}

Use the following command to get an existing zone. 

### Request 
{: #get-zone-request}
{: api}

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID \
  -H "Authorization: $TOKEN"
```
{: pre}

### Response
{: #get-zone-response}
{: api}

```json
{
    "success": true,
    "result": {
        "id": "example.com:ed10e4b2-8a64-4afa-a4e2-9e60a766d079",
        "created_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
        "modified_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
        "instance_id": "1a34bda8-9c94-4232-bea7-7df163b21d23",
        "name": "example.com",
        "description": "Example zone",
        "state": "PENDING_NETWORK_ADD"
    },
    "errors": [],
    "messages": []
}
```
{: codeblock}

## Updating a DNS zone with the API
{: #update-dns-zone-api}
{: api}

Use the following command to update an existing zone. You can update the description and label fields. All other fields are read-only.

### Request 
{: #update-zone-request}
{: api}

```bash
curl -X PATCH \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID \
  -H 'Content-Type: application/json' \
  -H "Authorization: $TOKEN" \
  -d '{
    "description": "The DNS zone is used for VPCs in us-east region",
    "label": "us-east"
}'

```
{: pre}

### Response
{: #update-zone-response}
{: api}

```json
{
  "created_on": "2019-01-01T05:20:00.12345Z",
  "description": "The DNS zone is used for VPCs in us-east region",
  "id": "example.com:2d0f862b-67cc-41f3-b6a2-59860d0aa90e",
  "instance_id": "1407a753-a93f-4bb0-9784-bcfc269ee1b3",
  "label": "us-east",
  "modified_on": "2019-01-01T05:20:00.12345Z",
  "name": "example.com",
  "state": "PENDING_NETWORK_ADD"
}
```
{: codeblock}


## List DNS zones with the API
{: #list-dns-zones-api}
{: api}

List one or more zones in your domain by using the following `curl` command: 

### Request
{: #list-zone-request}
{: api}

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones \
  -H "Authorization: $TOKEN"
```
{: pre}

### Response
{: #list-zone-response}
{: api}

```json
{
    "success": true,
    "result": [
        {
            "id": "example.com:ed10e4b2-8a64-4afa-a4e2-9e60a766d079",
            "created_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
            "modified_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
            "instance_id": "1a34bda8-9c94-4232-bea7-7df163b21d23",
            "name": "example.com",
            "description": "Example zone",
            "state": "PENDING_NETWORK_ADD"
        }
    ],
    "errors": [],
    "messages": []
}
```
{: codeblock}

### Delete a DNS zone with the API
{: #delete-dns-zone-api}
{: api}

#### Request
{: #delete-zone-request}
{: api}

```bash
curl -X DELETE \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID \
  -H "Authorization: $TOKEN"
```
{: pre}

#### Response
{: #delete-zone-response}
{: api}

```bash
HTTP/2 204 No Content
```
{: codeblock}

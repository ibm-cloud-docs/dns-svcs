---

copyright:
  years: 2019, 2020
lastupdated: "2020-08-14"

keywords: restricted zones

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Managing DNS zones
{: #managing-dns-zones}

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

## Using the {{site.data.keyword.cloud_notm}} console
{: #managing-dns-zones-ui}

DNS zones can be managed through the {{site.data.keyword.cloud}} console, or the API. The following sections cover the console usage.
{: shortdesc}

### Creating a DNS zone
{: #create-dns-zone-ui}

1. From the Resource page, select the desired {{site.data.keyword.dns_short}} instance.
1. Click the **Create Zone** button on the **DNS Zones** page.
1. In the panel that appears, enter your zone name in the **Name** field. Optionally, enter **Label** and **Description** fields. See [Restricted DNS zone names(#restricted-dns-zone-names) for information about what names are not permitted.
1. Click **Create Zone**.

If the zone creation is successful, you are directed to the Zone Details page.

Newly added zones have a pending state until you add permitted networks to the zone. The zone becomes active after permitted networks are added.
{: note}

If the zone creation is unsuccessful, an error notification appears with information about what caused the error.

#### Restricted DNS zone names
{: #restricted-dns-zone-names}

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

### Editing a DNS zone
{: #edit-dns-zone-ui}

1. From the DNS Zones page, select your zone. **Label** and **Description** options appear.
2. Click the edit icon for **Label**, then enter the label and click **Save**.
3. Click the edit icon for **Description**, then enter the description and click **Save**.

### Deleting a DNS zone
{: #delete-dns-zone-ui}

1. From the DNS Zones page, click the delete icon from the row for the zone you wish to delete. A confirmation dialog appears.
2. Click **Delete** button.

## Using the API
{: #managing-dns-zones-api}

First store the API endpoint in a variable so you can use it in API requests without having to type the full URL. For example, to store the production endpoint in a variable, run this command:

```bash
DNSSVCS_ENDPOINT=https://api.dns-svcs.cloud.ibm.com
```
{: pre}

To verify that this variable was saved, run `echo $DNSSVCS_ENDPOINT` and make sure the response is not empty.

### Authentication
{: #iam-authentication}

The Authorization header is required for each API call. This header is the bearer token for the user, which can be retrieved from IAM (for example, using the `ibmcloud iam oauth-tokens` command).

You must obtain an IAM token and export it into the `$TOKEN` for {{site.data.keyword.dns_short}}.

### Creating a DNS zone
{: #create-dns-zone-api}

Create a new zone by using the following `curl` command:

#### Request creating a DNS zone
{: #create-dns-zone-request}

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

#### Response to creating a DNS zone
{: #create-dns-zone-response}

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

### Getting a DNS zone
{: #get-dns-zone-api}

Use the following command to get an existing zone. 

#### Request getting a DNS zone
{: #get-zone-request}

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID \
  -H "Authorization: $TOKEN"
```
{: pre}

#### Response to getting a DNS zone
{: #get-zone-response}

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

### Updating a DNS zone
{: #update-dns-zone-api}

Use the following command to update an existing zone. You can update the description and label fields. All other fields are read-only.

#### Request update a DNS zone
{: #update-zone-request}

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

#### Response to update a DNS zone
{: #update-zone-response}

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


### Listing DNS zones
{: #list-dns-zones-api}

List one or more zones in your domain by using the following `curl` command: 

#### Request
{: #list-zone-request}

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones \
  -H "Authorization: $TOKEN"
```
{: pre}

#### Response
{: #list-zone-response}

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

### Deleting a DNS zone
{: #delete-dns-zone-api}

#### Request
{: #delete-zone-request}

```bash
curl -X DELETE \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID \
  -H "Authorization: $TOKEN"
```
{: pre}

#### Response
{: #list-zone-response}

```bash
HTTP/2 204 No Content
```
{: codeblock}

## Using the CLI
{: #managing-dns-zones-cli}

Follow these [instructions](/docs/dns-svcs?topic=dns-svcs-cli-plugin-dns-services-cli-commands#cli-ref-prereqs) to install DNS Services CLI plugin.

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


### Creating a DNS zone
{: #create-dns-zone-cli}

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


### Getting a DNS zone
{: #get-dns-zone-cli}

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


### Updating a DNS zone
{: #update-dns-zone-cli}

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

### Listing DNS zones
{: #list-dns-zones-cli}

Use the `ibmcloud dns zones` command to list all zones.

```bash
$ ibmcloud dns zones
Listing zones for service instance 'DNS Services-km' ...
OK

ID                                                      Name               Status
example.com:f7f40364-a5e6-48f7-9fc9-387434c579ae        example.com        PENDING_NETWORK_ADD
```
{: pre}


### Deleting a DNS zone
{: #delete-dns-zone-cli}

Use the `ibmcloud dns zone-delete` followed by the zone ID to delete a zone.

```bash

```
{: pre}

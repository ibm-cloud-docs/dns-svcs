---

copyright:
  years: 2022
lastupdated: "2022-06-24"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Understanding cross-account access
{: #cross-account-about}

Securely share DNS zones between IBM cloud accounts by enabling cross-account access.
{: shortdesc}

With cross-account access, you can have DNS zones and resource records information that are completely private. Only VPCs that are associated with the DNS zone are able to access the data over a private network on IBM Cloud. The DNS zone and records cannot be publicly accessed from the internet.


Previously, only VPCs from the same account as the provisioned DNS zone could access the DNS zone. With cross-account access, VPCs from separate accounts can now be granted access.

## Features of cross-account access
{: #cross-account-acl-features}

The cross-account access feature is offered with {{site.data.keyword.dns_full}} (Standard plan) and is available through UI, CLI and API. After getting the zone ID and ID of the owner's {{site.data.keyword.dns_short}} instance, you (as a requestor) can create a linked zone in your {{site.data.keyword.dns_short}} instance.

As a requestor, you create a linked zone and request access to the resources in the other account. The owner then reviews the cross-account access request, and approves or rejects your request. After the request is approved, you can add their resources as permitted networks in your account.

## Understanding key terms
{: #key-terms}

To understand the overall design of the cross-account access feature, it helps to understand some key terms:

Linked zone
:   When you need to access DNS resource records from private DNS zones that are defined in another account, you can create a request to access the zone in the other account. Then, you can add the DNS resource records from the other account as a linked zone in your {{site.data.keyword.dns_short}} instance.

Cross-account access
:   When a requestor creates a linked zone based on the zone ID and ID of the instance provided by the owner, the owner receives a cross-account access request for the zone.

## Example for cross-account access workflow
{: #cross-account-example}

In this example, a customer has multiple IBM Cloud accounts based on their business units.

* Account `A` is an IT service unit which provides services, for example, a database.
* Account `B` is the production unit.

Account `A` created the private DNS zone `services.customer.com` and, in this zone, they have a resource record for `database.services.customer.com`.

Because the production unit needs access to the database, it must be able to resolve the resource record `databases.services.customer.com` from VPCs in account `B`. To accomplish this, the administrator of account `B` does the following:

1. Creates a {{site.data.keyword.dns_short}} instance `Private DNS-1`
1. Gets the zone ID and ID of the instance from account `A`
1. Creates a linked zone in instance `Private DNS-1`
1. Waits for the cross-account access request approval from the administrator of account `A`
1. After the request is approved, adds VPCs from account `B` as permitted networks in account `A`


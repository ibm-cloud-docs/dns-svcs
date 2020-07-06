---

copyright:

  years: 2019, 2020

lastupdated: "2020-07-06"

keywords: dns, dns-svcs, DNS Services, Private DNS, dns vpc, Access Control Lists, IAM, permitted networks

subcollection: dns-svcs

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Managing IAM and {{site.data.keyword.dns_full_notm}}
{: #iam}

{{site.data.keyword.dns_full}} leverages IAM to perform authorization and Authentication.

Access to {{site.data.keyword.dns_short}} instances for users in your account is controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). Every user that accesses the {{site.data.keyword.dns_short}} in your account must be assigned an access policy with an IAM role defined. The policy determines what actions a user can perform within the context of the service or instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.cloud_notm}} service as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles.

Policies enable you to grant access at different levels. Some of the options include the following:

- Access across all instances of the service in your account.
- Access to an individual service instance in your account.
- Access to a specific resource within an instance.

## Roles and permissions
{: #roles-and-permissions}

With {{site.data.keyword.cloud_notm}} IAM, you can manage and define access for users and resources in your account.

To simplify access, {{site.data.keyword.dns_short}} aligns with {{site.data.keyword.cloud_notm}} IAM roles so that each user has a different view of the service, according to the role the user is assigned. If you are a security admin for your service, you can assign {{site.data.keyword.cloud_notm}} IAM roles that correspond to the specific {{site.data.keyword.dns_full}} permissions you want to grant to members of your team.

This section discusses {{site.data.keyword.cloud_notm}} IAM in the context of {{site.data.keyword.dns_short}}. For complete IAM documentation, see [Managing access](/docs/iam?topic=iam-cloudaccess) in {{site.data.keyword.cloud_notm}}.
{:note}

### Platform access roles
{: #platform-access-roles}

Use platform access roles to grant permissions at the account level, such as the ability to create or delete {{site.data.keyword.dns_short}} instances in your {{site.data.keyword.cloud_notm}} account.

| Action	                                       | Role                                     |
| ---------------------------------------------- | :--------------------------------------- |
|View {{site.data.keyword.dns_full}} instances 	 | Administrator, Operator, Editor, Viewer  |
|Create {{site.data.keyword.dns_full}} instances | Administrator, Editor                    |
|Delete {{site.data.keyword.dns_full}} instances | Administrator, Editor                    |

### Service access roles
{: #service-access-roles}

Use service access roles to grant permissions at the service level, such as the ability to view, create, or delete DNS zones, resource records, and permitted networks.

The following table shows how service access roles map to {{site.data.keyword.dns_short}} permissions.

| Role    | Description       | Actions  |
| :------ | :---------------- | :------- |
| Reader  | A reader can browse a high-level view of DNS zones, resource records, and permitted networks. Readers cannot create, delete or modify any resources under {{site.data.keyword.dns_short}} instances. | View DNS zones, resource records, and permitted networks. |
| Writer  | A writer can modify DNS zones and resource records, in addition to actions that a reader can perform. | All actions that a reader can perform, also can update DNS zones and resource records. |
| Manager | A manager can perform all actions that a reader and writer can perform, including the ability to create and delete DNS zones, create and delete resource records, and also add and remove permitted networks. | All actions that a Reader or a Writer can perform, also can create and delete DNS zones. Additionally, can create and delete resource records, and add or remove permitted networks. |

## Working with permitted network (VPC) related IAM access
{: #permitted-network-vpc-access-roles}

To add a VPC into permitted networks for a DNS zone, users must have the **Operator** role on the VPC resource. The permission can be granted to any user by creating an IAM access policy with the following assignments in {{site.data.keyword.cloud_notm}} UI:
1. Select **VPC Infrastructure** for *What type of access do you want to assign?*.
1. Select **Virtual Private Cloud** for *Resource Type*.
1. Choose the appropriate VPC under *VPC ID*.

To learn more about providing Operator level access to the VPC, see [VPC: Getting started with IAM](/docs/vpc?topic=vpc-iam-getting-started).

---

copyright:
  years:  2023
lastupdated: "2023-01-13"

keywords: context-based restrictions for dns services

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Protecting {{site.data.keyword.dns_short}} resources with context-based restrictions (limited availability)
{: #cbr}

Context-based restrictions give account owners and administrators the ability to define and enforce access restrictions for {{site.data.keyword.cloud}} resources based on the context of access requests. Access to {{site.data.keyword.dns_full_notm}} resources can be controlled with context-based restrictions and identity and access management (IAM) policies.
{: shortdesc}

The preview of this functionality is available only to authorized accounts. {: preview}

These restrictions work with traditional IAM policies, which are based on identity, to provide an extra layer of protection. Unlike IAM policies, context-based restrictions don't assign access. Context-based restrictions check that an access request comes from an allowed context that you configure. Since both IAM access and context-based restrictions enforce access, context-based restrictions offer protection even in the face of compromised or mismanaged credentials. For more information, see [What are context-based restrictions](/docs/account?topic=account-context-restrictions-whatis).

A user must have the `Administrator` role on the {{site.data.keyword.dns_short}} service to create, update, or delete rules. And a user must have either the `Editor` or `Administrator` role on the Context-based restrictions service to create, update, or delete network zones. A user with the `Viewer` role on the Context-based restrictions service can only add network zones to a rule. 
{: note}

Any {{site.data.keyword.cloudaccesstraillong_notm}} or audit log events generated come from the context-based restrictions service, not {{site.data.keyword.dns_short}}. For more information, see [Monitoring context-based restrictions](/docs/account?topic=account-cbr-monitor).

To get started protecting your {{site.data.keyword.dns_short}} resources with context-based restrictions, see the tutorial for [Leveraging context-based restrictions to secure your resources](/docs/account?topic=account-context-restrictions-tutorial).

## Creating network zones
{: #network-zone}

A network zone represents an allowlist of IP addresses where an access request is created. It defines a set of one or more network locations that are specified by the following attributes:

- IP addresses, which include individual addresses, ranges, or subnets
- VPCs

### Creating network zones by using the API
{: #network-zone-api} 
{: api}

You can create network zones by using the `create-zone` command. For more information, see the [API docs](/apidocs/context-based-restrictions#create-zone).

The `addresses` attribute specifies individual IP addresses, ranges, subnets, and VPCs where requests originating from are permitted. 
{: tip}

```json
{
    "name": "example-zone",
    "description": "this is an example of zone",
    "account_id": "12ab34cd56ef78ab90cd12ef34ab56cd",
    "addresses": [
        {
            "type": "ipAddress",
            "value": "169.23.56.234"
        },
        {
            "type": "ipRange",
            "value": "169.23.22.0-169.23.22.255"
        },
        {
            "type": "subnet",
            "value": "192.0.2.0/24"
        },
        {
            "type": "vpc",
            "value": "crn:v1:bluemix:public:is:us-south:a/12ab34cd56ef78ab90cd12ef34ab56cd::vpc:r134-d98a1702-b39a-449a-86d4-ef8dbacf281e"
        }
    ]
}
```
{: codeblock}

```json
{
  "id": "65810ac762004f22ac19f8f8edf70a34",
  "crn": "crn:v1:bluemix:public:context-based-restrictions:global:a/12ab34cd56ef78ab90cd12ef34ab56cd::zone:65810ac762004f22ac19f8f8edf70a34",
  "name": "example-zone",
  "description": "this is an example of zone",
  "account_id": "12ab34cd56ef78ab90cd12ef34ab56cd",
  "addresses": [
    {
      "type": "ipAddress",
      "value": "169.23.56.234"
    },
    {
      "type": "ipRange",
      "value": "169.23.22.0-169.23.22.255"
    },
    {
      "type": "subnet",
      "value": "192.0.2.0/24"
    },
    {
      "type": "vpc",
      "value": "crn:v1:bluemix:public:is:us-south:a/12ab34cd56ef78ab90cd12ef34ab56cd::vpc:r134-d98a1702-b39a-449a-86d4-ef8dbacf281e"
    }
  ],
  "address_count": 4,
  "excluded_count": 0,
  "href": "https://cbr.cloud.ibm.com/v1/zones/65810ac762004f22ac19f8f8edf70a34",
  "created_at": "2020-11-23T02:01:59Z",
  "created_by_id": "IBMid-120000P1JM",
  "last_modified_at": "2022-09-26T02:01:59Z",
  "last_modified_by_id": "IBMid-120000P1JM"
}
```
{: codeblock}

### Creating network zones by using the CLI
{: #network-zone-cli} 
{: cli}

1. To create network zones from the CLI, [install the CBR CLI plug-in](/docs/account?topic=cli-cbr-plugin#install-cbr-plugin).
2. Use the `cbr-zone-create` command to add network locations and VPCs to network zones. For more information, see the CBR
   [CLI reference](/docs/account?topic=cli-cbr-plugin#cbr-zones-cli).

   The following example command adds an individual IP, range, subnet, and a VPC to a network zone.

   ```sh
   ibmcloud cbr zone-create --name example-zone --description "this is an example of zone" --addresses 169.23.56.234,169.23.22.0-169.23.22.255,192.0.2.0/24 --vpc crn:v1:bluemix:public:is:us-south:a/12ab34cd56ef78ab90cd12ef34ab56cd::vpc:r134-d98a1702-b39a-449a-86d4-ef8dbacf281e
   ```
   {: pre}
   
## Limitations
{: #cbr-limitations}

Context-based restrictions protect only the actions associated with the [DNS Services API](/apidocs/dns-svcs). Actions associated with the following platform APIs are not protected by context-based restrictions. Reference the API docs for the specific action IDs.

- [Resource Instance APIs](/apidocs/resource-controller/resource-controller#list-resource-instances)
- [Resource Keys APIs](/apidocs/resource-controller/resource-controller#list-resource-keys)
- [Resource Bindings APIs](/apidocs/resource-controller/resource-controller#list-resource-bindings)
- [Resource Aliases APIs](/apidocs/resource-controller/resource-controller#list-resource-aliases)
- [IAM Policy APIs](/apidocs/iam-policy-management#list-policies)
- [Global Search APIs](/apidocs/search)
- Global Tagging [Attach](/apidocs/tagging#attach-tag) and [Detach](/apidocs/tagging#detach-tag) APIs
- [Context-based Restriction Rule APIs](/apidocs/context-based-restrictions#create-rule)

### DNS Services CBR Limitations
{: #cbr-dns-limitations}

- The CBR rules created on {{site.data.keyword.dns_short}} don't apply to platform actions such as Global Search and Tagging, resource instance creation and deletion on {{site.data.keyword.dns_short}} instances. You can still view {{site.data.keyword.dns_short}} instances on IBM Cloud Resource Explorer.
- When you create a rule, it might take up to 10 minutes to become enforced.
- At this time {{site.data.keyword.cloud_notm}} console cannot be used to create context-based restriction rules for {{site.data.keyword.dns_short}}.

## Creating rules
{: #cbr-rules}

Context-based restrictions for {{site.data.keyword.dns_short}} can be scoped to a service instance or resource group by using resource attributes.

You can select a service instance by entering the ID. Alternatively, you can use the `*` wildcard to select all applicable service instances. You can also specify which resource group the rule is applied to in the command.

### Creating rules by using the API
{: #rules-api} 
{: api}

Review the following example requests to create rules. For more information about the `v1/rules` API, see the [API docs](/apidocs/context-based-restrictions#create-rule).

When you create a rule with context attribute to restrict requests to private endpoint, it is not possible to restrict access to an overlay IP for an individual VPC virtual server instance or bare-metal server. You must specify the VPC zone's underlay IP addresses, which are also known as Cloud Service Endpoint IPs.
{: note}

The following example payload creates a rule that protects the {{site.data.keyword.dns_short}} instance and allows access only from the specified network zone via a private endpoint.

```json
{
  "contexts": [
    {
      "attributes": [
        {
          "name": "endpointType",
          "value": "private"
        },
        {
          "name": "networkZoneId",
          "value": "65810ac762004f22ac19f8f8edf70a34"
        }
      ]
    }
  ],
  "resources": [
    {
      "attributes": [
        {
          "name": "serviceName",
          "value": "dns-svcs"
        },
        {
          "name": "serviceInstance",
          "operator": "stringEquals",
          "value": "3bd0bc3c-232c-4886-a0c4-72aa26ec0d38"
        }
      ]
    }
  ]
}
```
{: codeblock}

### Creating rules by using the CLI
{: #rules-cli} 
{: cli}

1. To create rules from the CLI, [install the CBR CLI plug-in](/docs/account?topic=cli-cbr-plugin#install-cbr-plugin).
1. Use the [`ibmcloud cbr rule-create` command](/docs/account?topic=cli-cbr-plugin#cbr-cli-rule-create-command) to create CBR rules. For more information, see the CBR [CLI reference](/docs/account?topic=cli-cbr-plugin#cbr-zones-cli).

The examples in this section are enforcement rules. You can make them report-only by adding `--enforcement-mode report`.

The following example CLI command creates a context-based restriction rule for a {{site.data.keyword.dns_short}} instance in the current account:

```sh
ibmcloud cbr rule-create  --zone-id 65810ac762004f22ac19f8f8edf70a34 --description "example CBR rule" --service-name dns-svcs --service-instance 3bd0bc3c-232c-4886-a0c4-72aa26ec0d38
```
{: pre} 

## How {{site.data.keyword.dns_short}} authorizes VPC resource access
{: #authorizing-resource-access}

{{site.data.keyword.dns_short}} requires you have appropriate access to VPC resources in one of the following operations:

* Add a VPC to permitted networks of a DNS zone.
* Create custom resolver on a particular VPC.
* Create GLB origin pool with healthcheck on VPC subnets. 

You must work with an account administrator to ensure appropriate VPC operator permission for IAM access policy, and to ensure that no CBR rules blocking you operate on the VPC. For the latter two operations, you must also have subnet reader permission and ensure no CBR rules blocking you get details of the subnets.
{: tip}

## Monitoring context-based restrictions in {{site.data.keyword.dns_short}}
{: #cbr-monitoring}

The context-based restriction service generates audit logs every time a context-based rule is enforced. For more information, see
[Monitoring context-based restrictions](/docs/account?topic=account-cbr-monitor).

Activity tracker events that are generated by the context-based restriction service contain a *CorrelationId* field. You can search the value of this field to find the audit events that are generated by {{site.data.keyword.dns_short}}.

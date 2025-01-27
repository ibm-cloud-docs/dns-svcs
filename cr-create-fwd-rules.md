---

copyright:
  years: 2021, 2025
lastupdated: "2025-01-16"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Adding custom resolver forwarding rules
{: #cr-fwd-rules-add}

Use forwarding rules to configure where to forward DNS queries for resolution by using the UI, CLI, or API.
{: shortdesc}

Forwarding rules are configurations that you can set up to direct DNS queries to specific DNS resolvers. Two required parameters and two optional parameters need to be provided to setup a forwarding rule. At least one of the optional parameters needs to be configured:

* **Rule Type**: Currently only DNS Zone is supported.
* **Match**: The DNS Zone for which you want the DNS query forwarded.
* **Forwarding IP addresses (optional)**: The IP addresses of the DNS resolvers to which the query is forwarded. If multiple addresses are provided, the custom resolver goes through the list by using a sequential policy that selects hosts based on sequential ordering until a resolver responds.

    VPC network behavior and your VPC network configurations can also affect traffic to and from custom resolvers that are located on your VPC. For example, if you want to create a forwarding rule to a DNS resolver on the external internet for DNS queries matching a certain DNS zone, you must create a public gateway to allow external connectivity for your custom resolvers. See [About networking for VPC](/docs/vpc?topic=vpc-about-networking-for-vpc) for more information on VPC networking.
    {: tip}
* **Views (optional)**: Composed of an expression that when evaluated to true forwards the DNS query to the specified DNS resolvers.

After a rule is configured and the custom resolver is enabled, DNS query requests go to the custom resolver first.

Then, the custom resolver checks if the query is for any rules that have been configured by comparing against the Match value. If a rule exists for the DNS query, the custom resolver forwards the DNS query to the specified DNS resolver in the configured rule. If _no_ rules exist that matches the DNS query, the custom resolver forwards the DNS query to the specified DNS resolver in the default forwarding rule.

Custom resolvers support two types of forwarding rules:

* **DNS Zone** rules apply for a zone name.
* The **Default** rule is configured to forward queries to DNS Services DNS resolvers (`161.26.0.7`, `161.26.0.8`). Only one default rule is allowed per custom resolver; it can be edited, but cannot be deleted.

    Changing the Default rule might cause issues with DNS query resolution in VPCs that have virtual private endpoints, IKS clusters, ROKS clusters, or defined private DNS zones.
    {: important}

## Adding custom resolver forwarding rules in the UI
{: #ui-add-fwd-rules}
{: ui}

To add a forwarding rule:
1. Go to the custom resolver details page and select the **Forwarding rules** tab.
1. Click **Add rule**.
1. In the Create forwarding rule panel, select the rule type from the list menu.
1. Enter the matching zone.
1. Enter the forwarding IP addresses (in CIDR format) separated by commas.
1. Optionally, enter a description of the rule.
1. Click **Create**.

## Adding custom resolver forwarding rules from the CLI
{: #cli-add-fwd-rules}
{: cli}

To create a custom resolver forwarding rule by using the CLI, run the following command:

`ibmcloud dns custom-resolver-forwarding-rule-create RESOLVER_ID --type TYPE --match HOSTNAME --dns-svcs IPs [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **-t, --type** is the type of the forwarding rule. Valid values: "zone".
- **-d, --description** is the descriptive text of the custom resolver forwarding rule.
- **-match** is the matching zone.
- **--dns-svcs** is the upstream DNS servers to be forwarded to.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used instead.
- **--output** specifies output format. Currently, JSON is the only supported format.

## Adding custom resolver forwarding rules with the API
{: #api-add-fwd-rules}
{: api}

To create a custom resolver forwarding rule using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, create your custom resolver forwarding rule:

    ```sh
    {
      "description": "forwarding rule",
      "type": "zone",
      "match": "example.com",
      "forward_to": [
        "161.26.0.7"
      ]
    }
    ```
    {: codeblock}

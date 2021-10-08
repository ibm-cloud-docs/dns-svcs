---

copyright:
  years: 2021
lastupdated: "2021-07-13"

keywords:

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
{:beta: .beta}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic”}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}

# Adding custom resolver forwarding rules
{: #cr-fwd-rules-add}

This custom resolver feature is available to {{site.data.keyword.dns_short}} users with a Standard plan.
{: beta}

Use forwarding rules to configure where the DNS queries should be forwarded to for resolution.
{: shortdesc}

Custom resolvers support three types of forwarding rules:

* **DNS Zone** rules apply for a zone name.
* **Hostname** rules apply for a given hostname.
* The **Default** rule is configured to forward queries to DNS Services DNS resolvers (`161.26.0.7`, `161.26.0.8`). Only one default rule is allowed per custom resolver; it can be edited, but cannot be deleted.

    Changing the Default rule might cause issues with DNS query resolution in VPCs that have virtual private endpoints, IKS clusters, ROKS clusters, or defined private DNS zones.
    {: important}

## Adding custom resolver forwarding rules using the UI
{: #ui-add-fwd-rules}
{: ui}

To add a forwarding rule:
1. Click **Add rule**.
1. In the Create forwarding rule panel, select the rule type from the list menu.
1. Enter the match criteria.
1. Enter the forwarding IP addresses (in CIDR format) separated by commas.
1. Optionally, enter a description of the rule.
1. Click **Create**.

## Adding custom resolver forwarding rules using the CLI
{: #cli-add-fwd-rules}
{: cli}

To create a custom resolver forwarding rule using the CLI, run the following command:

`ibmcloud dns custom-resolver-forwarding-rule-create RESOLVER_ID --type TYPE --match HOSTNAME --dns-svcs IPs [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **-t, --type** is the type of the forwarding rule. Valid values: "zone".
- **-d, --description** is the descriptive text of the custom resolver forwarding rule.
- **-match** is the matching zone or hostname.
- **--dns-svcs** is the upstream DNS servers to be forwarded to.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by dns instance-target INSTANCE is used instead.
- **--output** specifies output format. Currently, JSON is the only supported format.

## Adding custom resolver forwarding rules using the API
{: #api-add-fwd-rules}
{: api}

To create a custom resolver forwarding rule using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, create your custom resolver forwarding rule:

    ```
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

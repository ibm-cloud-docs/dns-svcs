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

# Updating custom resolver forwarding rules
{: #cr-fwd-rules-update}

This custom resolver feature is available to {{site.data.keyword.dns_short}} users with a Standard plan. 
{: beta}

You can update custom resolver forwarding rules in {{site.data.keyword.dns_full}} by using the UI, CLI, or API. 
{: shortdesc}

Changing the Default rule might cause issues with DNS query resolution in VPCs that have virtual private endpoints, IKS clusters, ROKS clusters, or defined private DNS zones.
{: important}

## Updating custom resolver forwarding rules using the UI
{: #ui-cr-fwd-rules-update}
{: ui}

You can edit custom resolver forwarding rules from the custom resolver details page.

To edit a forwarding rule:
1. Click the overflow menu next to the rule you want to edit.
1. In the panel that appears, change the match conditions, forwarding IP addresses, or description.
1. Click **Save** to commit your changes, or click **Cancel** to discard them.

    You cannot edit the rule type. If you require a different rule type, create a new rule.
    {: tip}

## Updating custom resolver forwarding rules using the CLI
{: #cli-cr-fwd-rules-update}
{: cli}

To update a custom resolver forwarding rule using the CLI, run the following command:

`ibmcloud dns custom-resolver-forwarding-rule-update RESOLVER_ID RULE_ID [--match HOSTNAME] [--dns-svcs IPs] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **RULE_ID** is the ID of custom resolver forwarding rule.
- **-d, --description** is the descriptive text of the custom resolver forwarding rule.
- **-match** is the matching zone or hostname.
- **--dns-svcs** is the upstream DNS servers to be forwarded to.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by dns instance-target INSTANCE is used instead.
- **--output** specifies output format. Currently, JSON is the only supported format.

## Updating custom resolver forwarding rules using the API
{: #api-cr-fwd-rules-update}
{: api}

To update a custom resolver forwarding rule using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `rule_id`, which is the unique identifier of a forwarding rule.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all viariables are initiated, update your custom resolver forwarding rule:

    ```
    {
      "description": "forwarding rule",
      "match": "example.com",
      "forward_to": [
        "161.26.0.7"
      ]
    }
    ```
    {: codeblock}

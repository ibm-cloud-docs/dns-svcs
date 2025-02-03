---

copyright:
  years: 2021, 2025
lastupdated: "2025-02-03"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Updating custom resolver forwarding rules
{: #cr-fwd-rules-update}

You can update custom resolver forwarding rules in {{site.data.keyword.dns_full}} by using the UI, CLI, or API.
{: shortdesc}

Changing the Default rule might cause issues with DNS query resolution in VPCs that have virtual private endpoints, IKS clusters, ROKS clusters, or defined private DNS zones.
{: important}

## Updating custom resolver forwarding rules in the UI
{: #ui-cr-fwd-rules-update}
{: ui}

You can edit custom resolver forwarding rules from the custom resolver details page.

To edit a forwarding rule:
1. Click the **Forwarding rules** tab.
1. Click the overflow menu next to the rule you want to edit or click on the forwarding rules row to open the view panel and click **Edit** button.
1. In the panel that appears, change the match conditions, forwarding IP addresses, DNS views or description.
1. Click **Save** to commit your changes, or click **Cancel** to discard them.

    You cannot edit the rule type. If you require a different rule type, create a new rule.
    {: tip}

## Updating custom resolver forwarding rules from the CLI
{: #cli-cr-fwd-rules-update}
{: cli}

To update a custom resolver forwarding rule using the CLI, run the following command:

`ibmcloud dns custom-resolver-forwarding-rule-update RESOLVER_ID RULE_ID [--match HOSTNAME] [--dns-svcs IPs] [--description DESCRIPTION] [--add-view VIEW_PARAMETER --add-view VIEW_PARAMETER ...] [--update-view VIEW_PARAMETER --update-view VIEW_PARAMETER] [--reorder-view REORDER_VIEW_PARAMETER] [--remove-view VIEW_NAME --remove-view VIEW_NAME] [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **RULE_ID** is the ID of custom resolver forwarding rule.
- **-d, --description** is the descriptive text of the custom resolver forwarding rule.
- **-match** is the matching zone or hostname.
- **--dns-svcs** is the upstream DNS servers to be forwarded to.
- **--add-view** is the value of the view parameters to be added in the forwarding rule.
- **--update-view** is the value of the view parameters to be updated.
- **--reorder-view** is the name of the views to be reordered.
- **--remove-view** is the name of the view to be removed.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by dns instance-target INSTANCE is used instead.
- **--output** specifies output format. Currently, JSON is the only supported format.

## Updating custom resolver forwarding rules with the API
{: #api-cr-fwd-rules-update}
{: api}

To update a custom resolver forwarding rule using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `rule_id`, which is the unique identifier of a forwarding rule.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, update your custom resolver forwarding rule:

    ```sh
    {
      "description": "forwarding rule",
      "match": "example.com",
      "forward_to": [
        "161.26.0.7"
      ],
      "views": [
        {
          "name": "view name",
          "description": "view description",
          "forward_to": [
            "161.26.0.7"
          ],
          "expression": "ipInRange(source.ip,'10.11.12.0/24')"
        }
      ]
    }
    ```
    {: codeblock}

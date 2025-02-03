---

copyright:
  years: 2021, 2025
lastupdated: "2025-02-03"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Viewing details of custom resolver forwarding rules
{: #cr-fwd-rules-detail}

You view details of a single custom resolver forwarding rule and view a list of all custom resolver forwarding rules in {{site.data.keyword.dns_full}} by using the UI, CLI, or API.
{: shortdesc}

## Viewing custom resolver forwarding rules in the UI
{: #ui-cr-fwd-rules-view}
{: ui}

View the details of a custom resolver forwarding rule by navigating to the **Forwarding rules** tab in the custom resolver details page.

The Forwarding rules section lists all custom resolver rules associate with the custom resolver. To view the details of a specific forwarding rule, click on a row to see the configuration in more detail.

## Viewing custom resolver forwarding rules from the CLI
{: #cli-cr-fwd-rules-view}
{: cli}

To get the details of a custom resolver forwarding rule using the CLI, run the following command:

`ibmcloud dns custom-resolver-forwarding-rule RESOLVER_ID RULE_ID [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **RULE_ID** is the ID of custom resolver forwarding rule.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by dns instance-target INSTANCE is used instead.
- **--output** specifies output format. Currently, JSON is the only supported format.

### Listing all custom resolvers forwarding rule
{: #cli-list-fwd-rules}

To list all custom resolver forwarding rules using the CLI, run the following command:

`ibmcloud dns custom-resolver-forwarding-rules RESOLVER_ID [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used instead.
- **--output** specifies output format. Currently, JSON is the only supported format.


## Viewing custom resolver forwarding rules with the API
{: #api-cr-fwd-rules-view}
{: api}

To view the details of a custom resolver forwarding rule using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `rule_id`, which is the unique identifier of a forwarding rule.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, view the details of your custom resolver forwarding rule:

    ```sh
    {
      "id": "5365b73c-ce6f-4d6f-ad9f-d9c131b26370",
      "description": "forwarding rule",
      "type": "zone",
      "match": "example.com",
      "forward_to": [
        "161.26.0.7"
      ],
      "created_on": "2021-04-21T08:18:25Z",
      "modified_on": "2021-04-21T08:18:25Z"
    }
    ```
    {: codeblock}

### Viewing a list of all custom resolver forwarding rules using the API
{: #api-cr-fwd-rules-list}

To view the details of a custom resolver forwarding rule using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `rule_id`, which is the unique identifier of a forwarding rule.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, view the list of your custom resolver forwarding rule:

    ```sh
    {
      "forwarding_rules": [
        {
          "id": "5365b73c-ce6f-4d6f-ad9f-d9c131b26370",
          "description": "forwarding rule",
          "type": "zone",
          "match": "example.com",
        "forward_to": [
            "161.26.0.7"
          ],
          "created_on": "2021-04-21T08:18:25Z",
          "modified_on": "2021-04-21T08:18:25Z"
        }
      ]
    }
    ```
    {: codeblock}

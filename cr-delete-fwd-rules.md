---

copyright:
  years: 2021, 2025
lastupdated: "2025-06-03"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Deleting custom resolver forwarding rules
{: #cr-fwd-rules-delete}

You can delete custom resolver forwarding rules in {{site.data.keyword.dns_full}} by using the UI, CLI, or API.
{: shortdesc}

## Deleting custom resolver forwarding rules in the console
{: #ui-cr-fwd-rules-delete}
{: ui}

To delete a forwarding rule in the console, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login) and log in to your account.
1. Select the **Navigation Menu** ![Menu icon](../icons/icon_hamburger.svg), then click **Resource list > Networking > dns-cr-instance**.
1. Navigate to the **Custom resolver** tab.
1. In the Custom resolver table, click the name of the custom resolver that you want to edit.
1. In the Custom resolver details page, select the **Forwarding rules** tab.
1. Click the **Actions** menu ![Actions icon](../icons/action-menu-icon.svg "Actions") next to the rule that you want to delete.
1. Select **Delete**.

  You cannot delete the default rule.
  {: note}

## Deleting custom resolver forwarding rules from the CLI
{: #cli-cr-fwd-rules-delete}
{: cli}

To delete a custom resolver forwarding rule using the CLI, run the following command:

`ibmcloud dns custom-resolver-forwarding-rule-delete RESOLVER_ID RULE_ID [-i, --instance INSTANCE] [-f, --force]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **RULE_ID** is the ID of custom resolver forwarding rule.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used instead.
- **-f, --force** deletes the custom resolver forwarding rule without prompting for confirmation.

## Deleting custom resolver forwarding with using the API
{: #api-cr-fwd-rules-delete}
{: api}

To delete a custom resolver forwarding rule using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `rule_id`, which is the unique identifier of a forwarding rule.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, delete your custom resolver forwarding rule:

    ```curl
    curl -X DELETE https://api.dns-svcs.cloud.ibm.com/v1/instances/2be5d4a7-78f0-4c62-a957-41dc15342777/custom_resolvers/ddbe7a53-7971-46dc-b021-420335c31562/forwarding_rules/80b7d905-b2fd-416f-9e0c-b2e554125a4c -H 'Authorization: Bearer xxxxxx'
    ```
    {: codeblock}

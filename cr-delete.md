---

copyright:
  years: 2021, 2025
lastupdated: "2025-06-03"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Deleting a custom resolver
{: #cr-delete}

You can delete a custom resolver in {{site.data.keyword.dns_full}} by using the UI, CLI, or API.
{: shortdesc}

## Deleting a custom resolver by using the UI
{: #ui-cr-delete}
{: ui}

You can delete your custom resolver with the UI in two ways.

To delete a custom resolver from the custom resolver list view by using the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login) and log in to your account.
1. Select the **Navigation Menu** ![Menu icon](../icons/icon_hamburger.svg), then click **Resource list > Networking > dns-cr-instance**.
1. Navigate to the **Custom resolver** tab.
1. Click the overflow icon next to the custom resolver that you want to delete.
1. Select **Delete**.
1. Click **Delete** in the confirmation dialog that appears.

To delete a custom resolver from the custom resolver details view by using the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login) and log in to your account.
1. Select the **Navigation Menu** ![Menu icon](../icons/icon_hamburger.svg), then click **Resource list > Networking > dns-cr-instance**.
1. Navigate to the **Custom resolver** tab.
1. In the Custom resolver table, click the name of the custom resolver that you want to edit.
1. Select the custom resolver that you want to delete to open the details page.
1. Click **Delete resolver**.
1. Click **Delete** in the confirmation dialog that appears.

Deleting the enabled custom resolver is not permitted. {: note}

## Deleting a custom resolver from the CLI
{: #cli-delete-cr}
{: cli}

To delete a custom resolver using the CLI, run the following command:

`ibmcloud dns custom-resolver-delete RESOLVER_ID [-i, --instance INSTANCE] [-f, --force]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used instead.
- **--output** specifies output format. Currently, `json` is the only supported format.
- **-f, --force** deletes the custom resolver without prompting for confirmation.

## Deleting a custom resolver with the API
{: #api-delete-cr}
{: api}

To delete a custom resolver using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, update your custom resolver.

    ```sh
    curl -X DELETE https://api.dns-svcs.cloud.ibm.com/v1/instances/2be5d4a7-78f0-4c62-a957-41dc15342777/custom_resolvers/ddbe7a53-7971-46dc-b021-420335c31562 -H 'Authorization: Bearer xxxxxx'
    ```
    {: codeblock}

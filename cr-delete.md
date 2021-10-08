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

# Deleting a custom resolver
{: #cr-delete}

This custom resolver feature is available to {{site.data.keyword.dns_short}} users with a Standard plan.
{: beta}

You can delete a custom resolver in {{site.data.keyword.dns_full}} by using the UI, CLI, or API.
{: shortdesc}

## Deleting a custom resolver using the UI
{: #ui-cr-delete}
{: ui}

You can delete your custom resolver with the UI in two ways.

To delete a custom resolver from the custom resolver list view:
1. Click the overflow icon next to the custom resolver you want to delete.
1. Select **Delete**.
1. Click **Delete** in the confirmation dialog that appears.

To delete a custom resolver from the custom resolver details view:
1. Select the custom resolver you want to delete to open the details page.
1. Click **Delete resolver**.
1. Click **Delete** in the confirmation dialog that appears.

## Deleting a custom resolver using the CLI
{: #cli-delete-cr}
{: cli}

To delete a custom resolver using the CLI, run the following command:

`ibmcloud dns custom-resolver-delete RESOLVER_ID [-i, --instance INSTANCE] [-f, --force]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used insteaad.
- **--output** specifies output format. Currently, JSON is the only supported format.
- **-f, --force** deletes the custom resolver without prompting for confirmation.

## Deleting a custom resolver using the API
{: #api-delete-cr}
{: api}

To delete a custom resolver using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, update your custom resolver.

    ```
    curl -X DELETE https://api.dns-svcs.cloud.ibm.com/v1/instances/2be5d4a7-78f0-4c62-a957-41dc15342777/custom_resolvers/ddbe7a53-7971-46dc-b021-420335c31562 -H 'Authorization: Bearer xxxxxx'
    ```
    {: codeblock}

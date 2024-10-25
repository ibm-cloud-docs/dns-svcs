---

copyright:
  years: 2021, 2024
lastupdated: "2024-10-25"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Updating a custom resolver
{: #update-cr}

You can update custom resolvers in {{site.data.keyword.dns_full}} by using the UI, CLI, or API.
{: shortdesc}

## Updating a custom resolver in the UI
{: #ui-update-cr}
{: ui}

The custom resolver details view shows the name and status of a custom resolver. It also lists the custom resolver ID, the linked VPC name, the date the resolver was modified, the description, and the enabled toggle that was entered when it was created.

To edit the name and description of the custom resolver, click **Edit** next to the pencil icon to open the edit view. Click **Save** to commit the changes, or cancel.

Toggle the **Enablement** switch to enable or disable the custom resolver.

## Update a custom resolver from the CLI
{: #cli-update-cr}
{: cli}

To update a custom resolver using the CLI, run the following command:

`ibmcloud dns custom-resolver-update RESOLVER_ID [--name NAME] [--enabled true|false] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **-n, --name** is the name of the custom resolver.
- **-d, --description** is the descriptive text of the custom resolver.
- **--enabled** determines whether to enable the custom resolver.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used instead.
- **--output** specifies output format. Currently, JSON is the only supported format.

## Update a custom resolver with the API
{: #api-update-cr}
{: api}

To update a custom resolver using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, update your custom resolver:

    ```sh
    {
      "name": "my-resolver",
      "description": "custom resolver",
      "enabled": false
    }
    ```
    {: codeblock}


## Next steps
{: #next-steps-update-cr}

* [Adding custom resolver locations](/docs/dns-svcs?topic=dns-svcs-cr-res-loc-add)
* [Adding custom resolver forwarding rules](/docs/dns-svcs?topic=dns-svcs-cr-fwd-rules-add)
* [Deleting a custom resolver](/docs/dns-svcs?topic=dns-svcs-cr-delete)

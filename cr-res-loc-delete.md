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

# Deleting custom resolver locations
{: #cr-res-loc-delete}

This custom resolver feature is available to {{site.data.keyword.dns_short}} users with a Standard plan. 
{: beta}

You can delete custom resolver locations in {{site.data.keyword.dns_full}} by using the UI, CLI, or API. 
{: shortdesc}

## Deleting a resolver location using the UI
{: #ui-delete-res-loc}
{: ui}

To delete a resolver location by using the UI, take the following steps:
1. Select a custom resolver to open the details page.
1. Click the overflow menu icon.
1. Select **Delete**.


## Deleting a resolver location
{: #cli-delete-res-loc}
{: cli}

To delete a resolver location using the CLI, run the following command:

`ibmcloud dns custom-resolver-location-delete RESOLVER_ID LOCATION_ID [-i, --instance INSTANCE] [-f, --force]`

Where:

 - **RESOLVER_ID** is the ID of custom resolver.
 - **LOCATION_ID** is the ID of the custom resolver location.
 - **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by dns instance-target INSTANCE is used instead.
 - **-f, --force** deletes the resolver location without prompting for confirmation.


## Deleting a resolver location using the API
{: #api-delete-res-loc}
{: api}

To delete a custom resolver location using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
   * `instance_id`, which is the unique identifier of a service instance.
   * `resolver_id`, which is the unique identifier of a custom resolver.
   * `location_id`, which is the custom resolver location ID.
   * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all viariables are initiated, get the details of your custom resolver:

   ```
   curl -X DELETE https://api.dns-svcs.cloud.ibm.com/v1/instances/2be5d4a7-78f0-4c62-a957-41dc15342777/custom_resolvers/ddbe7a53-7971-46dc-b021-420335c31562/locations/bf6b4f83-bf0b-47c2-8bdf-e7fbd92db2c6 -H 'Authorization: Bearer xxxxxx'
   ```
   {:codeblock}
   

---

copyright:
  years: 2021, 2025
lastupdated: "2025-06-03"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Deleting custom resolver locations
{: #cr-res-loc-delete}

You can delete custom resolver locations in {{site.data.keyword.dns_full}} by using the UI, CLI, or API.
{: shortdesc}

## Deleting a resolver location by using the UI
{: #ui-delete-res-loc}
{: ui}

To delete a resolver location by using the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login) and log in to your account.
1. Select the **Navigation Menu** ![Menu icon](../icons/icon_hamburger.svg), then click **Resource list > Networking > dns-cr-instance**. 
1. Navigate to the **Custom resolver** tab.
1. Click the **Actions** menu ![Actions icon](../icons/action-menu-icon.svg "Actions") icon for the location that you want to delete. 
1. Select **Delete**.

Deleting an enabled location is not permitted. 
{: note}

## Deleting a resolver location from the CLI
{: #cli-delete-res-loc}
{: cli}

To delete a resolver location using the CLI, run the following command:

`ibmcloud dns custom-resolver-location-delete RESOLVER_ID LOCATION_ID [-i, --instance INSTANCE] [-f, --force]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **LOCATION_ID** is the ID of the custom resolver location.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used instead.
- **-f, --force** deletes the resolver location without prompting for confirmation.

## Deleting a resolver location with the API
{: #api-delete-res-loc}
{: api}

To delete a custom resolver location using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `location_id`, which is the custom resolver location ID.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, get the details of your custom resolver:

    ```sh
    curl -X DELETE https://api.dns-svcs.cloud.ibm.com/v1/instances/2be5d4a7-78f0-4c62-a957-41dc15342777/custom_resolvers/ddbe7a53-7971-46dc-b021-420335c31562/locations/ bf6b4f83-bf0b-47c2-8bdf-e7fbd92db2c6 -H 'Authorization: Bearer xxxxxx'
    ```
    {: codeblock}

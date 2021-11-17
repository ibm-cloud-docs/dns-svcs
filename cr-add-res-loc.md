---

copyright:
  years: 2021
lastupdated: "2021-11-17"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Adding custom resolver locations
{: #cr-res-loc-add}

The task of the resolver location instance is to provide DNS resolver functions based on the forwarding rules that you configure. Add resolver locations to manage where your custom resolver deploys. 
{: shortdesc}

## Adding a resolver location using the UI
{: #ui-add-res-loc}
{: ui}

To add a custom resolver location, from the custom resolver details page:
1. Fronm the Resolver locations tab, click **Add location**.
1. Select the subnet from the list menu in the row that appears.

   Each custom resolver can have a maximum of three locations within the same subnet, or in different subnets. Also, to achieve high availability, you must configure custom resolvers with a minimum of two resolver locations.
    {: important}

The location is added when the subnet selection is made.

## Adding a resolver location using the CLI
{: #cli-add-res-loc}
{: cli}

To add a resolver location using the CLI, run the following command:

`ibmcloud dns custom-resolver-location-add RESOLVER_ID --subnet SUBNET_CRN [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **--subnet** is the CRN of the subnet.
- **--enabled** determines whether to enable the resolver location.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used instead.
- **--output** specifies output format. Currently, JSON is the only supported format.

## Adding a resolver location using the API
{: #api-add-res-loc}
{: api}

To add a custom resolver location using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, get the details of your custom resolver:

    ```sh
    {
      "subnet_crn": "crn:v1:bluemix:public:is:us-south-1:a/01652b251c3ae2787110a995d8db0135::subnet:0716-b49ef064-0f89-4fb1-8212-135b12568f04",
      "enabled": false
    }
    ```
    {: codeblock}
  

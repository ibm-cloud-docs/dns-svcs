---

copyright:
  years: 2021, 2025
lastupdated: "2025-06-03"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Adding custom resolver locations
{: #cr-res-loc-add}

The task of the resolver location instance is to provide DNS resolver functions based on the forwarding rules that you configure. Add resolver locations to manage where your custom resolver deploys by using the UI, CLI, or API.
{: shortdesc}

## Custom resolver address propagation
{: #custom-resolver-address-propagation}

Custom resolver addresses are propagated to the virtual server instance on the VPC.

### Zone affinity settings
{: #zone-affinity-settings}

The order of IPs of a custom-resolver location is set with zone affinity. For example, say a custom resolver has the following locations.
* `us-south-1`: IP1
* `us-south-2`: IP2
* `us-south-3`: IP3

The DNS servers will appear similar to this example.
* Virtual server instance in `us-south-1`: IP1 IP2 IP3
* Virtual server instance in `us-south-2`: IP2 IP3 IP1
* Virtual server instance in `us-south-3`: IP3 IP1 IP2

## Adding a resolver location in the console
{: #ui-add-res-loc}
{: ui}

To add a custom resolver location by using the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login) and log in to your account.
1. Select the **Navigation Menu** ![Menu icon](../icons/icon_hamburger.svg), then click **Resource list > Networking > dns-cr-instance**.
1. Navigate to the **Custom resolver** tab.
1. In the Custom resolver table, click the name of the custom resolver that you want to edit.
1. In the Custom resolver details page, click the Resolver locations tab.
1. From the Resolver locations tab, click **Add location**.
1. Select the subnet from the list menu in the row that appears.

   Each custom resolver can have a maximum of three locations within the same subnet, or in different subnets. Also, to achieve high availability, you must configure custom resolvers with a minimum of two resolver locations.
    {: important}

The location is added when the subnet selection is made.

## Adding a resolver location from the CLI
{: #cli-add-res-loc}
{: cli}

To add a resolver location using the CLI, run the following command:

`ibmcloud dns custom-resolver-location-add RESOLVER_ID --subnet SUBNET_CRN [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **--subnet** is the CRN of the subnet.
- **--enabled** determines whether to enable the resolver location.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used instead.
- **--output** specifies output format. Currently, `json` is the only supported format.

## Adding a resolver location with the API
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

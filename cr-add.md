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

# Configuring a custom resolver
{: #ui-create-cr}



This custom resolver feature is available to {{site.data.keyword.dns_short}} users with a Standard plan.
{: beta}

You can add a custom resolver in {{site.data.keyword.dns_full}} by using the UI, CLI, or API.
{: shortdesc}

## Creating a custom resolver using the UI
{: #create-cr}
{: ui}

To add a custom resolver in {{site.data.keyword.dns_short}}, take the following steps:

1. Navigate to **Custom resolvers** in the {{site.data.keyword.dns_short}} navigation menu.
1. Click **Create custom resolver**.
1. Enter a name and description for your custom resolver.
1. Select a region from the list menu.
1. Select a VPC from the list menu.
1. Select a subnet from the list menu.
1. Click **Add+** if you want to add another subnet.

    Each VPC can have only one custom resolver.
    {: note}

1. Click **Create**.

The custom resolver details view appears, where you can manage the custom resolver. 

## Create a custom resolver using the CLI
{: #cli-create-cr}
{: cli}

To create a custom resolver using the CLI, run the following command:

`ibmcloud dns custom-resolver-create --name NAME --location LOCATION1 --location LOCATION2 [-description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **-n, --name** is the name of the custom resolver.
- **-d, --description** is the descriptive text of the custom resolver.
- **--location** is the location where the custom resolver is running. The location subnet CRN is required. For example: `--location subnet1,enable  --location subnet2,disable`
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used instead.
- **--output** specifies output format. Currently, JSON is the only supported format.

## Create a custom resolver using the API
{: #api-create-cr}
{: api}

To add a custom resolver using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all viariables are initiated, add your custom resolver:

```
{
  "name": "my-resolver",
  "description": "custom resolver",
  "locations": [
    {
      "subnet_crn": "crn:v1:bluemix:public:is:us-south-1:a/01652b251c3ae2787110a995d8db0135::subnet:0716-b49ef064-0f89-4fb1-8212-135b12568f04",
      "enabled": false
    }
  ]
}
```
{: codeblock}


## Next steps
{: #next-steps-create-cr}

* [Adding custom resolver locations](/docs/dns-svcs?topic=dns-svcs-cr-res-loc-add)
* [Setting up custom resolver forwarding rules](/docs/dns-svcs?topic=dns-svcs-cr-fwd-rules-add)
* [Deleting a custom resolver](/docs/dns-svcs?topic=dns-svcs-cr-delete)


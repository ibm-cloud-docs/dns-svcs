---

copyright:
  years: 2021
lastupdated: "2021-11-17"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Viewing custom resolver details
{: #details-cr}

You view details of a single custom resolver and view a list of all custom resolvers in {{site.data.keyword.dns_full}} by using the UI, CLI, or API.
{: shortdesc}

## Viewing custom resolver details using the UI
{: #ui-details-cr}
{: ui}

To view the details of a custom resolver using the UI, navigate to the custom resolver tab in the DNS Services instance. From the custom resolver view, you can view a list of all custom resolvers. There, you can view information about a specific custom resolver by clicking the custom resolver name.

## Get details of a custom resolver using the CLI
{: #cli-get-cr}
{: cli}

To get the details of a custom resolver using the CLI, run the following command:

`ibmcloud dns custom-resolver RESOLVER_ID [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **RESOLVER_ID** is the ID of custom resolver.
- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used instead.
- **--output** specifies output format. Currently, JSON is the only supported format.

### List all custom resolvers
{: #cli-list-cr}

To list all custom resolvers using the CLI, run the following command:

`ibmcloud dns custom-resolvers [-i, --instance INSTANCE] [--output FORMAT]`

Where:

- **-i, --instance** is the instance name or ID. If this is not set, the context instance specified by `dns instance-target INSTANCE` is used instead.
- **--output** specifies output format. Currently, JSON is the only supported format.

## Get details of a custom resolver using the API
{: #api-details-cr}
{: api}

### Get details of a single custom resolver
{: #api-details}

To get the details of a custom resolver using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `resolver_id`, which is the unique identifier of a custom resolver.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, get the details of your custom resolver:

    ```sh
    {
      "id": "5365b73c-ce6f-4d6f-ad9f-d9c131b26370",
      "name": "my-resolver",
      "description": "custom resolver",
      "enabled": false,
      "health": "HEALTHY",
      "locations": [
        {
          "id": "9a234ede-c2b6-4c39-bc27-d39ec139ecdb",
          "subnet_crn": "crn:v1:bluemix:public:is:us-south-1:a/01652b251c3ae2787110a995d8db0135::subnet:0716-b49ef064-0f89-4fb1-8212-135b12568f04",
          "enabled": true,
          "healthy": true,
          "dns_server_ip": "10.10.16.8"
        }
      ],
      "created_on": "2021-04-21T08:18:25Z",
      "modified_on": "2021-04-21T08:18:25Z"
    }
    ```
    {: codeblock}

### List all custom resolvers
{: #api-cr-list-all}

To list all custom resolvers using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `instance_id`, which is the unique identifier of a service instance.
    * `X-Correlation-ID`, which is a string that uniquely identifies a request.
1. When all variables are initiated, list your custom resolvers:

    ```sh
    {
      "custom_resolvers": [
        {
          "id": "5365b73c-ce6f-4d6f-ad9f-d9c131b26370",
          "name": "my-resolver",
          "description": "custom resolver",
          "enabled": false,
          "health": "HEALTHY",
          "locations": [
            {
              "id": "9a234ede-c2b6-4c39-bc27-d39ec139ecdb",
              "subnet_crn": "crn:v1:bluemix:public:is:us-south-1:a/01652b251c3ae2787110a995d8db0135::subnet:0716-b49ef064-0f89-4fb1-8212-135b12568f04",
              "enabled": true,
              "healthy": true,
             "dns_server_ip": "10.10.16.8"
            }
          ],
          "created_on": "2021-04-21T08:18:25Z",
          "modified_on": "2021-04-21T08:18:25Z"
        }
      ]
    }
    ```
    {: codeblock}

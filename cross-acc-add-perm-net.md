---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-25"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Adding a permitted network to a linked zone
{: #add-permit-network-linked}

Add a permitted network to your linked zone by using the UI, CLI, or API.
{: shortdesc}

## Adding a permitted network in the UI
{: #ui-add-permit-network}
{: ui}

To add a permitted network using the UI, take the following steps:

1. Navigate to the **Zones** section of your {{site.data.keyword.dns_short}} instance, then select the **Linked zones** tab.
1. Click the link in the **Zone name** column of the linked zone to which you want to add a permitted network. The **Add networks** panel appears.
1. Select a region.
1. Select a network.
1. Click **Add** to add the permitted network.

The **Status** column shows that the linked zone is "Active" after a permitted network is successfully added.


## Adding a permitted network from the CLI
{: #cli-add-permit-network}
{: cli}

To add a permitted network to your linked zone using the CLI, run the following command:

```sh
ibmcloud dns cross-account linked-zone-permitted-network-add LINKED_ZONE_ID --vpc-crn VPC_CRN [--type TYPE] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **LINKED_ZONE_ID** is the ID of the linked zone.
* **--type value** is the permitted network type. Valid values: vpc.
* **--vpc-crn value** is the CRN of VPC instance.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by `ibmcloud dns instance-target INSTANCE` is used.
* **--output value** specifies the output format. Currently, `json` is the only supported format.

## Adding a permitted network with the API
{: #api-add-permit-network}
{: api}

To add a permitted network to your linked zone using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `INSTANCE_ID`, which is the unique identifier of a service instance.
    * `LINKED_DNSZONE_ID` which is the unique identifier of a linked zone.
    * `IAM_TOKEN`, which is the IAM authorization token.
1. When all variables are initiated, add the permitted network:

    ```sh
    curl -X POST \
        https://api.dns-svcs.cloud.ibm.com/v1/instances/$INSTANCE_ID/linked_dnszones/$LINKED_DNSZONE_ID/permitted_networks \
        -H "Authorization: $IAM_TOKEN" \
        -H "Content-Type: application/json" \
        -d '{
                "permitted_network": {
                     "vpc_crn": "crn:v1:bluemix:public:is:us-south:a/a8c46c094344a98ec1d8ef6ea19da410::vpc:r134-02681b2e-3c65-42c0-8ce4-b31da3fafcb7"
                },
                "type": "vpc"
         }
    ```
    {: codeblock}

The following response is an example of when a permitted network is added successfully.

```sh
{
  "id": "fecd0173-3919-456b-b202-3029dfa1b0f7",
  "created_on": "2019-01-01T05:20:00.12345Z",
  "modified_on": "2019-01-01T05:20:00.12345Z",
  "permitted_network": {
    "vpc_crn": "crn:v1:bluemix:public:is:us-south:a/a8c46c094344a98ec1d8ef6ea19da410::vpc:r134-02681b2e-3c65-42c0-8ce4-b31da3fafcb"
  },
  "type": "vpc",
  "state": "ACTIVE"
}
```
{: screen}

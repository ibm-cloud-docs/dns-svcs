---

copyright:
  years: 2021, 2024
lastupdated: "2024-10-25"

keywords: vpe for dns services, virtual private endpoints for dns services, using vpe for vpc with dns services, isolation for dns services, private network for dns services, network isolation in dns services, non-public routes for dns services, private connection for dns services, private connectivity for dns services

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}


# Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.dns_short}}
{: #vpe-connection}

{{site.data.keyword.cloud}} Virtual Private Endpoints (VPE) for VPC enables you to connect to {{site.data.keyword.dns_short}} from your VPC network by using the IP addresses of your choosing, allocated from a subnet within your VPC.
{: shortdesc}

VPEs are virtual IP interfaces that are bound to an endpoint gateway created on a per service, or service instance, basis (depending on the service operation model). The endpoint gateway is a virtualized function that scales horizontally, is redundant and highly available, and spans all availability zones of your VPC. Endpoint gateways enable communications from virtual server instances within your VPC and {{site.data.keyword.cloud}} service on the private backbone. VPE for VPC gives you the experience of controlling all the private addressing within your cloud. For more information, see [About virtual private endpoint gateways](/docs/vpc?topic=vpc-about-vpe).

## Before you begin
{: #prereq-service-endpoint}

Before you target a virtual private endpoint for {{site.data.keyword.dns_short}} you must complete the following tasks.

* Ensure that a [Virtual Private Cloud is created](/docs/vpc?topic=vpc-getting-started).
* Make a plan for your [virtual private endpoints](/docs/vpc?topic=vpc-planning-considerations).
* Ensure that [correct access controls](/docs/vpc?topic=vpc-configure-acls-sgs-endpoint-gateways&interface=ui#vpe-configuring-acls) are set for your virtual private endpoint.
* Understand the [limitations](/docs/vpc?topic=vpc-limitations-vpe) of having a virtual private endpoint.
* Understand how to [view details](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway) about a virtual private endpoint.

## Setting up a VPE for {{site.data.keyword.dns_short}}
{: #endpoint-setup}

When you create a VPE gateway by using the CLI or API, use the following CRN information.

| Location | Region | Cloud Resource Name (CRN) |
|---------|-------|----------------|
| Global | `global` | `crn:v1:bluemix:public:dns-svcs:global::::` |
{: caption="Region availability and Cloud Resource Names (CRNs) for connecting {{site.data.keyword.dns_short}} over {{site.data.keyword.cloud_notm}} private networks" caption-side="bottom"}

### Configuring an endpoint gateway
{: #endpoint-gateway-dns-svcs}

To configure a virtual private endpoint gateway, follow these steps:

1. List the available services, including {{site.data.keyword.cloud_notm}} infrastructure services available (by default) for all VPC users.
1. [Create an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway) for {{site.data.keyword.dns_short}} that you want to be privately available to the VPC.
1. [Bind a reserved IP address](/docs/vpc?topic=vpc-bind-unbind-reserved-ip) to the endpoint gateway.
1. View the created VPE gateways associated with the {{site.data.keyword.dns_short}} instance. For more information, see [Viewing details of an endpoint gateway](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway).

Now your virtual server instances in the VPC can access your {{site.data.keyword.dns_short}} instance privately through it.

## Using your VPE for {{site.data.keyword.dns_short}}
{: #using-dns-svcs-vpe}

After you create an endpoint gateway for {{site.data.keyword.dns_short}}, follow these steps:

### Using the VPE from the CLI
{: #vpe-cli}
{: cli}

Use the following steps to update to the latest version of the CLI and the {{site.data.keyword.dns_short}} plug-in.

1. Update the {{site.data.keyword.cloud_notm}} CLI to the latest version:

   ```sh
   ibmcloud update
   ```
   {: pre}

1. Update the {{site.data.keyword.dns_short}} CLI plug-in:

   ```sh
   ibmcloud plugin update cloud-dns-services
   ```
   {: pre}

1. Log into `private.cloud.ibm.com`. For more information about logging into the private cloud, see [Securing your connection when using the IBM Cloud CLI](/docs/cli?topic=cli-service-connection).

### Using the VPE with the VPC API
{: #vpe-api}
{: api}

After creating an endpoint gateway for the {{site.data.keyword.dns_short}} service, use the service endpoints FQDN `api.private.dns-svcs.cloud.ibm.com` in the URL to access the service. For example:

```sh
curl https://api.private.dns-svcs.cloud.ibm.com/v1/dns-svcs?version='2020-03-31' -H "Authorization: Bearer $iam_token"
```
{: pre}

### Using the VPE with the SDK
{: #vpe-sdk}
{: api}

After creating an endpoint gateway for {{site.data.keyword.dns_short}}, you must use the private endpoint's FQDN when setting the service's FQDN during construction of the {{site.data.keyword.dns_short}} gateway service object.

```sh
api.private.dns-svcs.cloud.ibm.com
```
{: pre}

For examples of setting the service's FQDN for the specific SDK language, see [SDK API examples](/apidocs/dns-svcs?code=go#authentication).

### Using the VPE with Terraform
{: #vpe-terraform}
{: terraform}

If you plan to access the {{site.data.keyword.dns_short}} service using Terraform, make sure to set the `IBMCLOUD_PRIVATE_DNS_API_ENDPOINT` environment variable to `api.private.dns-svcs.cloud.ibm.com`. For example:

```sh
export IBMCLOUD_PRIVATE_DNS_API_ENDPOINT=api.private.dns-svcs.cloud.ibm.com
```
{: pre}

For more information, see [DNS Services resources and data sources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-resources-datasource-list#ibm-dns-service_rd).

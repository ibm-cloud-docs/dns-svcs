---

copyright:
  years: 2021, 2024
lastupdated: "2024-10-25"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Integrating with Virtual Private Endpoint for VPC
{: #vpe-for-dns-svcs}

You can integrate with Virtual Private Endpoint for VPC by using the CLI, API, SDK, or Terraform.
{: shortdesc}

{{site.data.keyword.cloud}} Virtual Private Endpoint (VPE) for VPC enables you to connect to supported {{site.data.keyword.cloud_notm}} services from your VPC network by using IP addresses of your choosing, allocated from a subnet within your VPC. A {{site.data.keyword.dns_short}} VPE allows you to communicate with the control plane of {{site.data.keyword.dns_short}}.

## Setting up a VPE gateway for the {{site.data.keyword.dns_short}} service
{: #vpe-setup}

Follow instructions in [Getting started](/docs/vpc?topic=vpc-about-vpe#vpe-getting-started) for VPE for VPC to create and configure a VPE gateway for the {{site.data.keyword.dns_short}} service offering.

### Integrating with Virtual Private Endpoint for VPC from the CLI
{: #cli-dns-svcs}
{: cli}

After creating an endpoint gateway for {{site.data.keyword.dns_short}}, follow these steps:

1. Update the {{site.data.keyword.cloud_notm}} CLI to the latest version:

    ```sh
    ibmcloud update
    ```
    {: pre}

1. Update the {{site.data.keyword.dns_short}} CLI plug-in:

    ```sh
    ibmcloud plugin update dns-svcs-cli
    ```
    {: pre}

1. Log in to the CLI [using a private endpoint](/docs/cli?topic=cli-service-connection#cli-private-login).

For more information on VPEs using the CLI, see [Virtual private endpoint gateways](/docs/vpc?topic=vpc-vpc-reference&interface=cli#vpe-clis).

### Integrating with Virtual Private Endpoint for VPC with the API
{: #vpe-setup-api}
{: api}

After creating an endpoint gateway for the {{site.data.keyword.dns_short}} instance, use the service endpoint's FQDN `api.private.dns-svcs.cloud.ibm.com` in the URL to access the service. For example:

```sh
curl https://api.private.dns-svcs.cloud.ibm.com/instance/<instance-id>/dnszones -H "Authorization: Bearer $iam_token"
```
{: pre}

### Integrating with Virtual Private Endpoint for VPC with the SDK
{: #sdk-dns-svcs}
{: api}

After creating an endpoint gateway for the {{site.data.keyword.dns_short}} service, you must use the private endpoint's FQDN when setting the service's FQDN during construction of the {{site.data.keyword.dns_short}} service object. For example:

```sh
api.private.dns-svcs.cloud.ibm.com
```
{: pre}

For more examples of setting the service's FQDN for the specific SDK language, see [SDK API examples](/apidocs/dns-svcs?code=go).

### Integrating with Virtual Private Endpoint for VPC with Terraform
{: #terraform-dns-svcs}
{: terraform}

If you plan to access the {{site.data.keyword.dns_short}} service using Terraform, make sure to set the `IBMCLOUD_PRIVATE_DNS_API_ENDPOINT` environment variable to `https://api.private.dns-svcs.cloud.ibm.com/v1`. For example:

```sh
export IBMCLOUD_PRIVATE_DNS_API_ENDPOINT=https://api.private.dns-svcs.cloud.ibm.com/v1
```
{: pre}

For more information on using Terraform, see [{{site.data.keyword.dns_short}} resources and data sources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-resources-datasource-list#ibm-dns-service_rd).

For more information on using VPEs in Terraform, see [`ibm_is_virtual_endpoint_gateway_ip`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_virtual_endpoint_gateway_ip){: external}.

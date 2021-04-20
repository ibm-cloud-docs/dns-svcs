---

copyright:
  years: 2021
lastupdated: "2021-03-09"

keywords:

subcollection: dns-svcs

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}
{:external: target="_blank" .external}
{:support: data-reuse='support'}
{:help: data-hd-content-type='help'}

# Integrating with Virtual Private Endpoint for VPC
{: #vpe-for-dns-svcs}

{{site.data.keyword.cloud}} Virtual Private Endpoint (VPE) for VPC enables you to connect to supported {{site.data.keyword.cloud_notm}} services from your VPC network by using IP addresses of your choosing, allocated from a subnet within your VPC.


## Setting up a VPE gateway for the {{site.data.keyword.dns_short}} service
{: #vpe-setup}

Follow instructions in [Getting started](/docs/vpc?topic=vpc-about-vpe#vpe-getting-started) for VPE for VPC to create and confirgue a VPE gateway for the {{site.data.keyword.dns_short}} service offering.

### Using the CLI
{: #cli-dns-svcs}

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

### Using the API 
{: #vpe-setup-api}
 
After creating an endpoint gateway for the {{site.data.keyword.dns_short}} instance, use the service endpoint's FQDN `api.private.dns-svcs.cloud.ibm.com` in the URL to access the service. For example:

```sh
curl https://api.private.dns-svcs.cloud.ibm.com/instance/<instance-id>/dnszones -H "Authorization: Bearer $iam_token"
```
{: pre}

### Using the SDK
{: #sdk-dns-svcs}

After creating an endpoint gateway for the {{site.data.keyword.dns_short}} service, you must use the private endpoint's FQDN when setting the service's FQDN during construction of the {{site.data.keyword.dns_short}} service object. For example:

```
api.private.dns-svcs.cloud.ibm.com
``` 
{:pre}

For more examples of setting the service's FQDN for the specific SDK language, see [SDK API examples](/apidocs/dns-svcs?code=go).  

### Using Terraform
{: #terrform-dns-svcs}

If you plan to access the {{site.data.keyword.dns_short}} service using Terraform, make sure to set the `IBMCLOUD_PRIVATE_DNS_API_ENDPOINT` environment variable to `https://api.private.dns-svcs.cloud.ibm.com/v1`. For example:

```sh
export IBMCLOUD_PRIVATE_DNS_API_ENDPOINT=https://api.private.dns-svcs.cloud.ibm.com/v1
```
{: pre}

For more information, see [{{site.data.keyword.dns_short}} resources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-dns-resources) and [{{site.data.keyword.dns_short}} data sources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-dns-data-sources).


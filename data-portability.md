---

copyright:
  years: 2024
lastupdated: "2025-04-16"

keywords: DNS Services

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Understanding data portability for DNS Services
{: #data-portability}

[Data Portability](#x2113280){: term} involves a set of tools and procedures that enable customers to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes procedures for copying and storing the service customer content, including the related configuration that is used by the service to store and process the data, on the customer's own location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.cloud_notm}} services provide interfaces and instructions to guide the customer to copy and store the service customer content, including the related configuration, on their own selected location.

The customer is responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

- The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.
- The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of customer's application code, deployment automation, and so on.
- The conversion of the exported data and configuration to the format that's required by the alternative infrastructure and adapted applications.

For more information about your responsibilities for DNS Services, see [Understanding your responsibilities when using DNS Services](/docs/dns-svcs?topic=dns-svcs-responsibilities-dns-svcs).

## Data export procedures
{: #data-portability-procedures}

DNS Services provides the mechanisms to export your content that's uploaded, stored, and processed when you use the service.

In addition, DNS Services provides mechanisms to export settings and configurations that are used to process the customer's content. For more information, see [Exporting your DNS Services configuration](/docs/dns-svcs?topic=dns-svcs-writing-dns-svcs-config-to-file).

## Exported data formats
{: #data-portability-data-formats}

DNS Services supports the following data format and schema of the exported data, configuration, and application:

* Export in JSON format only

   Example command using the [DNS Services CLI](/docs/dns-svcs?topic=dns-svcs-dns-services-cli-commands):

   ```sh
   ibmcloud dns zone ZONE_ID [-i, --instance INSTANCE] [--output json]
   ```

  Example request using the [DNS Services API](/apidocs/dns-svcs#introduction-to-dns-services-api):

   ```curl
   curl -X GET   https://api.dns-svcs.cloud.ibm.com/v1/instances/1407a753-a93f-4bb0-9784-bcfc269ee1b3/dnszones/2d0f862b-67cc-41f3-b6a2-59860d0aa90e \
   -H 'Content-Type: application/json' \
   -H 'Authorization: Bearer xxxxxx'
   ```

DNS Services doesn't support the export of other data formats and other schema of the exported data, configuration, and application, including the following:
* Exporting [zone files](https://en.wikipedia.org/wiki/Zone_file){: external}

## Data ownership
{: #data-portability-ownership}

All exported data is classified as customer content. Apply the full customer ownership and licensing rights, as stated in the [IBM Cloud Service Agreement](https://www.ibm.com/support/customer/csol/terms/?id=Z126-6304_WS&cc=in&lc=en){: external}.

---

copyright:
  years: 2020
lastupdated: "2020-11-16"

keywords:

subcollection: dns-svcs

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:support: data-reuse='support'}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}
{:troubleshoot: data-hd-content-type='troubleshoot'}


# Why is my origin status down?
{: #troubleshoot-origin-down}
{: troubleshoot}
{: support}

You checked the status of your origin, and it's down.
{:shortdesc}

Your origin status is `down`. It might be for one or more of the following reasons.
{: tsSymptoms}

## Initial health check might not be complete
{:#init-healthcheck-complete}

Your origin might be down because the initial health check has not finished yet. 

Wait for the health check interval to pass before checking again.
{: tsResolve}

## Security groups might not have been added yet
{:#no-security-group}

Your origin might be down because the security group rules have not been added yet.

Be sure the [security group rules](/docs/dns-svcs?topic=dns-svcs-global-load-balancers#security-groups-glb) have been added.
{: tsResolve}

## Application error
{:#application-error}

Your origin might be down because the application responsible for responding to the health check queries might not be running properly or on the correct port.

Verify that the application is running on the correct port, and is operating properly.
{: tsResolve}

## Incorrect type selected for health check type
{:#wrong-type}

Your origin might be down because you specified HTTPS as your type of health check. 

Make sure that a valid certificate exists on the origin. For a self-signed certificate, you can use the **Don't validate certificate** option for the health check.
{: tsResolve}

## Host header is not set
{:#host-header}

Your origin might be down because you specified an IP address for the origin and did not set the host header on the health check.

Set the host header. For more information, see [Creating a health check](/docs/dns-svcs?topic=dns-svcs-global-load-balancers#add-a-health-check).
{: tsResolve}

## Network interface limit
{:#network-interface-limit}

Your origin might be down because your subnet might have reached the limit for the number of network interfaces allowed. 

Try again with a subnet that has available space, or remove interfaces from the current subnet to give space for the health check virtual server instance.
{: tsResolve}

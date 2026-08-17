---

copyright:
  years: 2019, 2026
lastupdated: "2026-08-17"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Getting help and support for {{site.data.keyword.dns_short}}
{: #gettinghelp}

If you experience an issue or have questions when using {{site.data.keyword.dns_full}}, you can use the following resources before you open a support case.
{: shortdesc}

* Ask a question in the [AI assistant](/docs/overview?topic=overview-ask-ai-assistant) from the console or the {{site.data.keyword.cloud_notm}} CLI.
* Review [FAQs](/docs/dns-svcs?topic=dns-svcs-frequently-asked-questions) in the product documentation.
* Review [Troubleshooting](/docs/dns-svcs?topic=dns-svcs-troubleshoot-nxdomain) to diagnose and resolve common issues.
* Check the status of the {{site.data.keyword.cloud_notm}} platform and resources by going to the [Status page](/status){: external}.

If you still can't resolve the problem, you can open a support case. For more information, see [Creating support cases](/docs/support?topic=support-open-case&interface=ui). And, if you're looking to provide feedback, see [Submitting feedback](/docs/overview?topic=overview-feedback).

## Providing support case details for {{site.data.keyword.dns_short}}
{: #support-case-details}

To ensure that the support team has all of the details for investigating your issue to provide a timely resolution, you must provide detailed information about your issue. Review the following tips about the type of information to include in your support case for issues with {{site.data.keyword.dns_short}}.

Provide the following details:

1. The specific IDs of affected VPCs.
1. The IDs of the {{site.data.keyword.dns_short}} private resource records (if any).
1. The IDs of zones that have affected private resource records (if any).
1. The DNS queries made. If possible, give the details on DNS queries related to the issue, including DNS message ID and timestamp for each.
1. Information about the source of the DNS query (for example, the ID of the VPC from which the query originated).
1. If it affects a custom resolver, then include the custom resolver ID.
1. If it affects a GLB health check, then include the GLB health check ID and the IDs of affected GLBs.
1. If it is an issue with a forwarding rule, then include the forwarding rule ID.
1. If it is an issue with a secondary zone, then include the secondary zone rule ID.

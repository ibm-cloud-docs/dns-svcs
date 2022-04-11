---

copyright:
  years: 2022
lastupdated: "2022-04-08"

keywords: 

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I delete my Subnet?
{: #troubleshoot-delete-subnet}
{: troubleshoot}
{: support}

You attempted to delete your subnet, and received an error.
{: shortdesc}

The following error message appeared when you attempted to delete a subnet:
{: tsSymptoms}

![Delete subnet error](/images/delete-subnet-error.png "Delete subnet error"){: caption="Figure 1. Delete subnet error" caption-side="bottom}

When you create a pool and associate a health check to that pool, {{site.data.keyword.dns_short}} automatically provisions an appliance that attaches to a network interface in your subnet.
{: tsCauses}

To remove the subnet, first remove the health check configuration associated with your pool and then try deleting your subnet again. 
{: tsResolve}

To remove the health check, take the following steps:

1. Navigate to **Global load balancer > Origin pools**
1. Click the overflow menu ![overflow menu](/images/overflow-icon.png "overflow menu icon") and select **Edit**
1. In the side panel that appears, scroll to the Health monitoring section and select **No health check** from the drop down menu
1. Click **Save**

You do not need to delete the pool itself.
{: note}

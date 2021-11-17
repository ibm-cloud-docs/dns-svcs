---

copyright:
  years: 2020
lastupdated: "2020-07-23"

keywords: backup, restore

subcollection: dns-svcs
---

{{site.data.keyword.attribute-definition-list}}

# Backing up and restoring data
{: #backup-restore}

DNS Services takes daily backups. You can take your own backups, if needed. For IBM and customer responsibilities related to High Availability and Disaster Recovery, refer to [Understanding your responsibilities when using {{site.data.keyword.dns_full_notm}}](/docs/dns-svcs?topic=dns-svcs-responsibilities-dns-svcs#responsibilities-dns-svcs).
{: shortdesc}

## Backing up {{site.data.keyword.dns_short}} data
{: #backup-data}

{{site.data.keyword.dns_short}} takes point-in-time backups of all data and saves it in the **Dallas** and **Frankfurt** regions. 

## Restoring a deleted service instance
{: #restoring-a-deleted-service-instance}

After you delete an instance of {{site.data.keyword.dns_short}}, you can restore the deleted service instance within the data retention period of seven days. After the seven-day period expires, the service instance is permanently deleted.

To view which service instances are available for restoration, use the `ibmcloud resource reclamations` command. To restore a deleted service instance, use the `ibmcloud resource reclamation-restore` command.

Learn more about [managing resources](/docs/account?topic=account-manage_resource).
{: note}

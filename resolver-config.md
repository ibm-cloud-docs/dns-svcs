---

copyright:
  years: 2019, 2020
lastupdated: "2020-01-09"

keywords: DNS Resolver, CentOS, RHEL, Ubuntu

subcollection: dns-svcs

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}


# Updating the DNS resolver for different OSes
{: #updating-dns-resolver}

This document is intended as general guidance only. Refer to your operating system's documentation for full details.
{:important}

This section describes how to update the DNS resolver for the following operating systems:
{: shortdesc}
 - CentOS 7.x
 - RHEL 7.x
 - Ubuntu Linux 18.04 LTS Bionic Beaver

Always take backups of your original configuration file before performing any of the following operations.
{:tip}

## CentOS 7.x
{: #updating-dns-resolver-centos}

### Modifying **`/etc/resolv.conf`**
{: #updating-dns-resolver-centos-resolv}

CentOS 7.x makes use of the `/etc/resolv.conf` file for the DNS resolver configuration. Update this file with the DNS Services name servers `161.26.0.7` and `161.26.0.8`.

## RHEL 7.x
{: #updating-dns-resolver-rhel}

### Modifying **`/etc/resolv.conf`**
{: #updating-dns-resolver-rhel-resolv}

RHEL 7.x makes use of the `/etc/resolv.conf` file for the DNS resolver configuration. Update this file with the DNS Services name servers `161.26.0.7` and `161.26.0.8`.

## Ubuntu Linux 18.04 LTS Bionic Beaver
{: #updating-dns-resolver-ubuntu}

### Modifying **`/etc/netplan/50-cloud-init.yaml`**
{: #updating-dns-resolver-ubuntu-resolv}

Ubuntu Linux 18.04 makes use of netplan and the `/etc/netplan/50-cloud-init.yaml` file for the DNS resolver configuration. Update this file with the DNS Services name servers `161.26.0.7` and `161.26.0.8`. To apply the changes run the command:

```console
sudo netplan apply
```
{:pre}

If you are still unable to resolve with the new configuration, flush all DNS resource record caches the systemd service maintains locally, and try again.

```console
systemd-resolve --flush-caches
```
{:pre}

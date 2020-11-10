---

copyright:
  years: 2019, 2020
lastupdated: "2020-11-09"

keywords: DNS Resolver

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


# Updating the DNS resolver for your VSI
{: #updating-dns-resolver}

This document is intended as general guidance only. Refer to your operating system's documentation for full details.
{:important}

Any VPC added to a private DNS zone before November 10, 2020, must configure the virtual server instance to use private DNS resolvers (`161.26.0.7` and `161.26.0.8`). VPCs added after November 11, 2020 are configured automatically with private DNS resolvers. 
{:note}

[Generation 1](#updating-dns-resolver-vpcgen1) and [generation 2](#updating-dns-resolver-vpcgen2) VPC virtual server instances (VSI) have different networking configurations. Refer to the appropriate section for your use case.
{:shortdesc}

Always take backups of your original configuration file before performing any of the following operations.
{:tip}

## VPC with generation 2 compute instances
{: #updating-dns-resolver-vpcgen2}

The DNS name servers for VPC Gen2 compute instances are configured using DHCP. The following configuration changes ensure that the DNS configuration change persists across reboots.

### Configuring CentOS 7.x
{: #updating-dns-resolver-centos-vpcgen2}

Follow these steps to modify the DHCP client configuration in CentOS 7.x.

1. Create the file `/etc/dhcp/dhclient.conf` and write the following contents:

  ```
  supersede domain-name-servers 161.26.0.7, 161.26.0.8;
  ```
  {:codeblock}

2. Next run the following command to release the current lease and stop the running DHCP client. Then restart the DHCP client.

  ```console
  dhclient -v -r eth0; dhclient -v eth0
  ```
  {:pre}


### Configuring Ubuntu Linux 18.04 LTS Bionic Beaver
{: #updating-dns-resolver-ubuntu-vpcgen2}

Follow these steps to modify the DHCP client configuration in Ubuntu Linux 18.04 LTS Bionic Beaver.

1. Ensure your version of netplan is 0.95 or later:

   ```console
   dpkg -l |grep netplan
   ii  netplan.io                      0.98-0ubuntu1~18.04.1               amd64        YAML network configuration abstraction   for various backends
   ```
   {:codeblock}
  
   If your netplan version is earlier than 0.95, upgrade netplan:

   ```console
   apt-get update
   apt-get upgrade
   ```
   {:codeblock}

2. Create the file `/etc/netplan/99-custom-dns.yaml` with the following content:

   If your VSI has more than one ethernet device, add a stanza for each device. This example uses the device name `ens3`. Replace this with the appropriate name for your interface.
   {:note}
  
   ```yaml
   network:
       version: 2
       ethernets:
           ens3:
               nameservers:
                   addresses: [ "161.26.0.7", "161.26.0.8" ]
               dhcp4-overrides:
                   use-dns: false
   ```
   {:codeblock}

   The `use-dns: false` setting ensures the statically configured DNS servers take precedence for the interface.

3. Apply the changes to netplan:

   ```console
   netplan apply
   ```
   {:codeblock}

4. Open the `/etc/dhcp/dhclient.conf` file and add the line:

   ```
   supersede domain-name-servers 161.26.0.7, 161.26.0.8;
   ```
   {:codeblock}

5. Run the following command to release the current lease and stop the running DHCP client, then restart the DHCP client. Doing this ensures the statically configured DNS servers take precedence globally.

   ```console
   dhclient -v -r; dhclient -v
   ```
   {:pre}

If you are still unable to resolve with the new configuration, flush all DNS resource record caches the `systemd` service maintains locally, and try again.

```console
systemd-resolve --flush-caches
```
{:pre}

## VPC with generation 1 compute instances
{: #updating-dns-resolver-vpcgen1}
The DNS name servers for VPC Gen1 compute instances are configured using `/etc/resolv.conf`. The following configuration changes ensure that the DNS configuration change persists across reboots.


### Configuring CentOS 7.x
{: #updating-dns-resolver-centos-vpcgen1}

CentOS 7.x makes use of the `/etc/resolv.conf` file for the DNS resolver configuration. Update this file with the DNS Services name servers `161.26.0.7` and `161.26.0.8`.

### Configuring RHEL 7.x
{: #updating-dns-resolver-rhel-vpcgen1}

RHEL 7.x makes use of the `/etc/resolv.conf` file for the DNS resolver configuration. Update this file with the DNS Services name servers `161.26.0.7` and `161.26.0.8`.

### Configuring Ubuntu Linux 18.04 LTS Bionic Beaver
{: #updating-dns-resolver-ubuntu-vpcgen1}

Ubuntu Linux 18.04 makes use of netplan and the `/etc/netplan/50-cloud-init.yaml` file for the DNS resolver configuration. Update this file with the DNS Services name servers `161.26.0.7` and `161.26.0.8`. To apply the changes run the command:

```console
sudo netplan apply
```
{:pre}

If you are still unable to resolve with the new configuration, flush all DNS resource record caches the `systemd` service maintains locally, and try again.

```console
systemd-resolve --flush-caches
```
{:pre}


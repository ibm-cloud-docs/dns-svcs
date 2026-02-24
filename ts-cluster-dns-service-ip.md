---

copyright:
  years: 2026
lastupdated: "2026-02-24"

keywords:

subcollection: dns-svcs

---

{{site.data.keyword.attribute-definition-list}}

# How do I confirm my cluster DNS Service IP?
{: #troubleshoot-check-cluster-dns-service-ip}
{: troubleshoot}
{: support}

You need to confirm the cluster DNS Service IP.
{: shortdesc}

A custom resolver that has a secondary zone configured is not responding to DNS queries for the configured zone.
{: tsSymptoms}

The OpenShift DNS Operator maintains a `default` DNS custom resource that contains the cluster DNS Service IP.
Run the following command to obtain the cluster DNS Service IP:
{: tsCauses}

 ```sh
oc get dns.operator/default -o jsonpath='{.status.clusterIP}'; echo
   ```
   {: pre}

This command returns the Cluster DNS Service IP that is used internally by the cluster.

Confirm which nameserver the `node-resolver` is using.
{: tsResolve}

The `node-resolver` DaemonSet in the `openshift-dns` namespace configures node-level DNS resolution.
Run the following command to check the configured nameserver:

 ```sh
oc -n openshift-dns get ds/node-resolver \
  -o jsonpath='{.spec.template.spec.containers[0].env[?(@.name=="NAMESERVER")].value}'; echo
   ```
   {: pre}

This displays the value of the `NAMESERVER` environment variable used by `node-resolver`.

Check which upstream DNS servers the ROKS CoreDNS is pointing to by inspecting the `/etc/resolv.conf` file inside the CoreDNS pod. Run the following commands to check which upstream DNS servers the ROKS CoreDNS is pointing to:

1. Get DNS pods.

 ```sh
oc get pods -n openshift-dns
   ```
   {: pre}

1. Exec into one of the `dns-default` pods.

 ```sh
kubectl exec -it -n openshift-dns <dns-pod-name> -- sh
   ```
   {: pre}

Example:

 ```sh
kubectl exec -it -n openshift-dns dns-default-zdtr7 -- sh
   ```
   {: pre}

1. Check resolv.conf.

 ```sh
cat /etc/resolv.conf
   ```
   {: pre}

Example output:

 ```sh
nameserver 161.26.0.7
nameserver 161.26.0.8
   ```
   {: pre}

If the worker node `/etc/resolv.conf` is updated and CoreDNS does not automatically reflect the change, you must restart the DNS DaemonSet. This makes ROKS CoreDNS pick up changes in the worker node `/etc/resolv.conf`. Run the following commands to check which upstream DNS servers the ROKS CoreDNS is pointing to:

1. Run:

 ```sh
oc rollout restart daemonset/dns-default -n openshift-dns
   ```
   {: pre}

1. After restart, verify:

 ```sh
oc get pods -n openshift-dns
   ```
   {: pre}

Ensure all `dns-default` pods are in `Running` state and ready.

---
title: General FAQ
---

<head>
  <link rel="canonical" href="https://ranchermanager.docs.rancher.com/faq/general-faq"/>
</head>

This FAQ is a work in progress designed to answer the questions most frequently asked about Rancher v2.x.

See the [Technical FAQ](technical-items.md) for frequently asked technical questions.

## Does Rancher v2.x support Docker Swarm and Mesos as environment types?

Swarm and Mesos are no longer selectable options when you create a new environment in Rancher v2.x. However, both Swarm and Mesos will continue to be available as Catalog applications you can deploy. It was a tough decision to make but, in the end, it came down to adoption. For example, out of more than 15,000 clusters, only about 200 were running Swarm.

## Is it possible to manage Azure Kubernetes Services with Rancher v2.x?

Yes. See our [Cluster Administration](../pages-for-subheaders/manage-clusters.md) guide for what Rancher features are available on AKS, as well as our [documentation on AKS](../getting-started/installation-and-upgrade/install-upgrade-on-a-kubernetes-cluster/rancher-on-aks.md).

## Does Rancher support Windows?

Yes. Rancher supports Windows Server 1809 containers. For details on how to set up a cluster with Windows worker nodes, refer to the section on [configuring custom clusters for Windows.](../pages-for-subheaders/use-windows-clusters.md)

## Does Rancher support Istio?

Yes. Rancher supports [Istio](../pages-for-subheaders/istio.md).

## Will Rancher v2.x support Hashicorp's Vault for storing secrets?

Secrets management is on our roadmap but we haven't assigned it to a specific release yet.

## Does Rancher v2.x support RKT containers as well?

At this time, we only support Docker.

## Does Rancher v2.x support Calico, Contiv, Contrail, Flannel, Weave net, etc., for embedded and registered Kubernetes?

Out-of-the-box, Rancher provides the following CNI network providers for Kubernetes clusters: Canal, Flannel, Calico and Weave.  Always refer to the [Rancher Support Matrix](https://rancher.com/support-maintenance-terms/) for details about what is officially supported.

## Are you planning on supporting Traefik for existing setups?

We don't currently plan on providing embedded Traefik support, but we're still exploring load-balancing approaches.

## Can I import OpenShift Kubernetes clusters into v2.x?

Our goal is to run any Kubernetes clusters. Therefore, Rancher v2.x should work with OpenShift, but we haven't tested it yet.

## Is Longhorn integrated with Rancher?

Yes. Longhorn is integrated with Rancher v2.5 and later.

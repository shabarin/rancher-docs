---
title: Cloning Clusters
---

If you have a cluster in Rancher that you want to use as a template for creating similar clusters, you can use Rancher CLI to clone the cluster's configuration, edit it, and then use it to quickly launch the cloned cluster.

Duplication of imported clusters is not supported.

| Cluster Type                     | Cloneable?    |
|----------------------------------|---------------|
| [Nodes Hosted by Infrastructure Provider](../../../pages-for-subheaders/use-new-nodes-in-an-infra-provider.md) | ✓ |
| [Hosted Kubernetes Providers](../../../pages-for-subheaders/set-up-clusters-from-hosted-kubernetes-providers.md) | ✓    |
| [Custom Cluster](../../../pages-for-subheaders/use-existing-nodes.md)              | ✓              |
| [Imported Cluster](../../new-user-guides/kubernetes-clusters-in-rancher-setup/import-existing-clusters.md)            |               |

> **Warning:** During the process of duplicating a cluster, you will edit a config file full of cluster settings. However, we recommend editing only values explicitly listed in this document, as cluster duplication is designed for simple cluster copying, _not_ wide scale configuration changes. Editing other values may invalidate the config file, which will lead to cluster deployment failure.

## Prerequisites

Download and install [Rancher CLI](../../../pages-for-subheaders/cli-with-rancher.md). Remember to [create an API bearer token](../../../reference-guides/user-settings/api-keys.md) if necessary.


## 1. Export Cluster Config

Begin by using Rancher CLI to export the configuration for the cluster that you want to clone.

1. Open Terminal and change your directory to the location of the Rancher CLI binary, `rancher`.

1. Enter the following command to list the clusters managed by Rancher.


        ./rancher cluster ls


1. Find the cluster that you want to clone, and copy either its resource `ID` or `NAME` to your clipboard. From this point on, we'll refer to the resource `ID` or `NAME` as `<RESOURCE_ID>`, which is used as a placeholder in the next step.

1. Enter the following command to export the configuration for your cluster.


        ./rancher clusters export <RESOURCE_ID>


    **Step Result:** The YAML for a cloned cluster prints to Terminal.

1. Copy the YAML to your clipboard and paste it in a new file. Save the file as `cluster-template.yml` (or any other name, as long as it has a `.yml` extension).

## 2. Modify Cluster Config

Use your favorite text editor to modify the cluster configuration in `cluster-template.yml` for your cloned cluster.

> **Note:** As of Rancher v2.3.0, cluster configuration directives must be nested under the `rancher_kubernetes_engine_config` directive in `cluster.yml`. For more information, refer to the section on [the config file structure in Rancher v2.3.0+.](../../../reference-guides/cluster-configuration/rancher-server-configuration/rke1-cluster-configuration.md#config-file-structure-in-rancher-v230)

1. Open `cluster-template.yml` (or whatever you named your config) in your favorite text editor.

    >**Warning:** Only edit the cluster config values explicitly called out below. Many of the values listed in this file are used to provision your cloned cluster, and editing their values may break the provisioning process.


1. As depicted in the example below, at the `<CLUSTER_NAME>` placeholder, replace your original cluster's name with a unique name (`<CLUSTER_NAME>`). If your cloned cluster has a duplicate name, the cluster will not provision successfully.

    ```yml
    Version: v3
    clusters:
        <CLUSTER_NAME>: # ENTER UNIQUE NAME
        dockerRootDir: /var/lib/docker
        enableNetworkPolicy: false
        rancherKubernetesEngineConfig:
        addonJobTimeout: 30
        authentication:
            strategy: x509
        authorization: {}
        bastionHost: {}
        cloudProvider: {}
        ignoreDockerVersion: true
    ```

1. For each `nodePools` section, replace the original nodepool name with a unique name at the `<NODEPOOL_NAME>` placeholder.  If your cloned cluster has a duplicate nodepool name, the cluster will not provision successfully.

    ```yml
    nodePools:
        <NODEPOOL_NAME>:
        clusterId: do
        controlPlane: true
        etcd: true
        hostnamePrefix: mark-do
        nodeTemplateId: do
        quantity: 1
        worker: true
    ```

1. When you're done, save and close the configuration.

## 3. Launch Cloned Cluster

Move `cluster-template.yml` into the same directory as the Rancher CLI binary. Then run this command:

    ./rancher up --file cluster-template.yml

**Result:** Your cloned cluster begins provisioning. Enter `./rancher cluster ls` to confirm. You can also log into the Rancher UI and open the **Global** view to watch your provisioning cluster's progress.

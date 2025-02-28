---
title: Stopping and starting an Elasticsearch cluster
description: 'If necessary, you can stop the Elasticsearch cluster and restart it. When you stop the cluster, all data in it will be saved, they will be available again when you start the cluster. '
keywords:
  - stopping Elasticsearch
  - starting Elasticsearch
  - Elasticsearch

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---


# Stopping and starting clusters

If necessary, you can stop and restart {{ ES }} clusters. When a cluster is stopped, all data in it is retained: it will be available again when you restart the cluster.

You are not charged for the time when your cluster remains stopped: you still pay only for the storage size based on the [pricing policy](../pricing.md#prices-storage).

{% include [pricing-status-warning.md](../../_includes/mdb/pricing-status-warning.md) %}

## Stopping a cluster {#stop-cluster}

{% list tabs %}

- Management console

  To stop all hosts in the cluster:
  1. Go to the folder page and select **{{ mes-name }}**.
  1. Find the cluster in the list and click ![options](../../_assets/horizontal-ellipsis.svg), and select **Stop**.
  1. In the dialog box that opens, confirm that you want to stop the cluster and click **Stop**.

- API

  Use the `stop` API method to stop all the cluster hosts: pass the ID of the required cluster in the `clusterId` request parameter.

  To find out the cluster ID, [get a list of clusters in the folder](cluster-list.md#list-clusters).

{% endlist %}

## Starting a cluster {#start-cluster}

You can restart **STOPPED** clusters.

{% list tabs %}

- Management console

  To start a cluster:
  1. Go to the folder page and select **{{ mes-name }}**.
  1. Find the stopped cluster you need in the list and click ![options](../../_assets/horizontal-ellipsis.svg), and select **Start**.
  1. In the dialog box that opens, confirm that you want to start the cluster and click **Start**.

- API

  To start the cluster, use the `start` API method: pass the ID of the desired cluster in the `clusterId` request parameter.

  To find out the cluster ID, [get a list of clusters in the folder](cluster-list.md#list-clusters).

{% endlist %}


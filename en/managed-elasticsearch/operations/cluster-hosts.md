---
title: Managing Elasticsearch hosts
description: 'You can get a list of hosts in the Elasticsearch cluster, and add and remove hosts from the cluster. You can only manage hosts with the Data Node role.'
keywords:
  - management of Elasticsearch hosts
  - Elasticsearch hosts
  - Elasticsearch

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---


# Managing hosts

You can get a list of {{ ES }} cluster hosts and add or delete them.

{% note info %}

You can only add or delete hosts with the [_Data node_](../concepts/index.md) role.

{% endnote %}

## Getting a list of cluster hosts {#list-hosts}

{% list tabs %}

- Management console
  1. Go to the folder page and select **{{ mes-name }}**.
  1. Click on the name of the cluster you need and select the **Hosts** tab.

- API

  Use the `listHosts` API method: pass the ID of the desired cluster in the `clusterId` request parameter.

  To find out the cluster ID, [get a list of clusters in the folder](cluster-list.md#list-clusters).

{% endlist %}

## Adding hosts to a cluster {#add-hosts}

{% list tabs %}

- Management console

    1. Go to the folder page and select **{{ mes-name }}**.

    1. Click on the name of the cluster you need and select the **Hosts** tab.

    1. Click **Add host**.

    1. Specify the host parameters:
        - Availability zone.
        - Subnet (if the necessary subnet is not in the list, [create it](../../vpc/operations/subnet-create.md).
        - Select the **Public access** option if the host must be accessible from outside {{ yandex-cloud }}.

- API

  Use the `addHosts` API method: pass the ID of the required cluster in the `clusterId` request parameter.

  To find out the cluster ID, [get a list of clusters in the folder](cluster-list.md#list-clusters).

  Add the required number of `hostSpecs` parameters with the host's settings (one parameter for each new host).

{% endlist %}

## Deleting hosts from a cluster {#delete-hosts}

The following restrictions apply when deleting hosts:

- You can't delete a single host with the _Data node_ role.
- If a cluster consists of multiple hosts with the _Data node_ role, you can't delete the last two hosts.

{% list tabs %}

- Management console
    1. Go to the folder page and select **{{ mes-name }}**.
    1. Click on the name of the cluster you need and select the **Hosts** tab.
    1. Click the ![image](../../_assets/vertical-ellipsis.svg) in the line of the necessary host and select **Delete**.

- API

  Use the `deleteHosts` API method: pass the ID of the required cluster in the `clusterId` request parameter.

  To find out the cluster ID, [get a list of clusters in the folder](cluster-list.md#list-clusters).

  In one or more `hostNames[]` parameters, specify the names of the hosts you wish to delete from the cluster.

{% endlist %}


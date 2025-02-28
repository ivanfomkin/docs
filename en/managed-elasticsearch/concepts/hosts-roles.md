---
title: Elasticsearch host roles
description: Each cluster of a Managed Service for Elasticsearch consists of one or more Elasticsearch hosts with different Data node or Master node roles.
keywords:
  - Elasticsearch host roles
  - Elasticsearch
  - Elasticsearch hosts

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---


# Host roles

Each {{ mes-name }} cluster consists of one or more {{ ES }} hosts with different roles: _Data node_ or _Master node_.

## Dedicated hosts with the _Data node_ role {#data-node}

Hosts with this role store one or more indexes and handle search and analysis queries. To ensure index scalability and fault tolerance, configure [sharding and replication](scalability-and-resilience.md) for this index.

For better handling indexes and search queries, [Kibana](https://www.elastic.co/kibana/features) is installed and configured on these hosts. It can be accessed from the web interface. To learn more, see [{#T}](../operations/cluster-connect.md).

{% note info %}

There should be at least one host with the _Data node_ role in the cluster.

{% endnote %}

## Dedicated hosts with the _Master node_ role {#master-node}

Hosts with this role monitor the state of the cluster and manage its configuration, ensuring the performance of all {{ ES }} components.

When using dedicated hosts with the _Master node_ role, 3 such hosts are added to the cluster and you can't change their number.

If no hosts with the _Master node_ role are used, this role will be supported by hosts with the _Data node_ role. However, the presence of dedicated hosts with the _Master node_ role increases the overall cluster reliability and reduces the load on hosts with the _Data node_ role.


---

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---
# DB network and clusters


When creating a cluster, you can:

* Set the network for the cluster itself.

* Set the subnets for each host in the cluster.

* Request a public IP address to access the cluster from outside {{ yandex-cloud }}.

You can create a cluster without specifying any subnets for the hosts, if the availability zone selected for each host contains exactly one subnet of the cluster network.

## Hostname and FQDN {#hostname}

{{ mms-short-name }} generates a name for each cluster host during creation. This name will be the host's fully qualified domain name (FQDN). The hostname and, consequently, the FQDN cannot be changed.


You can use the FQDN to access the host within a single cloud network. Read more in the [{{ vpc-full-name }} documentation](../../vpc/).

## Public access to a host {#public-access-to-a-host}

Any cluster host can be accessible from outside {{ yandex-cloud }} if you requested public access when creating the host. To connect to such a host, use its FQDN.

It is not possible to request a public address after creating a host, but you can replace one of the existing hosts with a new host that has a public address.

When deleting a host with a public FQDN, the assigned IP address is revoked.


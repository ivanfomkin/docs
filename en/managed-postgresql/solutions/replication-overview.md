---

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---
# Logical PostgreSQL replication

{{ mpg-name }} supports [logical replication](https://www.postgresql.org/docs/current/logical-replication.html).

Logical replication streams for a {{ mpg-name }} cluster are transparently passed through the [Odyssey connection pooler](../concepts/pooling.md). This helps perform the following tasks using logical replication:

* [{#T}](../operations/data-migration.md).
* [{#T}](../solutions/outbound-replication.md).
* [{#T}](../operations/logical-replica-from-rds.md).


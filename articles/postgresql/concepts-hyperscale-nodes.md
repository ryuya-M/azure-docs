---
title: Nodes – Hyperscale (Citus) - Azure Database for PostgreSQL
description: Learn about the two types of nodes, coordinator and workers, in a server group in Azure Database for PostgreSQL.
author: jonels-msft
ms.author: jonels
ms.service: postgresql
ms.subservice: hyperscale-citus
ms.topic: conceptual
ms.date: 07/28/2020
---

# Nodes in Azure Database for PostgreSQL – Hyperscale (Citus)

The Hyperscale (Citus) hosting type allows Azure Database for
PostgreSQL servers (called nodes) to coordinate with one another in a "shared
nothing" architecture. The nodes in a server group collectively hold more data
and use more CPU cores than would be possible on a single server. The
architecture also allows the database to scale by adding more nodes to the
server group.

## Coordinator and workers

Every server group has a coordinator node and multiple workers. Applications
send their queries to the coordinator node, which relays it to the relevant
workers and accumulates their results. Applications are not able to connect
directly to workers.

Hyperscale (Citus) allows the database administrator to *distribute* tables,
storing different rows on different worker nodes. Distributed tables are the
key to Hyperscale performance. Failing to distribute tables leaves them entirely
on the coordinator node and cannot take advantage of cross-machine parallelism.

For each query on distributed tables, the coordinator either routes it to a
single worker node, or parallelizes it across several depending on whether the
required data lives on a single node or multiple. The coordinator decides what
to do by consulting metadata tables. These tables track the DNS names and
health of worker nodes, and the distribution of data across nodes.

## Next steps
- Learn about [distributed tables](concepts-hyperscale-distributed-data.md)

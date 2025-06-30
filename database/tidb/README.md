## 🐲 Why TiDB?

We chose **TiDB** to power systems that require:

* High **concurrent connection handling**
* Effortless **horizontal scaling** for growth
* Support for both **transactional (OLTP)** and **analytical (OLAP)** queries
* Built-in **fault tolerance** and **high availability**
* Simplified infrastructure for fast-moving teams

TiDB offers the flexibility to start small — even with a single node — and evolve into a fully distributed, cloud-native architecture as demand increases.

---

## 🌚 TiDB vs PostgreSQL – Practical Trade-offs

| Feature/Concern               | PostgreSQL (Standalone)                         | TiDB (Single Node or Clustered)                         |
| ----------------------------- | ----------------------------------------------- | ------------------------------------------------------- |
| **Connections Handling**      | Requires connection pooling (e.g., PgBouncer)   | Built-in, stateless SQL layer handles high concurrency  |
| **Horizontal Scaling (OLTP)** | Manual sharding or complex extensions needed    | Native support through distributed TiKV + PD            |
| **OLAP Support**              | Add-ons (e.g., Citus) or external tools needed  | OLAP support is built-in and SQL-compliant              |
| **High Availability**         | Requires additional setup (e.g., Patroni, Etcd) | Built-in with automatic leader election and replication |
| **Storage Engine**            | Single-node, monolithic                         | Distributed, Raft-based key-value store                 |
| **Operational Overhead**      | Low for basic use; high for HA and scale        | Simplified scaling and resilience with cluster mode     |
| **Deployment (Single Node)**  | Very lightweight                                | Heavier footprint but suitable for small-scale setup    |
| **Backup/Restore**            | pg\_dump / pg\_basebackup                       | Fast, parallelized backup/restore via BR tool           |
| **Open Source License**       | PostgreSQL License                              | Apache 2.0 (Community Edition)                          |

---

## 🚀 Ideal Use Cases for TiDB

TiDB is well-suited for:

* Applications expecting **organic growth** in data or users
* Systems with **spiky or sustained high concurrency**
* Platforms needing **OLTP and OLAP** support from a unified engine
* Engineering teams seeking to **minimize operational complexity** while planning for future scale

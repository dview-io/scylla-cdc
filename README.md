# scylla-cdc
Release v1.0.0.0

scylla-cdc is a library that makes it easy to consume the [Scylla CDC log](https://docs.scylladb.com/using-scylla/cdc/) and push it to [KAFKA](https://kafka.apache.org/). The library automatically and transparently handles errors and topology changes of the underlying Scylla cluster.

It is recommended to get familiar with the Scylla CDC documentation first, in order to understand the concepts used in the documentation of scylla-cdc-java: https://docs.scylladb.com/using-scylla/cdc/.

## Scylla CDC Source Connector
[Scylla CDC Source Connector](https://github.com/scylladb/scylla-cdc-source-connector) is a source connector capturing row-level changes in the tables of a Scylla cluster.

## Why Use a Library?
Scylla's design of CDC is based on the concept of CDC log tables. For every table whose changes you wish to track, an associated CDC log table is created. We refer to this new table as the CDC log table and the original table as a base table. Every time you modify your data in the base table — insert, update or delete — this fact is recorded by inserting one or more rows to the corresponding CDC log table. This library also supports replication of **UDT & Collections (Map, List & Set)** columns. 

## Key Features:
    1. Checkpointing
    2. Table level observability
    3. UDT & Collection Type support    

## Installation

You can integrate it in your application by using helm installation. Make changes in values.yaml as per instructions:

**Prerequisite:**

    ```bash
        Create Database scylla_cdc;
        CREATE TABLE `scylla_checkpoint` (
        `id` int unsigned NOT NULL AUTO_INCREMENT,
        `instance_name` varchar(128) DEFAULT NULL,
        `keyspace_table_combination` varchar(128) DEFAULT NULL,
        `last_read_cdc_timestamp` bigint DEFAULT NULL,
        `created_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
        `updated_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
        PRIMARY KEY (`id`)
        );
    ```

```bash
git clone https://github.com/dview-io/scylla-cdc
helm install {ReleaseName} ./helm -n {Namespace}
```


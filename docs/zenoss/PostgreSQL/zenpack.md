# PostgreSQL

@lb[](img/zenpack-postgresql-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.zenoss.PostgreSQL

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.PostgreSQL){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.PostgreSQL.git){.external-link}

### Applications Monitored:

[PostgreSQL (8.1, 8.4, 9.1-9.5)](https://www.postgresql.org/){.external-link}

[Postgres-BDR 9.4](https://www.2ndquadrant.com/en/resources/bdr/){.external-link}

## PostgreSQL ZenPack

This ZenPack provides status and performance monitoring of PostgreSQL.

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 1.0.12
- [Download](https://delivery.zenoss.com/){.external-link}
Released on 2020/1/14
Compatible with Zenoss 6.4.1 - 6.5.0, Zenoss Cloud and Service Impact
5.5.3

Version
1.0.10-[Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.PostgreSQL/1.0.10/ZenPacks.zenoss.PostgreSQL-1.0.10.egg){.external-link}
Released on 2018/1/5
Compatible with Zenoss 4.2.x-6.1.x

Version
1.0.9-[Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.PostgreSQL/1.0.9/ZenPacks.zenoss.PostgreSQL-1.0.9.egg){.external-link}
Released on 2017/4/27
Compatible with Zenoss 4.2.x-5.2.x

Version
1.0.8-[Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.PostgreSQL/1.0.8/ZenPacks.zenoss.PostgreSQL-1.0.8.egg){.external-link}
Released on 2014/11/06
Compatible with Zenoss Core 4.2.x-5.0.x, Zenoss RM 4.2.x

## Contents

-   [Background](#background)
-   [Features](#features)
    -   [Discovery](#discovery)
    -   [Monitoring](#monitoring)
-   [Usage](#usage)
    -   [PostgreSQL Server Impact](#post-gresqlserver-impact)
-   [Limitations](#limitations)
    -   [Troubleshooting Modeling](#troubleshooting-modeling)
-   [Changes](#changes)

## Background

This ZenPack makes it possible to monitor the performance of a
PostgreSQL database server, the individual databases, and the tables
within those databases.

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Discovery of PostgreSQL components.
-   Monitoring of PostgreSQL metrics.

### Discovery

The following types of components will be automatically discovered. The
attributes and collections will be updated on Zenoss' normal remodeling
interval which defaults to every 12 hours.

Databases:

-   Attributes:

    -   Name
    -   OID
    -   Size
    -   Table Count

-   Collections:

    -   Tables

Tables:

-   Attributes: Name

    -   OID
    -   Schema
    -   Size
    -   Size
    -   Database

### Monitoring

The following metrics will be collected every 5 minutes by default.

-   Server

    -   Metrics: Summaries of all databases and tables.

-   Databases

    -   Metrics: Size, Backends, Summaries of all tables.
    -   Latency Metrics: Connection, SELECT 1
    -   Connection Metrics: Total, Active, Idle
    -   Duration Metrics: Active Transactions (min/avg/max), Idle
        Transactions (min/avg/max), Queries (min/avg/max)
    -   Efficiency Metrics: Transaction Rollback Percentage, Tuple Fetch
        Percentage
    -   Transaction Rate Metrics: Commits/sec, Rollbacks/sec
    -   Tuple Rate Metrics: Returned/sec, Fetched/sec, Inserted/sec,
        Updated/sec, Deleted/sec
    -   Lock Metrics: Total, Granted, Waiting, Exclusive,
        AccessExclusive

-   Tables

    -   Scan Rate Metrics: Sequential/sec, Indexed/sec
    -   Tuple Rate Metrics: Sequentially Read/sec, Index Fetched/sec,
        Inserted/sec, Updated/sec, Hot Updated/sec, Deleted/sec
    -   Tuple Metrics: Live, Dead

## Usage

Once the PostgreSQL ZenPack is installed you will have the following new
configuration properties which should be set either for device classes
or individual devices.

-   Configuration Properties

    -   *zPostgreSQLPort* - Port where PostgreSQL is listening. Default:
        5432
    -   *zPostgreSQLUseSSL* - Whether to use SSL or not. Default: False
    -   *zPostgreSQLUsername* - Must be a superuser. Default: postgres
    -   *zPostgreSQLPassword* - Password for user. No default.
    -   *zPostgreSQLDefaultDB* - Default database. Default: postgres

In addition to setting these properties you must add the
''zenoss.PostgreSQL'' modeler plugin to a device class or individual
device. This modeler plugin will discover all databases and tables using
the connectivity information provided through the above settings. Each
database and table will automatically be monitored.

### PostgreSQL Server Impact

Zenoss will run the following queries every five (5) minutes. These
queries are intended to be lightweight so as to not adversely affect the
server's performance.

~~~ sourceCode
-- Database statistics - Run once. SELECT d.datname, pg_database_size(s.datid) AS size, numbackends, xact_commit, xact_rollback, blks_read, blks_hit, tup_returned, tup_fetched, tup_inserted, tup_updated, tup_deleted FROM pg_database AS d JOIN pg_stat_database AS s ON s.datname = d.datname WHERE NOT datistemplate AND datallowconn -- Connection statistics - Run once. SELECT datname, xact_start, query_start, backend_start, now() AS now FROM pg_stat_activity -- Lock statistics - Run once. SELECT d.datname, l.mode, l.granted FROM pg_database AS d LEFT JOIN pg_locks AS l ON l.database = d.oid WHERE NOT d.datistemplate AND d.datallowconn -- Table statistics - Run once per database. SELECT relname, pg_relation_size(relid), pg_total_relation_size(relid), seq_scan, seq_tup_read, idx_scan, idx_tup_fetch, n_tup_ins, n_tup_upd, n_tup_del, n_tup_hot_upd, n_live_tup, n_dead_tup, last_vacuum, last_autovacuum, last_analyze, last_autoanalyze FROM pg_stat_user_tables
~~~

The following queries will be run whenever the PostgreSQL server device
is remodeled. This occur once every 12 hours.

~~~ sourceCode
-- Database list - Run once. SELECT d.datname, s.datid, pg_database_size(s.datid) AS size FROM pg_database AS d JOIN pg_stat_database AS s ON s.datname = d.datname WHERE NOT datistemplate AND datallowconn -- Table list - Run once per database. SELECT relname, relid, schemaname, pg_relation_size(relid) AS size, pg_total_relation_size(relid) AS total_size FROM pg_stat_user_tables
~~~

## Limitations

### Troubleshooting Modeling

If the device fails to model PostgreSQL components with the error:
"WARNING zen.ZenModeler: Python client creation failed" you can either
1) clear the events and remodel the device or 2) set the
zSnmpMonitorIgnore property to True and remodel.

## Changes

1.0.12

-   Resolved issue with error in pg8000 library on Ubuntu OS (ZPS-7424)
-   Resolved issue with falling data collecting after platform upgrade.
    (ZPS-6818)
-   Tested with Zenoss Cloud, Zenoss 6.4.1, Zenoss 6.5.0 and Service
    Impact 5.5.3

1.0.10

-   Add support for Bi-Directional Replication (ZPS-249)

-   Add support variable default database name (ZPS-2767)

-   Added zProperties:

    -   zPostgreSQLDefaultDB: Sets default database for administration
        data

-   Added doc updates for failed modeling (ZEN-29375)

-   Tested with Zenoss Resource Manager 5.3.3 ,Zenoss Resource Manager
    6.0.1, Zenoss Resource Manager 6.1.0 and Zenoss Resource Manager
    4.2.5 RPS 743

1.0.9

-   Filter PIDs for lock query (ZEN-15165)
-   Guard against locks in PGSQL poller (ZPS-312)

1.0.8

-   Handle null data by skipping it (ZEN-14276)
-   Update pg8000 lib to 1.9.14 (ZEN-12752)

## Attachments:

-   [postgresql-zenpack.png](img/zenpack-postgresql-zenpack.png)
-   [postgresql-zenpack.png](img/zenpack-postgresql-zenpack.png)
-   [postgresql-zenpack.png](img/zenpack-postgresql-zenpack.png)
-   [postgresql-zenpack.png](img/zenpack-postgresql-zenpack.png)


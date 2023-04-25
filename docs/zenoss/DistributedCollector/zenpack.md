# Distributed Collector

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.DistributedCollector

## Distributed Collector ZenPack

Distributed Collector allows you to deploy additional performance
collection and event monitoring daemons to the Resource Manager server
or other servers.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.DistributedCollector ZenPack allows you to deploy
additional performance collection and event monitoring daemons, on the
Zenoss platform master host, and on other hosts.

This feature allows you to:

-   Distribute processor, disk, and network load across multiple
    servers.
-   Collect performance and events from networks that cannot be reached
    by the Zenoss platform server.
-   Configure more than one set of monitoring settings, such as
    different cycle times, for the `zenperfsnmp` daemon.

When you first install Distributed Collector, Zenoss platform is
configured with one hub and one collector. You cannot delete the initial
hub and collector (each named localhost) that are set up by Distributed
Collector.

## About Collectors

A *collector* is a set of collection daemons, on the Zenoss platform
server or another server, that shares a common configuration. That
configuration contains values, such as:

-   Number of seconds between SNMP collections cycles
-   Default discovery networks
-   Maximum number of `zenprocess` parallel jobs

Each collector has its own copy of each of the Zenoss platform
collection daemons. For example, Zenoss platform initially contains
collection daemons with names like `zenperfsnmp`, `zenprocess`, and
`zenping`.

## About Hubs

Distributed Collector also allows you to set up new hubs. A *hub*
represents an instance of the zenhub daemon, through which all collector
daemons communicate with the object and event databases.

All collectors must belong to exactly one hub; however, a hub can have
many collectors associated with it. All hubs (and indirectly all
collectors) refer to the same object and event databases. Typically, in
Zenoss 4.x and up, only very large systems with more than five
collectors (or more than 1,500 devices) benefit from multiple hubs. In
5.x and up, only one hub is recommended.

Hubs manage configuration data and pass it to the collectors. Hubs also
take data from the collectors and pass it to the Zenoss DataStore.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.4 or higher |
| Required ZenPacks | ZenPacks.zenoss.DistributedCollector      |

## Additional Documentation

For more documentation on using remote collectors, please see the
[Zenoss Service Dynamics Help Center](https://help.zenoss.com/zsd){.external-link}

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


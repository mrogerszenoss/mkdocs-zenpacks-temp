# HBase

@lb[](img/zenpack-apache-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.zenoss.HBase

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.HBase){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.HBase.git){.external-link}

### Applications Monitored:

Apache HBase

## HBase ZenPack

Monitoring for Apache HBase databases.

## Contents

[1 HBase ZenPack](#hbase-zenpack)

[1.1 Support](#support)

[1.2 Releases](#releases)

[1.3 Background](#background)

[1.4 Features](#features)

[1.4.1 Discovery](#discovery)

[1.4.2 Performance Monitoring](#performance-monitoring)

[1.4.3 Event monitoring](#event-monitoring)

[1.4.4 Service Impact](#service-impact)

[1.5 Usage](#usage)

[1.5.1 Access Authentication to Apache HBase](#access-authentication-to-apache-hbase)

[1.6 Prerequisites](#prerequisites)

[1.7 Troubleshooting](#troubleshooting)

[1.8 Installed Items](#installed-items)

[1.9 Daemons](#daemons)

[1.10 Changes](#changes)

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 1.0.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.HBase/1.0.0/ZenPacks.zenoss.HBase-1.0.0.egg){.external-link}:   Released on 2014/09/05:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Resource Manager 4.1.x,
    Zenoss Resource Manager 4.2.x, Zenoss Resource Manager 5.0.x

## Background

The ZenPacks.zenoss.HBase ZenPack monitors HBase clusters via *Apache
HBase REST Interface* and Python `twisted.web.client` asynchronous
framework.

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Discovery and periodic remodeling of relevant components.
-   Performance monitoring.
-   Event monitoring.
-   Optional service impact with addition of Zenoss Service Dynamics
    product.

### Discovery

The following components will be automatically discovered through
zProperties you provide:

Region Servers:   *Attributes*: Name (DomainName:port), Start Code, Handler Count,
    Memstore Upper Limit, Memstore Lower Limit, Log Flush Interval:   *Collections*: Regions

Regions:   *Attributes*: Table, Start Key, Region ID, Region Server, Memstore
    Flush Size, Max File Size

Tables:   *Attributes*: Name, Number of Column Families, Column Family Block
    Size, Compaction, Enabled

### Performance Monitoring

The following metrics will be collected and graphed every 5 minutes by
default:

HBase Cluster Metrics:   *Region Server Statistics*: The number of dead, live and overall
    number of Region Servers:   *Performance*: Average load, Requests

Region Servers:   *Region Statistics*: Number of Regions, Storefiles and Stores:   *Memory Usage*: Max and Used Heap Memory Size (MB):   *Storage Statistics*: Memstore Size (MB), Storefile Index Size (MB),
    Storefile Size (MB):   *Requests*: Read, Write, Requests/sec:   *Blocks*: Block Cache Count, Block Cache Evicted Count, Block Cache
    Hit Ratio (%), Block Cache Hit Caching Ratio (%):   *Performance metrics*: Compaction Queue Length, Flush Queue Length,
    Call Queue Length

Regions:   *Storage Statistics*: Memstore Size (MB), Storefile Index Size (MB),
    Storefile Size (MB), Storefiles, Stores:   *Requests*: Read, Write

### Event monitoring

The following events will be triggered with respect to the monitored
metrics:

HBase Cluster:   *Error*: Connection refused/Credentials not valid.
:   *Critical*: The percentage of dead servers exceeds 50%.
:   *Warning*: The percentage of dead servers exceeds 10%.

Region Servers:   *Error*: Connection refused/Credentials not valid.
:   *Error*: The server is dead.
:   *Warning*: The Memstore Size is nearing or exceeding its
    global.memstore.size (defaults to 40% of maxHeapSize).
:   *Info*: One or more region servers have been added/removed.

Regions:   *Error*: Connection refused/Credentials not valid.
:   *Warning*: The Memstore Size is nearing or exceeding its flush size
    (128MB by default).
:   *Warning*: The Storefile Size is nearing or exceeding the
    recommended maximum size (10GB by default).

Tables:   *Info*: New table is added.
:   *Error*: Connection refused/Credentials not valid.
:   *Error*: The table is disabled or dropped.

### Service Impact

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact capability for HBase. The following service
impact relationships are automatically added. These will be included in
any services containing one or more of the explicitly mentioned
entities.

<dl markdown="1">
<dt markdown="1">
Service Impact Relationships
</dt>
</dl>

-   Region failure affects related Table.
-   Region Server failure affects related Regions.
-   Region servers are affected by HBase hosting device failure.

<dl markdown="1">
<dt markdown="1">
External Impact Relationships
</dt>
</dl>

-   Region servers are affected by hosting Hadoop Data Node failure.

## Usage

Use the following steps to start monitoring HBase:

1.  Select Infrastructure from the navigation bar.
2.  Click the device name in the device list. The device overview page
    appears.
3.  Select *Configuration Properties* from the left panel.
4.  Set *zHBasePassword*, *zHBaseUsername* and select https for
    *zHBaseScheme* if you have Basic access authentication configured on
    your HBase master (otherwise leave *zHBasePassword* and
    *zHBaseUsername* blank).
5.  Set the *zHBaseRestPort*, *zHBaseMasterPort* and
    *zHBaseRegionServerPort* zProperties, if the values for those ports
    differ from the default ones.
6.  Navigate to the *Modeler plugins* page of the device containing your
    HBase server, add the *HBaseCollector* and *HBaseTableCollector*
    modeler plugins.
7.  Select *Model device* from the gear menu.

------------------------------------------------------------------------

Alternatively you can use zenbatchload to add HBase monitoring servers
from the command line. To do this, you must create a text file with
hostname, username and password of all the servers you want to add. The
devices should be added under the target machine device class (e.g.
'/Devices/Server/Linux' in the example below).

    /Devices/Server/Linux <HOST NAME or IP>
    zCollectorPlugins=['HBaseCollector', 'HBaseTableCollector'], zHBaseRestPort='8080', zHBaseMasterPort='60010', zHBaseRegionServerPort='60030', zHBasePassword='', zHBaseUsername='', zHBaseScheme='<http(s)>'

You can then load the HBase monitoring servers into Zenoss Core or
Resource Manager as devices with the following command.

    $ zenbatchload <filename>

### Access Authentication to Apache HBase

Access authentication may be configured on the target machine in one of
the following ways:

1.  apply appropriate firewall rules, which would permit only an
    explicit set of IP addresses permission to access HBase;
2.  configure proxy authentication.

## Prerequisites

This ZenPack uses the *Apache HBase REST Interface* for performance
monitoring, therefore the rest daemon should be started and running on
the port specified in *zHBaseRestPort* zProperty.

You can start the rest daemon by executing the following command:
`bin/hbase-daemon.sh start rest`

Please make sure that the ports for the HBase Master web UI and Hbase
Regionserver web UI are correctly set in *zHBaseMasterPort* and
*zHBaseRegionServerPort* zProperties, and that the UI instances are
running, as they are used for monitoring.

## Troubleshooting

Please refer to the Zenoss Service Dynamics documentation if you run
into any of the following problems:

-   ZenPack will not install
-   Adding a device fails
-   Don't understand how to add a device
-   Don't understand how to model a device

If you cannot find the answer in the documentation, then Resource
Manager (Service Dynamics) users should contact [Zenoss Customer Support](https://support.zenoss.com){.external-link}. Core users can use
the \#zenoss IRC channel or the community.zenoss.org forums.

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Modeler Plugins
</dt>
</dl>

-   HBaseCollector
-   HBaseTableCollector

<dl markdown="1">
<dt markdown="1">
Monitoring Templates
</dt>
</dl>

-   HBaseCluster (in /Device)
-   HBaseRegionServer (in /Device)
-   HBaseHRegion (in /Device)
-   HBaseTable (in /Device)

<dl markdown="1">
<dt markdown="1">
Component Types
</dt>
</dl>

-   HBaseRegionServer (on related device)
-   HBaseHRegion (on HBaseRegionServer)
-   HBaseTable (on related device)

## Daemons

|                       |           |
|-----------------------|-----------|
| Type                  | Name      |
| Performance Collector | zenpython |

## Changes

<dl markdown="1">
<dt markdown="1">
1.0.0
</dt>
</dl>

-   Initial release

## Attachments:

-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [External_Impact_Relationships.png](img/zenpack-external_impact_relationships.png)
-   [HBase_Cluster_graphs.png](img/zenpack-hbase_cluster_graphs.png)
-   [HBase_Impact.png](img/zenpack-hbase_impact.png)
-   [HBase_Region_Server.png](img/zenpack-hbase_region_server.png)
-   [HBase_Region.png](img/zenpack-hbase_region.png)
-   [HBase_Table.png](img/zenpack-hbase_table.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [External_Impact_Relationships.png](img/zenpack-external_impact_relationships.png)
-   [HBase_Cluster_graphs.png](img/zenpack-hbase_cluster_graphs.png)
-   [HBase_Impact.png](img/zenpack-hbase_impact.png)
-   [HBase_Region_Server.png](img/zenpack-hbase_region_server.png)
-   [HBase_Region.png](img/zenpack-hbase_region.png)
-   [HBase_Table.png](img/zenpack-hbase_table.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [External_Impact_Relationships.png](img/zenpack-external_impact_relationships.png)
-   [HBase_Cluster_graphs.png](img/zenpack-hbase_cluster_graphs.png)
-   [HBase_Impact.png](img/zenpack-hbase_impact.png)
-   [HBase_Region_Server.png](img/zenpack-hbase_region_server.png)
-   [HBase_Region.png](img/zenpack-hbase_region.png)
-   [HBase_Table.png](img/zenpack-hbase_table.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [External_Impact_Relationships.png](img/zenpack-external_impact_relationships.png)
-   [HBase_Cluster_graphs.png](img/zenpack-hbase_cluster_graphs.png)
-   [HBase_Impact.png](img/zenpack-hbase_impact.png)
-   [HBase_Region_Server.png](img/zenpack-hbase_region_server.png)
-   [HBase_Region.png](img/zenpack-hbase_region.png)
-   [HBase_Table.png](img/zenpack-hbase_table.png)


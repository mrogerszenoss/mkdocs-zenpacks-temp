# Hadoop

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

ZenPacks.zenoss.Hadoop

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.Hadoop){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.Hadoop.git){.external-link}

### Applications Monitored:

Apache Hadoop

## Hadoop ZenPack

Monitoring for the Apache Hadoop framework.

## Contents

[1 Hadoop ZenPack](#hadoop-zenpack)

[1.1 Support](#support)

[1.2 Releases](#releases)

[1.3 Background](#background)

[1.4 Features](#features)

[1.4.1 Discovery](#discovery)

[1.4.2 Performance Monitoring](#performance-monitoring)

[1.4.3 Event monitoring](#event-monitoring)

[1.4.4 Service Impact](#service-impact)

[1.4.5 HBase Autodiscover](#hbase-autodiscover)

[1.5 Usage](#usage)

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

Version 1.0.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.Hadoop/1.0.0/ZenPacks.zenoss.Hadoop-1.0.0.egg){.external-link}:   Released on 2014/09/05:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Resource Manager 4.1.x,
    Zenoss Resource Manager 4.2.x, Zenoss Resource Manager 5.0.x

## Background

The ZenPacks.zenoss.Hadoop ZenPack monitors Hadoop clusters via JMX web
interface (*JMXJsonServlet*) and Python `twisted.web.client`
asynchronous framework.

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Discovery and periodic remodeling of relevant components.
-   Performance monitoring.
-   Event monitoring.
-   Optional service impact with addition of Zenoss Service Dynamics
    product.
-   Optional HBase auto discovery.

### Discovery

The following components will be automatically discovered through
zProperties you provide:

Hadoop Data Node:   *Attributes*: Name, HBase Device, Last Contacted, Health State

Hadoop Secondary Name Node:   *Attributes*: Name, Health State

Hadoop Job Tracker:   *Attributes*: Name, Health State

Hadoop Task Tracker:   *Attributes*: Name, Health State

Hadoop Resource Manager:   *Attributes*: Name, Health State

Hadoop Node Manager:   *Attributes*: Name, Health State

Hadoop Job History:   *Attributes*: Name, Health State

**Note:** Yarn components (Resource Manager, Node Manager, Job History)
will be modeled for 2.x version of Hadoop and MapReduce components (Job
Tracker, Task Tracker) for previous versions.

### Performance Monitoring

The following metrics will be collected and graphed every 5 minutes by
default:

Device (Hadoop Name Node):   *Heap/Non Heap Memory*: Heap Memory Capacity Bytes, Heap Memory Used
    Bytes, Non Heap Memory Capacity Bytes, Non Heap Memory Used Bytes:   *Nodes*: Dead Nodes Count, Live Nodes Count:   *Performance metrics*: Threads, Total Files, HDFS: Configured
    Capacity, DFS Remaining, DFS Used

Hadoop Data Node:   *Blocks*: Blocks Written, Blocks Read, Blocks Removed:   *Heap/Non Heap Memory*: Heap Memory Capacity Bytes, Heap Memory Used
    Bytes, Non Heap Memory Capacity Bytes, Non Heap Memory Used Bytes

Hadoop Secondary Name Node:   *Heap/Non Heap Memory*: Heap Memory Capacity Bytes, Heap Memory Used
    Bytes, Non Heap Memory Capacity Bytes, Non Heap Memory Used Bytes

Hadoop Task Tracker:   *Tasks*: Tasks Completed, Tasks Failed Timeout, Tasks Failed Ping:   *Performance metrics*: Reduces Running, Maps Running

Hadoop Job Tracker:   *Heap/Non Heap Memory*: Heap Memory Capacity Bytes, Heap Memory Used
    Bytes, Non Heap Memory Capacity Bytes, Non Heap Memory Used Bytes:   *Jobs*: Jobs Running, Jobs Failed, Jobs Completed:   *Performance metrics*: Reduces Running, Maps Running

Hadoop Resource Manager:   *Heap/Non Heap Memory*: Heap Memory Capacity Bytes, Heap Memory Used
    Bytes, Non Heap Memory Capacity Bytes, Non Heap Memory Used Bytes:   *Nodes*: Active Nodes, Decommissioned Nodes, Lost Nodes, Unhealthy
    Nodes, Rebooted Nodes:   *Apps*: Apps Submitted, Apps Pending, Apps Running, Apps Completed

Hadoop Node Manager:   *Heap/Non Heap Memory*: Heap Memory Capacity Bytes, Heap Memory Used
    Bytes, Non Heap Memory Capacity Bytes, Non Heap Memory Used Bytes:   *Containers*: Containers Running, Containers Launched, Containers
    Completed, Containers Failed, Containers Initing, Containers Killed

Hadoop Job History:   *Heap/Non Heap Memory*: Heap Memory Capacity Bytes, Heap Memory Used
    Bytes, Non Heap Memory Capacity Bytes, Non Heap Memory Used Bytes

### Event monitoring

The following events will be triggered:

-   *Error*: Any of the components is down or not available
-   *Info*: HBase was discovered on one of the Data Nodes or Name Node

### Service Impact

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact capability for Hadoop. The following
service impact relationships are automatically added. These will be
included in any services containing one or more of the explicitly
mentioned entities.

<dl markdown="1">
<dt markdown="1">
Service Impact Relationships
</dt>
</dl>

-   Secondary Name Node, Job Tracker, Task Tracker, Resource Manager,
    Node Manager or Job History failure affects associated Data Node.
-   Secondary Name Node, Job Tracker, Task Tracker, Resource Manager,
    Node Manager and Job History are affected by hosting Device failure.

<dl markdown="1">
<dt markdown="1">
External Impact Relationships
</dt>
</dl>

-   Data Node failure affects associated HBase Region Servers.
-   Secondary Name Node, Job Tracker, Task Tracker, Resource Manager,
    Node Manager and Job History are affected by ZooKeeper failure.

### HBase Autodiscover

With a fully deployed Hadoop environment, the HBase Master server can
move around to different Hadoop Nodes. This ZenPack provides optional
discovery of HBase Master Device within Hadoop Data Nodes, which may be
configured with the help of the following configuration properties:

-   zHBaseAutodiscover
-   zHBaseDeviceClass

If you checkmark *zHBaseAutodiscover* property, every 5 minutes by
default each Hadoop Data Node will be probed for hosting HBase Master.
In case HBase is found, the HBase device will be created in the Device
Class set in *zHBaseDeviceClass* (usually /Server/Linux or
/Server/Microsoft/Windows) with HBase modeler plugins bound. If the
HBase device was already discovered, but HBase Master moves to a
different Node, the device's IP address will be changed to a new one.

## Usage

Use the following steps to start monitoring Hadoop cluster:

1.  Select *Infrastructure* from the navigation bar.
2.  Click the device name in the device list. The device overview page
    appears.
3.  Select *Configuration Properties* from the left panel.
4.  Set *zHadoopUsername*, *zHadoopPassword* and select https for
    *zHadoopScheme* if you have Basic access authentication configured
    on your Hadoop UI instances (otherwise leave *zHadoopUsername* and
    *zHadoopPassword* blank).
5.  Set *zHadoopNameNodePort* if the Name Node UI instance port differs
    from the default one.
6.  Optionally checkmark *zHBaseAutodiscover* to setup discovering HBase
    on Hadoop data nodes.
7.  Optionally set the device class for discovered HBase device in
    *zHBaseDeviceClass* if it differs from the default one.
8.  Navigate to the *Modeler plugins* page of the device containing your
    Hadoop server, add the *HadoopDataNode* and *HadoopServiceNode*
    modeler plugins.
9.  Select *Model device* from the gear menu.

------------------------------------------------------------------------

Alternatively you can use zenbatchload to add Hadoop monitoring servers
from the command line. To do this, you must create a text file with
hostname, username and password of all the servers you want to add. The
devices should be added under the target machine device class (e.g.
'/Devices/Server/Linux' in the example below).

    /Devices/Server/Linux <HOST NAME or IP>
    zCollectorPlugins=['HadoopDataNode', 'HadoopServiceNode'], zHadoopNameNodePort='50070' zHadoopPassword='', zHadoopUsername='', zHadoopScheme='<http(s)>'

You can then load the Hadoop monitoring servers into Zenoss Core or
Resource Manager as devices with the following command.

    $ zenbatchload <filename>

## Prerequisites

This ZenPack uses the NameNode WebUI port for Hadoop modeling and
performance monitoring, therefore please make sure that the UI instance
is running. For more information refer to [HDFS Ports](http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.2.0/bk_reference/content/reference_chap2_1.html){.external-link}.

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

-   HadoopDataNode
-   HadoopServiceNode

<dl markdown="1">
<dt markdown="1">
Monitoring Templates
</dt>
</dl>

-   Hadoop (in /Device)
-   HadoopDataNode (in /Device)
-   HadoopSecondaryNameNode (in /Device)
-   HadoopJobTracker (in /Device)
-   HadoopTaskTracker (in /Device)
-   HadoopResourceManager (in /Device)
-   HadoopNodeManager (in /Device)
-   HadoopJobHistory (in /Device)
-   HBaseDiscoverMonitor (in /Device)

<dl markdown="1">
<dt markdown="1">
Component Types
</dt>
</dl>

-   HadoopDataNode (on related device)
-   HadoopSecondaryNameNode (on related device)
-   HadoopJobTracker (on related device)
-   HadoopTaskTracker (on related device)
-   HadoopResourceManager (on related device)
-   HadoopNodeManager (on related device)
-   HadoopJobHistory (on related device)

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
-   [Hadoop_Data_Nodes.png](img/zenpack-hadoop_data_nodes.png)
-   [Hadoop_Device_Graphs.png](img/zenpack-hadoop_device_graphs.png)
-   [Hadoop_Impact.png](img/zenpack-hadoop_impact.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [External_Impact_Relationships.png](img/zenpack-external_impact_relationships.png)
-   [Hadoop_Data_Nodes.png](img/zenpack-hadoop_data_nodes.png)
-   [Hadoop_Device_Graphs.png](img/zenpack-hadoop_device_graphs.png)
-   [Hadoop_Impact.png](img/zenpack-hadoop_impact.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [External_Impact_Relationships.png](img/zenpack-external_impact_relationships.png)
-   [Hadoop_Data_Nodes.png](img/zenpack-hadoop_data_nodes.png)
-   [Hadoop_Device_Graphs.png](img/zenpack-hadoop_device_graphs.png)
-   [Hadoop_Impact.png](img/zenpack-hadoop_impact.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [External_Impact_Relationships.png](img/zenpack-external_impact_relationships.png)
-   [Hadoop_Data_Nodes.png](img/zenpack-hadoop_data_nodes.png)
-   [Hadoop_Device_Graphs.png](img/zenpack-hadoop_device_graphs.png)
-   [Hadoop_Impact.png](img/zenpack-hadoop_impact.png)


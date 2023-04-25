# ZooKeeper

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

ZenPacks.zenoss.ZooKeeper

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.ZooKeeper){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.ZooKeeper.git){.external-link}

### Applications Monitored:

Apache ZooKeeper

## ZooKeeper ZenPack

Monitoring of Apache ZooKeeper nodes and clusters.

## Contents

[1 ZooKeeper ZenPack](#zookeeper-zenpack)

[1.1 Support](#support)

[1.2 Releases](#releases)

[1.3 Background](#background)

[1.4 Features](#features)

[1.4.1 Discovery](#discovery)

[1.4.2 Performance Monitoring](#performance-monitoring)

[1.4.3 Event monitoring](#event-monitoring)

[1.4.4 Service Impact](#service-impact)

[1.5 Usage](#usage)

[1.6 Troubleshooting](#troubleshooting)

[1.7 Installed Items](#installed-items)

[1.8 Daemons](#daemons)

[1.9 Changes](#changes)

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 1.0.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.ZooKeeper/1.0.0/ZenPacks.zenoss.ZooKeeper-1.0.0.egg){.external-link}:   Released on 2014/09/05:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Resource Manager 4.2.x

## Background

The ZenPacks.zenoss.ZooKeeper ZenPack monitors Apache ZooKeeper server
via Twisted client TCP connection.

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Discovery and periodic remodeling of ZooKeeper component.
-   Performance monitoring.
-   Event monitoring.
-   Optional service impact with addition of Zenoss Service Dynamics
    product.

### Discovery

The following component will be automatically discovered through the
ZooKeeper port you provide:

ZooKeeper:   *Attributes*: Name, Mode, Status, Node Count, ZooKeeper Version,
    Zxid

### Performance Monitoring

The following metrics will be collected and graphed every 5 minutes by
default:

ZooKeeper:   *Metrics*: Outstanding Requests, Received/Sent Packets, Connections,
    Avg/Min/Max Latencies

### Event monitoring

The following events will be triggered:

ZooKeeper:   *Error*: Incorrect port supplied or connection refused.

### Service Impact

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact capability for ZooKeeper. The following
service impact relationships are automatically added. These will be
included in any services containing one or more of the explicitly
mentioned entities.

<dl markdown="1">
<dt markdown="1">
Service Impact Relationships
</dt>
</dl>

-   ZooKeeper is affected by hosting Device failure.

<dl markdown="1">
<dt markdown="1">
External Impact Relationships
</dt>
</dl>

-   ZooKeeper failure affects associated Hadoop Data Node, Secondary
    Name Node, Job Tracker, Task Tracker, Resource Manager, Node Manager
    and Job History.

## Usage

Use the following steps to start monitoring ZooKeeper server:

1.  Select *Infrastructure* from the navigation bar.
2.  Click the device name in the device list. The device overview page
    appears.
3.  Select *Configuration Properties* from the left panel.
4.  Set *zZooKeeperPort* if ZooKeeper port differs from the default one
    (2181).
5.  Navigate to the *Modeler plugins* page of the device containing your
    ZooKeeper server and add the *ZooKeeperCollector* modeler plugin.
6.  Select *Model device* from the gear menu.

------------------------------------------------------------------------

Alternatively you can use zenbatchload to add ZooKeeper monitoring
servers from the command line. To do this, you must create a text file
with hostname and ZooKeeper port of all the servers you want to add. The
devices should be added under the target machine device class (e.g.
'/Devices/Server/Linux' in the example below).

    /Devices/Server/Linux zCollectorPlugins=['ZooKeeperCollector']
    <HOST NAME> zZooKeeperPort='2181'

You can then load the ZooKeeper monitoring servers into Zenoss Core or
Resource Manager as devices with the following command.

    $ zenbatchload <filename>

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

-   ZooKeeperCollector

<dl markdown="1">
<dt markdown="1">
Monitoring Templates
</dt>
</dl>

-   ZooKeeper (in /Device)

<dl markdown="1">
<dt markdown="1">
Component Types
</dt>
</dl>

-   ZooKeeper (on related device)

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
-   [ZooKeeper_Graphs.png](img/zenpack-zookeeper_graphs.png)
-   [ZooKeeper_Impact.png](img/zenpack-zookeeper_impact.png)
-   [ZooKeeper.png](img/zenpack-zookeeper.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [External_Impact_Relationships.png](img/zenpack-external_impact_relationships.png)
-   [ZooKeeper_Graphs.png](img/zenpack-zookeeper_graphs.png)
-   [ZooKeeper_Impact.png](img/zenpack-zookeeper_impact.png)
-   [ZooKeeper.png](img/zenpack-zookeeper.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [External_Impact_Relationships.png](img/zenpack-external_impact_relationships.png)
-   [ZooKeeper_Graphs.png](img/zenpack-zookeeper_graphs.png)
-   [ZooKeeper_Impact.png](img/zenpack-zookeeper_impact.png)
-   [ZooKeeper.png](img/zenpack-zookeeper.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [External_Impact_Relationships.png](img/zenpack-external_impact_relationships.png)
-   [ZooKeeper_Graphs.png](img/zenpack-zookeeper_graphs.png)
-   [ZooKeeper_Impact.png](img/zenpack-zookeeper_impact.png)
-   [ZooKeeper.png](img/zenpack-zookeeper.png)


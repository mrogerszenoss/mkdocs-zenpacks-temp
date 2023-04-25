# OpenStack Object Storage (Swift)

@lb[](img/zenpack-openstack-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.zenoss.OpenStackSwift

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.OpenStackSwift.git){.external-link}

### Applications Monitored:

OpenStack Swift

## OpenStack Object Storage (Swift) ZenPack

Monitoring for Swift, OpenStack's object server software.

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 0.7.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.OpenStackSwift/0.7.0/ZenPacks.zenoss.OpenStackSwift-0.7.0.egg){.external-link}:   **Summary of changes:** First release.
:   Released on 2013/01/03:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.1.x, Zenoss Core
    3.2.x, Zenoss Core 4.2.x, Zenoss Resource Manager 4.1.x, Zenoss
    Resource Manager 4.2.x

## Background

This ZenPack allows for monitoring of Swift. Swift is the project name
for the Object Store in OpenStack.

From the [Swift project site](http://docs.openstack.org/developer/swift/){.external-link}:

       Swift is a highly available, distributed, eventually consistent object/blob store. Organizations can use Swift to store lots of data efficiently, safely, and cheaply.

## Requirements & Dependencies

All monitoring is performed through the optional swift-recon API
endpoint that can be enabled on all of your Swift object servers. Before
using this ZenPack you must install and configure swift-recon on your
Swift object servers.

## Usage

Installing the ZenPack will add the following objects to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Configuration Properties
</dt>
</dl>

-   zSwiftObjectServerPort: Listening port of swift-object-server.
    Defaults to 6000.

<dl markdown="1">
<dt markdown="1">
Monitoring Templates
</dt>
</dl>

-   SwiftObjectServer in /Devices

<dl markdown="1">
<dt markdown="1">
Process Classes
</dt>
</dl>

-   OpenStack/Swift
    -   swift-account-auditor
    -   swift-account-reaper
    -   swift-account-replicator
    -   swift-account-server
    -   swift-container-auditor
    -   swift-container-replicator
    -   swift-container-server
    -   swift-container-sync
    -   swift-container-updater
    -   swift-object-auditor
    -   swift-object-replicator
    -   swift-object-server
    -   swift-object-updater
    -   swift-proxy-server

<dl markdown="1">
<dt markdown="1">
Event Classes
</dt>
</dl>

-   /Status/Swift
-   /Perf/Swift

The zSwiftObjectServerPort property is used by the SwiftObjectServer
monitoring template to control what port it will attempt to find the
recon API on. Normally the default of 6000/tcp will work unless you've
chosen a different port for your swift-object-server process.

By default the SwiftObjectServer monitoring template will not be bound
to any devices. To make use of it you will need to either bind it
directly to your Swift object server devices, or put your object servers
into their own device class and bind the template to that device class.
Typically this will be under either /Server/Linux or /Server/SSH/Linux
so you get normal operating system monitoring in addition to the
Swift-specific monitoring.

### Swift Metrics

Assuming you have swift-recon and Zenoss setup properly you can expect
to see the following extra graphs on your Swift object servers.

Swift Object Server - Async Pending:   Trend of asynchronous pending tasks. When a Swift proxy server
    updates an object it attempts to synchronously update the object's
    container with the new object information. There is a three second
    timeout on this task and if it can't be completed in that time, it
    will be put into an asynchronous pending bucket to be executed
    later. By trending and thresholding on how many tasks are pending
    you can get an early read on cluster performance problems. By
    default a maximum threshold of 10 is set on this metric and will
    raise a warning severity event in the /Perf/Swift event class when
    it is breached.

<!-- -->

Swift Object Server - Disks:   Trend of total and unmounted disks on the storage node. Swift's
    mechanism for detecting failing or failed drives and taking them
    offline is to unmount them. By proactively monitoring for unmounted
    disks and replacing them you can keep your cluster healthy. By
    default a maximum threshold of 0 is set on unmounted disks and will
    raise a warning severity event in the /Status/Swift event class.

<!-- -->

Swift Object Server - Quarantine:   Trend of accounts, containers and objects that have been
    quarantined. Swift has an auditor process that will find corrupt
    items and move them into a quarantine area so good objects will be
    replicated back into their place.
:   Sudden increases in quarantined items can indicate hardware problems
    on storage nodes. Additionally quarantine is not automatically
    pruned and can result in some storage nodes filling up their disk at
    a faster rate than others and running out of space. By default a
    maximum threshold of 100 is set individually on quarantined
    accounts, containers and objects. A warning event will be raised in
    the /Status/Swift event class if it is breached.

<!-- -->

Swift Object Server - Replication Time:   Trend of replication time. Swift has a replicator process that
    cycles continually. If a single replication cycle takes more than 30
    minutes it can reduce the resiliency of the cluster. By default a
    maximum threshold of 30 minutes is set on replication time and will
    raise a warning severity event in the /Perf/Swift event class when
    breached.

<!-- -->

Swift Object Server - Load Averages:   Trend of 1, 5 and 15 minute operating system load average.
    Additionally the 15 minute load average divided by total disks is
    calculated. A perfectly efficient storage node will run at a load
    average of 1.0 per disk. By default a maximum treshold of 2.0 is set
    on 15 minute load average divided by total disks and will raise a
    warning severity event in the /Perf/Swift event class when breached.

<!-- -->

Swift Object Server - Process Churn:   Trend of processes created per second. High process churn can
    indicate a broken process being unnecessarily restarted. By default
    a maximum treshold of 100 processes per second is set and will raise
    a warning severity event in the /Perf/Swift event class when
    breached.

<!-- -->

Swift Object Server - Disk Usages:   Trend of maximum, average and minimum disk usage for all disks in
    the storage node. These are the primary storage capacity metrics
    within a cluster. Depending on the size of each individual disk,
    weights and the skew of store object sizes, an entire cluster can
    exceed capacity if a single disk runs out of capacity. By default a
    maximum threshold is set on the maximum usage metric. It will raise
    a warning severity in the /Status/Swift event class when breached.

<!-- -->

Swift Object Server - Disk Sizes:   Trend of maximum, average and minimum disk sizes for all disks in
    the storage node. Ideally all disks in a storage node will be the
    same size unless weights are closely managed. No default thresholds
    are set on these metrics.

<!-- -->

Swift Object Server - Processes:   Trend of total and running processes. No default thresholds are set
    on these metrics.

### Process Monitoring

All Swift processes will be discovered and monitored based on the
process classes listed above. If one of the processes is found to not be
running on a node where it should be, an error severity event will be
raised in the /Status/OSProcess event class.

Each of the individual Swift process will also be monitored for its CPU
and memory utilization.

## What's Next

While this ZenPack currently has wide coverage of metrics that are
important to the successful operation of a Swift cluster, there are more
opportunities. The following is a list of metrics that are not currently
monitored, but would be useful.

-   Dispersion Report Results
-   Ring consistency between all object, container and account servers.

## Attachments:

-   [openstack-zenpack.png](img/zenpack-openstack-zenpack.png)
-   [Swift_aggregate1.png](img/zenpack-swift_aggregate1.png)
-   [Swift_aggregate2.png](img/zenpack-swift_aggregate2.png)
-   [Swift_async_pending.png](img/zenpack-swift_async_pending.png)
-   [Swift_disk_sizes.png](img/zenpack-swift_disk_sizes.png)
-   [Swift_disk_usages.png](img/zenpack-swift_disk_usages.png)
-   [Swift_disks.png](img/zenpack-swift_disks.png)
-   [Swift_load_averages.png](img/zenpack-swift_load_averages.png)
-   [Swift_osprocesses.png](img/zenpack-swift_osprocesses.png)
-   [Swift_process_churn.png](img/zenpack-swift_process_churn.png)
-   [Swift_processes.png](img/zenpack-swift_processes.png)
-   [Swift_quarantine.png](img/zenpack-swift_quarantine.png)
-   [openstack-zenpack.png](img/zenpack-openstack-zenpack.png)
-   [Swift_aggregate1.png](img/zenpack-swift_aggregate1.png)
-   [Swift_aggregate2.png](img/zenpack-swift_aggregate2.png)
-   [Swift_async_pending.png](img/zenpack-swift_async_pending.png)
-   [Swift_disk_sizes.png](img/zenpack-swift_disk_sizes.png)
-   [Swift_disk_usages.png](img/zenpack-swift_disk_usages.png)
-   [Swift_disks.png](img/zenpack-swift_disks.png)
-   [Swift_load_averages.png](img/zenpack-swift_load_averages.png)
-   [Swift_osprocesses.png](img/zenpack-swift_osprocesses.png)
-   [Swift_process_churn.png](img/zenpack-swift_process_churn.png)
-   [Swift_processes.png](img/zenpack-swift_processes.png)
-   [Swift_quarantine.png](img/zenpack-swift_quarantine.png)
-   [openstack-zenpack.png](img/zenpack-openstack-zenpack.png)
-   [Swift_aggregate1.png](img/zenpack-swift_aggregate1.png)
-   [Swift_aggregate2.png](img/zenpack-swift_aggregate2.png)
-   [Swift_async_pending.png](img/zenpack-swift_async_pending.png)
-   [Swift_disk_sizes.png](img/zenpack-swift_disk_sizes.png)
-   [Swift_disk_usages.png](img/zenpack-swift_disk_usages.png)
-   [Swift_disks.png](img/zenpack-swift_disks.png)
-   [Swift_load_averages.png](img/zenpack-swift_load_averages.png)
-   [Swift_osprocesses.png](img/zenpack-swift_osprocesses.png)
-   [Swift_process_churn.png](img/zenpack-swift_process_churn.png)
-   [Swift_processes.png](img/zenpack-swift_processes.png)
-   [Swift_quarantine.png](img/zenpack-swift_quarantine.png)
-   [openstack-zenpack.png](img/zenpack-openstack-zenpack.png)
-   [Swift_aggregate1.png](img/zenpack-swift_aggregate1.png)
-   [Swift_aggregate2.png](img/zenpack-swift_aggregate2.png)
-   [Swift_async_pending.png](img/zenpack-swift_async_pending.png)
-   [Swift_disk_sizes.png](img/zenpack-swift_disk_sizes.png)
-   [Swift_disk_usages.png](img/zenpack-swift_disk_usages.png)
-   [Swift_disks.png](img/zenpack-swift_disks.png)
-   [Swift_load_averages.png](img/zenpack-swift_load_averages.png)
-   [Swift_osprocesses.png](img/zenpack-swift_osprocesses.png)
-   [Swift_process_churn.png](img/zenpack-swift_process_churn.png)
-   [Swift_processes.png](img/zenpack-swift_processes.png)
-   [Swift_quarantine.png](img/zenpack-swift_quarantine.png)


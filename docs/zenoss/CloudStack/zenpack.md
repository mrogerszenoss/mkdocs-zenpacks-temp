# CloudStack

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

ZenPacks.zenoss.CloudStack

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.CloudStack){.external-link}

### Link To More Docs:

[View Documentation](https://github.com/zenoss/ZenPacks.zenoss.CloudStack#readme){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.CloudStack.git){.external-link}

### Applications Monitored:

Apache CloudStack (2, 3, 4)

Citrix CloudPlatform (3)

## CloudStack ZenPack

Monitor CloudStack

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 1.2.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.CloudStack/1.2.0/ZenPacks.zenoss.CloudStack-1.2.0.egg){.external-link}:   Released on 2016/01/25:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss
    Resource Manager 4.2.x, Zenoss Resource Manager 5.0.x

<!-- -->

Version 1.1.3- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.CloudStack/1.1.3/ZenPacks.zenoss.CloudStack-1.1.3.egg){.external-link}:   Released on 2015/03/05:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss
    Resource Manager 4.2.x, Zenoss Resource Manager 5.0.x

<!-- -->

Version 1.0.9- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.CloudStack/1.0.9/ZenPacks.zenoss.CloudStack-1.0.9.egg){.external-link}:   Released on 2013/04/24:   Compatible with Zenoss Core 3.2.x, Zenoss Core 4.2.x, Zenoss
    Resource Manager 4.1.x, Zenoss Resource Manager 4.2.x

## Background

Monitoring for [Apache CloudStack](http://incubator.apache.org/cloudstack/){.external-link} and
by extension, [Citrix CloudPlatform](http://www.citrix.com/products/cloudplatform/overview.html){.external-link}.

The easiest way to start monitoring CloudStack is to navigate to the
Infrastructure page, click the \*+\* menu to add a device and choose
*Add CloudStack*. Fill out the *Device to Create*, *URL*, *API Key*, and
*Secret Key* fields, select a collector, then click *OK*. The URL should
only include the protocol, host and port (i.e.
*<http://cloudstack.example.com/>*). You can find or create the keys by
logging into the CloudStack web interface and navigate to Accounts and
users.

Zenoss will then add the CloudStack device to the system. For root
administrator users, the associated zones, pods, clusters, hosts,
routers, system VMs and VMs will also be added; zones, routers and VMs
for domain administrator users; zones and VMs for all non administrator
users. Monitoring will also start after the discovery is complete.

## Upgrade Notes

If you are upgrading from a version earlier than 1.1.3 you will need to
perform the following manual steps after upgrading to fix the collection
of network throughput metrics. These steps must be performed on any
Zenoss collector server monitoring CloudStack. These steps will remove
all historical performance data collected for network throughput, but
that matters less because the historical data is completely wrong. If
you do not perform these steps, the network data collected after
upgrading will continue to be wrong.

**Note:** These steps are only necessary on Zenoss versions earlier than
5.0.

    su - zenoss
    cd $ZENHOME/perf/Devices
    find. -name cloudstack_network\*.rrd -delete

## Metrics

Once you've successfully added a CloudStack cloud to Zenoss you will
begin to see the following metrics available for the entire cloud to
root administrator users. These numbers are aggregated from all zones,
pods, clusters and hosts.

-   Memory, CPU, Private Storage: Allocation
-   Public IPs: Total and Used
-   Private IPs: Total and Used
-   Memory: Total (with and without over-provisioning), Allocated and
    Used
-   CPU: Total (with and without over-provisioning), Allocated and Used
-   Primary Storage: Total (with and without over-provisioning),
    Allocated and Used
-   Secondary Storage: Total and Used
-   Network: Read and Write

The same list of metrics are available for each zone to root
administrator users. The same metrics with the exception of public IPs
and secondary storage are also available for each pod.

The following metrics are available aggregated to each cluster, and for
each host.

-   Memory: Total, Used and Allocated
-   CPU: Total (with and without over-provisioning), Allocated, Used and
    Cores
-   Network: Read and Write

The following list of metrics for VMs is available to non root
administrator users.

-   CPU: Cores, Total, Used and Used Percent
-   Network: Read and Write

## Events

CloudStack has both alerts and events. Once you've successfully added a
CloudStack cloud to Zenoss you will automatically receive all CloudStack
alerts as events in Zenoss. You will also automatically receive all
CloudStack events. However, the events will go straight into your event
history by default.

To avoid overloading CloudStack and Zenoss, only the last one (1) hour
of events will be checked. This allows for timezone discrepancy between
the Zenoss and CloudStack servers as well as some downtime without
missing events. There is no real-time event collection mechanism with
the CloudStack API, so alerts and events will only be polled once per
minute.

## Installed Items

Installing the ZenPack will add the following items to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Device Classes
</dt>
</dl>

-   /CloudStack

<dl markdown="1">
<dt markdown="1">
Configuration Properties
</dt>
</dl>

-   zCloudStackURL
-   zCloudStackAPIKey
-   zCloudStackSecretKey

<dl markdown="1">
<dt markdown="1">
Modeler Plugins
</dt>
</dl>

-   zenoss.CloudStack

<dl markdown="1">
<dt markdown="1">
Monitoring Templates
</dt>
</dl>

-   CloudStackCloud
-   CloudStackZone
-   CloudStackPod
-   CloudStackCluster
-   CloudStackHost
-   CloudStackVirtualMachine
-   CloudStackConsoleProxy
-   CloudStackFileTouch (If hypervisor type is KVM)

<dl markdown="1">
<dt markdown="1">
Event Classes
</dt>
</dl>

-   /Status/CloudStack
-   /Perf/CloudStack
-   /App/CloudStack

## Changes

<dl markdown="1">
<dt markdown="1">
1.2.0
</dt>
</dl>

-   Hide API secret key (ZEN-21404)
-   Migration script (ZEN-21675)
-   Allow CloudStack devices to be created for domain administrator
    users, non-administrator users, in addition to root administrator
    users.

<dl markdown="1">
<dt markdown="1">
1.1.3
</dt>
</dl>

-   Fix monitoring of network throughput metrics. (ZEN-16956)

<dl markdown="1">
<dt markdown="1">
1.1.2
</dt>
</dl>

-   Fix conflict with SolarisMonitor 2.2.0.

## Attachments:

-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)


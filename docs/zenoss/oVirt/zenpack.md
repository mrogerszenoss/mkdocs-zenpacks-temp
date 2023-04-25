# oVirt

@lb[](img/zenpack-ovirt-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.zenoss.oVirt

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.oVirt.git){.external-link}

### Applications Monitored:

OVirt (3.0, 3.1, 3.2)

Red Hat Enterprise Virtualization (RHEV / RHEV-M) (3.0, 3.1, 3.2)

## OVirt ZenPack

Monitoring for oVirt and Red Hat Enterprise Virtualization (RHEV)

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 1.2.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.oVirt/1.2.1/ZenPacks.zenoss.oVirt-1.2.1.egg){.external-link}:   Released on 2016/01/20:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Resource Manager 4.1.x,
    Zenoss Resource Manager 4.2.x

## Background

This ZenPack provides the ability to monitor oVirt and by extension, Red
Hat Enterprise Virtualization (RHEV). An explanation of what oVirt is
can be found on the [oVirt](http://www.ovirt.org/){.external-link} and
[Red Hat Enterprise Virtualization](http://www.redhat.com/products/virtualization/){.external-link}
sites.

> The oVirt Project is an open virtualization project for anyone who
> cares about Linux-based KVM virtualization. Providing a feature-rich
> server virtualization management system with advanced capabilities for
> hosts and guests, including high availability, live migration, storage
> management, system scheduler, and more. This ZenPack models, collects
> events, and collects performance information from an oVirt server for
> data centers, clusters, hosts and virtual machines.

## Features

### Metrics

Once you've successfully added a ovirt system to Zenoss you will begin
to see the following metrics available.

-   Host CPU, memory, network utilization
-   VM CPU, memory, network, disk utilization and throughput
-   Counts of hosts, VMs residing in the various containers

### Events

oVirt/Rhev has a single event stream containing both events and alerts.
The API does not appear to map an opening event to a closing event. For
this reason automatic closing of events is not yet supported.
Additionally it appears that oVirt may drop events off of its queue very
quickly. We are reading events every minute to reduce the chance of a
missed event since there is no real time event mechanism in oVirt.

## Limitations

This version of the ZenPack only supports HTTP access to the oVirt
server. This version of the ZenPack does not automatically clear events.
The oVirt API seems appears to be limited in regards to events. This
version of the ZenPack does not automatically detect device models in
real time and this can be worked around by manually scheduling
zenmodeler to run via cron on a regular basis.

The oVirt controller node is really a Linux device. It might be
desirable to set the appropriate modeler plugins and templates to add
additional Linux metrics to this organizer. Alternatively, you could use
a CNAME for this device and model the real device under a different
hostname and organizer.

## Configuration

Installing the ZenPack will add the following items to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Device Classes
</dt>
</dl>

-   /oVirt

<dl markdown="1">
<dt markdown="1">
Configuration Properties
</dt>
</dl>

-   zOVirtPassword
-   zOVirtUrl
-   zOVirtDomain
-   zOVirtUser

<dl markdown="1">
<dt markdown="1">
Modeler Plugins
</dt>
</dl>

-   zenoss.oVirt

<dl markdown="1">
<dt markdown="1">
Monitoring Templates
</dt>
</dl>

-   oVirtCluster
-   oVirtDataCenter
-   oVirtHost
-   oVirtHostNic
-   oVirtStorageDomain
-   oVirtSystem
-   oVirtVm
-   oVirtVmDisk
-   oVirtVmNic

<dl markdown="1">
<dt markdown="1">
Event Classes
</dt>
</dl>

-   /oVirt

The above Configuration Properties will be automatically set when adding
a new oVirt instance.

**Note:** If the zOVirtUrl changes it would be recommended to rename the
ovirt device as well.

## Usage

### Add an oVirt Server

1.  Navigate to the *Infrastructure* page
2.  Click on the *Add Device* menu item and select *Add oVirt
    Infrastructure...* option.
3.  Fill in the appropriate fields in the dialog box:
    1.  *URL*: URL of the oVirt instance. (i.e.
        <http://ovirt.example.com:8080>)
    2.  *Authentication Domain*: Domain in which the user credentials
        are valid.
    3.  *Username*: User name.
    4.  *Password*: Password for the user.
    5.  *Collector*: Zenoss collector to which the device will be
        assigned.
4.  Click on the *Add* button.
    1.  Wait for the device to be modeled.
    2.  Navigate to the new device.

### Add an oVirt Server (zenbatchload)

1\. Add an entry like the following to your zenbatchload input file.

    /Devices/oVirt loader='oVirt', loader_arg_keys=['url', 'username', 'domain', 'password']
    ovirt.zenosslabs.com url='http://ovirt.zenosslabs.com', username='admin', domain='internal', password='zenoss'

2\. Run *zenbatchload*.

    zenbatchload inputfile

### Add an oVirt Server (zendmd)

1.  Run the following snippet in *zendmd*.

    ovirt_facade = getFacade('oVirt')
    ovirt_facade.add_ovirt('http://ovirt.example.com','username', 'domain', 'password')
    commit()

## Change Log

<dl markdown="1">
<dt markdown="1">
1.2.1 - 2016-01-20
</dt>
</dl>

-   Licensing fixes. No functional changes.

<dl markdown="1">
<dt markdown="1">
1.2.0 - 2013-04-11
</dt>
</dl>

-   Support for oVirt 3.2.
-   Introduced dependency on PythonCollector ZenPack.
-   Moved from COMMAND datasources to Python datasources for better
    performance.

<dl markdown="1">
<dt markdown="1">
1.1.0 - 2012-08-28
</dt>
</dl>

-   Support for RHEV 3.
-   Discovery of oVirt or RHEV product and version information.
-   RHEV and oVirt Icons for all component types.
-   Fix for "No data returned for command" events.

<dl markdown="1">
<dt markdown="1">
1.0.3 - 2012-08-06
</dt>
</dl>

-   First fully-featured release.
-   No longer dependent on Liberator ZenPack.

<dl markdown="1">
<dt markdown="1">
1.0.1 - 2012-03-21
</dt>
</dl>

-   Initial demonstration release.

## Attachments:

-   [ovirt-zenpack.png](img/zenpack-ovirt-zenpack.png)
-   [ovirt-zenpack.png](img/zenpack-ovirt-zenpack.png)
-   [ovirt-zenpack.png](img/zenpack-ovirt-zenpack.png)
-   [ovirt-zenpack.png](img/zenpack-ovirt-zenpack.png)


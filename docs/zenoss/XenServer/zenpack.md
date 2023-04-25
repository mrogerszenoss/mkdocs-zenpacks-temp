# XenServer

@lb[](img/zenpack-citrix-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.zenoss.XenServer

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.XenServer){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.XenServer.git){.external-link}

### Applications Monitored:

XenServer (6.0, 6.1, 6.2)

Citrix XenServer (6.0, 6.1, 6.2)

## XenServer ZenPack

Monitoring for XenServer pools, hosts and related resources.

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 1.0.7- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.XenServer/1.0.7/ZenPacks.zenoss.XenServer-1.0.7.egg){.external-link}:   Released on 2016/01/20:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss Core
    5.1.x, Zenoss Resource Manager 4.2.x, Zenoss Resource Manager 5.0.x,
    Zenoss Resource Manager 5.1.x, Zenoss Resource Manager 5.x.x

## Background

This ZenPack provides support for monitoring
[XenServer](http://xenserver.org/){.external-link}. Monitoring is
performed using
[XenAPI](http://xenproject.org/developers/teams/xapi.html){.external-link}.

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Initial discovery and continual synchronization of relevant
    components.
-   Performance monitoring.
-   Event management.
-   Service impact and root cause analysis. (Requires Zenoss Service
    Dynamics)

### Discovery

The following components will be automatically discovered through the
XenServer host, username and password you provide. The properties and
relationships will be continually maintained by way consuming events
from the host. By default model changes will be polled every 60 seconds.
This can be configured with the *zXenServerModelInterval* configuration
property.

@lb[](img/zenpack-xenserver_model_yuml.png)

Model Diagram

Pool:   Properties: HA Allow Overcommit, HA Enabled, HA Host Failures to
    Tolerate, CPU ID Feature Mask, HVM Memory Ratio, PV Memory Ratio,
    Description, Label, vSwitch Controller:   Relationships: Master Host, Default Storage Repository, Suspend
    Image Storage Repository, Crash Dump Storage Repository

<!-- -->

Host:   Properties: API Version Major, API Version Minor, API Version
    Vendor, Address, Allowed Operations, Capabilities, CPU Count, CPU
    Speed, Edition, Enabled, Hostname, Is Pool Master, Description,
    Label, Scheduling Policy, Total Memory:   Relationships: Master for Pool, Suspend Image Storage Repository,
    Crash Dump Storage Repository, Local Cache Storage Repository,
    Server Device, Host CPUs, Physical Block Devices, Physical NICs, VMs

<!-- -->

Host CPU (HostCPU):   Properties: Family, Features, Flags, Model, Model Name, Number,
    Speed, Stepping, Vendor:   Relationships: Host

<!-- -->

Physical Block Device (PBD):   Properties: Currently Attached, Device Name, Legacy Mode, Location:   Relationships: Host, Storage Repository, Server Disk

<!-- -->

Physical NIC (PIF):   Properties: DNS Server Address, IPv4 Addresses, IPv6 Addresses, MAC
    Address, MTU, VLAN, Carrier, Currently Attached, Network Device,
    Network Device ID, Network Device Name, Disallow Unplug, IPv4
    Gateway, IPv4 Configuration Mode, IPv6 Configuration Mode, IPv6
    Gateway, Management, IPv4 Netmask, Physical, Primary Address Type,
    Speed, Vendor Name:   Relationships: Host, Network, Server Interface

<!-- -->

Storage Repository (SR):   Properties: Allowed Operations, Content Type, Local Cache Enabled,
    Description, Label, Physical Size, Shared, SM Type, Type:   Relationships: Virtual Disk Images, Physical Block Devices

<!-- -->

Virtual Disk Image (VDI):   Properties: Allow Caching, Allowed Operations, Is a Snapshot,
    Location, Managed, Missing, Description, Label, On Boot, Read Only,
    Sharable, Storage Lock, Type, Virtual Size:   Relationships: Storage Repository, Virtual Block Devices

<!-- -->

Network:   Properties: MTU, Allowed Operations, Bridge, Default Locking Mode,
    Description, Label, IPv4 Begin, IPv4 End, Guest Installer Network,
    Host Internal Management Network, IPv4 Netmask:   Relationships: Physical NICs, Virtual NICs

<!-- -->

vApp (VMAppliance):   Properties: Allowed Operations, Description, Label:   Relationships: VMs

<!-- -->

VM:   Properties: HVM Shadow Multiplier, vCPUs at Startup, Maximum vCPUs,
    Actions After Crash, Actions After Reboot, Actions After Shutdown,
    Allowed Operations, Domain Architecture, Domain ID, HA Always Run,
    HA Restart Priority, Is a Snapshot, Is a Template, Is a Control
    Domain, Is a Snapshot from VMPP, Actual Memory, Description, Label,
    Power State, Shutdown Delay, Start Delay, User Version, Version:   Relationships: Host, vApp, Guest Device, Virtual Block Devices,
    Virtual NICs

<!-- -->

Virtual Block Device (VBD):   Properties: Allowed Operations, Bootable, Currently Attached, Device
    Name, Empty, Mode, Storage Lock, Type, Unpluggable, User Device:   Relationships: VM, Virtual Disk Image, Guest Disk

<!-- -->

Virtual NIC (VIF):   Properties: MAC Address, Autogenerate MAC Address, MTU, Allowed
    Operations, Currently Attached, Device Name, IPv4 Allowed, IPv6
    Allowed, Locking Mode:   Relationships: VM, Network, Guest Interface

### Performance Monitoring

The following metrics will be collected every 5 minutes by default. This
can be configured with the *zXenServerPerfInterval* configuration
property. Any metric that is available either via a XenAPI get_record or
rrd_updates call can be collected by adding a new *XenServer XenAPI* or
*XenServer RRD* datasource to the appropriate monitoring template. Note
that as of XenServer 6.2, all available metrics are collected by
default.

@lb[](img/zenpack-xenserver_pools.png)

Pools

<dl markdown="1">
<dt markdown="1">
Pool
</dt>
</dl>

-   property_haPlanExistsFor: Number of future host failures we have
    managed to find a plan for. Once this reaches zero any future host
    failures will cause the failure of protected VMs. (*number*)
-   property_haHostFailuresToTolerate: Number of host failures to
    tolerate before the Pool is declared to be overcommitted. (*number*)

@lb[](img/zenpack-xenserver_hosts.png)

Hosts

<dl markdown="1">
<dt markdown="1">
Host
</dt>
</dl>

-   property_memoryOverhead: Virtualization memory overhead. (*bytes*)
-   rrd_memoryTotal: Total memory. (*bytes*)
-   rrd_memoryFree: Free memory. (*bytes*)
-   rrd_xapiMemoryUsage: Memory allocated by xapi that is used.
    (*bytes*)
-   rrd_xapiFreeMemory: Memory allocated by xapi that is free. (*bytes*)
-   rrd_xapiLiveMemory: Memory allocated by xapi that is live. (*bytes*)
-   rrd_xapiAllocation: Total memory allocated by xapi. (*bytes*)
-   rrd_pifAggrRX: Total inbound throughput for all host PIFs.
    (*bits/sec*)
-   rrd_pifAggrTX: Total outbound throughput for all host PIFs.
    (*bits/sec*)
-   rrd_cpuAvg: Average CPU utilization for all host CPUs. (*percent*)
-   rrd_loadAvg: Load average. (*processes*)
-   rrd_srCacheHitsSum: Storage repository cache hit rate. (*hits/sec*)
-   rrd_srCacheMissesSum: Storage repository cache miss rate.
    (*misses/sec*)

@lb[](img/zenpack-xenserver_hostcpus.png)

Host CPUs

<dl markdown="1">
<dt markdown="1">
Host CPU (HostCPU)
</dt>
</dl>

-   rrd_cpu: Average CPU utilization. (*percent*)

@lb[](img/zenpack-xenserver_pbds.png)

Physical Block Devices

<dl markdown="1">
<dt markdown="1">
Physical Block Device (PBD)
</dt>
</dl>

-   No metrics available.

@lb[](img/zenpack-xenserver_pifs.png)

Physical NICs

<dl markdown="1">
<dt markdown="1">
Physical NIC (PIF)
</dt>
</dl>

-   metric_speed: Speed of interface. (*bits/sec*)
-   rrd_rx: Inbound throughput. (*bits/sec*)
-   rrd_tx: Outbound throughput. (*bits/sec*)

@lb[](img/zenpack-xenserver_srs.png)

Storage Repositories

<dl markdown="1">
<dt markdown="1">
Storage Repository (SR)
</dt>
</dl>

-   property_physicalSize: Total physical storage size. (*bytes*)
-   property_physicalUtilisation: Used physical storage. (*bytes*)
-   property_virtualAllocation: Allocated physical storage. (*bytes*)

@lb[](img/zenpack-xenserver_vdis.png)

Virtual Disk Images

<dl markdown="1">
<dt markdown="1">
Virtual Disk Image (VDI)
</dt>
</dl>

-   property_physicalUtilisation: Used physical storage. (*bytes*)
-   property_virtualSize: Total virtual storage size. (*bytes*)

@lb[](img/zenpack-xenserver_networks.png)

Networks

<dl markdown="1">
<dt markdown="1">
Network
</dt>
</dl>

-   No metrics available.

@lb[](img/zenpack-xenserver_vapps.png)

vApps

<dl markdown="1">
<dt markdown="1">
vApp (VMAppliance)
</dt>
</dl>

-   No metrics available.

@lb[](img/zenpack-xenserver_vms.png)

VMs

<dl markdown="1">
<dt markdown="1">
VM
</dt>
</dl>

-   property_memoryOverhead: Virtualization memory overhead. (*bytes*)
-   metric_vcpusNumber: Current number of vCPUs. (*number*)
-   metric_memoryActual: Guest's actual memory. (*bytes*)
-   rrd_cpuAvg: Average utilization for all vCPUs. (*percent*)
-   rrd_memory: Memory currently allocated to VM. (*bytes*)
-   rrd_vifRXSum: Total inbound throughput for all VM VIFs. (*bits/sec*)
-   rrd_vifTXSum: Total outbound throughput for all VM VIFs.
    (*bits/sec*)
-   rrd_vbdReadSum: Total read rate for all VM VBDs. (*bytes/sec*)
-   rrd_vbdWriteSum: Total write rate for all VM VBDs. (*bytes/sec*)
-   rrd_memoryInternalFree: Memory used as reported by the guest agent.
    (*bytes*)
-   rrd_memoryTarget: Target of VM balloon driver. (*bytes*)

@lb[](img/zenpack-xenserver_vbds.png)

Virtual Block Devices

<dl markdown="1">
<dt markdown="1">
Virtual Block Device (VBD)
</dt>
</dl>

-   rrd_read: Read rate. (*bytes/sec*)
-   rrd_write: Write rate. (*bytes/sec*)

@lb[](img/zenpack-xenserver_vifs.png)

Virtual NICs

<dl markdown="1">
<dt markdown="1">
Virtual NIC (VIF)
</dt>
</dl>

-   rrd_rx: Inbound throughput. (*bits/sec*)
-   rrd_tx: Outbound throughput. (*bits/sec*)

### Event Management

Zenoss watches for XenAPI *messages* and creates Zenoss events when they
occur. XenAPI messages are the system alerts you see in XenCenter. By
default, Zenoss will poll for new messages every 60 seconds. This can be
configured with the *zXenServerEventsInterval* configuration property.

@lb[](img/zenpack-xenserver_events.png)

Events

The created Zenoss events will have the following fields set.

<dl markdown="1">
<dt markdown="1">
Standard Zenoss Event Fields
</dt>
</dl>

-   device: Set to the XenServer endpoint device in the /XenServer
    device class.
-   component: Looked up in from Zenoss components using the message's
    *obj_uuid* value.
-   summary: In preference order: message's body field then name field
    then "no body or name provided".
-   severity: Mapped from message's priority field using the map below.
-   eventKey: Message's uuid value.
-   eventClassKey: Literally "XenServerMessage".

<dl markdown="1">
<dt markdown="1">
Additional Event Fields
</dt>
</dl>

-   xenserver_name: Message's name value.
-   xenserver_cls: Message's cls value.

<dl markdown="1">
<dt markdown="1">
XenAPI Message Priority to Zenoss Event Severity Mapping
</dt>
</dl>

-   Priority 1: Critical
-   Priority 2: Error
-   Priority 3: Warning
-   Priority 4: Clear
-   Priority 5: Info

### Service Impact and Root Cause Analysis

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact and root cause analysis capabilities for
services running on XenServer. The service impact relationships shown in
the diagram and described below are automatically added. These will be
included in any services that contain one or more of the explicitly
mentioned components.

@lb[](img/zenpack-xenserver_impact_yuml.png)

Impact Relationship Diagram

<dl markdown="1">
<dt markdown="1">
Internal Impact Relationships
</dt>
</dl>

-   XenAPI (endpoint) access failure impacts all hosts.
-   Host failure impacts the host's pool and any resident VMs.
-   Network failure impacts all related virtual NICs.
-   Physical block device failure impacts its host and storage
    repository.
-   Physical NIC failure impacts its host and network.
-   Pool failure impacts any contained VMs.
-   Storage repository failure impacts any pools and hosts for which it
    is a default, suspend image, crash dump or local cache repository.
-   Virtual block device failure impacts its VM.
-   Virtual disk image failure impacts any related virtual block
    devices.
-   Virtual NIC failure impacts its VM.
-   VM failure impacts its vApp.

@lb[](img/zenpack-xenserver_impact.png)

XenServer Hosted VM in a Service

<dl markdown="1">
<dt markdown="1">
External Impact Relationships
</dt>
</dl>

-   Underlying server failure impacts the associated XenServer host.
-   Underlying server disk failure impacts the associated XenServer
    physical block device.
-   Underlying server interface failure impacts the associated XenServer
    physical NIC.
-   XenServer VM failure impacts the associated guest device.
-   XenServer virtual block device failure impacts the associated guest
    hard disk.
-   XenServer virtual NIC failure impacts the associated guest
    interface.
-   XenServer host failure impacts the associated CloudStack host.
-   XenServer VM failure impacts the associated CloudStack router VM,
    system VM or regular VM.

## Usage

### Adding XenServer Endpoint

Use the following steps to start monitoring XenServer using the Zenoss
web interface.

1.  Navigate to the Infrastructure page.

    @lb[](img/zenpack-xenserver_add_menu.png)

    Add Menu Item

2.  Choose *Add XenServer Endpoint* from the add device button.
3.  Fill out the form.

    @lb[](img/zenpack-xenserver_add_dialog.png)

    Add Dialog

    -   *Name* can be anything you want.
    -   *Address* must be resolvable and accessible from the collector
        server chosen in the *Collector* field.
    -   *Username* and *Password* are the same as what you'd use in
        XenCenter.
4.  Click *ADD*.

------------------------------------------------------------------------

Alternatively you can use zenbatchload to add XenServer endpoints from
the command line. To do this, you must create a file with contents
similar to the following. Replace all values in angle brackets with your
values minus the brackets. Multiple endpoints can be added under the
same */Devices/XenServer* section.

    /Devices/XenServer loader='XenServer', loader_arg_keys=['name', 'address', 'username', 'password', 'collector']
    my-xenserver-pool name='my-xenserver-pool', address='<address>', username='<username>', password='<password>', collector='localhost'

You can then load the endpoint(s) with the following command.

    zenbatchload <filename>

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Configuration Properties
</dt>
</dl>

-   zXenServerAddresses
-   zXenServerUsername
-   zXenServerPassword
-   zXenServerPerfInterval: Metric collection interval in seconds.
    Default is 300.
-   zXenServerModelInterval: Model update interval in seconds. Default
    is 60.
-   zXenServerEventsInterval: Events collection interval in seconds.
    Default is 60.

<dl markdown="1">
<dt markdown="1">
Device Classes
</dt>
</dl>

-   /XenServer

<dl markdown="1">
<dt markdown="1">
Modeler Plugins
</dt>
</dl>

-   zenoss.XenServer

<dl markdown="1">
<dt markdown="1">
Datasource Types
</dt>
</dl>

-   XenServer XenAPI
-   XenServer RRD

<dl markdown="1">
<dt markdown="1">
Monitoring Templates (all in /XenServer)
</dt>
</dl>

-   Endpoint
-   Host
-   HostCPU
-   Network
-   PBD
-   PIF
-   Pool
-   SR
-   VBD
-   VDI
-   VIF
-   VM
-   VMAppliance
-   VMGuest

<dl markdown="1">
<dt markdown="1">
Event Classes
</dt>
</dl>

-   /XenServer

<dl markdown="1">
<dt markdown="1">
Event Class Mappings
</dt>
</dl>

-   XenServerCollectionError (in /Status)
-   XenServerCollectionSuccess (in /Status)
-   XenServerMessage (in /XenServer)

## Zenoss Analytics

This ZenPack provides additional support for Zenoss Analytics. Perform
the following steps to install extra reporting resources into Zenoss
Analytics after installing the ZenPack.

1.  Copy analytics-bundle.zip from
    $ZENHOME/ZenPacks/ZenPacks.zenoss.XenServer/analytics/ on your
    Zenoss server.
2.  Navigate to Zenoss Analytics in your browser.
3.  Login as superuser.
4.  Remove any existing *XenServer ZenPack* folder.
    1.  Choose *Repository* from the *View* menu at the top of the page.
    2.  Expand *Public* in the list of folders.
    3.  Right-click on *XenServer ZenPack* folder and choose *Delete*.
    4.  Confirm deletion by clicking *OK*.
5.  Add the new *XenServer ZenPack* folder.
    1.  Choose *Server Settings* from the *Manage' menu at the top of
        the page.*
    2.  Choose *Import* in the left page.
    3.  Remove checks from all check boxes.
    4.  Click *Choose File* to import a data file.
    5.  Choose the analytics-bundle.zip file copied from your Zenoss
        server.
    6.  Click *Import*.

You can now navigate back to the *XenServer ZenPack* folder in the
repository to see the following resources added by the bundle.

<dl markdown="1">
<dt markdown="1">
Domains
</dt>
</dl>

-   XenServer Domain

Domains can be used to create ad hoc views using the following steps.

1.  Choose *Ad Hoc View* from the *Create* menu.
2.  Click *Domains* at the top of the data chooser dialog.
3.  Expand *Public* then *XenServer ZenPack*.
4.  Choose the *XenServer Domain* domain.

## Changes

<dl markdown="1">
<dt markdown="1">
1.0.7
</dt>
</dl>

-   Licensing fixes. No functional changes.

<dl markdown="1">
<dt markdown="1">
1.0.6
</dt>
</dl>

-   Remove CPU count graph and datapoint

<dl markdown="1">
<dt markdown="1">
1.0.5
</dt>
</dl>

-   Add Analytics support.
-   Add Zenoss 5 support.

<dl markdown="1">
<dt markdown="1">
1.0.4
</dt>
</dl>

-   Fix "argument of type 'NoneType' is not iterable" errors.
    (ZEN-14856)
-   Fix potential for failing to remove storage repositories.

<dl markdown="1">
<dt markdown="1">
1.0.3
</dt>
</dl>

-   Fix issue where VBDs impact all VMs. (ZEN-13467)

<dl markdown="1">
<dt markdown="1">
1.0.2
</dt>
</dl>

-   Fix "'XenServer' object has no attribute 'device'" modeling error.
    (ZEN-12978)

<dl markdown="1">
<dt markdown="1">
1.0.1
</dt>
</dl>

-   Clear Zenoss events when messages are dismissed in XenCenter.
    (ZEN-11101)
-   Prevent sending of duplicate events. (ZEN-11100)
-   Tweak message priority to event severity mapping.
-   Fix timezone handling on message timestamps.
-   Add invalidation filtering to improve performance.

<dl markdown="1">
<dt markdown="1">
1.0.0
</dt>
</dl>

-   Initial release.

## Attachments:

-   [citrix-zenpack.png](img/zenpack-citrix-zenpack.png)
-   [Xenserver_add_dialog.png](img/zenpack-xenserver_add_dialog.png)
-   [Xenserver_add_menu.png](img/zenpack-xenserver_add_menu.png)
-   [Xenserver_events.png](img/zenpack-xenserver_events.png)
-   [Xenserver_hostcpus.png](img/zenpack-xenserver_hostcpus.png)
-   [Xenserver_hosts.png](img/zenpack-xenserver_hosts.png)
-   [Xenserver_impact_yuml.png](img/zenpack-xenserver_impact_yuml.png)
-   [Xenserver_impact.png](img/zenpack-xenserver_impact.png)
-   [Xenserver_model_yuml.png](img/zenpack-xenserver_model_yuml.png)
-   [Xenserver_networks.png](img/zenpack-xenserver_networks.png)
-   [Xenserver_pbds.png](img/zenpack-xenserver_pbds.png)
-   [Xenserver_pifs.png](img/zenpack-xenserver_pifs.png)
-   [Xenserver_pools.png](img/zenpack-xenserver_pools.png)
-   [Xenserver_srs.png](img/zenpack-xenserver_srs.png)
-   [Xenserver_vifs.png](img/zenpack-xenserver_vifs.png)
-   [Xenserver_vbds.png](img/zenpack-xenserver_vbds.png)
-   [Xenserver_vdis.png](img/zenpack-xenserver_vdis.png)
-   [Xenserver_vms.png](img/zenpack-xenserver_vms.png)
-   [citrix-zenpack.png](img/zenpack-citrix-zenpack.png)
-   [Xenserver_add_dialog.png](img/zenpack-xenserver_add_dialog.png)
-   [Xenserver_add_menu.png](img/zenpack-xenserver_add_menu.png)
-   [Xenserver_events.png](img/zenpack-xenserver_events.png)
-   [Xenserver_hostcpus.png](img/zenpack-xenserver_hostcpus.png)
-   [Xenserver_hosts.png](img/zenpack-xenserver_hosts.png)
-   [Xenserver_impact_yuml.png](img/zenpack-xenserver_impact_yuml.png)
-   [Xenserver_impact.png](img/zenpack-xenserver_impact.png)
-   [Xenserver_model_yuml.png](img/zenpack-xenserver_model_yuml.png)
-   [Xenserver_networks.png](img/zenpack-xenserver_networks.png)
-   [Xenserver_pbds.png](img/zenpack-xenserver_pbds.png)
-   [Xenserver_pifs.png](img/zenpack-xenserver_pifs.png)
-   [Xenserver_pools.png](img/zenpack-xenserver_pools.png)
-   [Xenserver_srs.png](img/zenpack-xenserver_srs.png)
-   [Xenserver_vapps.png](img/zenpack-xenserver_vapps.png)
-   [Xenserver_vbds.png](img/zenpack-xenserver_vbds.png)
-   [Xenserver_vdis.png](img/zenpack-xenserver_vdis.png)
-   [Xenserver_vifs.png](img/zenpack-xenserver_vifs.png)
-   [Xenserver_vms.png](img/zenpack-xenserver_vms.png)
-   [Xenserver_model_yuml.png](img/zenpack-xenserver_model_yuml.png)
-   [Xenserver_vdis.png](img/zenpack-xenserver_vdis.png)
-   [Xenserver_vifs.png](img/zenpack-xenserver_vifs.png)
-   [citrix-zenpack.png](img/zenpack-citrix-zenpack.png)
-   [Xenserver_add_dialog.png](img/zenpack-xenserver_add_dialog.png)
-   [Xenserver_add_menu.png](img/zenpack-xenserver_add_menu.png)
-   [Xenserver_events.png](img/zenpack-xenserver_events.png)
-   [Xenserver_hostcpus.png](img/zenpack-xenserver_hostcpus.png)
-   [Xenserver_hosts.png](img/zenpack-xenserver_hosts.png)
-   [Xenserver_impact_yuml.png](img/zenpack-xenserver_impact_yuml.png)
-   [Xenserver_impact.png](img/zenpack-xenserver_impact.png)
-   [Xenserver_model_yuml.png](img/zenpack-xenserver_model_yuml.png)
-   [Xenserver_networks.png](img/zenpack-xenserver_networks.png)
-   [Xenserver_pbds.png](img/zenpack-xenserver_pbds.png)
-   [Xenserver_pifs.png](img/zenpack-xenserver_pifs.png)
-   [Xenserver_pools.png](img/zenpack-xenserver_pools.png)
-   [Xenserver_srs.png](img/zenpack-xenserver_srs.png)
-   [Xenserver_vapps.png](img/zenpack-xenserver_vapps.png)
-   [Xenserver_vbds.png](img/zenpack-xenserver_vbds.png)
-   [Xenserver_vdis.png](img/zenpack-xenserver_vdis.png)
-   [Xenserver_vifs.png](img/zenpack-xenserver_vifs.png)
-   [Xenserver_vms.png](img/zenpack-xenserver_vms.png)
-   [citrix-zenpack.png](img/zenpack-citrix-zenpack.png)
-   [Xenserver_add_dialog.png](img/zenpack-xenserver_add_dialog.png)
-   [Xenserver_add_menu.png](img/zenpack-xenserver_add_menu.png)
-   [Xenserver_events.png](img/zenpack-xenserver_events.png)
-   [Xenserver_hostcpus.png](img/zenpack-xenserver_hostcpus.png)
-   [Xenserver_hosts.png](img/zenpack-xenserver_hosts.png)
-   [Xenserver_impact_yuml.png](img/zenpack-xenserver_impact_yuml.png)
-   [Xenserver_impact.png](img/zenpack-xenserver_impact.png)
-   [Xenserver_model_yuml.png](img/zenpack-xenserver_model_yuml.png)
-   [Xenserver_networks.png](img/zenpack-xenserver_networks.png)
-   [Xenserver_pbds.png](img/zenpack-xenserver_pbds.png)
-   [Xenserver_pifs.png](img/zenpack-xenserver_pifs.png)
-   [Xenserver_srs.png](img/zenpack-xenserver_srs.png)
-   [Xenserver_pools.png](img/zenpack-xenserver_pools.png)
-   [Xenserver_vapps.png](img/zenpack-xenserver_vapps.png)
-   [Xenserver_vbds.png](img/zenpack-xenserver_vbds.png)
-   [Xenserver_vdis.png](img/zenpack-xenserver_vdis.png)
-   [Xenserver_vms.png](img/zenpack-xenserver_vms.png)
-   [Xenserver_vifs.png](img/zenpack-xenserver_vifs.png)


# Dynamic Service View

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.DynamicView

## Dynamic Service View ZenPack

Dynamic Service View ("dynamic view") is a visualization of system
objects and their relationships to other objects.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.DynamicView ZenPack provides a dynamic visualization
of system objects and their relationships to other objects.

You can access the dynamic view from groups, systems, and locations.
Depending on the object type, different relationships are illustrated.
Each dynamic view shows related objects in a graph. Each object in that
graph displays its associated event information.

Dynamic Service View: Device Graph

@lb[](img/zenpack-image2021-5-19_15-11-19.png)

When you click an object in the graph, the "inspector" panel appears.
This panel provides detailed information about the object and links
directly to it. Information that appears in the inspector depends on the
object type selected.

Dynamic Service View: Inspector Panel

@lb[](img/zenpack-image2021-5-19_15-12-28.png)

## Prerequisites

|                   |                             |
|-------------------|-----------------------------|
| Prerequisite      | Restriction                 |
| Product           | Zenoss 6.6.0                |
| Required ZenPacks | ZenPacks.zenoss.DynamicView |

## Dynamic View of Organizers

The dynamic view of organizers shows objects that can impact the status
of the organizer, such as other organizers and devices. This view also
shows relationships between devices and a virtual infrastructure, such
as VMware or Cisco UCS objects monitored by the system, as well as
storage information.

To access the dynamic view for an organizer (such as a group, system, or
location):

1.  From Infrastructure &gt; Devices, select the organizer in the
    devices hierarchy.
2.  Click **Details**.
3.  Select Dynamic Service View.

## Dynamic View of Devices

The dynamic view of devices shows the relationship between a device and
monitored components.

To access the dynamic view for a device:

1.  From Infrastructure &gt; Devices, click a device in the device list.
    The device overview page appears.
2.  Select Dynamic Service View in the left panel.

### Dynamic View of Cisco UCS Devices

On Cisco UCS devices, the dynamic view shows the components and
relationships that make up a Cisco UCS cluster.

### Dynamic View of VMware Hosts

On VMware Hosts (ESX servers), the dynamic view shows the relative
VMware elements that are connected to the host, such as:

-   VMs that currently are running on the Host
-   Data stores that are mounted by the Host
-   Clusters to which the Host belongs

### Dynamic View of Storage Devices

On storage devices, such as NetApp Filers, there are two dynamic views:

-   **Physical Storage View** - Shows the device's storage enclosures
    and associated hard disks.
-   **Logical Storage View** - Shows the logical storage arrangement
    that the storage device presents, such as file systems and raid
    groups.

## Changes

2.0.0 (distributed with Zenoss 6.6.0)

-   Dynamic View (Visualization) updated to eliminate the dependency on
    Adobe Flash

## Attachments:

-   [(DynamicView)DynamicServiceView.dynamicviewcontrols.png](img/zenpack-dynamicserviceview.dynamicviewcontrols.png)
-   [(DynamicView)DynamicServiceView.dynamicviewgraph.png](img/zenpack-dynamicserviceview.dynamicviewgraph.png)
-   [(DynamicView)DynamicServiceView.dynamicviewinspectorpanel.png](img/zenpack-dynamicserviceview.dynamicviewinspectorpanel.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [(DynamicView)DynamicServiceView.dynamicviewcontrols.png](img/zenpack-dynamicserviceview.dynamicviewcontrols.png)
-   [(DynamicView)DynamicServiceView.dynamicviewgraph.png](img/zenpack-dynamicserviceview.dynamicviewgraph.png)
-   [(DynamicView)DynamicServiceView.dynamicviewinspectorpanel.png](img/zenpack-dynamicserviceview.dynamicviewinspectorpanel.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [(DynamicView)DynamicServiceView.dynamicviewgraph.png](img/zenpack-dynamicserviceview.dynamicviewgraph.png)
-   [(DynamicView)DynamicServiceView.dynamicviewinspectorpanel.png](img/zenpack-dynamicserviceview.dynamicviewinspectorpanel.png)
-   [(DynamicView)DynamicServiceView.dynamicviewcontrols.png](img/zenpack-dynamicserviceview.dynamicviewcontrols.png)


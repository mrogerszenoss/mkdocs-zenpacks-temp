# Dell Monitor (Core)

@lb[](img/zenpack-dell-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.DellMonitor

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-3492){.external-link}

## Dell Monitor (Core) ZenPack

DellMonitor provides custom modeling of devices running the Dell
OpenManage agents. It also contains hardware identification for Dell
proprietary hardware. The information is collected through the SNMP
interface.

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Background

The ZenPacks.zenoss.DellMonitor ZenPack provides customized modeling of
devices running Dell OpenManage agents, and includes identification for
proprietary Dell hardware.

The following information is collected through SNMP:

-   Hardware Model
-   Hardware Serial Number
-   Operating System
-   CPU Information (socket, speed, cache, voltage)
-   PCI Card Information (manufacturer, model)

## Prerequisites

|                       |                                                                                |
|-----------------------|--------------------------------------------------------------------------------|
| Prerequisite          | Restriction                                                                    |
| Product               | Zenoss platform 4.x, 5.x, Zenoss 2.2 or higher                                 |
| Required ZenPacks     | ZenPacks.zenoss.DellMonitor                                                    |
| On each remote device | The Dell OpenManage SNMP Agent is used to gather information about the device. |

## Enable Enhanced Modeling

To enable modeling:

1.  Select Infrastructure from the navigation bar.
2.  Click the device name in the device list. The device overview page
    appears.
3.  Select Modeler Plugins from the left panel.
4.  Click Add Fields to reveal the list of available plugins.
5.  Select the following plugins from the Available fields list, and
    then drag them to the Plugins list:
    -   DellCPUMap
    -   DellDeviceMap
    -   DellPCIMap
6.  Remove the following plugins by clicking on the 'X' button located
    to the right of the plugin.
    -   zenoss.snmp.CpuMap
    -   zenoss.snmp.DeviceMap
7.  Click Save to save the updates.
8.  Remodel the device using these new plugins by selecting Model Device
    from the Action menu.

## Daemons

|                       |             |
|-----------------------|-------------|
| Type                  | Name        |
| Modeler               | zenmodeler  |
| Performance Collector | zenperfsnmp |

## Attachments:

-   [dell-zenpack.png](img/zenpack-dell-zenpack.png)
-   [dell-zenpack.png](img/zenpack-dell-zenpack.png)
-   [dell-zenpack.png](img/zenpack-dell-zenpack.png)


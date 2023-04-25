# HP Monitor

@lb[](img/zenpack-hp-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.HPMonitor

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-3448){.external-link}

## HP Monitor ZenPack

HPMonitor provides custom modeling of devices running the HP/Compaq
Insight Management Agents. It also contains hardware identification for
HP proprietary hardware. The information is collected through the SNMP
interface.

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Background

The ZenPacks.zenoss.HPMonitor ZenPack provides customized modeling of
devices running HP Insight Management Agents, and includes
identification for proprietary HP hardware.

The following information is collected through SNMP:

-   Hardware Model
-   Hardware Serial Number
-   Operating System
-   CPU Information (socket, speed, cache)

## Prerequisites

|                       |                                                                            |
|-----------------------|----------------------------------------------------------------------------|
| Prerequisite          | Restriction                                                                |
| Product               | Zenoss platform 4.x, Zenoss 2.2 or higher                                  |
| Required ZenPacks     | ZenPacks.zenoss.HPMonitor                                                  |
| On each remote device | The HP Insight SNMP Management Agent gathers information about the device. |

## Enable Enhanced Modeling

To enable enhanced modeling:

1.  Select Infrastructure from the navigation bar.
2.  Click the device name in the device list. The device overview page
    appears.
3.  Select Modeler Plugins from the left panel.
4.  Click Add Fields to reveal the list of available plugins.
5.  Select the following available plugins and drag them to the plugins
    list:
    -   HPCpuMap
    -   HPDeviceMap
6.  Remove the following plugins by clicking the 'X' button to the right
    of the plugin:
    -   zenoss.snmp.CPUMap
    -   zenoss.snmp.DeviceMap
7.  Click **Save**.
8.  Remodel the device using the new plugins. To do this, select Model
    Device from the Action menu.

## Daemons

|                       |             |
|-----------------------|-------------|
| Type                  | Name        |
| Modeler               | zenmodeler  |
| Performance Collector | zenperfsnmp |

## Attachments:

-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)
-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)
-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)
-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)


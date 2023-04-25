# Nortel Passport Switches (Commercial)

@lb[](img/zenpack-nortel-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.NortelMonitor

## Nortel Passport Switches (Commercial) ZenPack

Monitoring for Nortel Passport switches.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.NortelMonitor ZenPack monitors devices from Nortel
Networks.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.2 or higher |
| Required ZenPacks | ZenPacks.zenoss.NortelMonitor             |

## Configuring Nortel Devices to Allow SNMP Queries

Configure the Nortel device to allow SNMP queries from the Zenoss
platform server, and send SNMP v1 or SNMP v2 traps to the Zenoss
platform server.

## Configuring Zenoss platform

All Nortel devices must exist under the /Devices/Network/Nortel device
class.

1.  Navigate to the device or device class in the Zenoss platform
    interface.
    -   If applying changes to a device class:
        1.  Select the class in the devices hierarchy.
        2.  Click **Details**.
        3.  Select Configuration Properties.
    -   If applying changes to a device:
        1.  Click the device in the device list.
        2.  Select Configuration Properties.
2.  Edit the appropriate configuration properties for the device or
    devices.

    Nortel Configuration Properties
    |                    |                                                                                     |
    |--------------------|-------------------------------------------------------------------------------------|
    | Name               | Description                                                                         |
    | zSnmpCommunity     | Consult with your network administrators to determine the SNMP community permitted. |
    | zSnmpMonitorIgnore | This should be set to `False`                                                       |
    | zSnmpPort          | The default port is 161.                                                            |
    | zSnmpVer           | This should be set to `v2c`                                                         |

3.  Click Save to save your changes. You will now be able to start
    collecting the Nortel device metrics from this device.
4.  Navigate to Graphs and you should see some placeholders for graphs.
    After approximately fifteen minutes you should see the graphs start
    to become populated with information.

## Daemons

|                       |             |
|-----------------------|-------------|
| Type                  | Name        |
| Modeler               | zenmodeler  |
| Performance Collector | zenperfsnmp |

## Attachments:

-   [nortel-zenpack.png](img/zenpack-nortel-zenpack.png)
-   [nortel-zenpack.png](img/zenpack-nortel-zenpack.png)


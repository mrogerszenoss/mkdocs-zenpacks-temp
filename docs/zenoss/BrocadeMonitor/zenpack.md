# Brocade SAN Switches

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.BrocadeMonitor

## Brocade SAN Switches ZenPack

BrocadeMonitor allows you to monitor Brocade Storage Area Network (SAN)
switches.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 2.1.1- [GitHub Repo](https://github.com/zenoss/ZenPacks.zenoss.BrocadeMonitor){.external-link}:   Released on 2014/10/23:   Compatible with Zenoss Resource Manager 4.1.x, Zenoss Resource
    Manager 4.2.x, Zenoss Resource Manager 5.0.x

## Background

The ZenPacks.zenoss.BrocadeMonitor ZenPack monitors Brocade Storage Area
Network (SAN) switches.

## Prerequisites

| Prerequisite      | Restriction                                                 |
|-------------------|-------------------------------------------------------------|
| Product           | Zenoss platform 4.x                                         |
| Required ZenPacks | ZenPacks.zenoss.BrocadeMonitor, ZenPacks.zenoss.StorageBase |

## Configuring Brocade Devices to Allow SNMP Queries

Configure the Brocade devices to allow SNMP queries from the Zenoss
platform server, and send SNMP v1 or SNMP v2 traps to the Zenoss
platform server.

## Configuring Zenoss platform

All Brocade devices must exist under the /Devices/Storage/Brocade device
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

    Brocade Configuration Properties
    | Name               | Description                                                                        |
    |--------------------|------------------------------------------------------------------------------------|
    | zSnmpCommunity     | Consult with your storage administrators to determine the SNMP community permitted |
    | zSnmpMonitorIgnore | This should be set to `False`                                                      |
    | zSnmpPort          | The default port is 161                                                            |
    | zSnmpVer           | This should be set to `v2c`                                                        |

3.  Click Save to save your changes. You will now be able to start
    collecting the Brocade switch metrics from this device.

## Viewing Fibre Channel Port Information

To view the virtual servers, select Brocade Details.

## Daemons

| Type                  | Name        |
|-----------------------|-------------|
| Modeler               | zenmodeler  |
| Performance Collector | zenperfsnmp |

## Changes

**2.1.1** (2014-10-23)

-   Improve performance of FCPort component grid on Zenoss 5.

# Juniper Devices

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.JuniperMonitor

## Juniper Devices ZenPack

The JuniperMonitor ZenPack allows system administrators to monitor their
Juniper devices.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 2.1.1- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2014/03/05:   Compatible with Zenoss Resource Manager 4.1.x, Zenoss Resource
    Manager 4.2.x, Zenoss Resource Manager 5.x.x

## Background

The ZenPacks.zenoss.JuniperMonitor ZenPack monitors devices from Juniper
Networks.

## Prerequisites

| Prerequisite      | Restriction                               |
|-------------------|-------------------------------------------|
| Product           | Zenoss platform 4.x, Zenoss 2.2 or higher |
| Required ZenPacks | ZenPacks.zenoss.JuniperMonitor            |

## Configuring Juniper Devices to Allow SNMP Queries

Configure the Juniper device to allow SNMP queries from the Zenoss
platform server, and send SNMP v1 or SNMP v2 traps to the Zenoss
platform server.

## Configuring Zenoss platform

All Juniper devices must exist under the /Devices/Network/Juniper device
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

    Juniper Configuration Properties
    | Name               | Description                                                                         |
    |--------------------|-------------------------------------------------------------------------------------|
    | zSnmpCommunity     | Consult with your network administrators to determine the SNMP community permitted. |
    | zSnmpMonitorIgnore | Set to a value of `False`.                                                          |
    | zSnmpPort          | Set the SNMP port. The default port is 161.                                         |
    | zSnmpVer           | Set the SNMP version. Set to a value of `v2c`.                                      |

3.  Click Save to save your changes. You will now be able to start
    collecting the Juniper device metrics from this device.
4.  Navigate to Graphs and you should see some place holders for graphs.
    After approximately fifteen minutes you should see the graphs start
    to become populated with information.

## Daemons

| Type                  | Name        |
|-----------------------|-------------|
| Type                  | Name        |
| Modeler               | zenmodeler  |
| Performance Collector | zenperfsnmp |

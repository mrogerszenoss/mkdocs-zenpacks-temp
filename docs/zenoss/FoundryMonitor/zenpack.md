# Foundry Networks Devices

@lb[](img/zenpack-foundry-networks-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.FoundryMonitor

## Foundry Networks Devices ZenPack

Monitoring of Foundry Networks devices.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.FoundryMonitor ZenPack monitors networking devices
built by Foundry Networks (now Brocade Communication Systems).

Note: This ZenPack is not installed when Zenoss platform is installed.
To download it, visit the [Zenoss Support](https://support.zenoss.com){.external-link} site.

This ZenPack models specific details on Foundry devices, including:

-   DRAM
-   Serial Number
-   Processor
-   Product type

This ZenPack monitors memory utilization, as well as CPU utilization
averages for 1 minute, 1 second, and 5 seconds.

It also includes all Foundry traps to ensure proper decoding of those
traps through `zentrap`.

## Prerequisites

|                   |                                |
|-------------------|--------------------------------|
| Prerequisite      | Restriction                    |
| Product           | Zenoss platform 4.x            |
| Required ZenPacks | ZenPacks.zenoss.FoundryMonitor |

## Configuring Zenoss platform

All Foundry devices must exist in the `/Devices/Network/Foundry` device
class.

Follow these steps to configure Zenoss platform:

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

    Foundry Configuration Properties
    |                    |                                                                                     |
    |--------------------|-------------------------------------------------------------------------------------|
    | Name               | Description                                                                         |
    | zSnmpCommunity     | Consult with your network administrators to determine the SNMP community permitted. |
    | zSnmpMonitorIgnore | Set to a value of `False`.                                                          |
    | zSnmpPort          | The default port is 161.                                                            |
    | zSnmpVer           | Set to a value of `v2c`.                                                            |

3.  Click **Save** to save your changes. Zenoss platform now will begin
    collecting Foundry device metrics from this device.
4.  Navigate to Graphs and you should see some placeholders for
    performance graphs. After approximately fifteen minutes you should
    see the graphs start to become populated with information.

## Daemons

|                       |             |
|-----------------------|-------------|
| Type                  | Name        |
| Modeler               | zenmodeler  |
| Performance Collector | zenperfsnmp |
| Traps                 | zentrap     |

## Attachments:

-   [foundry-networks-zenpack.png](img/zenpack-foundry-networks-zenpack.png)
-   [foundry-networks-zenpack.png](img/zenpack-foundry-networks-zenpack.png)


# StorageBase

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.StorageBase

## StorageBase ZenPack

The StorageBase ZenPack adds additional reports for storage device
licenses, clients and disk firmware.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 1.4.4- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2019/09/17:   Requires [DynamicView ZenPack](http://help.zenoss.com/display/in/Dynamic+Service+View){.external-link}:   Compatible with Zenoss 6.3-6.4, Zenoss Cloud with and Service Impact
    5.5.1

Version 1.4.3- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2017/07/19:   Requires [DynamicView ZenPack](http://help.zenoss.com/display/in/Dynamic+Service+View "ZenPack:DynamicView"){.external-link}:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x, Zenoss Resource Manager 5.1.x, Zenoss Resource
    Manager 5.x.x

Version 1.4.2- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2017/05/30:   Requires [DynamicView ZenPack](http://help.zenoss.com/display/in/Dynamic+Service+View "ZenPack:DynamicView"){.external-link}:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x, Zenoss Resource Manager 5.1.x, Zenoss Resource
    Manager 5.x.x

Version 1.4.1- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2016/01/22:   Requires [DynamicView ZenPack](http://help.zenoss.com/display/in/Dynamic+Service+View "ZenPack:DynamicView"){.external-link}:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x, Zenoss Resource Manager 5.1.x, Zenoss Resource
    Manager 5.x.x

Version 1.4.0- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2015/11/30:   Requires [DynamicView ZenPack](http://help.zenoss.com/display/in/Dynamic+Service+View "ZenPack:DynamicView"){.external-link}:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x, Zenoss Resource Manager 5.1.x, Zenoss Resource
    Manager 5.x.x

Version 1.3.2- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2015/10/19:   Requires [DynamicView ZenPack](http://help.zenoss.com/display/in/Dynamic+Service+View "ZenPack:DynamicView"){.external-link}:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x, Zenoss Resource Manager 5.1.x, Zenoss Resource
    Manager 5.x.x

## Background

The ZenPacks.zenoss.StorageBase ZenPack contains base classes and
reports for ZenPacks that use the base classes.

Reports include:

-   Licenses - Shows the storage devices and installed licenses.
-   Clients - Shows the devices that use the storage devices.
-   Disk Firmware - After selecting a storage device, displays disk
    firmware information.

## Prerequisites

Verify that you have the following prerequisites before installing and
using this ZenPack.

Zenoss Prerequisites

-   Zenoss &gt;= 4.2
-   ZenPacks.zenoss.DynamicView

## Changes

**1.4.4**

-   Do not automatically generate storage reports (ZPS-4174)
-   Do not show spinning wheel when generating reports (ZPS-4304)
-   Tested with Zenoss 6.4.1, Zenoss Cloud with and Service Impact 5.5.1

**1.4.3**

-   Fix issue which caused to missing data on analytics server.
    (ZPS-1673)

**1.4.2**

-   Fix incorrect DynamicView relations for ConvergedNetworkAdapter
    components. (ZPS-1162)

**1.4.1**

-   Handle stale catalog entries when looking up WWNs and IQNs.
    (ZEN-21699)

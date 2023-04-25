# Huawei Wireless

@lb[](img/zenpack-huawei-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Nick Muir

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.community.HuaweiWireless

### More Information:

[GitHub page/HomePage](https://github.com/nickmuir/ZenPacks.community.HuaweiWireless){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/nickmuir/ZenPacks.community.HuaweiWireless.git){.external-link}

## Huawei Wireless ZenPack

Monitors Huawei Enterprise Wireless Controllers and their Access Points

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.5.3-beta- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.HuaweiWireless/1.5.3-beta/ZenPacks.community.HuaweiWireless-1.5.3-beta.egg){.external-link}:   Released on 2016/05/16:   Compatible with Zenoss Core 4.2.x

## Background

This ZenPack provides support for monitoring Huawei Enterprise Wireless
Controllers. Monitoring is performed via SNMP.

## Features

The features added by this ZenPack be summarized as follows. They are
each detailed further below.

-   Discovery of Access Points and AP Regions
-   Performance monitoring of Controller and Access Points

### Discovery

The following components will be automatically discovered through via
the Wireless Controller.

Access Points:   Attributes: Name, Model, IP Address, MAC Address, AP Status, AP
    Region, Firmware Version, Serial Number, AP Neighbour (Collected via
    LLDP), AP Neighbour port (Collected via LLDP)

<!-- -->

AP Regions:   Attributes: Name, Deployment Type, Number of Access Points

### Performance Monitoring

The following metrics will be collected every 5 minutes by default.

Wireless Controller:   hwAcCurAuthSucessStaNum:   hwAcCurJointApNum:   hwEntityCpuUsage:   hwEntityMemUsage

<!-- -->

Access Points:   hwApCpuUseRate:   hwApMemoryUseRate:   hwApOnlineUserNum

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Device Classes
</dt>
</dl>

-   /Network/Wireless/Access Controller/Huawei

<dl markdown="1">
<dt markdown="1">
Modeler Plugins
</dt>
</dl>

-   HuaweiAccessControllerMap

<dl markdown="1">
<dt markdown="1">
Monitoring Templates
</dt>
</dl>

-   HuaweiAccessPoint
-   HuaweiAPRegion

## Attachments:

-   [huawei-zenpack.png](img/zenpack-huawei-zenpack.png)
-   [HuaweiAccessPoints.png](img/zenpack-huaweiaccesspoints.png)
-   [HuaweiAPRegions.png](img/zenpack-huaweiapregions.png)
-   [HuwaeiWirelessController.png](img/zenpack-huwaeiwirelesscontroller.png)
-   [huawei-zenpack.png](img/zenpack-huawei-zenpack.png)
-   [HuaweiAccessPoints.png](img/zenpack-huaweiaccesspoints.png)
-   [HuaweiAPRegions.png](img/zenpack-huaweiapregions.png)
-   [HuwaeiWirelessController.png](img/zenpack-huwaeiwirelesscontroller.png)
-   [HuaweiAccessPoints.png](img/zenpack-huaweiaccesspoints.png)
-   [huawei-zenpack.png](img/zenpack-huawei-zenpack.png)
-   [HuaweiAPRegions.png](img/zenpack-huaweiapregions.png)
-   [HuwaeiWirelessController.png](img/zenpack-huwaeiwirelesscontroller.png)


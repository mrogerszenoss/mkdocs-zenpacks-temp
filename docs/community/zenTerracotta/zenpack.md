# Terracotta Server

@lb[](img/zenpack-terracotta-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Joseph Anderson

### Maintainers:

Joseph Anderson

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.community.zenTerracotta

### More Information:

[GitHub page/HomePage](https://github.com/j053ph4/ZenPacks.community.zenTerracotta){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/j053ph4/ZenPacks.community.zenTerracotta.git){.external-link}

## Terracotta Server ZenPack

Provides JMX-based monitoring of Terracotta distributed caching
software.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 2.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.zenTerracotta/2.0/ZenPacks.community.zenTerracotta-2.0.egg){.external-link}:   **Summary of changes:** Version 4.x support, migrated to
    Construction Kit:   Released on 2013/04/02:   Requires [ConstructionKit ZenPack](https://help.zenoss.com/display/in/constructionkit "ZenPack:ConstructionKit"){.external-link},[zenJavaApp ZenPack](https://help.zenoss.com/display/in/zenjavaapp-page-does-not-exist "ZenPack:ZenJavaApp (page does not exist){.external-link}"):   Compatible with Zenoss Core 3.2.x, Zenoss Core 4.2.x

<!-- -->

Version 2.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.zenTerracotta/2.1/ZenPacks.community.zenTerracotta-2.1.egg){.external-link}:   **Summary of changes:** updated to support ConstructionKit 2.0,
    added object relations to other components/devices:   Released on 2013/11/05:   Requires [ConstructionKit ZenPack](https://help.zenoss.com/display/in/constructionkit "ZenPack:ConstructionKit"){.external-link},[zenJavaApp ZenPack](https://help.zenoss.com/display/in/zenjavaapp-page-does-not-exist "ZenPack:ZenJavaApp (page does not exist){.external-link}"):   Compatible with Zenoss Core 4.2.x

## Background

Developed by: Joseph Anderson Description:

This Monitoring Zenpack provides monitoring of Terracotta distributed
caching software. It collects Terracotta-specific metrics via JMX, and
provides a modeler script for JMX detection.

Dependencies:

ZenPacks.community.ConstructionKit ZenPacks.community.zenJavaApp

Components:

"TerracottaServer" OS component and RRD Template "/App/Terracotta" Event
Class "TerracottaServerMap" modeler plugin script

Requirements:

       Zenoss Versions Supported: 3.x, 4.x
       External Dependencies: None
       ZenPack Dependencies: ZenPacks.community.ConstructionKit, ZenPacks.community.zenJavaApp
       Installation Notes: zenoss restart after installing this ZenPack.
       Configuration:

'zTerracottaServerPortRange' gives a port range that the modeler will
scan Add "TerracottaServerMap" to the list of modeler plugins for the
desired device/device class

History:

Change History:

       1.0 initial release
       2.0 rebuilt using ConstructionKit for 4.x compatibility

rewrote modeler script to leverage new JavaApp detection logic

       2.1 rebuilt for ConstructionKit 2.0

Tested: This ZenPack was tested with versions 3.2.5 and 4.2.3.

Source: <https://github.com/j053ph4/ZenPacks.community.zenTerracotta>

Known issues:

## Attachments:

-   [terracotta-zenpack.png](img/zenpack-terracotta-zenpack.png)
-   [terracotta-zenpack.png](img/zenpack-terracotta-zenpack.png)
-   [terracotta-zenpack.png](img/zenpack-terracotta-zenpack.png)


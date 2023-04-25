# HPMSA

@lb[](img/zenpack-hp-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

ilya.tm

### Maintainers:

ilya.tm

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.community.HPMSA

### Git Sources (For Cloning):

[Link](https://github.com/ilyatm/ZenPacks.community.HPMSA){.external-link}

## HPMSA ZenPack

Monitoring for HP MSA Storages

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.1.2- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.HPMSA/1.1.2/ZenPacks.community.HPMSA-1.1.2.egg){.external-link}:   **Summary of changes:** Added event class. Device version on
    overview panel. Fix for msa 2000 g2 events.
:   Released on 2016/05/19:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link}:   Compatible with Zenoss Core 4.2.x

<!-- -->

Version 1.1.3- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.HPMSA/1.1.3/ZenPacks.community.HPMSA-1.1.3.egg){.external-link}:   **Summary of changes:** Fix for msa 2000 g2 events.
:   Released on 2016/05/19:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link}:   Compatible with Zenoss Core 4.2.x

## Background

This ZenPack provides support for monitoring HP MSA Storages.

## Features

### Metrics

HP MSA API provides statistics for: Controllers, HDD, Virtual Disks,
Volumes, Host Ports.

### Events

For all components ZenPack check health status. If it is not OK you get
an event.

## Limitations

-   No statistic for HP MSA 2000 G2

## Configuration

Installing the ZenPack will add the following items to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Device Classes
</dt>
</dl>

-   /Storage/HP/MSA

<dl markdown="1">
<dt markdown="1">
Configuration Properties
</dt>
</dl>

-   zHPMSAControllers
-   zHPMSAPassword
-   zHPMSASecureConnection
-   zHPMSAUser

<dl markdown="1">
<dt markdown="1">
Modeler Plugins
</dt>
</dl>

-   community.api.hpmsa

<dl markdown="1">
<dt markdown="1">
Monitoring Templates
</dt>
</dl>

-   HPMSAEvents
-   Enclosure
-   PowerSupp
-   Controller
-   HardDisk
-   HostPort
-   ExpansionPort
-   ManagementPort
-   IOModule
-   CompactFlash
-   VirtualDisk
-   Volume

<dl markdown="1">
<dt markdown="1">
Event Classes
</dt>
</dl>

-   /Storage/HPMSA

## Usage

Add device to /Storage/HP/MSA class without modeling. Change
zHPMSAControllers properties(list controllers ip) Set zHPMSAUser,
zHPMSAPassword, zHPMSASecureConnection.

## Attachments:

-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)
-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)
-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)


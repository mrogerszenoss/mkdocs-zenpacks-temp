# Windows SNMP Service Monitor

@lb[](img/zenpack-microsoft-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Ryan Matte

### Maintainers:

Ryan Matte

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.Nova.WinServiceSNMP

### More Information:

[GitHub page/HomePage](http://community.zenoss.org/docs/DOC-12999){.external-link}

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-12999){.external-link}

### Applications Monitored:

Windows Services

## Windows SNMP Service Monitor ZenPack

The Windows SNMP Service Monitor ZenPack allows Zenoss to monitor
Windows Services via SNMP.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.1 (4.2.x)- [Download](http://dmon.org/downloads/zenoss/zenpacks/zenoss4/ZenPacks.Nova.WinServiceSNMP-1.1-py2.7.egg){.external-link}:   Compatible with Zenoss Core 4.2.x:   Incompatible with Zenoss Core 2.5.x, Zenoss Core 3.1.x, Zenoss Core
    3.2.x

<!-- -->

Version 1.0 (3.2.x)- [Download](http://dmon.org/downloads/zenoss/zenpacks/zenoss3/ZenPacks.Nova.WinServiceSNMP-1.0-py2.6.egg){.external-link}:   Compatible with Zenoss Core 3.2.x:   Incompatible with Zenoss Core 2.5.x, Zenoss Core 4.2.x

<!-- -->

Version 1.0 (2.5.x)- [Download](http://dmon.org/downloads/zenoss/zenpacks/zenoss2/ZenPacks.Nova.WinServiceSNMP-1.0-py2.4.egg){.external-link}:   Compatible with Zenoss Core 2.5.x:   Incompatible with Zenoss Core 3.2.x, Zenoss Core 4.2.x

## Background

**DESCRIPTION:**

The Windows SNMP Service Monitor ZenPack allows Zenoss to monitor
Windows Services via SNMP. It automatically links to the /Server/Windows
device class. After installing the pack you can simply remodel devices
in /Server/Windows and Zenoss will discover any services running on
them.

Make sure that you lock the services to prevent them from being removed
during a remodel while a service is down. Modeling will only pick up
services that are running.

**INSTALLATION:**

During installation and removal the ZenPack rebuilds device relations
for all devices within the /Server/Windows device class. Depending on
the number of devices that you have in that class, it can take a long
time. You will notice some errors in the UI while the relations are
being rebuilt, which is normal. Please be patient and allow it to
complete. After the relations have been rebuilt Zenoss should be
restarted. Make sure that the zenwinsrvsnmp daemon is running after the
restart is performed.

**ZPROPERTIES:**

-   zWinServiceSNMPIgnoreNames: Place the full names of any services
    that you want to ignore in this line by line.
-   zWinServiceSNMPMonitorNames: Place the full names of any services
    which you explicitly want to monitor (ignoring all others) in this
    line by line.
-   zWinServiceSNMPMonitorNamesEnable: This enables/disables the use of
    zWinServiceSNMPMonitorNames

Note that you need to remodel your devices for the above to take effect.

Keep in mind that zWinServiceSNMPIgnoreNames is constantly in use. If
you put the same service name in both zWinServiceSNMPIgnoreNames and
zWinServiceSNMPMonitorNames it will be ignored.

**DAEMON:**

-   zenwinsrvsnmp: Make sure this daemon is running or service
    monitoring won't work.

**TEMPLATE:**

-   WinServiceSNMP in /Server/Windows: This template is required for
    monitoring services. Do not bind this template to the device. Make
    sure the template is in the class that the device is in (or a higher
    class). The template will automatically be used for the windows
    services components.

**MODELER PLUGIN:**

-   community.snmp.WinServiceMap: This plugin is required during
    modeling.

**TIPS:**

Generally changes to monitoring status are immediately pushed to
collector daemons, but sometimes if the daemon is too busy the daemon
misses the change. In those cases the monitoring status doesn't get
picked up by the daemon until the next reconfig cycle, which can take a
while. If you notice that you're often still getting windows service
down notifications shortly after you've toggled monitoring off on a
windows service, you can add the following transform to the
/Status/WinServiceSNMP event class to resolve this (this transform will
only work on Zenoss 4.2.x and later).

    # drop events for unmonitored winservicesnmp components
    if component.monitor == False: evt._action = 'drop'

**SCREENSHOTS:**

@lb[](img/zenpack-zp1.png)

@lb[](img/zenpack-zp2.png)

@lb[](img/zenpack-zp3.png)

## Attachments:

-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)
-   [ZP1.png](img/zenpack-zp1.png)
-   [ZP2.png](img/zenpack-zp2.png)
-   [ZP3.png](img/zenpack-zp3.png)
-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)
-   [ZP1.png](img/zenpack-zp1.png)
-   [ZP2.png](img/zenpack-zp2.png)
-   [ZP3.png](img/zenpack-zp3.png)
-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)
-   [ZP1.png](img/zenpack-zp1.png)
-   [ZP2.png](img/zenpack-zp2.png)
-   [ZP3.png](img/zenpack-zp3.png)


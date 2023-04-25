# NTP Monitor

@lb[](img/zenpack-zenpack-general.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.zenoss.NtpMonitor

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.NtpMonitor.git){.external-link}

### Applications Monitored:

NTP

## NTP Monitor ZenPack

The NTPMonitor ZenPack checks the offset of a local / internal NTP
server against it's sync peer (usually a public NTP server on the
internet) to ensure that syncing is working properly and that the NTP
server is healthy.

**This ZenPack will <u>*NOT*</u> monitor the offset between the clocks
on monitored hosts and the NTP servers that they are using to sync their
clocks.  It is *<u>NOT</u>* intended to detect time drift on monitored
hosts.**
**
This ZenPack is only intended to be used to monitor NTP servers**.  **An
NTP server process must be running on the host that you apply the
NTPMonitor template to.

**Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 3.0.0-[Download](https://delivery.zenoss.com){.external-link}:   Released on 2018/05/18:   Compatible with Zenoss 5.x and 6.x

Version 2.2.2-[Download](https://delivery.zenoss.com){.external-link}:   Released on 2015/12/08:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.1.x, Zenoss Core
    3.2.x, Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss Resource Manager
    4.1.x, Zenoss Resource Manager 4.2.x, Zenoss Resource Manager
    5.0.x

Version 2.2.1-[Download](https://delivery.zenoss.com){.external-link}:   Released on 2015/02/03:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.1.x, Zenoss Core
    3.2.x, Zenoss Core 4.2.x, Zenoss Resource Manager 4.1.x, Zenoss
    Resource Manager 4.2.x

## Contents

-   [Background](#background)
    -   [Prerequisites](#prerequisites)
-   [Usage](#usage)
-   [Changes](#changes)

### Prerequisites

-   Zenoss 5.0+
-   ZenPacks.zenoss.PythonCollector
-   ZenPacks.zenoss.ZenPackLib

## Usage

The NTPMonitor template must be bound to the device class or device you
want to monitor.

-   Select Infrastructure from the navigation bar.
-   Click the device name in the device list.
-   Expand Monitoring Templates, and then select Device from the left
    panel.
-   Select Bind Templates from the Action menu.appears.
-   Add the NTPMonitor template to the list of selected templates, and
    then click Submit.

The NTPMonitor template is added to the list of monitoring templates.
You can now start collecting the clock offset between the NTP server and
it's sync peer.

## Changes

3.0.0

-   No longer relies on Nagios plugins to monitor NTP servers
-   Added unit tests
-   Rewritten as a PythonCollector&rsquo;s PythonDataSource
-   Now uses yaml definition (ZenPackLib) instead of objects.xml
-   Added IPv6 support
-   Tested with Zenoss Resource Manager 5.3.3, 6.1.2 and 6.2.0

2.2.1

-   Switched from check_ntp_peer to check_ntp_offset. (ZEN-15833)

2.2.2

-   Switched back to check_ntp_peer (ZEN-15833)
-   Tested for compatibility on Zenoss 5.0.9

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


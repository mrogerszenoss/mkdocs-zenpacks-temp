# Dig Monitor

@lb[](img/zenpack-zenpack-general.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.DigMonitor

### More Information:

[GitHub page/HomePage](http://community.zenoss.org/docs/DOC-3393){.external-link}

### Applications Monitored:

DNS

## Dig Monitor ZenPack

DigMonitor monitors the response time of DNS lookups for devices running
a DNS server.

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Background

The ZenPacks.zenoss.DigMonitor ZenPack monitors the response time of DNS
lookups.

To collect data, this ZenPack uses the check_dig Nagios plugin, which in
turn uses the dig command.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.2 or higher |
| Required ZenPacks | ZenPacks.zenoss.DigMonitor                |

## Enable Monitoring

To enable monitoring by the system:

1.  Select Infrastructure from the navigation bar.
2.  Click the device name in the device list. The device overview page
    appears.
3.  Expand Monitoring Templates in the left panel, and then select
    Device.
4.  Select Bind Templates from the Action menu. The Bind Templates
    dialog appears.
5.  Add the DigMonitor template to the list of selected templates, and
    then click **OK**. The DigMonitor template appears under Monitoring
    Templates.
6.  Select the DigMonitor template in the left panel, and change options
    as needed.

    DigMonitor Data Source Options
    |             |                                                                                               |
    |-------------|-----------------------------------------------------------------------------------------------|
    | Option      | Description                                                                                   |
    | DNS Server  | Name server against which the dig command should be run. The default is the device host name. |
    | Port        | Port on which the name server is listening. This is normally port 53.                         |
    | Record Name | Name of the record you want to look up. The default is zenoss.com.                            |
    | Record Type | DNS record type (for example, A, MX, CNAME).                                                  |

## Daemons

|                       |            |
|-----------------------|------------|
| Type                  | Name       |
| Performance Collector | zencommand |

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


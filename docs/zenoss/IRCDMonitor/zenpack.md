# IRCD Monitor

@lb[](img/zenpack-zenpack-general.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.IRCDMonitor

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-3490){.external-link}

## IRCD Monitor ZenPack

The IRCD Monitor monitors the number of users connected to an IRC
server.

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Background

The ZenPacks.zenoss.IRCDMonitor ZenPack monitors the number of users
connected to an Internet Relay Chat (IRC) server.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.2 or higher |
| Required ZenPacks | ZenPacks.zenoss.IRCDMonitor               |

## Enable Monitoring

To enable monitoring:

1.  Select Infrastructure from the navigation bar.
2.  Click the device name in the device list. The device overview page
    appears.
3.  Expand Monitoring Templates in the left panel, and then select
    Device.
4.  Select Bind Templates from the Action menu. The Bind Templates
    dialog appears.
5.  Move the IrcdMonitor template from the Available list and move it to
    the Selected list.
6.  Click **Save**. The IrcdMonitor template is added.
7.  Click the new template in the left panel and change options as
    needed.

    IRC Basic Data Source Options
    |              |                                                                 |
    |--------------|-----------------------------------------------------------------|
    | Option       | Description                                                     |
    | Port         | Specifies the port to connect to the IRC server (default 6667). |
    | warning_num  | Creates a warning event when this number of users are seen.     |
    | critical_num | Creates a critical event when this number of users are seen.    |

## Daemons

|                       |            |
|-----------------------|------------|
| Type                  | Name       |
| Performance Collector | zencommand |

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


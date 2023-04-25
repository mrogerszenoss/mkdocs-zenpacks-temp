# Jabber Monitor

@lb[](img/zenpack-cisco-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.JabberMonitor

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-3390){.external-link}

## Jabber Monitor ZenPack

Jabber Monitor monitors the response time of devices running a Jabber
server.

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Background

The ZenPacks.zenoss.JabberMonitor ZenPack monitors the response times of
Jabber instant messaging servers.

## Prerequisites

|                   |                               |
|-------------------|-------------------------------|
| Prerequisite      | Restriction                   |
| Product           | Zenoss platform 4.x           |
| Required ZenPacks | ZenPacks.zenoss.JabberMonitor |

## Enable Monitoring

To enable monitoring:

1.  Select Infrastructure from the navigation bar.
2.  Click the device in the device list. The device overview page
    appears.
3.  Expand Monitoring Templates in the left panel, and then select
    Device.
4.  Select Bind Templates from the Action menu. The Bind Templates
    dialog appears.
5.  Move the Jabber template from the Available list to the Selected
    list, and then click **Save**. The Jabber template is added. The
    system can begin collecting Jabber server metrics from the device.
6.  Select the newly added template and change options as needed.

    Jabber Data Source Options
    |                   |                                                                                |
    |-------------------|--------------------------------------------------------------------------------|
    | Option            | Description                                                                    |
    | Timeout (seconds) | Seconds before connection times out (default: 60)                              |
    | Port              | The port on which the Jabber server is listening. Typically this is port 5223. |
    | Send String       | string to send to the server: default                                         |
    | Expect String     | String to expect in server response.                                           |

## Daemons

|                       |            |
|-----------------------|------------|
| Type                  | Name       |
| Performance Collector | zencommand |

## Attachments:

-   [cisco-zenpack.png](img/zenpack-cisco-zenpack.png)
-   [cisco-zenpack.png](img/zenpack-cisco-zenpack.png)
-   [cisco-zenpack.png](img/zenpack-cisco-zenpack.png)
-   [cisco-zenpack.png](img/zenpack-cisco-zenpack.png)


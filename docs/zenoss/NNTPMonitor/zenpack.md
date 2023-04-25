# NNTP Monitor

@lb[](img/zenpack-zenpack-general.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.NNTPMonitor

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-3488){.external-link}

### Applications Monitored:

NNTP (Network News Transfer Protocol)

## NNTP Monitor ZenPack

NNTPMonitor monitors the response time of an NNTP server in
milliseconds.

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Background

The ZenPacks.zenoss.NNTPMonitor ZenPack monitors the response time of
Network News Transfer Protocol (NNTP) servers.

The response time unit of measurement is milliseconds.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.2 or higher |
| Required ZenPacks | ZenPacks.zenoss.NNTPMonitor               |

## Enable Monitoring

To enable monitoring for a device:

1.  Select Infrastructure from the navigation bar.

2.  Click the device name in the device list. The device overview page
    appears.

3.  Expand Monitoring Templates, and then select Device from the left
    panel.

4.  Select Bind Templates from the Action menu. The Bind Templates
    dialog appears.

5.  Add the NNTPMonitor template to the list of selected templates, and
    then click **Submit**. The NNTPMonitor template is added to the list
    of monitoring templates.

6.  Select the template and change options as needed.

7.  Validate your configuration by running zencommand and observing that
    the check_nntp or check_nntps command correctly connects to your
    NNTP server:

        zencommand run -v10 -d yourdevicenamehere

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


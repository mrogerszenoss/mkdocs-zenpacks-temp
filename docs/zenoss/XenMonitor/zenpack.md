# Xen Virtual Hosts

@lb[](img/zenpack-citrix-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.XenMonitor

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-5803){.external-link}

### Applications Monitored:

Xen

## Xen Virtual Hosts ZenPack

The XenMonitor ZenPack allows you to monitor Xen para-virtualized
domains with Zenoss.
Note: This ZenPack is deprecated has been superseded by
[http://wiki.zenoss.org/ZenPack:XenServer](https://help.zenoss.com/display/in/){.external-link}

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Background

The ZenPacks.zenoss.XenMonitor ZenPack monitors Xen para-virtualized
domains.

With this ZenPack, the zenmodeler can discover guests running on Xen
hosts, and Zenoss platform includes screens and templates for collecting
and displaying resources allocated to guests.

## Prerequisites

|                   |                                                                     |
|-------------------|---------------------------------------------------------------------|
| Prerequisite      | Restriction                                                         |
| Product           | Zenoss platform 4.x                                                 |
| Required ZenPacks | ZenPacks.zenoss.XenMonitor ZenPacks.zenoss.ZenossVirtualHostMonitor |

## Model Hosts and Guest

For each Xen server, follow this procedure:

1.  Optionally, place an SSH key to your Xen server to allow the zenoss
    user from the Zenoss platform server to log in as root without
    requiring further credentials.
2.  Create the Xen server in the /Servers/Virtual Hosts/Xen device
    class. Warning: If you have this server modeled already, remove the
    server and recreate it under the Xen device class. Do not move it.
3.  Select the Guest menu and ensure that the guest hosts were found
    during the modeling process.

## Daemons

|                       |            |
|-----------------------|------------|
| Type                  | Name       |
| Modeler               | zenmodeler |
| Performance Collector | zencommand |

## Monitoring with sudo

To configure sudo in order to run the xm on the Virtual Machine Host,
you will need to modify a few things.

-   Modify the zCommandPath zProperty to be blank, otherwise this path
    will be pre-pended to the sudo command.
-   Modify the zCommandUsername and zCommandPassword configuration
    properties to be a non-root user with sudo access to the xm command.
-   Modify the Xen.py modeler to add the sudo command. The modeler can
    be found under the
    $ZENHOME/ZenPacks/ZenPacks.zenoss.ZenossVirtualHostMonitor
    directory, under the modeler/plugins directory.
-   Modify the performance templates.
    1.  Navigate to the /Devices/Server/Virtual Machine Host/Xen device
        class
    2.  From the device class click on the Templates tab
    3.  Click on the VirtualMachine performance template
    4.  In the Data Sources table, click on the resources Data Source
    5.  Edit the command template to add the sudo command to the
        beginning of the xm command

## Attachments:

-   [citrix-zenpack.png](img/zenpack-citrix-zenpack.png)
-   [citrix-zenpack.png](img/zenpack-citrix-zenpack.png)
-   [citrix-zenpack.png](img/zenpack-citrix-zenpack.png)
-   [citrix-zenpack.png](img/zenpack-citrix-zenpack.png)


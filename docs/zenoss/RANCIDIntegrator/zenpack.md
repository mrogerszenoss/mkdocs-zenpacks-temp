# RANCID Integration

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.RANCIDIntegrator

### Applications Monitored:

RANCID

## RANCID Integration ZenPack

The RANCID Integrator ZenPack allows Zenoss to work in conjunction with
Shrubbery Networks' RANCID (Really Awesome New Cisco confIg Differ)

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.RANCIDIntegrator ZenPack enables integration between
the RANCID configuration management tool and Zenoss platform.

The integration points are:

-   Zenoss platform will build the router.db file for
    [RANCID](http://www.shrubbery.net/rancid/){.external-link}. This
    allows for the centralization of administration activities and
    reduces the duplication of effort normally required to maintain the
    two tools.
-   Implementation of this feature is as easy as adding a cron job to
    execute $ZENHOME/bin/zenrancid to update the router.db file.
-   Zenoss platform will automatically run RANCID's rancid-runm tool on
    a single device in response to a `ciscoConfigManEvent` SNMP trap
    being sent from the device to Zenoss platform. Cisco devices will
    send this trap whenever their configuration is changed. This allows
    for real-time capturing of router configuration changes in your CVS
    repository.

Note: The RANCID integrator is dependent on a connection to the Zope
server, hence it can run only on the Zenoss platform master and as such
works only with managed resources on the master.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.2 or higher |
| Required ZenPacks | ZenPacks.zenoss.RANCIDIntegrator          |

## Configure Cisco Devices to Send Traps

To implement this feature you must configure your Cisco devices to send
their SNMP traps to the Zenoss platform server.

Link from Cisco device status pages to the most recent configuration
stored in your CVS repository via
[viewvc](http://www.viewvc.org/){.external-link}.

## Configure RANCID Update Information in Zenoss platform

1.  From Infrastructure &gt;Devices, click the device in the device
    list.
2.  Select Configuration Properties in the left panel.
3.  Edit the appropriate configuration properties for the device.

    RANCID Configuration Properties
    |              |                                                                                                                                                                                       |
    |--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Name         | Description                                                                                                                                                                           |
    | zRancidRoot  | File system directory where RANCID is installed. It may be NFS mounted from the RANCID server. Default is /opt/rancid                                                                 |
    | zRancidUrl   | Base URL to viewvc                                                                                                                                                                    |
    | zRancidGroup | RANCID group attribute. Controls what router.db file the device is written to. Can be set at the device class or device level. Default is `router` on the /Network/Router/Cisco class |
    | zRancidType  | RANCID type attribute. Controls what device type is written to the router.db file. Can be set at the device class or device level. Default is `cisco` on the /Network/Router/Cisco    |

4.  Click Save to save your changes.

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


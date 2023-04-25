# SugarCRM

@lb[](img/zenpack-sugar-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.SugarCRMMonitor

### Applications Monitored:

SugarCRM

## SugarCRM ZenPack

The SugarCRMMonitor ZenPack allows you to monitor SugarCRM services.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.SugarCRMMonitor ZenPack monitors SugarCRM services.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.2 or higher |
| Required ZenPacks | ZenPacks.zenoss.SugarCRMMonitor           |

## Configuring Zenoss platform

All SugarCRM devices must exist under the /Devices/Web/SugarCRM device
class.

1.  Navigate to the device or device class under the
    /Devices/Server/Tomcat device class in the Zenoss platform
    interface.
    -   If applying changes to a device class:
        1.  Select the class in the devices hierarchy.
        2.  Click **Details**.
        3.  Select Configuration Properties.
    -   If applying changes to a device:
        1.  Click the device in the device list.
        2.  Select Configuration Properties.
2.  Edit the appropriate configuration properties for the device or
    devices.

    SugarCRM Configuration Properties
    |                      |                                                    |
    |----------------------|----------------------------------------------------|
    | Name                 | Description                                        |
    | zSugarCRMBase        |                                                    |
    | zSugarCRMPassword    | Password for the zSugarCRMUsername user.           |
    | zSugarCRMTestAccount |                                                    |
    | zSugarCRMUsername    | Username allowed to log into the Sugar CRM server. |

3.  Click Save to save your changes.
4.  From the left panel, select Device under Monitoring Templates.
5.  Select Bind Templates from the Action menu. The Bind Templates
    dialog appears.
6.  Move the SugarCRM template from the Available list to the Selected
    list.
7.  Click **Save**. The SugarCRM template should now be displayed under
    the Monitoring Templates for Device. You will now be able to start
    collecting the Sugar CRM metrics from this device.
8.  Navigate to Graphs and you should see some placeholders for graphs.
    After approximately fifteen minutes you should see the graphs start
    to become populated with information.

## Daemons

|                       |            |
|-----------------------|------------|
| Type                  | Name       |
| Performance Collector | zencommand |

## Attachments:

-   [sugar-zenpack.png](img/zenpack-sugar-zenpack.png)
-   [sugar-zenpack.png](img/zenpack-sugar-zenpack.png)


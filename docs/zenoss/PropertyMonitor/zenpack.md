# PropertyMonitor

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

ZenPacks.zenoss.PropertyMonitor

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.PropertyMonitor){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.PropertyMonitor.git){.external-link}

## PropertyMonitor ZenPack

This ZenPack provides support for monitoring any numeric property of any
Zenoss component.

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 1.1.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.PropertyMonitor/1.1.1/ZenPacks.zenoss.PropertyMonitor-1.1.1.egg){.external-link}:   **Summary of changes:** Fix errors that can occur with components
    with certain characters in their IDs (ZPS-293):   Released on 2015/10/30:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.x

<!-- -->

Version 1.1.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.PropertyMonitor/1.1.0/ZenPacks.zenoss.PropertyMonitor-1.1.0.egg){.external-link}:   **Summary of changes:** Ignore ping issues on monitoring devices.
:   Released on 2015/10/30:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.x

<!-- -->

Version 1.0.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.PropertyMonitor/1.0.0/ZenPacks.zenoss.PropertyMonitor-1.0.0.egg){.external-link}:   **Summary of changes:** Initial Release:   Released on 2014/11/17:   Compatible with Zenoss Core 4.2.x, Zenoss Resource Manager 4.2.x

## Background

This ZenPack provides support for monitoring any numeric property of any
Zenoss component.

## Features

This ZenPack provides a new datasource type ("Property"), which allows
you to pull the current numeric value of any numeric property of any
zenoss Device or DeviceComponent object.

These datasources may then be used in monitoring templates to build
graphs and thresholds.

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Configuration Properties
</dt>
</dl>

-   zPropertyMonitorInterval: Polling interval of the configured
    property data sources. This is a systemwide setting, and defaults to
    300 (5 minutes)

<dl markdown="1">
<dt markdown="1">
Datasource Types
</dt>
</dl>

-   Property

<dl markdown="1">
<dt markdown="1">
Collector Daemons
</dt>
</dl>

-   zenpropertymonitor

## Changes

<dl markdown="1">
<dt markdown="1">
1.1.1
</dt>
</dl>

-   Fix errors that can occur with components with certain characters in
    their IDs (ZPS-293)

<dl markdown="1">
<dt markdown="1">
1.0.0
</dt>
</dl>

-   Initial release.

## Attachments:

-   [Edit_datasource.png](img/zenpack-edit_datasource.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [Edit_datasource.png](img/zenpack-edit_datasource.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [Edit_datasource.png](img/zenpack-edit_datasource.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [Edit_datasource.png](img/zenpack-edit_datasource.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


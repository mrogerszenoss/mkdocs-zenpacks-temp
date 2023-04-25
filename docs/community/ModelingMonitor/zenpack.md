# ModelingMonitor

@lb[](img/zenpack-zenpack-general.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

argaliev

### Maintainers:

argaliev

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.community.ModelingMonitor

### More Information:

[GitHub page/HomePage](https://github.com/argaliev/ZenPacks.community.ModelingMonitor){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/argaliev/ZenPacks.community.ModelingMonitor.git){.external-link}

## ModelingMonitor ZenPack

This ZenPack provides datasource ModelingMonitorDataSource to get
information about modeling status

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.0.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.ModelingMonitor/1.0.0/ZenPacks.community.ModelingMonitor-1.0.0.egg){.external-link}:   **Summary of changes:** First release:   Released on 2016/07/15:   Compatible with Zenoss Core 4.2.x

## Background

#### Description

This ZenPack provides datasource ModelingMonitorDataSource to get
information about modeling status. Zenpack check last modelling time of
device and number of component classes, that must be presented in
device. How it can be usefull:
- When you applied several modeler on device, and some of them wasn't
create expected component classes, this will trigger an event. I my
case, there was snmp plugin, that returns no data and failed events,
until special vendor drivers was installed.
- When, for some reason, modelling was performing later than given time
ago(in days)

#### Requirements & Dependencies

       * Zenoss Versions Supported: > 4.0
       * External Dependencies:
       * ZenPack Dependencies:
       * Installation Notes: zenhub and zopectl restart after installing this ZenPack.
       * Configuration:

#### Installation

Normal Installation (packaged egg)

------------------------------------------------------------------------

Copy the downloaded .egg to your Zenoss server and run the following
commands as the zenoss user::

      * zenpack --install <package.egg>
      * zenhub restart
      * zopectl restart

Developer Installation (link mode)

------------------------------------------------------------------------

If you wish to further develop and possibly contribute back to this
ZenPack you should clone the git repository, then install the ZenPack in
developer mode::

      * zenpack --link --install <package>
      * zenhub restart
      * zopectl restart

zProperties

------------------------------------------------------------------------

     - **zCompClassCount** - number of class components that expected to appear in device
     - **zExpiryDaysPast** - number of days when last modeling time become outdated
     - **zModelingMonitorInterval** - time interval to perform monitor

Monitoring Templates

------------------------------------------------------------------------

     - **/Devices/Server/rrdTemplates/ModelingMonitor**

Event Classes

------------------------------------------------------------------------

     - **/Status/Modeling**
     - **/Status/Modeling/ComponentMismatch**
     - **/Status/Modeling/ModelTimeExpired**

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


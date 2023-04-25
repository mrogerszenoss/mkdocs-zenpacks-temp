# TrueNAS

@lb[](img/zenpack-truenas-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

f.noushi

### Maintainers:

f.noushi

### Organization:

iXsystems

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.iXsystems.TrueNAS

### Git Sources (For Cloning):

[Link](https://github.com/N-faycal/ZenPacks.iXsystems.TrueNAS.git){.external-link}

### Applications Monitored:

TrueNAS (9.3)

FreeNAS (9.3)

## TrueNAS ZenPack

Monitoring of FreeNAS/TrueNAS servers with auto-discovery feature for
pools and datasets

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 0.9.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.iXsystems.TrueNAS/0.9.0/ZenPacks.iXsystems.TrueNAS-0.9.0.egg){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x

## Background

## Notes

This ZenPack relies on SNMP to extract performance metrics as well as
discovering pools and datasets.Therefore, the correct community has to
be set. Apart from SNMP-based monitoring, FreeNAS/TrueNAS events are
also translated to Zenoss events. Dismissing them on the web interface
clears them on Zenoss. Syslog monitoring can also be enabled on the web
interface regardless of this ZenPack's installation.

## Usage

Before installing the ZenPack, be sure to install PyYAML as the Zenoss
user:

       easy_install PyYAML

The ZenPack provides a device class named TrueNAS nested under
/Server/Linux. FreeNAS/TrueNAS devices should be added to that class,
configured then modelled. Below a list of zProperties added by the
ZenPack.

|                        |                                                                   |
|------------------------|-------------------------------------------------------------------|
| zProperty              | Description                                                       |
| zTrueNASLogin          | FreeNAS/TrueNAS web login. Used to extract alerts from the API    |
| zTrueNASPass           | FreeNAS/TrueNAS web password. Used to extract alerts from the API |
| zTrueNASIgnorePools    | List of pools to ignore on modeling.                              |
| zTrueNASIgnoreDatasets | List of datasets to ignore on modeling.                           |

## Attachments:

-   [truenas-zenpack.png](img/zenpack-truenas-zenpack.png)
-   [truenas-zenpack.png](img/zenpack-truenas-zenpack.png)
-   [truenas-zenpack.png](img/zenpack-truenas-zenpack.png)


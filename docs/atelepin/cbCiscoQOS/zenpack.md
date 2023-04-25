# Cisco Base QOS

@lb[](img/zenpack-cisco-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Andrey Telepin

### Maintainers:

Andrey Telepin

### Organization:

atelepin

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.atelepin.cbCiscoQOS

### Git Sources (For Cloning):

[Link](https://github.com/atelepin/ZenPacks.atelepin.cbCiscoQOS){.external-link}

## Cisco Base QOS ZenPack

Gather information about QOS objects like ClassMap

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.2- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.atelepin.cbCiscoQOS/1.2/ZenPacks.atelepin.cbCiscoQOS-1.2.egg){.external-link}:   Compatible with Zenoss Core 3.1.x, Zenoss Core 3.2.x

## Background

This project is a Zenoss extension (ZenPack) primarily intended for ISPs
which extensively use different QoS on their network (like MPLS), and
need to know statistics by each class.

About Cisco Base QOS on Cisco site

This is prerelease but all main functionality work. Almost think i need
change or add write in the code as TODO or FIXME

## Overview

Because ServicePolicy bound to Interface (IpInterface), installation
create additional relation between cbServicePolicy and IpInterface.
ZenPack contain automated modeler which grab QOS Object configuration
from device. From this configuration modeler create particular class
instance and create hierarchy of that objects (see more about nested
object in cisco site).

In this release i collect only two statistic item PostPolicyBitRate and
PostPolicyDropRate. From code point of view each statistic item is
different component, but from user point of view, this item belong to
cbServicePolicy and statistics should be visible as single item (for
example on single graph). In this case cbServicePolicy work not only as
container but also provide internal API to gather statistic from his
child.

## Known issues

1.  For to see SPGraphReport need manualy change
    Product/ZenModel/ReportClass.py line 133 to
    spec=('Report','DeviceReport','GraphReport','MultiGraphReport',
    'SPGraphReport')):
2.  For enable "change button" in Report manualy change

<!-- -->

      Products/Zen3UI/browser/resources/js/zenoss/Report.js comments

      /* Ext.getCmp('edit-button').setDisabled
         (!/^(Device |(Multi)?Graph)Report$/.test(attrs.meta_type)); */

## Requirements & Dependencies

-   Zenoss Versions Supported: 3.x

## Attachments:

-   [cisco-zenpack.png](img/zenpack-cisco-zenpack.png)
-   [cisco-zenpack.png](img/zenpack-cisco-zenpack.png)
-   [cisco-zenpack.png](img/zenpack-cisco-zenpack.png)


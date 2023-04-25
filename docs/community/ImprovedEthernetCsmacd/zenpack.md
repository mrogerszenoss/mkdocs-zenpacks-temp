# Improved EthernetCsmacd

@lb[](img/zenpack-zenpack-general.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Nick Muir

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.community.ImprovedEthernetCsmacd

### More Information:

[GitHub page/HomePage](https://github.com/nickmuir/ZenPacks.community.ImprovedEthernetCsmacd){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/nickmuir/ZenPacks.community.ImprovedEthernetCsmacd.git){.external-link}

## Improved EthernetCsmacd ZenPack

Provides additional network interface monitoring

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.0.1-beta- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.ImprovedEthernetCsmacd/1.0.1-beta/ZenPacks.community.ImprovedEthernetCsmacd-1.0.1-beta.egg){.external-link}:   Released on 2016/05/13:   Compatible with Zenoss Core 4.2.x

## Background

Creates a ethernetCsmacd_64 monitoring template on /network that
includes the regular ethernetCsmacd_64 datasources/graphs and adds:

Datasources/datapoints:

-   ifHCInMulticastPkts
-   ifHCOutMulticastPkts
-   ifHCInBroadcastPkts
-   ifHCInBroadcastPkts

Graphs

-   Broadcast Packets
-   Multicast Packets

Thresholds

-   Errors (Raises event on 10 errors or more)

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


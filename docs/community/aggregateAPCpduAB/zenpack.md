# APC PDU Aggregate A-B Monitor

@lb[](img/zenpack-apc-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

nianderson

### Maintainers:

nianderson

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.community.aggregateAPCpduAB

### More Information:

[GitHub page/HomePage](http://github.com/nickanderson/ZenPacks.community.aggregateAPCpduAB){.external-link}

### Link To More Docs:

[View Documentation](https://github.com/nickanderson/ZenPacks.community.aggregateAPCpduAB/blob/master/README.txt){.external-link}

### Git Sources (For Cloning):

[Link](http://github.com/nickanderson/ZenPacks.community.aggregateAPCpduAB.git){.external-link}

### Devices Monitored:

APC Rack PDU

## APC PDU Aggregate A/B Monitor ZenPack

This ZenPack aggregates the total AMP load from two APC PDUs.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.aggregateAPCpduAB/1.1/ZenPacks.community.aggregateAPCpduAB-1.1.egg){.external-link}:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.1.x, Zenoss Core
    3.2.x, Zenoss Core 4.2.x, Zenoss Resource Manager 4.1.x

## Background

This ZenPack aggregates the total AMP load from two APC PDUs.

Example Situation:

-   1 Rack
-   2 20A circuits
-   1 PDU for each circuit.

Each piece of equipment has redundant power supplies and has access to
both legs of power. This allows one circuit to fail without bringing
down equipment. In order to ensure that failure of one circuit does not
cause the second circuit to overload and fail the aggregate AMP load
must be monitored.



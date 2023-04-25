# VMware Data Source

@lb[](img/zenpack-vmware-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Eric Enns

### Maintainers:

Eric Enns

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.community.VMwareDataSource

### More Information:

[GitHub page/HomePage](http://community.zenoss.org/docs/DOC-10242){.external-link}

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-10242){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/ericenns/ZenPacks.community.VMwareDataSource.git){.external-link}

### Applications Monitored:

VSphere

## VMware Data Source ZenPack

This ZenPack gathers performance data from VSphere hosts (ESX/ESXi)
using the VSphere Perl SDK.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.1.2- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.VMwareDataSource/1.1.2/ZenPacks.community.VMwareDataSource-1.1.2.egg){.external-link}:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.2.x

<!-- -->

Version 1.1.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.VMwareDataSource/1.1.1/ZenPacks.community.VMwareDataSource-1.1.1.egg){.external-link}:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.2.x

## Background

### Introduction

Currently there are only two allowed datasources, VMwareHost and
VMwareGuest. There are a few in development, and as I have time I will
continue to add more. The data is collected by backend perl scripts
which use the Vsphere Perl SDK. Would like to transition a python api
but none are currently available, there is a pshere project but it
hasn't been tested enough to be a reliable option
<http://bitbucket.org/jkinred/psphere/src/tip/psphere/>. This zenpack is
currently only being used by ZenPacks.community.VMwareESXiMonitor.

### Notes

The device that you want to get performance data needs to be added into
zenoss with it's fqdn (fully qualified domain name, also this must be
lowercase because fqdn is case sensitive and will stay this way) as it's
device name. If you followed the instructions in VMwareESXiMonitor I
gave on how to add a device you would be gathering performance data with
no problem.

### Installation

First install the dependencies. Secondly install the zenpack from
command line or gui as usual and you are set to go.

### Dependencies

VMware VSphere Perl SDK:   [available here](http://www.vmware.com/support/developer/viperltoolkit){.external-link}

## Attachments:

-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)


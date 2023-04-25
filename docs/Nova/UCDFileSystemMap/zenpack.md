# UCD FileSystem

@lb[](img/zenpack-zenpack-general.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Ryan Matte

### Maintainers:

Ryan Matte

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.Nova.UCDFileSystemMap

### More Information:

[GitHub page/HomePage](http://community.zenoss.org/docs/DOC-10286){.external-link}

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-10286){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.Nova.UCDFileSystemMap.git){.external-link}

## UCD FileSystem ZenPack

This ZenPack is for monitoring filesystems via a different MIB than
HOST-RESOURCES (which Zenoss uses by default).

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.2- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.Nova.UCDFileSystemMap/1.2/ZenPacks.Nova.UCDFileSystemMap-1.2.egg){.external-link}:   Compatible with Zenoss Core 3.1.x, Zenoss Core 3.2.x

## Background

This ZenPack is for monitoring filesystems via a different MIB than
HOST-RESOURCES (which Zenoss uses by default). The main application for
this pack is as follows. If you are running net-snmp on a Solaris
server, and AutoMountFS is in use on that server, every time someone
logs in to the server their home directory gets automatically mounted.
It is then unmounted when they log out. The problem with this is that it
wreaks havoc on the SNMP indexes for the filesystems making it
impossible for Zenoss to properly monitor them.

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


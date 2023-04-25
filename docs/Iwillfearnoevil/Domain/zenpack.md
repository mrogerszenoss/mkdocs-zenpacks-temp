# Domain-SSL Certificate Expiration Monitor

@lb[](img/zenpack-zenpack-general.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Christopher Hubbard

### Maintainers:

Christopher Hubbard

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.Iwillfearnoevil.Domain

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.Iwillfearnoevil.Domain){.external-link}

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-4551){.external-link}

### Git Sources (For Cloning):

[Link](http://github.com/zenoss/ZenPacks.Iwillfearnoevil.Domain.git){.external-link}

## Domain/SSL Certificate Expiration Monitor ZenPack

This ZenPack check on the expiration date of domain and SSL
certificates.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.0.6- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.Iwillfearnoevil.Domain/1.0.6/ZenPacks.Iwillfearnoevil.Domain-1.0.6.egg){.external-link}:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.1.x, Zenoss Core
    3.2.x, Zenoss Core 4.2.x

## Background

This ZenPack check on the expiration date of domain and SSL
certificates. The ZenPack will create **/Devices/Ping/Domain** and
**/Devices/Ping/Domain/SSL**. Since zProperties are inherited, this
isolates domain checks that dont necessairly have SSL from SSL enabled
domains.



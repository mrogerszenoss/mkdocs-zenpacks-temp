# Apache Virtual Host Modeler

@lb[](img/zenpack-apache-zenpack.png)

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

ZenPacks.community.ApacheVirtualHost

### More Information:

[GitHub page/HomePage](https://github.com/nickmuir/ZenPacks.community.ApacheVirtualHost){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/nickmuir/ZenPacks.community.ApacheVirtualHost.git){.external-link}

## Apache Virtual Host Modeler ZenPack

Models Apache virtual hosts using a command modeler running apachectl -S

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.0.4-beta- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.ApacheVirtualHost/1.0.4-beta/ZenPacks.community.ApacheVirtualHost-1.0.4-beta.egg){.external-link}:   Released on 2016/04/29:   Compatible with Zenoss Core 4.2.x

## Background

Assign the modeler plugin to any device under /server and it will model
then monitor the Virtual Hosts

Monitoring template requires nagios check_http plugin

Any sites running on 443 will be monitored as HTTPS and they will have
the TLS certificate checked and events raised if the expiry time is 30
days or less

If the modeler gets a Syntax Error back from apachectl check that your
configs are fine and that the user running apachectl has sufficient
permissions to read all the necessary files

Noticed on SuSE based distros that the command is apache2ctl... for now
I have been linking apachectl to it.

## Attachments:

-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)


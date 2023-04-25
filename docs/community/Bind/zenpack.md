# Bind

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

ZenPacks.community.Bind

### More Information:

[GitHub page/HomePage](https://github.com/nickmuir/ZenPacks.community.Bind){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/nickmuir/ZenPacks.community.Bind.git){.external-link}

## Bind ZenPack

Monitoring Bind via rdnc stats

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.0.3-beta- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.Bind/1.0.3-beta/ZenPacks.community.Bind-1.0.3-beta.egg){.external-link}:   Released on 2016/03/16:   Compatible with Zenoss Core 4.2.x

## Background

This zenpack uses rndc to generate statistics for bind. The stats are
parsed via a python script which is executed from a command data source.

Setup steps:

-   Configure the server for rndc
    (<https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s2-bind-rndc.html)->
-   Setup a cronjob to run rndc stats every 5 minutes
-   Copy the script/namedstats.py to the server you want to montior (I
    use puppet for this)
-   Update the Bind monitoring template to point to where the script
    resides and the path to the named.stats file
-   Set the command username and password of an account with sufficient
    privildeges to read the named.stats file - I used an account which
    is in the named group

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


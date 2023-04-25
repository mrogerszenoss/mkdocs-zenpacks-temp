# Rundeck

@lb[](img/zenpack-rundeck-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

David Petzel

### Maintainers:

David Petzel

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.community.Rundeck

### Git Sources (For Cloning):

[Link](https://github.com/dpetzel/ZenPacks.community.Rundeck.git){.external-link}

### Applications Monitored:

Rundeck (1.5.x)

## Rundeck ZenPack

Monitors Rundeck

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.0.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.Rundeck/1.0.0/ZenPacks.community.Rundeck-1.0.0.egg){.external-link}:   **Summary of changes:** Initial Release:   Released on 2013/06/10:   Compatible with Zenoss Core 3.2.x, Zenoss Core 4.2.x

## Background

This ZenPack enables to Zenoss to monitor
[Rundeck](http://rundeck.org/){.external-link}, by leveraging the
[Rundeck API](http://rundeck.org/docs/api/index.html){.external-link}.
It will add the following new items to your Zenoss installation:

-   A new Monitoring Template - **Rundeck**
-   3 new zProperties:
    -   zRundeckAPIPort - This is the HTTP/HTTPS port that the Rundeck
        API is listening on. Defaults to 4440
    -   zRundeckAPIToken - The Zenpack will leverage the API Token for
        authentication to the API. Currently password authentication is
        **not supported**. There is no default value for this property,
        you will need to supply a value before stats are collected.
    -   zRundeckAPIScheme - Determines if Zenoss will use HTTP or HTTPS
        when communicating with the API. The default is http. Valid
        values are http or https (lower case)

## Configuration

In order to leverage this ZenPack there are two important tasks you will
need to complete.

1.  The first thing you need to do is create (or use an existing)
    Rundeck account and generate an APIToken. You should review the
    [official Rundeck documentation](http://rundeck.org/docs/api/index.html#token-authentication){.external-link}
    on the steps necessary to accomplish that.
2.  Once you have your API Token in hand, you will need to enter this
    value into the **zRundeckAPIToken** zProperty. The steps necessary
    to update a zProperty are discussed in the [official Zenoss Administration guide](http://community.zenoss.org/community/documentation/official_documentation/zenoss-guide){.external-link},
    and you should refer to the section titled **Configuration
    Properties**

## Screen Shots

[@lb[](img/zenpack-zenpacks.community.rundeck_memory.png)](https://help.zenoss.com/sites/default/files/zenpack/Rundeck/ZenPacks.community.Rundeck_memory.PNG "Rundeck Memory Usage")

[@lb[](img/zenpack-zenpacks.community.rundeck_loadavg.png)](https://help.zenoss.com/sites/default/files/zenpack/Rundeck/ZenPacks.community.Rundeck_loadavg.PNG "Rundeck Load Average (As reported via the API)")

[@lb[](img/zenpack-zenpacks.community.rundeck_projects.png)](https://help.zenoss.com/sites/default/files/zenpack/Rundeck/ZenPacks.community.Rundeck_projects.PNG "Rundeck Projects")

[@lb[](img/zenpack-zenpacks.community.rundeck_totaljobs.png)](https://help.zenoss.com/sites/default/files/zenpack/Rundeck/ZenPacks.community.Rundeck_totaljobs.PNG "Total Jobs")

## Attachments:

-   [rundeck-zenpack.png](img/zenpack-rundeck-zenpack.png)
-   [ZenPacks.community.Rundeck_loadavg.PNG](img/zenpack-zenpacks.community.rundeck_loadavg.png)
-   [ZenPacks.community.Rundeck_memory.PNG](img/zenpack-zenpacks.community.rundeck_memory.png)
-   [ZenPacks.community.Rundeck_projects.PNG](img/zenpack-zenpacks.community.rundeck_projects.png)
-   [ZenPacks.community.Rundeck_totaljobs.PNG](img/zenpack-zenpacks.community.rundeck_totaljobs.png)
-   [rundeck-zenpack.png](img/zenpack-rundeck-zenpack.png)
-   [ZenPacks.community.Rundeck_loadavg.PNG](img/zenpack-zenpacks.community.rundeck_loadavg.png)
-   [ZenPacks.community.Rundeck_memory.PNG](img/zenpack-zenpacks.community.rundeck_memory.png)
-   [ZenPacks.community.Rundeck_projects.PNG](img/zenpack-zenpacks.community.rundeck_projects.png)
-   [ZenPacks.community.Rundeck_totaljobs.PNG](img/zenpack-zenpacks.community.rundeck_totaljobs.png)
-   [rundeck-zenpack.png](img/zenpack-rundeck-zenpack.png)
-   [ZenPacks.community.Rundeck_loadavg.PNG](img/zenpack-zenpacks.community.rundeck_loadavg.png)
-   [ZenPacks.community.Rundeck_memory.PNG](img/zenpack-zenpacks.community.rundeck_memory.png)
-   [ZenPacks.community.Rundeck_totaljobs.PNG](img/zenpack-zenpacks.community.rundeck_totaljobs.png)
-   [ZenPacks.community.Rundeck_projects.PNG](img/zenpack-zenpacks.community.rundeck_projects.png)


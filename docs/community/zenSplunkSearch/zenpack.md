# Splunk Search Component

@lb[](img/zenpack-splunk-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Joseph Anderson

### Maintainers:

Joseph Anderson

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.community.zenSplunkSearch

### More Information:

[GitHub page/HomePage](https://github.com/j053ph4/ZenPacks.community.zenSplunkSearch){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/j053ph4/ZenPacks.community.zenSplunkSearch.git){.external-link}

## Splunk Search Component ZenPack

Perform Splunk searches within Zenoss

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 2.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.zenSplunkSearch/2.0/ZenPacks.community.zenSplunkSearch-2.0.egg){.external-link}:   **Summary of changes:** Zenoss 4.x support, migrated to
    ConstructionKit:   Released on 2013/03/20:   Requires [ConstructionKit ZenPack](https://help.zenoss.com/display/in/constructionkit "ZenPack:ConstructionKit"){.external-link}:   Compatible with Zenoss Core 3.2.x, Zenoss Core 4.2.x

<!-- -->

Version 2.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.zenSplunkSearch/2.1/ZenPacks.community.zenSplunkSearch-2.1.egg){.external-link}:   **Summary of changes:** updated to support ConstructionKit 2.0:   Released on 2013/11/05:   Requires [ConstructionKit ZenPack](https://help.zenoss.com/display/in/constructionkit "ZenPack:ConstructionKit"){.external-link}:   Compatible with Zenoss Core 4.2.x

## Background

This ZenPack provides a "Splunk Search" component and allows for the
execution of Splunk Searches within Zenoss.

Each "Splunk Search" component has a "query" property that contains the
query string.

Connection parameters are defined in zProperties, but can be overriden
on a per component basis

The component data is passed to a "check_splunk.py" script that was
copied/modified from an earlier community ZenPack that no longer seems
to be available.

## Attachments:

-   [splunk-zenpack.png](img/zenpack-splunk-zenpack.png)
-   [splunk-zenpack.png](img/zenpack-splunk-zenpack.png)
-   [splunk-zenpack.png](img/zenpack-splunk-zenpack.png)


# Duration Threshold (Community)

@lb[](img/zenpack-zenpack-general.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

agaliev

### Maintainers:

argaliev

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.community.DurationThreshold

### More Information:

[GitHub page/HomePage](https://github.com/argaliev/ZenPacks.community.DurationThreshold){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/argaliev/ZenPacks.community.DurationThreshold.git){.external-link}

## ZenPacks.community.DurationThreshold

Version 1.0.0- Download:

    Summary of changes: First release Released on 2016/07/07 Compatible with Zenoss Core 4.2.x

## Description

This ZenPack adds a new Duration Threshold type for determining when to
trigger an event. The threshold count average value for datapoints in
the time interval.

## Requirements & Dependencies

> -   Zenoss Versions Supported: &gt; 4.0
> -   External Dependencies:
> -   ZenPack Dependencies:
> -   Installation Notes: zenhub and zopectl restart after installing
>     this ZenPack.
> -   Configuration:

## Installation

### Normal Installation (packaged egg)

Copy the downloaded .egg to your Zenoss server and run the following
commands as the zenoss user:

    * zenpack --install <package.egg> * zenhub restart * zopectl restart

### Developer Installation (link mode)

If you wish to further develop and possibly contribute back to this
ZenPack you should clone the git repository, then install the ZenPack in
developer mode:

    * zenpack --link --install <package> * zenhub restart * zopectl restart

## Configuration

Tested with Zenoss 4.2.5

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


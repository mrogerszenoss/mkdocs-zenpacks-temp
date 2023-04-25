# IBM V7000 Storwize

@lb[](img/zenpack-ibm-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

emcrispim

### Maintainers:

emcrispim

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.community.IBMV7000

### More Information:

[GitHub page/HomePage](https://github.com/emcrispim/ZenPacks.community.IBMV7000){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/emcrispim/ZenPacks.community.IBMV7000.git){.external-link}

## IBM V7000 Storwize ZenPack

IBM V7000 Storwize Monitoring Through SSH

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.0.3- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.IBMV7000/1.0.3/ZenPacks.community.IBMV7000-1.0.3.egg){.external-link}:   Released on 2015/10/12:   Compatible with Zenoss Core 4.2.x

## Background

This ZenPack will monitor the IBMV7000 Storwize. In the instalation
process will create a new device class organizer "/Storage/IBMV7000"
with local defined configuration properties.

#### CONFIGURATION

A user account is required in order to login against the IBMV7000 SSH
service. The account only requires a low level permission ("Monitor"
User Group). This can be achieved by adding/changing a user within the
web console, browsing menu:

-   access &gt; users

Use the account in the follow Configurations Properties

-   zCommandUsername
-   zCommandPassword

Altough the IBMV7000 SSH service can also be
authenticated with SSH Keys.

##### MODELER PLUGINS

-   community.cmd.IBMV7000

##### MONITORING TEMPLATES

-   IBMV7000

##### PERFORMANCE GRAPHS

-   CPU utilization
-   Interfaces throughput
-   Volumes
    -   Read and Write (MBps)
    -   Read and Write Latency (ms)
-   MDisks
    -   Read and Write (MBps)
    -   Read and Write Latency (ms)

## Attachments:

-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)
-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)
-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)


# Siebel CRM Components

@lb[](img/zenpack-siebel-zenpack.png)

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

ZenPacks.community.zenSiebelCRM

### More Information:

[GitHub page/HomePage](http://community.zenoss.org/docs/DOC-12921){.external-link}

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-12921){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/j053ph4/ZenPacks.community.zenSiebelCRM.git){.external-link}

### Applications Monitored:

Siebel CRM Application Server

## Siebel CRM Components ZenPack

This Zenpack provides modeling and monitoring of the Siebel CRM
Application Server.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 2.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.zenSiebelCRM/2.0/ZenPacks.community.zenSiebelCRM-2.0.egg){.external-link}:   Released on 2013/04/02:   Requires [ConstructionKit ZenPack](https://help.zenoss.com/display/in/constructionkit "ZenPack:ConstructionKit"){.external-link}:   Compatible with Zenoss Core 3.2.x, Zenoss Core 4.2.x

<!-- -->

Version 1.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.zenSiebelCRM/1.0/ZenPacks.community.zenSiebelCRM-1.0.egg){.external-link}:   Compatible with Zenoss Core 3.2.x

<!-- -->

Version 2.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.zenSiebelCRM/2.1/ZenPacks.community.zenSiebelCRM-2.1.egg){.external-link}:   Released on 2013/05/16:   Requires [ConstructionKit ZenPack](https://help.zenoss.com/display/in/constructionkit "ZenPack:ConstructionKit"){.external-link}:   Compatible with Zenoss Core 3.2.x, Zenoss Core 4.2.x

<!-- -->

Version 2.7- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.zenSiebelCRM/2.7/ZenPacks.community.zenSiebelCRM-2.7.egg){.external-link}:   **Summary of changes:** updated to support ConstructionKit 2.0,
    added object relations to WinService:   Released on 2013/11/05:   Requires [ConstructionKit ZenPack](https://help.zenoss.com/display/in/constructionkit "ZenPack:ConstructionKit"){.external-link}:   Compatible with Zenoss Core 4.2.x

## Background

Developed by: Joseph Anderson Description:

This Zenpack provides modeling and monitoring of the Siebel CRM
Application Server.

       No agent or changes needed on the remote server.
       Tested against Windows, but should support mutliple platforms
       Provides component-level modeling of Siebel CRM Application subcomponents
       Collects an average of 112 data points per component
           subcomponents may have different data points available
           component template can be easily localized and datapoints added
           data collection script will provide this data without modification

(Nagios format)

This ZenPack is very heavily inspired by the recently released "Siebel
CRM Monitoring" Zenpack, and this author owes an enormous debt of
gratitude to the author of that ZenPack, for sharing his knowledge and
expertise. I can say personally that there is a strong need for this
capability, and extremely few open-source options providing it.

Although it was comprehensive, that ZenPack was unsuitable for our
environment (we have an extensive Siebel deployment). This ZenPack
"repackages" the best parts of the other one while simplifying its
deployment and configuration. It's construction/layout is perhaps also
better taylored to the conventional Zenoss Administration conventions.

Rather than specifying the specific Siebel component against which to
collect data, this ZenPack models the remote server and creates
components corresponding to all available subcomponents. These
subcomponents are then modeled and managed as typical device
"components" (such as a file system).

Components:

The ZenPack provides the following

       SiebelComponent Template provides:
           Data Sources
               SiebelStatus returns number corresponding to component status
               SiebelTasks returns the number of total tasks, good tasks, and bad tasks
               SiebelPerf returns performance statistics per component
           Thresholds
               various (Min/Max)
       ZenModeler plugins:
           siebelComponentMap
       Event Class:
           /App/Siebel
       zensiebelperf collector daemon

Installation:

This ZenPack relies on a local install of the "srvrmgr" binary that
ships with Siebel Enterprise Server. That binary must reside on the
Zenoss server, as all commands to the remote server are performed
through it. It is assumed that a working installation exists, and that
the srvrmgr binary is symlinked to /opt/zenoss/libexec (the zenpack
install will attempt to do this). The srvrmgr binary may also require
modified permissions to run (mine is 755).

If /opt/zenoss/libexec/srvrmgr works as the "zenoss" user, then the
configuration is likely correct.

New Device zProperties are added (these correspond to the command-line
arguments of srvmgr):

       zSiebelEnterprise
       zSiebelGateway
       zSiebelServer
       zSiebelUser
       zSiebelPassword

All are required for the modeler/data source to function.

A "Siebel" Device class should be added at some level of the Devices
heirarchy, with the following:

       zCollectorPlugins should contain siebelComponentMap in the list of modeler

plugins

Requirements:

       Zenoss Versions Supported: 3.x, 4.x
       External Dependencies: see above notes
       ZenPack Dependencies:
       Installation Notes: zopectl restart; zenhub restart; zensiebelperf

restart after installing this ZenPack.

       Configuration: see above notes

History:

Change History:

       1.0 initial release
       1.5
           3 datasources added to collect state, task, and performance data
           zensiebelperf daemon added to collect data and serialize data collection
           support for useMonitoredAttribute added to javascript
           support for manual deletion of components added to SiebelComponent
       2.0 rebuilt to support Construction Kit and Zenoss 4.x
       2.7 support for ConstructionKit 2.0

Tested: This ZenPack was tested with Zenoss versions 3.x and Zenoss 4.x

Source: <https://github.com/zenoss/ZenPacks.community.zenSiebelCRM>

Known issues: None

## Attachments:

-   [siebel-zenpack.png](img/zenpack-siebel-zenpack.png)
-   [siebel-zenpack.png](img/zenpack-siebel-zenpack.png)
-   [siebel-zenpack.png](img/zenpack-siebel-zenpack.png)


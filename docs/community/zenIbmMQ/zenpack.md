# IBM WebSphere MQ Components

@lb[](img/zenpack-ibm-zenpack.png)

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

ZenPacks.community.zenIbmMQ

### More Information:

[GitHub page/HomePage](http://community.zenoss.org/docs/DOC-12919){.external-link}

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-12919){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/j053ph4/ZenPacks.community.zenIbmMQ.git){.external-link}

### Applications Monitored:

Websphere MQ

## IBM WebSphere MQ Components ZenPack

This Monitoring Zenpack provides monitoring of MQ Managers, Channels,
and Queues for IBM Websphere MQ.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.zenIbmMQ/1.0/ZenPacks.community.zenIbmMQ-1.0.egg){.external-link}:   Compatible with Zenoss Core 3.2.x, Zenoss Resource Manager 4.1.x

<!-- -->

Version 1.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.zenIbmMQ/1.1/ZenPacks.community.zenIbmMQ-1.1.egg){.external-link}:   Released on 2012/04/02:   Compatible with Zenoss Core 3.2.x

<!-- -->

Version 2.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.zenIbmMQ/2.0/ZenPacks.community.zenIbmMQ-2.0.egg){.external-link}:   **Summary of changes:** ConstructionKit support (3.x, 4.x compat),
    other minor revisions:   Released on 2013/04/02:   Requires [ConstructionKit ZenPack](https://help.zenoss.com/display/in/constructionkit "ZenPack:ConstructionKit"){.external-link}:   Compatible with Zenoss Core 3.2.x, Zenoss Core 4.2.x

<!-- -->

Version 2.1:   **Summary of changes:** trying to fix auto-build issues:   Released on 2013/05/15:   Requires [ConstructionKit ZenPack](https://help.zenoss.com/display/in/constructionkit "ZenPack:ConstructionKit"){.external-link}:   Compatible with Zenoss Core 3.2.x, Zenoss Core 4.2.x

<!-- -->

Version 2.2- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.zenIbmMQ/2.2/ZenPacks.community.zenIbmMQ-2.2.egg){.external-link}:   **Summary of changes:** updated to support ConstructionKit 2.0,
    rewrote data parser and changed modeler plugins to multiplatform:   Released on 2013/11/05:   Requires [ConstructionKit ZenPack](https://help.zenoss.com/display/in/constructionkit "ZenPack:ConstructionKit"){.external-link}:   Compatible with Zenoss Core 4.2.x

## Background

This Monitoring Zenpack provides monitoring of MQ Managers, Channels,
and Queues for IBM Websphere MQ.

       No agent is needed on the remote server.
       Support for Windows and Unix-based platforms
       Provides component-level modeling of the IBM MQ application components.

This ZenPack was inspired by the "IBM Websphere MQ ZenPack", and I'm
grateful to its author for sharing some of his expertise regarding MQ.

I have been using a shell script to monitor specific MQ Queues on
Windows/Unix servers for a couple of years. The good thing about the
script is that it requires minimal support to run against Windows and
Unix servers. The bad part is that all of the MQ-specific paramters
(Manager, Queue) have to be supplied to it. It is also a pain to use to
monitor multiple queues on a single machine, as new command definitions
have to be made on a locally bound template that differ only in the
command line options. A component-based template provides a much better
solution, while the modelling scripts remove the need to keep track of
the needed parameters.

Components:

The ZenPack has the following Device Class(es)

       /Server/Linux/MQ, /Server/Windows/MQ Device Classes
           MQManager Template provides:
               Data Sources
                   mgr-status-nix (Command)
                   mgr-status-win (Command)
               Thresholds
                   Manager Status (Min/Max)
           MQQueue Template provides:
               Data Sources
                   queue-status-nix (Command)
                   queue-status-win (Command)
               Thresholds
                   Queue Depth (Min/Max)
           MQChannel Template provides:
               Data Sources
                   channel-status-nix (Command)
                   channel-status-win (Command)
       ZenModeler plugins:
           MqManagerMap
           MqQueueMap
           MqChannelMap

           Common (shared class--do not use as a plugin)
       Event Class:
           /App/MQ

Installation:

After installing this Zenpack as usual, ensure that the authentication
zProperties are set for Windows and Unix-based servers respectively.

SSH requires username/password, assumes mqm is the MQ user.

WINEXE on later Windows versions (2003(?) and up) may fail with an error
similar to "problem installing winexesvc". This can be corrected by
running the following commands from the Command Prompt (on the Windows
server):

             sc create winexesvc binPath= WINEXESVC.EXE start= auto DisplayName=

winexesvc

             sc description winexesvc "Remote command provider for Zenoss

monitoring"

## Attachments:

-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)
-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)
-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)


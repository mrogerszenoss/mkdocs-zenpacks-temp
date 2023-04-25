# JMX Notification Listener

@lb[](img/zenpack-oracle-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.zenoss.JMXNotificationListener

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.JMXNotificationListener){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.JMXNotificationListener.git){.external-link}

### Applications Monitored:

JMX Notifications

## JMX Notification Listener ZenPack

Capture JMX notifications as Zenoss events.

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 0.9.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.JMXNotificationListener/0.9.0/ZenPacks.zenoss.JMXNotificationListener-0.9.0.egg){.external-link}:   **Summary of changes:** Initial release.
:   Released on 2013/02/03:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.1.x, Zenoss Core
    3.2.x, Zenoss Core 4.2.x, Zenoss Resource Manager 4.1.x, Zenoss
    Resource Manager 4.2.x

## Background

This ZenPack allows
[JMX](http://en.wikipedia.org/wiki/Java_Management_Extensions){.external-link}
[notifications](http://docs.oracle.com/javase/tutorial/jmx/notifs/index.html){.external-link}
to be captured as Zenoss events.

See
[ZenPacks.zenoss.ZenJMX](https://help.zenoss.com/display/in/){.external .external-link}
for a ZenPack that allows polling of metrics from MBean attributes and
operations.

## Usage

To collect JMX notifications you must edit
*$ZENHOME/etc/zenjmxnotificationlistener.conf*. This file must be used
to specify which JMX agents to connect to, and what notifications to
collect. After modifying this file you must run
*zenjmxnotificationlistener restart* for the changes to be affected.

Upon installing the ZenPack a default *zenjmxnotificationlistener.conf*
will be created with the following contents.

    # Generic configuration
    monitorName=localhost
    heartbeatInterval=60
    heartbeatTimeout=75
    connectionRetryInterval=10

    # Zenoss XML-RPC connection properties
    # xmlRpcUrl is the zenhub url
    xmlRpcUrl=http://localhost:8081/zport/dmd/ZenEventManager
    xmlRpcUsername=admin
    xmlRpcPassword=zenoss

    # Each comma-delimited token in serverList must have at least a
    # server.TOKEN.url= entry specified below.
    #serverList=LOCAL_TOMCAT,LOCALHOST
    serverList=LOCALHOST

    # Properties where <TOKEN> matches one of the entries in the serverList property
    # server.TOKEN.zenossDevice is REQUIRED
    # server.TOKEN.url is REQUIRED
    # server.TOKEN.scope is OPTIONAL and defaults to *:* or all notification mbeans
    # server.TOKEN.username is OPTIONAL and defaults to null
    # server.TOKEN.password is OPTIONAL and defaults to null
    # server.TOKEN.attributeFilters is OPTIONAL, filter for attributes of interest

    # example Definitions for a local Tomcat instance
    #server.LOCAL_TOMCAT.zenossDevice=bixby
    #server.LOCAL_TOMCAT.url=service:jmx:rmi:///jndi/rmi://10.204.210.40:11111/jmxrmi
    #server.LOCAL_TOMCAT.scope=Catalina:type=RequestProcessor
    #server.LOCAL_TOMCAT.attributeFilters=attribOne,attribTwo
    #server.LOCAL_TOMCAT.username=zenjmxnl
    #server.LOCAL_TOMCAT.password=GOAWAY!

    server.LOCALHOST.zenossDevice=localhost
    server.LOCALHOST.url=service:jmx:rmi:///jndi/rmi://localhost:54107/jmxrmi

The *scope* and *attributeFilters* properties are optional, and can be
used to restrict the notifications captured from a given server.
MBeanServerNotification type notifications are ignored by default as
they are noisy and unlikely to be useful.

## Attachments:

-   [oracle-zenpack.png](img/zenpack-oracle-zenpack.png)
-   [oracle-zenpack.png](img/zenpack-oracle-zenpack.png)
-   [oracle-zenpack.png](img/zenpack-oracle-zenpack.png)
-   [oracle-zenpack.png](img/zenpack-oracle-zenpack.png)


# JBoss Application Server

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.JBossMonitor

### Applications Monitored:

JBoss

## JBoss Application Server ZenPack

This ZenPack allows system administrators to monitor JBoss Appliciation
Servers.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 2.4.2- [Download](https://zenoss.leapfile.net/){.external-link}:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x

## Background

The ZenPacks.zenoss.JBossMonitor ZenPack monitors JBoss application
servers.

This ZenPack uses the JMX Remote API and accesses MBeans deployed within
JBoss that contain performance information about the components that are
being managed. The collected performance information includes: pool
sizes for data sources (JDBC), Enterprise Java Beans (EJBs), message
queues (JMS), threads, servlets, JSPs, and classloaders. Cache
information is also accessible, providing system administrators insight
into the number of hits (or misses) their cache policy has produced.

This ZenPack also aggregates individual performance metrics into higher
level concepts that provide a picture of the performance of the
application. Cache hits and misses are combined on the same graph to
provide an overall picture of cache performance. Likewise, queue metrics
are combined to show the number of messages currently on the queue,
being processed, and being placed on the queue. Queue subscribers and
publishers are also graphed.

Each of the individual performance metrics can be trended and predicted,
and thresholds can be explicitly defined. Both the predicted thresholds
and explicit thresholds inform system administrators of potential future
problems before they occur. Since so much of J2EE involves "managed
resources", the ability to monitor pool sizes and alert administrators
prior to resources being exhausted is extremely valuable and can reduce
the likelihood of a fatal outage caused by resource depletion.

Most of the metrics represent combinations of individual component
metrics. For example, the Thread Pool metric represents all threads in
all pools. It is possible to configure this ZenPack to perform at higher
granularity and have it monitor a Thread Pool with a particular name.
However, since these names are application specific we have chosen to
configure this ZenPack to collect at a rather coarse-grained level by
default. The installer is highly encouraged to customize and configure!

One particular monitoring template that requires end-user configuration
involves Servlets. If a site to be monitored is revenue generating, and
credit card submissions from the website are handled via a back-end
servlet, it may be critically important to monitor the resources made
available by the JBoss container to the servlet container. If the number
of free spaces in the servlet pool dwindles to zero it could prevent
your application from making a sale.

The following are the collected metrics for JBoss servers:

-   Active Threads
-   JMS Message cache memory usage
-   JMS Message hits/misses
-   JMS Topic/Destination queue size
-   Java heap memory usage
-   JCA commit, rollback, and transaction count
-   JCA Connection pool in-use connections and available connections
-   JCA connections created/destroyed
-   JCA total connections
-   JGroups cluster messages sent/received
-   JGroups cluster bytes sent/received
-   MBean creation/removal count
-   MBean messages processed count

## Prerequisites

<table>
<colgroup>
<col />
<col />
</colgroup>
<tbody>
<tr markdown="1">
<th width="50%">Prerequisite</th>
<th width="50%">Restriction</th>
</tr>

<tr markdown="1">
<td>Product</td>
<td>Zenoss platform 4.x, Zenoss 2.2 or higher</td>
</tr>
<tr markdown="1">
<td>Required ZenPacks</td>
<td>ZenPacks.zenoss.ZenJMX,
<p>ZenPacks.zenoss.JBossMonitor</p></td>
</tr>
</tbody>
</table>

## Configuring JBoss to Allow JMX Queries

JBoss uses the JAVA_OPTS approach for enabling remote access to MBeans.
However, it requires some additional properties. To set up your
JAVA_OPTS for use in JBoss see the following code segment:

    JAVA_OPTS="-Dcom.sun.management.jmxremote.port=12345"
    JAVA_OPTS="${JAVA_OPTS} -Dcom.sun.management.jmxremote.authenticate=false"
    JAVA_OPTS="${JAVA_OPTS} -Dcom.sun.management.jmxremote.ssl=false"
    JAVA_OPTS="${JAVA_OPTS} -Djboss.platform.mbeanserver"
    JAVA_OPTS="${JAVA_OPTS} -Djavax.management.builder.initial=org.jboss.system\
    .server.jmx.MBeanServerBuilderImpl"
    export JAVA_OPTS

When you start JBoss via the run.sh you must also pass the "-b 0.0.0.0"
argument:

    cd ${JBOSS_HOME}/bin
    ./run.sh -b 0.0.0.0

JMX actually uses two separate ports for MBean access: one is used for
initial connection handling and authentication, and the other is used
for RMI access. During the handshake between a JMX Client and the JMX
Agent the agent tells the client the IP address and port number for the
RMI registry. By default JBoss sets the IP address to 127.0.0.1. This
works when the JMX client and the JMX agent reside on the same device,
but it won't work in a distributed environment.

By passing the "-b 0.0.0.0" argument you instruct JBoss to bind to all
available network ports, and this results in the JMX Agent's handshaking
logic using a network reachable address when informing clients of the
RMI registry hostname and port.

The `jmx-console` Web page in JBoss allows you to view the different
MBeans that are available; however, this does not mean that these MBeans
are available remotely. If JConsole can view MBeans, then so can the
zenjmx daemon that gathers this information.

## Configuring Zenoss platform

All JBoss services must have a device entry under the
/Devices/Server/JBoss device class.

Note: The zenjmx daemon must be configured and running. .

1.  Navigate to the device or device class in the Zenoss platform
    interface.
    -   If applying changes to a device class:
        1.  Select the class in the devices hierarchy.
        2.  Click **Details**.
        3.  Select Configuration Properties.
    -   If applying changes to a device:
        1.  Click the device in the device list.
        2.  Select Configuration Properties.
2.  Edit the appropriate configuration properties for the device or
    devices.

    JBoss Configuration Properties
    | Name                            | Description                                    |
    |---------------------------------|------------------------------------------------|
    | zJBossJmxManagementAuthenticate | This configuration property is deprecated.     |
    | zJBossJmxManagementPassword     | JMX password                                   |
    | zJBossJmxManagementPort         | The port number used to gather JMX information |
    | zJBossJmxManagementUsername     | JMX username for authentication                |

3.  Click Save to save your changes. You will now be able to start
    collecting the JBoss server metrics from this device.
4.  Navigate to Graphs and you should see some placeholders for graphs.
    After approximately fifteen minutes you should see the graphs start
    to become populated with information.

Tip: The out-of-the-box JBoss data source configuration has been defined
at the macro level, but can be configured to operate on a more granular
basis. For example, the Servlet Reload Count applies to all servlets in
all Web applications but it could be narrowed to be Servlet /submitOrder
in Web application "production server."

## Change the Amount of Data Collected and Graphed

1.  Navigate to the device or device class under the
    /Devices/Server/JBoss device class in the interface.
2.  In the left panel, select Monitoring Templates
3.  Select Bind Templates from the Action menu.
4.  To add other templates and retain existing monitoring templates,
    hold down the control key while clicking on the original entries.

    JBoss Templates

    | Name                      | Description                                                                           |
    |---------------------------|---------------------------------------------------------------------------------------|
    | JBoss Core                | Core information about any JBoss server, including memory usage, threads, and uptime. |
    | JBoss JCA Connection Pool |                                                                                       |
    | JBoss JGroups Channel     |                                                                                       |
    | JBoss JMS Cache           |                                                                                       |
    | JBoss JMS Destination     |                                                                                       |
    | JBoss JMS Topic           |                                                                                       |
    | JBoss Message Driven EJB  |                                                                                       |

5.  Click the OK button to save your changes.

## Viewing Raw Data

\[\[../../../../../../ZenPacks.zenoss.ZenJMX/ZenPacks/zenoss/ZenJMX/dox/topics/JConsole.html\|../../../../../../ZenPacks.zenoss.ZenJMX/ZenPacks/zenoss/ZenJMX/dox/topics/JConsole.html\]\].

## Daemons

| Type                  | Name   |
|-----------------------|--------|
| Performance Collector | zenjmx |

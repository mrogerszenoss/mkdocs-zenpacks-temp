# Apache Tomcat

@lb[](img/zenpack-apache-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.TomcatMonitor

### Applications Monitored:

Apache Tomcat

## Apache Tomcat ZenPack

This ZenPack allows you to monitor the Tomcat Application Server. Tomcat
is a Web application container that conforms to many parts of the J2EE
Specification.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 2.3.0- [Download](https://zenoss.leapfile.net/){.external-link}:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x

## Background

The ZenPacks.zenoss.TomcatMonitor ZenPack monitors Apache Tomcat
servers.

Tomcat is a Web application container that conforms to many parts of the
J2EE Specification.

This ZenPack focuses on the metrics that Tomcat updates in its internal
MBean container that is accessible via the remote JMX API. These metrics
focus on attributes that relate to the servicing of web pages and
primarily include thread pool size, CPU use, available file descriptors,
JSP and servlet counts, and request counts.

This ZenPack places much emphasis on monitoring thread status because
every web request is serviced in a separate thread. Each thread requires
file descriptors to be maintained, and thus those are monitored as well.
The amount of CPU time spent servicing each thread is also captured and
reported.

This ZenPack also reports on the number of times JSPs and Servlets are
reloaded. This metric can be useful in highly dynamic sites where JSPs
or Servlets change on the fly and need to be reloaded periodically.
Monitoring of this metric can lead to the identification of small
"Reloading Storms" before they cause production outages.

The amount of time Tomcat spends servicing a request is also recorded.
This extremely high level metric can provide insight into downstream
systems that are not monitored. If all the Tomcat resources are within
normal tolerances but processing time suddenly spikes it can be an
indication that a back-end service (such as a database or another web
service) is misbehaving.

The following metrics can be collected and graphed:

-   Tomcat cache (accesses vs hits)
-   Daemon and User thread count
-   Overall CPU time
-   Global Request Traffic: bytes sent/received
-   Global Request Traffic: request count and error count
-   Global Request processing time
-   JSP/Servlet reload time
-   Servlet class loading and processing time
-   Servlet request and error count

Tip: The more extensive JBoss Application Server uses Tomcat as a Web
Application engine to manage web applications deployed inside enterprise
applications within JBoss. As a result, this ZenPack can be used to
monitor Tomcat MBeans that are active within JBoss.

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
<p>ZenPacks.zenoss.TomcatMonitor</p></td>
</tr>
</tbody>
</table>

## Configuring Tomcat to Allow JMX Queries

Before running the Tomcat bin/start.sh script, run the following to
allow unsecured queries against the Tomcat server:

    JAVA_OPTS="-Dcom.sun.management.jmxremote.port=12346"
    JAVA_OPTS="${JAVA_OPTS} -Dcom.sun.management.jmxremote.authenticate=false"
    JAVA_OPTS="${JAVA_OPTS} -Dcom.sun.management.jmxremote.ssl=false"
    export JAVA_OPTS

The same JAVA_OPTS approach can be used to enable remote access to
Tomcat MBeans. Set the JAVA_OPTS variable as illustrated above and then
execute the ./catalina.sh start command in the ${TOMCAT_HOME}/bin
directory.

Note: Tomcat 6.0.14's catalina.sh does not process the stop command
properly when the JAVA_OPTS variable is set. We recommend using two
separate shell scripts when troubleshooting JMX problems in Tomcat: one
for starting Tomcat (with the JAVA_OPTS variable set) and a different
one for stopping Tomcat (where the JAVA_OPTS variable is not set).

If you add the above lines to the to bin/setenv.sh (as seems to be the
logical thing to do in catalina.sh to get the environment variables set
up), the bin/shutdown.sh script will get those same environment
variables. This will cause the shutdown.sh script to attempt to bind to
the ports, fail, and then not stop Apache Tomcat.

## Configuring Zenoss platform

All Apache Tomcat services must have a device entry under the
/Devices/Server/Tomcat device class.

Note: The zenjmx daemon must be configured and running. See for more
information about configuring the zenjmx daemon with the Sun JRE tools.

1.  Navigate to the device or device class under the
    /Devices/Server/Tomcat device class in the Zenoss platform
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

    Tomcat Configuration Properties
    |                                    |                                                                                                                                                                                               |
    |------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Name                               | Description                                                                                                                                                                                   |
    | `zTomcatJ2EEApplicationName`       | Used to construct MBean names for a specific application deployed on Tomcat, typically used for JSP and Servlet statistics.                                                                   |
    | `zTomcatJ2EEServerName`            | Used to construct MBean names for a specific application deployed on Tomcat, typically used for JSP and Servlet statistics.                                                                   |
    | `zTomcatJmxManagementAuthenticate` | This configuration property is deprecated.                                                                                                                                                    |
    | `zTomcatJmxManagementPassword`     | JMX password.                                                                                                                                                                                 |
    | `zTomcatJmxManagementPort`         | The port number used to gather JMX information.                                                                                                                                               |
    | `zTomcatJmxManagementUsername`     | JMX username for authentication.                                                                                                                                                              |
    | `zTomcatListenHost`                | The hostname on which Tomcat is listening for web requests. This is used to construct MBean names.                                                                                            |
    | `zTomcatListenPort`                | The Tomcat connector, which is a port and protocol (http, jk...) that Tomcat is listening on. This is used to construct MBean names that monitor bytes, error and requests on that connector. |
    | `zTomcatServletName`               | Specific Servlet name to monitor.                                                                                                                                                             |
    | `zTomcatServletUri`                | URI of Servlet to monitor.                                                                                                                                                                    |
    | `zTomcatWebAppUri`                 | URI path for a Tomcat web application. Used to construct MBean names.                                                                                                                         |

3.  Click Save to save your changes. You will now be able to start
    collecting the Tomcat server metrics from this device.
4.  Navigate to Graphs and you should see some placeholders for
    performance graphs. After approximately fifteen minutes you should
    see the graphs start to become populated with information.

Tip: The out-of-the-box TomcatMonitor data source configuration has been
defined at the macro level, but can be configured to operate on a more
granular basis. For example, the Servlet Reload Count applies to all
servlets in all web applications but it could be narrowed to be Servlet
/submitOrder in web application "production server".

## Change the Amount of Data Collected and Graphed

1.  Navigate to the device or device class under the
    /Devices/Server/Tomcat device class in the Zenoss platform
    interface.
2.  From the left panel, select Monitoring Templates.
3.  From the Action menu, select Bind Templates.
4.  Move one or more templates to Selected, and then click **Save**.

    Tomcat Templates
    |                                   |                                                                               |
    |-----------------------------------|-------------------------------------------------------------------------------|
    | Name                              | Description                                                                   |
    | `Tomcat Cache`                    | Cache information about a specific Web application deployed.                  |
    | `Tomcat Core`                     | Core information about any Tomcat server: memory usage, threads, uptime, etc. |
    | `Tomcat Global Request Processor` | Connection information over a Tomcat connector: bytes, errors, requests.      |
    | `Tomcat JSPS`                     | Metrics about a specific JSP page.                                            |
    | `Tomcat Servlet`                  | Metrics about a specific Servlet.                                             |
    | `Tomcat Thread Pool`              | Threadpool metrics measured per Tomcat connector.                             |
    | `Tomcat Web Module`               | Processing time metrics for a Web module.                                     |

5.  Click the OK button to save your changes.

## Viewing Raw Data

\[\[../../../../../../ZenPacks.zenoss.ZenJMX/ZenPacks/zenoss/ZenJMX/dox/topics/JConsole.html\|../../../../../../ZenPacks.zenoss.ZenJMX/ZenPacks/zenoss/ZenJMX/dox/topics/JConsole.html\]\].

## Daemons

|                       |        |
|-----------------------|--------|
| Type                  | Name   |
| Performance Collector | zenjmx |

## Attachments:

-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)
-   [apache-zenpack.png](img/zenpack-apache-zenpack.png)


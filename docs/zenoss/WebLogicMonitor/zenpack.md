# Oracle WebLogic Server

@lb[](img/zenpack-oracle-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.WebLogicMonitor

### Applications Monitored:

Oracle WebLogic Server

## Oracle WebLogic Server ZenPack

This ZenPack allows you to monitor an Oracle WebLogic Server.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 2.3.0- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2017/07/24:   Requires [ZenPacks.zenoss.ZenJMX ZenPack](https://help.zenoss.com/display/in/zenpackszenosszenjmx-page-does-not-exist "ZenPack:ZenPacks.zenoss.ZenJMX (page does not exist){.external-link}"):   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.x

<!-- -->

Version 2.2.3- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2016/01/14:   Requires [ZenPacks.zenoss.ZenJMX ZenPack](https://help.zenoss.com/display/in/zenpackszenosszenjmx-page-does-not-exist "ZenPack:ZenPacks.zenoss.ZenJMX (page does not exist){.external-link}"):   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.x

## Background

The ZenPacks.zenoss.WebLogicMonitor ZenPack monitors Oracle WebLogic
Server services.

This ZenPack uses the JMX Remote API and and accesses MBeans deployed
within WebLogic that contain performance information about the
components that are being managed. This performance information includes
pool sizes for data sources (JDBC), threads, connections (JCA), queues
(JMS), servlets, JSPs, Enterprise Java Beans (EJB), timer queues.

Throughput is also monitored when it is available. This metric is
computed by WebLogic and is based on the number of messages moving
through a queue at any given time. The throughput metric gives a good
picture of the health of the messaging subsystem, which is commonly used
throughout many enterprise applications. Stateless, Stateful, and Entity
EJB performance metrics are monitored, as are message driven bean
performance.

Security realms are also monitored for potential denial of service
attacks. This includes recording of authentication failures, broken out
by valid accounts, invalid accounts, and accounts that are currently
locked out. Application specific realms can be monitored by customizing
the built in WebLogic default realm.

## Overall Application Server Vitals

-   Number of total and active JMS connections and servers
-   Overall number of JTA transactions that are rolled back or abandoned
-   JTA transactions rolled back due to system, application, or resource
    issues
-   Number of JTA rollbacks that timeout
-   Active and committed JTA transaction count
-   Timer exceptions, executions, and scheduled triggers
-   User accounts that are locked and unlocked
-   Authentication failures against locked accounts and non-existent
    accounts
-   Total sockets opened, and the current number of open sockets
-   JVM Mark/Sweep and Scavenge garbage collector execution counts
-   Number of JVM daemon threads
-   JVM Heap/Non-Heap used and committed memory

## Entity EJB, Message Driven Bean (MDB), and Session EJB Subsystem Metrics

-   Rollback and commit count on a per-EJB basis
-   Bean pool accesses, cache hits, and cache misses
-   Number of Beans in use, idle, and destroyed
-   Number of activations and passivations

## Data Pool (JDBC) metrics

-   Leaked, Total, and Active connections
-   Number of requests waiting for a connection
-   Number of reconnect failures

## Queue (JMS) Metrics

-   Bytes received, currently active, and pending in the queue
-   Number of queue consumers
-   Number of current, pending, and receives messages

## Prerequisites

WebLogic 10.0 or higher is required.

## Configuring WebLogic to Allow JMX Queries

To enable remote JMX access set the following variables in
"startWebLogic.sh" (Linux) or "startWebLogic.cmd" (Windows):

    set JAVA_OPTIONS=%JAVA_OPTIONS% -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=12347 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false -Djavax.management.builder.initial=weblogic.management.jmx.mbeanserver.WLSMBeanServerBuilder

This file normally located in "bin" directory under your domain. For
example on Windows with domain "base_domain" this may be
"C:\\Oracle\\Middleware\\user_projects\\domains\\base_domain\\bin\\startWebLogic.cmd"

Open it with text editor and search for "echo WLS Start
Mode=%WLS_DISPLAY_MODE%" line. Put JAVA options above after this line.
Then save file and restart WebLogic. Now you have your 12347 port binded
to JMX queries from Zenoss (zJmxManagementPort property). This port
number may be changed due to your needs.

Depending on your OS security, it may be required to add appropriate
rule to firewall.

## Configuring Zenoss platform

All WebLogic services must have a device entry under the
/Devices/Server/WebLogic device class.

Note: The zenjmx daemon must be configured and running. See
[ZenPack:Java_2\_Platform_Standard_Edition\_(J2E){.external-link}](https://help.zenoss.com/display/in/Java+2+Platform+Standard+Edition+-+J2E "ZenPack:Java 2 Platform Standard Edition (J2E){.external-link}")
for more information about configuring the zenjmx daemon with the Sun
JRE tools.

1.  Navigate to the device class or device.
    -   If applying changes to a device class:
        1.  Select the class in the devices hierarchy.
        2.  Click **Details**.
        3.  Select Configuration Properties.
    -   If applying changes to a device:
        1.  Click the device in the device list.
        2.  Select Configuration Properties.
2.  Edit the appropriate configuration properties for the device or
    devices.

    WebLogic Configuration Properties
    |                                    |                                                |
    |------------------------------------|------------------------------------------------|
    | Name                               | Description                                    |
    | zWebLogicJmxManagementAuthenticate | This configuration property is deprecated      |
    | zWebLogicJmxManagementPassword     | JMX password                                   |
    | zWebLogicJmxManagementPort         | The port number used to gather JMX information |
    | zWebLogicJmxManagementUsername     | JMX username for authentication                |

3.  Click Save to save your changes. You will now be able to start
    collecting the WebLogic server metrics from this device.
4.  Navigate to Graphs and you should see some placeholders for
    performance graphs. After approximately 15 minutes you should see
    the graphs start to become populated with information.

Tip: The out-of-the-box WebLogic data source configuration has been
defined at the macro level, but can be configured to operate on a more
granular basis. For example, the Servlet Reload Count applies to all
servlets in all web applications but it could be narrowed to be Servlet
/submitOrder in web application "production server".

## Change the Amount of Data Collected and Graphed

For performance reasons you may reduce the amount of metrics retrieved.

1.  Navigate to the device or device class.
2.  Select Monitoring Templates in the left panel.
3.  From the Action menu, select Bind Templates to display the Bind
    Templates dialog.
4.  Move templates from the Available area to the Selected area, and
    then click **Save**.

    WebLogic Templates
    |                          |                                                                                          |
    |--------------------------|------------------------------------------------------------------------------------------|
    | Name                     | Description                                                                              |
    | WebLogic Core            | Core information about any WebLogic server, including memory usage, threads, and uptime. |
    | WebLogic JCA             |                                                                                          |
    | WebLogic JMS             |                                                                                          |
    | WebLogic JMS Destination |                                                                                          |
    | WebLogic JTA             |                                                                                          |
    | WebLogic JTA Rollbacks   |                                                                                          |
    | WebLogic JVM             |                                                                                          |
    | WebLogic Thread Pool     | Threadpool metrics measured per Tomcat connector                                         |
    | WebLogic Timer Service   |                                                                                          |
    | WebLogic User Lockouts   |                                                                                          |

5.  Click the OK button to save your changes.

## Viewing Raw Data

WebLogic has a tool to check with monitoring data - "WebLogic
ServerAdministration Console". By default it is available on:

<http://WEB_LOGIC_HOST:7001/console/dashboard>

To view raw data JConsole application from Java suite can be used. To
connect to WebLogic Server JMX point JConsole to:

service:jmx:rmi:///jndi/rmi://SERVER_IP:JMX_PORT/jmxrmi

## Monitor SSL-Proxied WebLogic Servers

If you are monitoring a Web application running on WebLogic server, you
may find that the transaction always fails with a code 550 regardless of
how you configure the script. This could be a result of the WebLogic
server being behind an SSL proxy. When used in this configuration,
WebLogic requires that a `WL-Proxy-SSL` header be added to the request
so that it knows to redirect to HTTPS instead of HTTP.

To support this extra header in your Zenoss platform Web transaction,
you must make the following changes on the script tab of your WebTx data
source.

-   Remove any content from the Initial URL field.

-   Add the following to the beginning of the Script box.

        add_extra_header WL-Proxy-SSL true
        go

## Monitor JDBC Datasources and JDBC Connection Pools

By default this template not binded to WebLogic device.

*WebLogic JDBC* monitoring template is an example of configuration. It
should be copied and modified to use with your JDBC datasources. In this
template *testds* datasource name should be changed to actual datasource
name.

To add additional JDBC metrics one may use
*http://WEB_LOGIC_HOST:7001/console/dashboard* monitoring dashboard and
set filters:

-   Servers: WEB_LOGIC_SERVER
-   Types: JDBCDataSource / JDBCConnectionPool
-   Instances: JDBC_DATASOURCE_NAME

Metrics list will be populated with available options. These may be set
as datasource params in *WebLogic JDBC* monitoring template.

To test these metrics on WebLogic dashboard new view (graph) may be
created. Then it is required to click "Run" button at left top corner to
run monitoring.

## Limitations

Depending on WebLogic server configuration it may happen that not all
JMX datapoints are collected. This may occur when all monitoring
templates are enabled. To deal with it turn off monitoring templates you
not interested in as described in "Change the Amount of Data Collected
and Graphed" section.

## Daemons

|                       |        |
|-----------------------|--------|
| Type                  | Name   |
| Performance Collector | zenjmx |

## Changes

<dl markdown="1">
<dt markdown="1">
2.3.0
</dt>
</dl>

-   Added JDBC monitoring template
-   Updated documentation for newer versions of WebLogic Server

<dl markdown="1">
<dt markdown="1">
2.2.3
</dt>
</dl>

-   Dropped support of 9.0
-   Updated monitoring templates for newer versions of WebLogic Server
-   Added tests

## Attachments:

-   [oracle-zenpack.png](img/zenpack-oracle-zenpack.png)
-   [oracle-zenpack.png](img/zenpack-oracle-zenpack.png)
-   [oracle-zenpack.png](img/zenpack-oracle-zenpack.png)


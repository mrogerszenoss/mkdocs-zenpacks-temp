# Java 2 Platform Standard Edition - J2E

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

ZenPacks.zenoss.ZenJMX

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.ZenJMX){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.ZenJMX.git){.external-link}

## Java 2 Platform Standard Edition (J2E) ZenPack

ZenJMX is a ZenPack that allows Zenoss Core to communicate with remote
Java Management Extensions (JMX) agents.

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 3.14.0- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2022/05/11:   Compatible with Zenoss 6.x and Zenoss Cloud

<!-- -->

Version 3.13.1- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2021/12/17:   Compatible with Zenoss 6.x and Zenoss Cloud

<!-- -->

Version 3.13.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.ZenJMX/3.13.0/ZenPacks.zenoss.ZenJMX-3.13.0.egg){.external-link}:   Released on 2020/10/26:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss
    Resource Manager 4.2.x, Zenoss Resource Manager 5.x

<!-- -->

Version 3.12.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.ZenJMX/3.12.1/ZenPacks.zenoss.ZenJMX-3.12.1.egg){.external-link}:   Released on 2016/01/08:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss
    Resource Manager 4.2.x, Zenoss Resource Manager 5.x

## Background

The ZenPacks.zenoss.ZenJMX ZenPack adds the zenjmx daemon, which
communicates with remote Java Management Extensions (JMX) agents, to
collect data from Java-based applications.

This ZenPack defines a data source named `JMX` that allows you to query
any single or complex-value attribute, or invoke an MBean operation. It
also comes with a built-in template named `Java` that contains MBean
information for a few beans built into the JVM.

Note: This ZenPack also includes a built-in template named `ZenJMX`.
This template should be used only on devices running Java applications
that make information available through JMX. To monitor other Java
applications, use the included Java template.

When the zenjmx daemon is started it communicates with its zenhub daemon
and retrieves a list of devices that possess `JMX` data sources. It also
spawns a Java process. The zenjmx daemon asynchronously issues queries
for each of those devices to the Java process via XML-RPC. The Java
process then collects the data from the Java application to be
monitored, and returns the results to the zenjmx daemon. Any collection
or configuration errors are sent as events to Zenoss platform and appear
in the event console.

Also, the zenjmx daemon sends heartbeat data to its zenhub daemon after
each collection attempt, to let Zenoss platform know it is still alive
and well.

## JMX Background

The JMX technology is used throughout the Java Virtual Machine to
provide performance and management information to clients. Using a
combination of JConsole (Oracle's JMX client that is shipped with the
JDK) and JMX, a system operator can examine the number of threads that
are active in the JVM or change the log level. There are numerous other
performance metrics that can be gleaned from the JVM, as well as several
management interfaces that can be invoked that change the behavior of
the JVM.

In Java 5, Oracle introduced the Remote API for Java Management
Extensions. This enhancement defines an RMI wrapper around a JMX agent
and allows for independent client development. The zenjmx daemon
accesses remote JMX agents via the Remote API for Java Management
Extensions. It currently does not support local connections (provided
via the temporary directory) to JMX Agents. JMX also specifies the
manner in which various protocols can be used to connect to clients, and
send and receive information. The original, most commonly used protocol
is RMI. The zenjmx daemon supports RMI and JMXMP connections.

## ZenJMX Capabilities

The zenjmx daemon is a full-featured JMX client that works "out of the
box" with JMX agents that have their remote APIs enabled. It supports
authenticated and unauthenticated connections, and it can retrieve
single-value attributes, complex-value attributes, and the results of
invoking an operation. Operations with parameters are also supported so
long as the parameters are primitive types (Strings, booleans, numbers),
as well as the object version of primitives (such as `java.lang.Integer`
and `java.lang.Float`). Multi-value responses from operations (Maps and
Lists) are supported, as are primitive responses from operations.

The `JMX` data source installed by this ZenPack allows you to define the
connection, authentication, and retrieval information you want to use to
retrieve performance information. The IP address is extracted from the
parent device, but the port number of the JMX Agent is configurable in
each data source. This allows you to operate multiple JMX Agents on a
single device and retrieve performance information for each agent
separately. This is commonly used on production servers that run
multiple applications.

Authentication information is also associated with each JMX data source.
This offers the most flexibility for site administrators because they
can run some JMX agents in an open, unauthenticated fashion and others
in a hardened and authenticated fashion. SSL-wrapped connections are
supported by the underlying JMX Remote subsystem built into the JDK, but
were not tested in the Zenoss labs. As a result, your success with SSL
encrypted access to JMX Agents may vary.

The data source allows you to define the type of performance information
you want to achieve: single-value attribute, complex-value attribute, or
operation invocation. To specify the type of retrieval, you must specify
an attribute name (and one or more data points) or provide operation
information.

Any numerical value returned by a JMX agent can be retrieved by Zenoss
platform and graphed and checked against thresholds. Non-numerical
values (Strings and complex types) cannot be retrieved and stored by
Zenoss platform.

When setting up data points, make sure you understand the semantics of
the attribute name and choose the correct Zenoss platform data point
type. Many JMX Agent implementations use inconsistent nomenclature when
describing attributes. In some cases the term "Count" refers to an
ever-increasing number (a "Counter" data point type). In other cases the
term "Count" refers to a snapshot number (a "Gauge" data point type).

## Allowable Parameter Types

The following primitive data types are allowed in `JMX` calls:

-   `java.lang.Integer`
-   `java.lang.Long`
-   `java.lang.Double`
-   `java.lang.Float`
-   `java.lang.String`
-   `java.lang.Boolean`
-   `int`
-   `long`
-   `double`
-   `float`
-   `boolean`

## Single Value Attribute Calls

This is the most basic usage scenario. If you are interested in
retrieving a single value from an MBean in a JMX Agent, and the
attribute returns simple numeric data, you fall into the "single value
attribute" category. To define a single-value attribute call simply
provide the fully qualified name of your MBean and then provide the name
of the attribute in the Attribute Name field of the data source. Lastly,
you must define a data point.

Some examples of this include the commonly referenced JDK Threading
information:

-   MBean Name: java.lang:type=Threading
-   Attribute Name: ThreadCount
-   Data Points:
    -   ThreadCount (type: gauge)

Java uses lots of file descriptors during normal operation. The number
of open file descriptors the JVM is working with can be measured using
the following information:

-   MBean Name: java.lang:type=OperatingSystem
-   Attribute Name: OpenFileDescriptorCount
-   Data Points:
    -   OpenFileDescriptorCount (type: gauge)

There are several other single-value attributes that can be retrieved
from the JDK. We recommend using JConsole to interactively navigate
through the MBean hierarchy to determine which MBeans contain useful
information to you. See for additional information on how to inspect the
MBeans deployed in an JMX Agent.

## Complex-Value Attribute Calls

If your MBean attribute defines multiple sub-attributes (via
CompositeData or Tabular) that you are interested in capturing, then you
fall into the category of a "complex-value attribute" call. The JDK
contains a few complex-value attributes you might be interested in
capturing, including garbage collection statistics that were captured
during the copy and mark-sweep compact collection cycles.

To extract data from a complex-value attribute, you must define one or
more data points in the data source. The names of the data points are
used as keys into the complex-value data structure returned from the
MBean attribute. For JMX CompositeData attributes, the data point names
are used as a key to map the results. For JMX TabularData, the data
point names are used as indexes into the structure to map the result.

The JDK also provides heap memory information via a complex-value
attribute. The amount of committed, used, and maximum heap memory can be
viewed by setting up a complex-value attribute in Zenoss platform with
the following information:

-   MBean Name: java.lang:type=Memory
-   Attribute Name: HeapMemoryUsage
-   Data Points:
    -   committed (type: gauge)
    -   used (type: gauge)
    -   max (type: gauge)

## Example Method Calls

Some management values need to be computed. These situations frequently
arise when custom MBeans are deployed alongside an enterprise
application. An MBean named "Accounting" might be deployed within an
enterprise application that defines operations intended for operators or
support staff. These operations might include methods such as
"getBankBalance()" or "countTotalDeposits()".

The zenjmx daemon can invoke operations, but there are some subtleties
in how it sends parameters to a JMX Agent, and interprets the response.

### No parameters, single return value

In the most basic usage scenario no arguments are passed to the
operation and a single value is returned. This usage scenario is very
similar to a single-value attribute call, except we're invoking an
operation to retrieve the value rather than accessing an attribute. The
configuration for this hypothetical usage scenario follows:

-   MBean Name: Application:Name=Accounting,Type=Accounting
-   Operation Name: getBankBalance()
-   Data Points:
    -   balance (type: gauge)

### No parameters, multiple values returned in List format

In this scenario no parameters are passed to an operation, but multiple
response values are provided in a List. The values returned are
expressed in a List &lt;object&gt; , but they are coerced (but not
casted) to doubles prior to being stored in Zenoss platform. This means
that returning a numeric value as "1234" will work, but "1,234" will not
work. The litmus test is to evaluate if
`Double.valueOf(object.toString())` will successfully evaluate.
&lt;/object&gt;

The zenjmx daemon can be configured to read multiple values from an
operation's results by defining multiple data points. You must define a
data point for each value returned from the operation, and if there is a
mismatch between the number of data points you define and the size of
the List &lt;object&gt; returned an exception will be generated. The
configuration for the zenjmx daemon follows: &lt;/object&gt;

-   MBean Name: Application:Name=Accounting,Type=Accounting
-   Operation Name: getBalanceSummary()
-   Data Points:
    -   dailyBalance (type: gauge)
    -   annualBalance (type: gauge)

### No parameters, multiple values returned in Map format

In this scenario no parameters are passed to an operation, but multiple
response values are provided in a Map&lt;String, Object&gt;. The keyset
of the Map contains the names of data points that can be defined, and
the values are the values of said data points. When a Map&lt;String,
Object&gt; is returned you need not capture all of the returned values
as data points, and you can instead pick the exact values you are
interested in. To choose the values to capture you simply define data
points with the same names as Strings in the keyset.

The following configuration demonstrates how to extract specific data
points from an operation that returns a Map&lt;String, Object&gt;. The
key item to note in this configuration is that "dailyBalance" and
"annualBalance" must be present as keys in the returned Map&lt;String,
Object&gt; and their values must be coercible via the
Double.valueOf(object.toString()) idiom.

-   MBean Name: Application:Name=Accounting,Type=Accounting
-   Operation Name: getBalances()
-   Data Points:
    -   dailyBalance (type: gauge)
    -   annualBalance (type: gauge)

### Single parameter in polymorphic operation

MBeans are implemented as Java classes and Java permits parameterized
polymorphic behavior. This means that multiple methods can be defined
with the same name so long as their parameter signatures differ. You can
safely define "getBalance(String)" and "getBalance()" and the two exist
as separate methods.

In order to properly resolve methods with the same name the caller must
provide a Class\[\] that lists the types of parameters that exist in the
method's signature. This resolves the candidate methods to an individual
method which can then be invoked by passing an Object\[\].

The zenjmx daemon allows you to resolve methods of the same name and
asks you to provide the fully qualified class names of each parameter in
comma delimited format when you set up the data source. Note that
primitive types (String, Boolean, Integer, Float) are supported but
complex types are not supported, and that you must include the class'
package name when providing the information (java.lang.String).

The Object\[\] of parameter values must line up with Class\[\] of
parameter types, and if there is a mismatch in the number of types and
values that are provided an exception will be generated.

The marshaling of values from String to Boolean, Integer, and Float
types is provided via the .valueOf() static method on each of those
types. That is, if you define an attribute of type java.lang.Integer you
must provide a String that can be successfully passed to
java.lang.Integer.fromValue(). If you fail to do so an exception is
generated.

This example illustrates how to pass a single parameter to a polymorphic
operation:

-   MBean Name: Application:Name=Accounting,Type=Accounting
-   Operation Name: getBalances()
-   Paramater Types: java.lang.Integer
-   Parameter Values: 1234
-   Data Points:
    -   balance (type: gauge)

Here is another example where we've changed the type of the parameter
passed to the method to be a String. Semantically it represents a
different type of Account in our example:

-   MBean Name: Application:Name=Accounting,Type=Accounting
-   Operation Name: getBalances()
-   Paramater Types: java.lang.String
-   Parameter Values: sbb552349999
-   Data Points:
    -   balance (type: gauge)

### Multiple parameters in polymorphic operations

The preceding example describes how polymorphic behavior in Java
functions and how method resolution can be provided by identifying the
Class\[\] that represents the parameters passed to a method. The
situation where multiple parameters are passed to a polymorphic
operation is no different then the situation where a single parameter is
passed to a polymorphic operation, except that the length of the
Class\[\] and Object\[\] is greater than one.

When multiple parameters are required to invoke an operation you must
provide the fully qualified class names of each parameter's type in
comma delimited format, as well as the object values for each type (also
in comma delimited format).

The following example demonstrates a configuration that passes two
parameters to an MBean operation. The second parameter passed is a
default value to return if no account can be located matching the first
parameter.

-   MBean Name: Application:Name=Accounting,Type=Accounting
-   Operation Name: getBalances()
-   Parameter Types: java.lang.String, java.lang.Integer
-   Parameter Values: sbb552349999, 0
-   Data Points:
    -   balance (type: gauge)

There are additional combinations that are possible with polymorphic
methods and the values they return, and those combinations are left as
an exercise for the reader to explore. The logic for extracting results
from multi-value operation invocations follows the same rules as the
logic for extracting results from a multi-value attribute read. For
additional information on the rules of that logic see the section above
on multi-value attributes.

## Special Service URLs

By default, URLs are assembled as:

    service:jmx:rmi:///jndi/rmi://hostName:portNum/jmxrmi

This host name and port points to a registry. After a JMX agent connects
to the registry, the registry tells the agent which host and port to use
for remote calls.

In some situations, you may want to explicitly provide the registry host
and port, as well as the host and port for the remote calls. Use the
long form, as in:

    service:jmx:rmi://127.0.0.1:8999/jndi/rmi://127.0.0.1:8999/jmxrmi

## Prerequisites

|                   |                                               |
|-------------------|-----------------------------------------------|
| Prerequisite      | Restriction                                   |
| Product           | Zenoss platform 4.x, Zenoss 2.2 or higher     |
| Required ZenPacks | ZenPacks.zenoss.ZenJMX                        |
| Other             | Oracle JRE Version 5.0 or higher is required. |

## Oracle Java Runtime Environment (JRE)

This ZenPack requires Oracle JRE Version 5.0 or higher. Make sure that
after you install the JRE you update your PATH such that the java
executable works. You can test this using the command:

    $ which java
    /usr/java/default/bin/java

If the above returns a fully qualified path, then you have successfully
installed Java.

If Java is not installed, the which will return a message similar to the
following:

    $ which java
    /usr/bin/which: no java in (/usr/local/bin:/bin:/usr/bin:/opt/zenoss/bin)

To determine which version of Java is installed, run the following
command:

    $ java -version
    java version "1.5.0_16"
    Java(TM) 2 Runtime Environment, Standard Edition (build 1.5.0_16-b06-284)
    Java HotSpot(TM) Client VM (build 1.5.0_16-133, mixed mode, sharing)

Warning: Oracle Java is required. Other Java implementations do not
work.

## Example to Monitor a JMX Value

### Enabling Remote JMX Access

Each application server has a slightly different process for enabling
remote JMX Access. You should consult with your application server for
specific instructions. This section includes instructions for a few
commonly used configurations.

JMX agents can be configured in two ways: remote access and local-only.
When configured for remote access a JMX client communicates with the JMX
agent via a socket and uses a remote protocol such as Remote Method
Invocation (RMI) or JMXMP to access the MBeans. When configured for
local-only access the JMX agent periodically dumps serialized MBeans to
a temporary directory on the machine. JConsole can be used to access JMX
agents in local-only mode as well as in remote mode. The zenjmx daemon
can be used only with remote servers via RMI or JMXMP and cannot work
with local-only serialized MBeans. This is not a significant limitation
because the zenjmx daemon can establish RMI connections to localhost in
the same manner that it creates connections to remote hosts.

The JAVA_OPTS environment variable can be used to enable remote access
to JVM MBeans. Set it as follows:

    JAVA_OPTS="-Dcom.sun.management.jmxremote.port=12345"
    JAVA_OPTS="${JAVA_OPTS} -Dcom.sun.management.jmxremote.authenticate=false"
    JAVA_OPTS="${JAVA_OPTS} -Dcom.sun.management.jmxremote.ssl=false"

    export JAVA_OPTS

When starting an application pass the JAVA_OPTS variable as an argument
to the JVM as follows:

    java ${JAVA_OPTS} -classpath /path/to/application.jar com.yourcompany.Main

You can then use JConsole to connect to localhost:12345. Authentication
can be configured by modifying the java.security file as well as
java.policy. There are lots of examples available on the Internet that
can provide guidance in how to achieve authenticated remote access to
JVM MBeans.

### Configure Zenoss platform with a Custom Data Source

Custom JMX data sources allow system administrators to monitor any
attribute or operation result accessible via a JMX call. This ZenPack
creates a `JMX` data source and allows you to provide object
information, as well as authentication settings, and attribute/operation
information. Determining which object and attribute names, as well as
which operations to invoke, is the key to customizing this feature.

To configure the system with a custom data source:

1.  Select Infrastructure from the navigation bar.

2.  Click the device in the device list. The device overview page
    appears.

3.  Expand Monitoring Templates in the left panel, and then select
    Device.

4.  Select Add Local Template from the Action menu. The Add Local
    Template dialog appears.

5.  Enter a name for the template (such as JVM Values), and then click
    **Submit**. The template is added.

6.  Select the newly created template.

7.  Click Add in the Data Sources area. The Add Data Source dialog
    appears.

8.  Enter a name for the data source (Heap Memory), select JMX as the
    type, and then click Submit. The data source is added.

9.  Double-click the data source to edit it. Change options as needed,
    and then click **Save**. Memory Head Example ZenJMX Data Source
    Options

    |                     |                                                                                                                   |
    |---------------------|-------------------------------------------------------------------------------------------------------------------|
    | Option              | Description                                                                                                       |
    | Protocol            | RMI or JMXMP. Consult your Java application documentation to determine which JMX Connector protocols it supports. |
    | JMX Management Port | This is not necessarily the same as the listen port for your server.                                              |
    | Object Name         | The Object Name is also referred to as the MBean name. Enter `java.lang:type=Memory`                              |
    | Attribute Name      | Enter `HeapMemoryUsage`                                                                                           |

10. Add data points named `committed`, `max`, and `used`:
    1.  Select Add Data Point from the Action menu. The Add Data Point
        dialog appears.
    2.  Enter the name of the data point (`committed`, `max`, or `used`)
        and then click **Submit**.

11. After adding all data points, add graphs that reference them.

Review to learn how to determine the object name, attribute name, and
data points that might be interesting in your application.

## Monitor Values in TabularData and CompositeData Objects

The Attribute Path input value on the ZenJMX data source allows you to
monitor values nested in the TabularData and CompositeData complex open
data objects. Using this value you can specify a path to traverse and
index into these complex data structures.

If the result of traversing and extracting a value out of the nested
open data is a single numeric value then it is automatically mapped to
the datapoint in the data source. However, if the value from the open
data is another open data object then the data point names from the
datasource are used as indexes or keys to map values out of the open
data.

The input value is a dot-separated string that represents a path through
the object. Non-bracketed values are keys into CompositeData. Bracketed
values are indexes into TabularData.

For TabularData indexes with more than one value, use a comma-separated
list with no spaces (for example, \[key1,key2\]).

To specify a column name (needed only when the table has more than two
columns) use curly brackets after the table index.

### Example

To get the used Tenured Generation memory after the last garbage
collection from the Garbage Collector MBean, set the Attribute Name on
the datasource to lastGcInfo. Set the Attribute Path to:

    memoryUsageAfterGc.[Tenured Gen].{value}.used

The key `memoryUsageAfterGc` is evaluated against the CompositeData
returned from the `lastGcInfo` attribute. The evaluation results in a
TabularData object. Then, the `[Tenured Gen]` index is evaluated against
the TableData, which returns a row in the table.

Since a row in the table can contain multiple columns, the key `value`
(in curly brackets) is used to pick a column in the row. Lastly, the key
`used` is evaluated against the CompositeData in the column to return
the memory value.

In this example, since the index being used for the tabular data is not
a multi-value index and so the column name is optional. The Attribute
Path can be written as:

    memoryUsageAfterGc.[Tenured Gen].used

## Using JConsole to Query a JMX Agent

JConsole is a tool built into the JDK that allows system administrators
to query a JMX Agent and examine the MBeans deployed within the server.
JConsole also allows administrators to view JVM summary information,
including the amount of time the JVM has been running, how many threads
are active, how much memory is currently used by the heap, how many
classes are currently loaded, and how much physical memory exists on the
machine.

JConsole also provides a graph that shows memory, thread, and class
usage over time. The scale of the graph can be adjusted so that a system
administrator can examine a specific period of time, or can zoom out to
view a longer range picture of usage. Unfortunately, JConsole can only
produce graphs that show usage while JConsole was running.
Administrators cannot look back in time to a point where the JVM was
running but JConsole was not monitoring the JVM.

JMX Heap Graph

![](plugins/servlet/confluence/placeholder/unknown-attachment){.confluence-embedded-image .confluence-external-resource}

The MBeans tab along the top of JConsole provides an interactive method
for examining MBean values. After clicking on the MBeans tab a panel
will be displayed with a tree on the left hand side. The tree contains a
hierarchical list of all MBeans deployed in the JVM.

The standard JVM MBeans are all in the java.lang and java.util.logging
packages. Application server specific MBeans do not follow any standard
naming pattern. Some vendors choose to use package names for their MBean
names while other vendors choose package-like names (but not fully
qualified packages).

To get started expand the java.lang node in the Tree. This will expose
several MBeans as well as additional folders. Click on the Memory MBean
and observe how the right hand side of the panel is populated with
information about the Memory MBean.

Memory MBean

![](plugins/servlet/confluence/placeholder/unknown-attachment){.confluence-embedded-image .confluence-external-resource}

MBeans can contain attributes and operations. MBeans can also fire
notifications to observers, but that's beyond the scope of this
document. The attributes tab lists all of the attributes in the first
column and their values (or a clickable attribute type) in the second
column. In the case of Memory the HeapMemoryUsage is a Composite
attribute, otherwise referred to as a "complex-value attribute" in
Zenoss platform. Double click the
"javax.management.openmbean.CompositeDataSupport" type and you will see
multiple attributes appear. The show the amount of committed, maximum,
and used memory sizes for the heap.

Memory MBean Expanded

![](plugins/servlet/confluence/placeholder/unknown-attachment){.confluence-embedded-image .confluence-external-resource}

The unique name of the MBean can be viewed by clicking on the Info tab.
The first value is MBean Name. Its value in the case of Memory is:
"java.lang:type=Memory."

Note: There is no standardized way to name MBeans; application server
vendors name them differently.

You can also examine operation information by clicking on the Operations
tab. These are methods that JConsole can remotely invoke on an MBean
that will result in some value being computed or some state changing in
the application. The Threading MBean has several operations that can be
invoked that return information. Click on the java.lang package and then
click on the Threading operation. Lastly, click on the Operations tab.
Methods like "getThreadUserTime" are invocable.

Operations Tab

![](plugins/servlet/confluence/placeholder/unknown-attachment){.confluence-embedded-image .confluence-external-resource}

Test the "getThreadUserTime" method by changing the p0 parameter to 1
and clicking the "getThreadUserTime" button. A dialog window will be
raised that displays the amount of CPU user time thread \#1 has used.
Try adjusting the parameter to different values to observe the different
CPU times for the threads.

## zenjmx Options

To display the options supported by the zenjmx daemon, enter the
following command:

    zenjmx help

### Memory Allocation

Use the `--javaheap` option to set the max heap. The value is 512MB.

### ZenJMX Logging

You can adjust logging levels to reduce the size of ZenJMX log files. In
the log4j.properties file (in $ZENHOME/Products/ZenJMX), update the
first line and change DEBUG to INFO, WARN, or ERROR.

## Daemons

|                       |        |
|-----------------------|--------|
| Type                  | Name   |
| Performance Collector | zenjmx |

## Changes

<dl markdown="1">
<dt markdown="1">
3.14.0
</dt>
</dl>

-   JMX Remote Operational jar file appears to have non-compliant
    license (ZPS-1824)
-   Update Log4j version (ZPS-7966)
-   XML External Entity vulnerability in zenjmx service (ZPS-5765)
-   Tested with Zenoss Cloud, Zenoss 6.6.0

<dl markdown="1">
<dt markdown="1">
3.13.1
</dt>
</dl>

-   Create migration to add new volume zenjmx-libs (ZPS-7217)
-   Tested with Zenoss Cloud, Zenoss 6.6.0

<dl markdown="1">
<dt markdown="1">
3.13.0
</dt>
</dl>

-   Zenjmx port 9988 might pose a security risk (ZEN-17033)
-   Fix build of the zenpack on java 11 (ZPS-7192)

<dl markdown="1">
<dt markdown="1">
3.12.1
</dt>
</dl>

-   Create events for XML-RPC errors. (ZEN-21392)
-   Fix reporting of unexpected errors. (ZEN-21472)

## Attachments:

-   [(ZenJMX)JavaManagementExtensions.jmx-heapgraph.png](img/zenpack-javamanagementextensions.jmx-heapgraph.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-memorymbean.png](img/zenpack-javamanagementextensions.jmx-memorymbean.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-memorymbeanexpanded.png](img/zenpack-javamanagementextensions.jmx-memorymbeanexpanded.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-operation.png](img/zenpack-javamanagementextensions.jmx-operation.png)
-   [oracle-zenpack.png](img/zenpack-oracle-zenpack.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-heapgraph.png](img/zenpack-javamanagementextensions.jmx-heapgraph.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-memorymbean.png](img/zenpack-javamanagementextensions.jmx-memorymbean.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-memorymbeanexpanded.png](img/zenpack-javamanagementextensions.jmx-memorymbeanexpanded.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-operation.png](img/zenpack-javamanagementextensions.jmx-operation.png)
-   [oracle-zenpack.png](img/zenpack-oracle-zenpack.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-heapgraph.png](img/zenpack-javamanagementextensions.jmx-heapgraph.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-memorymbean.png](img/zenpack-javamanagementextensions.jmx-memorymbean.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-memorymbeanexpanded.png](img/zenpack-javamanagementextensions.jmx-memorymbeanexpanded.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-operation.png](img/zenpack-javamanagementextensions.jmx-operation.png)
-   [oracle-zenpack.png](img/zenpack-oracle-zenpack.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-heapgraph.png](img/zenpack-javamanagementextensions.jmx-heapgraph.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-memorymbeanexpanded.png](img/zenpack-javamanagementextensions.jmx-memorymbeanexpanded.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-memorymbean.png](img/zenpack-javamanagementextensions.jmx-memorymbean.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-operation.png](img/zenpack-javamanagementextensions.jmx-operation.png)
-   [oracle-zenpack.png](img/zenpack-oracle-zenpack.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-memorymbeanexpanded.png](img/zenpack-javamanagementextensions.jmx-memorymbeanexpanded.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-operation.png](img/zenpack-javamanagementextensions.jmx-operation.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-memorymbean.png](img/zenpack-javamanagementextensions.jmx-memorymbean.png)
-   [(ZenJMX)JavaManagementExtensions.jmx-heapgraph.png](img/zenpack-javamanagementextensions.jmx-heapgraph.png)


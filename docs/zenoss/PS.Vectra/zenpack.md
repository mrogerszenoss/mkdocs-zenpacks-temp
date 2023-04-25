# Vectra

##                VECTRA

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.PS.Vectra

### Applications Monitored:

Vectra Services

## [Releases](#releases){.toc-backref}

**Version 1.1.0  **[Download](https://delivery.zenoss.com/){.external-link}:   ZenPacks.zenoss.PS.Vectra

**Prerequisite Restriction**

<dl markdown="1">
<dd markdown="1">
Required ZenPacks:
ZenPacks.zenoss.ZenPackLib&gt;=2.1.1,
ZenPacks.zenoss.PS.Util&gt;=1.9.8
</dd>
<dd markdown="1">
Compatible with Zenoss Resource
Manager 6.0 or higher and Zenoss Cloud
</dd>
</dl>

**Configuration**

The following zProperties configure the API connection:

-   zVectraApiKey - Api Key which received by Vectra
-   zVectraApiUrl - url endpoint of Vectra API which needed to monitor
    (Default is https://${here/id}/api/v2.2/health where here/id is a
    device host)
-   zVectraValidateHttpsCert - property which check validation of SSL
    certificate (Default is False)
-   zVectraApiResponseTimeout - response timeout (in seconds) for Vectra
    API requests (Default is 5)

**Generating the API Key**

Once logged-in the Vectra Detect UI, under My Profile, you can generate
an API Token (or copy an existing one)

**Modeler Plugins**

By default all modeler plugins were selected automatically. You can
change this list manually using Modeler Plugins item in left hand menu.

-   API Based Plugins

**      -  vectra.rest.Disk**

-   modeling from values via https://${here/id}/api/v2.2/health/disk

          Modeled properties:

-   status
-   output
-   error

**      - vectra.rest.Cpu**

-   modeling from values via https://${here/id}/api/v2.2/health/cpu

           Modeled properties:

-   label

**      - vectra.rest.Sensor**

-   modeling from values via https://${here/id}/api/v2.2/health/network
-   modeling from values via https://${here/id}/api/v2.2/health/sensors

          Modeled properties:

-   sensor_name
-   ip_address
-   luid
-   serial_number
-   link

**      - vectra.rest.Brain**

-   modeling from values via https://${here/id}/api/v2.2/health/network

          Modeled properties:

-   link
-   link_stable

**      - vectra.rest.System**

-   modeling from values via https://${here/id}/api/v2.2/health/system

          Modeled properties (displays on the Device Overview page):

-   vectraVersionLastUpdate (&rsquo;System Version Last Update&rsquo; field)
-   vectraVersion (&rsquo;Version Number&rsquo; field)
-   vectraMode (&rsquo;Vectra Mode&rsquo; field)
-   serial_number (&rsquo;Serial Number&rsquo; field)
-   model (&rsquo;Hardware Model&rsquo; field)

**Usage**

-   Add a Vectra host as you would add any device, but specify /Vectra
    as the Device Class.
-   Make sure needed zProperties mentioned in configuration section are
    set.
-   Once configured, model the device.
-   After modeling, managed Vectra device will be discovered and added
    as a separate device under device class specified in Vectra

** **

**Thresholds settings**

-   CPU utilization threshold setting up in CPU Templates/Thresholds
    part (default value is 90% of cpu load)
-   Disk utilization threshold setting up in Disk Templates/Thresholds
    part (default value is 90% of disk utilization)

**API Based Monitoring Events**

Monitoring Events are generated from the following Templates, which
depend on these API Commands.

-   **Cpu** Monitors interface values from
    https://${here/id}/api/v2.2/health/cpu /Perf/CPU event generated
    from threshold
    -   "threshold of CPU utilization exceeded"
-   **Disk** Monitors interface values from
    https://${here/id}/api/v2.2/health/disk /Status event generated from
    threshold
    -   "threshold of Disk utilization exceeded"
-   **Sensor & Brain** Monitors interface values from
    https://${here/id}/api/v2.2/health/network Raises an /Status/Vectra
    event if the link of Sensor or Brain is &rsquo;DOWN&rsquo; with
    vectraComponentLink

** **

** **

**Changes**

Release 1.1.0

-   **Features**
    -   Added zVectraApiResponseTimeout to configure response timeout

Release 1.0.0

-   **Features**
    -   Monitoring Vectra CPU
    -   Monitoring Vectra Disk
    -   Monitoring Vectra Network Brains
    -   Monitoring Vectra Network Sensors
    -   Raising events of CPU overload using threshhold
    -   Raising events of Disk space overload using threshhold
    -   Raising events of network Sensor is down
    -   Raising events of network Brain is down

** **

**Modeler Plugins**

-   rest.Disk
-   rest.Cpu
-   rest.Sensor
-   rest.Brain
-   rest.System

**Components Modeled**

-   Sensor Interface
-   Disk
-   Cpu
-   Brain

**Device Class Templates - Devices/Vectra**

-   Brain
    -   Graphs
        -   Brain Interface Peak Traffic
    -   Datapoints
        -   brainPeakTraffic
        -   brainLink
        -   DEFAULTS
-   Disk
    -   Graphs
        -   Disk Space Load
        -   Disk Load
        -   DEFAULTS
    -   Thresholds
        -   Disk utilization
    -   Datapoints
        -   usagePercent
        -   freeSpace
        -   totalSpace
        -   usedSpace
        -   DEFAULTS
-   Sensor
    -   Graphs
        -   Sensor Interface Peak Traffic
    -   Datapoints
        -   sensorLink
        -   sensorPeakTraffic
        -   DEFAULTS
-   Cpu
    -   Graphs
        -   CPU Total Load
        -   CPU Loads
        -   DEFAULTS
    -   Thresholds
        -   CPU utilization
    -   Datapoints
        -   nicePercent
        -   totalPercent
        -   DEFAULTS
        -   systemPercent
        -   idlePercent
        -   userPercent
-   SystemUptime
    -   Datapoints
        -   systemUptime

## Attachments:

-   [Oracle DB Monitoring Tablespace.png](img/zenpack-oracle-db-monitoring-tablespace.png)
-   [Oracle DB Monitoring Instance.png](img/zenpack-oracle-db-monitoring-instance.png)
-   [Oracle DB Monitoring Instance     -2.png](img/zenpack-oracle-db-monitoring-instance-2.png)
-   [Oracle DB Monitoring Modeler Plugin.png](img/zenpack-oracle-db-monitoring-modeler-plugin.png)
-   [Oracle DB Monitoring Configuration.png](img/zenpack-oracle-db-monitoring-configuration.png)
-   [Oracle DB Monitoring Tablespace Zenoss Smartview.png](img/zenpack-oracle-db-monitoring-tablespace-zenoss-smartview.png)
-   [Databasemonitor_ts_io.png](img/zenpack-databasemonitor_ts_io.png)
-   [Databasemonitor_add_connectionstring.png](img/zenpack-databasemonitor_add_connectionstring.png)
-   [Databasemonitor_messages.png](img/zenpack-databasemonitor_messages.png)
-   [Databasemonitor_physical_ops.png](img/zenpack-databasemonitor_physical_ops.png)
-   [Databasemonitor_ts.png](img/zenpack-databasemonitor_ts.png)
-   [Databasemonitor_components.png](img/zenpack-databasemonitor_components.png)
-   [Databasemonitor_instances.png](img/zenpack-databasemonitor_instances.png)
-   [Databasemonitor_monitoring_template.png](img/zenpack-databasemonitor_monitoring_template.png)
-   [Databasemonitor_ts_diskspace.png](img/zenpack-databasemonitor_ts_diskspace.png)
-   [Databasemonitor_sga.png](img/zenpack-databasemonitor_sga.png)
-   [oracle-zenpack.png](img/zenpack-oracle-zenpack.png)
-   [Databasemonitor_chr.png](img/zenpack-databasemonitor_chr.png)
-   [Databasemonitor_model_device.png](img/zenpack-databasemonitor_model_device.png)


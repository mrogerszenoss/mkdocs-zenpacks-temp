# AIX_v2

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.AixMonitor

### Applications Monitored:

-   IBM AIX (5.3)
-   IBM AIX (6.1)
-   IBM AIX (7.1)

## AIX ZenPack

This ZenPack provides status and performance monitoring of AIX systems.

The **ZenPacks.zenoss.AixMonitor** ZenPack uses Secure Shell (SSH) to
monitor AIX hosts.

This ZenPack models and monitors devices placed in the
**/Server/SSH/AIX** device class by running commands and parsing the
output. The account used to monitor the device does not require root
access or special privileges.

## Support

This ZenPack is included with commercial versions of Zenoss. Enterprise
support for this ZenPack is provided to active Zenoss customers.

## Releases

Version 2.2.3-[Download](https://zenoss.leapfile.net){.external-link}:   Released on 2017/05/18:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x - 5.1.x

Version 2.2.2-[Download](https://zenoss.leapfile.net){.external-link}:   Released on 2016/08/30:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x - 5.1.x

Version 2.0.1-[Download](https://zenoss.leapfile.net){.external-link}:   Released on 2015/04/02:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Initial discovery and periodic remodeling of relevant components.
-   Performance monitoring.

This ZenPack provides:

-   File system and process monitoring
-   Network interfaces and route modeling
-   CPU utilization information
-   Hardware information (memory, number of CPUs, machine serial
    numbers, model numbers)
-   OS information (OS level command style information)
-   LPP and RPM information (such as installed software)

## Gallery

@lb[](img/zenpack-zenoss aix monitoring graphs.png){.confluence-embedded-image width="898"}

### Discovery

The following components will be automatically discovered through the
AIX server address, username and password you provide. The properties
and relationships will be periodically updated by modeling.

Server (Device):   Attributes: ent_cpu, ent_vproc, active_cpu, systemId, 
prof_max_mem, ent_mem

EntAdapter:   Attributes: devname, location, parent, physloc

FCAdapter:   Attributes: devname, location, parent, physloc

HDisk:   Attributes: devname, location, parent, physloc

### Performance Monitoring

The following metrics will be collected every 5 minutes by default.

-   Default OS performance Metrics

Device

-   ssCpuIdle
-   ssCpuSystem
-   ssCpuUser
-   ssCpuWait
-   ssRawContexts
-   ssRawInterrupts
-   io_read
-   io_written
-   hrMemorySize
-   memAvailReal
-   percentMemUsed
-   swap_percentUsed
-   sysUptime
-   laLoadInt1
-   laLoadInt5
-   laLoadInt15

EntAdapter

-   receive_bytes
-   receive_packets_dropped
-   transmit_bytes
-   transmit_packets_dropped
-   recvHugeutil
-   recvLargeutil
-   recvMediumutil
-   recvSmallutil
-   recvTinyutil

FCAdapter

-   control_requests
-   input_bytes
-   input_requests
-   output_requests
-   output_bytes
-   output_requests

HDisk

-   b_written
-   b_read
-   policies_algorithm
-   policies_reserve_policy

## Service Impact and Root Cause Analysis

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact and root cause analysis capabilities for
services running on IBM Power. The service impact relationships shown in
the diagram and described below are automatically added. These will be
included in any services that contain one or more of the explicitly
mentioned components.

@lb[](img/zenpack-aix-impact-yuml.png)

IBM and Power Server Impact Relationship Diagram

Internal Impact Relationships

-   Ethernet Adapter impacts related Device (LPAR)
-   Fibre Channel Adapter impacts related Device (LPAR)
-   HDisk Drive impacts related Device (LPAR)

## Usage

**Note:** If using a distributed collector setup, SSH requires firewall
access (default of port 22) from the collector to the monitored server.

### Set AIX Server Monitoring Credentials

All AIX servers must have a device entry in an organizer below the
**/Devices/Server/SSH/AIX** device class.

**Note:** The SSH monitoring feature will attempt to use key-based
authentication before using a configuration properties password value.

1.  Navigate to the device class or device.
    -   If applying changes to a device class:
        1.  Select the class in the devices hierarchy.
        2.  Click **Details**.
        3.  Select Configuration Properties.
    -   If applying changes to a device:
        1.  Click the device in the device list.
        2.  Select Configuration Properties.

2.  Verify the credentials for the service account to access the
    service.

    **AIX Configuration Properties**

    | Name             | Description                                                |
    |:-----------------|:-----------------------------------------------------------|
    | zCommandUsername | AIX user with privileges to gather performance information |
    | zCommandPassword | Password for the AIX user                                  |

3.  Click **Save** to save your changes.

### Add an AIX Server

The following procedure assumes that the credentials have been set.

1.  From Infrastructure &gt; Devices, select Add a Single Device.

2.  Enter the following information in the dialog:

    **Adding AIX Device Information**

    | Name         | Description                                                                                                                                                                                                         |
    |:-------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Name or IP   | AIX host to model                                                                                                                                                                                                   |
    | Device Class | **/Server/SSH/AIX**                                                                                                                                                                                                 |
    | Model Device | Select this option unless adding a device with username/password different than found in the device class. If you do not select this option, then you must add the credentials, and then manually model the device. |

3.  Click **Add Device** to add the device.

## Troubleshooting

This ZenPack requires the following collector process to be running.

| Type                  | Name       |
|:----------------------|:-----------|
| Modeler               | zenmodeler |
| Performance Collector | zencommand |

### IBM_PowerVM Device Class

The Devices/Server/SSH/AIX/IBM_PowerVM device class is intended to be
used when monitoring PowerVM LPARs. This device class creates an
additional AIXExt template to be used in monitoring the PowerVM
equipment.

### Resolving CHANNEL_OPEN_FAILURE Issues

The **zencommand** daemon's log file
(**$ZENHOME/collector/zencommand.log**) may show messages stating:

```
ERROR zen.SshClient CHANNEL_OPEN_FAILURE: Authentication failure WARNING:zen.SshClient:Open of command failed (error code 1): open failed
```

If the **sshd** daemon's log file on the remote device is examined, it
may report that the *MAX_SESSIONS* number of connections has been
exceeded and that it is denying the connection request. At least in the
OpenSSH daemons, this *MAX_SESSIONS* number is a compile-time option and
cannot be reset in a configuration file.

To work around this limitation of the **sshd** daemon, use the
configuration property zSshConcurrentSessions to control the number of
connections created by **zencommand** to the remote device.

1.  Navigate to the device or device class in the Zenoss platform
    interface.

    -   If applying changes to a device class:
        1.  Select the class in the devices hierarchy.
        2.  Click **Details**.
        3.  Select Configuration Properties.
    -   If applying changes to a device:
        1.  Click the device in the device list.
        2.  Select Configuration Properties.

2.  Apply an appropriate value for the maximum number of sessions.

    **Concurrent SSH Configuration Properties**

    | Name                   | Description                                                                                                              |
    |:-----------------------|:-------------------------------------------------------------------------------------------------------------------------|
    | zSshConcurrentSessions | Maximum number of sessions supported by the remote device's *MAX_SESSIONS* parameter. Common values for AIX are 2 or 10. |

3.  Click **Save** to save your changes.

### Resolving Timeout Issues

The **zencommand** daemon's log file
(**$ZENHOME/collector/zencommand.log**) may show messages stating:

```
WARNING:zen.zencommand:Command timed out on device device_name: command
```

If this occurs, it usually indicates that the remote device has taken
too long to return results from the commands. To increase the amount of
time for devices to return results, change the configuration property
zCommandCommandTimeout to a larger value.

1.  Navigate to the device or device class in the Zenoss platform
    interface.

    -   If applying changes to a device class:
        1.  Select the class in the devices hierarchy.
        2.  Click **Details**.
        3.  Select Configuration Properties.
    -   If applying changes to a device:
        1.  Click the device in the device list.
        2.  Select Configuration Properties.

2.  Apply an appropriate value for the command timeout.

    **SSH Timeout Configuration Properties**

    | Name                   | Description                                                                  |
    |:-----------------------|:-----------------------------------------------------------------------------|
    | zCommandCommandTimeout | The number of seconds to wait for commands to complete on the remote device. |

3.  Click **Save** to save your changes.

### Known Issues

When Migrating from 1.2.0 to a newer version of this ZenPack the
Filesystem cycle time changed from 60 to 300. If your filesystem graphs
are not updating you will need to delete the existing filesystem rrd
files so that new ones can be generated with the new 300 second step
time.

When upgrading this ZenPack from version 1.3.0 to a later version, a
traceback containing the text:

```
AttributeError: 'ZenPack' object has no attribute '__of__'
```

may be encountered. This traceback does not affect the functionality of
the ZenPack, which should function normally after installation is
completed.

### Limitations

Some commands used in the AIXExt template may be incompatible with your
version of AIX. You should disable those datasources if that is the case
and it is impacting your installation.

### Changes

**2.2.3**

-   Fix aliases for standard reports (ZPS-1390)

**2.2.2**

-   Make event class /Status/OSProcess for process monitoring
    (ZEN-21999)
-   Add zCredentialsZProperties: zCommandUsername & zCommandPassword
-   Add mem\_\_pct and fs\_\_pct datapoint aliases (ZEN-24619)

**2.2.1**

-   Updated zenpacklib.py to address modeler timeouts from
    attribute-indexed components

**2.2.0**

-   Fix excessive remote command execution (ZEN-16740)
-   IP Service modeling no longer ignoring zIpServiceMapMaxPort
    (ZEN-17360)
-   Fix incorrect ssCpuIdle alias for multi-core systems (ZEN-17360)
-   Fix handling of European date formats (ZEN-19089)
-   Fix incorrect template bindings (ZEN-20078)
-   Fix incorrect modeling time (ZEN-22127)
-   Add/revise custom component icons, fix icon positioning (ZEN-22191,
    ZEN-22294)
-   Fix missing Impact YAML file (ZEN-22250)
-   Fixed missing graph datapoints (ZEN-22259)

**2.0.1**

-   Fix handling of locales that use comma for decimals. (ZEN-16506)
-   Fix inability to discover DB2 databases on AIX servers. (ZEN-17193)

**2.0.0**

-   AIX 7.1 Support
-   AIX SS CPU data inaccurate (ZEN-8637)
-   AIX Parser Broken (ZEN-15092)
-   Graphs returning Nan (ZEN-15099, ZEN-15157, ZEN-15199)
-   Unable to gather some memory metrics (ZEN-15139)
-   Added Impact Adapters (ZEN-15153)
-   Rename Components (ZEN-15155)
-   Disk Drive Components returning wrong data (ZEN-15159)
-   Add graph legends (ZEN-15162)
-   Installation Traceback (ZEN-15166)
-   Supply Missing Template (ZEN-15180)
-   Some components missing during upgrade (ZEN-15193)
-   Traceback during installation (ZEN-15166)

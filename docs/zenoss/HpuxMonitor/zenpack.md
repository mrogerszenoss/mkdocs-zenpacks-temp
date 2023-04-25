# HP-UX (Commercial)

@lb[](img/zenpack-hp-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.HpuxMonitor

## HP-UX ZenPack

This ZenPack provides status and performance monitoring of HP-UX.

## Support

This ZenPack is included with commercial versions of Zenoss. Enterprise
support for this ZenPack is provided to active Zenoss customers.

## Releases

Version 2.0.1-[Download](https://zenoss.leapfile.net){.external-link}:   Released on 2016/09/06:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x - 5.1.x

Version 2.0.2-[Download](https://zenoss.leapfile.net){.external-link}:   Released on 2017/05/09:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x - 5.1.x

## Contents

-   [Features](#features)
    -   [Discovery](#discovery)
    -   [Performance Monitoring](#performance-monitoring)
-   [Usage](#usage)
    -   [Set HP-UX Server Monitoring Credentials](#uxserver-monitoring-credentials)
    -   [Add an HP-UX Server](#uxserver)
-   [Troubleshooting](#troubleshooting)
    -   [Itanium Device Class](#itanium-device-class)
    -   [Resolving CHANNEL_OPEN_FAILURE Issues](#resolving-channel-_open-_failure-issues)
    -   [Resolving Timeout Issues](#resolving-timeout-issues)
    -   [Notes](#notes)
    -   [Known Issues](#known-issues)
    -   [Limitations](#limitations)
    -   [Changes](#changes)

The **ZenPacks.zenoss.HpuxMonitor** ZenPack uses Secure Shell (SSH) to
monitor HP-UX hosts.

This ZenPack models and monitors devices placed in the
**/Server/SSH/HP-UX** device class (or **/Server/SSH/HP-UX/Itanium** if
appropriate) by running commands and parsing the output.

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
-   Installed software information

### Discovery

Standard device components will be automatically discovered through the
HP-UX server address, username and password you provide. The properties
and relationships will be periodically updated by modeling.

The components, relations, and attributes will be updated on Zenoss'
normal remodeling interval, which defaults to every 12 hours.

### Performance Monitoring

The following metrics will be collected every 5 minutes by default.

-   Default OS performance Metrics

    -   Device

        -   sysUptime
        -   laLoadInt1
        -   laLoadInt5
        -   laLoadInt15
        -   ssCpuIdle
        -   ssCpuSystem
        -   ssCpuUser
        -   ssCpuInterrupt
        -   io_reads_and_writes
        -   percentMemUsed
        -   percentSwapUsed

    -   FileSystem

        -   availBlocks
        -   availInodes
        -   totalBlocks
        -   totalInodes
        -   usedBlocks
        -   usedInodes
        -   percentInodesUsed

    -   OSProcess

        -   ps_cpu
        -   ps_mem
        -   ps_count

    -   ethernetCsmacd

        -   ifInErrors
        -   ifInOctets
        -   ifInPackets
        -   ifOutErrors
        -   ifOutOctets
        -   ifOutPackets

## Usage

**Note:** If using a distributed collector setup, SSH requires firewall
access (default of port 22) from the collector to the monitored server.

### Set HP-UX Server Monitoring Credentials

All HP-UX servers must have a device entry in an organizer below the
**/Devices/Server/SSH/HP-UX** device class.

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

    **HP-UX Configuration Properties**
    | Name             | Description                                                  |
    |:-----------------|:-------------------------------------------------------------|
    | zCommandUsername | HP-UX user with privileges to gather performance information |
    | zCommandPassword | Password for the HP-UX user                                  |

3.  Click **Save** to save your changes.

### Add an HP-UX Server

The following procedure assumes that the credentials have been set.

1.  From Infrastructure -&gt; Devices, select Add a Single Device.

2.  Enter the following information in the dialog:

    Adding HP-UX Device Information
    | Name         | Description                                                                                                                                                                                                         |
    |:-------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Name or IP   | HP-UX host to model                                                                                                                                                                                                 |
    | Device Class | **/Server/SSH/HP-UX** or **/Server/SSH/HP-UX/Itanium**                                                                                                                                                              |
    | Model Device | Select this option unless adding a device with username/password different than found in the device class. If you do not select this option, then you must add the credentials, and then manually model the device. |

3.  Click **Add Device** to add the device.

## Troubleshooting

This ZenPack requires the following collector process to be running:

**Required Collectors**

| Type                  | Name           |
|:----------------------|:---------------|
| Modeler               | **zenmodeler** |
| Performance Collector | **zencommand** |

### Itanium Device Class

The Devices/Server/SSH/HP-UX/Itanium device class is intended to be used
when monitoring Intel Itanium-based hardware. This device class uses
some different commands to obtain Itanium-related data.

### Resolving CHANNEL_OPEN_FAILURE Issues

The **zencommand** daemon's log file
(**$ZENHOME/collector/zencommand.log**) may show messages stating:

    ERROR zen.SshClient CHANNEL_OPEN_FAILURE: Authentication failure WARNING:zen.SshClient:Open of command failed (error code 1): open failed

If the **sshd** daemon's log file on the remote device is examined, it
may report that the **MAX_SESSIONS** number of connections has been
exceeded and that it is denying the connection request. At least in the
OpenSSH daemons, this **MAX_SESSIONS** number is a compile-time option
and cannot be reset in a configuration file.

To work around this limitation of the **sshd** daemon, use the
configuration property **zSshConcurrentSessions** to control the number
of connections created by **zencommand** to the remote device.

1.  Navigate to the device or device class in the **Zenoss platform**
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
    | Name                   | Description                                                                                                                |
    |:-----------------------|:---------------------------------------------------------------------------------------------------------------------------|
    | zSshConcurrentSessions | Maximum number of sessions supported by the remote device's **MAX_SESSIONS** parameter. Common values for AIX are 2 or 10. |

3.  Click **Save** to save your changes.

### Resolving Timeout Issues

The **zencommand** daemon's log file
(**$ZENHOME/***collector***/zencommand.log**) may show messages stating:

    WARNING:zen.zencommand:Command timed out on device device_name: command

If this occurs, it usually indicates that the remote device has taken
too long to return results from the commands. To increase the amount of
time for devices to return results, change the configuration property
**zCommandCommandTimeout** to a larger value.

1.  Navigate to the device or device class in the **Zenoss platform**
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

### Notes

The HP-UX machines may require updating /etc/PATH

You may want only one of the cpu or cpu_itanium plugins. Listing the
PA-RISC or Itanium processors requires root access on the HP-UX to call
/usr/bin/adb. Alternatively, the command strings can be modified to use
sudo. Sudo can be installed from
<http://hpux.connect.org.uk/ftp/hpux/Sysadmin/sudo-1.8.0/>

Some modeler commands depend on the "machinfo" command, which may need
to be installed on the target HP-UX device

### Known Issues

### Limitations

### Changes

2.0.2

-   Update processes parser for changes CommandParser (ZPS-711)

2.0.1

-   Fix modeling "ValueError" when swap volumes are disabled (ZEN-23286)
-   Add common datapoint aliases (ZEN-24619)

2.0.0

-   conversion to YAML definitions and ZenPackLib
-   More user friendly graph legends (ZEN-22432)
-   Lowered default zSshConcurrentSessions to 5 (ZEN-22431)
-   Changed event class for High Load threshold (ZEN-22433)

## Attachments:

-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)


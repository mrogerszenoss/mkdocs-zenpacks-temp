# Linux Monitor

This ZenPack monitors the Linux Operating System.

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License

GNU General Public License, Version 2, or later

### Name

ZenPacks.zenoss.LinuxMonitor

## [Releases](#releases){.toc-backref}

[Version-2.3.3](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.LinuxMonitor/2.3.3/ZenPacks.zenoss.LinuxMonitor-2.3.3.egg){.external-link}:

    Released on 2019/06/04

    Compatible with Zenoss Cloud, 6.3 - 5.3, 4.2.5

    Requires [ZenPackLib ZenPack](http://help.zenoss.com/display/in/ZenPackLib){.external-link}

<!-- -->

[Version-2.2.7](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.LinuxMonitor/2.2.7/ZenPacks.zenoss.LinuxMonitor-2.2.7.egg){.external-link}:

    Released on 2017/12/01

    Compatible with Zenoss 4.2.5 - 6.0

<!-- -->

[Version-2.1.3](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.LinuxMonitor/2.1.3/ZenPacks.zenoss.LinuxMonitor-2.1.3.egg){.external-link}:

    Released on 2017/03/31

    Compatible with Zenoss 4.2 - 5.2

<!-- -->

[Version-2.0.6](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.LinuxMonitor/2.0.6/ZenPacks.zenoss.LinuxMonitor-2.0.6.egg){.external-link}:

    Released on 2016/11/01

    Compatible with Zenoss 4.2 - 5.1

## [Background](#background){.toc-backref}

This ZenPack provides monitoring support for Linux, leveraging OpenSSH
for data access. In addition to system health, disks, LVM, services, and
processes are monitored.

## [Features](#features){.toc-backref}

-   Monitors multiple Linux flavors and versions
-   OpenStack LVM volume integration
-   Monitors LVM Physical Volumes, Volume Groups, Thin Pools, and
    Logical Volumes
-   Block Device monitoring
-   Service Monitoring via **Sysvinit**, **`Systemd`**, or **`Upstart`**
-   Root Cause Analysis with Impact Support
-   Dynamic View support

This version of the LinuxMonitor ZenPack completely replaces the
EnterpriseLinux ZenPack. To avoid errors arising from conflicts between
them, the EnterpriseLinux ZenPack should be removed after the new
LinuxMonitor ZenPack has been installed.

## [Discovery](#discovery){.toc-backref}

The following entities will be automatically discovered. The attributes
and collections will be updated on Zenoss normal remodeling interval
which defaults to every 12 hours.

Hard Disks:   Attributes: Name, Size, LVM PV
    **Notes**:
     - On CentOS5, RHEL5 (and possibly others), the `lsblk` command is
    not available, in which case this component will be missing.
     - To ignore unmounted drives, set the *zIgnoreUnmounted*
    configuration property to True.

Processors

<dl markdown="1">
<dd markdown="1">
Attributes: Socket, Manufacturer, Model, Speed, Ext Speed, L1, L2,
Voltage
</dd>
<dt markdown="1">
IP Services
</dt>
<dd markdown="1">
Attributes: Name, Protocol, Port, IPs, Description
</dd>
<dt markdown="1">
File Systems
</dt>
<dd markdown="1">
Attributes: Mount Point, Storage Device, Total Bytes, Used Bytes, Free
Bytes, % Util
**Note**: Some links between the
server and clients of NFS File Systems and other storage devices are
intentionally removed as they significantly impact performance.
</dd>
</dl>

Interfaces

<dl markdown="1">
<dd markdown="1">
Attributes: IP Interface, IP Addresses, Description, MAC Address,
Operational Status, Admin Status
</dd>
<dt markdown="1">
Network Routes
</dt>
<dd markdown="1">
Attributes: Destination, Next Hop, Interface, Protocol, Type
</dd>
<dt markdown="1">
Snapshot Volumes
</dt>
<dd markdown="1">
Attributes: Name, Volume Group, Logical Volume, Size, Block Device, File
System, Active Relations: Logical Volumes
</dd>
<dt markdown="1">
Physical Volumes
</dt>
<dd markdown="1">
Attributes: Name, Format, Size, Free, % Util, Block Device, Volume Group
Relations: Volume Groups
</dd>
<dt markdown="1">
Volume Groups
</dt>
<dd markdown="1">
Attributes: Name, Size, Free, % Util, Snapshot Volumes, Logical Volumes,
Physical Volumes, Thin Pools
</dd>
<dt markdown="1">
Logical Volumes
</dt>
<dd markdown="1">
Attributes: Name, Volume Group, Size, Block Device, File System, Active,
Snapshot Volumes Relations: Volume Groups, Thin Pools
</dd>
<dt markdown="1">
Thin Pools
</dt>
<dd markdown="1">
Attributes: Name, Volume Group, Size, Block Device, File System, Active,
Metadata Size Relations: Volume Groups
</dd>
<dt markdown="1">
OS Processes
</dt>
<dd markdown="1">
Attributes: Process Class, Process Set, Restart Alert?, Fail Severity
</dd>
<dt markdown="1">
OS Services
</dt>
<dd markdown="1">
Attributes: Name, Description, Init System
**Note**: Some links between the
server and clients of NFS File Systems and other storage devices are
intentionally removed as they significantly impact performance.
</dd>
</dl>

##  [Set Linux Server Monitoring Credentials](#set-lin-uxserver-monitoring-credentials){.toc-backref}

All Linux servers must have a device entry in an organizer below the
**/Devices/Server/SSH/Linux** device class.

**Tip**: The SSH monitoring feature will attempt to use key-based
authentication before using a configuration properties password value.

1.  Select INFRASTRUCTURE from the top navigation bar.
2.  Click the device name in the device list on the right.
3.  On the Device Overview page, select Configuration Properties from
    the left pane.
4.  Verify the credentials for the service account. The
    *zCommandUsername* property must be set. To use public key
    authentication, the public portion of the key referenced in
    *zKeyPath* is must be listed in the `~/.ssh/authorized_keys` file
    for the appropriate user on the Linux server. If this key has a
    passphrase you should set it in the *zCommandPassword* property. If
    you'd rather use password authentication than configure keys, simply
    put the user's password in the *zCommandPassword* property.

| Name             | Description                                                   |
|------------------|---------------------------------------------------------------|
| zCommandUsername | Linux user with privileges to gather performance information. |
| zCommandPassword | Password for the Linux user.                                  |

## [Using a Root User](#usinga-root-user){.toc-backref}

This ZenPack requires the ability to run the `pvs`, **`vgs`**,
**`lvs`**, `systemctl`, **`initctl`**, **`df`**, and `service` commands,
remotely on your Linux server(s) using SSH. By default, these commands
are only allowed to be run locally. To run these commands remotely, the
root user must not be required to use a tty.

1.  Install the **sudo** package on your server.

2.  Allow root user to execute commands via ssh without a TTY.

    1.  Run the `visudo` command to edit the `/etc/sudoers` file.

    2.  Find the line containing *root ALL=(ALL) ALL*.

    3.  Add this line underneath it:
        **Defaults:root !requiretty**

    4.  Save the changes and exit.

## [Using a Non-Root User](#root-user){.toc-backref}

This ZenPack requires the ability to run the `pvs`, **`vgs`**,
**`lvs`**, `systemctl`, **`initctl`**, **`df`**, and `service` commands,
remotely on your Linux server(s) using SSH. By default, most of these
commands are only allowed to be run by the *root* user. The output of
the `systemctl`, `initctl`, **`df`***,* and `service` commands can vary
depending on whether or not they are executed by a user with root
privileges. Furthermore, this ZenPack expects these commands be in the
user's path. Normally this is only true for the root user.

Assuming that you've created a user named *zenmonitor* on your Linux
servers for monitoring purposes, you can follow these steps to allow the
*zenmonitor* user to run the commands.

1.  Install the **sudo** package on your server

2.  Allow the *zenmonitor* user to run the required commands via SSH
    without a tty.

    -   Edit `/etc/sudoers.d/zenoss` (or `/etc/sudoers` if
        `sudoers.d` is not supported)
        and add the following lines to the bottom of the file:

        ~~~ literal-block
        Defaults:zenmonitor !requiretty

        Cmnd_Alias ZENOSS_CMDS = \
            /usr/sbin/dmidecode, \
            /bin/df, \
            /bin/dmesg

        Cmnd_Alias ZENOSS_LVM_CMDS = \
            /sbin/pvs, /usr/sbin/pvs, \
            /sbin/vgs, /usr/sbin/vgs, \
            /sbin/lvs, /usr/sbin/lvs

        Cmnd_Alias ZENOSS_SVC_CMDS = \
            /sbin/initctl list, \
            /sbin/service *, /usr/sbin/service *, \
            /sbin/runlevel, \
            /bin/ls -l /etc/rc?.d/

        zenmonitor ALL=(ALL) NOPASSWD: \
            ZENOSS_CMDS, \
            ZENOSS_LVM_CMDS, \
            ZENOSS_SVC_CMDS
        ~~~

    -   Save, ensuring all paths for these commands are correct

Make sure that you have the latest release of OpenSSH installed on the
target system. This is especially important for older versions of RHEL,
CentOS, Ubuntu, and SUSE Linux.

If using a non-root user on SUSE Linux, you must run the following as
root due to SUSE restrictions on the `dmesg` command:
**`echo 0 > /proc/sys/kernel/dmesg_restrict`**

On SUSE Linux, the **`pvs`**, **`vgs`**, and **`lvs`** commands are
located in `/sbin`. Please ensure that each command can be manually
executed remotely.

The zSshConcurrentSessions configuration property has a default value of
5. If you increase this value, you must update the allowed number of
sessions in the `sshd` configuration on the target device and restart
the `sshd` daemon.

## [Add a Linux Server](#add-a-lin-uxserver){.toc-backref}

The following procedure assumes that credentials have been set.

1.  Select Infrastructure from the navigation bar.

2.  Select Add a Single Device from the Add Device list of options. The
    Add a Single Device dialog appears.

3.  Enter the following information in the dialog:

    | Name         | Description                                                                                                                                                                                                               |
    |--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Name or IP   | Linux host to add.                                                                                                                                                                                                        |
    | Device Class | /Server/SSH/Linux                                                                                                                                                                                                         |
    | Model Device | Select this option unless adding a device with a user name and password different than found in the device class. If you do not select this option, then you must add the credentials and then manually model the device. |

4.  Click **Add**.

Alternatively you can use **`zenbatchload`** to add Linux servers from
the command line. To do this, you must create a text file with the host
name, username, and password of each of the servers you want to add.
Multiple endpoints can be added under the same
`/Devices/Server/SSH/Linux` section. Here is an example.

```sh
/Devices/Server/SSH/Linux
HOST-NAME zCommandUsername="USER", zCommandPassword="PASSWORD"
```

You can then load the Linux servers into the Zenoss Platform with the
following command:  **`zenbatchload FILE-NAME`**

## [Modeling and Monitoring OS Services](#modeling-and-monitoring-osservices){.toc-backref}

The Linux OS services are modeled using the
*zenoss.cmd.linux.os_service* modeler plugin. The following systems are
supported:

-   RHEL 5
-   RHEL 6
-   RHEL 7
-   RHEL 8
-   CentOS 5
-   CentOS 6
-   CentOS 7
-   CentOS 8
-   Debian 8
-   Debian 9
-   Suse 12
-   Ubuntu 12
-   Ubuntu 14
-   Ubuntu 15
-   Ubuntu 16

Version 2.3.0 supports monitoring the status of the `systemd`,
`upstart`, and `systemV` system services. The *OSService-SYSTEMD*,
*OSService-UPSTART* and *OSService-SYSTEMD* monitoring templates are
automatically bound to a service component based on the target's modeled
init system value. The configuration properties *zLinuxServicesModeled*
and *zLinuxServicesNotModeled* restrict the services that are modeled
and thereby monitored.

For `systemd`, only services that are enabled (or have "enabled-runtime"
status) are modeled and monitored. Furthermore, "oneshot" services or
services with unmet conditions are not modeled or monitored. In order to
prevent a service from being modeled and monitored by Zenoss, the
service will have to be stopped and disabled. One of those actions alone
won't be sufficient. Another way to prevent a service from being modeled
is to add it to the zLinuxServicesNotModeled zProperty. To also model
active services of any UnitFileState (enabled, disabled, static, etc.),
the *zLinuxModelAllActiveServices* configuration property should be set
to *True*.

`Upstart` devices monitor all enabled services managed by `upstart` and
additionally also monitor `systemV` services that run in the current
runlevel of the same device. The *Init System* property, found in the
*Details* menu of the service, displays which init system the service is
managed by.

`SystemV` devices model and monitor all services in the current
runlevel.

| Name                         | Description                                                                                |
|------------------------------|--------------------------------------------------------------------------------------------|
| zLinuxServicesModeled        | Accepts regular expressions that matches one or more services to model                     |
| zLinuxServicesNotModeled     | Accepts regular expressions that matches one or more services to not model                 |
| zLinuxModelAllActiveServices | Boolean value used for `systemd` services that models active services of any UnitFileState |

*zLinuxServiceModeled* and *zLinuxServiceNotModeled* can support
multiple regular expressions separated by new lines. Although the
*zLinuxModelAllActiveServices* property models all active services that
are also disabled when checked, this property will still not model
"oneshot" services or those services whose conditions are not met. The
*OSService* monitoring template generates events on every collection
cycle for a service that is down. The events are automatically cleared
if the service is up again.

*zLinuxServicesNotModeled* overrules *zLinuxServicesModeled*. If a
service name matches the regular expressions in both configuration
properties, the service will not modeled.

## [Installed Items](#installed-items){.toc-backref}

Installing this ZenPack will add the following items to your Zenoss
system.

Configuration Properties

-   zLinuxServicesModeled
-   zLinuxServicesNotModeled

Device Classes

-   /Server/SSH/Linux

Modeler Plugins

-   zenoss.cmd.uname
-   zenoss.cmd.linux.df
-   zenoss.cmd.linux.alt_kernel_name
-   zenoss.cmd.linux.cpuinfo
-   zenoss.cmd.linux.interfaces
-   zenoss.cmd.linux.lvm
-   zenoss.cmd.linux.memory
-   zenoss.cmd.linux.netstat_an
-   zenoss.cmd.linux.netstat_rn
-   zenoss.cmd.linux.process
-   zenoss.cmd.linux.rpm
-   zenoss.cmd.linux.sudo_dmidecode
-   zenoss.cmd.linux.os_release
-   zenoss.cmd.linux.os_service

As of version 2.3.0, the zenoss.cmd.linux.rpm and
zenoss.cmd.linux.alt_kernel_name modeler plugins are disabled by default
on new installs. If upgrading from a version previous to 2.3.0 they will
still be enabled by default. We recommend that you disable
the *zenoss.cmd.linux.alt_kernel_name* modeler plugin if you have a
customized `/etc/issue` file as the customization could affect modeling
results.

[Monitoring Templates](#monitoring-templates){.toc-backref}

-   Device (in /Devices/Server/SSH/Linux)
-   HardDisk (in /Devices/Server/SSH/Linux)
-   IpService (in /Devices)
-   FileSystem (in /Devices/Server/SSH/Linux)
-   ethernetCsmacd (in /Devices/Server/SSH/Linux)
-   SnapshotVolume (in /Devices/Server/SSH/Linux)
-   PhysicalVolume (in /Devices/Server/SSH/Linux)
-   VolumeGroup (in /Devices/Server/SSH/Linux)
-   LogicalVolume (in /Devices/Server/SSH/Linux)
-   OSProcess (in /Devices/Server/SSH/Linux)
-   OSService-SYSTEMD (in /Devices/Server/SSH/Linux)
-   OSService-UPSTART (in /Devices/Server/SSH/Linux)
-   OSService-SYSTEMV (in /Devices/Server/SSH/Linux)
-   ThinPool (in /Devices/Server/SSH/Linux)

Device (in /Devices/Server/SSH/Linux)

-   Data Points

    -   ssCpuUsedPerCpu
    -   ssCpuIdlePerCpu
    -   ssCpuUserPerCpu
    -   ssCpuNicePerCpu
    -   ssCpuSystemPerCpu
    -   ssCpuWaitPerCpu
    -   ssCpuInterruptPerCpu
    -   ssCpuSoftInterruptPerCpu
    -   ssCpuStealPerCpu
    -   sysUpTime
    -   laLoadInt15
    -   laLoadInt5
    -   laLoadInt1
    -   Buffers
    -   Cached
    -   MemFree
    -   MemTotal
    -   SwapFree
    -   SwapTotal
    -   ssIORawReceived
    -   ssIORawSent

-   Thresholds

    -   *None*

-   Graphs

    -   CPU Utilization
    -   Load Average
    -   Memory Utilization
    -   Memory Usage
    -   IO Throughput

    In version 2.3.0, support for the *MemAdjustedUsed* and
    *MemAdjustedUsedPercent* data points were added. These data points
    include Buffers, Cached, and Free in the memory used calculation.
    These data points are not added by default. To use them, you will
    need to create data points called *MemAdjustedUsed* and
    *MemAdjustedUsedPercent* in the *mem* data source on the device
    template.

CPU (in /Devices/Server/SSH/Linux)

-   Data Points - ssCpuUsed - ssCpuIdle - ssCpuUser - ssCpuNice -
    ssCpuSystem - ssCpuWait - ssCpuInterrupt - ssCpuSoftInterrupt -
    ssCpuSteal
-   Thresholds
    -   *None*
-   Graphs
    -   CPU Utilization

HardDisk (in /Devices/Server/SSH/Linux)

-   Data Points
    -   readsCompleted
    -   readsMerged
    -   sectorsRead
    -   msReading
    -   writesCompleted
    -   writesMerged
    -   sectorsWritten
    -   msWriting
    -   ioInProgress
    -   msDoingIO
    -   msDoingIOWeighted
-   Thresholds
    -   *None*
-   Graphs
    -   Operation Throughtput
    -   Merge Rate
    -   Sector Throughtput
    -   IO Operation in Progress
    -   IO Utilization
    -   Weighted IO Utilization

There were significant changes between 2.4 and 2.6 in the I/O subsystem.
As a result, some statistic information disappeared. The translation
from a disk address relative to a partition to the disk address relative
to the host disk happens much earlier. All merges and timings now happen
at the disk level rather than at both the disk and partition level as in
2.4. There are only **four** fields available for partitions on 2.6
machines and in this case few data points will be missed.

IpService (in /Devices)

-   Data Points
    -   *None*
-   Thresholds
    -   *None*
-   Graphs
    -   *None*

FileSystem (in /Devices/Server/SSH/Linux)

-   Data Points
    -   usedBlocks
    -   percentInodesUsed
    -   totalInodes
    -   usedInodes
    -   availableInodes
-   Thresholds
    -   90 percent used
-   Graphs
    -   Utilization
    -   Usage
    -   Inode Utilization
    -   Inode Usage

**Note**: File Systems components will also show graphs from their
related Logical Volume or Hard Disk.

ethernetCsmacd (in
/Devices/Server/SSH/Linux)

-   Data Points
    -   ifInOctets
    -   ifOutOctets
    -   ifInPackets
    -   ifOutPackets
    -   ifInErrors
    -   ifInDropped
    -   ifInOverruns
    -   ifOutErrors
    -   ifOutCarrier
    -   ifOutCollisions
    -   ifOutDropped
-   Thresholds
    -   75 percent utilization
-   Graphs
    -   Data Throughput
    -   Packet Throughput
    -   Error Rate

SnapshotVolume (in /Devices/Server/SSH/Linux)

-   Data Points
    -   state
    -   health
-   Thresholds
    -   *None*
-   Graphs
    -   *None
        *

**Note**: Snapshot Volumes will also show graphs from its related Volume
Group and Hard Disk.

PhysicalVolume (in /Devices/Server/SSH/Linux)

-   Data Points
    -   size
    -   free
    -   allocatable
    -   exported
    -   missing
-   Thresholds
    -   unallocatable
    -   exported
    -   missing
-   Graphs
    -   Utilization

**Note**: Physical Volumes will also show graphs from its related Hard
Disk.

VolumeGroup (in /Devices/Server/SSH/Linux)

-   Data Points
    -   size
    -   free
    -   partial
-   Thresholds
    -   partial
-   Graphs
    -   Utilization

**Note**: Volume Groups will also show graphs from its related Physical
Volumes.

LogicalVolume (in /Devices/Server/SSH/Linux)

-   Data Points
    -   state
    -   health
-   Thresholds
    -   *None*
-   Graphs
    -   *None*

**Note:** Logical Volumes will also show graphs from its related Volume
Group and Hard Disk.

ThinPool (in /Devices/Server/SSH/Linux)

-   Data Points
    -   state
    -   health
    -   percentDataUsed
    -   percentMetaDataUsed
-   Thresholds
    -   90 percent used
-   Graphs
    -   Pool Utilization

**Note**: Thin Pools will also show graphs from its related Volume Group
and Hard Disk.

OSProcess (in
/Devices/Server/SSH/Linux)

-   Data Points
    -   count
    -   cpu
    -   mem
-   Thresholds
    -   count
-   Graphs
    -   Process Count
    -   CPU Utilization
    -   Memory Usage

OSService-SYSTEMD (in /Devices/Server/SSH/Linux)

-   Data Points
    -   status
-   Thresholds
    -   *None*
-   Graphs
    -   *None*

OSService-UPSTART (in /Devices/Server/SSH/Linux)

-   Data Points
    -   status
-   Thresholds
    -   *None*
-   Graphs
    -   *None*

OSService-SYSTEMV (in /Devices/Server/SSH/Linux)

-   Data Points
    -   status
-   Thresholds
    -   *None*
-   Graphs
    -   *None

        *

## [Service Impact](#service-impact){.toc-backref}

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in Service Impact capability for services running on Linux.
The following service impact relationships are automatically added.
These will be included in any services that contain one or more of the
explicitly mentioned entities.

Service Impact Relationships

-   HardDisk, IpInterface, IpService, OSProcess, CPU, OSService are
    impacted by LinuxDevice
-   PhysicalVolume is impacted by HardDisk
-   VolumeGroup is impacted by PhysicalVolume
-   LogicalVolume is impacted by VolumeGroup or HardDisk
-   SnapshotVolume is impacted by LogicalVolume or HardDisk
-   FileSystem is impacted by SnapshotVolume or LogicalVolume or
    HardDisk or LinuxDevice or ThinPool
-   ThinPool is impacted by VolumeGroup or HardDisk or logicalVolume

## [Daemons](#daemons){.toc-backref}

| Type                  | Name       |
|-----------------------|------------|
| Modeler               | zenmodeler |
| Performance Collector | zencommand |

[Supported Distributions](#supported-distributions){.toc-backref}

The following Linux distributions are officially supported. Other
distributions may also be supported, especially derivatives of Debian
and Red Hat Enterprise Linux.

<table data-border="1">
<colgroup>
<col />
<col />
<col />
<col />
</colgroup>
<thead>
<tr markdown="1">
<th>Linux Flavor</th>
<th>Version</th>
<th>Released</th>
<th>End of Support</th>
</tr>
</thead>
<tbody>
<tr markdown="1">
<td>Ubuntu</td>
<td>16.04 LTS</td>
<td>April 2016</td>
<td>April 2021</td>
</tr>
<tr markdown="1">
<td><br />
</td>
<td>15.10</td>
<td>October 2015</td>
<td>July 2016</td>
</tr>
<tr markdown="1">
<td><br />
</td>
<td>15.04</td>
<td>April 2015</td>
<td>February 2016</td>
</tr>
<tr markdown="1">
<td><br />
</td>
<td>14.04 LTS</td>
<td>April 2014</td>
<td>April 2019</td>
</tr>
<tr markdown="1">
<td><br />
</td>
<td>12.04 LTS</td>
<td>April 2012</td>
<td>April 2017</td>
</tr>
<tr markdown="1">
<td>Debian</td>
<td>8</td>
<td>April 2015</td>
<td>April 2020</td>
</tr>
<tr markdown="1">
<td><br />
</td>
<td>9</td>
<td>June 2017</td>
<td>June 2022</td>
</tr>
<tr markdown="1">
<td>RedHat Enterprise Linux</td>
<td>8</td>
<td>May 2019</td>
<td><br />
</td>
</tr>
<tr markdown="1">
<td><br />
</td>
<td>7</td>
<td>June 2014</td>
<td>June 2020</td>
</tr>
<tr markdown="1">
<td><br />
</td>
<td>6</td>
<td>November 2010</td>
<td>November 2020</td>
</tr>
<tr markdown="1">
<td><br />
</td>
<td>5</td>
<td>March 2007</td>
<td>March 2017</td>
</tr>
<tr markdown="1">
<td>CentOS</td>
<td>8</td>
<td>May 2019</td>
<td><br />
</td>
</tr>
<tr markdown="1">
<td><br />
</td>
<td>7</td>
<td>July 2014</td>
<td>June 2024</td>
</tr>
<tr markdown="1">
<td><br />
</td>
<td>6</td>
<td>July 2011</td>
<td>November 2020</td>
</tr>
<tr markdown="1">
<td><br />
</td>
<td>5</td>
<td>April 2007</td>
<td>March 2017</td>
</tr>
<tr markdown="1">
<td>SUSE Linux Enterprise Server</td>
<td>12</td>
<td>October 2014</td>
<td>October 2027</td>
</tr>
<tr markdown="1">
<td><br />
</td>
<td>11</td>
<td>March 2009</td>
<td>March 2022</td>
</tr>
</tbody>
</table>

## [Changes](#changes){.toc-backref}

**2.3.3**

-   Fix and optimize various impact relationship calculations.
    (ZPS-5664, ZPS-5711, ZPS-5792, ZPS-5806)
-   Fix "NotFound" modeling exception for snapshots of thin pools.
    (ZPS-5816)

**2.3.2**

-   Guard against out of date sudoers configuration in service
    monitoring. (ZPS-4334)
-   Allow filesystem modeling and monitoring to work with or without
    sudo access. (ZPS-4340)
-   Fix LVM monitoring when \*/sbin not in user's path. (ZPS-4349)
-   Fix undocumented sudo usage of "systemctl status". (ZPS-4121)
-   Update reduced recommended sudoers configuration. (ZPS-4121)
-   Tested with Zenoss Cloud and Zenoss Resource Manager 6.3.0, 6.2.1,
    and 5.3.3.

**2.3.1**

-   Fix CPU Busy metric on "CPU Utilization" graph. (ZPS-3531)
-   Fix 'no volume group' warning events during modeling. (ZPS-3475)
-   Add Idle, Interrupt, Soft Interrupt, Steal metrics on CPU
    Utilization graph. (ZPS-3547)
-   Enable better management of service events. (ZPS-3616)
-   Fix OSService template binding errors in zenhub. (ZPS-3709)
-   Add systemV services to upstart devices. (ZPS-3478)
-   Update systemd services to not model oneshot or unmet conditions.
    (ZPS-3478, ZPS-3545)
-   Added new zProperty for systemd, zLinuxModelAllActiveServices.
    (ZPS-3478)
-   Added migration script to change the default value of
    zLinuxServicesModeled.
-   Tested with Zenoss Resource Manager 4.2.5 RPS 743, 5.3.3 and 6.1.2
    and Service Impact 5.3.1.

2.3.0

-   The zenoss.cmd.linux.rpm modeler plugin is now disabled by default.
    (ZPS-1603)
-   Fix netmask as hex parsing and KeyError when meminfo is absent.
    (ZPS-2462)
-   Added ZenPackLib requirement. (ZPS-3000)
-   Fix custom banner errors and disabled
    zenoss.cmd.linux.alt_kernel_name modeler plugin by default.
    (ZPS-2998)
-   Additionally supports OS service monitoring for service modeling
    released in 2.0.0. (ZPS-2722)
-   Add dpkg support to zenoss.cmd.linux.rpm modeler plugin. (ZPS-1474)
-   Added support for Thin Pool Monitoring. (ZPS-2494)
-   Fixed alert spam for services. (ZPS-1625)
-   Added monitoring for individual processor components. (ZPS-2444)
-   Added Nice CPU usage for Processors. (ZPS-3315)
-   Fix OS Manufacturer not showing. (ZPS-1864)
-   Add sudo to df commands. (ZPS-1594)
-   Remove old modeler plugins, ensure model consistency. (ZPS-3411)
-   Add support for adjustedMemory datapoints. (ZPS-862)
    -   New Component: The following Component was added:
        -   ThinPools
    -   New Graph: The following graph was added:
        -   ThinPools: Pool MetaData/Data Utilization
    -   New Relationships: The following relationships were added:
        -   VolumeGroup 1:MC ThinPool
        -   ThinPool 1:M LogicalVolume
-   Tested with Zenoss Resource Manager 4.2.5 RPS 743, 5.3.3 and 6.1.2
    and Service Impact 5.3.0

2.2.7

-   Allow for restricted dmesg access in Debian 9 and SUSE 12.
    (ZPS-1933, ZPS-550)

2.2.6

-   Fix issue with links between Linux and NetApp FileSystem components.
    (ZPS-1736)
-   Prevent the creation of orphaned processes when an NFS mount becomes
    unavailable. (ZPS-1499)
-   Document support for RHEL 7, Ubuntu 16.04 LTS, and Debian 8.
    (ZPS-1820)
-   Fix spurious warnings in zencommand log when monitoring NFS mounted
    filesystems. (ZPS-1823)
-   Calculate memory utilization using "MemAvailable" when possible.
    (ZPS-1144)
-   Fix 0.0% utilization in Windows filesystem threshold event
    summaries. (ZPS-1844)

2.2.5

-   Fix modeler 'AttributeError: type' error when
    zInterfaceMapIgnoreTypes is set. (ZPS-1695)
-   Fix RPN errors in aliases for memory, swap, and LVM (ZPS-757)

2.2.4

-   Escape the commandTemplate expression for disk and idisk datasources
    to avoid TALES errors. (ZPS-1616)

2.2.3

-   Use FileSystem_NFS_Client template for all NFS mounts (including
    nfs4). (ZPS-1495)
-   Fix "IndexError" when modeling tun interfaces. (ZPS-971)
-   Add percentUsed datapoint for filesystems. Use for UI and events.
    (ZPS-1545)

2.2.2

-   Fix query service overloading during Analytics ETL of Linux devices.
    (ZPS-1312)
-   Honor zFileSystemIgnoreTypes in zenoss.cmd.linux.df modeler plugin.
    (ZPS-1494)

2.2.1

-   Improved OS Model parser for os_release modeler plugin. (ZPS-1177)

2.2.0

-   Add disk id modeling for correlation with underlying hardware.
    (ZPS-510)
-   Add link to underlying hardware from disk details if possible.
    (ZPS-939)
-   Handle root filesystem reservation more like "df" command.
    (ZPS-1266)
-   Fix NFS filesystem monitoring not working as expected. (ZPS-1006)

2.1.3

-   Properly account for reserved space to match df output. (ZPS-26739)

2.1.2

-   Improve OS process detection. (ZPS-659)
-   Quiet modeler error messages for missing services. (ZPS-644)

2.1.1

-   Fix "ifconfig" is checked before "ip" Linux Monitor (ZEN-25425)

2.1.0

-   Add cpu_ssCpuUsedPerCpu and mem_MemUsedPercent datapoints.
    (ZEN-22978)
-   Add common datapoint aliases. (ZEN-24619)
-   Improve ability to model network interface speeds.
-   Improve support for NFS filesystem impact. (ZEN-24478)
-   Improve NFS filesystem linking to NFS server. (ZEN-24478)
-   Disable monitor of NFS mounted filesystems by default. (ZEN-24650)
-   Prevent threshold violations on interfaces with unknown speed.
-   Fix IndexError when modeling older LVM versions. (ZEN-25792)
-   Fix setIdForRelationship error when modeling some LVM versions.
    (ZEN-22409)

2.0.6

-   Fix "string index out of range" error when modeling older LVM
    versions (ZEN-25792)

2.0.4

-   Fix "unimplemented" SSH error on 4.2.5 SP709. (ZEN-23392)

2.0.3

-   Fix migration of Linux devices to new type. (ZEN-24293)

2.0.2

-   Added property to ignore unmounted hard disks
-   Improve 1.x to 2.x migration time. (ZEN-24024)

2.0.1

-   Fix invalid event class in filesystem threshold

2.0.0

-   Added support for LVM Physical Volumes, Volume Groups, and Logical
    Volumes
-   Added support for OpenStack-LVM Integration
-   Added disk (block device) monitoring.
-   Added service monitoring (sysvinit, systemd, upstart).
-   Combined EnterpriseLinux and LinuxMonitor capabilities.
-   Enhanced Impact Support
-   Added Dynamic View Support
-   Completely replaces EnterpriseLinux ZenPack
-   Many other smaller improvements.

## Attachments:

-   [linux-zenpack.png](img/zenpack-linux-zenpack.png)
-   [linux-zenpack.png](img/zenpack-linux-zenpack.png)
-   [linux-zenpack.png](img/zenpack-linux-zenpack.png)
-   [linux-zenpack.png](img/zenpack-linux-zenpack.png)
-   [linux-zenpack.png](img/zenpack-linux-zenpack.png)

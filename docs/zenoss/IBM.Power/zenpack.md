# IBM Power

@lb[](img/zenpack-ibm-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.IBM.Power

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.IBM.Power){.external-link}

## IBM Power ZenPack

Monitoring IBM Power Servers with the help of HMC interface.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 1.2.0 - [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2019/11/28:   Requires [PythonCollector ZenPack](http://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},
    [AIX Monitor ZenPack](http://help.zenoss.com/display/in/aix-monitor "ZenPack:AIX Monitor"){.external-link},
    [CalculatedPerformance ZenPack](http://help.zenoss.com/display/in/calculatedperformance "ZenPack:CalculatedPerformance"){.external-link},
    [ZenPackLib ZenPack](http://help.zenoss.com/display/in/ZenpackLib "ZenPack:ZenPackLib"){.external-link}:   Compatible with Zenoss 6.x and Zenoss Cloud

<!-- -->

Version 1.1.3 - [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2019/06/06:   Requires [PythonCollector ZenPack](http://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},
    [AIX Monitor ZenPack](http://help.zenoss.com/display/in/aix-monitor "ZenPack:AIX Monitor"){.external-link},
    [CalculatedPerformance ZenPack](http://help.zenoss.com/display/in/calculatedperformance "ZenPack:CalculatedPerformance"){.external-link}:   Compatible with Zenoss 4.2.5 - 6.3 and Zenoss Cloud

## Background

This ZenPack provides support for monitoring IBM Power Server
(P5/P6/P7/P8/P9), with the IBM HMC interface. Monitoring is performed
using the HMC interface. This ZenPack is currently supported for IBM
Power servers running on the AIXLinux Operating System.

Supported versions of HMC:   V 7, V 8, V 9

<!-- -->

Supported versions of Power Servers:   POWER9, POWER8, POWER7, POWER6 and POWER5

<!-- -->

Supported Operating systems of Logical partition:   AIX, Linux

## Prerequisites

<dl markdown="1">
<dt markdown="1">
Zenoss Version: 6.x, Zenoss Cloud
</dt>
<dt markdown="1">
PythonCollector &gt;= 1.2
</dt>
<dt markdown="1">
CalculatedPerformance &gt;= 2.0
</dt>
<dt markdown="1">
AixMonitor &gt;= 1.0
</dt>
<dt markdown="1">
ZenPackLib &gt;= 2.0
</dt>
</dl>

External Dependencies:   SSH should be configured and running on IBM HMC Server.

<dl markdown="1">
<dd markdown="1">
This should be verified using SSH command from HMC server:

    lssyscfg -r sys

</dd>
</dl>

-   This will list all the Managed Systems under HMC

## Features

The features added by this ZenPack be summarized as follows. They are
each detailed further below.

-   Initial discovery and continual synchronization of relevant
    components.

<!-- -->

-   Performance monitoring.

<!-- -->

-   Service impact and root cause analysis. (Requires Zenoss Service
    Dynamics)

## Discovery

#### IBM HMC Server

The following components will be automatically discovered through the
HMC Server IP address and the host name you provide. The properties and
relationships will be continually maintained

<dl markdown="1">
<dt markdown="1">
HMC Server
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Serial Number, BIOS, Model Number, Version, Build Level,
Service Pack, Release
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: Managed Systems, Logical Partitions, HMC Service
Processor
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
Managed Systems
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Server Name, Status, Serial Number, Model, Service
Partition, State
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: HMC Server, I/O Devices, Processor Pools, HEA, HEAPorts,
LHEA, LHEA Ports, Profiles, Port Groups, IO Pools
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
LPAR Profiles
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Managed system, LPAR
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: LogicalPartitions
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
I/O Devices
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Slot, Server Name, Owner, Description, Bus ID, I/O Pool ID
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: Managed Systems
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
I/O Pools
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Pool ID, Server Name, LPAR Name, LPAR ID, I/O Pools Allowed
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: Managed Systems
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
LPAR
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: LPAR Name, LPAR ID, Server Name, Serial Number, Work Group
ID, OS Version, Processing Units, Assigned Memory, State
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: HMC Server
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
Service Processor
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Serial Number, IP Address, Location Code, Service Processor
Role, Connection State
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: HMC Server
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
Processor Pools
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Pool Name, Shared Processor Pool ID, LPAR IDs
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: ManagedSystem
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
Hea
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Physical Location, State
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: ManagedSystem
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
Hea Port
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Configured Connection Speed, Current Connection Speed,
Current Duplex, Configured Duplex, Physical Port State
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: ManagedSystem, Hea, PortGroup, LogicalPartition
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
Logical HEA
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Capability, Dynamic Reconfiguration Connector Name
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: ManagedSystem, LogicalPartition
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
Logical HEA Port
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Dynamic Reconfiguration Connector Name, Dynamic
Reconfiguration Connector Index, State, Logical Port ID
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: ManagedSystem, PortGroup, LogicalPartition
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
Port Group
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Physical Port IDs, Current Side MCS, Temporary Side MCS
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: ManagedSystem, LogicalPartition, HeaPort, LHeaPort
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
Virtual Ethernet Adapters
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Attached Virtual Switch, State
</dd>
</dl>
<dl markdown="1">
<dd markdown="1">
Relationships: ManagedSystem, LogicalPartition
</dd>
</dl>
<dl markdown="1">
<dt markdown="1">
Virtual SCSI Adapters
</dt>
</dl>
<dl markdown="1">
<dd markdown="1">
Attributes: Adaptor Type, State
</dd>
</dl>

## Performance Monitoring

The following metrics will be collected every 5 minutes by default. Any
other IBM HMC Server metrics can also be collected by adding them to the
appropriate monitoring template.

<dl markdown="1">
<dt markdown="1">
HEA Port
</dt>
</dl>

-   Packets

HEA

-   Packets

<dl markdown="1">
<dt markdown="1">
LPARs
</dt>
</dl>

-   Processor Utilization
-   Processor Units Used
-   Current Memory

<dl markdown="1">
<dt markdown="1">
ManagedSystems
</dt>
</dl>

-   Memory
-   Percent Pool Cycles
-   Processors

<dl markdown="1">
<dt markdown="1">
ProcessorPools
</dt>
</dl>

-   Shared Processor Pool Utilization

## Event Monitoring

This zenpack will monitor the power states of the logical partitions and
managed systems. Currently this is the only out of box event creation.

#### IBM Power Server

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Configuration Properties
</dt>
</dl>

-   zCollectorPlugins
-   zSnmpMonitorIgnore
-   zDeviceTemplates
-   zCommandUsername
-   zCommandPassword
-   zCommandCommandTimeout
-   zCommandPort
-   zKeyPath

<dl markdown="1">
<dt markdown="1">
Device Classes
</dt>
</dl>

-   /Devices/Server/IBM/Power/HMC

<dl markdown="1">
<dd markdown="1">
IBM HMC Server will be added in this device class using HMC IP.
</dd>
</dl>

<dl markdown="1">
<dt markdown="1">
Modeler Plugins
</dt>
</dl>

The following plugins will be used for modeling HMC Server and IBM Power
Server using the HMC Server IP Addresses via SSH interface.

-   HMCModelerPlugin

<dl markdown="1">
<dd markdown="1">
This plugin is for modeling IBM HMC Server and IBM Power Server.
</dd>
</dl>

<dl markdown="1">
<dt markdown="1">
Datasource Types
</dt>
</dl>

-   COMMAND

<dl markdown="1">
<dt markdown="1">
Monitoring Templates
</dt>
</dl>

-   HeaPort (in /Server/IBM/Power/HMC)

<!-- -->

-   Hea (in /Server/IBM/Power/HMC)

<!-- -->

-   LogicalPartitions (in /Server/IBM/Power/HMC)

<!-- -->

-   LHeaPort (in /Server/IBM/Power/HMC)

<!-- -->

-   LHea (in /Server/IBM/Power/HMC)

<!-- -->

-   ManagedSystems (in /Server/IBM/Power/HMC)

<!-- -->

-   ProcessorPools (in /Server/IBM/Power/HMC)

<!-- -->

-   ServiceProcessor (in /Server/IBM/Power/HMC)

<!-- -->

-   VirtEth (in /Server/IBM/Power/HMC)

<!-- -->

-   VirtScsi (in /Server/IBM/Power/HMC)

## Service Impact and Root Cause Analysis

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact and root cause analysis capabilities for
services running on IBM Power. The service impact relationships shown in
the diagram and described below are automatically added. These will be
included in any services that contain one or more of the explicitly
mentioned components.

@lb[](img/zenpack-ibm_yuml_1.png){.confluence-embedded-image width="714"}

IBM and Power Server Impact Relationship Diagram

<dl markdown="1">
<dt markdown="1">
Internal Impact Relationships
</dt>
</dl>

-   Managed Systems, Logical Partitions, HMC Service Processor and
    Processor Pools impacts the related HMC Server.

<!-- -->

-   HEAs, HEA Ports, Logical HEAs, Logical HEA Ports, I/O Devices, I/O
    Pools, Port Groups, Processor Pools, Logical Partitions, Virtual
    Ethernet Adapters, Virtual SCSI Adapters failures impact the related
    Managed Systems which impacts the HMC Server.

<!-- -->

-   Logical Partitions failures impact the related Logical HEAs, Logical
    HEA Ports, I/O Devices, I/O Pools, Processor Pools, Virtual Ethernet
    Adapters, Virtual SCSI Adapters.

<!-- -->

-   Managed Systems failures impact the related Logical Partitions.

<!-- -->

-   Port Groups failures impact HEA Port.

<!-- -->

-   Logical HEA Ports failures impact Port Groups, HEAs.

<!-- -->

-   I/O Pools failures impact I/O Devices which impacts the Logical
    Partitions.

Most of the impacts described above follow the default policy of a node
being in the worst state of the nodes that impact it. For example, an
HMC Server failure will imply that all related hosts are also failed.

## Zenoss Analytics

This ZenPack provides additional support for Zenoss Analytics. Perform
the following steps to install extra reporting resources into Zenoss
Analytics after installing the ZenPack.

1.  Copy analytics-bundle.zip from
    $ZENHOME/ZenPacks/ZenPacks.zenoss.IBM.Power/analytics/ on your
    Zenoss server.
2.  Navigate to Zenoss Analytics in your browser.
3.  Login as superuser.
4.  Remove any existing *IBM Power ZenPack* folder.
    1.  Choose *Repository* from the *View* menu at the top of the page.
    2.  Expand *Public* in the list of folders.
    3.  Right-click on *IBM Power ZenPack* folder and choose *Delete*.
    4.  Confirm deletion by clicking *OK*.
5.  Add the new *IBM Power ZenPack* folder.
    1.  Choose *Server Settings* from the *Manage' menu at the top of
        the page.*
    2.  Choose *Import* in the left page.
    3.  Remove checks from all check boxes.
    4.  Click *Choose File* to import a data file.
    5.  Choose the analytics-bundle.zip file copied from your Zenoss
        server.
    6.  Click *Import*.You can now navigate back to the *IBM Power
        ZenPack* folder in the repository to see the following resources
        added by the bundle.

## Usage

#### Adding HMC Server

Use the following steps to start monitoring HMC Server using the Zenoss
web interface.

1.  Navigate to the Infrastructure page.

    @lb[](img/zenpack-ibm_add_menu.png)

    Add Device

2.  Navigate to organizer Devices/Server/IBM/Power/HMC.
3.  Choose Add a Single Device from the add button.
4.  Fill out the form.

    @lb[](img/zenpack-ibm_add_dialog.png)

    Add Dialog

    -   *Name* can be anything you want.
    -   *Hostname or IP* must be resolvable and accessible from the
        collector server chosen in the *Collector* field.
5.  Click *ADD*.
6.  IBM HMC Server will be added in the /Devices/Server/IBM/Power/HMC
    device class.

Use the following steps for successful modeling.

1.  Select the device added.
2.  Navigate to Configuration Properties.

    @lb[](img/zenpack-ibm_model_device.png)

    Model device

3.  Provide the values for zCommandUsername and zCommandPassword.
4.  Model the device.

------------------------------------------------------------------------

#### zenbatchload

-   Alternatively you can use zenbatchload to add devices from the
    command line.
-   To do this, you must create a file with contents similar to the
    following.
-   Replace all values in angle brackets with your values minus the
    brackets.
-   Multiple devices can be added under the same sections.

    '/Devices/Server/IBM/Power/HMC' <device name>  setManageIp="<IP Address>", zCommandUsername='<username>', zCommandPassword='<password>'

    Example: /Devices/Server/IBM/Power/HMC HMC_1 setManageIp='10.100.75.35', zCommandUsername='hcladmin', zCommandPassword='root123'

You can then load the Devices using zenbatchload with the following
command.

    zenbatchload <filename>

------------------------------------------------------------------------

## Limitation

-   Storage Mapping has not been implemented in this release.

## Changes

**1.2.0**

-   Migrate to ZenPackLib 2.x
-   Honor zCommandCommandTimeout (ZPS-468)
-   Respect user-defined monitored components (ZPS-840)
-   Refactor/streamline datasources and modeler plugin
-   Allow shared serial numbers (ZPS-1311)
-   Support HMC v8, remove HEA based components and error messages
    (ZPS-5589)
-   Two new components: Virtual Ethernet Adapters and Virtual SCSI
    Adapters (ZPS-5589)
-   New event polling Datasource (ZPS-5589)
-   Fix modeler plugin to return correct values for relationship setter
    (ZPS-1498)
-   Fixed error while opening links in a new window (ZPS-4111)
-   Added support for POWER8, POWER9 (ZPS-4112)
-   Added more descriptive failure event messages (ZPS-6669)
-   Updated icons
-   Tested with Zenoss Cloud, Zenoss Resource Manager 6.4.1 and Service
    Impact 5.5.1

1.1.3

-   Fix inconsistencies in Impact relationships
-   Do not attempt to set invalid LPAR relations (ZPS-5873)

<dl markdown="1">
<dt markdown="1">
1.1.2
</dt>
</dl>

-   Guard against empty fields used for component IDs
-   Less ambiguous event summary for incremental model update failures
-   ZEN-25867: Updated to txsshclient 1.0.0 for Twisted 15 compatibility

<dl markdown="1">
<dt markdown="1">
1.1.1
</dt>
</dl>

-   Updated zenpacklib.py to address modeler timeouts from
    attribute-indexed components

<dl markdown="1">
<dt markdown="1">
1.1.0
</dt>
</dl>

-   Audited, revised, and standardized component classes and relations
    model throughout
-   Added Dynamic View functionality
-   Updated Analytics Bundle
-   Complete conversion to ZPL
-   ZEN-21613: Update all documentation
-   ZEN-21555: No metric values collected for various components
-   ZEN-21537: Changes in configuration applied" occurs after remodeling
-   ZEN-21536: Connection Information shows wrong information
-   ZEN-21541: Update Impact documentation
-   ZEN-18852: Incorrect value format for the 'Installed Count' field
-   ZEN-18853: Duplicated fields for components
-   ZEN-18851: Incorrect value in the 'Manufacture Config' field
-   ZEN-18850: No friendly names for fields
-   ZEN-18819: Analytics details for HMC Server component should be
    changed
-   ZEN-15818: Small code coverage by unit tests for ZenPack
-   ZEN-15746: Default icons for all components
-   ZEN-16216: Provide friendlier event message if there is connection
    failure due to user timeout
-   ZEN-18848: Incorrect impact relations
-   ZEN-18847: No node exist error when add component to Service
-   ZEN-18787: Dynamic View error for Service Processors component
-   ZEN-18863: Traceback during running 'zenpython run' command
-   ZEN-15808: Include status icon to all components affected by managed
    system
-   ZEN-16222: The 'Y' scale for the Processor Units Used of LPARs is
    not adjusting correctly
-   ZEN-15299: Long component load times
-   ZEN-16544: percent_pool_cycles missing from managed systems
    component
-   ZEN-15715: Traceback when attempting to open IBM Power device

<dl markdown="1">
<dt markdown="1">
1.0.2
</dt>
</dl>

-   ZEN-16881: Fix Links in the right hand Services pane
-   ZEN-16544: Fix missing percent_pool_cycles

<dl markdown="1">
<dt markdown="1">
1.0.1
</dt>
</dl>

-   Add pool cycles to managed systems that support them
-   ZEN-16510 Traceback on some datasources.

<dl markdown="1">
<dt markdown="1">
1.0.0
</dt>
</dl>

-   Initial release.

## Attachments:

-   [HMC_analytics.PNG](img/zenpack-hmc_analytics.png)
-   [HMC_events.PNG](img/zenpack-hmc_events.png)
-   [HMC_HEA_Ports.PNG](img/zenpack-hmc_hea_ports.png)
-   [HMC_HEAs.PNG](img/zenpack-hmc_heas.png)
-   [HMC_impact.PNG](img/zenpack-hmc_impact.png)
-   [HMC_IO_Devices.PNG](img/zenpack-hmc_io_devices.png)
-   [HMC_IO_Pools.PNG](img/zenpack-hmc_io_pools.png)
-   [HMC_Logical_HEA_Ports.PNG](img/zenpack-hmc_logical_hea_ports.png)
-   [HMC_Logical_HEAs.PNG](img/zenpack-hmc_logical_heas.png)
-   [HMC_LPAR_Profiles.PNG](img/zenpack-hmc_lpar_profiles.png)
-   [HMC_LPARs.PNG](img/zenpack-hmc_lpars.png)
-   [HMC_Managed_Systems.PNG](img/zenpack-hmc_managed_systems.png)
-   [HMC_Overview.PNG](img/zenpack-hmc_overview.png)
-   [HMC_Port_Groups.PNG](img/zenpack-hmc_port_groups.png)
-   [HMC_Processor_Pools.PNG](img/zenpack-hmc_processor_pools.png)
-   [HMC_Service_Processor.PNG](img/zenpack-hmc_service_processor.png)
-   [IBM_add_dialog.png](img/zenpack-ibm_add_dialog.png)
-   [IBM_add_menu.png](img/zenpack-ibm_add_menu.png)
-   [IBM_model_device.png](img/zenpack-ibm_model_device.png)
-   [Ibm_yuml_1.png](img/zenpack-ibm_yuml_1.png)
-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)
-   [HMC_analytics.PNG](img/zenpack-hmc_analytics.png)
-   [HMC_events.PNG](img/zenpack-hmc_events.png)
-   [HMC_HEA_Ports.PNG](img/zenpack-hmc_hea_ports.png)
-   [HMC_HEAs.PNG](img/zenpack-hmc_heas.png)
-   [HMC_impact.PNG](img/zenpack-hmc_impact.png)
-   [HMC_IO_Devices.PNG](img/zenpack-hmc_io_devices.png)
-   [HMC_IO_Pools.PNG](img/zenpack-hmc_io_pools.png)
-   [HMC_Logical_HEA_Ports.PNG](img/zenpack-hmc_logical_hea_ports.png)
-   [HMC_Logical_HEAs.PNG](img/zenpack-hmc_logical_heas.png)
-   [HMC_LPARs.PNG](img/zenpack-hmc_lpars.png)
-   [HMC_Managed_Systems.PNG](img/zenpack-hmc_managed_systems.png)
-   [HMC_Overview.PNG](img/zenpack-hmc_overview.png)
-   [HMC_Port_Groups.PNG](img/zenpack-hmc_port_groups.png)
-   [HMC_Processor_Pools.PNG](img/zenpack-hmc_processor_pools.png)
-   [HMC_Service_Processor.PNG](img/zenpack-hmc_service_processor.png)
-   [IBM_add_dialog.png](img/zenpack-ibm_add_dialog.png)
-   [IBM_add_menu.png](img/zenpack-ibm_add_menu.png)
-   [IBM_model_device.png](img/zenpack-ibm_model_device.png)
-   [Ibm_yuml_1.png](img/zenpack-ibm_yuml_1.png)
-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)
-   [HMC_LPAR_Profiles.PNG](img/zenpack-hmc_lpar_profiles.png)
-   [IBM_add_menu.png](img/zenpack-ibm_add_menu.png)
-   [HMC_analytics.PNG](img/zenpack-hmc_analytics.png)
-   [Ibm_yuml_1.png](img/zenpack-ibm_yuml_1.png)


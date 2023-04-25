# Dell PowerEdge

@lb[](img/zenpack-dell-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.Dell.PowerEdge

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.Dell.PowerEdge){.external-link}

## Dell PowerEdge ZenPack

The Dell PowerEdge ZenPack allows you to monitor Dell PowerEdge Servers
(including Dell EMC VxRail appliances based on PowerEdge Hardware),
including blade servers with the Dell PowerEdge M1000e chassis.

## Background

This ZenPack provides support for monitoring Dell PowerEdge Servers
(11G, 12G, 13G, and 14G), including blade servers with the Dell
PowerEdge M1000e chassis.

Monitoring is performed via the OpenManage Server Agent (OMSA) using the
SNMP API, on servers running either the Windows or Linux OS. This
ZenPack also provides support for monitoring via the Dell iDRAC using
the WSMAN interface, regardless of host OS.

**Note**: Please restart Zenoss after installing this ZenPack.

## Releases

Version 3.0.1 - [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2019/10/28:   Requires [WSMAN ZenPack](https://help.zenoss.com/display/in/ZenPacks.zenoss.WSMAN "ZenPack:WSMAN"){.external-link}:   Compatible with Zenoss 5.3.3 - 6.4 and Zenoss Cloud

Version 2.0.4 - [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2017/11/01:   Requires [WSMAN ZenPack](http://help.zenoss.com/display/in/ZenPacks.zenoss.WSMAN "ZenPack:WSMAN"){.external-link}:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.x.x

## Contents

-   [Features](#features)
-   [Discovery](#discovery)
    -   [Dell M1000e Blade Chassis](#dell-m1000e-blade-chassis)
    -   [Dell PowerEdge 11g, 12g, 13g, and 14g Servers](#dell-power-edge-11g-12g-13g-and-14g-servers)
    -   [Rack and Tower Servers](#rack-and-tower-servers)
    -   [Dell iDRAC (Dell Remote Access Controller)](#DellPowerEdge-DelliDRAC(DellRemoteAccessController))
    -   [iDRAC7, iDRAC8, and iDRAC9 Controllers](#idrac7-idrac8-and-idrac9-controllers)
-   [Performance Monitoring](#performance-monitoring)
-   [Event Management](#event-management)
-   [Installed Items](#installed-items)
    -   Configuration Properties:
    -   [Device Classes](#device-classes)
    -   [Event Classes](#event-classes)
    -   [Event Mappings](#event-mappings)
    -   [Event Plugins](#event-plugins)
    -   [Event Transforms](#event-transforms)
    -   [Modeler Plugins](#modeler-plugins)
    -   [Datasource Types](#datasource-types)
    -   [Monitoring Templates](#monitoring-templates)
-   [Dynamic View](#dynamic-view)
    -   Chassis Management Controller @lb[](img/zenpack-cmc_device_dv.png)
    -   PowerEdge Server @lb[](img/zenpack-poweredge_device_dv.png)
-   [Service Impact and Root Cause Analysis](#service-impact-and-root-cause-analysis)
-   [Usage](#usage)
    -   [Prerequisites](#prerequisites)
    -   [Adding ChassisController](#adding-chassis-controller)
    -   [Adding Linux SNMP Dell Blade/Rack Device](#DellPowerEdge-AddingLinuxSNMPDellBlade/RackDevice)
    -   [Adding Windows SNMP Dell Blade/Rack Device](#DellPowerEdge-AddingWindowsSNMPDellBlade/RackDevice)
    -   [Adding iDRAC6 Controller](#adding-idrac6-controller)
    -   [Adding iDRAC7 Controller](#adding-idrac7-controller)
    -   [Adding iDRAC8 Controller](#adding-idrac8-controller)
    -   [Adding iDRAC9 Controller](#adding-idrac9-controller)
    -   [zenbatchload](#zenbatchload)
-   [Limitations](#limitations)
-   [Troubleshooting](#troubleshooting)
    -   [iDRAC Connection Timeouts](#idrac-connection-timeouts)
-   [Changes](#changes)

## Features

The features added by this ZenPack be summarized as follows. They are
each detailed further below.

-   Initial discovery and continual synchronization of relevant
    components.
-   Performance monitoring.
-   Event monitoring and management.
-   Service impact and root cause analysis. (Requires Zenoss Service
    Dynamics)

## Discovery

### Dell M1000e Blade Chassis

The following components will be automatically discovered through the
Chassis Management Controller(CMC) IP address and the hostname you
provide. The properties and relationships will be continually
maintained.

Chassis Management Controller:   Attributes: Name, System Slot, Chassis Name, Service Tag, Product
    Name, Description, Version, Location, Firmware Version:   Relationships: Chassis Power Consumptions, Chassis Power Supply
    Units, Chassis Slots, Chassis Temperature Sensors

Chassis Power Consumptions:   Attributes: Name, Chassis Name, Current Usage, Peak Usage, Min
    Usage, Max Power, Status, Chassis Index, Chassis Location, Idle
    Power, Potential Power, Power Surplus:   Relationships: Chassis Management Controller

Chassis Power Supply Units:   Attributes: Name, Location, Chassis Name, Power in Amps, Power in
    Watts, Idle Power, Chassis Index:   Relationships: Chassis Management Controller

Chassis Slots:   Attributes: Name, Slot Name, Slot ID, Server Index, Service Tag,
    Model:   Relationships: Chassis Management Controller

Chassis Temperature Sensors:   Attributes: Name, Chassis Name, Front Panel, CMC Board, CMC
    Processor, State:   Relationships: Chassis Management Controller

Interfaces:   Attributes: IP Interface, IP Addresses (All), Description, MAC
    Address, Admin Status, Operational Status, IP Address (Primary),
    Type, Speed, MTU, Duplex Mode

### Dell PowerEdge 11g, 12g, 13g, and 14g Servers

The following components will be automatically discovered through the
Server IP address and the hostname you provide. The properties and
relationships will be continually maintained.

Chip Sets:   Attributes: Name, Slot Index, Speed, Status, Device Index, Chassis
    System Name, Data Bus Width, Adapter Fault, State Capability,
    Chassis Index, State Setting, Manufacturer, Model:   Relationships: Main System Chassis

File Systems:   Attributes: Mount Point, Storage Device, Total Bytes, Used Bytes,
    Free Bytes, Percent Util

Interfaces:   Attributes: IP Interface, IP Addresses (All), Description, MAC
    Address, Admin Status, Operational Status, IP Address (Primary),
    Type, Speed, MTU, Duplex Mode

Main System Chassis:   Attributes: Name, Chassis Name, Host Name, Service Code, Service
    Tag, Lock Present, Chassis Type, Device Index, Manufacturer, Model:   Relationships: Chip Sets, Cooling Fans, Memory Cards, Physical
    Disks, Virtual Disks, Ports, Processors, Processor Caches,
    Temperature Sensors

Memory Cards:   Attributes: Name, Chassis Name, Speed, Type, Asset Tag, Memory
    Status, Size, Device Index, State Capability, Location, State
    Settings, Error Count, Manufacturer, Model:   Relationships: Main System Chassis

Physical Disks:   Attributes: Name, Chassis Name, Consumers, Capacity, Used Space,
    Free Space, State, Host Name, Disk Number, Negotiated Speed,
    Protocol Type, Enclosure ID, Revision, Manufacturer, Model:   Relationships: Main System Chassis

Ports:   Attributes: Name, Port Name, Chassis Name, Connector Type, Security
    State, Port Status, Port Index, IRQ Level, Base IO Address:   Relationships: Main System Chassis

Power Consumptions:   Attributes: Name, Status, Warning Trap, Probe Type, Critical Trap,
    Location, Chassis Index:   Relationships: Main System Chassis

Processors:   Attributes: Name, Chassis Name, Server, Type, Core Count, Status,
    Device Index, Upgrade Info, Family, Current Speed, Voltage,
    Manufacturer, Model:   Relationships: Main System Chassis, Processor Caches

Processor Caches:   Attributes: Name, Server Name, Associativity, Current Size, Maximum
    Size, Policy, Cache Status, Speed, Device Index, Is Socketed,
    Current Type, Level, Processor Device Index, Type, Device Status,
    State Capability, State Settings, ECC Type, Supported Type, Device
    Location:   Relationships: Main System Chassis, Processor

Temperature Sensors:   Attributes: Name, Chassis Name, Probe Name, State, Temperature
    Status, Type, Maximum Failure Trap, Minimum Failure Trap, Maximum
    Warning Trap, Minimum Warning Trap, Probe Capability, Probe Index:   Relationships: Main System Chassis

Virtual Disks:   Attributes: Name, Type, Chassis Name, Disk Number, Disk Status, Read
    Policy, Write Policy, Cache Policy, Layout, Disk Cache:   Relationships: Main System Chassis

### Rack and Tower Servers

The following additional components apply only to Rack and Tower
servers.

Cooling Fans:   Attributes: Name, Number, Chassis Name, Location, Fan Status,
    Critical Trap, Warning Trap:   Relationships: Main System Chassis

### Dell iDRAC (Dell Remote Access Controller)

The following components will be automatically discovered through the
iDRAC IP address and the hostname you provide. The properties and
relationships will be continually maintained.

Chip Sets:   Attributes: Name, Slot Index, Speed, Status, Device Index, Chassis
    System Name, Slot Type, Slot Length, Data Bus Width, Adapter Fault,
    State Capability, Chassis Index, State Setting:   Relationships: Main System Chassis

Enclosures:   Attributes: Name, FQDD, Slot Count, Version, Product Name, Chassis
    Name, Chassis Package Type, Package Type, Removal Conditions,
    Manufacturer, Chassis Model, Part Number, Serial Number, Chassis
    Tag, Connector, Enclosure Position:   Relationships: Main System Chassis, Controller, Physical Disks

Main System Chassis:   Attributes: Name, Chassis Name, Host Name, Service Code, Service
    Tag, Lock Present, Chassis Type, Device Index, BIOS Release Date,
    BIOS Version String, Base Board Chassis Slot, Board Serial Number,
    CMC IP, Life Cycle Controller Version, Max CPU Sockets, Max DIMM
    Slots, Memory Max Capacity Size, Memory Total Size, System
    Generation, System Revision, Power State:   Relationships: NIC Ports, Chip Sets, Cooling Fans, Enclosures,
    Memory Cards, Physical Disks, Virtual Disks, Processors, Processor
    Caches, Controllers, Controller Batteries, Server Power Supplies,
    Server Power Supply Sensors, Softwares, Video Controllers, Analog
    Sensors, Digital Sensors

Memory Cards:   Attributes: Name, Chassis Name, Speed, Type, Asset Tag, Memory
    Status, Size, Device Index, State Capability, Location, State
    Settings, Error Count, Serial Number, Bank Label, Part Number, Rank,
    Current Speed:   Relationships: Main System Chassis

Physical Disks:   Attributes: Name, Chassis Name, Consumers, SAS Address, Capacity,
    Used Space, Free Space, State, Host Name, Product ID, Disk Number,
    Negotiated Speed, Protocol Type, Enclosure ID, Revision, Part
    Number, Max Capable Speed, Serial Number, Security State, Hot Spare
    Status, Media Type:   Relationships: Main System Chassis, Controller, Enclosure, Virtual
    Disks

Processors:   Attributes: Name, Chassis Name, Server, Type, Core Count, Status,
    Device Index, Upgrade Info, Family, Current Speed, Voltage, Enabled
    Threads Count, Enabled Cores Count, External Bus Clock Speed, Max
    Clock Speed, CPU Status:   Relationships: Main System Chassis, Processor Caches

Processor Caches:   Attributes: Name, Policy, Size, Status, Error Methodology,
    Associativity, SRAM Type, Level, Type:   Relationships: Processor

Softwares:   Attributes: Name, Software Name, Installation Date, Identity Info
    Type, Identity Info Value, Version, Vendor ID, Device ID, Build
    Number, Classifications, Component ID, Component Type, Major
    Version, Minor Version:   Relationships: Main System Chassis

Virtual Disks:   Attributes: Name, Type, Chassis Name, Disk Number, Disk Status, Read
    Policy, Write Policy, Cache Policy, Layout, Disk Cache, State, Size,
    Media Type, Stripe Size, Remaining Redundancy:   Relationships: Main System Chassis, Controller, Physical Disks

### iDRAC7, iDRAC8, and iDRAC9 Controllers

The following additional components apply only to iDRAC7, iDRAC8, and
iDRAC9 Controllers.

Analog Sensors:   Attributes: Name, Description, Location, Type, Possible States,
    Units, Unit Modifier, Upper Threshold Critical, Upper Threshold
    Non-Critical, Lower Threshold Critical, Lower Threshold Non-Critical:   Relationships: Main System Chassis

Controllers:   Attributes: Name, Description, Status:   Relationships: Main System Chassis, Controller Batteries, Enclosure,
    Physical Disks, Virtual Disks

Controller Batteries:   Attributes: Name, Predictive Capacity, Status, RAID State:   Relationships: Main System Chassis, Controller

Cooling Fans:   Attributes: Name, Number, Chassis Name, Location, Fan Status,
    Critical Trap, Warning Trap:   Relationships: Main System Chassis

Digital Sensors:   Attributes: Name, Description, Location, Type, Possible States:   Relationships: Main System Chassis

NIC Ports:   Attributes: Name, PCI Device ID, PCI Device Status, FQDD, Current
    MAC Address, Link Status:   Relationships: Main System Chassis

Server Power Supplies:   Attributes: Name, Description, Power Type, Status:   Relationships: Main System Chassis, Server Power Supply Sensors

Server Power Supply Sensors:   Attributes: Name, Description, Location, Type, Possible States,
    Units, Unit Modifier, Upper Threshold Critical, Upper Threshold
    Non-Critical, Lower Threshold Critical, Lower Threshold Non-Critical:   Relationships: Main System Chassis, Server Power Supply

Video Controllers:   Attributes: Name, Bus Number, Data Bus Width, Description, Last
    System Inventory Time, Last Update Time, PCI Device ID, PCI Vendor
    ID, Slot Type, Function Number, PCI Sub Device ID, PCI Sub Vendor
    ID, Slot Length:   Relationships: Main System Chassis

## Performance Monitoring

The following metrics will be collected every 5 minutes by default. Any
other Dell PowerEdge Server metrics can also be collected by adding them
to the appropriate monitoring template.

Power Consumptions:   Power Consumption: consumption in watts @lb[](img/zenpack-poweredge_linux_power_consumptions_power_consumption_graph.png)

Processor Caches:   Cache Utilization: usage in percentage @lb[](img/zenpack-poweredge_linux_processor_caches_cache_utilization_graph.png)

Temperature Sensors:   Temperature: current temperature in celsius @lb[](img/zenpack-poweredge_linux_temperature_sensors_temperature_graph.png)

Dell Remote Access Controller(iDRAC) will also provide performance
metrics data of the Dell PowerEdge Server. The following metrics will be
collected every 5 minutes by default. Any other Dell PowerEdge Server
metrics can also be collected by adding them to the appropriate
monitoring template.

Analog Sensors:   RPM: fan rate per minute @lb[](img/zenpack-poweredge_analog_sensors_rpm_graph.png):   Temperature: temperature in celsius @lb[](img/zenpack-poweredge_analog_sensors_temperature_graph.png):   Usage: utilization in percent @lb[](img/zenpack-poweredge_analog_sensors_usage_graph.png):   Voltage: voltage in volts @lb[](img/zenpack-poweredge_analog_sensors_voltage_graph.png)

**Note:** Main System Chassis, Cooling Fans, Processors and Server Power
Supplies show graphs based on related Analog Sensors.

NIC Ports:   Packets: Tx/Rx packet rate per minute @lb[](img/zenpack-poweredge_nic_ports_packets_graph.png):   Error Rate: Rx errors per minute @lb[](img/zenpack-poweredge_nic_ports_error_rate_graph.png)

Server Power Supply Sensors:   Current: electric current in amps @lb[](img/zenpack-poweredge_server_power_supply_sensors_current_graph.png):   Power: consumption in watts @lb[](img/zenpack-poweredge_server_power_supply_sensors_power_graph.png)

**Note:** Main System Chassis and Server Power Supplies show graphs
based on related Server Power Supply Sensors.

## Event Management

#### Lifecycle Log Monitoring on Dell PowerEdge iDRAC 7, 8 and 9 versions

Zenoss periodically polls the Dell PowerEdge iDRAC for Lifecycle Log
entries and creates Zenoss events when they occur. The event polling
runs by LifecycleLog datasource which is defined on the device level.

**LifecycleLog Data Source Fields**

-   Name: Specifies the name of the data source.
-   Type: Type of the datasource, *PowerEdge Event* by default.
-   Cycle Time(seconds): Sets the frequency the polling should be run,
    *${here/zPowerEdgeEventInterval}* by default.
-   Creation Time Stamp: Allows to filter the incoming events on the API
    side and avoid the collection of any events which occurred earlier
    than the selected value. The following values are possible for the
    field:
    -   Last Successful Run (default, initial value equals to *1 Day
        Ago*)
    -   1 Day Ago
    -   2 Days Ago
    -   5 Days Ago
    -   10 Days Ago

The Lifecycle Log entry closely matches that of a Zenoss event. This
means that corresponding Zenoss events will automatically clear when
their Lifecycle Log counterparts clear.

**Note:** To improve performance, LifeCycle audit level logs are not
monitored.

**Note:** Zenoss attempts to set the timestamp on Lifecycle Log events
to the timestamp the Dell PowerEdge iDRAC reported their occurrence
instead of the time that Zenoss collected them. For this reason, it is
recommended that both your Dell PowerEdge and Zenoss servers keep
accurate time.

The following fields will be populated for each event:

**Standard Zenoss Event Fields**

-   device: iDRAC device in one of the following device classes:
    -   */Server/Dell/iDRAC7*
    -   */Server/Dell/iDRAC8*
    -   */Server/Dell/iDRAC9*
-   component: Zenoss component related to the event.
-   count: Occurrences for the Lifecycle Log event.
-   eventKey: Lifecycle Log message ID for the event.
-   eventClassKey: Used as the first step in mapping an unknown event
    into an event class, equals *poweredge.idrac.lifecycle-log.event*.
-   eventGroup: Used to group similar types of events, equals
    eventClassKey.
-   rcvtime: Event creation time taken from *CreationTimeStamp*.
-   summary: Description or *descr* for the Lifecycle Log event.
-   severity: Mapped from the Lifecycle Log *PerceivedSeverity* for the
    event using the following table:
    -   Lifecycle Log Unknown = Zenoss Info
    -   Lifecycle Log Other = Zenoss Info
    -   Lifecycle Log Information = Zenoss Info
    -   Lifecycle Log Degraded/Warning = Zenoss Warning
    -   Lifecycle Log Minor = Zenoss Warning
    -   Lifecycle Log Major = Zenoss Error
    -   Lifecycle Log Critical = Zenoss Critical
    -   Lifecycle Log Fatal/NonRecoverable = Zenoss Critical

The following additional fields and potentially more will also be
populated for each event. These are the fields native to a Lifecycle Log
event. If an event occurs that has other fields, those fields will be
added with the same *poweredge.idrac.lifecycle-log* prefix.

**Additional Lifecycle Log Event Details**

-   poweredge.idrac.lifecycle-log.AgentID
-   poweredge.idrac.lifecycle-log.Category
-   poweredge.idrac.lifecycle-log.Comment
-   poweredge.idrac.lifecycle-log.ConfigResultsAvailable
-   poweredge.idrac.lifecycle-log.CreationTimeStamp
-   poweredge.idrac.lifecycle-log.ElementName
-   poweredge.idrac.lifecycle-log.FQDD
-   poweredge.idrac.lifecycle-log.InstanceID
-   poweredge.idrac.lifecycle-log.LogInstanceID
-   poweredge.idrac.lifecycle-log.LogName
-   poweredge.idrac.lifecycle-log.Message
-   poweredge.idrac.lifecycle-log.MessageArguments
-   poweredge.idrac.lifecycle-log.MessageID
-   poweredge.idrac.lifecycle-log.OwningEntity
-   poweredge.idrac.lifecycle-log.PerceivedSeverity
-   poweredge.idrac.lifecycle-log.RawEventData
-   poweredge.idrac.lifecycle-log.RecordID
-   poweredge.idrac.lifecycle-log.SequenceNumber

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

### Configuration Properties:

-   zPowerEdgeEventInterval - Interval to collect PowerEdge events, *180
    seconds* by default.

### Device Classes

-   /Devices/Server/Dell/ChassisController: Chassis Management
    Controller will be added in this device class using Chassis IP.

-   /Devices/Server/Linux/Dell: Linux Dell server will be added in this
    device class using device IP.

-   /Devices/Server/Windows/Dell: Windows Dell server will be added in
    this device class using device IP.

-   /Devices/Server/Dell/iDRAC6: iDRAC6 controller will be added in this
    device class using respective iDRAC6 IP.

-   /Devices/Server/Dell/iDRAC7: iDRAC7 controller will be added in this
    device class using respective iDRAC7 IP.

-   /Devices/Server/Dell/iDRAC8: iDRAC8 controller will be added in this
    device class using respective iDRAC8 IP.

-   /Devices/Server/Dell/iDRAC9: iDRAC9 controller will be added in this
    device class using respective iDRAC9 IP.

### Event Classes

-   /Status/PowerEdge: The event class covers the Dell PowerEdge
    statuses.

-   /PowerEdge: The event class covers Dell PowerEdge events.

-   /PowerEdge/Error: The error class covers Dell PowerEdge errors.

### Event Mappings

-   poweredge.idrac.lifecycle-log.event: Mapped to /PowerEdge event
    class.

-   poweredge.idrac.lifecycle-log.error: Mapped to /PowerEdge/Error
    event class.

### Event Plugins

-   PowerEdge Event: Mapped to LifecycleLog data source for iDRAC 7, 8
    and 9 devices.

### Event Transforms

-   /Status/PowerEdge: transforms event messages by mapping status codes
    for PrimaryStatus, LinkStatus, RaidStatus, RAIDState and
    TempRollupStatus.

### Modeler Plugins

The following plugins will be used for modeling a PowerEdge Blade or
Chassis Controller details, using the respective blade or controller IP
addresses via SNMP interface:

-   zenoss.snmp.NewDeviceMap: Determines OS and hardware manufacturer
    information based on the SNMP description (sysDescr).

-   zenoss.snmp.DeviceMap: Gathers sysDescr, sysContact, sysName, and
    sysLocation information and adds it to the device.

-   zenoss.snmp.InterfaceMap: Gathers IPv4 and IPv6 network interface
    information.

-   zenoss.snmp.HRFileSystemMap: Retrieves information about
    filesystems.

-   zenoss.dell.snmp.DellDeviceModeler: This plugin is for retrieving
    the basic Dell hardware and OS information.

-   zenoss.dell.snmp.PowerEdgeModeler: SNMP plugin that gathers Dell
    PowerEdge blade device information.

-   zenoss.dell.snmp.ChassisControllerModeler: This plugin is for
    modeling Chassis Controller.

The following plugins will be used for modeling a PowerEdge Rack or
Blade details, using the iDRAC controller via WSMAN interface:

-   DellIDRACModeler: This plugin is for retrieving the basic iDRAC
    manufacturer, firmware information.

-   iDRAC6Modeler: This plugin is for modeling Dell Remote Access
    Controller 6.

-   iDRAC7Modeler: This plugin is for modeling Dell Remote Access
    Controller 7.

-   iDRAC8Modeler: This plugin is for modeling Dell Remote Access
    Controller 8.

-   iDRAC9Modeler: This plugin is for modeling Dell Remote Access
    Controller 9.

### Datasource Types

-   SNMP
-   WSMAN

### Monitoring Templates

-   AnalogSensor (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   AnalogSensor-Amps (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   AnalogSensor-DegreesC (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   AnalogSensor-DegreesF (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   AnalogSensor-Percentage (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   AnalogSensor-RPM (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   AnalogSensor-Volts (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   AnalogSensor-Watts (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   ChassisPowerConsumption (/Server/Dell/ChassisController)
-   Controller (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   CoolingFan (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   DigitalSensor (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   MemoryCard (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   NICPort (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   PhysicalDisk (/Server/Linux/Dell, /Server/Windows/Dell,
    /Server/Dell/iDRAC6, /Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   PowerConsumption (/Server/Linux/Dell, /Server/Windows/Dell)
-   PowerEdgeServer (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   ProcessorCache (/Server/Linux/Dell, /Server/Windows/Dell)
-   Processor (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   ServerPowerSupply (/Server/Dell/iDRAC7, /Server/Dell/iDRAC8,
    /Server/Dell/iDRAC9)
-   ServerPowerSupplySensor-Amps (/Server/Dell/iDRAC7,
    /Server/Dell/iDRAC8, /Server/Dell/iDRAC9)
-   ServerPowerSupplySensor-Watts (/Server/Dell/iDRAC7,
    /Server/Dell/iDRAC8, /Server/Dell/iDRAC9)
-   Temperature (/Server/Linux/Dell, /Server/Windows/Dell)

## Dynamic View

To provide a high-level overview of the modeled device, on device level
a separate Dynamic View diagram is provided.

### Chassis Management Controller @lb[](img/zenpack-cmc_device_dv.png)

-   Devices
-   Chassis Management Controllers
-   Chassis Power Supply Units
-   Chassis Temperature Sensors

### PowerEdge Server @lb[](img/zenpack-poweredge_device_dv.png)

-   Devices
-   Chip Sets
-   Cooling Fans
-   Main System Chassis
-   Processors
-   Server Power Supplies
-   Server Power supply Sensors

## Service Impact and Root Cause Analysis

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact and root cause analysis capabilities for
services running on Dell PowerEdge. The service impact relationships
shown in the diagram and described below are automatically added. These
will be included in any services that contain one or more of the
explicitly mentioned components.

@lb[](img/zenpack-chassis_mgmt_controller_impact.jpg)
**@lb[](img/zenpack-poweredge_server_impact.jpg)**

**Internal Impact Relationships:**

-   Chassis temperature sensor and chassis power supply unit failure
    impacts chassis management controller.
-   Chassis management controller failure impacts all related chassis
    slots, chassis power consumption, and the device.
-   Chassis management controller failure impacts all the blade devices
    available in its slots.

<!-- -->

-   Server power supply sensor failure impacts server power supply.
-   Processor failure impacts processor cache.
-   Temperature, server power supply, cooling fan, chip set, and
    processor failure impacts main system chassis.
-   Controller battery failure impacts controller.
-   Main system chassis failure impacts device, video controller,
    software, port, nic port, memory card, digital sensor, power
    consumption, analog sensor, controller.
-   Controller and enclosure failure impacts physical disks.
-   Physical disk failure impacts virtual disk.

**External Impact Relationships:**

-   In the scope of VxRail integration, a PowerEdge physical disk
    failure impacts vSphere datastore.

Most of the impacts described above follow the default policy of a node
being in the worst state of the nodes that impact it. For example, a
Chassis Management Controller failure will imply that all related blade
devices are also failed.

## Usage

### Prerequisites

External Dependencies:

-   OpenManage Server Administrator Agent 7.2.0 (OMSA Agent) should be
    running on Linux/Windows devices.

-   OMSA is only required for "Adding Linux SNMP Dell Blade/Rack Device"
    and "Adding Windows SNMP Dell Blade/Rack Device".

-   This should be verified using snmpwalk from your Zenoss server:

        snmpwalk -v2c -c [community] [hostname]

### Adding ChassisController

Use the following steps to start monitoring ChassisController using the
Zenoss web interface.

-   Navigate to the Infrastructure page. @lb[](img/zenpack-add_menu.png)
-   Navigate to organizer Devices/Server/Dell/ChassisController.
-   Choose Add a Single Device from the add button.

Fill out the form. @lb[](img/zenpack-cmc_add_dialog.png)

-   *Name* can be anything you want.
-   *Hostname or IP* must be resolvable and accessible from the
    collector server chosen in the *Collector* field.
-   Optionally, click *More...* and edit the *SNMP Community* field.
-   Click *ADD*.

### Adding Linux SNMP Dell Blade/Rack Device

Use the following steps to start monitoring Linux Dell PowerEdge device
using the Zenoss web interface.

-   Navigate to the Infrastructure page. @lb[](img/zenpack-add_menu.png)
-   Navigate to organizer Devices/Server/Linux/Dell.
-   Choose Add a Single Device from the add button.

Fill out the form. @lb[](img/zenpack-poweredge_linux_add_dialog.png)

-   *Name* can be anything you want.
-   *Hostname or IP* must be resolvable and accessible from the
    collector server chosen in the *Collector* field.
-   Optionally, click *More...* and edit the *SNMP Community* field.
-   Click *ADD*.

Dell Blade/Rack server that runs on Linux will be added in the
/Devices/Server/Linux/Dell device class.

### Adding Windows SNMP Dell Blade/Rack Device

Use the following steps to start monitoring Windows Dell PowerEdge
device using the Zenoss web interface.

-   Navigate to the Infrastructure page. @lb[](img/zenpack-add_menu.png)
-   Navigate to organizer Devices/Server/Windows/Dell.
-   Choose Add a Single Device from the add button.

Fill out the form. @lb[](img/zenpack-poweredge_windows_add_dialog.png)

-   *Name* can be anything you want.
-   *Hostname or IP* must be resolvable and accessible from the
    collector server chosen in the *Collector* field.
-   Optionally, click *More...* and edit the *SNMP Community* field.
-   Click *ADD*.

Dell Blade/Rack server that runs on Windows will be added in the
/Devices/Server/Windows/Dell device class.

### Adding iDRAC6 Controller

**Note:** Dell PowerEdge 3.0.0 and greater no longer supports iDRAC6.

Use the following steps to start monitoring iDRAC6 using the Zenoss web
interface.

-   Navigate to the Infrastructure page. @lb[](img/zenpack-add_menu.png)
-   Navigate to organizer Devices/Server/Dell/iDRAC6.
-   Choose Add a Single Device from the add button.

Fill out the form. @lb[](img/zenpack-idrac6_add_dialog.png)

-   *Name* can be anything you want.
-   *Hostname or IP* must be resolvable and accessible from the
    collector server chosen in the *Collector* field.
-   Click *ADD*.
-   iDRAC6 controller of Dell Blade server will be added in the
    /Devices/Server/Dell/iDRAC6 device class.

Use the following steps for successful modeling:

-   Select the added device.
-   Navigate to the overview page. @lb[](img/zenpack-idrac6_connection_info.png)
-   Click on the *edit* button in the Connection Information section.
-   In the appeared dialog fill in WSMAN Username, WSMAN Password, WSMAN
    SSL and WSMAN Port fields.
-   Click on the *SUBMIT AND REMODEL* button.

### Adding iDRAC7 Controller

Use the following steps to start monitoring iDRAC7 using the Zenoss web
interface.

-   Navigate to the Infrastructure page. @lb[](img/zenpack-add_menu.png)
-   Navigate to organizer Devices/Server/Dell/iDRAC7.
-   Choose Add a Single Device from the add button.

Fill out the form. @lb[](img/zenpack-idrac7_add_dialog.png)

-   *Name* can be anything you want.
-   *Hostname or IP* must be resolvable and accessible from the
    collector server chosen in the *Collector* field.
-   Click *ADD*.
-   iDRAC7 controller will be added in the /Devices/Server/Dell/iDRAC7
    device class.

Use the following steps for successful modeling.

-   Select the added device.
-   Navigate to the overview page. @lb[](img/zenpack-idrac7_connection_info.png)
-   Click on the *edit* button in the Connection Information section.
-   In the appeared dialog fill in WSMAN Username, WSMAN Password, WSMAN
    SSL and WSMAN Port fields.
-   Click on the *SUBMIT AND REMODEL* button.

### Adding iDRAC8 Controller

Use the following steps to start monitoring iDRAC8 using the Zenoss web
interface.

-   Navigate to the Infrastructure page. @lb[](img/zenpack-add_menu.png)
-   Navigate to organizer Devices/Server/Dell/iDRAC8.
-   Choose Add a Single Device from the add button.

Fill out the form. @lb[](img/zenpack-idrac8_add_dialog.png)

-   *Name* can be anything you want.
-   *Hostname or IP* must be resolvable and accessible from the
    collector server chosen in the *Collector* field.
-   Click *ADD*.
-   iDRAC8 controller will be added in the /Devices/Server/Dell/iDRAC8
    device class.

Use the following steps for successful modeling.

-   Select the added device.
-   Navigate to the overview page. @lb[](img/zenpack-idrac8_connection_info.png)
-   Click on the *edit* button in the Connection Information section.
-   In the appeared dialog fill in WSMAN Username, WSMAN Password, WSMAN
    SSL and WSMAN Port fields.
-   Click on the *SUBMIT AND REMODEL* button.

### Adding iDRAC9 Controller

Use the following steps to start monitoring iDRAC9 using the Zenoss web
interface.

-   Navigate to the Infrastructure page. @lb[](img/zenpack-add_menu.png)
-   Navigate to organizer Devices/Server/Dell/iDRAC9.
-   Choose Add a Single Device from the add button.

Fill out the form. @lb[](img/zenpack-idrac9_add_dialog.png)

-   *Name* can be anything you want.
-   *Hostname or IP* must be resolvable and accessible from the
    collector server chosen in the *Collector* field.
-   Click *ADD*.
-   iDRAC9 controller will be added in the /Devices/Server/Dell/iDRAC9
    device class.

Use the following steps for successful modeling.

-   Select the added device.
-   Navigate to the overview page. @lb[](img/zenpack-idrac9_connection_info.png)
-   Click on the *edit* button in the Connection Information section.
-   In the appeared dialog fill in WSMAN Username, WSMAN Password, WSMAN
    SSL and WSMAN Port fields.
-   Click on the *SUBMIT AND REMODEL* button.

### zenbatchload

Alternatively, you can use zenbatchload to add devices from the command
line. To do this, you must create a file with contents similar to the
following. Replace all values in angle brackets with your values minus
the brackets. Multiple devices can be added under the same sections.

    '/Devices/Server/Dell/ChassisController' setManageIp=""
    '/Devices/Server/Dell/iDRAC8' setManageIp="", zWSMANUsername='', zWSMANPassword='', zWSMANPort=443, zWSMANUseSSL='true'
    '/Devices/Server/Dell/iDRAC7' setManageIp="", zWSMANUsername='', zWSMANPassword='', zWSMANPort=443, zWSMANUseSSL='true'
    '/Devices/Server/Dell/iDRAC6' setManageIp="", zWSMANUsername='', zWSMANPassword='', zWSMANPort=443, zWSMANUseSSL='true'
    '/Devices/Server/Windows/Dell' setManageIp=""
    '/Devices/Server/Linux/Dell' setManageIp=""

Examples:

    /Server/Dell/ChassisController CMC_1 setManageIp='10.100.10.30'
    /Server/Dell/iDRAC6 iDRAC6_1 setManageIp='10.100.10.32', zWSMANUsername='root', zWSMANPassword='calvin'
    /Server/Dell/iDRAC7 iDRAC7_1 setManageIp='10.100.10.31', zWSMANUsername='root', zWSMANPassword='calvin'
    /Server/Dell/iDRAC8 iDRAC8_1 setManageIp='10.100.10.30', zWSMANUsername='root', zWSMANPassword='calvin'
    /Server/Windows/Dell Windows-Blade setManageIp='10.100.10.27'
    /Server/Linux/Dell Linux-Blade setManageIp='10.100.10.29'

You can then load the Devices using zenbatchload with the following
command.

    zenbatchload <filename>

## Limitations

-   Dell Servers running VMware are not monitored by this ZenPack.
-   Currently, this ZenPack does not recognize/model IO modules and
    Chassis Fans.
-   The HP Proliant Mibs were inadvertently added to the Dell PowerEdge
    ZenPack in a previous version. v2.0.4 will remove them. If you have
    the HP Proliant ZenPack installed, you will need to reinstall it
    after upgrading to 2.0.4 in order to have the Mib definitions
    restored.
-   Dell PowerEdge 3.0.0 and greater no longer supports iDRAC6.

## Troubleshooting

### iDRAC Connection Timeouts

It was found that WSMAN API isn't available for iDRAC 7 device when
1.30.30 firmware is installed, 1.31.30 update has resolved the issue.
Therefore, if you get `Fault Value: s:Receiver wsman:TimedOut` error
while connecting to your iDRAC device via WSMAN API, make sure the
firmware version is updated to the recent stable version. The timeout
error may appear on the other iDRAC versions as well.

Another confirmed solution is a restart of Dell iDRAC interface, use the
following steps to restart the interface: - Open a browser software,
enter the IP address of your iDRAC interface and access the
administrative web interface. - On the prompt screen, enter the
administrative login information. After a successful login, the
administrative menu will be displayed.

    Factory default access information: Username: root Password: calvin

-   Access the iDRAC settings menu, access the Troubleshooting tab and
    select the Diagnostics Console option.
-   On the Diagnostics screen, click on the Reset button to restart your
    iDRAC interface. This will not restart the Dell server, only the
    iDRAC interface.
-   Wait a couple of minutes for the iDRAC interface to come back on.

## Changes

3.0.1

-   Fix missed runs in zenpython from client iDRAC device. (ZPS-4694)
-   Handle empty empty data from iDRAC device. (ZPS-4794)
-   Don't generate events for physical drives in Non-RAID state.
    (ZPS-4924)
-   Notify with an event in case attempt to model using wrong device
    class. (ZPS-5897)
-   Fix traceback during modeling of analog sensors components.
    (ZPS-6104)
-   Fix modeling error AttributeError: 'Item' object has no attribute
    'SASAddress'. (ZPS-6393)
-   Fix modeling failure related to embedded Cache drives for Dell EMC
    VxRail device. (ZPS-6522)
-   Fix collection failures related to
    embedded·Cache·drives·for·Dell·EMC·VxRail·device. (ZPS-6546)
-   Tested with Zenoss Cloud, Zenoss 6.4.1 and Service Impact 5.5.1.

3.0.0

-   Convert Dell PowerEdge device classes configuration to ZenPackLib
    format. (ZPS-3678)
-   Convert monitoring templates to ZPL format. (ZPS-3682)
-   Collect Lifecycle Log events on Dell PowerEdge iDRAC 7, 8 and 9
    versions. (ZPS-4006)
-   Add PrimaryStatus threshold to monitor for disk failures on Dell
    PowerEdge iDRAC 6, 7, 8 and 9 versions. (ZPS-280)
-   Monitor Analog and Digital sensor components on iDRAC 7, 8 and 9.
    (ZPS-3905)
-   Remove Disk Utilization graph from PhysicalDisk monitoring template
    for Dell iDRAC and Linux/Windows SNMP devices, as in a
    normally-configured server, we would always expect available RAID
    space to be zero. (ZPS-3717, ZPS-4596)
-   Convert Dell PowerEdge components to ZenPackLib format. (ZPS-3681)
-   Update Processor template with ClockSpeed data source on all the
    supported iDRACs. (ZPS-3673)
-   Fix SNMP index and device name for Virtual Disk modeling. (ZPS-2482,
    ZPS-1155)
-   Add support for Controller Battery component and associate it with a
    controller. Rename Enclosure Views component to Enclosures.
    (ZPS-4283)
-   Associate enclosure, physical and virtual disks with their RAID
    controller. Associate enclosure and physical disks with their
    virtual disks. Associate server power supply with its server power
    supply sensors. (ZPS-4284)
-   Improve Impact relationships. (ZPS-4285)
-   Improve Dependency View relationships. (ZPS-4287)
-   Fix chassis modeling. (ZPS-638)
-   Rename duplicated 'Name' column for Chassis Power Supply Units to
    'Location'. (ZPS-4503)
-   Remove spaces from component id's and replace with underscore.
    (ZPS-4418)
-   Add impact relations between Dell PowerEdge Physical Disks and
    vSphere vSAN Datastores. (ZPS-4518)
-   Fix modeling errors and add 'Troubleshooting' section with 'iDRAC
    connection timeouts' sub-section to the documentation. (ZPS-4365)
-   Ignore SNMP monitoring on iDRAC devices. (ZPS-4647)
-   Add hardware level metrics and graphs for Analog Sensors, Server
    Power Supply sensors, NIC ports and display associated sensor graphs
    for Cooling Fans, Processors and Main System Chassis. (ZPS-4574)
-   Return data for RAIDState datasource on Controller component.
    (ZPS-4590)
-   Move iDRAC 7/8/9 templates to "/Server/Dell" class. (ZPS-4704)
-   Fix "Changes in configuration applied" message on repeatable
    modeling of iDRAC, Chassis Controller, Windows and Linux Dell
    devices. (ZPS-4458, ZPS-4749, ZPS-4750)
-   Show correct WSMAN connection information for iDRAC 7, 8 and 9 on
    the overview page. (ZPS-4405)
-   Handle rare parsing errors on event monitoring. (ZPS-4691)
-   Tested with Zenoss Resource Manager 5.3.3, Zenoss Resource Manager
    6.2.1, Zenoss Cloud and Service Impact 5.3.1

2.0.4

-   Fix Dell PowerEdge ZP removed software component navigation menu for
    all devices (ZPS-2016)
-   Fix Dell PowerEdge ZenPack objects.xml includes HP MIBs (ZPS-244)
-   Tested with Zenoss 5.3.2 / 4.2.5 RPS 743

2.0.3

-   Fix PowerEdgeModeler modeling. (SVC-833m, ZEN-23224)
-   Fix Dell PowerEdge 2.0.2 breaks Modeling Plugins page (ZPS-1273)
-   Fix modeling of IDRAC version 7. (ZEN-21718)

2.0.2

-   Add iDRAC8 and Dell 13G Server support. (ZEN-20738)
-   Add NIC components to iDRAC7 and iDRAC8 controllers. (ZEN-17954)
-   Several user interface fixes. (ZEN-20376, ZEN-16190, ZEN-14015,
    ZEN-13987)

2.0.1

-   Fix "compname" error during modeling. (ZEN-13273)

2.0.0

-   Add support for iDRAC.

1.0.0

-   Initial release.

## Attachments:

-   [add_menu.png](img/zenpack-add_menu.png)
-   [chassis_mgmt_controller_impact.jpg](img/zenpack-chassis_mgmt_controller_impact.jpg)
-   [cmc_add_dialog.png](img/zenpack-cmc_add_dialog.png)
-   [cmc_device_dv.png](img/zenpack-cmc_device_dv.png)
-   [dell-zenpack.png](img/zenpack-dell-zenpack.png)
-   [idrac6_add_dialog.png](img/zenpack-idrac6_add_dialog.png)
-   [idrac6_connection_info.png](img/zenpack-idrac6_connection_info.png)
-   [idrac7_add_dialog.png](img/zenpack-idrac7_add_dialog.png)
-   [idrac7_connection_info.png](img/zenpack-idrac7_connection_info.png)
-   [idrac8_add_dialog.png](img/zenpack-idrac8_add_dialog.png)
-   [idrac9_add_dialog.png](img/zenpack-idrac9_add_dialog.png)
-   [idrac9_connection_info.png](img/zenpack-idrac9_connection_info.png)
-   [poweredge_analog_sensors_rpm_graph.png](img/zenpack-poweredge_analog_sensors_rpm_graph.png)
-   [poweredge_analog_sensors_temperature_graph.png](img/zenpack-poweredge_analog_sensors_temperature_graph.png)
-   [poweredge_analog_sensors_usage_graph.png](img/zenpack-poweredge_analog_sensors_usage_graph.png)
-   [poweredge_analog_sensors_voltage_graph.png](img/zenpack-poweredge_analog_sensors_voltage_graph.png)
-   [poweredge_device_dv.png](img/zenpack-poweredge_device_dv.png)
-   [poweredge_linux_add_dialog.png](img/zenpack-poweredge_linux_add_dialog.png)
-   [poweredge_linux_power_consumptions_power_consumption_graph.png](img/zenpack-poweredge_linux_power_consumptions_power_consumption_graph.png)
-   [poweredge_linux_processor_caches_cache_utilization_graph.png](img/zenpack-poweredge_linux_processor_caches_cache_utilization_graph.png)
-   [poweredge_linux_temperature_sensors_temperature_graph.png](img/zenpack-poweredge_linux_temperature_sensors_temperature_graph.png)
-   [poweredge_nic_ports_error_rate_graph.png](img/zenpack-poweredge_nic_ports_error_rate_graph.png)
-   [poweredge_nic_ports_packets_graph.png](img/zenpack-poweredge_nic_ports_packets_graph.png)
-   [poweredge_server_impact.jpg](img/zenpack-poweredge_server_impact.jpg)
-   [poweredge_server_power_supply_sensors_current_graph.png](img/zenpack-poweredge_server_power_supply_sensors_current_graph.png)
-   [poweredge_server_power_supply_sensors_power_graph.png](img/zenpack-poweredge_server_power_supply_sensors_power_graph.png)
-   [poweredge_windows_add_dialog.png](img/zenpack-poweredge_windows_add_dialog.png)
-   [idrac8_connection_info.png](img/zenpack-idrac8_connection_info.png)
-   [chassis_mgmt_controller_impact.jpg](img/zenpack-chassis_mgmt_controller_impact.jpg)
-   [add_menu.png](img/zenpack-add_menu.png)
-   [cmc_add_dialog.png](img/zenpack-cmc_add_dialog.png)
-   [cmc_device_dv.png](img/zenpack-cmc_device_dv.png)
-   [dell-zenpack.png](img/zenpack-dell-zenpack.png)
-   [idrac6_add_dialog.png](img/zenpack-idrac6_add_dialog.png)
-   [idrac6_connection_info.png](img/zenpack-idrac6_connection_info.png)
-   [idrac7_add_dialog.png](img/zenpack-idrac7_add_dialog.png)
-   [idrac7_connection_info.png](img/zenpack-idrac7_connection_info.png)
-   [idrac8_add_dialog.png](img/zenpack-idrac8_add_dialog.png)
-   [idrac8_connection_info.png](img/zenpack-idrac8_connection_info.png)
-   [idrac9_add_dialog.png](img/zenpack-idrac9_add_dialog.png)
-   [idrac9_connection_info.png](img/zenpack-idrac9_connection_info.png)
-   [poweredge_analog_sensors_rpm_graph.png](img/zenpack-poweredge_analog_sensors_rpm_graph.png)
-   [poweredge_analog_sensors_temperature_graph.png](img/zenpack-poweredge_analog_sensors_temperature_graph.png)
-   [poweredge_analog_sensors_usage_graph.png](img/zenpack-poweredge_analog_sensors_usage_graph.png)
-   [poweredge_analog_sensors_voltage_graph.png](img/zenpack-poweredge_analog_sensors_voltage_graph.png)
-   [poweredge_device_dv.png](img/zenpack-poweredge_device_dv.png)
-   [poweredge_linux_power_consumptions_power_consumption_graph.png](img/zenpack-poweredge_linux_power_consumptions_power_consumption_graph.png)
-   [poweredge_linux_add_dialog.png](img/zenpack-poweredge_linux_add_dialog.png)
-   [poweredge_linux_processor_caches_cache_utilization_graph.png](img/zenpack-poweredge_linux_processor_caches_cache_utilization_graph.png)
-   [poweredge_linux_temperature_sensors_temperature_graph.png](img/zenpack-poweredge_linux_temperature_sensors_temperature_graph.png)
-   [poweredge_nic_ports_error_rate_graph.png](img/zenpack-poweredge_nic_ports_error_rate_graph.png)
-   [poweredge_nic_ports_packets_graph.png](img/zenpack-poweredge_nic_ports_packets_graph.png)
-   [poweredge_server_impact.jpg](img/zenpack-poweredge_server_impact.jpg)
-   [poweredge_server_power_supply_sensors_current_graph.png](img/zenpack-poweredge_server_power_supply_sensors_current_graph.png)
-   [poweredge_server_power_supply_sensors_power_graph.png](img/zenpack-poweredge_server_power_supply_sensors_power_graph.png)
-   [poweredge_windows_add_dialog.png](img/zenpack-poweredge_windows_add_dialog.png)
-   [idrac8_connection_info.png](img/zenpack-idrac8_connection_info.png)
-   [idrac6_add_dialog.png](img/zenpack-idrac6_add_dialog.png)


# HP Proliant - Commercial

@lb[](img/zenpack-hp-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.HP.Proliant

## HP Proliant (Commercial) ZenPack

Monitoring HP Proliant G6/G7/G8/G9/G10 rack/blade servers and
enclosures.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 3.3.5 - [Download](https://delivery.zenoss.com/){.external-link}:   Release on 2020/05/21:   Requires [WBEM ZenPack](http://help.zenoss.com/display/in/WBEM){.external-link},[PythonCollector ZenPack](http://help.zenoss.com/display/in/PythonCollector){.external-link},[ ZenPackLib ZenPack](http://help.zenoss.com/display/in/ZenPackLib){.external-link} (&gt;=2.0.6):   Compatible with Zenoss 4.2.5-6.4.1 and Zenoss Cloud

Version 3.2.2 - [Download](https://delivery.zenoss.com/){.external-link}:   Release on 2017/04/03:   Requires [WBEM ZenPack](http://help.zenoss.com/display/in/WBEM){.external-link},[PythonCollector ZenPack](http://help.zenoss.com/display/in/PythonCollector){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss Core
    5.1.x, Zenoss Core 5.2.x, Zenoss Resource Manager 4.2.x, Zenoss
    Resource Manager 5.0.x, Zenoss Resource Manager 5.1.x, Zenoss
    Resource Manager 5.2.x

## Contents

-   [Background](#background)
-   [External Dependencies](#external-dependencies)
-   [Features](#features)
    -   [Discovery](#discovery)
    -   [Monitoring](#monitoring)
    -   [Event Management](#event-management)
    -   [Service Impact](#service-impact)
-   [Data Collection](#data-collection)
    -   [SNMP](#snmp)
    -   [ILO](#ilo)
    -   [WBEM](#wbem)
-   [Usage](#usage)
    -   [Adding SNMP Onboard Administrator Device         (Enclosure)](#HPProliant-Commercial-AddingSNMPOnboardAdministratorDevice(Enclosure))
    -   [Adding Linux SNMP or Windows (SNMP) Blade/Rack Device](#HPProliant-Commercial-AddingLinuxSNMPorWindows(SNMP)Blade/RackDevice)
    -   [Adding ILO Device](#adding-ilo-device)
    -   [Adding ILO Device         (SNMP)](#HPProliant-Commercial-AddingILODevice(SNMP))
    -   [Adding ESXi Device](#adding-esxi-device)
    -   [Combining HP Proliant SNMP monitoring with existing Device Classes](#combining-hpproliant-snmp-monitoring-with-existing-device-classes)
    -   [Command Line Tools](#command-line-tools)
-   [Installed Items](#installed-items)
-   [Required Daemons](#required-daemons)
-   [Upgrade](#upgrade)
-   [Limitations](#limitations)
-   [Known Issues](#known-issues)
    -   [Known Issue when monitoring systems with Failover Onboard Administrators](#known-issue-when-monitoring-systems-with-failover-onboard-administrators)
    -   [Known Issue upgrading from 1.0 to 3.0](#)
    -   [Known issue regarding ilo unknown or N/A values](#HPProliant-Commercial-KnownissueregardingilounknownorN/Avalues)
    -   [Known issue regarding ilo monitoring](#known-issue-regarding-ilo-monitoring)
    -   [Known issue when removing ZenPack](#known-issue-when-removing-zenpack)
-   [Changes](#changes)

## [Background](#contents)

This ZenPack provides support for monitoring HP Proliant Servers (G6,
G7, G8, G9, and G10), including blade servers with the HP Proliant c7000
Enclosure. Discovery and monitoring are performed using SNMP, iLO
(XML/HTTP), and/or WBEM protocols depending on environment.

This ZenPack currently supports HP Proliant servers running Windows or
Linux (with installed/configured HP SIM SNMP subagent), HP Enclosures
(via SNMP) as well as iLO devices (via either iLO or SNMP) and VMWare
ESXi (using HP custom ESXi with WBEM/CIM access configured).

It is important to note that not all features of this ZenPack are
supported across all protocols, since each of them provides a part, but
not all, of the total information used by the ZenPack. This limitation
is based on the amount and quality information that is available from
each of the supported protocol. What this means is that certain metrics
for a given component type (such as a temperature sensor) may or may not
be available depending on the type of device that is monitored and/or on
the protocol used to collect that data.

## [External Dependencies](#contents)

This ZenPack relies on several protocols to achieve coverage of various
aspects of the HP Proliant architecture. At the most basic level, SNMP
should be configured so as to facilitate access to HP/Compaq MIBs
(CPQSINFO-MIB, CPQRACK-MIB, etc) and the associated OIDs. Support on a
bare metal install of Linux or Windows OS, for example, requires
installation of HP SIM and its associated software components, including
a SNMP subagent and associated configuration for its use with the OS
SNMP agent. Configuration of these software components is covered by
various documentation available from HP and is beyond the scope of this
document.

SNMP is also supported natively by HP OnboardAdministrator (if
available) and optionally by the iLO management interface.

As noted above, iLO management interface can be monitored (as a Zenoss
device) via iLO protocol (essentially XML via HTTP) or SNMP (which can
be enabled in the iLO GUI interface).

An additional important item to note is that the iLO management
interface GUI requires that the associated server's FQDN and IP address
be set manually.
This ZenPack requires the configuration of FQDN(or hostname)/IP be set
in order for Zenoss to create associations on its side between monitored
Proliant servers and their associated iLO device in Zenoss.

Support for HP Proliant hardware running VMWare ESXi OS relies on a
custom ESXi image available from HP. This custom image provides support
for Proliant-specific monitoring and performance data that is not
avaiable using the version of ESXi provided by VMWare. Additionally,
WBEM support must be configured and enabled on the ESXi host.

## [Features](#contents)

The features added by this ZenPack can be summarized as follows. They are each detailed further below.
:   Initial discovery and continual synchronization of relevant
    components:   Performance monitoring:   Event management and monitoring:   Command line utilities for troubleshooting and diagnostics:   Optional service impact with addition of Zenoss Service Dynamics
    product

### [Discovery](#contents)

The following components will be automatically discovered using either
the SNMP, iLO, or WBEM related connection parameters you provide. The
properties and relationships will be continually updated on Zenoss'
normal remodeling interval which defaults to every 12 hours.

HPEnclosure:   Attributes: Firmware Version, Model, Part Number, Serial Number,
    Spare Part Number:   Relationships: Cooling Fan, Device Bay, Interconnect Bay, Onboard
    Administrator, Power Supply, Temp Sensor, HPTemperatureSensors,
    HPThermalSubsystem

HPDeviceBay:   Attributes: BIOS Revision, Blade Device Link, Firmware Version, Part
    Number, Product ID, Service Tag, Slot Number, Spare Part Number:   Relationships: Enclosure

HPEnclosureCoolingFan:   Attributes: Location, Part Number, Present, Redundant, Spare Part
    Number:   Relationships: Enclosure

HPInterconnectBay:   Attributes: Product Name, Location, Part Number, Present, Serial
    Number, Spare Part Number, Switch Index:   Relationships: Enclosure

HPOnboardAdmin:   Attributes: OAIndex, UUID, Bay Number, Part Number, Present,
    Redundant, Role, Serial Number, Spare Part Number, Enclosure Serial
    Number:   Relationships: Enclosure

HPTemperatureSensor:   Attributes: Location, Threshold, Threshold Type:   Relationships: Enclosure

HPChassis:   Attributes: Total RAM, Product ID, Product, Server Name, Serial
    Number, Enclosure Manager Serial, Enclosure Manager Name, Enclosure
    Manager IP, Enclosure Manager URL:   Relationships: Processor, Cooling Fan, Logical Drive, Management
    Controller, Memory Slot, Network Interface, NIC, HPOSHypervisor, PCI
    Device, Physical Drive, Power Supply, System Board, Temp Sensor,
    RAID Controller, FC Adapter, FC Port

HPFibreChannelAdapter:   Attributes: Description, Device ID:   Relationships: Chassis, FC Port

HPFibreChannelPort:   Attributes: Description, Device ID, WWN, WWPN:   Relationships: Chassis, FC Adapter

HPCoolingFan:   Attributes: Name, Type, Hot Plug, Location, Present, Redundant:   Relationships: Chassis

HPArrayController:   Attributes: Model, Firmware Revision, Slot, Product Revision,
    Partner Slot, Serial Number, Daughter Board Type, HW Location,
    Number of Buses, Rebuild Priority, Expand Priority, Internal Ports,
    External Ports, Write Cache, Partner Serial Number, ROM Revision,
    Encryption:   Relationships: Chassis, Logical Drive, Physical Drive

HPLogicalDrive:   Attributes: Redundant, Capacity, Stripe Size:   Relationships: Chassis, RAID Controller

HPManagementController:   Attributes: Firmware Version, Firmware Date, ipv4 Address, Active
    License Type, Model, Serial Number, Security Override Switch, url:   Relationships: Chassis

HPMemory:   Attributes: Module Number, Cpu Number, Frequency, Size, Type,
    Technology:   Relationships: Chassis

HPNetworkInterface:   Attributes: AutoSense, Capabilities, Description, Full Duplex, Link
    Technology, MTU, Max Speed, Name, Port Number, Port Type, Speed:   Relationships: Chassis

HPNetworkInterfaceController:   Attributes: MAC Address, ID, Type, IP Address, Description:   Relationships: Chassis

HPPCIDevice:   Attributes: Physical Slot, Board Name, Slot Type, Slot Width:   Relationships: Chassis

HPPhysicalDrive:   Attributes: Capacity, Firmware, Model, Speed, Location,
    Manufacturer, productId, Serial Number:   Relationships: Chassis, RAID Controller

HPPowerSubsystem:   Attributes: Part Number, Serial Number, Max Output, Present,
    sparePartNumber:   Relationships: Enclosure

HPServerPowerSupply:   Attributes: Part Number, Serial Number, Max Output, Redundant,
    Present, sparePartNumber:   Relationships: Chassis

HPProcessor:   Attributes: L1, L2, L3, Coprocessor Count, Coprocessor Speed,
    Coprocessor Type, Cores, HyperThread, Model, Socket, Speed,
    Stepping, Thread Count:   Relationships: Chassis

HPSystemBoard:   Attributes: Product Name, ROM Version, Serial Number, TPM Module:   Relationships: Chassis

HPTemperature:   Attributes: Location, Threshold, Threshold Type:   Relationships: Chassis

### [Monitoring](#contents)

The following metrics will be collected every 5 minutes by default. The
average statistic is collected, and the graphed value is per second for
anything that resembles a rate.

HPFibreChannelAdapter:   Metrics (WBEM):

HPFibreChannelPort:   Metrics (SNMP): cpqFcaHostCntlrCondition, cpqFcaHostCntlrStatus:   Metrics (WBEM): FramesTooLong, EncodingDisparityErrors,
    RXBroadcastFrames, ErrorFrames, MulticastFramesTransmitted,
    LossOfSyncCounter, LinkFailures, LinkResetsReceived, BytesReceived,
    DumpedFrames, FramesTooShort, CRCErrors, PacketsReceived,
    PacketsTransmitted, LossOfSignalCounter, TXBroadcastFrames,
    DelimiterErrors, LinkResetsTransmitted,
    PrimitiveSeqProtocolErrCount, BytesTransmitted, AddressErrors,
    MulticastFramesReceived

HPChassis:   Metrics (SNMP): status:   Metrics (ILO): status:   Metrics (WBEM): status

HPCoolingFan:   Metrics (SNMP): status, speed:   Metrics (ILO): status, speed:   Metrics (WBEM): status, speed

HPDeviceBay:   Metrics (SNMP): status, cpqRackServerBladeWattageAvg,
    cpqRackServerBladePOSTStatus, cpqRackServerBladePowered, condition

HPEnclosure:   Metrics (SNMP): status

HPEnclosureCoolingFan:   Metrics (SNMP): status

HPArrayController:   Metrics (SNMP): cpqDaAccelBattery, cpqDaCntlrPerfCpuPercentBusy,
    cpqDaAccelWriteErrs, cpqDaCntlrBoardStatus, cpqDaAccelBadData,
    cpqDaCntlrBoardCondition, cpqDaAccelStatus, cpqDaAccelErrCode,
    cpqDaCntlrPerfAvgLatency, cpqDaAccelReadErrs, cpqDaCntlrCondition,
    cpqDaAccelCondition, cpqDaCntlrPerfCommandCount,
    cpqDaCntlrPartnerBoardStatus:   Metrics (ILO): cpqDaAccelBattery, cpqDaCntlrCondition,
    cpqDaCntlrBoardStatus:   Metrics (WBEM): cpqDaAccelBattery, CacheReadPercent,
    cpqDaAccelStatus, CacheParityReadErrors, CacheModuleTemperature,
    ControllerTemperature, CacheParityWriteErrors, cpqDaCntlrCondition,
    CacheWritePercent

HPLogicalDrive:   Metrics (SNMP): status, sectorsRead, condition, driveWrite,
    driveRead, sectorsWrite:   Metrics (ILO): condition:   Metrics (WBEM): status

HPManagementController:   Metrics (SNMP): status, cpqSm2CntlrBatteryStatus, interfaceStatus,
    cpqSm2CntlrPendingAlerts, cpqSm2NicCondition,
    cpqSm2CntlrVideoStatus, cpqSm2CntlrAlertStatus,
    cpqSm2CntlrKeyboardCableStatus, cpqSm2CntlrRemoteSessionStatus:   Metrics (ILO): status:   Metrics (WBEM): status

HPMemory:   Metrics (SNMP): status, condition:   Metrics (ILO): status:   Metrics (WBEM): status

HPNetworkInterface:   Metrics (WBEM): status, BytesReceived, PacketsReceived,
    PacketsTransmitted, InternalMACReceiveErrors,
    InternalMACTransmitErrors, BytesTransmitted

HPNetworkInterfaceController:   Metrics (ILO): status

HPOnboardAdmin:   Metrics (SNMP): status

HPPhysicalDrive:   Metrics (SNMP): cpqDaPhyDrvHardWriteErrs, cpqDaPhyDrvDrqTimeouts,
    cpqDaPhyDrvHardwareErrs, cpqDaPhyDrvWrites,
    cpqDaPhyDrvOtherTimeouts, cpqDaPhyDrvFormatErrs,
    cpqDaPhyDrvBadTargetErrs, cpqDaPhyDrvCondition,
    cpqDaPhyDrvMediaErrs, cpqDaPhyDrvReads, status,
    cpqDaPhyDrvHardReadErrs, cpqDaPhyDrvNotReadyErrs:   Metrics (ILO): status:   Metrics (WBEM): MediaFailures, ReadOperations, HardwareErrors,
    SectorsWritten, SectorsRead, OtherTimeOuts, BadTargetErrors,
    WriteOperations, status, NotReadyErrors, HardReadErrors,
    DRQTimeOuts, FormatErrors, HardWriteErrors

HPPowerSubsystem:   Metrics (SNMP): status, currentPowerSupply, condition

HPServerPowerSupply:   Metrics (SNMP): status, currentPowerSupply, condition:   Metrics (ILO): status

HPProcessor:   Metrics (SNMP): status:   Metrics (ILO): status:   Metrics (WBEM): status

HPSystemBoard:   Metrics (SNMP): hoursInService

HPTemperature:   Metrics (SNMP): status, currentReading:   Metrics (ILO): status, currentReading:   Metrics (WBEM): status, currentReading

HPTemperatureSensor:   Metrics (SNMP): status, currentReading

### [Event Management](#contents)

Event managment is handled both actively and passively. Passively, this
takes the form of SNMP traps, translations and correlations for which
516 notifications defined in the various HP/Compaq MIBs are included in
the form of Event class instances with transforms.

Active Event managment revolves around the tracking of the numeric state
indicators defined variously according to SNMP, ILO, or WBEM and mapped
to corresponding Zenoss event severities.

Enclosure:   Clear Event (snmp): status is Other or OK:   Clear Event (esx): status is Unknown or OK:   Info Event (snmp): status is Disabled:   Warning Event (snmp): status is Degraded:   Warning Event (esx): status is Degraded or Minor Failure or Error:   Critical Event (snmp): status is Failed:   Critical Event (esx): status is Major Failure or Critical Failure or
    Non-recoverable Error

Device Bay:   Clear Event (snmp): status is Other or OK:   Clear Event (snmp): cpqRackServerBladePOSTStatus is Other or Started
    or Completed:   Clear Event (snmp): condition is Other or True:   Warning Event (snmp): status is Degraded:   Warning Event (snmp): cpqRackServerBladePOSTStatus is Failed:   Warning Event (snmp): condition is False or Power Staged Off or
    Reboot:   Critical Event (snmp): status is Failed

Cooling Fan (Enclosure):   Clear Event (snmp): status is Other or OK:   Clear Event (esx): status is Unknown or OK:   Info Event (snmp): status is Disabled:   Warning Event (snmp): status is Degraded:   Warning Event (esx): status is Degraded or Minor Failure or Error:   Critical Event (snmp): status is Failed:   Critical Event (esx): status is Major Failure or Critical Failure or
    Non-recoverable Error

Temp Sensor (Enclosure):   Clear Event (snmp): status is Other or OK:   Warning Event (snmp): status is Degraded:   Critical Event (snmp): status is Failed

Interconnect Bay:   Clear Event (snmp): status is Other or OK:   Clear Event (esx): status is Unknown or OK:   Info Event (snmp): status is Disabled:   Warning Event (snmp): status is Degraded:   Warning Event (esx): status is Degraded or Minor Failure or Error:   Critical Event (snmp): status is Failed:   Critical Event (esx): status is Major Failure or Critical Failure or
    Non-recoverable Error

Chassis:   Clear Event (snmp): status is Other or OK:   Clear Event (esx): status is Unknown or OK:   Info Event (snmp): status is Disabled:   Warning Event (snmp): status is Degraded:   Warning Event (esx): status is Degraded or Minor Failure or Error:   Critical Event (snmp): status is Failed:   Critical Event (esx): status is Major Failure or Critical Failure or
    Non-recoverable Error

Cooling Fan:   Clear Event (snmp): status is Other or OK:   Clear Event (esx): status is OK:   Clear Event (snmp): speed is Other or Normal:   Clear Event (esx): speed is OK:   Warning Event (snmp): status is Degraded:   Warning Event (esx): status is Degraded:   Warning Event (snmp): speed is High:   Warning Event (esx): speed is Degraded:   Critical Event (snmp): status is Failed:   Critical Event (esx): status is Major Failure:   Critical Event (esx): speed is Major Failure

FC Adapter:   Clear Event (snmp): status is Other or OK:   Clear Event (esx): status is Unknown or OK:   Info Event (snmp): status is Disabled:   Warning Event (snmp): status is Degraded:   Warning Event (esx): status is Degraded or Minor Failure or Error:   Critical Event (snmp): status is Failed:   Critical Event (esx): status is Major Failure or Critical Failure or
    Non-recoverable Error

FC Port:   Clear Event (snmp): cpqFcaHostCntlrCondition is Other or OK:   Clear Event (snmp): cpqFcaHostCntlrStatus is Other or OK:   Debug Event (snmp): cpqFcaHostCntlrCondition is Not Connected:   Debug Event (snmp): cpqFcaHostCntlrStatus is Not Connected:   Warning Event (snmp): cpqFcaHostCntlrCondition is Shut Down or Loop
    Degraded:   Warning Event (snmp): cpqFcaHostCntlrStatus is Degraded or Loop
    Degraded:   Error Event (snmp): cpqFcaHostCntlrCondition is Loop Failed:   Error Event (snmp): cpqFcaHostCntlrStatus is Loop Failed:   Critical Event (snmp): cpqFcaHostCntlrCondition is Failed:   Critical Event (snmp): cpqFcaHostCntlrStatus is Failed

RAID Controller:   Clear Event (snmp): cpqDaAccelBattery is Other or OK:   Clear Event (snmp): cpqDaCntlrBoardStatus is Other or OK or Disabled:   Clear Event (snmp): cpqDaAccelBadData is Other or None:   Clear Event (snmp): cpqDaCntlrBoardCondition is Other or OK:   Clear Event (snmp): cpqDaAccelStatus is Other or Invalid or Enabled:   Clear Event (ilo): cpqDaCntlrCondition is Other or OK:   Clear Event (snmp): cpqDaCntlrCondition is Other or OK:   Clear Event (snmp): cpqDaAccelCondition is Other or OK:   Clear Event (snmp): cpqDaCntlrPartnerBoardStatus is Other or OK or
    Disabled:   Debug Event (snmp): cpqDaAccelBattery is Missing:   Debug Event (snmp): cpqDaAccelStatus is Not Attached:   Debug Event (ilo): cpqDaCntlrCondition is Not Installed:   Info Event (snmp): cpqDaAccelBattery is Recharging:   Warning Event (snmp): cpqDaAccelBattery is Degraded:   Warning Event (snmp): cpqDaCntlrBoardStatus is Cable Fault or Failed:   Warning Event (snmp): cpqDaAccelBadData is Possible:   Warning Event (snmp): cpqDaCntlrBoardCondition is Degraded:   Warning Event (snmp): cpqDaAccelStatus is Temporarily Disabled or
    Degraded or Read Cache Unmapped:   Warning Event (ilo): cpqDaCntlrCondition is Degraded or Degraded:   Warning Event (snmp): cpqDaCntlrCondition is Degraded:   Warning Event (snmp): cpqDaAccelCondition is Degraded:   Error Event (snmp): cpqDaAccelBattery is Failed or Capacitor Failed:   Error Event (snmp): cpqDaAccelStatus is Permanently Disabled:   Error Event (ilo): cpqDaCntlrCondition is Major Warning:   Critical Event (snmp): cpqDaCntlrBoardStatus is Failed:   Critical Event (snmp): cpqDaCntlrBoardCondition is Failed:   Critical Event (snmp): cpqDaAccelStatus is Critical Failure:   Critical Event (ilo): cpqDaCntlrCondition is Failed:   Critical Event (snmp): cpqDaCntlrCondition is Failed:   Critical Event (snmp): cpqDaAccelCondition is Failed:   Critical Event (snmp): cpqDaCntlrPartnerBoardStatus is Failed

Logical Drive:   Clear Event (ilo): status is Other or OK:   Clear Event (snmp): status is Other or OK:   Clear Event (esx): status is Unknown or OK:   Clear Event (ilo): condition is OK:   Clear Event (snmp): condition is Other or OK:   Warning Event (ilo): status is Unconfigured or Recovering or Ready
    For Rebuild or Rebuilding or Wrong Drive or Bad Connect or Over
    heating or Shutdown or Expanding or Not Available or Queued For
    Expansion or Multipath Access Degraded or Erasing or Predictive
    Spare Rebuild Ready or Rapid Parity Init In Progress or Rapid Parity
    Init Pending:   Warning Event (snmp): status is Unconfigured or Recovering or Ready
    For Rebuild or Rebuilding or Wrong Drive or Bad Connect or Over
    heating or Shutdown or Expanding or Not Available or Queued For
    Expansion or Multipath Access Degraded or Erasing or Predictive
    Spare Rebuild Ready or Rapid Parity Init In Progress or Rapid Parity
    Init Pending:   Warning Event (esx): status is Degraded or Minor Failure:   Warning Event (snmp): condition is Degraded:   Critical Event (ilo): status is Failed:   Critical Event (snmp): status is Failed:   Critical Event (esx): status is Major Failure or Critical Failure or
    Non-recoverable Error:   Critical Event (ilo): condition is Failed:   Critical Event (snmp): condition is Failed

Management Controller:   Clear Event (snmp): status is Other or Online:   Clear Event (esx): status is Unknown or OK:   Clear Event (snmp): cpqSm2CntlrBatteryStatus is Other or OK:   Clear Event (snmp): interfaceStatus is Other or OK:   Clear Event (snmp): cpqSm2CntlrPendingAlerts is Other or None:   Clear Event (snmp): cpqSm2CntlrVideoStatus is Other or Enabled:   Clear Event (snmp): cpqSm2CntlrAlertStatus is Other or Enabled:   Clear Event (snmp): cpqSm2CntlrRemoteSessionStatus is Other or
    Inactive:   Clear Event (snmp): cpqSm2CntlrKeyboardCableStatus is Other or
    Connected or Disconnected:   Debug Event (snmp): cpqSm2CntlrVideoStatus is Disabled:   Debug Event (snmp): cpqSm2CntlrAlertStatus is Disabled:   Debug Event (snmp): cpqSm2CntlrRemoteSessionStatus is Active:   Warning Event (snmp): status is No Data or Offline:   Warning Event (esx): status is Degraded:   Warning Event (snmp): cpqSm2CntlrBatteryStatus is Disconnected:   Warning Event (snmp): interfaceStatus is Not Responding:   Warning Event (snmp): cpqSm2CntlrPendingAlerts is Pending or
    Remaining:   Critical Event (esx): status is Major failure:   Critical Event (snmp): cpqSm2CntlrBatteryStatus is Failed

Memory Slot:   Clear Event (ilo): status is Other or OK or Not Present or Good:   Clear Event (snmp): status is Other or Not Present or In Use or
    Spare:   Clear Event (esx): status is Unknown or OK or Degraded:   Clear Event (snmp): condition is Other or OK:   Info Event (snmp): status is Present or Added or Upgraded or
    Unmatched or Partial Use:   Warning Event (ilo): status is Degraded or Degraded Module Index
    Unknown:   Warning Event (snmp): status is Missing or Not Supported or Bad
    Configuration:   Warning Event (snmp): condition is Degraded or Degraded Module Index
    Unknown:   Error Event (snmp): status is Degraded

Network Interface:   Clear Event (esx): status is OK or Degraded or MajorFailure

NIC:   Clear Event (ilo): status is Other or OK:   Clear Event (snmp): status is Other or OK:   Clear Event (esx): status is Unknown or OK:   Debug Event (ilo): status is Disabled:   Debug Event (snmp): status is Unknown:   Warning Event (ilo): status is Link Down:   Warning Event (snmp): status is Link Down:   Warning Event (esx): status is Degraded or Minor Failure:   Error Event (esx): status is Major Failure or Non-recoverable Error:   Critical Event (esx): status is Critical Failure

Onboard Administrator:   Clear Event (snmp): status is Other or OK:   Clear Event (esx): status is Unknown or OK:   Info Event (snmp): status is Disabled:   Warning Event (snmp): status is Degraded:   Warning Event (esx): status is Degraded or Minor Failure or Error:   Critical Event (snmp): status is Failed:   Critical Event (esx): status is Major Failure or Critical Failure or
    Non-recoverable Error

PCI Device:   Clear Event (snmp): status is Other or OK:   Clear Event (esx): status is Unknown or OK:   Info Event (snmp): status is Disabled:   Warning Event (snmp): status is Degraded:   Warning Event (esx): status is Degraded or Minor Failure or Error:   Critical Event (snmp): status is Failed:   Critical Event (esx): status is Major Failure or Critical Failure or
    Non-recoverable Error

Physical Drive:   Clear Event (ilo): status is Other or OK:   Clear Event (snmp): status is Other or OK:   Clear Event (esx): status is Unknown or OK:   Clear Event (snmp): condition is Other or OK:   Warning Event (ilo): status is Predictive Failure or Erasing or
    Erase Done or Erase Queued or SSD Wear Out or Degraded (Not
    Authenticated):   Warning Event (snmp): status is Predictive Failure or Erasing or
    Erase Done or Erase Queued or SSD Wear Out or Degraded (Not
    Authenticated):   Warning Event (esx): status is Degraded or Minor Failure:   Warning Event (snmp): condition is Degraded:   Critical Event (ilo): status is Failed:   Critical Event (snmp): status is Failed:   Critical Event (esx): status is Major Failure or Critical Failure or
    Non-recoverable Error:   Critical Event (snmp): condition is Failed

Power Supply:   Clear Event (snmp): status is Other or OK:   Clear Event (snmp): condition is No Error:   Warning Event (snmp): status is Degraded:   Critical Event (snmp): status is Failed:   Critical Event (snmp): condition is General Failure or Bist Failure
    or Fan Failure or Temp Failure or Inter Lock Open or Eprom Failed or
    Vref Failed or Dac Failed or Ram Test Failed or Voltage Channel
    Failed or Orring Diode Failed or Brown Out or Give Up On Startup or
    Nvram Invalid or Calibration Table Invalid

Power Supply:   Clear Event (snmp): status is Other or OK:   Clear Event (snmp): condition is No Error:   Warning Event (snmp): status is Degraded:   Critical Event (snmp): status is Failed:   Critical Event (snmp): condition is General Failure or Bist Failure
    or Fan Failure or Temp Failure or Inter Lock Open or Eprom Failed or
    Vref Failed or Dac Failed or Ram Test Failed or Voltage Channel
    Failed or Orring Diode Failed or Brown Out or Give Up On Startup or
    Nvram Invalid or Calibration Table Invalid

Processor:   Clear Event (ilo): status is OK:   Clear Event (snmp): status is OK:   Clear Event (esx): status is OK:   Debug Event (ilo): status is Unknown:   Debug Event (snmp): status is Unknown:   Debug Event (esx): status is Unknown:   Info Event (ilo): status is Disabled:   Info Event (snmp): status is Disabled:   Warning Event (ilo): status is Degraded:   Warning Event (snmp): status is Degraded:   Warning Event (esx): status is Stopped:   Critical Event (ilo): status is Failed:   Critical Event (snmp): status is Failed:   Critical Event (esx): status is Predictive Failure or Error

System Board:   Clear Event (snmp): status is Other or OK:   Clear Event (esx): status is Unknown or OK:   Info Event (snmp): status is Disabled:   Warning Event (snmp): status is Degraded:   Warning Event (esx): status is Degraded or Minor Failure or Error:   Critical Event (snmp): status is Failed:   Critical Event (esx): status is Major Failure or Critical Failure or
    Non-recoverable Error

Temp Sensor:   Clear Event (snmp): status is Other or OK or Not Installed:   Warning Event (snmp): status is Degraded:   Critical Event (snmp): status is Failed

### [Service Impact](#contents)

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact and root cause analysis capabilities for
services running on HP Proliant. The service impact relationships shown
in the diagram and described below are automatically added. These will
be included in any services that contain one or more of the explicitly
mentioned components.

Service Impact Relationships:   Device impacts related Enclosure, Chassis:   Enclosure impacts related Device Bay, Cooling Fan, Interconnect Bay,
    Power Subsystem, Temperature Sensor:   Chassis impacts related Processor, Memory, System Board, Temperature
    Sensor, Cooling Fan, Power Supply, Management Controller, Network
    Interface, Onboard Administrator, PCI Device, Array Controller,
    Physical Drive, Logical Drive, Fibre Channel Adapter, Fibre Channel
    Controller:   Fibre Channel Adapter impacts related Fibre Channel Port:   Array Controller impacts related Logical Drive, Physical Drive:   Device Bay impacts related Chassis:   Managment Controller impacts related Device (iLO)

## [Data Collection](#contents)

The HP Proliant ZenPack uses several methods to collect both model and
performance data depending on the device types, which fall into 3
categories:

### [SNMP](#contents)

Onboard Administrator is HP's solution for hardware management and
monitoring. It provides a SNMP interface that Zenoss uses to monitor
both HP chassis and blade hardware as well as certain OS components with
the OA agent installed and configured. SNMP access can also be
configured for use with the iLO management interface (via the managment
GUI) or with a bare metal install of Linux or Windows by installing HP
SIM and related software (including its SNMP subagent)

### [ILO](#contents)

Data from ILO devices is provided by a HTTPS interface listening on port
443. The zILOUserName, zILOPassword, zILOUseSSL, and zILOPort
zProperties control access to ILO devices. The ILO interface accepts and
returns XML-formatted query strings, and this ZenPack features a custom
api definining these queries and their output formatting.

### [WBEM](#contents)

WBEM support is required for montitoring ESXi on HP Proliant hardware.
The zWBEMUsername, zWBEMPassword, zWBEMPort, and zWBEMUseSSL zProperties
control access to HP ESXi devices. Data collection relies on the WBEM
ZenPack, and also uses a HTTP-based protocol (WBEM). HP provides
custom-built ESXi ISOs that provide the HP WBEM software to the base
ESXi image.

Endpoint configuration is beyond the scope of this document, but online
resources are available at
<http://h10032.www1.hp.com/ctg/Manual/c04341228>

## [Usage](#contents)

### [Adding SNMP Onboard Administrator Device (Enclosure)](#contents)

Use the following steps to start monitoring the Onboard Administrator
using the Zenoss web interface.

1.  Navigate to the Infrastructure page.
2.  Navigate to organizer *Devices/Server/HP/OnboardAdministrator*.
3.  Choose *Add a Single Device* from the add button
4.  Fill out the form:
    -   *Name* can be anything you want.
    -   *Hostname or IP* must be resolvable and accessible from the
        collector server chosen in the *Collector* field.
5.  Click *ADD*.

### [Adding Linux SNMP or Windows (SNMP) Blade/Rack Device](#contents)

Use the following steps to start monitoring Linux HP Proliant device
using the Zenoss web interface.

1.  Navigate to the Infrastructure page.
2.  Navigate to organizer *Devices/Server/HP/Proliant*.
3.  Choose *Add a Single Device* from the add button
4.  Fill out the form:
    -   *Name* can be anything you want.
    -   *Hostname or IP* must be resolvable and accessible from the
        collector server chosen in the *Collector* field.
5.  Click *ADD*.

### [Adding ILO Device](#contents)

Use the following steps to start monitoring a HP ILO device using the
Zenoss web interface.

1.  Navigate to the Infrastructure page.
2.  Navigate to organizer *Devices/Server/HP/ILO*.
3.  Choose *Add a Single Device* from the add button
4.  Fill out the form:
    -   *Name* can be anything you want.
    -   *Hostname or IP* must be resolvable and accessible from the
        collector server chosen in the *Collector* field.
5.  Click *ADD*.

### [Adding ILO Device (SNMP)](#contents)

Use the following steps to start monitoring a HP ILO device using the
Zenoss web interface.

1.  Navigate to the Infrastructure page.
2.  Navigate to organizer *Devices/Server/HP/ILO/SNMP*.
3.  Choose *Add a Single Device* from the add button
4.  Fill out the form:
    -   *Name* can be anything you want.
    -   *Hostname or IP* must be resolvable and accessible from the
        collector server chosen in the *Collector* field.
5.  Click *ADD*.

### [Adding ESXi Device](#contents)

Use the following steps to start monitoring a HP ILO device using the
Zenoss web interface.

1.  Navigate to the Infrastructure page.
2.  Navigate to organizer *Devices/Server/VMware/ESXi/HP*.
3.  Choose *Add a Single Device* from the add button
4.  Fill out the form:
    -   *Name* can be anything you want.
    -   *Hostname or IP* must be resolvable and accessible from the
        collector server chosen in the *Collector* field.
5.  Click *ADD*.

### [Combining HP Proliant SNMP monitoring with existing Device Classes](#contents)

Use the following steps to start monitoring a HP ILO device using the
Zenoss web interface.

1.  Navigate to the Infrastructure page.
2.  Navigate to the desired organizer containing SNMP-monitorable
    devices, such as *Devices/Server/Linux*.
3.  Choose *Details* link above the Devices column
4.  Select the *Modeler Plugins* menu item
5.  Add the *HP.snmp.HPSNMPModeler* plugin to the list of Selected
    plugins
6.  Click *Save*
7.  Devices in this class should now model and monitor components as
    they are found

### [Command Line Tools](#contents)

Several scripts are included for use with troubleshooting or sample data
collection. These scripts reside in the

$ZENPACK/ZenPacks/zenoss/HP/Proliant/utilities

directory and calling --help will display usage information for each.
:   collect-samples-ilo.sh (performs several queries against ILO devices
    and saves output to individual files):   collect-samples-wbem.sh (performs several queries against WBEM
    devices and saves output to individual files):   hp-ilo-samples.py (execute given ILO command against remote target
    and save output):   hp-wbem-dump.py (output list of valid WBEM classnames from ESXi
    target):   hp-wbem-query.py (execute WBEM query against remote ESXi target):   hp-wbem-smx-instances (perform exhaustive iteration of WBEM classes
    on remote ESXi target)

## [Installed Items](#contents)

Installing this ZenPack will add the following items to your Zenoss
system.

Device Classes:   /Server/HP/OnboardAdministrator *Enclosure monitoring*
:   /Server/HP/ILO: *iLO device monitoring with iLO*
:   /Server/HP/ILO/SNMP: *iLO device monitoring with SNMP*
:   /Server/VMware/ESXi/HP: *ESXi monitoring with WBEM*
:   /Server/HP/Proliant: *SNMP monitoring with HP MIBs*

Configuration Properties:   zILOPort:   zILOUseSSL:   zILOUserName:   zILOPassword:   zILOCollectSamples

Modeler Plugins:   HP.snmp.HPEnclosureModeler:   HP.snmp.HPSNMPModeler:   HP.ilo.HPILO3Modeler:   HP.wbem.HPWBEMPlugin

Datasource Types:   HP ILO Datasource:   HP WBEM Datasource:   SNMP Datasource (SNMP)

Monitoring Templates:   HPArrayControllerILO:   HPArrayControllerSNMP:   HPArrayControllerWBEM:   HPChassisILO:   HPChassisSNMP:   HPChassisWBEM:   HPCoolingFanILO:   HPCoolingFanSNMP:   HPCoolingFanWBEM:   HPDeviceBaySNMP:   HPDeviceSNMP:   HPEnclosureCoolingFanSNMP:   HPEnclosureSNMP:   HPFibreChannelAdapterWBEM:   HPFibreChannelPortSNMP:   HPFibreChannelPortWBEM:   HPLogicalDriveILO:   HPLogicalDriveSNMP:   HPLogicalDriveWBEM:   HPManagementControllerILO:   HPManagementControllerSNMP:   HPManagementControllerWBEM:   HPMemoryILO:   HPMemorySNMP:   HPMemoryWBEM:   HPNetworkInterfaceControllerILO:   HPNetworkInterfaceWBEM:   HPOnboardAdminSNMP:   HPPhysicalDriveILO:   HPPhysicalDriveSNMP:   HPPhysicalDriveWBEM:   HPPowerSubsystemSNMP:   HPProcessorILO:   HPProcessorSNMP:   HPProcessorWBEM:   HPServerPowerSupplyILO:   HPServerPowerSupplySNMP:   HPSystemBoardSNMP:   HPTemperatureILO:   HPTemperatureSNMP:   HPTemperatureSensorSNMP:   HPTemperatureWBEM

Component Types:   Enclosure (HPEnclosure):   Chassis (HPChassis):   Cooling Fan (HPCoolingFan):   Device Bay (HPDeviceBay):   Cooling Fan (HPEnclosureCoolingFan):   Interconnect Bay (HPInterconnectBay):   RAID Controller (HPArrayController):   Logical Drive (HPLogicalDrive):   Management Controller (HPManagementController):   Memory Slot (HPMemory):   Network Interface (HPNetworkInterface):   NIC (HPNetworkInterfaceController):   Onboard Administrator (HPOnboardAdmin):   PCI Device (HPPCIDevice):   Physical Drive (HPPhysicalDrive):   Power Supply (HPPowerSubsystem):   Power Supply (HPServerPowerSupply):   Processor (HPProcessor):   System Board (HPSystemBoard):   Temp Sensor (HPTemperature):   Temp Sensor (HPTemperatureSensor):   FC Adapter (HPFibreChannelAdapter):   FC Port (HPFibreChannelPort)

Event Classes:   /Status/HP:   /Perf/HP

## [Required Daemons](#contents)

Modeler:

:   zenmodeler

Performance Collector:
:   zenpython:   zenperfsnmp

## [Upgrade](#contents)

The HP Proliant Zenpack can be upgraded. To upgrade the ZenPack, install
the latest version over the existing one. There is no action for the
user to migrate the data. The performance data and events of old ZenPack
are retained as per the retain policy settings.

## [Limitations](#contents)

## [Known Issues](#contents)

### [Known Issue when monitoring systems with Failover Onboard Administrators](#contents)

In order to fully support monitoring a system with multiple onboard
administrators the "enclosure ip mode" option must be enabled and the
enclosure must be given a static ip address that is shared between the
two onboard administrators. Failure to do so may cause monitoring to
stop when the active onboard administrator goes offline.

### [Known Issue upgrading from 1.0 to 3.0](#contents)

When upgrading from 1.0 to 3.0 you may see an issue related to catalogs.
If you installed the zenpack from the ui the ui may complain that the
zenpack install failed. Install the zenpack from the command line as a
workaround. The observe messages similar to "WARNING zen.catalogservice:
Detected catalog inconsistency - to repair, run: 'python
/opt/zenoss/ZenPacks/ZenPacks.zenoss.CatalogService-1.0.19.10-py2.7.egg/ZenPacks/zenoss/CatalogService/sync_rids.py'"
to finish the installation of this zenpack run the script as it
suggests. then restart the zenoss instances.

### [Known issue regarding ilo unknown or N/A values](#contents)

Ilo device modelling reuses the original snmp components of this
zenpack. Because the ilo does not return exactly the same results as is
available via snmp monitoring, there will be cases where some fields are
always set to N/A or Unknown. This is a known issue and is not currently
considered a defect.

### [Known issue regarding ilo monitoring](#contents)

The servername variable needs to be set inside the ILO for this zenpack
to work properly with ILO hardware. - For the ILO 4, please go into the
ILO GUI under Administration -&gt; Access Settings -&gt; Under Access
Options there is "Server Name" and update the name for the ILO server.

### [Known issue when removing ZenPack](#contents)

Since this ZenPack depends on the PythonCollector ZenPack for some of
its capabilities, the zenpython collector daemon should be stopped
manually prior to uninstallation of this ZenPack in order to avoid a
traceback error. The zenpython daemon can be restared again once
uninstallation is complete.

## [Changes](#contents)

3.3.5

-   Make zenpack compatible with twisted 19.10.0 (ZPS-6981)
-   Tested with
    Zenoss Resource Manager 6.4.1, Zenoss Cloud and Service Impact
    5.5.1

3.3.4

-   Add log
    message to notify when "SERVER NAME" is blank in the iLO
    (ZPS-6128)
-   Tested with
    Zenoss Resource Manager 6.4.1, Zenoss Cloud and Service Impact
    5.5.1

3.3.3

-   Updated icons with dark-theme
    compatible versions
-   ILO modeler timeout should
    follow zCollectorClientTimeout
-   Fix exceptions in impact
    relationship providers
-   Overhaul impact
    relationships
-   Hide credentials from logging
    (ZPS-4338)
-   Add support for ILO Gen 7
    physical drives (ZPS-5274)
-   Fix WBEM component metric
    duplication issue (ZPS-6132)

3.3.2:   Fix Error modeling Generation 9 iLO hardware when memory/swap info
    is missing (ZPS-3101):   Ensure all NICs are discovered and monitored (ZPS-3645):   Correct unrecognized "Good, In Use" status (ZPS-3737):   Modeling should succeed when drive enclosure is absent (ZPS-3306):   Update Physical Disk possible status values (ZPS-2946)

    Tested with Zenoss 5.3.3, Zenoss 6.2.0, and Zenoss Cloud

3.3.1:   Updated unit tests for build platform compatability (ZPS-29150,
    ZEN-28507)

3.3.0:   Ported to ZenPackLib 2.0:   Extend support to G9 and G10 platforms (ZPS-2086):   Add support for Fibre Channel Adapter and Port monitoring (ZPS-2086):   Added scripts for debug and data collection of iLO and WBEM clients:   Revised monitoring template organziation and protocol dependency:   Added new HP WBEM Datasource and revised all WBEM templates:   Added multiple new metrics for WBEM monitoring:   New icons added for device and all component classes:   WBEM modeling and performance data collection completely revised:   Additional mappings for SNMP traps (ZPS-679):   Fix bidirectional links on Device Status Page (ZPS-745, ZPS-2280):   Fix various SNMP modeling tracebacks (ZPS-1621):   Fix various issues during upgrade (ZPS-2088, ZPS-2256, ZPS-2257):   Fix various ILO modeling issues (ZPS-)

3.2.2:   Fixed ILO and WBEM modeler plugins to better handle empty results:   Updated list of recognized XML status strings

3.2.1:   Updated ILO Protocol handler to address SSL certificate validation
    issue while preserving HTTP/1.1 compliance:   Updated XML parser to better handle invalid XML output:   Fix bad threshold datasource reference in HPArrayController template:   Corrected type of cycletime parameter:   Ensure all SNMP templates available to /Devices/Server/HP/ILO/SMNP

3.2.0:   Added "HP Chassis List" and "HP Device Bay List" reports (ported
    from HPBladeChassis community ZP):   Update Impact documentation (ZEN-25324):   Added "zILOCollectSamples" zProperty (raw modeler output storage):   Updated zProperties (removed zProperty zILOSSLPort, replace with
    zILOUsesSSL and zILOPort):   Adjust component labels and titles for DynamicView (ZEN-25248):   Add ResetClassRelations migrate script (ZEN-25281):   Sensible thresholds for Temperature graphs (ZEN-25260):   More informative event logging (ZEN-24270):   Ensure that ILODatasource, HPStatusThreshold, and GUI use shared
    reference data:   Updated graph datapoints and templates (ZEN-24886):   Improved datasource/datapoint access methdos for status string
    retrieval (ZEN-24277):   Fix traceback during WBEM modeling (ZEN-24786):   updated and new unit testing to handle ILO datasource/modeler
    testing (ZEN-24810):   Revised and simplified all string-to-integer status mapping code:   Added new ILOProtocolHandler ILO client (ZEN-25277):   Added new ILOXMLParser for shared access to ILO output:   Added cross-reference functions to HPDevice and HPChassis (get_ilo,
    get_cpus, get_mem):   Revised shared component attributes for consistency:   Remove/migrate code from utils.py and ErrorHandler.py:   Added ManagedObject base to contine shared component code:   deprecate ILO2 support (ZEN-22388):   Rewrite of all modeler plugins:   Added HPPluginBase, HPSnmpPlugin to contain shared plugin code:   Prevent premature data collection termination (ZEN-24277):   Add support for RAID controller monitoring via SNMP and ILO
    (ZEN-24211, ZEN-23388):   Fix HPStatusThreshold issue causing data collection to stop
    (ZEN-23040):   Improved handling of components with blank id (ZEN-22872, ZEN-22851,
    ZEN-21680)

3.1.1:   Updated zenpacklib.py to address modeler timeouts from
    attribute-indexed components

3.1.0:   Numerous enhancements and bugfixes

3.0.2:   Fixes ZEN-18151. HP.wbem.HPWBEMPlugin modeling traceback on
    tempStatus()

3.0.1:   Standardized commonly used code for converting RRD status to
    formatted string:   Standardized most component properties to those common between
    collection methods (some still outstanding):   Standardized common datasource/datapoint names throughout templates:   Simplified customized classes to reduce duplication of function:   Removed duplicate property definitions with similar names but
    identical values:   Removed most component properties that should have been performance
    or status datasources:   Standardized unit testing for modeler plugins and class loading:   Folded deviceMap modeler plugins into component modeler plugins,
    removed device map plugins:   Added ZenPack class to remove all RRD templates upon ZP uninstall:   Changed Fan Speed to display status string (only ILO shows actual
    speed):   SNMP modeler plugins are now appropriate for use wherever SNMP is
    supported:   Deprecated HPOSHypervisor and HPThermalSubsystem components:   Removed COMMAND datasource from HPLogicalDrive (used snmpindex_dct
    instead):   Added ILO datasource queries for HPChassis, HPProcessor,
    HPManagementController, HPNetworkInterfaceController, and updated
    ILODatasource to accommodate:   Added "perfID" to ILO HPTemperature components to correct some
    missing datapoints:   Updated migrate methods to remove all templates before re-adding
    from YAML:   Removed "uptime" metric from HPSystemBoard since it duplicates the
    Device sysUptime datapoint:   Added several status indicators to HPManagementController component
    (SNMP):   Re-based SNMP Device templates on /Server/Linux to ensure
    consistency

3.0.0:   Major rewrite of significant sections of the zenpack to use
    zenpacklib and remove obvious defects.

1.0.0:   Initial release.

## Attachments:

-   [array-controller-graphs-esx.PNG](img/zenpack-array-controller-graphs-esx.png)
-   [dynamic-view-chassis.PNG](img/zenpack-dynamic-view-chassis.png)
-   [enclosure-device-status.PNG](img/zenpack-enclosure-device-status.png)
-   [enclosure-onboard-admin.PNG](img/zenpack-enclosure-onboard-admin.png)
-   [esx-device-status.PNG](img/zenpack-esx-device-status.png)
-   [esx-fc-port.PNG](img/zenpack-esx-fc-port.png)
-   [esx-raid-controller.PNG](img/zenpack-esx-raid-controller.png)
-   [esx-temp-sensor.PNG](img/zenpack-esx-temp-sensor.png)
-   [fc-port-component-errors-graph.PNG](img/zenpack-fc-port-component-errors-graph.png)
-   [fc-port-ilo-snmp-status.PNG](img/zenpack-fc-port-ilo-snmp-status.png)
-   [fc-ports-component-graphs.PNG](img/zenpack-fc-ports-component-graphs.png)
-   [fc-ports-details.PNG](img/zenpack-fc-ports-details.png)
-   [fc-ports.PNG](img/zenpack-fc-ports.png)
-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)
-   [ilo-device-status.PNG](img/zenpack-ilo-device-status.png)
-   [impact-graph-small.PNG](img/zenpack-impact-graph-small.png)
-   [impact.png](img/zenpack-impact.png)
-   [model.png](img/zenpack-model.png)
-   [network-iface-stats-esx.PNG](img/zenpack-network-iface-stats-esx.png)
-   [new-icons.PNG](img/zenpack-new-icons.png)
-   [phys-drive-graphs-esx.PNG](img/zenpack-phys-drive-graphs-esx.png)
-   [proliant-server-graph.PNG](img/zenpack-proliant-server-graph.png)
-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)
-   [network-iface-stats-esx.PNG](img/zenpack-network-iface-stats-esx.png)
-   [enclosure-temp-sensor.PNG](img/zenpack-enclosure-temp-sensor.png)
-   [array-controller-graphs-esx.PNG](img/zenpack-array-controller-graphs-esx.png)
-   [dynamic-view-chassis.PNG](img/zenpack-dynamic-view-chassis.png)
-   [enclosure-device-status.PNG](img/zenpack-enclosure-device-status.png)
-   [enclosure-onboard-admin.PNG](img/zenpack-enclosure-onboard-admin.png)
-   [enclosure-temp-sensor.PNG](img/zenpack-enclosure-temp-sensor.png)
-   [esx-fc-port.PNG](img/zenpack-esx-fc-port.png)
-   [esx-raid-controller.PNG](img/zenpack-esx-raid-controller.png)
-   [fc-port-component-errors-graph.PNG](img/zenpack-fc-port-component-errors-graph.png)
-   [fc-port-ilo-snmp-status.PNG](img/zenpack-fc-port-ilo-snmp-status.png)
-   [fc-ports-component-graphs.PNG](img/zenpack-fc-ports-component-graphs.png)
-   [fc-ports-details.PNG](img/zenpack-fc-ports-details.png)
-   [fc-ports.PNG](img/zenpack-fc-ports.png)
-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)
-   [ilo-device-status.PNG](img/zenpack-ilo-device-status.png)
-   [impact-graph-small.PNG](img/zenpack-impact-graph-small.png)
-   [impact.png](img/zenpack-impact.png)
-   [model.png](img/zenpack-model.png)
-   [network-iface-stats-esx.PNG](img/zenpack-network-iface-stats-esx.png)
-   [phys-drive-graphs-esx.PNG](img/zenpack-phys-drive-graphs-esx.png)
-   [proliant-server-graph.PNG](img/zenpack-proliant-server-graph.png)
-   [esx-device-status.PNG](img/zenpack-esx-device-status.png)
-   [new-icons.PNG](img/zenpack-new-icons.png)
-   [array-controller-graphs-esx.PNG](img/zenpack-array-controller-graphs-esx.png)
-   [esx-temp-sensor.PNG](img/zenpack-esx-temp-sensor.png)
-   [fc-ports-details.PNG](img/zenpack-fc-ports-details.png)
-   [fc-ports-component-graphs.PNG](img/zenpack-fc-ports-component-graphs.png)


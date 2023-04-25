# F5 BIG-IP (Commercial)

@lb[](img/zenpack-f5-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.BigIPMonitor

## F5 BIG-IP (Commercial) ZenPack

The F5 BIG-IP network device monitoring feature monitors load balancer
CPU and memory utilization. It also tracks per-instance metrics for each
load-balanced virtual server that is configured.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 2.7.2 - [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2020/09/22:   Tested with Zenoss Resource
    Manager 6.4.1, Zenoss Resource Manager 6.5.0, Zenoss Cloud and
    Service Impact 5.5.2

<!-- -->

Version 2.6.4- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2015/02/04:   Compatible with Zenoss Resource Manager 4.1.x, Zenoss Resource
    Manager 4.2.x

## Background

This ZenPack provides support for monitoring F5 BIG-IP load balancers.
Monitoring is performance using SNMP.

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Initial discovery and periodic remodeling of relevant components.
-   Performance monitoring.
-   Event management.

## Gallery

@lb[](img/zenpack-f5 big ip zenoss monitoring.png){.confluence-embedded-image width="898"}

## Discovery

The following components will be automatically discovered using SNMP.
The components, properties and relationships will be periodically
remodeled to provide automatically up-to-date monitoring when the load
balancer configuration changes.

Load Balancer (Device):   Properties: Hardware Model, OS Version, Total Memory:   Relationships: LTM Virtual Servers, Load Balancer Pools, Load
    Balancer Ports, Network Interfaces, CPUs, Fans, Power Supplies,
    Temperature Sensors

<!-- -->

LTM Virtual Server:   Properties: Display Name, IP Address, Port, Protocol, Enabled,
    Connection Limit, Rate Class, Connection Mirroring, Translate
    Address, Translate Port, Server Type:   Relationships: Load Balancer

<!-- -->

Load Balancer Pool:   Properties: Simple Timeout, IP ToS To Client, IP ToS to Server, Link
    QoS to Client, Link QoS to Server, Dynamic Ratio Sum, Monitor Rule,
    Mode, Slow Ramp Time, Member Count, Action On Service Down, Minimum
    Up Members, Minimum Up Members Enable, Minimum Up Members Action,
    Minimum Active Members, Active Member Count, Disallow NAT, Disallow
    SNAT:   Relationships: Load Balancer, Load Balancer Pool Members

<!-- -->

Load Balancer Pool Member:   Properties: Pool Name, Monitor State, Monitor Status, New Session
    Enable, Session Status, Monitor Rule, Address Type, Address, Port,
    Connection Limit, Ratio, Weight, Priority, Dynamic Ratio:   Relationships: Load Balancer Pool

<!-- -->

Load Balancer Port:   Properties: Flow Control Request State, STP Link, STP Edge, STP Edge
    Active, STP Auto, STP Enable, STP Reset, Status, Combo Port, Prefer
    SFP, Media Max Speed, SFP Media, Physical Master, Media Max Duplex,
    Media Active Speed, Media Active Duplex, MAC Address, MTU, Enabled,
    Learn Mode:   Relationships: Load Balancer

<!-- -->

Network Interfaces (Physical & VLAN):   Properties: Name, IP Addresses, MAC Address, Administrative Status,
    Operational Status, Speed, Duplex, MTU:   Relationships: Load Balancer

<!-- -->

CPU:   Properties: Name, Socket:   Relationships: Load Balancer

<!-- -->

Fan:   Properties: Name, State:   Relationships: Load Balancer

<!-- -->

Power Supply:   Properties: Name, State:   Relationships: Load Balancer

<!-- -->

Temperature Sensor:   Properties: Name:   Relationships: Load Balancer

### Performance Monitoring

The following metrics will be collected every 5 minutes by default. This
can be configured with the *zSnmpCollectionInterval* configuration
property. Additional SNMP values can be collected for any of the
component types listed in the [: Discovery](#)
section.

<dl markdown="1">
<dt markdown="1">
Load Balancer (Device)
</dt>
</dl>

-   CPU Utilization: Busy, Idle, Sleep (*percent*)
-   Memory Utilization: System, Host (*percent*)
-   Connection Pool: Max Size, Current Size (*connections*)
-   Packet Failure Rates: Inbound Errors, Outbound Errors, Dropped, No
    Handler Denied, Non-Syn Deny, License Deny (*packets/sec*)
-   Connection Failure Rates: Connection Limit Exceeded, Connection
    Failed due to Memory Errors (*connections/sec*)
-   HTTP Rates: HTTP Requests, Cookies Generated, Cookies Detected
    (*requests/sec*)
-   Throughput: Inbound Client, Outbound Client, Inbound Server,
    Outbound Server (*bytes/sec*)
-   Connections: Current Client, Max Client, Current Server, Max Server
    (*connections/sec*)
-   Packet Rates: Inbound Client, Outbound Client, Inbound Server,
    Outbound Server (*packets/sec*)
-   Accelerated Connections: Current Client, Max Client, Current Server,
    Max Server, Partially Accelerated (*connections/sec*)
-   Accelerated Throughput: Inbound Client, Outbound Client, Inbound
    Server, Outbound Server (*bytes/sec*))
-   Accelerated Packet Rates: Inbound Client, Outbound Client, Inbound
    Server, Outbound Server (*packets/sec*)

<dl markdown="1">
<dt markdown="1">
LTM Virtual Server
</dt>
</dl>

-   Connections: Client, Client High Water Mark, Client Connections/sec,
    Ephemeral, Ephemeral High Water Mark, Ephemeral Total
    Connections/sec, Hardware Accelerated, Hardware Accelerated High
    Water Mark, Hardware Accelerated Connections/sec, Partially Hardware
    Accelerated (*connections*)
-   Throughput: Client Received, Client Sent, Ephemeral Received,
    Ephemeral Sent, Hardware Accelerated Received, Hardware Accelerated
    Sent (*bits/sec*)
-   Packets: Client Received, Client Sent, Ephemeral Received, Ephemeral
    Sent, Hardware Accelerated Received, Hardware Accelerated Sent
    (*packets/sec*)
-   Connection Duration: Minimum, Maximum, Average (*milliseconds*)
-   Request Rate: Total (*requests/sec*)

<dl markdown="1">
<dt markdown="1">
Load Balancer Pool Member
</dt>
</dl>

-   Member Status

<dl markdown="1">
<dt markdown="1">
Load Balancer Port
</dt>
</dl>

-   Throughput: Inbound, Outbound (*bytes/sec*)

<dl markdown="1">
<dt markdown="1">
Network Interface
</dt>
</dl>

-   Throughput: Inbound, Outbound (*bits/sec*)
-   Packets: Inbound, Outbound (*packets/sec*)
-   Errors: Inbound, Outbound (*errors/sec*)
-   Drops: Inbound, Outbound (*drops/sec*)
-   Collisions: Collisions (*collisions/sec*)

<dl markdown="1">
<dt markdown="1">
Fan
</dt>
</dl>

-   Fan Speed: Fan Speed (*rpm*)

<dl markdown="1">
<dt markdown="1">
Temperature Sensor
</dt>
</dl>

-   Temperature: Temperature (*celsius*)

### Event Management

Zenoss will create events for any syslog messages or SNMP traps sent by
the load balancer. The load balancer must be configured to send these
messages. Beyond standard SNMP traps, custom traps may be configured on
the BIG-IP according [these instructions](https://devcentral.f5.com/articles/custom-snmp-traps){.external-link}.

This ZenPack includes the following event class mappings for handling
specific syslog messages.

-   /BIG-IP/gtmd: Generic handling of events from gtmd.
-   /BIG-IP/mcpd: Generic handling of events from mcpd.
-   /BIG-IP/tmm: Generic handling of events from tmm.
-   /BIG-IP/monitor_instance_down: Instance monitoring down.
-   /BIG-IP/monitor_instance_up: Instance monitoring up.
-   /BIG-IP/pool_member_down: Pool member down.
-   /BIG-IP/pool_member_up: Pool member up.
-   /BIG-IP/state_change_down: State change down.
-   /BIG-IP/state_change_up: State change up.
-   /BIG-IP/sync_group_joined: Joined sync group.
-   /BIG-IP/sync_group_left: Left sync group.

<dl markdown="1">
<dt markdown="1">
Event Class Mappings (SNMP Notifications)
</dt>
</dl>

-   /Status/Snmp/F5 Labs/bigipARPConflict
-   /Status/Snmp/F5 Labs/bigipActive
-   /Status/Snmp/F5 Labs/bigipActiveActive
-   /Status/Snmp/F5 Labs/bigipAgentRestart
-   /Status/Snmp/F5 Labs/bigipAgentShutdown
-   /Status/Snmp/F5 Labs/bigipAgentStart
-   /Status/Snmp/F5 Labs/bigipAggrReaperStateChange
-   /Status/Snmp/F5 Labs/bigipAomCpuTempTooHigh
-   /Status/Snmp/F5 Labs/bigipAsmBruteForceAttackDetected
-   /Status/Snmp/F5 Labs/bigipAsmDosAttackDetected
-   /Status/Snmp/F5 Labs/bigipAsmFtpRequestBlocked
-   /Status/Snmp/F5 Labs/bigipAsmFtpRequestViolation
-   /Status/Snmp/F5 Labs/bigipAsmRequestBlocked
-   /Status/Snmp/F5 Labs/bigipAsmRequestViolation
-   /Status/Snmp/F5 Labs/bigipAsmSmtpRequestBlocked
-   /Status/Snmp/F5 Labs/bigipAsmSmtpRequestViolation
-   /Status/Snmp/F5 Labs/bigipAuthFailed
-   /Status/Snmp/F5 Labs/bigipAvrAlertsMetricSmtp
-   /Status/Snmp/F5 Labs/bigipAvrAlertsMetricSnmp
-   /Status/Snmp/F5 Labs/bigipBladeNoPower
-   /Status/Snmp/F5 Labs/bigipBladeOffline
-   /Status/Snmp/F5 Labs/bigipBladeTempHigh
-   /Status/Snmp/F5 Labs/bigipChassisFanBad
-   /Status/Snmp/F5 Labs/bigipChassisPowerSupplyBad
-   /Status/Snmp/F5 Labs/bigipChassisTempHigh
-   /Status/Snmp/F5 Labs/bigipChmandAlertFanTrayBad
-   /Status/Snmp/F5 Labs/bigipClusterdNoResponse
-   /Status/Snmp/F5 Labs/bigipCompLimitExceeded
-   /Status/Snmp/F5 Labs/bigipConfigLoaded
-   /Status/Snmp/F5 Labs/bigipCpuFanSpeedBad
-   /Status/Snmp/F5 Labs/bigipCpuFanSpeedLow
-   /Status/Snmp/F5 Labs/bigipCpuTempHigh
-   /Status/Snmp/F5 Labs/bigipDiskPartitionGrowth
-   /Status/Snmp/F5 Labs/bigipDiskPartitionWarn
-   /Status/Snmp/F5 Labs/bigipDosAttackStart
-   /Status/Snmp/F5 Labs/bigipDosAttackStop
-   /Status/Snmp/F5 Labs/bigipExternalLinkChange
-   /Status/Snmp/F5 Labs/bigipFeatureFailed
-   /Status/Snmp/F5 Labs/bigipFeatureOnline
-   /Status/Snmp/F5 Labs/bigipGtmAppAvail
-   /Status/Snmp/F5 Labs/bigipGtmAppNotAvail
-   /Status/Snmp/F5 Labs/bigipGtmAppObjAvail
-   /Status/Snmp/F5 Labs/bigipGtmAppObjNotAvail
-   /Status/Snmp/F5 Labs/bigipGtmBig3dSslCertExpired
-   /Status/Snmp/F5 Labs/bigipGtmBig3dSslCertWillExpire
-   /Status/Snmp/F5 Labs/bigipGtmBoxAvail
-   /Status/Snmp/F5 Labs/bigipGtmBoxNotAvail
-   /Status/Snmp/F5 Labs/bigipGtmDcAvail
-   /Status/Snmp/F5 Labs/bigipGtmDcDisabled
-   /Status/Snmp/F5 Labs/bigipGtmDcEnabled
-   /Status/Snmp/F5 Labs/bigipGtmDcNotAvail
-   /Status/Snmp/F5 Labs/bigipGtmJoinedGroup
-   /Status/Snmp/F5 Labs/bigipGtmKeyGenerationExpiration
-   /Status/Snmp/F5 Labs/bigipGtmKeyGenerationRollover
-   /Status/Snmp/F5 Labs/bigipGtmLeftGroup
-   /Status/Snmp/F5 Labs/bigipGtmLinkAvail
-   /Status/Snmp/F5 Labs/bigipGtmLinkDisabled
-   /Status/Snmp/F5 Labs/bigipGtmLinkEnabled
-   /Status/Snmp/F5 Labs/bigipGtmLinkNotAvail
-   /Status/Snmp/F5 Labs/bigipGtmPoolAvail
-   /Status/Snmp/F5 Labs/bigipGtmPoolDisabled
-   /Status/Snmp/F5 Labs/bigipGtmPoolEnabled
-   /Status/Snmp/F5 Labs/bigipGtmPoolMbrAvail
-   /Status/Snmp/F5 Labs/bigipGtmPoolMbrDisabled
-   /Status/Snmp/F5 Labs/bigipGtmPoolMbrEnabled
-   /Status/Snmp/F5 Labs/bigipGtmPoolMbrNotAvail
-   /Status/Snmp/F5 Labs/bigipGtmPoolNotAvail
-   /Status/Snmp/F5 Labs/bigipGtmProberPoolDisabled
-   /Status/Snmp/F5 Labs/bigipGtmProberPoolEnabled
-   /Status/Snmp/F5 Labs/bigipGtmProberPoolMbrDisabled
-   /Status/Snmp/F5 Labs/bigipGtmProberPoolMbrEnabled
-   /Status/Snmp/F5 Labs/bigipGtmProberPoolMbrStatusChange
-   /Status/Snmp/F5 Labs/bigipGtmProberPoolMbrStatusChangeReason
-   /Status/Snmp/F5 Labs/bigipGtmProberPoolStatusChange
-   /Status/Snmp/F5 Labs/bigipGtmProberPoolStatusChangeReason
-   /Status/Snmp/F5 Labs/bigipGtmServerAvail
-   /Status/Snmp/F5 Labs/bigipGtmServerDisabled
-   /Status/Snmp/F5 Labs/bigipGtmServerEnabled
-   /Status/Snmp/F5 Labs/bigipGtmServerNotAvail
-   /Status/Snmp/F5 Labs/bigipGtmSslCertExpired
-   /Status/Snmp/F5 Labs/bigipGtmSslCertWillExpire
-   /Status/Snmp/F5 Labs/bigipGtmVsAvail
-   /Status/Snmp/F5 Labs/bigipGtmVsDisabled
-   /Status/Snmp/F5 Labs/bigipGtmVsEnabled
-   /Status/Snmp/F5 Labs/bigipGtmVsNotAvail
-   /Status/Snmp/F5 Labs/bigipGtmWideIpAvail
-   /Status/Snmp/F5 Labs/bigipGtmWideIpDisabled
-   /Status/Snmp/F5 Labs/bigipGtmWideIpEnabled
-   /Status/Snmp/F5 Labs/bigipGtmWideIpNotAvail
-   /Status/Snmp/F5 Labs/bigipHardDiskFailure
-   /Status/Snmp/F5 Labs/bigipInetPortExhaustion
-   /Status/Snmp/F5 Labs/bigipLibhalBladePoweredOff
-   /Status/Snmp/F5 Labs/bigipLibhalDiskBayRemoved
-   /Status/Snmp/F5 Labs/bigipLibhalSensorAlarmCritical
-   /Status/Snmp/F5 Labs/bigipLibhalSsdLogicalDiskRemoved
-   /Status/Snmp/F5 Labs/bigipLibhalSsdPhysicalDiskRemoved
-   /Status/Snmp/F5 Labs/bigipLicenseExpired
-   /Status/Snmp/F5 Labs/bigipLicenseFailed
-   /Status/Snmp/F5 Labs/bigipLogAlert
-   /Status/Snmp/F5 Labs/bigipLogCrit
-   /Status/Snmp/F5 Labs/bigipLogEmerg
-   /Status/Snmp/F5 Labs/bigipLogErr
-   /Status/Snmp/F5 Labs/bigipLogWarning
-   /Status/Snmp/F5 Labs/bigipMemberRate
-   /Status/Snmp/F5 Labs/bigipNetLinkDown
-   /Status/Snmp/F5 Labs/bigipNodeDown
-   /Status/Snmp/F5 Labs/bigipNodeRate
-   /Status/Snmp/F5 Labs/bigipNodeUp
-   /Status/Snmp/F5 Labs/bigipPacketRejected
-   /Status/Snmp/F5 Labs/bigipRaidDiskFailure
-   /Status/Snmp/F5 Labs/bigipServiceDown
-   /Status/Snmp/F5 Labs/bigipServiceUp
-   /Status/Snmp/F5 Labs/bigipSsdMwiNearThreshold
-   /Status/Snmp/F5 Labs/bigipSsdMwiReachedThreshold
-   /Status/Snmp/F5 Labs/bigipSslLimitExceeded
-   /Status/Snmp/F5 Labs/bigipStandByFail
-   /Status/Snmp/F5 Labs/bigipStandby
-   /Status/Snmp/F5 Labs/bigipSystemCheckAlertCurrentHigh
-   /Status/Snmp/F5 Labs/bigipSystemCheckAlertCurrentLow
-   /Status/Snmp/F5 Labs/bigipSystemCheckAlertFanSpeedLow
-   /Status/Snmp/F5 Labs/bigipSystemCheckAlertMilliVoltageHigh
-   /Status/Snmp/F5 Labs/bigipSystemCheckAlertMilliVoltageLow
-   /Status/Snmp/F5 Labs/bigipSystemCheckAlertPowerHigh
-   /Status/Snmp/F5 Labs/bigipSystemCheckAlertPowerLow
-   /Status/Snmp/F5 Labs/bigipSystemCheckAlertTempHigh
-   /Status/Snmp/F5 Labs/bigipSystemCheckAlertVoltageHigh
-   /Status/Snmp/F5 Labs/bigipSystemCheckAlertVoltageLow
-   /Status/Snmp/F5 Labs/bigipTamdAlert
-   /Status/Snmp/F5 Labs/bigipUnsolicitedRepliesExceededThreshold
-   /Status/Snmp/F5 Labs/bigipVcmpAlertsVcmpHBDetected
-   /Status/Snmp/F5 Labs/bigipVcmpAlertsVcmpHBLost
-   /Status/Snmp/F5 Labs/bigipVcmpAlertsVcmpPowerOff
-   /Status/Snmp/F5 Labs/bigipVcmpAlertsVcmpPowerOn
-   /Status/Snmp/F5 Labs/bigipVirtualRate
-   /Status/Snmp/F5 Labs/emASMSigInstallComplete
-   /Status/Snmp/F5 Labs/emASMSigInstallFailed
-   /Status/Snmp/F5 Labs/emASMSigUpdateAvailable
-   /Status/Snmp/F5 Labs/emASMSigUpdateFailed
-   /Status/Snmp/F5 Labs/emCertificateExpiration
-   /Status/Snmp/F5 Labs/emCpuUsage
-   /Status/Snmp/F5 Labs/emDeviceActiveMode
-   /Status/Snmp/F5 Labs/emDeviceClockSkew
-   /Status/Snmp/F5 Labs/emDeviceConfigSettingChanged
-   /Status/Snmp/F5 Labs/emDeviceConfigSync
-   /Status/Snmp/F5 Labs/emDeviceForcedOfflineMode
-   /Status/Snmp/F5 Labs/emDeviceImpaired
-   /Status/Snmp/F5 Labs/emDeviceOfflineMode
-   /Status/Snmp/F5 Labs/emDeviceStandbyMode
-   /Status/Snmp/F5 Labs/emDeviceUnreachable
-   /Status/Snmp/F5 Labs/emDiskUsage
-   /Status/Snmp/F5 Labs/emGatherServiceContractFailure
-   /Status/Snmp/F5 Labs/emHaSyncFailed
-   /Status/Snmp/F5 Labs/emHotfixInstallComplete
-   /Status/Snmp/F5 Labs/emHotfixInstallFailed
-   /Status/Snmp/F5 Labs/emMemoryUsage
-   /Status/Snmp/F5 Labs/emPerformanceStorageCap
-   /Status/Snmp/F5 Labs/emPerformanceStorageDays
-   /Status/Snmp/F5 Labs/emPerformanceThreshold
-   /Status/Snmp/F5 Labs/emRaidDriveFailureDetected
-   /Status/Snmp/F5 Labs/emRaidDriveRebuildComplete
-   /Status/Snmp/F5 Labs/emSchedBackupFailed
-   /Status/Snmp/F5 Labs/emScheduledArchiveFailed
-   /Status/Snmp/F5 Labs/emServiceContractExpiry
-   /Status/Snmp/F5 Labs/emSoftwareInstallComplete
-   /Status/Snmp/F5 Labs/emSoftwareInstallFailed
-   /Status/Snmp/F5 Labs/emStatsCollectionRateCap
-   /Status/Snmp/F5 Labs/emStatsDBConnectivityLost
-   /Status/Snmp/F5 Labs/emStatsDBConnectivityRestored
-   /Status/Snmp/F5 Labs/loadBalTrapAddUnit
-   /Status/Snmp/F5 Labs/loadBalTrapDenial
-   /Status/Snmp/F5 Labs/loadBalTrapLogin
-   /Status/Snmp/F5 Labs/loadBalTrapMisc
-   /Status/Snmp/F5 Labs/loadBalTrapRemoveUnit
-   /Status/Snmp/F5 Labs/loadBalTrapReset
-   /Status/Snmp/F5 Labs/loadBalTrapServiceDown
-   /Status/Snmp/F5 Labs/loadBalTrapServiceUP
-   /Status/Snmp/F5 Labs/threednsTrapCRCFailure
-   /Status/Snmp/F5 Labs/threednsTrapServerGreenToRed
-   /Status/Snmp/F5 Labs/threednsTrapServerRedToGreen
-   /Status/Snmp/F5 Labs/threednsTrapVSGreenToRed
-   /Status/Snmp/F5 Labs/threednsTrapVSRedToGreen

This ZenPack includes the following SNMP MIBs and therefore the ability
to decode traps defined therein.

-   F5-3DNS-MIB
-   F5-BIGIP-APM-MIB
-   F5-BIGIP-COMMON-MIB
-   F5-BIGIP-LOCAL-MIB
-   F5-BIGIP-SYSTEM-MIB
-   F5-BIGIP-WAM-MIB
-   F5-BIGIP-EM-MIB
-   LOAD-BAL-SYSTEM-MIB

## Service Impact and Root Cause Analysis

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact and root cause analysis capabilities for
services running on IBM Power. The service impact relationships shown in
the diagram and described below are automatically added. These will be
included in any services that contain one or more of the explicitly
mentioned components.

@lb[](img/zenpack-bigip-impact-yuml.png)

<dl markdown="1">
<dt markdown="1">
Internal Impact Relationships
</dt>
</dl>

-   Device impacts LTM Virtual Server
-   Device impacts LB Port
-   Device impacts LB Pool/LB Pool Member
-   LB Pool impacts LB Pool Member

## Usage

### Adding BIG-IP Load Balancer

BIG-IP load balancer devices must be added to the /Network/BIG-IP device
class. Otherwise they are added in the same manner as any SNMP device.

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Configuration Properties
</dt>
</dl>

-   zLTMVirtualServerIgnoreNames: Regular expression that can be used to
    prevent matching LTM Virtual Servers from being modeled.

<dl markdown="1">
<dt markdown="1">
Device Classes
</dt>
</dl>

-   /Network/BIG-IP

<dl markdown="1">
<dt markdown="1">
Modeler Plugins
</dt>
</dl>

-   snmp.bigip.DeviceMap (Load Balancer, CPUs, Fans, Power Supplies,
    Temperator Sensors)
-   snmp.bigip.InterfaceMap (Network Interfaces: Physical & VLAN)
-   snmp.bigip.LBPoolMap (Load Balancer Pools and Pool Members)
-   snmp.bigip.LBPort (Load Balancer Ports)
-   snmp.bigip.VirtualServers (LTM Virtual Servers)

<dl markdown="1">
<dt markdown="1">
Monitoring Templates (all in /Network/BIG-IP)
</dt>
</dl>

-   BigIpDevice (Load Balancer)
-   bigipInterface (Network Interface: Physical)
-   bigipVLAN (Network Interface: VLAN)
-   CPU
-   Fan
-   LBPool (Load Balancer Pool)
-   LBPoolMember (Load Balancer Pool Member)
-   LBPort (Load Balancer Port)
-   LTMVirtualServer (LTM Virtual Server)
-   TemperatureSensor (Temperature Sensor)

## Known issues

**Upgrade from 2.7.1**

When
upgrading from 2.7.1 to a newer version, a message such as
"ERROR:zen.zenpacklib:Monitoring template /Network/BIG-IP/CPU has been
modified since the ZenPacks.zenoss.BigIpMonitor ZenPack was installed.
These local changes will be lost as this ZenPack is upgraded or
reinstalled. Existing template will be renamed to
'CPU-upgrade-1600253879'. Please review and reconcile local changes:"
may be displayed.

If
the only difference shown is the changing of some datapoints types from
'{}' to 'GAUGE' and 'oid' fields from unicode to string, this may be
disregarded, and the CPU-upgrade-&lt;number&gt; template may be deleted
if desired.

## Changes

<dl markdown="1">
<dt markdown="1">
2.7.2
</dt>
</dl>

-   Improve UI loading speed of LB
    Pool Members (ZPS-6488)
-   Fix invalid Threshold in
    /Network/BIG-IP "Free TMM memory" (ZPS-4831)
-   Fix uncorroborated impact
    relationships for LB Pool Members (ZPS-5890)
-   Fix CPU Utilization graph
    (ZPS-7245)
-   Add ZenPackLib ZP and
    CalculatedPerformance ZP to requirements
-   Tested with Zenoss Resource
    Manager 6.4.1, Zenoss Resource Manager 6.5.0, Zenoss Cloud and
    Service Impact 5.5.2

<dl markdown="1">
<dt markdown="1">
2.7.1
</dt>
</dl>

-   Convert load balancer port speed from megabits to bits
-   Add datapoint aliases: mem\_\_pct, in\_\_pct, out\_\_pct (ZEN-24619)

<dl markdown="1">
<dt markdown="1">
2.7.0
</dt>
</dl>

-   Conversion to ZPL
-   Updated F5 MIBs
-   Fixed MIB conflict issues for independently loaded MIBs
-   Added Event Class Instances for all SNMP notifications including
    correlations
-   Integration with Service Impact
-   Added Icons for Service Impact/Dynamic View
-   Additional monitoring for PowerSupply
-   Revised/corrected datapoint types within RRD Templates
-   Improved device resource modeling for memory (host vs. TMM) and swap
-   Fixed numerous modeler issues
-   Improved Zenoss 5.x compatibility

<dl markdown="1">
<dt markdown="1">
2.6.4
</dt>
</dl>

-   Update CPU Utilization graph to work on Zenoss 5.
-   Allow toggling of monitoring for components. (ZEN-15232)

<dl markdown="1">
<dt markdown="1">
2.6.3
</dt>
</dl>

-   Change LTM virtual server and pool IDs to be unique.

<dl markdown="1">
<dt markdown="1">
2.6.2
</dt>
</dl>

-   Change pool member IDs to &lt;pool-address-port&gt;.
-   Model chassis serial number.

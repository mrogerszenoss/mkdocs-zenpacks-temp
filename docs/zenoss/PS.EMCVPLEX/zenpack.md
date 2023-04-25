# EMC VPLEX Integration ZenPack

** **Subscription

This integration is a subscription-based Professional Services
engagement. Our Integration Services are offered as subscriptions in
order to provide initial setup and ongoing compatibility and
maintenance. All standard packages are renewable every 12 months from
the date of purchase. Contact Zenoss to request more information
regarding this or any other ZenPacks.

**Authors:**

Zenoss Inc.

**Maintainers:**

Zenoss Inc.

**Organization:**

Zenoss Inc.

**Name:**

EMC VPLEX Integration ZenPack

**Release:**

1.0

## EMC VPLEX Integration ZenPack

## About

This ZenPack receives SNMP Traps and transforms them into Zenoss Events.
Device modeling and monitoring is provided via SNMP and REST API
Connectivity.

## Limitations

ZenPack is designed to support the following VPLEX device models: Local
and Metro version 5.3

## Prerequisites

| Prerequisite       | Restriction                                                                |
|--------------------|----------------------------------------------------------------------------|
| Product            | Zenoss 4.2.5 or higher                                                     |
| Required ZenPacks  | ZenPacks.zenoss.ZenPackLib &gt;= 2.1.1 ZenPacks.zenoss.PS.Util &gt;= 1.2.0 |
| Other dependencies | None                                                                       |

## Features

### Device Classes

A new device class **/Storage/EMCVPLEX** will be added

### Configuration properties

Basic device monitoring uses SNMP, for full modeling REST API
Credentials must be provided:

> -   zEMCVPLEXUsername
> -   zEMCVPLEXPassword
> -   zEMCVPLEXPort
> -   zEMCVPLEXSSL
> -   zEMCVPLEXConcurrency
>     -   The number of concurrent connections allowed to the VPLEX
>         endpoint. (Note: the limit is enforced per-process, so
>         Modeling and Collection may both hit this limit.)
>     -   Default: 3

### Device Monitoring

The following metrics are monitored on the VPLEX Device via SNMP.

> -   CPU Idle
> -   Heap Used
> -   Front End Ports
>     -   Bytes Read/Write
>     -   Ops Read/Write
>     -   Average Read/Write Latency
>     -   Ops Active
>     -   Ops Queued
> -   Backend Ports
>     -   Bytes Read/Write
>     -   Ops Read/Write

### Components

> -   VPLEX Engine
>     -   Modeled Attributes
>         -   family
>         -   part_number
>         -   revision_number
>         -   serial_number
>         -   wwn_seed
>     -   Monitoring
>         -   HealthState
>         -   OperationalStatus
> -   VPLEX Fan
>     -   Monitoring
>         -   OperationalStatus
>         -   SpeedThresholdStatus
> -   VPLEX Power Supply
>     -   Modeled Attributes
>         -   part_number
>         -   revision_number
>         -   serial_number
>     -   Monitoring
>         -   OperationalStatus
>         -   TemperatureThresholdStatus
> -   VPLEX Consistency Group
>     -   Modeled Attributes
>         -   cache_mode
>         -   detach_rule
>         -   recoverpoint_enabled
>         -   storage_at_cluster
> -   VPLEX Storage Volume
>     -   Modeled Attributes
>         -   capacity
>         -   io_status
>         -   storage_volume_type
>         -   total_free_space
>         -   vendor_specific_name
>         -   storage_array
>     -   Monitoring
>         -   OperationalStatus
>         -   HealthState
> -   VPLEX Virtual Volume
>     -   Modeled Attributes
>         -   capacity
>         -   expandable
>         -   expandable_capacity
>         -   expansion_method
>         -   recoverpoint_usage
>         -   volume_type
> -   VPLEX Cluster
>     -   Modeled Attributes
>         -   top_level_assembly
>         -   default_director
>     -   Monitoring
>         -   HealthState
>         -   OperationalStatus
> -   VPLEX Extent
>     -   Modeled Attributes
>         -   capacity
>         -   vendor_name
>         -   storage_volume
>         -   storage_volume_type
>         -   system_id
>     -   Monitoring
>         -   HealthState
>         -   OperationalStatus
> -   VPLEX Local Device
>     -   Modeled Attributes
>         -   capacity
>         -   expandable_capacity
>         -   geometry
>         -   stripe_depth
>     -   Monitoring
>         -   HealthState
>         -   OperationalStatus
> -   VPLEX Storage Array
>     -   Modeled Attributes
>         -   auto_switch
>         -   controllers
>         -   ports
>     -   Monitoring
>         -   ConnectivityStatus
> -   VPLEXLun
>     -   Modeled Attributes
>         -   active_controller
>         -   alua_support
>         -   passive_controller
>         -   visibility
>     -   Monitoring
>         -   ConnectivityStatus

### Events

This ZenPack uses Transforms to generate the following events from SNMP
Traps:

| VPLEX Event Code | Severity | Description                                                                                                                                                                  |
|------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x8a029033       | CRITICAL | The on-disk configuration information for the reported device is inconsistent, due to the parent having an invalid type.                                                     |
| 0x8a029034       | CRITICAL | The on-disk configuration information for the reported device is inconsistent.                                                                                               |
| 0x8a029035       | CRITICAL | The on-disk configuration information for the reported device is inconsistent.                                                                                               |
| 0x8a029036       | CRITICAL | The on-disk configuration information for the reported device is inconsistent.                                                                                               |
| 0x8a029037       | CRITICAL | The on-disk configuration information for the reported device is inconsistent.                                                                                               |
| 0x8a029038       | CRITICAL | The on-disk configuration information for the reported device is inconsistent because a parent device has a blocksize of zero.                                               |
| 0x8a029039       | CRITICAL | The on-disk configuration information for the reported device is inconsistent.                                                                                               |
| 0x8a02903a       | CRITICAL | The on-disk configuration information for the reported device is inconsistent due to inconsistent child and parent node counts.                                              |
| 0x8a02903b       | CRITICAL | The on-disk configuration information for the reported device has inconsistent sibling IDs.                                                                                  |
| 0x8a02903c       | CRITICAL | The on-disk version configuration information for the reported device is inconsistent.                                                                                       |
| 0x8a02903d       | CRITICAL | The on-disk configuration information for the reported device is inconsistent because different child and parent versions were detected.                                     |
| 0x8a02903e       | CRITICAL | The on-disk configuration information for the reported device is inconsistent because of an unknown parent type.                                                             |
| 0x8a02903f       | CRITICAL | The on-disk configuration information for the reported device is inconsistent because the parent's child slot already in use.                                                |
| 0x8a029040       | CRITICAL | The on-disk configuration information for the reported device is inconsistent due to the proposed and current child versions.                                                |
| 0x8a029045       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent because the child name exceeds the maximum length.                                              |
| 0x8a029046       | CRITICAL | The on-disk configuration information for the reported device is inconsistent because there is no noodecount for the parent.                                                 |
| 0x8a029047       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent because a parent ID has an invalid length.                                                      |
| 0x8a029048       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent due to the invalid length of the parent type.                                                   |
| 0x8a029049       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent due to the child node count being exceeded.                                                     |
| 0x8a02904b       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent.                                                                                                |
| 0x8a02904c       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent.                                                                                                |
| 0x8a02904d       | CRITICAL | Check the status of the devices to determine which device is not available.                                                                                                  |
| 0x8a02904e       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent.                                                                                                |
| 0x8a02904f       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent.                                                                                                |
| 0x8a029050       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent.                                                                                                |
| 0x8a029051       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent.                                                                                                |
| 0x8a029052       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent.                                                                                                |
| 0x8a029053       | CRITICAL | Check the status of the devices to determine which device is not available.                                                                                                  |
| 0x8a029054       | CRITICAL | The on-disk configuration information for the reported device is inconsistent.                                                                                               |
| 0x8a029055       | CRITICAL | The on-disk configuration information for the reported device is inconsistent.                                                                                               |
| 0x8a029056       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent.                                                                                                |
| 0x8a029057       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent.                                                                                                |
| 0x8a029058       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent.                                                                                                |
| 0x8a029059       | CRITICAL | The on-disk configuration information for one of the devices is inconsistent.                                                                                                |
| 0x8a02905c       | CRITICAL | The on-disk configuration information for the reported device is inconsistent.                                                                                               |
| 0x8a029060       | CRITICAL | The storage volume has become unreachable.                                                                                                                                   |
| 0x8a029061       | CRITICAL | The storage volume has failed, and there is no mirror of the storage volume.                                                                                                 |
| 0x8a026062       | ERROR    | The system lost access to the reported storage volume.                                                                                                                       |
| 0x8a02606f       | ERROR    | Two discovered devices reported the same device name.                                                                                                                        |
| 0x8a029071       | CRITICAL | Conflicting device configuration information was found on storage volumes.                                                                                                   |
| 0x8a029072       | CRITICAL | The given storage volume has problems that prevent VPLEX from reading data on it.                                                                                            |
| 0x8a02907a       | CRITICAL | The on-disk configuration information for the reported device is inconsistent.                                                                                               |
| 0x8a02907b       | CRITICAL | The on-disk configuration information for the reported device is inconsistent.                                                                                               |
| 0x8a02307e       | WARNING  | The system has lost access to the logging-volume device on which it was maintaining a list of changes to the reported device.                                                |
| 0x8a029089       | CRITICAL | VPLEX cannot do the necessary sector reassignment, because the reported storage volume has no mirror.                                                                        |
| 0x8a02308d       | WARNING  | If we are currently rebuilding the mirror, we will roll back the write only as far as the block in question.                                                                 |
| 0x8a029092       | CRITICAL | All of the mirrors of the specified distributed device had been marked out of date.                                                                                          |
| 0x8a029093       | CRITICAL | A miki-rebuild has failed because I/O that was part of that rebuild has failed to the local child of a distributed RAID-1.                                                   |
| 0x8a02609e       | ERROR    | A storage volume has been provisioned to this cluster, even though the storage volume logically belongs to another cluster.                                                  |
| 0x8a0290a2       | CRITICAL | The active meta-volume has become unhealthy and is at risk.                                                                                                                  |
| 0x8a0260b5       | ERROR    | Manual intervention is required.                                                                                                                                             |
| 0x8a0260be       | ERROR    | The automatic detach of the given cluster from the given device was disallowed, in order to preserve consistency on the device and avoid losing data.                        |
| 0x8a0260bf       | ERROR    | The automatic detach of missing clusters from the given device was disallowed based on majority rules, in order to preserve consistency on the device and avoid losing data. |
| 0x8a0290c5       | CRITICAL | A write to the specified metadata volume has failed.                                                                                                                         |
| 0x8a0290d1       | CRITICAL | A conflict has been detected between the views of two or more directors as to which metadata amf should be marked active at a cluster.                                       |
| 0x8a0290dd       | CRITICAL | The same disk has been not only presented to multiple clusters, but claimed at those clusters as well.                                                                       |
| 0x8a0230df       | WARNING  | A disk in a metadata volume has become unreachable or unhealthy, thereby reducing the redundancy of the metadata volume.                                                     |
| 0x8a0230e2       | WARNING  | A fixed time has passed after the local cluster last booted, and the active metadata volume has not yet been detected.                                                       |
| 0x8a0290e5       | CRITICAL | Invalid settings were read from the metadata.                                                                                                                                |
| 0x8a0290e6       | CRITICAL | Check the status of the devices to determine which device is not available.                                                                                                  |
| 0x8a0290e7       | CRITICAL | Check the status of the devices to determine which device is not available.                                                                                                  |
| 0x8a0230e9       | WARNING  | Metavolume is running out of available space.                                                                                                                                |
| 0x8a0290f4       | CRITICAL | All the storage-volume(s) supporting this mirror leg are performing very poorly, causing severe degradation in the RAID-1 performance.                                       |
| 0x8a036010       | ERROR    | Ensure the spare pools required to support automatic storage volume replacement exist and contain storage volumes.                                                           |
| 0x8a0a300b       | WARNING  | Local directors are running different versions of software.                                                                                                                  |
| 0x8a0a6018       | ERROR    | Several wan-com or local-com messages took longer than the allowed round-trip latency in the past hour.                                                                      |
| 0x8a459010       | CRITICAL | An IP network device is no longer present.                                                                                                                                   |
| 0x8a453013       | WARNING  | Link went down on a port, depending on the port role, a physical path to local or remote cluster has been lost.                                                              |
| 0x8a459018       | CRITICAL | An SFP is missing, inserted incorrectly, or faulty.                                                                                                                          |
| 0x8a45901a       | CRITICAL | The EMC part number of the SFP was not recognized.                                                                                                                           |
| 0x8a45901c       | CRITICAL | Incoming laser is not detected on an optical Ethernet port.                                                                                                                  |
| 0x8a45901e       | CRITICAL | One 10Gig Ethernet IO module has defective firmware.                                                                                                                         |
| 0x8a45301f       | WARNING  | One 10Gig Ethernet IO module has firmware version that is earlier than any validated version.                                                                               |
| 0x8a453022       | WARNING  | Attempts to establish the link is failing continuously.                                                                                                                      |
| 0x8a456027       | ERROR    | The WAN-COM port is configured with non IPV4 protocol.                                                                                                                       |
| 0x8a45302e       | WARNING  | The last redundant IP path to the specified director is down.                                                                                                                |
| 0x8a0e901c       | CRITICAL | A series of transient errors were detected while trying to read or write the given block range of the given storage volume.                                                  |
| 0x8a109002       | CRITICAL | During failure recovery, another disruption occurred, and could not be handled.                                                                                              |
| 0x8a113014       | WARNING  | Recovery from simple director failure took too long.                                                                                                                         |
| 0x8a183004       | WARNING  | If the director has halted due to a software error, it will be reset automatically; otherwise, manual intervention will be required.                                         |
| 0x8a18901f       | CRITICAL | Either a memory leak has occurred or the VPLEX has exceeded its configuration limits.                                                                                        |
| 0x8a186020       | ERROR    | An internal environment operation failed.                                                                                                                                    |
| 0x8a266032       | ERROR    | The last director with the given cluster id has departed.                                                                                                                    |
| 0x8a269038       | CRITICAL | This director is trying to kill the identified director, but the call to do that has failed.                                                                                 |
| 0x8a269039       | CRITICAL | An internal call to reset another director has failed.                                                                                                                       |
| 0x8a266040       | ERROR    | A director with a different version of firmware may have been inserted into the cluster.                                                                                     |
| 0x8a266041       | ERROR    | A director with a different version of firmware may have been inserted into the cluster.                                                                                     |
| 0x8a266042       | ERROR    | A director with a different version of firmware may have been inserted into the cluster.                                                                                     |
| 0x8a266043       | ERROR    | A director with a different version of firmware may have been inserted into the cluster.                                                                                     |
| 0x8a269045       | CRITICAL | The director will be in a partially booted state, which allows a value to be set for director-count.                                                                         |
| 0x8a266064       | ERROR    | This failure exposes the cluster to a Data Unavailability condition in certain director failure/inter-director link failure scenarios.                                       |
| 0x8a269069       | CRITICAL | The cluster reporting this event has been unable to establish communication with Cluster Witness Server.                                                                     |
| 0x8a266073       | ERROR    | Cluster Witness cannot be enabled on systems with more than the supported number of clusters.                                                                                |
| 0x8a269074       | CRITICAL | The cluster reporting this event has been unable to receive any guidance from the Cluster Witness Server for the last 10 seconds.                                            |
| 0x8a266078       | ERROR    | There are no known causes for this condition.                                                                                                                                |
| 0x8a276005       | ERROR    | The non-volatile file system has been corrupted and must be repaired.                                                                                                        |
| 0x8a276006       | ERROR    | The non-volatile file system is either not configured or has been corrupted.                                                                                                 |
| 0x8a276007       | ERROR    | Create a larger meta-volume with a larger NVOL file system.                                                                                                                  |
| 0x8a276009       | ERROR    | A write error occurred to the non-volatile storage server and data was not written to disk.                                                                                  |
| 0x8a2d6045       | ERROR    | The failure is due to the limit on number of steps that can be added was reached.                                                                                            |
| 0x8a2d6046       | ERROR    | Tried to allocate structure and failed.                                                                                                                                      |
| 0x8a2d6047       | ERROR    | A logical unit has inconsistent path types.                                                                                                                                  |
| 0x8a2d304f       | WARNING  | Target device advertised a behavior which is not supported by the VPLEX initiator.                                                                                           |
| 0x8a2d605b       | ERROR    | LuId already has maximum controllers allowed on this array.                                                                                                                  |
| 0x8a2d307b       | WARNING  | A back end Logical Unit has reported an unexpected peripheral qualifier.                                                                                                     |
| 0x8a2d307e       | WARNING  | An inconsistent ALUA support level has been detected for a logical unit.                                                                                                     |
| 0x8a2d608A       | ERROR    | This logical unit is reserved by another initiator.                                                                                                                          |
| 0x8a2d6093       | ERROR    | LU mapping on the back-end array had changed.                                                                                                                                |
| 0x8a2d6094       | ERROR    | This Initiator-Target connection is failing and is out of service.                                                                                                           |
| 0x8a2d309A       | WARNING  | This logical unit has been busy more often than is considered acceptable                                                                                                     |
| 0x8a2d309e       | WARNING  | The array reported an unexpected serial number.                                                                                                                              |
| 0x8a04900f       | CRITICAL | This is likely indicative of severely degraded hardware and/or fabric condition.                                                                                             |
| 0x8a343017       | WARNING  | The host application or OS requested an invalid transfer size on a Scsi Compare and Write Command.                                                                           |
| 0x8a343018       | WARNING  | The host application or OS specified an out of range Logical Block Address on a Scsi Compare and Write Command.                                                              |
| 0x8a346019       | ERROR    | The VPLEX director had insufficient memory resources to process the Scsi Compare and Write Command.                                                                          |
| 0x8a34601a       | ERROR    | The attempt to start a cache transaction for a Scsi Compare and Write command failed.                                                                                        |
| 0x8a34601d       | ERROR    | The VPLEX director had insufficient memory resources to process the Scsi Write Same Command.                                                                                 |
| 0x8a34301e       | WARNING  | The attempt to start a cache transaction for a Scsi Write Same command failed.                                                                                               |
| 0x8a34301f       | WARNING  | Scsi Write Same command processing is disabled on VPLEX.                                                                                                                     |
| 0x8a346020       | ERROR    | Host initiator has issued target reset due to slow I/O processing.                                                                                                           |
| 0x8a3a9000       | CRITICAL | An internal software error has occurred, which may be triggered by unexpected changes in the cluster's environment or configuration.                                         |
| 0x8a3a6010       | ERROR    | There are already three instances of the given management command currently running, and more than three are not allowed.                                                    |
| 0x8a523001       | WARNING  | A persisted record for a consistency group had a format unrecognized by the system.                                                                                          |
| 0x8a523002       | WARNING  | A persisted record for a volume set property had a format unrecognized by the system.                                                                                        |
| 0x8a523003       | WARNING  | A persisted record for a volume set property had a type unrecognized by the system.                                                                                          |
| 0x8a52601d       | ERROR    | The system disallowed the automatic detach of the given cluster from the given volume set, in order to preserve consistency on the volumes in the set and avoid losing data. |
| 0x8a52601f       | ERROR    | The system did not allow the automatic majority detach of missing clusters on the given volume set.                                                                          |
| 0x8a403008       | WARNING  | Crash consistency has been lost on the given async consistency group, due to unplanned loss of data, or inability to write a crash-consistent image.                         |
| 0x8a40901d       | CRITICAL | The "active-cluster-wins" rule-set has been set on the given consistency group, and the given cluster has departed.                                                          |
| 0x8a250018       | INFO     | NDU of the VPLEX has finished successfully.                                                                                                                                  |
| 0x8a256019       | ERROR    | NDU of the VPLEX encountered a problem.                                                                                                                                      |
| 0x8A486197       | ERROR    | The Management Module is not present in the specified slot.                                                                                                                  |
| 0x8A486198       | ERROR    | The operational state of the management module has changed to faulted.                                                                                                       |
| 0x8A48619A       | ERROR    | The FC I/O Module is not present in the specified slot.                                                                                                                      |
| 0x8A48619E       | ERROR    | The power supply in the specified slot is in faulted state.                                                                                                                  |
| 0x8A48926C       | CRITICAL | The input air temperature to the power supply has exceeded the threshold levels.                                                                                             |
| 0x8A4861A0       | ERROR    | The fan in the specified slot has faulted.                                                                                                                                   |
| 0x8A489259       | CRITICAL | The speed of the fan has dropped below the threshold value.                                                                                                                  |
| 0x8A4861B9       | ERROR    | The SPS is in a faulted state.                                                                                                                                               |
| 0x8A48925A       | CRITICAL | The temperature of the enclosure has exceeded the threshold and a result of which the director is shutting down.                                                             |
| 0x8A4830D7       | WARNING  | The director fault code represents the last hardware operation or a hardware fault.                                                                                          |
| 0x8A4861A7       | ERROR    | A communication failure has been reported while attempting to contact the UPS.                                                                                               |
| 0x8A4861A8       | ERROR    | The state of the I/O Annex is faulted                                                                                                                                        |
| 0x8A4861BB       | ERROR    | The UPS is in a faulted state.                                                                                                                                               |
| 0x8A48925D       | CRITICAL | This could be due to faulty serial port on management module, faulty serial cable between the management module and the UPS, faulty UPS or missing UPS in the cluster.       |
| 0x8A4830DE       | WARNING  | The UPS has a problem with its charging hardware.                                                                                                                            |
| 0x8A4861A9       | ERROR    | The I/O Module is not present in the specified slot of the I/O Annex.                                                                                                        |
| 0x8A4861AB       | ERROR    | The Gigabit Ethernet I/O Module is not present in the specified slot.                                                                                                        |
| 0x8A48926D       | CRITICAL | The power supply is not present in the specified slot.                                                                                                                       |
| 0x8A4861AE       | ERROR    | The fan in the specified slot is not present.                                                                                                                                |
| 0x8A489264       | CRITICAL | Fans in the specified slots are in faulted state.                                                                                                                            |
| 0x8A4861B1       | ERROR    | The midplane is not present in the specified slot.                                                                                                                           |
| 0x8A4861B2       | ERROR    | The operating status of the director is faulted.                                                                                                                             |
| 0x8A4861B3       | ERROR    | The director specified is not present in the engine.                                                                                                                         |
| 0x8A4861B4       | ERROR    | The state of the FC I/O Module has changed to faulted.                                                                                                                       |
| 0x8A4861B5       | ERROR    | The state of the Gigabit Ethernet I/O Module has changed to faulted.                                                                                                         |
| 0x8A4861B6       | ERROR    | The state of the SSD drive has changed to faulted.                                                                                                                           |
| 0x8A4861B7       | ERROR    | The SSD drive could not be detected in the director.                                                                                                                         |
| 0x8A4861B8       | ERROR    | The configuration on the ethernet switch of the management module could not be updated due to a software failure.                                                            |
| 0x8A4861C5       | ERROR    | The SSD drive on the director failed.                                                                                                                                        |
| 0x8A48925E       | CRITICAL | The power and environment monitoring process failed due to an internal error.                                                                                                |
| 0x8A489269       | CRITICAL | An internal hardware error has been detected on one of the directors.                                                                                                        |
| 0x8A48926A       | CRITICAL | An internal hardware error has been detected on one of the directors.                                                                                                        |
| 0x8A4a31F4       | WARNING  | Management of remote and distributed resources is no longer possible.                                                                                                        |
| 0x8A4a61F6       | ERROR    | The Host Certificate will expire within a week.                                                                                                                              |
| 0x8A4a61F7       | ERROR    | The CA certificate will expire in a week.                                                                                                                                    |
| 0x8A4a91F8       | CRITICAL | Your CA certificate has expired.                                                                                                                                             |
| 0x8A4a91F9       | CRITICAL | Your Host certificate has expired.                                                                                                                                           |
| 0x8A4a61FA       | ERROR    | A partition on your Management Server has exceeded a critical capacity threshold.                                                                                            |
| 0x8A4a31FB       | WARNING  | A partition on your Management Server has reached a high capacity.                                                                                                           |
| 0x8a363014       | WARNING  | Some amount of IO failure on a login due to dropped frames.                                                                                                                  |
| 0x8a369015       | CRITICAL | Some amount of IO failed because frames timed out.                                                                                                                           |
| 0x8a369018       | CRITICAL | A Fibre Channel port is continuously toggling between linkup and linkdown.                                                                                                   |
| 0x8a36301a       | WARNING  | The RX Power level on a Fibre Channel port is below the low limit and IO timeouts have occurred.                                                                             |
| 0x8a36901c       | CRITICAL | The EMC part number of the SFP was not recognized.                                                                                                                           |
| 0x8a36301d       | WARNING  | The port is equipped with an SFP with approved EMC part number for this product, but the vendor part number is not on the recognized list.                                   |
| 0x8a363030       | WARNING  | An FC chip detected persistent PCI error.                                                                                                                                    |
| 0x8a363034       | WARNING  | Interface received frames with EOFa (End of Frame Abort) delimiter in the last minute.                                                                                       |
| 0x8a363035       | WARNING  | Interface discarded frame(s) in the last minute.                                                                                                                             |
| 0x8a363036       | WARNING  | Interface received frames with CRC error in the last minute.                                                                                                                 |
| 0x8a363037       | WARNING  | Interface received frames with protocol error in the last minute.                                                                                                            |
| 0x8a363039       | WARNING  | An FC port is being turned off because RX power low and IO timeout.                                                                                                          |
| 0x8a36303a       | WARNING  | An FC port's TX power is too low.                                                                                                                                            |
| 0x8a4b9000       | CRITICAL | The filesystem monitor failed to retrieve the status of one of the filesystems that it was monitoring.                                                                       |
| 0x8a4b9001       | CRITICAL | A filesystem has exceeded its usage threshold and is getting low on free space.                                                                                              |
| 0x8A4830D8       | WARNING  | The temperate of the I/O Annex is nearing the error threshold levels due to some environmental conditions.                                                                   |
| 0x8A4830DB       | WARNING  | Conditioning of an SPS has been missed for two cycles.                                                                                                                       |
| 0x8A4830DC       | WARNING  | The fibre channel switch and/or management server are not plugged in to the UPS.                                                                                             |
| 0x8A4861C7       | ERROR    | The I/O Annex is not present in the specified slot.                                                                                                                          |
| 0x8A4861C8       | ERROR    | An I/O Annex fuse has faulted.                                                                                                                                               |
| 0x8A4861C9       | ERROR    | A fan in the I/O Annex has faulted.                                                                                                                                          |
| 0x8A4830E7       | WARNING  | An internal PROM has become corrupted.                                                                                                                                       |
| 0x8A4861CE       | ERROR    | Unable to arbitrate for the top-level I2C mux.                                                                                                                               |
| 0x8A4861CF       | ERROR    | Unable to arbitrate for the I2C bus.                                                                                                                                         |
| 0x8A4861D0       | ERROR    | Unable to configure the top-level I2C mux.                                                                                                                                   |
| 0x8A4861D1       | ERROR    | Configuration of the switches on the I2C bus failed.                                                                                                                         |
| 0x8A4861D3       | ERROR    | The SCL signal on the specified I2C bus is shorted to ground.                                                                                                                |
| 0x8A489265       | CRITICAL | The temperature of the I/O Annex has exceeded the threshold and a result of which the I/O Annex is shutting down.                                                            |
| 0x8A489266       | CRITICAL | Both fans in the I/O Annex have faulted.                                                                                                                                     |
| 0x8A4830E9       | WARNING  | The specified FRU cannot be accessed.                                                                                                                                        |
| 0x8A4861D6       | ERROR    | The specified FRU is not present.                                                                                                                                            |
| 0x8A4861D7       | ERROR    | The state of the specified FRU is faulted                                                                                                                                    |
| 0x8A4830EA       | WARNING  | Memory configuration error has been detected.                                                                                                                                |
| 0x8A4830EB       | WARNING  | An internal hardware error has been detected.                                                                                                                                |
| 0x8A4830EC       | WARNING  | An error occurred accessing an NVRAM log.                                                                                                                                    |
| 0x8A4861DA       | ERROR    | An SPS conditioning cycle has failed because the battery can no longer hold a sufficient charge.                                                                             |
| 0x8A4E9002       | CRITICAL | The cluster has started vaulting either because user initiated a manual vault or due to a persistent power and/or environmental conditions.                                  |
| 0x8A4E900D       | CRITICAL | Vault recovery on the cluster cannot proceed because all director(s) required to complete recovery are either not operational or communicating.                              |
| 0x8A4E9015       | CRITICAL | The director(s) in the cluster are taking more than expected time to quiesce IO and freeze the cache for vaulting.                                                           |
| 0x8A4C9259       | CRITICAL | GeoSynchrony has failed three times continuously.                                                                                                                            |
| 0x8A4C925A       | CRITICAL | GeoSynchrony has failed due to an internal error.                                                                                                                            |
| 0x8a519001       | CRITICAL | Errors have been detected that prevent the director from starting fully.                                                                                                     |
| 0x8a519002       | CRITICAL | Errors have been detected that prevent the director from starting fully.                                                                                                     |
| 0x8a519003       | CRITICAL | Errors have been detected that prevent the director from starting fully.                                                                                                     |
| 0x8A4A3002       | WARNING  | Automated meta-volume backup has not been properly configured, or the configuration file was removed.                                                                        |
| 0x8A4A3003       | WARNING  | One, or both, Storage volumes reserved for automated meta-volume backup are used by manually created meta-volume backups.                                                    |
| 0x8A4A6007       | ERROR    | Detected incorrect number of storage-volumes configured for automated meta-volume backup.                                                                                    |
| 0x8A4A6006       | ERROR    | The automated backup of the meta-volume could not be completed.                                                                                                              |
| 0x8a543013       | WARNING  | A communication port didn't reach link up in time.                                                                                                                           |
| 0x8a543019       | WARNING  | The last redundant FC path to the specified VPLEX WAN-COM port is down.                                                                                                      |
| 0x8a54601b       | ERROR    | Stuck IO had been detected on an FC port.                                                                                                                                    |
| 0x8a54301d       | WARNING  | Large number of i/os have timed out on this connection in the past one minute.                                                                                               |
| 0x8a559001       | CRITICAL | A service has stopped running because it has encountered multiple failures.                                                                                                  |
| 0x8a556002       | ERROR    | A service has stopped running because it has encountered multiple failures.                                                                                                  |
| 0x8a4A6067       | ERROR    | The queue of call-home events being processed hit the length of the queue.                                                                                                   |
| 0x8a4A0065       | INFO     | Attempting to resume normal monitoring                                                                                                                                       |
| 0x8a4A0066       | INFO     | Attempting to resume normal monitoring                                                                                                                                       |
| 0x8a343022       | WARNING  | Scsi xcopy command processing is disabled on VPLEX.                                                                                                                          |
| 0x8a346026       | ERROR    | A xcopy command was aborted because of a system memory allocation failure.                                                                                                   |
| 0x8a346027       | ERROR    | A xcopy command was aborted because of a slab memory allocation failure.                                                                                                     |
| 0x8a349035       | CRITICAL | An IO failed to complete or be properly aborted and cleaned up.                                                                                                              |

## Impact diagram v1

EMC Vplex internal impact diagram(EMC Vplex device and components)

\[VplexDevice\]-impacts&gt;\[Engine\]

\[VplexDevice\]-impacts&gt;\[Cluster\]

\[Engine\]-impacted by&gt;\[Fan\]

\[Engine\]-impacted by&gt;\[PowerSupply\]

\[Engine\]-impacted by&gt;\[VplexDevice\]

\[Fan\]-impacts&gt;\[Engine\]

\[Fan\]-impacted by&gt;\[PowerSupply\]

\[PowerSupply\]-impacts&gt;\[Fan\]

\[PowerSupply\]-impacts&gt;\[Engine\]

\[ConsistencyGroup\]-impacted by&gt;\[Cluster\]

\[StorageVolume\]-impacts&gt;\[Lun\]

\[StorageVolume\]-impacted by&gt;\[StorageArray\]

\[VirtualVolume\]-impacted by&gt;\[Extent\]

\[Cluster\]-impacted by&gt;\[VplexDevice\]

\[Cluster\]-impacts&gt;\[StorageArray\]

\[Cluster\]-impacts&gt;\[ConsistencyGroup\]

\[Extent\]-impacts&gt;\[VirtualVolume\]

\[Extent\]-impacted by&gt;\[StorageVolume\]

\[StorageVolume\]-impacts&gt;\[Extent\]

\[Extent\]-impacted by&gt;\[LocalDevice\]

\[LocalDevice\]-impacts&gt;\[Extent\]

\[StorageArray\]-impacts&gt;\[StorageVolume\]

\[StorageArray\]-impacted by&gt;\[Cluster\]

\[Lun\]-impacted by&gt;\[StorageVolume\]

## Changelog

-   1.1.0
    -   Add REST based modeling and monitoring.



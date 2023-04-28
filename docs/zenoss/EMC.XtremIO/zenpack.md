# Dell EMC XtremIO (Commercial)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Name:

ZenPacks.zenoss.EMC.XtremIO

### Applications Monitored:

[Dell/EMC XtremIO Storage Platform](https://www.dellemc.com/en-us/storage/xtremio-all-flash.htm){.external-link}

### Devices Monitored:

[Dell/EMC XtremIO Storage Platform](https://www.dellemc.com/en-us/storage/xtremio-all-flash.htm){.external-link}

## Dell EMC XtremIO ZenPack

The EMC XtremIO ZenPack adds support for monitoring Dell EMC XtremIO
storage management clusters.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 1.0.1- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2018/10/30:   Compatible with Zenoss 5.3.x - 6.2.x and Zenoss Cloud:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},
    [ZenPackLib ZenPack     (&gt;=2.0.9){.external-link}](https://help.zenoss.com/display/in/ZenPackLib "ZenPack:ZenPackLib"){.external-link}

Version 1.0.0- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2018/03/30:   Compatible with Zenoss 5.0.x - 6.1.x:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},
    [ZenPackLib ZenPack     (&gt;=2.0.9){.external-link}](https://help.zenoss.com/display/in/ZenPackLib "ZenPack:ZenPackLib"){.external-link}

## Background

The EMC XtremIO ZenPack provides support for monitoring the Dell EMC
XtremIO storage platform. Discovery and monitoring are performed over
HTTP using the XtremIO XMS HTTP REST API, which provides discovery and
monitoring functionality.  The EMC XtremIO ZenPack supports X1 and X2
series arrays running XIOS v4.0.x and higher via the RESTful API v2.0.x
and higher (via the XMS).

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below. - Simple provisioning for XtremIO
environment using the XMS' IP address, port, and credentials - Robust
support for XMS HTTP API (version 2 and above) - Event management and
monitoring - Optional service impact with addition of Zenoss Service
Dynamics product - Optional Capacity Thresholds with addition of Zenoss
Capacity ZenPack

### Discovery

The following components will be automatically discovered through the
XtremIO XMS IP address, port and credentials you provide. The properties
and relationships will be continually updated on Zenoss' normal
remodeling interval which defaults to every 12 hours. Some components
are updated on a more frequent basis (hourly by default).

XtremIO XMS:   Attributes: Name, Build Number, DB Version, XMS Version, SW Version,
    XMS Name:   Relationships: Tags, Cluster

Cluster:   Attributes: Name, NAA System ID, Software Version, Serial Number,
    Product Part Number, Shared Memory, Severity:   Relationships: X-Brick, Fibre Channel Switch, iSCSI Portal, Data
    Protection Group, Consistency Group, Initiator, Initiator Group,
    Target, Target Group, Volume, Snapshot, Snapshot Set, Scheduler,
    XtremIO XMS, Tag

X-Brick:   Attributes: Name, Severity:   Relationships: Cluster, Battery Backup, Storage Controller, DAE, Tag

Fibre Channel Switch:   Attributes: Name, FW Version, Enabled Status, Model Name, Serial
    Number, FRU Status, Hardware Revision, Part Number, Severity:   Relationships: Cluster, Fibre Channel Port, Fibre Channel Temp
    Sensor, Fibre Channel Voltage Sensor, Tags, targetPorts

Fibre Channel Port:   Attributes: Name, Switch Index, Result Key, Enabled Status, Result
    Index:   Relationships: Fibre Channel Switch, Port Target

Fibre Channel Temp Sensor:   Attributes: Name, Switch Index, Result Key, Result Index:   Relationships: Fibre Channel Switch

Fibre Channel Voltage Sensor:   Attributes: Name, Switch Index, Result Key, Result Index:   Relationships: Fibre Channel Switch

Consistency Group:   Attributes: Name, Severity:   Relationships: Cluster, Snapshot Set, Volume, Tag

Data Protection Group:   Attributes: Name, Severity:   Relationships: Cluster, SSD, Storage Controller, Tag

Initiator:   Attributes: Name, Severity:   Relationships: Cluster, Initiator Group, Tag

Initiator Group:   Attributes: Name, Severity:   Relationships: Cluster, Initiator, Target Group, Volume, Tag

iSCSI Portal:   Attributes: Name, Severity:   Relationships: Cluster, Target, Tag

Scheduler:   Attributes: Name, Enabled Status, Scheduler Type, Snapshot Type,
    Severity:   Relationships: Cluster, Tag

Snapshot:   Attributes: Name, Creation Time, Logical Block Size, NAA Name,
    Volume Access, Volume Size, Volume Type, Severity:   Relationships: Cluster, Volume, Snapshot Set, Tag

Snapshot Set:   Attributes: Name, Severity:   Relationships: Cluster, Snapshot, Consistency Group, Tag

Target:   Attributes: Name, Driver Version, FW Version, MTU, Port Address,
    Port Index, Port MAC Address, Port Speed, Port Type, Severity:   Relationships: Cluster, Target Group, iSCSI Portal, Tag

Target Group:   Attributes: Name, Severity:   Relationships: Cluster, Target, Volume, Initiator Group, Tag

Volume:   Attributes: Name, Logical Block Size, NAA Name, Volume Access, Type,
    Size, Severity:   Relationships: Cluster, Target Group, Initiator Group, Snapshot,
    Consistency Group, Tag

Battery Backup:   Attributes: Name, Fimware Version, Enabled, Model Name, Serial
    Number, FRU Status, Enabled Status, Hardware Revision, Part Number,
    Severity:   Relationships: X-Brick, Tag

DAE:   Attributes: Name, Model Name, Serial Number, FRU Status, Enabled
    Status, Hardware Revision, Part Number, Severity:   Relationships: DAE Controller, DAE PSU, Slot, SSD, X-Brick,
    xtremIoTags

DAE Controller:   Attributes: Name, Location, Model Name, Serial Number, FRU Status,
    Enabled Status, Hardware Revision, Part Number, Severity:   Relationships: DAE, Tag

DAE PSU:   Attributes: Name, Fimware Version, Location, Model Name, Serial
    Number, FRU Status, Enabled Status, Hardware Revision, Part Number,
    Severity:   Relationships: DAE, Tag

Local Disk:   Attributes: Name, Encryption Status, Local Disk Purpose, Local Disk
    Type, Local Disk UID, Model Name, Serial Number, FRU Status, Enabled
    Status, Hardware Revision, Part Number, Severity:   Relationships: Storage Controller, Tag

Slot:   Attributes: Name, Product Model, Slot, State, Severity:   Relationships: DAE, SSD, Tag

Storage Controller:   Attributes: Name, BIOS Version, FC HBA FW Version, FC HBA HW
    Revision, FC HBA Model, IPMI Port Speed, IPMI Address, IPMI Subnet,
    IPMI BMC FW Version, IPMI BMC HW Revision, IPMI BMC Model, IPMI
    Gateway IP, Local Disk Ctrl FW Version, Local Disk Ctrl HW Revision,
    Local Disk Ctrl Model, Management Gateway IP, Management Port
    Duplex, Management Port Speed, Node GUID, SC Manager Address, SC
    Manager Subnet, OS Version, Model Name, Serial Number, FRU Status,
    Enabled Status, Hardware Revision, Part Number, Severity:   Relationships: X-Brick, Storage Controller PSU, Local Disk, XEnv,
    Data Protection Group, Fibre Channel Port, Tag

Storage Controller PSU:   Attributes: Name, Location, Input, Model Name, Serial Number, FRU
    Status, Enabled Status, Hardware Revision, Part Number, Severity:   Relationships: Storage Controller, Tag

SSD:   Attributes: Name, Slot Number, Fimware Version, UUID, Size, Model
    Name, Serial Number, FRU Status, Enabled Status, Hardware Revision,
    Part Number, Severity:   Relationships: DAE, Slot, Data Protection Group, Tag

XEnv:   Attributes: Name, Severity:   Relationships: Storage Controller, Tag

Tag:   Attributes: Name, Caption, Object Type:   Relationships: Parent Tag, XtremIO XMS, Tagged Object

### Monitoring

The following metrics will be collected every 5 minutes by default. The
average statistic is collected, and the graphed value is per second for
anything that resembles a rate. Each metric name corresponds with the
descriptions given in the XMS documentation (available from EMC), with
the exception that "\_" (underscore) characters is used by Zenoss where
"-" (hyphen) is used by the XMS API

XtremIoXMS:   Metrics: iops, ram_usage, logical_space_in_use, rd_iops, logs_size,
    obj_severity, vol_size, wr_latency, thin_provisioning_savings,
    wr_bw, ssd_space_in_use, bw, wr_iops, ram_total,
    overall_efficiency_ratio, avg_latency, rd_bw, ssd_size_in_kb,
    rd_latency, cpu

XtremIoCluster:   Metrics: avg_latency_256kb, rd_iops_4kb, rd_iops_128kb, iops,
    rd_bw_512kb, dedup_ratio, wr_iops_512b, unaligned_wr_iops,
    rd_iops_32kb, rd_iops_64kb, wr_latency_512kb, wr_latency,
    ud_ssd_space, rd_bw_1kb, acc_num_of_small_rd, rd_iops_1mb,
    wr_bw_64kb, data_reduction_ratio, unaligned_wr_bw, rd_iops_2kb,
    wr_bw_16kb, avg_latency_1kb, acc_size_of_wr, small_wr_bw,
    rd_latency_512b, wr_iops_16kb, logical_space_in_use, rd_bw_128kb,
    wr_latency_1kb, acc_num_of_unaligned_wr, wr_bw_32kb,
    rd_latency_256kb, rd_iops_gt1mb, avg_latency_512b, vol_size,
    wr_latency_8kb, wr_bw_1kb, thin_provisioning_savings,
    rd_latency_1kb, wr_latency_512b, rd_iops_512kb, ssd_size_in_kb,
    small_wr_iops, rd_bw_256kb, avg_latency_4kb, wr_iops_256kb,
    thin_provisioning_ratio, wr_iops, wr_bw_512b, acc_size_of_rd,
    wr_iops_gt1mb, rd_latency, rd_iops_16kb, avg_latency_2kb,
    rd_latency_128kb, avg_latency_8kb, rd_latency_512kb, rd_bw_1mb,
    avg_latency_1mb, rd_iops_256kb, rd_bw_gt1mb, rd_iops_1kb,
    ssd_space_in_use, bw, small_iops, acc_num_of_rd, rd_bw_4kb,
    wr_iops_2kb, wr_latency_1mb, rd_bw_2kb, wr_iops_4kb,
    avg_latency_gt1mb, wr_bw_1mb, small_rd_bw, wr_latency_4kb,
    unaligned_rd_bw, wr_latency_2kb, acc_num_of_unaligned_rd,
    acc_num_of_wr, avg_latency, wr_bw_gt1mb, ud_ssd_space_in_use,
    rd_latency_16kb, avg_latency_16kb, rd_latency_8kb,
    unaligned_rd_iops, rd_iops_512b, wr_latency_32kb, wr_bw_256kb,
    avg_latency_64kb, wr_iops_1kb, wr_iops_64kb, rd_bw_8kb, wr_iops_8kb,
    unaligned_iops, rd_bw, avg_latency_32kb,
    total_memory_in_use_in_percent, wr_latency_64kb, wr_latency_16kb,
    wr_iops_32kb, free_ud_ssd_space_in_percent, small_bw,
    compression_factor, acc_num_of_small_wr, wr_bw, rd_latency_2kb,
    wr_latency_256kb, rd_latency_64kb, obj_severity,
    total_memory_in_use, wr_bw_512kb, rd_latency_gt1mb, rd_bw_32kb,
    wr_bw_4kb, avg_latency_128kb, small_rd_iops,
    useful_ssd_space_per_ssd, wr_iops_512kb, rd_bw_64kb,
    space_saving_ratio, rd_bw_16kb, wr_iops_128kb, wr_bw_2kb, wr_bw_8kb,
    rd_bw_512b, unaligned_bw, rd_latency_4kb, rd_iops_8kb,
    avg_latency_512kb, wr_latency_128kb, rd_iops, wr_bw_128kb,
    rd_latency_32kb, wr_iops_1mb, dedup_space_in_use, space_in_use,
    rd_latency_1mb, wr_latency_gt1mb

XtremIoFibreChannelSwitch:   Metrics: fan_1\_rpm, fan_4\_rpm, obj_severity, fan_3\_rpm,
    enabled_state, fru_lifecycle_state, fan_2\_rpm

XtremIoDataProtectionGroup:   Metrics: ud_ssd_space_in_use, rd_iops, iops, ssd_size, obj_severity,
    useful_ssd_space, bw, wr_iops, wr_bw, ud_ssd_space, rd_bw

XtremIoInitiator:   Metrics: acc_num_of_unaligned_rd, wr_iops, acc_num_of_wr, iops,
    acc_size_of_rd, avg_latency, rd_latency, unaligned_wr_iops,
    small_rd_iops, unaligned_rd_iops, wr_latency, acc_num_of_small_rd,
    unaligned_wr_bw, acc_size_of_wr, small_wr_bw, bw, small_iops,
    acc_num_of_rd, rd_bw, unaligned_bw, acc_num_of_unaligned_wr,
    obj_severity, rd_iops, small_rd_bw, small_bw, unaligned_iops,
    acc_num_of_small_wr, wr_bw, unaligned_rd_bw, small_wr_iops

XtremIoInitiatorGroup:   Metrics: acc_num_of_unaligned_rd, wr_iops, acc_num_of_wr, iops,
    acc_size_of_rd, unaligned_wr_iops, small_rd_iops, unaligned_rd_iops,
    acc_num_of_small_rd, unaligned_wr_bw, acc_size_of_wr, small_wr_bw,
    bw, small_iops, acc_num_of_rd, rd_bw, unaligned_bw,
    acc_num_of_unaligned_wr, obj_severity, rd_iops, small_rd_bw,
    small_bw, unaligned_iops, acc_num_of_small_wr, wr_bw,
    unaligned_rd_bw, small_wr_iops

XtremIoSnapshot:   Metrics: acc_num_of_unaligned_rd, wr_iops, acc_num_of_wr, iops,
    acc_size_of_rd, avg_latency, rd_latency, unaligned_wr_iops,
    obj_severity, small_rd_iops, unaligned_io_ratio, unaligned_rd_iops,
    wr_latency, acc_num_of_small_rd, wr_bw, unaligned_wr_bw,
    acc_size_of_wr, small_wr_bw, bw, small_iops, acc_num_of_rd, rd_bw,
    unaligned_bw, acc_num_of_unaligned_wr, logical_space_in_use,
    rd_iops, vol_size, small_rd_bw, small_bw, unaligned_iops,
    acc_num_of_small_wr, small_io_ratio, unaligned_rd_bw, small_wr_iops

XtremIoTarget:   Metrics: acc_num_of_unaligned_rd, eth_pkt_tx, wr_iops,
    acc_num_of_wr, fc_dumped_frames, iops, acc_size_of_rd,
    fc_loss_of_signal_count, avg_latency, rd_latency, unaligned_wr_iops,
    fc_seq_retx_req_count, small_rd_iops, fc_prim_seq_prot_err_count,
    eth_pkt_tx_error, unaligned_rd_iops, wr_latency,
    acc_num_of_small_rd, unaligned_wr_bw, fc_link_failure_count,
    acc_size_of_wr, small_wr_bw, fc_loss_of_sync_count, bw, small_iops,
    acc_num_of_rd, rd_bw, eth_kbytes_tx, unaligned_bw, eth_kbytes_rx,
    eth_pkt_rx_crc_error, acc_num_of_unaligned_wr, obj_severity,
    rd_iops, eth_pkt_rx_no_buffer_error, small_rd_bw, small_bw,
    fc_invalid_crc_count, unaligned_iops, acc_num_of_small_wr, wr_bw,
    eth_pkt_rx, unaligned_rd_bw, small_wr_iops

XtremIoTargetGroup:   Metrics: obj_severity

XtremIoVolume:   Metrics: acc_num_of_unaligned_rd, wr_iops, acc_num_of_wr, iops,
    acc_size_of_rd, avg_latency, rd_latency, unaligned_wr_iops,
    obj_severity, small_rd_iops, unaligned_rd_iops, wr_latency,
    acc_num_of_small_rd, unaligned_wr_bw, acc_size_of_wr, small_wr_bw,
    bw, small_iops, acc_num_of_rd, rd_bw, unaligned_bw,
    acc_num_of_unaligned_wr, logical_space_in_use, rd_iops, vol_size,
    small_rd_bw, small_bw, unaligned_iops, acc_num_of_small_wr, wr_bw,
    unaligned_rd_bw, small_wr_iops

XtremIoBatteryBackup:   Metrics: input_frequency, ups_load_in_percent, battery_runtime,
    power, avg_daily_temp, battery_voltage, obj_severity, enabled_state,
    real_power, output_frequency, output_voltage, output_current,
    ups_battery_charge_in_percent, fru_lifecycle_state, ups_voltage

XtremIoDAEController:   Metrics: sas2_last_24h_number_of_phy_problems, enabled_state,
    sas1_last_24h_number_of_phy_problems, fru_lifecycle_state,
    obj_severity

XtremIoLocalDisk:   Metrics: enabled_state, num_bad_sectors, fru_lifecycle_state,
    obj_severity

XtremIoStorageController:   Metrics: sas1_last_24h_number_of_phy_problems,
    ib1_last_24h_number_of_port_problems, obj_severity,
    ib2_local_link_integrity_errors,
    ib1_excessive_buffer_overrun_errors,
    ib2_port_rcv_remote_physical_errors, enabled_state,
    ib1_last_24h_number_of_port_faults,
    ib2_excessive_buffer_overrun_errors, ib1_port_rcv_errors,
    ib2_symbol_errors, ib1_port_rcv_remote_physical_errors,
    ib2_link_error_recoveries, sas2_last_24h_number_of_phy_problems,
    ib2_last_24h_number_of_port_problems, ib2_link_downed,
    ib2_port_rcv_errors, ib1_local_link_integrity_errors,
    ib1_link_error_recoveries, ib1_symbol_errors,
    ib2_last_24h_number_of_port_faults, dimm_correctable_errors,
    ib1_link_downed, fru_lifecycle_state

XtremIoSSD:   Metrics: obj_severity, rd_iops, percent_endurance_remaining,
    wr_iops, wr_bw, ssd_space_in_use, iops, bw, enabled_state, rd_bw,
    ssd_size_in_kb, num_bad_sectors, fru_lifecycle_state

XtremIoXenv:   Metrics: cpu_usage, obj_severity

XtremIoStorageControllerPSU:   Metrics: enabled_state, fru_lifecycle_state, obj_severity

XtremIoDAEPSU:   Metrics: enabled_state, fru_lifecycle_state, obj_severity

XtremIoDAE:   Metrics: ssd_space_in_use, ssd_size_in_kb, fru_lifecycle_state,
    obj_severity

XtremIoScheduler:   Metrics: enabled_state

XtremIoConsistencyGroup:   Metrics: obj_severity

XtremIoConsistencyGroupVolume:   Metrics: obj_severity

XtremIoBrick:   Metrics: ssd_space_in_use, ssd_size_in_kb, obj_severity

XtremIoSwitchTempSensor:   Metrics: temperature

XtremIoSwitchVoltSensor:   Metrics: volts

XtremIoSwitchPort:   Metrics: status

### Event Management

A monitoring plugin collects events detected by the XMS and mirrors
events displayed in the XMS administration interface.

### Service Impact

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact and root cause analysis capabilities for
services running on EMC XtremIO. The service impact relationships shown
in the diagram and described below are automatically added. These will
be included in any services that contain one or more of the explicitly
mentioned components.

Service Impact Relationships

-   XtremIoXMS impacted by related XtremIoCluster
-   XtremIoCluster impacted by related XtremIoBrick,
    XtremIoFibreChannelSwitch, XtremIoConsistencyGroup,
    XtremIoISCSIPortal, XtremIoDataProtectionGroup, XtremIoInitiator,
    XtremIoInitiatorGroup, XtremIoTarget, XtremIoTargetGroup,
    XtremIoSnapshot, XtremIoSnapshotSet, XtremIoScheduler, XtremIoVolume
-   XtremIoBrick impacted by related XtremIoBatteryBackup,
    XtremIoStorageController, XtremIoDAE
-   XtremIoDAE impacted by related XtremIoSSD, XtremIoSlot,
    XtremIoDAEController, XtremIoDAEPSU
-   XtremIoStorageController impacted by related
    XtremIoStorageControllerPSU, XtremIoLocalDisk, XtremIoXenv,
    XtremIoSwitchPort
-   XtremIoFibreChannelSwitch impacted by related XtremIoSwitchPort,
    XtremIoSwitchTempSensor, XtremIoSwitchVoltSensor
-   XtremIoInitiatorGroup impacted by related XtremIoInitiator,
    XtremIoVolume
-   XtremIoTargetGroup impacted by related XtremIoTarget, XtremIoVolume
-   XtremIoSSD impacted by related XtremIoSlot
-   XtremIoDataProtectionGroup impacted by related XtremIoSSD,
    XtremIoStorageController
-   XtremIoTarget impacted by related XtremIoISCSIPortal
-   XtremIoConsistencyGroup impacted by related XtremIoVolume
-   XtremIoSnapshotSet impacted by related XtremIoSnapshot

Note: Relations to external systems like Linux, Windows, and vSphere
require updated versions of the related ZenPacks.

### Capacity ZenPack Thresholds

This ZenPack contains several thresholds that can be used with the
Capacity ZenPack. Install order doesn't matter, but the Capacity
thresholds will not be loaded unless the Capacity ZenPack is installed
before or after the XtremIO ZenPack.

## Usage

### Adding XtremIO Devices

Use the following steps to start monitoring an XtremIO environment using
the Zenoss web interface.

1.  Navigate to Infrastructure tab in the Zenoss web interface
2.  Select the /Devices/Storage/EMC/XtremIO device class
3.  Optionally Select the "Details" link, followed by "Configuration
    Properties". Type "XtremIo" into the "Name" column filter and edit
    the relevant zProperties
4.  Select the "Add Single Device" or "Add Multiple Devices" option from
    the Add Device drop-down menu
5.  Provision the "Name or IP" field with the XMS IP Address
6.  Click *Add*.
7.  A device representing the XMS will be added to the
    /Devices/Storage/EMC/XtremIO device class
8.  After modeling, the title of the XMS will reflect the configured XMS
    name.
9.  If device is not automatically modeled, check that the values of
    zProperties beginning with "zXtremIo..." are appropriate

### Command Line Tools

Several scripts are included for use with troubleshooting or sample data
collection. These scripts reside in the

$ZENPACK/ZenPacks/zenoss/EMC/XtremIO/utilities

directory and calling --help will display usage information for each. -
get-object.py (Performs a single query against the remote API endpoint)
- list-objects.py (Performs a walk (multiple "list" queries) against the
remote API endpoint)

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

Device Classes

-   /Storage/EMC/XtremIO

Configuration Properties

-   zEMCXtremIoUser
-   zEMCXtremIoPassword
-   zEMCXtremIoUseSSL
-   zEMCXtremIoHttpPort
-   zEMCXtremIoHttpTimeout
-   zEMCXtremIoPoolSize
-   zEMCXtremIoApiVersion
-   zEMCXtremIoCollectionInterval

Modeler Plugins

-   EMC.XtremIO.http.XMSMap

Datasource Types

-   XtremIO Datasource (HTTP)
-   XtremIO Events Datasource (HTTP)
-   XtremIO Modeler Datasource (HTTP)

Monitoring Templates

-   XtremIoXMS
-   XtremIoCluster
-   XtremIoFibreChannelSwitch
-   XtremIoDataProtectionGroup
-   XtremIoInitiator
-   XtremIoInitiatorGroup
-   XtremIoSnapshot
-   XtremIoTarget
-   XtremIoTargetGroup
-   XtremIoVolume
-   XtremIoBatteryBackup
-   XtremIoDAEController
-   XtremIoLocalDisk
-   XtremIoStorageController
-   XtremIoSSD
-   XtremIoXenv
-   XtremIoTag
-   XtremIoStorageControllerPSU
-   XtremIoSlot
-   XtremIoDAEPSU
-   XtremIoDAE
-   XtremIoSnapshotSet
-   XtremIoISCSIPortal
-   XtremIoScheduler
-   XtremIoConsistencyGroup
-   XtremIoConsistencyGroupVolume
-   XtremIoBrick
-   XtremIoSwitchTempSensor
-   XtremIoSwitchVoltSensor
-   XtremIoSwitchPort

Device Types

-   XMSDevice (in /Storage/EMC/XtremIO)

Component Types

-   Cluster
-   X-Brick
-   Fibre Channel Switch
-   Fibre Channel Port
-   Fibre Channel Temp Sensor
-   Fibre Channel Voltage Sensor
-   Consistency Group
-   Data Protection Group
-   Initiator
-   Initiator Group
-   iSCSI Portal
-   Scheduler
-   Snapshot
-   Snapshot Set
-   Target
-   Target Group
-   Volume
-   Battery Backup
-   DAE
-   DAE Controller
-   DAE PSU
-   Local Disk
-   Slot
-   Storage Controller
-   Storage Controller PSU
-   SSD
-   XEnv
-   Tag

Event Classes

-   /XtremIO/Status
-   /XtremIO/Perf

## Required Daemons

Modeler:

-   zenmodeler

Performance Collector:

-   zenpython

## Upgrade

The EMC XtremIO Zenpack can be upgraded. To upgrade the ZenPack, install
the latest version over the existing one. There is no action for the
user to migrate the data. The performance data and events of old ZenPack
are retained as per the retain policy settings.

## Limitations

## Known Issues

### Known Issue when importing xtremio-bundle.zip into Analytics

Due to the large amount of data available for export, the Analytics
server database (MySQL) may require a configuration change prior to
importing the xtremio-bundle.zip file. To prevent this issue, execute
the following commands on the analytics server:

-   echo "max_allowed_packet=100M" &gt;&gt; /etc/my.cnf
-   /etc/init.d/mysql restart

Symptoms of this issue include a GUI flare message containing:

"Import failed. Reason: Could not roll back Hibernate transaction;
nested exception is org.hibernate.TransactionException: JDBC rollback
failed"

## Changes

**1.0.1**

-   Maintenance release.
-   Updated icons for better theme compatibility
-   Revised Alert monitoring to mirror XMS UI Alerts (ZPS-4430)
-   Allow custom device title (ZPS-3807)
-   Compatible with Zenoss 5.3.3 - 6.2 and Zenoss Cloud: Incompatible
    with Zenoss Resource Manager 4.x

**1.0.0**

-   Initial release.
-   Tested with Zenoss Resource Manager 5.2.5, Zenoss Resource Manager
    5.3.3, Zenoss Resource Manager 6.1.2, Service Impact Service Impact
    5.2.3 and Analytics 5.1.0

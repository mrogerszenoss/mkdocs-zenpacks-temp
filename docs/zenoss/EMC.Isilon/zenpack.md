# Dell EMC Isilon (Commercial)

@lb[](img/zenpack-emc-zenpack.png)

## Dell EMC Isilon ZenPack

The Dell EMC Isilon ZenPack adds support for monitoring Dell EMC Isilon
storage management clusters.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 1.1.0 - [Download](https://delivery.zenoss.com){.external-link}:   Released 2022/03/17:   Requires [PythonCollector ZenPack](https://www.zenoss.com/product/zenpacks/pythoncollector){.external-link},
    [ZenPackLib ZenPack](https://www.zenoss.com/product/zenpacks/product/zenpacks/zenpacklib){.external-link}
    (&gt;=2.0.6), [CalculatedPerformance ZenPack](https://www.zenoss.com/product/zenpacks/calculated-performance){.external-link}:   Tested with Zenoss Cloud, Zenoss 6.6.0 and Service Impact 5.5.5

Version 1.0.4 - [Download](https://delivery.zenoss.com){.external-link}:   Released 2021/04/09:   Requires [PythonCollector ZenPack](https://www.zenoss.com/product/zenpacks/pythoncollector){.external-link},
    [ZenPackLib ZenPack](https://www.zenoss.com/product/zenpacks/product/zenpacks/zenpacklib){.external-link}
    (&gt;=2.0.6), [CalculatedPerformance ZenPack](https://www.zenoss.com/product/zenpacks/calculated-performance){.external-link}:   Tested with Zenoss Cloud, Zenoss 6.5.0, Zenoss 6.4.1 and Service
    Impact 5.5.3

Version 1.0.3 - [Download](https://delivery.zenoss.com){.external-link}:   Released 2020/11/16:   Requires [PythonCollector ZenPack](http://help.zenoss.com/display/in/PythonCollector){.external-link},
    [ZenPackLib ZenPack](http://help.zenoss.com/display/in/ZenPackLib){.external-link}
    (&gt;=2.0.6), [CalculatedPerformance ZenPack](http://help.zenoss.com/display/in/Calculated+Performance){.external-link}

    Compatible with Zenoss Cloud and Zenoss 6.5 with Service Impact
    5.5.2

Version 1.0.0 - [Download](https://delivery.zenoss.com){.external-link}:   Released 2017/08/15:   Requires [PythonCollector ZenPack](http://help.zenoss.com/display/in/PythonCollector){.external-link},
    [ZenPackLib ZenPack](http://help.zenoss.com/display/in/ZenPackLib){.external-link}
    (&gt;=2.0.6), [CalculatedPerformance ZenPack](http://help.zenoss.com/display/in/Calculated+Performance){.external-link}:   Compatible with Zenoss 4.2 - 5.2

## Contents

-   [Background](#background)
-   [Features](#features)
    -   [Discovery](#discovery)
    -   [Monitoring](#monitoring)
    -   [Event Management](#event-management)
    -   [Service Impact](#service-impact)
-   [Usage](#usage)
    -   [Adding Isilon Clusters](#adding-isilon-clusters)
    -   [Configuring optional SNMP Monitoring](#configuring-optional-snmp-monitoring)
    -   [Configuring Debug Mode](#configuring-debug-mode)
    -   [Command Line Tools](#command-line-tools)
    -   [Isilon Cluster Networking Considerations](#isilon-cluster-networking-considerations)
    -   [OneFS API Minimally Privileged User](#one-fsapi-minimally-privileged-user)
-   [Installed Items](#installed-items)
-   [Required Daemons](#required-daemons)
-   [Upgrade](#upgrade)
-   [Limitations](#limitations)
-   [Known Issues](#known-issues)
-   [Changes](#changes)

## [Background](#contents)

The EMC Isilon ZenPack provides support for monitoring the Dell EMC
Isilon storage platform. Discovery and monitoring are performed over
HTTP using Isilon OneFS HTTP API, which provides the bulk of the
discovery and monitoring functionality.

SNMP is optionally supported as well, although the scope of data
available via SNMP is fairly limited by comparison.

## [Features](#contents)

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Simple provisioning for each Isilon cluster using IP address, port,
    and credentials
-   Auto-discovery of node devices via cluster modeling
-   Limited support for SNMP discovery and monitoring
-   Robust support for OneFS HTTP API
-   Event management and monitoring
-   Optional service impact with addition of Zenoss Service Dynamics
    product
-   Optional debug mode provides analysis of OneFS API utilization

### [Discovery](#contents)

The following components will be automatically discovered through the
Isilon Cluster IP address, port and credentials you provide. The
properties and relationships will be continually updated on Zenoss'
normal remodeling interval which defaults to every 12 hours.

IsilonCluster:   Attributes: Node Count, Cluster State, Description, Encoding, Has
    Quorum, Compliance Mode, Virtual, vOneFS ESXi, Join Mode, Cluster
    IP, Cluster ID:   Relationships: Endpoint, Quota, License, File Pool, Access Zone,
    Flexnet Pool, GroupNet, SubNet, Rule, Cluster Node, Protocol, SMB
    Share, NFS Export, NTP Server, NDMP Context, NDMP User, NDMP
    Session, HDFS Proxy User, HDFS Rack, SmartPool Tier, SmartPool Node,
    Cloud Pool, CloudAccount, Cloud Policy

IsilonNode:   Attributes: Cluster ID, Node Name, Node Type, Node State, Local
    Device ID, Logical Node Number, Serial Number, Node Config ID,
    Description, Isilon Product Name, OneFS Build Version, Cluster:   Relationships: Cluster Node, Fiber Channel Ports, ZenModel
    (platform) component relationships

NodeComponent:   Attributes: Description, Node Device, LNN, Serial Number, Node
    Config ID, Isilon Product Name, OneFS Build Version:   Relationships: Isilon Cluster, Isilon Node, SmartPool Node,
    SmartPool Tier

SmartTierPool:   Attributes: Tier ID, Auto IO Optimize, Auto Manage Protection,
    Namespace Accel Enabled, Additional Directory Protection, Spillover
    Enabled, Spillover Target, Virtual Hot Spare Write Deny, Hot Spare
    Space Hidden, Hot Spare Reserved Drives, Hot Spare Limit Percent:   Relationships: Isilon Cluster, SmartPool Node, Cluster Node

SmartNodePool:   Attributes: L3 Cache Enabled, L3 Status, Manual, Protection Policy,
    Auto IO Optimize, Auto Manage Protection, Namespace Accel Enabled,
    Additional Directory Protection, Spillover Enabled, Spillover
    Target, Virtual Hot Spare Write Deny, Hot Spare Space Hidden, Hot
    Spare Reserved Drives, Hot Spare Limit Percent:   Relationships: Isilon Cluster, SmartPool Tier, Cluster Node

Quota:   Attributes: Type, Enforced, Snapshots, Container, Linked,
    Notifications, Threshold Includes Overhead, Ready:   Relationships: Isilon Cluster

License:   Attributes: Duration, Expiration, License Status:   Relationships: Isilon Cluster

FilePool:   Attributes: Default Policy:   Relationships: Isilon Cluster

AccessZone:   Attributes: Use Available Auth, Alternate Provider, Cache Size,
    Create Path, HDFS Authentication, HDFS Kerberos Keytab, HDFS Root
    Directory, Home Directory Umask, NetBIOS Name, Directory Path,
    Protocol Audit Enabled, Skeleton Directory, System Provider, WebHDFS
    Enabled, Zone ID:   Relationships: Isilon Cluster, GroupNet, Flexnet Pool

FlexnetPool:   Attributes: Description, Rebalance Policy, Unsuspend Delay, Connect
    Policy, Failover Policy:   Relationships: Isilon Cluster, SubNet, Access Zone, GroupNet,
    Interface, Rule

GroupNet:   Attributes: Name:   Relationships: Isilon Cluster, Access Zone, SubNet, Flexnet Pool,
    Interface, Rule, IP Service

SubNet:   Attributes: Name:   Relationships: Isilon Cluster, Flexnet Pool, GroupNet, Interface,
    Rule

NetworkRule:   Attributes: Description, Node Type:   Relationships: Isilon Cluster, Cluster Interface, GroupNet, SubNet,
    Flexnet Pool

Protocol:   Attributes: Description, Protocol:   Relationships: SMB Share, NFS Export, NTP Server, NDMP Context, NDMP
    User, NDMP Session, HDFS Proxy User, HDFS Rack, Isilon Cluster

SMBShare:   Attributes: Share Path:   Relationships: Isilon Cluster, Protocol

NFSExport:   Attributes: Name:   Relationships: Isilon Cluster, Protocol

NTPServer:   Attributes: Name:   Relationships: Isilon Cluster, Protocol

NDMPContext:   Attributes: Name:   Relationships: Isilon Cluster, Protocol

NDMPUser:   Attributes: Name:   Relationships: Isilon Cluster, Protocol

NDMPSession:   Attributes: Name:   Relationships: Isilon Cluster, Protocol

HDFSProxyUser:   Attributes: Name:   Relationships: Isilon Cluster, Protocol

HDFSRack:   Attributes: Name:   Relationships: Isilon Cluster, Protocol

StorageEnclosure:   Attributes: Configuration, Serial number, Model:   Relationships: Isilon Node

FiberChannelPort:   Attributes: Logical Network Node, Port ID, WWN, WWPN, Topology, Rate:   Relationships: Isilon Node

HardDiskIsilon:   Attributes: Zenoss Reference Attribute, Bay, Logical ID, Chassis ID,
    Device Name, Model, Serial, Firmware, Size:   Relationships: Storage Enclosure

FanModule:   Attributes: description:   Relationships: Storage Enclosure

PowerSupply:   Attributes: Firmware, Type:   Relationships: Storage Enclosure

TemperatureSensor:   Attributes: description:   Relationships: Storage Enclosure

ClusterIpInterface:   Attributes: NIC Name, IP Address:   Relationships: Rule, Interface

NodeIpInterface:   Attributes: Logical Node, status_health_value,
    severity_health_value, NIC Name, IP Address:   Relationships: Flexnet Pool, SubNet, GroupNet, Cluster Interface

ClusterIpService:   Attributes: Name, Port:   Relationships: GroupNet

CloudPolicy:   Attributes: Name:   Relationships: Isilon Cluster, Cloud Pool

CloudAccount:   Attributes: Account ID, Account Username, Birth Cluster ID, Cloud
    Protocol:   Relationships: Isilon Cluster, Cloud Pool

CloudPool:   Attributes: Description, Vendor, Birth Cluster ID, Cloud Protocol,
    Auto IO Optimize, Auto Manage Protection, Namespace Accel Enabled,
    Additional Directory Protection, Spillover Enabled, Spillover
    Target, Virtual Hot Spare Write Deny, Hot Spare Space Hidden, Hot
    Spare Reserved Drives, Hot Spare Limit Percent:   Relationships: Isilon Cluster, CloudAccount, Cloud Policy

Endpoint:   Attributes: URI:   Relationships: Isilon Cluster

### [Monitoring](#contents)

The following metrics will be collected every 5 minutes by default. The
average statistic is collected, and the graphed value is per second for
anything that resembles a rate.

IsilonClusterSNMP:   Metrics: nodeCount, clusterHealth, clusterCPUUser, clusterCPUNice,
    clusterCPUSystem, clusterCPUInterupt, clusterCPUIdlePct,
    clusterNetworkInBytes, clusterNetworkOutBytes, clusterIfsInBytes,
    clusterIfsOutBytes, ifsTotalBytes, ifsUsedBytes, ifsAvailableBytes,
    ifsFreeBytes

IsilonClusterDevice:   Metrics: cluster_cpu_count, cluster_cpu_idle_avg,
    cluster_cpu_user_avg, cluster_cpu_sys_avg, cluster_cpu_intr_avg,
    cluster_cpu_nice_avg, cluster_disk_bytes_out_rate,
    cluster_disk_bytes_in_rate

IsilonClusterNetworkTraffic:   Metrics: cluster_net_ext_bytes_in_rate,
    cluster_net_ext_bytes_out_rate, cluster_net_ext_errors_in_rate,
    cluster_net_ext_errors_out_rate, cluster_net_ext_packets_in_rate,
    cluster_net_ext_packets_out_rate, cluster_net_int_bytes_in_rate,
    cluster_net_int_bytes_out_rate, cluster_net_int_errors_in_rate,
    cluster_net_int_errors_out_rate, cluster_net_int_packets_in_rate,
    cluster_net_int_packets_out_rate

IsilonClusterAggregateDisk:   Metrics: filesystemStats, cluster_disk_xfer_size_in,
    cluster_disk_xfer_size_out, cluster_disk_xfers_in_rate,
    cluster_disk_xfers_out_rate

IsilonClusterDeduplication:   Metrics: cluster_dedupe_estimated_deduplicated_bytes,
    cluster_dedupe_estimated_saved_bytes,
    cluster_dedupe_logical_deduplicated_bytes,
    cluster_dedupe_logical_saved_bytes,
    cluster_dedupe_total_physical_bytes, cluster_dedupe_total_used_bytes

IsilonClusterNodes:   Metrics: cluster_node_count_all, cluster_node_count_diskless,
    cluster_node_count_down, cluster_node_count_readonly,
    cluster_node_count_smartfailed, cluster_node_count_up

IsilonNodeDevice:   Metrics: node_uptime, node_cpu_count, node_cpu_idle_avg,
    node_cpu_user_avg, node_cpu_sys_avg, node_cpu_intr_avg,
    node_cpu_nice_avg, node_load_1min, node_load_5min, node_load_15min,
    node_memory_used, node_memory_free,  node_open_files,
    node_process_count, node_disk_bytes_out_rate_avg,
    node_disk_bytes_in_rate_avg, norm_load_1min, norm_load_5min,
    norm_load_15min

IsilonNodeIFS:   Metrics: node_ifs_bytes_deleted_rate, node_ifs_bytes_in_rate,
    node_ifs_bytes_out_rate, node_ifs_files_created_rate,
    node_ifs_files_removed_rate, node_ifs_num_lookups_rate,
    node_ifs_ops_in_rate, node_ifs_ops_out_rate,
    node_ifs_heat_write_total, node_ifs_journal_stats,
    abort_attempted_pct, commit_attempted_pct, flush_attempted_pct,
    btl_drain_attempted_pct, blocks_meta_attempted_pct,
    blocks_data_attempted_pct, drive_replay_attempted_pct,
    prepare_attempted_pct, node_ifs_ssd_bytes_avail,
    node_ifs_ssd_bytes_total

IsilonNodeNetworkTraffic:   Metrics: node_net_ext_bytes_in_rate, node_net_ext_bytes_out_rate,
    node_net_ext_errors_in_rate, node_net_ext_errors_out_rate,
    node_net_ext_packets_in_rate, node_net_ext_packets_out_rate,
    node_net_int_bytes_in_rate, node_net_int_bytes_out_rate,
    node_net_int_errors_in_rate, node_net_int_errors_out_rate,
    node_net_int_packets_in_rate, node_net_int_packets_out_rate

IsilonNodeAggregateDisk:   Metrics: node_disk_access_latency_avg, node_disk_access_slow_avg,
    node_disk_busy_avg, node_disk_iosched_latency_avg,
    node_disk_iosched_queue_avg, node_disk_xfer_size_in_avg,
    node_disk_xfer_size_out_avg, node_disk_xfers_in_rate_avg,
    node_disk_xfers_out_rate_avg

IsilonNodeClients:   Metrics: node_clientstats_active_cifs, node_clientstats_active_ftp,
    node_clientstats_active_hdfs, node_clientstats_active_http,
    node_clientstats_active_irp, node_clientstats_active_jobd,
    node_clientstats_active_lsass_out, node_clientstats_active_nfs,
    node_clientstats_active_nfs3, node_clientstats_active_nfs4,
    node_clientstats_active_nlm, node_clientstats_active_papi,
    node_clientstats_active_siq, node_clientstats_active_smb1,
    node_clientstats_active_smb2, node_clientstats_connected_cifs,
    node_clientstats_connected_ftp, node_clientstats_connected_hdfs,
    node_clientstats_connected_http, node_clientstats_connected_ndmp,
    node_clientstats_connected_nfs, node_clientstats_connected_nlm,
    node_clientstats_connected_papi, node_clientstats_connected_siq,
    node_clientstats_connected_smb

IsilonNodeNFS:   Metrics: svc_counters, v3_counters, v4_counters, ccb, icb,
    replay_tcp, replay_udp, sec_principal, sec_sid, sec_uid_gid,
    sec_username, v4_dircache

IsilonNodeSNMP:   Metrics: nodeHealth, nodeCPUUser, nodeCPUNice, nodeCPUSystem,
    nodeCPUInterrupt, nodeCPUIdle, nodeNetworkInBytes,
    nodeNetworkOutBytes, nodeIfsInBytes, nodeIfsOutBytes

SmartPool:   Metrics: usage

Endpoint:   Metrics: GET, PUT, POST, DELETE, HEAD, UNSUPPORTED

Quota:   Metrics: usage

NodeIpInterface:   Metrics: health, node_net_iface_bytes_in_rate,
    node_net_iface_bytes_out_rate, node_net_iface_packets_in_rate,
    node_net_iface_packets_out_rate, node_net_iface_errors_in_rate,
    node_net_iface_errors_out_rate

Protocol:   Metrics: protostats

ProtocolSNMP:   Metrics: protocolOpCount, inAvgBytes, inStdDevBytes,
    inBitsPerSecond, outAvgBytes, outStdDevBytes, outBitsPerSecond,
    latencyAverage, latencyStdDev

ProtocolSMB:   Metrics: sessions, openfiles

ProtocolHDFS:   Metrics: proxyusers

ProtocolNFS:   Metrics: nlm_locks, nlm_waiters

ProtocolNDMP:   Metrics: sessions

FileSystem:   Metrics: node_sysfs_bytes_avail, node_sysfs_percent_avail,
    availBlocks, usedBlocks

HardDiskIsilon:   Metrics: health, node_disk_xfers_in_rate_all,
    node_disk_xfers_out_rate_all, node_disk_xfer_size_in_all,
    node_disk_xfer_size_out_all, node_disk_bytes_in_rate_all,
    node_disk_bytes_out_rate_all, node_disk_busy_all,
    node_disk_access_latency_all, node_disk_access_slow_all,
    node_disk_iosched_queue_all, node_disk_iosched_latency_all,
    node_disk_ifs_bytes_total_all, node_disk_ifs_bytes_free_all,
    node_disk_ifs_inodes_used_all

HardDiskIsilonSNMP:   Metrics: diskPerfOpsPerSecond, diskPerfInBitsPerSecond,
    diskPerfOutBitsPerSecond

FanModule:   Metrics: node_sensor_fan_rpms

FanModuleSNMP:   Metrics: fanSpeed

PowerSupply:   Metrics: node_sensor_power_watts

PowerSupplySNMP:   Metrics: powerSensorValue

TemperatureSensor:   Metrics: node_sensor_temp_celsius

TemperatureSensorSNMP:   Metrics: tempSensorValue

### [Event Management](#contents)

A monitoring plugin collects events detected by the Isilon cluster and
mirror events displayed in the OneFS HTTP web interface.

### [Service Impact](#contents)

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact and root cause analysis capabilities for
services running on EMC Isilon. The service impact relationships shown
in the diagram and described below are automatically added. These will
be included in any services that contain one or more of the explicitly
mentioned components.

Service Impact Relationships

-   IsilonCluster impacts related Quota, License, FilePool, AccessZone,
    FlexnetPool, GroupNet, SubNet, NetworkRule, SmartTierPool,
    SmartNodePool, CloudPool
-   IsilonCluster impacts related CloudAccount, CloudPolicy, Protocol,
    Endpoint
-   IsilonNode impacts related IsilonCluster, NodeComponent,
    SmartNodePool, SmartTierPool, NodeIpInterface, StorageEnclosure,
    FileSystem, FiberChannelPort
-   StorageEnclosure impacts related FanModule, HardDiskIsilon,
    PowerSupply, TemperatureSensor
-   SmartTierPool impacts related NodeComponent, SmartNodePool
-   SmartNodePool impacts related NodeComponent
-   AccessZone impacts related GroupNet, FlexnetPool
-   NetworkRule impacts related FlexnetPool, GroupNet
-   GroupNet impacts related FlexnetPool
-   SubNet impacts related FlexnetPool
-   NodeIpInterface impacts related FlexnetPool, GroupNet
-   FlexnetPool impacts related GroupNet
-   GroupNet impacts related SubNet
-   NetworkRule impacts related SubNet
-   NodeIpInterface impacts related SubNet
-   NetworkRule impacts related ClusterIpInterface
-   Protocol impacts related SMBShare, NFSExport, NTPServer,
    NDMPContext, NDMPUser, NDMPSession, HDFSProxyUser, HDFSRack
-   NodeIpInterface impacts related ClusterIpInterface
-   ClusterIpInterface impacts related Protocol
-   ClusterIpService impacts related GroupNet
-   CloudPolicy impacts related CloudPool
-   CloudAccount impacts related CloudPool

## [Usage](#contents)

### [Adding Isilon Clusters](#contents)

Use the following steps to start monitoring an Isilon cluster using the
Zenoss web interface.

1.  Navigate to Infrastructure tab in the Zenoss web interface
2.  Select the "Add EMC Isilon Cluster" option from the Add Device
    drop-down menu
3.  Specify the IP Address, Username, Password and optionally the Port
    and SSL fields if your cluster is not using the default values
4.  Click *Add*.
5.  A device representing the Isilon cluster will be added to the
    /Devices/Storage/EMC/Isilon device class
6.  After modeling, the title of the cluster will reflect the configured
    cluster name.
7.  A device class (/Devices/Storage/EMC/Isilon/\[CLUSTER_NAME\]) and
    willcontain discovered node devices
8.  Node device ids will follow the \[CLUSTER_NAME\]-lnn-\[NODE_ID\]
    convention

### [Configuring optional SNMP Monitoring](#contents)

SNMP discovery and monitoring is disabled by default, since most of its
data is available via HTTP. To use SNMP monitoring, set the
`zSnmpMonitorIgnore` zProperty to False at either the Device Class or
Device level. Please note that each node must have its own externally
available IP address in order for SNMP monitoring to function

### [Configuring Debug Mode](#contents)

Debug Mode can be enabled by setting the `zEMCIsilonDebugMode` property
to True on the device class or Isilon cluster device. Debug Mode
provides additional monitoring of the API usage itself, creating
components that represent available URI endpoints. Collected metrics
include counts for HTTP transactions against each URI by type (GET,
POST, PUT, etc). Because this adds overhead to an already monitored
system, these components are disabled by default and must be enabled by
the user (component grid `Monitoring` dialog). Debug mode is intended to
assist with identifying potential bottlenecks and query inefficiencies
caused either by this ZenPack or by other applications utilizing the
OneFS HTTP API.

### [Command Line Tools](#contents)

Several scripts are included for use with troubleshooting or sample data
collection. These scripts reside in the

-   $ZENPACK/ZenPacks/zenoss/EMC/Isilon/utilities

directory and calling --help will display usage information for each

-   collect-samples (performs iterative walk through API collecting as
    much as it can)
-   collect-statistics-keys (Narrowed focus on statistics and available
    keys for use in URI endpoints)
-   collect-statistics (Performs a metric collection query and returns
    the JSON output)
-   check-authorization (Displays configured permissions for the
    authenticating user)

### [Isilon Cluster Networking Considerations](#contents)

Currently, modeling of the Isilon cluster environment (including the
nodes) is conducted using the Cluster IP address. This is so that IP
configuration changes to nodes can be updated even in cases where a node
no longer has an external IP.

Please note that IP address changes that take place will be updated when
the Cluster device is remodeled (not the Node device).

For performance data collection, queries are conducted on a randomly
selected external IP address belonging to either the cluster or one of
the nodes. If a SmartHost IP is used as the host when initially adding
the Cluster, then the SmartHost IP will be included in this selection.

Monitoring of the Isilon cluster and its nodes is designed with the
expectation that each node will have at least one external IP interface
that is accessible for monitoring.

Although version 1.0.1 removes this requirement (nodes can now be
modeled/monitored without an external interface), it should still be
considered a strong recommendation since monitoring multiple nodes
against a single IP address could impact monitoring performance and/or
reliability.

Operating with a small pool of IPs against a larger number of nodes
means that API queries (used by this ZenPack) for each node, in addition
to the cluster itself, will be directed at a subset of the nodes for the
cluster. The `zEMCIsilonHttpPoolSize` zProperty has been introduced
(version 1.0.1) and may ameliorate this concern by limiting the number
of simultaneous API queries.

The EMC Isilon documentation seems to support this perspective in that
it recommends a scaling formula for determining the number of IP
Addresses that should be made available depending on the size of a
cluster:

-   [Isilon External Network Connectivity Guide](https://blog.dellemc.com/en-us/emc-isilon-external-network-connectivity-guide/){.external-link}
-   [Isilon Advanced Networking Fundamentals     (pdf)](https://www.emc.com/collateral/white-papers/h16463-isilon-advanced-networking-fundamentals.pdf){.external-link}

For example, the "Isilon External Network Connectivity Guide" recommends
a total of 19 IP addresses (divided into pools) for a 3-node cluster.

One additional thing to note is that the optional SNMP monitoring will
not work without at least one external IP address assigned to each node.

### [OneFS API Minimally Privileged User](#contents)

Certainly the default "admin" account privileges are more than
sufficient for this ZenPack.

Security concerns (such as API write access for the admin user),
however, make the creation of a separate "monitoring" User/Role a good
idea, and we strongly recommend it.

Performance may also be improved by using a minimally configured
account, since API calls with read/write access uses two client
connections (according to the "isi statistics client" command output)
instead of just one.

Fortunately, the creation of a Role with the needed Privileges is
straightforward and can be done from the Isilon Admin UI.

The list of (read) permissions consists of:

-   Platform API
-   Auth
-   CloudPool
-   Cluster
-   Devices
-   Event
-   FTP
-   HDFS
-   HTTP
-   NDMP
-   Network
-   NFS
-   NTP
-   Quota
-   SmartPools
-   SMB
-   SNMP
-   Statistics
-   Namespace Access
-   Namespace Traverse

Creating a Role with this list of Privileges and assigning a User to
this Role will be sufficient for the ZenPack's monitoring requirements.

## [Installed Items](#contents)

Installing this ZenPack will add the following items to your Zenoss
system.

Device Classes

-   /Storage/EMC/Isilon

Configuration Properties

-   zEMCIsilonHttpPort
-   zEMCIsilonUseSSL
-   zEMCIsilonUser
-   zEMCIsilonPassword
-   zEMCIsilonHttpTimeout
-   zEMCIsilonHttpPageSize
-   zEMCIsilonHttpPoolSize
-   zEMCIsilonDebugMode

Modeler Plugins

-   EMC.Isilon.http.IsilonClusterMap
-   EMC.Isilon.http.IsilonNodeMap
-   EMC.Isilon.snmp.IsilonNodeMap

Datasource Types

-   Isilon Datasource (HTTP)
-   Isilon Events Datasource (HTTP)
-   SNMP Datasource (SNMP)

Monitoring Templates

-   IsilonCluster
-   IsilonClusterSNMP
-   IsilonClusterDevice
-   IsilonClusterNetworkTraffic
-   IsilonClusterAggregateDisk
-   IsilonClusterDeduplication
-   IsilonClusterNodes
-   IsilonNode
-   IsilonNodeDevice
-   IsilonNodeIFS
-   IsilonNodeNetworkTraffic
-   IsilonNodeAggregateDisk
-   IsilonNodeClients
-   IsilonNodeNFS
-   IsilonNodeSNMP
-   SmartPool
-   Endpoint
-   Quota
-   License
-   LicenseSNMP
-   FilePool
-   AccessZone
-   FlexnetPool
-   GroupNet
-   SubNet
-   NetworkRule
-   NodeIpInterface
-   Protocol
-   ProtocolSNMP
-   ProtocolSMB
-   ProtocolHDFS
-   ProtocolNFS
-   ProtocolNTP
-   ProtocolNDMP
-   ProtocolFTP
-   ProtocolHTTP
-   ProtocolSYNCIQ
-   StorageEnclosure
-   FileSystem
-   FiberChannelPort
-   HardDiskIsilon
-   HardDiskIsilonSNMP
-   FanModule
-   FanModuleSNMP
-   PowerSupply
-   PowerSupplySNMP
-   TemperatureSensor
-   TemperatureSensorSNMP
-   CloudPolicy
-   CloudAccount
-   CloudPool

Device Types

-   IsilonCluster (in /Storage/EMC/Isilon)
-   IsilonCluster (in /Storage/EMC/Isilon/CLUSTER_NAME)

Component Types

-   NodeComponent
-   SmartTierPool
-   SmartNodePool
-   Quota
-   License
-   FilePool
-   AccessZone
-   FlexnetPool
-   GroupNet
-   SubNet
-   NetworkRule
-   Protocol
-   SMBShare
-   NFSExport
-   NTPServer
-   NDMPContext
-   NDMPUser
-   NDMPSession
-   HDFSProxyUser
-   HDFSRack
-   StorageEnclosure
-   FileSystem
-   FiberChannelPort
-   HardDiskIsilon
-   FanModule
-   PowerSupply
-   TemperatureSensor
-   ClusterIpInterface
-   NodeIpInterface
-   ClusterIpService
-   CloudPolicy
-   CloudAccount
-   CloudPool
-   Endpoint

Event Classes

-   /Status/Isilon
-   /Perf/Isilon

## [Required Daemons](#contents)

Modeler:

-   zenmodeler

Performance Collector:

-   zenpython

## [Upgrade](#contents)

The EMC Isilon Zenpack can be upgraded. To upgrade the ZenPack, install
the latest version over the existing one. There is no action for the
user to migrate the data. The performance data and events of old ZenPack
are retained as per the retain policy settings.

## [Limitations](#contents)

## [Known Issues](#contents)

ANA-386 - CreateDimmTables() Return Error When rrddata_source
Processing.

To solve this this issue follow instructions according this arcticle:
[ANA-386 - CreateDimmTables() Return Error When rrddata_source Processing](https://support.zenoss.com/hc/en-us/articles/360059133212-Known-Issue-ANA-386-createDimmTables-return-error-when-rrddata-source-processing){.external-link}

## [Changes](#contents)

1.1.0

-   Added support API for OneFS 8.2.x, 9.0.0.0, 9.1.0.0 (ZPS-6907)
-   Tested with Zenoss Cloud, Zenoss 6.6.0 and Service Impact 5.5.5

1.0.4

-   ZenPack does not cause issues with building dim tables in Analytics
    (ZPS-3594)

1.0.3

-   Datapoints are now unique, preventing values from mashing and being
    overwriten (ZPS-7171)

1.0.2

-   Correct zenbatchdump output (ZPS-2900)
-   IpInterface method override output corrected (ZPS-6182)
-   Reduce logging verbosity (ZPS-4975)
-   Tested with Zenoss 6.4.1, Zenoss Cloud with and Service Impact 5.5.1

1.0.1

-   Allow monitoring of nodes without external IP (reservations noted
    above) (ZPS-3910)
-   Added "zEMCIsilonHttpPoolSize" zProperty to restrict simultaneous
    client connections
-   Updated icons to improve visibility in Cloud Zenoss
-   Handling of "Infinity" and "nan" output values (ZPS-3459)
-   Improved support for Cloud Zenoss (ZPS-3801)
-   Refactored and simplified utility scripts (ZPS-3787)
-   Added support for ISICSRF cookies (ZPS-4391)
-   Corrected plural of "Cloud Policy" in component list (ZPS-4648)
-   Fix flare message on Cluster IP Service components (ZPS-4645)
-   Fix FileSystem component grid display issues (ZPS-4649)
-   Fix warnings about Datapoint Alias length during installation
    (ZPS-4646)
-   Improved detail in error/warning logging (HTTP status and return
    messaging)
-   Improved data collection performance by consolidation of tasks using
    session pools
-   Documentation updated with notes about cluster IP allocation and
    user/role/privilege configuration
-   Tested with Zenoss Cloud, Zenoss Resource Manager 6.2.1 and 5.3.3

1.0.0

-   Initial release.

|                            |                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ZenPack Classification** |                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| **Commercial**             | This ZenPack is developed and supported by Zenoss Inc. Commercial ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to view all available Zenoss Commercial ZenPacks. |
| **Organization**           | Zenoss, Inc.                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **Name**                   | ZenPacks.zenoss.EMC.Isilon                                                                                                                                                                                                                                                                                                                                                                                                             |
| **Applications Monitored** | EMC Isilon Storage Platform                                                                                                                                                                                                                                                                                                                                                                                                            |

## Attachments:

-   [emc-zenpack.png](img/zenpack-emc-zenpack.png)
-   [emc-zenpack.png](img/zenpack-emc-zenpack.png)


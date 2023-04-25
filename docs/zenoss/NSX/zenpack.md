# VMware NSX

@lb[](img/zenpack-vmware-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.NSX

### Applications Monitored:

VMware NSX (6)

## VMware NSX ZenPack

VMware NSX-T monitoring.

## Releases

Version 2.0.0- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2021/10/21:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link}, [ZenPackLib ZenPack](http://help.zenoss.com/display/in/ZenPackLib){.external-link}
    Compatible with Zenoss Resource Manager 6.5.0, 6.6.0, and Zenoss
    Cloud

Version 1.2.1- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2017/02/01:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link}:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.x.x:   This is the last version that supports VMware NSX-V

## Background

This ZenPack provides support for monitoring VMware NSX-T. Modeling and
monitoring of devices placed in the /VMware/NSX device class is
performed using the NSX-T API by executing queries and parsing the
output.

## Gallery

@lb[](img/zenpack-nsx_add_device.png)

@lb[](img/zenpack-nsx_device_overview.png)

@lb[](img/zenpack-nsx_edge_transport_nodes.png)

@lb[](img/zenpack-nsx_firewall_rules.png)

@lb[](img/zenpack-nsx_host_transport_nodes.png)

@lb[](img/zenpack-nsx_ip_pools.png)

@lb[](img/zenpack-nsx_manager_nodes.png)

@lb[](img/zenpack-nsx_network_interfaces.png)

@lb[](img/zenpack-nsx_segments.png)

@lb[](img/zenpack-nsx_tier0_gateways.png)

@lb[](img/zenpack-nsx_tier1_gateways.png)

@lb[](img/zenpack-nsx_transport_zones.png)

@lb[](img/zenpack-nsx_vni_pools.png)

@lb[](img/zenpack-nsx_vpn_services.png)

@lb[](img/zenpack-nsx_virtual_switches.png)

## Features

The NSX ZenPack provides:

-   Initial discovery and continual synchronization of relevant
    components.
-   Performance monitoring.
-   System event management.
-   Service impact and root cause analysis (Requires Zenoss Service
    Dynamics).
-   Collection of detailed configuration data, including NAT Rules,
    Routing Protocols, Load Balancer Configs, and Firewall Configs.
-   Service impact and root cause analysis (Requires Zenoss Service
    Dynamics).

### Discovery

The following entities will be automatically discovered. The attributes
and collections will be updated on Zenoss's normal remodeling interval
which defaults to every 12 hours.

NSX-T Manager Nodes:   Attributes: Fully Qualified Domain Name, Node ID, Status, Uptime

<!-- -->

NSX-T Compute Managers:   Attributes: Access Level to NSX, Service Account is Created,
    Description, Origin Type, Proxy HTTPS Port, OIDC Provider, Tags:   Relations: NSX-T Virtual Switches

<!-- -->

NSXT-T IP Pools:   Attributes: Description, IP Release Delay, Tags

<!-- -->

NSX-T Host Transport Nodes:   Attributes: Description, Failure Domain, Maintenance Mode, IP
    Addresses, Transport Node ID, Display Name, IP Addresses, OS Type,
    OS Version:   Relations: NSX-T Network Interfaces

<!-- -->

NSX-T Edge Transport Nodes:   Attributes: Description, Failure Domain, Maintenance Mode, IP
    Addresses, Transport Node ID, Display Name, IP Addresses, Deployment
    Type, Enable SSH, Hostname, Compute Folder in The Specified vCenter
    Server, Cluster or Resourcepool ID, Connected Distributed Portgroups
    or VLANs, Host ID, Manage Network, Storage, vCenter Server ID, CPU
    Count, Memory Allocation MB, vSphere Host ID:   Relations: NSX-T Network Interfaces

<!-- -->

NSX-T Transport Zones:   Attributes: Host Switch ID, Host Switch Mode, Host Switch Name, Is
    Default, Nested NSX Environment, Transport Type, Tags:   Relations: NSX-T Segments

<!-- -->

NSX-T Network Interfaces:   Attributes: Administration Status, Backing VNI by NSX, Connected
    Switch, Connected Switch Type, Driver name, Managed by the Host,
    Link Status, Interface Type, PCI device, Interface MTU, Status
    source:   Relations: NSX-T Host Transport Node, NSX-T Edge Transport Node

<!-- -->

NSX-T Tier0 Gateways:   Attributes: ARP limit, Default Rule Logging, Description, DHCP
    configuration, Disable Firewall, Failover Mode, Force whitelisting,
    High-availability Mode, Internal Transit Subnets, IPv6 profiles
    configuration, Transit Subnets, Tags:   Relations: NSX-T Tier1 Gateways, NSX-T Segments

<!-- -->

NSX-T Tier1 Gateways:   Attributes: ARP limit, Default Rule Logging, Description, DHCP
    configuration, Disable Firewall, Enable Standby Relocation, Failover
    Mode, Force whitelisting, IPv6 profiles configuration, Route
    Advertisement Types, Pool Allocation, Tags:   Relations: NSX-T Tier0 Gateway, NSX-T Segments

<!-- -->

NSX-T Segments:   Attributes: Admin State, Description, DNS domain name, Evpn Segment
    Flag, Allocation MAC Pool, Replication Mode, Subnets, Tags, Segment
    Type, VLAN ids:   Relations: NSX-T Tier0 Gateway, NSX-T Tier1 Gateway, NSX-T Transport
    Zone

<!-- -->

NSX-T Firewall Rules:   Attributes: Action, Description, Destination Groups, Negation of
    destination groups, Direction of Traffic, Is Disabled, IP Protocol,
    Is Default, Enable Packet Logging, Notes, Profiles, Policy Paths,
    Sequence number, Services, Source Group Paths,  Negation of Source
    Groups, Domain ID, Policy ID, Policy Category, Firewall Rule ID

<!-- -->

NSX-T VPN Services:   Attributes: Description, Admin Status, Internet key exchange log
    level, IPSec HA Sync, Logical Router ID, Tags

<!-- -->

NSX-T VNI Pools:   Attributes: Description, Ranges, Tags

NSX-T Virtual Switches
          Attributes: ID of the virtual switch in compute manager,
Discovered Nodes, Description, ID of the compute manager, Portgroup
UUID, Tags, Uplink Port Names, Uplink portgroup
          Relations: NSX-T Compute Manager

## Usage

The installation of this ZenPack will create the device class
*/VMware/NSX*. This new device class will provide five new zProperties
*zNSXUsername*, *zNSXPassword*, *zNSXPort*, *zNSXSSL*, and
*zNSXConcurrentHTTP*

### Add a NSX-T Device

The following procedure assumes that credentials have been set.

-   Select Infrastructure from the navigation bar.

-   Select Add a Single Device from the Add Device list of options. The
    Add a Single Device dialog appears.
    @lb[](img/zenpack-nsx_add_device.png){.confluence-embedded-image width="822"}

-   Enter the following information in the dialog:

    <table>
    <tbody>
    <tr markdown="1">
    <th>Name</th>
    <th>Description</th>
    </tr>

    <tr markdown="1">
    <td>Name or IP</td>
    <td>NSX host to model.</td>
    </tr>
    <tr markdown="1">
    <td>Device Class</td>
    <td>/VMware/NSX</td>
    </tr>
    <tr markdown="1">
    <td>Model Device</td>
    <td>Select this option unless adding a device with a user name and password<br />
    different than found in the device class. If you do not select this option,<br />
    then you must add the credentials (see) and then manually model the device.</td>
    </tr>
    <tr markdown="1">
    <td>zNSXUsername</td>
    <td>NSX user with privileges to gather performance information</td>
    </tr>
    <tr markdown="1">
    <td>zNSXPassword</td>
    <td>Password for the NSX User</td>
    </tr>
    <tr markdown="1">
    <td>zNSXSSL</td>
    <td>Enable SSL for communication with NSX</td>
    </tr>
    </tbody>
    </table>

-   Click **Add**.

### System Event Monitoring

Monitoring plugin collects System Events from NSX-T Manager and shows
them as Zenoss Events with the same time and severity.

<dl markdown="1">
<dt markdown="1">
Standard Zenoss Event Fields
</dt>
</dl>

-   device
-   component
-   summary
-   severity
-   eventClassKey (for mapping specific event types)
-   eventKey (for de-duplication and auto-clear fingerprinting)

Once the event is sent, it will not be sent again. If the user clears
the event, it will not reappear again. There&rsquo;s no automatic mechanism to
clear system events, as they can not be cleared from NSX manager and do
not have expire date, therefore the user is to close new events manually
from Zenoss UI.

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Configuration Properties
</dt>
</dl>

-   zNSXUsername
-   zNSXPassword
-   zNSXPort
-   zNSXSSL
-   zNSXConcurrentHTTP

<dl markdown="1">
<dt markdown="1">
Device Classes
</dt>
</dl>

-   /VMware/NSX

<dl markdown="1">
<dt markdown="1">
Modeler Plugins
</dt>
</dl>

-   zenoss.VMwareNSX

<dl markdown="1">
<dt markdown="1">
Monitoring Templates
</dt>
</dl>

-   NSXManager (in /VMware/NSX)
-   NSXManagerNode (in /VMware/NSX)
-   NSXTransportNode (in /VMware/NSX)
-   NSXTIPPool (in /VMware/NSX)
-   NSXNetworkInterface (in /VMware/NSX)
-   NSXTFirewallRule (in /VMware/NSX)

## Monitoring Templates

<dl markdown="1">
<dt markdown="1">
NSXManager (in /VMware/NSX)
</dt>
</dl>

-   Data Points
    -   control_cluster_status
    -   mgmt_cluster_status
-   Graphs
    -   *None*

<dl markdown="1">
<dt markdown="1">
NSXManagerNode (in /VMware/NSX)
</dt>
</dl>

-   Data Points
    -   disk_space_total
    -   disk_space_used
    -   load_average_1\_min
    -   load_average_5\_min
    -   load_average_15_min
    -   mem_total
    -   mem_cache
    -   mem_used
    -   swap_total
    -   swap_used
    -   uptime
-   Graphs
    -   Memory Usage
    -   Storage Usage
    -   System Load
    -   Disk Swap

Note: `disk_space_total` and `disk_space_used` values may be different
from the values in NSX UI. Zenoss takes these values from the NSX API,
but NSX UI doesn't. NSX UI iterates though `file_systems` field and sums
the `total_space` of each file system with some inaccuracy (NSX UI uses
1000 as base, not 1024, for converting kbytes to other units)

<dl markdown="1">
<dt markdown="1">
NSXTransportNode (in /VMware/NSX)
</dt>
</dl>

-   Data Points
    -   disk_space_total
    -   disk_space_used
    -   load_average_1\_min
    -   load_average_5\_min
    -   load_average_15_min
    -   mem_total
    -   mem_cache
    -   mem_used
    -   swap_total
    -   swap_used
    -   avg_cpu_core_usage_dpdk
    -   avg_cpu_core_usage_non_dpdk
-   Graphs
    -   CPU Usage
    -   Memory Usage
    -   Storage Usage
    -   System Load
    -   Disk Swap

<dl markdown="1">
<dt markdown="1">
NSXTIPPool (in /VMware/NSX)
</dt>
</dl>

-   Data Points
    -   allocated_ips
    -   total_ips
-   Graphs
    -   IP Pool Usage

<dl markdown="1">
<dt markdown="1">
NSXNetworkInterface (in /VMware/NSX)
</dt>
</dl>

-   Data Points
    -   rx_bytes
    -   rx_dropped
    -   rx_errors
    -   rx_frame
    -   rx_packets
    -   tx_bytes
    -   tx_carrier
    -   tx_colls
    -   tx_dropped
    -   tx_errors
    -   tx_packets
-   Graphs
    -   Total Bytes
    -   Total Packets
    -   Error Counts
    -   Dropped Packets

<dl markdown="1">
<dt markdown="1">
NSXTFirewallRule (in /VMware/NSX)
</dt>
</dl>

-   Data Points
    -   byte_count
    -   hit_count
    -   max_popularity_index
    -   max_session_count
    -   packet_count
    -   popularity_index
    -   session_count
    -   total_session_count
-   Graphs
    -   Packet Count
    -   Bytes Count
    -   Sessions

## Daemons

|                       |            |
|-----------------------|------------|
| Type                  | Name       |
| Modeler               | zenmodeler |
| Performance Collector | zenpython  |

## Changes

<dl markdown="1">
<dt markdown="1">
2.0.0
</dt>
</dl>

-   Add Support for NSX-T
-   Tested with Zenoss Resource Manager 6.5.0, 6.6.0, Zenoss Cloud and
    Service Impact 5.5.3.

<dl markdown="1">
<dt markdown="1">
1.2.1
</dt>
</dl>

-   Fixed traceback when modeling edge firewall rules. (ZPS-508)

<dl markdown="1">
<dt markdown="1">
1.2.0
</dt>
</dl>

-   Add zNSXConcurrentHTTP zProperty to limit maximum number of
    simultaneous http connections allowed per NSX manager.
-   Add configuration check for openstack_neutron_integration. (OSI
    2.1.1)
-   Fixed metric collection stopping for all Edge and Interfaces if one
    or more edge vm is powered off. (ZEN-19008)
-   Fixed invalid dictionary for event messages when NSX edge is powered
    off. (ZEN-19009)
-   Fixed NSX devices failing to collect when there is a 5.x edge
    device. (ZEN-21660)
-   Fixed TypeError on Edge components. (ZEN-22734)
-   Added modeling and usage monitoring for IP Pools and Segment ID
    Pools. (ZEN-22189)
-   Link NSX Edge components to vSphere VMs (requires vSphere ZP).
-   Added modeling and monitoring for Edge Firewall Rules for each Edge.
-   Added modeling and monitoring for NSX Subinterfaces
-   Added monitoring for connection state to vCenter (requires vSphere
    ZP).
-   Added modeling for Routing Protocols.
-   Added modeling for NAT Rules.
-   Added load balancer modeling and monitoring.

<dl markdown="1">
<dt markdown="1">
1.0.1
</dt>
</dl>

-   Fixed traceback during modeling NSX Manager device if one or more
    Edges is powered off. (ZEN-18984)

<dl markdown="1">
<dt markdown="1">
1.0.0
</dt>
</dl>

-   Initial release

## Attachments:

-   [NSX_AddNSXManager.png](img/zenpack-nsx_addnsxmanager.png)
-   [NSX_Cluster_Controllers.png](img/zenpack-nsx_cluster_controllers.png)
-   [NSX_Controllers.png](img/zenpack-nsx_controllers.png)
-   [NSX_Credential.png](img/zenpack-nsx_credential.png)
-   [NSX_Edge_Firewall_Rules.png](img/zenpack-nsx_edge_firewall_rules.png)
-   [NSX_Edges-Edge_Firewall_Rules.png](img/zenpack-nsx_edges-edge_firewall_rules.png)
-   [NSX_Edges-Firewall_Config.png](img/zenpack-nsx_edges-firewall_config.png)
-   [NSX_Edges-Loadbalancer_Config.png](img/zenpack-nsx_edges-loadbalancer_config.png)
-   [NSX_Edges-NAT_Rules.png](img/zenpack-nsx_edges-nat_rules.png)
-   [NSX_Edges-Routing_Protocols.png](img/zenpack-nsx_edges-routing_protocols.png)
-   [NSX_Edges.png](img/zenpack-nsx_edges.png)
-   [NSX_Firewall_Rules.png](img/zenpack-nsx_firewall_rules.png)
-   [NSX_Impact.png](img/zenpack-nsx_impact.png)
-   [NSX_Interfaces.png](img/zenpack-nsx_interfaces.png)
-   [NSX_IP_Pools.png](img/zenpack-nsx_ip_pools.png)
-   [NSX_IPSec_Tunnels.png](img/zenpack-nsx_ipsec_tunnels.png)
-   [NSX_Network_Scopes.png](img/zenpack-nsx_network_scopes.png)
-   [NSX_Segment_ID_Pools.png](img/zenpack-nsx_segment_id_pools.png)
-   [NSX_SSL.png](img/zenpack-nsx_ssl.png)
-   [NSX_Subinterfaces.png](img/zenpack-nsx_subinterfaces.png)
-   [NSX_Virtual_Switches.png](img/zenpack-nsx_virtual_switches.png)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)
-   [NSX_Cluster_Controllers.png](img/zenpack-nsx_cluster_controllers.png)
-   [NSX_AddNSXManager.png](img/zenpack-nsx_addnsxmanager.png)
-   [NSX_Controllers.png](img/zenpack-nsx_controllers.png)
-   [NSX_Credential.png](img/zenpack-nsx_credential.png)
-   [NSX_Edge_Firewall_Rules.png](img/zenpack-nsx_edge_firewall_rules.png)
-   [NSX_Edges-Edge_Firewall_Rules.png](img/zenpack-nsx_edges-edge_firewall_rules.png)
-   [NSX_Edges-Firewall_Config.png](img/zenpack-nsx_edges-firewall_config.png)
-   [NSX_Edges-Loadbalancer_Config.png](img/zenpack-nsx_edges-loadbalancer_config.png)
-   [NSX_Edges-NAT_Rules.png](img/zenpack-nsx_edges-nat_rules.png)
-   [NSX_Edges-Routing_Protocols.png](img/zenpack-nsx_edges-routing_protocols.png)
-   [NSX_Edges.png](img/zenpack-nsx_edges.png)
-   [NSX_Firewall_Rules.png](img/zenpack-nsx_firewall_rules.png)
-   [NSX_Impact.png](img/zenpack-nsx_impact.png)
-   [NSX_Interfaces.png](img/zenpack-nsx_interfaces.png)
-   [NSX_IP_Pools.png](img/zenpack-nsx_ip_pools.png)
-   [NSX_IPSec_Tunnels.png](img/zenpack-nsx_ipsec_tunnels.png)
-   [NSX_Network_Scopes.png](img/zenpack-nsx_network_scopes.png)
-   [NSX_SSL.png](img/zenpack-nsx_ssl.png)
-   [NSX_Segment_ID_Pools.png](img/zenpack-nsx_segment_id_pools.png)
-   [NSX_Virtual_Switches.png](img/zenpack-nsx_virtual_switches.png)
-   [NSX_Subinterfaces.png](img/zenpack-nsx_subinterfaces.png)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)
-   [NSX_Edge_Firewall_Rules.png](img/zenpack-nsx_edge_firewall_rules.png)
-   [NSX_Credential.png](img/zenpack-nsx_credential.png)
-   [NSX_AddNSXManager.png](img/zenpack-nsx_addnsxmanager.png)
-   [NSX_SSL.png](img/zenpack-nsx_ssl.png)


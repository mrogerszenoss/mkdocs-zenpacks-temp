# Nutanix

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Authors:

Zenoss, Inc.

### Organization:

Zenoss, Inc

### Name:

ZenPacks.zenoss.Nutanix

### Applications Monitored:

[Nutanix Hyperconverged Infrastructure](https://www.nutanix.com/){.external-link}

## Nutanix ZenPack

This ZenPack provides system monitoring for Nutanix hyper-converged
infrastructure.

## Releases

**Version 2.0.1** - [Download](https://delivery.zenoss.com){.external-link}:   Released on 2022/07/29:   Requires [PythonCollector ZenPack](http://zenoss.com/product/zenpacks/pythoncollector){.external-link},[ZenPackLib ZenPack](http://zenoss.com/product/zenpacks/zenpacklib){.external-link}:   Compatible with Zenoss 6.x, Zenoss Cloud, and Impact

<!-- -->

**Version 2.0.0** - [Download](https://delivery.zenoss.com){.external-link}:   Released on 2020/07/02:   Requires [PythonCollector ZenPack](http://zenoss.com/product/zenpacks/pythoncollector){.external-link},[ZenPackLib ZenPack](http://zenoss.com/product/zenpacks/zenpacklib){.external-link}:   Compatible with Zenoss 6.x, Zenoss Cloud, and Impact

<!-- -->

**Version 1.0.3** - [Download](https://delivery.zenoss.com){.external-link}:   Released on 2020/01/17:   Requires [PythonCollector ZenPack](http://zenoss.com/product/zenpacks/pythoncollector){.external-link},[ZenPackLib ZenPack](http://zenoss.com/product/zenpacks/zenpacklib){.external-link}:   Compatible with Zenoss 6.x and Zenoss Cloud

<!-- -->

**Version 1.0.2** - [Download](https://delivery.zenoss.com){.external-link}:   Released on 2019/04/17:   Requires [PythonCollector ZenPack](http://zenoss.com/product/zenpacks/pythoncollector){.external-link},[ZenPackLib ZenPack](http://zenoss.com/product/zenpacks/zenpacklib){.external-link}:   Compatible with Zenoss 6.x and Zenoss Cloud

<!-- -->

**Version 1.0.1** - [Download](https://delivery.zenoss.com){.external-link}:   Released on 2017/11/14:   Requires [PythonCollector ZenPack](http://zenoss.com/product/zenpacks/pythoncollector){.external-link},[ZenPackLib ZenPack](http://zenoss.com/product/zenpacks/zenpacklib){.external-link}:   Compatible with Zenoss Resource Manager 5.2 - 6.0

<!-- -->

**Version 1.0.0** - [Download](https://delivery.zenoss.com){.external-link}:   Released on 2017/09/22:   Requires [PythonCollector ZenPack](http://zenoss.com/product/zenpacks/pythoncollector){.external-link},[ZenPackLib ZenPack](http://zenoss.com/product/zenpacks/zenpacklib){.external-link}:   Compatible with Zenoss Resource Manager 5.2.x and 5.3.x

## Background

This ZenPack monitors Nutanix hyper-converged infrastructure.

### Prerequisites

-   Nutanix (5.15+)
-   Nutanix API V1/V2
-   Prism API credentials
-   ZenPackLib ZenPack 2.0.8+

### Gallery

**Nutanix Overview**

-   Contains the device summary, status, and list of components.

@lb[](img/zenpack-nutanixoverview.png)

**Cluster Summary**

New graphs to 2.0.0 include the IO Bandwidth and IO Latency

@lb[](img/zenpack-nutanixclusters.png)

**Nutanix Component - Interfaces**

-   A new component introduced in 2.0.0, is responsible for tracking
    network usage

@lb[](img/zenpack-nutanixinterfaces.png)

**Nutanix Dependencies View**

-   Displays the known associations between the selected component and
    other components of the same device or linked devices.

@lb[](img/zenpack-dependencyview.png)

**Nutanix Dynamic View**

-   Provides a visual representation of how the device's components are
    organized.

@lb[](img/zenpack-dynamicview.png)

## Features

Nutanix features include:

-   Overall Cluster Health Monitoring
-   Health Monitoring for Clusters, Hosts, and CVMs
-   Graphs for key Nutanix settings and performance metrics
-   Service Impact and root cause analysis. (Requires Zenoss Service
    Dynamics)
-   Incremental modeling, when changes to the cluster are detected
-   Event Management

### Nutanix Structure and Discovery

Objects are automatically discovered via the Nutanix API. The ZenPack
class structure can be visualized in the following Diagram:

@lb[](img/zenpack-nutanixclasses.png)Nutanix
ZP Design

#### Nutanix Device (NutanixEndpoint)

-   Description: The Nutanix device, can host multiple clusters.
-   Attributes: cluster_external_ipaddress, cluster_uuid, device_uuid,
    hypervisor_types, model_name, ncc_version, product_version, timezone
-   Relationships: nutanixClusters
-   Datasources:
    -   events
    -   alerts

#### Nutanix Clusters (NutanixCluster)

-   Description: The cluster component. Nutanix can host multiple
    clusters.
-   Attributes: cluster_external_ipaddress, cluster_uuid, num_hosts,
    operation_mode, storage_usage_percent, total_cpu, total_memory,
    total_storage, version
-   Relationships: nutanixEndpoint, nutanixCVMs, nutanixHosts,
    nutanixStoragePools, nutanixVMs, nutanixVdisks
-   Datapoints:
    -   cluster:
        -   operation_mode
    -   stats:
        -   content_cache_hit_percent
        -   controller_read_io_percent
        -   controller_write_io_percent
        -   hypervisor_cpu_usage_percent
        -   hypervisor_kvm_cpu_usage_percent
        -   hypervisor_kvm_memory_usage_percent
        -   hypervisor_memory_usage_percent
        -   read_io_percent
        -   write_io_percent
        -   io_bandwidth_kBps
        -   read_io_bandwidth_kBps
        -   write_io_bandwidth_kBps
        -   hypervisor_io_bandwidth_kBps
        -   hypervisor_read_io_bandwidth_kBps
        -   hypervisor_write_io_bandwidth_kBps
        -   controller_io_bandwidth_kBps
        -   controller_read_io_bandwidth_kBps
        -   controller_write_io_bandwidth_kBps
        -   replication_transmitted_bandwidth_kBps
        -   replication_received_bandwidth_kBps
        -   avg_io_latency_usecs
        -   hypervisor_avg_io_latency_usecs
        -   hypervisor_avg_read_io_latency_usecs
        -   hypervisor_avg_write_io_latency_usec
        -   controller_avg_io_latency_usecs
        -   controller_avg_read_io_latency_usecs
        -   controller_avg_write_io_latency_usecs
    -   usagestats:
        -   storage.capacity_bytes
        -   storage.free_bytes
        -   storage.usage_percent
        -   storage_tier.das-sata.capacity_bytes
        -   storage_tier.das-sata.free_bytes
        -   storage_tier.das-sata.usage_percent
        -   storage_tier.ssd.capacity_bytes
        -   storage_tier.ssd.free_bytes
        -   storage_tier.ssd.usage_percent
-   Graphs:
    -   IO Bandwidth
    -   IO Latency
    -   IO
    -   IO Cache Hit Ratio
    -   Controller IO
    -   Hypervisor Memory Utilization
    -   Storage Utilization
    -   SSD Storage
    -   DAS Storage
-   Thresholds:
    -   90 Percent Storage
    -   95 Percent Storage
    -   95 Percent hypervisor memory
    -   98 Percent Controller IO
    -   98 Percent Disk IO

#### Hosts (NutanixHost)

-   Description: Hosts that Nutanix services run on
-   Attributes: cluster_uuid, host_uuid, hypervisor_address,
    service_vmexternal_ip, cpu_capacity_in_hz, memory_capacity_in_bytes,
    hypervisor_version
-   Relationships: nutanixCluster, nutanixHardDisks
-   Datapoints:
    -   host:
        -   num_vms
        -   state
    -   stats:
        -   content_cache_hit_percent
        -   controller_read_io_percent
        -   controller_write_io_percent
        -   hypervisor_cpu_usage_percent
        -   hypervisor_memory_usage_percent
        -   read_io_percent
        -   write_io_percent
        -   io_bandwidth_kBps
        -   read_io_bandwidth_kBps
        -   write_io_bandwidth_kBps
        -   hypervisor_io_bandwidth_kBps
        -   hypervisor_read_io_bandwidth_kBps
        -   hypervisor_write_io_bandwidth_kBps
        -   controller_io_bandwidth_kBps
        -   controller_read_io_bandwidth_kBps
        -   controller_write_io_bandwidth_kBps
        -   avg_io_latency_usecs
        -   hypervisor_avg_io_latency_usecs
        -   hypervisor_avg_read_io_latency_usecs
        -   hypervisor_avg_write_io_latency_usecs
        -   controller_avg_io_latency_usecs
        -   controller_avg_read_io_latency_usecs
        -   controller_avg_write_io_latency_usecs
    -   usagestats:
        -   storage.capacity_bytes
        -   storage.free_bytes
        -   storage.usage_percent
        -   storage_tier.das-sata.capacity_bytes
        -   storage_tier.das-sata.free_bytes
        -   storage_tier.das-sata.usage_percent
        -   storage_tier.ssd.capacity_bytes
        -   storage_tier.ssd.free_bytes
        -   storage_tier.ssd.usage_percent
-   Graphs:
    -   IO Bandwidth
    -   IO Latency
    -   IO
    -   IO Cache Hit Ratio
    -   Hypervisor CPU Utilization
    -   Hypervisor Memory Utilization
    -   Storage Utilization
    -   SSD Storage
    -   DAS Storage
-   Thresholds:
    -   90 Percent Storage
    -   95 Percent Storage
    -   95 Percent hypervisor cpu
    -   95 Percent hypervisor memory
    -   98 Percent Disk IO

#### NutanixVM/NutanixCVM

Nutanix CVMs and VMs have a very similar structure and we cover them
together although they are completely distinct components.

-   Description: Virtual Machines and Controller Virtual Machines
-   Attributes: cluster_uuid, host_uuid, ipAddresses, mac_addresses,
    memoryCapacityInBytes, network_uuids, nonNdfsDetails, num_vcpus,
    vdisk_uuids, vm_uuid
-   Relationships: nutanixCluster, nutanixVdisk
-   Datapoints:
    -   stats:
        -   memory_usage_percent
        -   hypervisor_consumed_memory_bytes
        -   guest.memory_usage_bytes
        -   guest.memory_usage_percent
        -   hypervisor_cpu_usage_percent
        -   hypervisor_io_bandwidth_kBps
        -   hypervisor_read_io_bandwidth_kBps
        -   hypervisor_write_io_bandwidth_kBps
        -   controller_io_bandwidth_kBps
        -   controller_read_io_bandwidth_kBps
        -   controller_write_io_bandwidth_kBps
        -   hypervisor_avg_io_latency_usecs
        -   hypervisor_avg_read_io_latency_usecs
        -   hypervisor_avg_write_io_latency_usecs
        -   controller_avg_io_latency_usecs
        -   controller_avg_read_io_latency_usecs
        -   controller_avg_write_io_latency_usecs
    -   vm:
        -   powerState
-   Graphs:
    -   IO Bandwidth
    -   IO Latency
    -   Hypervisor CPU Utilization
    -   Memory Utilization
-   Thresholds:
    -   98 percent of guest memory

#### Network Interfaces (NutanixInterface)

-   Description: Physical network interfaces associated with each host
-   Attributes: cluster_uuid, host_uuid, interface_uuid, name,
    mac_address,
    ipv4_addr, ipv6_addr, link_mtu, link_capacity, details,
    discovery_protocol,
    switch, switch_port, switch_vlan_id, switch_mac_address,
    switch_details
-   Relationships: nutanixHost
-   Datapoints:
    -   nic:
        -   network.transmitted_bytes
        -   network.received_bytes
-   Graphs:
    -   Network Usage

#### Hard Disks (NutanixHardDisk)

-   Description: Physical hard disks used for VM storage
-   Attributes: cluster_uuid, disk_uuid, host_uuid, location, model,
    serial_number, size, storage_tier_name
-   Relationships: nutanixHost, nutanixStoragePool
-   Datapoints:
    -   disk:
        -   disk_status
        -   online
    -   stats:
        -   read_io_percent
        -   write_io_percent
        -   read_io_bandwidth_kBps
        -   write_io_bandwidth_kBps
        -   avg_io_latency_usecs
    -   usagestats:
        -   storage.capacity_bytes
        -   storage.free_bytes
        -   storage.usage_bytes
        -   storage.usage_percent
-   Graphs:
    -   Disk IO Bandwidth
    -   Disk IO Latency
    -   Storage Utilization
-   Thresholds:
    -   90 Percent Storage
    -   95 Percent Storage

#### Storage Pools (NutanixStoragePool)

-   Description: The Nutanix logical storage objects
-   Attributes: cluster_uuid, disk_uuids, free_bytes, size,
    storagepool_uuid, used_bytes
-   Relationships: nutanixContainers, nutanixHardDisks
-   Datapoints:
    -   stats:
        -   avg_io_latency_usecs
        -   read_io_bandwidth_kBps
        -   write_io_bandwidth_kBps
        -   read_io_ppm
        -   write_io_ppm
        -   read_io_percent
        -   write_io_percent
    -   usagestats:
        -   storage.capacity_bytes
        -   storage.free_bytes
        -   storage.usage_pbytes
        -   storage.usage_percent
        -   storage_tier.das-sata.capacity_bytes
        -   storage_tier.das-sata.free_bytes
        -   storage_tier.das-sata.usage_bytes
        -   storage_tier.das-sata.usage_percent
        -   storage_tier.ssd.capacity_bytes
        -   storage_tier.ssd.free_bytes
        -   storage_tier.ssd.usage_bytes
        -   storage_tier.ssd.usage_percent
-   Graphs:
    -   IO Bandwidth
    -   IO Latency
    -   Storage Utilization
    -   SSD Storage
    -   DAS Storage
-   Thresholds:
    -   90 Percent Storage
    -   95 Percent Storage

#### Nutanix Storage Containers (NutanixContainer)

-   Description: Storage containers sub-divide Nutanix storage pools.
-   Attributes: cluster_uuid, compressionEnabled, container_uuid,
    erasureCode, free_bytes, replicationFactor, size, storagepool_uuid,
    used_bytes
-   Relationships: nutanixStoragePool, nutanixVdisks
-   Datapoints:
    -   stats:
        -   controller_avg_read_io_size_kbytes
        -   controller_avg_write_io_size_kbytes
        -   controller_read_io_bandwidth_kBps
        -   controller_write_io_bandwidth_kBps
        -   controller_avg_read_io_latency_usecs
        -   controller_avg_write_io_latency_usecs
    -   usagestats:
        -   storage.usage_percent
        -   storage.usage_bytes
        -   storage.capacity_bytes
        -   storage.free_bytes
        -   storage_tier.das-sata.usage_bytes
        -   storage_tier.ssd.usage_bytes
-   Graphs:
    -   Controller IO Bandwidth
    -   Controller IO Latency
    -   Storage Utilization
    -   SSD Usage
    -   DAS Usage
-   Thresholds
    -   90 Percent Storage
    -   95 Percent Storage

#### Nutanix Virtual Disks (NutanixVdisk)

-   Description: Virtual disks existing inside a NutanixContainer.
-   Attributes: attached_vm_uuid, cluster_uuid, size,
    storage_container_uuid, vdisk_uuid
-   Relationships: nutanixCVM, nutanixCluster, nutanixContainer,
    nutanixVM
-   Datapoints:
    -   stats:
        -   controller_avg_read_io_size_kbytes
        -   controller_avg_write_io_size_kbytes
        -   controller_read_io_bandwidth_kBps
        -   controller_write_io_bandwidth_kBps
        -   controller_avg_read_io_latency_usecs
        -   controller_avg_write_io_latency_usecs
-   Graphs: IO
    -   Controller IO Bandwidth
    -   Controller IO Latency

## Usage

You must expose the Nutanix V1 and V2 APIs on your Prism system. Once
you have the username and password, you can enter the device in Zenoss
as follows:

-   Go to Infrastructure Tab
-   From the Add Device pull-down, select *Add Nutanix Device*
    -   Enter the hostname or IP address
    -   Enter the username
    -   Enter the password
    -   Select the correct collector
    -   Finally, click on *Add*
-   After the modeling is complete you should see your device components
-   If modeling large numbers of components you may have to increase
    zCollectorClientTimeout well beyond 600 to avoid model timeout.

### Nutanix Batch Configuration

You can also add your devices in batch for convenience and automation.

-   Attach to the Zope container:

         serviced service attach zope

-   Create a text file (filename: `/tmp/batch.txt`) as follows:

         /Devices/Nutanix nutanix64 setManageIp='10.1.1.7', \ zNutanixUsername='username', \ zNutanixPassword='password'

-   Now run the zenbatchload command:

         zenbatchload /tmp/batch.txt

-   The device should now load and model automatically

## Install and Upgrade Instructions

If this is a new, clean install, no special actions are required.

When upgrade ZenPacks.zenoss.Nutanix from a version prior to 2.0.0, the
service 'zenjobs' must be stopped in order to fully complete the upgrade
to the latest version!
If you run the upgrade while zenjobs is running, a warning message will
appear. Please stop zenjobs and rerun the installation once more.

Alternatively, you can add the install job manually. If you have
previously successfully installed this version, no further action is
necessary.

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system:

### Configuration and zProperties

The zProperties and default settings are as follows:

-   zNutanixAlertsInterval: Interval to collect alerts; default 60
    seconds
-   zNutanixEventsInterval: Interval to collect events; default 60
    seconds
-   zNutanixPerfInterval: Interval to collect metric data; default 300
    seconds
-   zNutanixUsername: API username
-   zNutanixPassword: API password
-   zNutanixPort: API port; default 9440
-   zNutanixUseSSL: API SSL boolean; default True

### Modeler Plugins

-   zenoss.Nutanix

## Zenoss Analytics

This ZenPack provides additional support for Zenoss Analytics. Perform
the following steps to install extra reporting resources into Zenoss
Analytics after installing the ZenPack.

1.  Copy analytics-bundle.zip from
    $ZENHOME/ZenPacks/ZenPacks.zenoss.Nutanix\*/ZenPacks/zenoss/Nutanix/analytics/
    on your Zenoss server.

2.  Navigate to Zenoss Analytics in your browser.

3.  Log in as a superuser.

4.  Remove any existing *Nutanix_ZenPack* folder.

    > 1.  Choose *Repository* from the *View* menu at the top of the
    >     page.
    > 2.  Expand *Public* in the list of folders.
    > 3.  Right-click on *Nutanix_ZenPack* folder and choose *Delete*.
    > 4.  Confirm deletion by clicking *OK*.

5.  Add the new *Nutanix_ZenPack* folder.

    > 1.  Choose *Server Settings* from the &lsquo;&rsquo;Manage&rsquo; menu at the top of
    >     the page.
    > 2.  Choose *Import* in the left page.
    > 3.  Remove checks from all check boxes.
    > 4.  Click *Choose File* to import a data file.
    > 5.  Choose the analytics-bundle.zip file copied from your Zenoss
    >     server.
    > 6.  Click *Import*.

You can now navigate back to the *Nutanix_ZenPack* folder in the
repository to see the following resources added by the bundle.

Domains

-   Nutanix Domain

Domains can be used to create ad hoc views using the following steps.

1.  Choose *Ad Hoc View* from the *Create* menu.
2.  Click *Domains* at the top of the data chooser dialog.
3.  Expand *Public* then *Nutanix ZenPack*.
4.  Choose the *Nutanix Domain* domain

## Service Impact and Root Cause Analysis

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact and root cause analysis capabilities. The
service impact relationships shown in the diagram (right) and described
below are automatically added and maintained. These will be included in
any services that contain one or more of the explicitly mentioned
components.

The following object types would typically be added to Impact services.

-   NutanixVM
-   Linux or Windows devices associated with a NutanixVM

@lb[](img/zenpack-nutaniximpact.png)Impact
Relationship Diagram

### Internal Impact Relationships between Nutanix Components

-   NutanixEndpoint: impacts all NutanixHosts.
-   NutanixCluster: impacts NutanixVMs, NutanixStoragePools
-   NutanixHost: impacts NutanixCVMs
-   NutanixCVM: impacts NutanixCluster
-   NutanixHardDisk: impacts NutanixStoragePool
-   NutanixStoragePool: impacts NutanixContainers
-   NutanixContainers: impacts NutanixVdisks
-   NutanixVdisks: impacts NutanixVM

### Internal Impact Relationships between Nutanix Components

-   NutanixVM: impacts: GuestDevice (the hosted Linux or Windows system)

@lb[](img/zenpack-impactview.png)

## Changes

**2.0.1**

-   Fixed pulling critical events after the original ones are aged out
    (ZPS-7317)
-   Fixed generation of critical events when there are no changes in the
    Nutanix cluster (ZPS-7525)
-   Fixed modeling of a Nutanix 5.20 instances (ZPS-7703)
-   Tested with Zenoss Cloud, Zenoss Resource Manager 6.6.0, and Service
    Impact 5.5.5

**2.0.0**

-   Updated to be compatible with
    Nutanix Prism 5.15 LTS
-   Added incremental modeling
    support (ZPS-7013)
-   Corrected the relations between
    hosts, CVMs, VMs, and other components (ZPS-6823)
-   Updated the callhome routine to
    correctly count monitored systems (ZPS-5843)
-   Added Network Interface
    components, contained by hosts (ZSP-5625)
-   Updated component graphs to
    report bandwidth and latency, similar to the Nutanix console
    (ZPS-7095)
-   Correctly linking VMs to their
    devices in Zenoss (ZPS-7128)
-   Tested with Zenoss Resource
    Manager 6.4.1, 6.5, Zenoss Cloud and Impact 5.5.1

**1.0.3**

-   Fix relationships between CVMs
    &lt;-&gt; Hosts (ZPS-6676)
-   Fix flare in UI when Storage
    Summary Data is wrong (ZPS-5832)
-   Fix memory leak in zenpython
    caused by Nutanix datasource (ZPS-4701)
-   Tested with Zenoss Resource
    Manager 6.4.1, Zenoss Cloud, and Impact 5.5.1

**1.0.2**

-   Fix minor log warnings (ZPS-5620)
-   Fix incorrect datapoint for vm/cvm memory_usage_pct (ZPS-2904)
-   Fix unhandled plugin errors while monitoring (ZPS-3428)
-   Fix modeling when cluster uuid missing from API (ZPS-4189)
-   Tested with Zenoss Cloud, Zenoss 6.3.2, and Service Impact 5.3.4 ￼

**1.0.1**

-   Add debug info for modeler (ZPS-2310)
-   Guard for missing disk hw info (ZPS-2311)
-   Extend zCollectorClientTimeout to 600, optimize modeling (ZPS-2316,
    ZPS-2430)
-   Tested with Zenoss Resource Manager 5.3.2 & 6.0.0, Service Impact
    5.2.2, Analytics 5.0.8

**1.0.0**

-   Initial Release
-   Tested with Zenoss Resource Manager 5.2.6 & 5.3.1, Service Impact
    5.1.7, Analytics 5.0.8

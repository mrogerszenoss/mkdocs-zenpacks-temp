# Viptela SD-WAN Integration Service

@lb[](img/zenpack-viptela-logo.png)

## Subscription

This integration is a subscription-based Professional Services
engagement. Our Integration Services are offered as subscriptions in
order to provide initial setup and ongoing compatibility and
maintenance. All standard packages are renewable every 12 months from
the date of purchase. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks.

### Authors:

Zenoss Inc.

### Maintainers:

Zenoss Inc.

### Organization:

Zenoss Inc.

### Name:

Viptela SD-WAN Integration Service

**Version:**

1.11

## Viptela SD-WAN Integration Service

This ZenPack adds SNMP modeling/monitoring for Viptela vedge devices
Optionally a vManage device, acting as an endpoint, can use the Viptela
REST API to create events based on /dataservice/alarms and create/delete
Viptela devices (vedge, vbond, vsmart, vmanage) based on
/dataservice/device

##     Prerequisites

Zenoss RM 4.2.5 or greater

ZenPacks.zenoss.ZenPackLib 2.0.0 or greater

##     Configuration

### [vManage REST API](https://github.com/zenoss/ZenPacks.zenoss.PS.Viptela#id4){.external-link}

Add a vManage device to the DeviceClass /Network/Viptela/Endpoint. This
DeviceClass contains the devices which will be using the REST API
endpoint to discover available devices.

To enable discovery of other devices via the API, configure the
following zProperties for this Device.

#### [API Configuration](https://github.com/zenoss/ZenPacks.zenoss.PS.Viptela#id5){.external-link}

> -   zViptelaUsername and zViptelaPasswordNOTE: The values for these
>     properties are the same you would use to login to the UI of the
>     vManage device
>
> -   zViptelaURLSchemeWhether to use 'http' or 'https'
>
> -   zViptelaURLPortPort to use for API communication
>
> -   zViptelaBulkPageSizeused in alarm retrieval to specify how many to
>     load per request
>
> -   zViptelaHttpsCertValidationWhether to enforce certificate
>     checking. New in 1.10.3, previously used 'viptelahttpspolicy' in
>     global.conf. NOTE: if 'viptelahttpspolicy' was previously set to
>     False, then it will override the new zViptelaHttpsCertValidation
>     value.
>
> -   viptelahttpspolicy (default is blank or not present)This approach
>     has been deprecated starting since 1.10.3
>     and zViptelaHttpsCertValidation should be used to achieve the same
>     result. Add a configuration option in the global.conf of
>     zenpython, zenmodeler, zminion services. If the value is set to
>     "insecure", certificates checking on https connections to Viptela
>     Endpoint will be disabled. Like the name suggest this is insecure
>     and the proper work around is to add the necessary trusted roots
>     to Zenoss. Instead of editing global.conf in the 3 services
>     zenpython, zenmodeler, and zminion you can "Edit Variables" in
>     Control Center on the Zenoss Application like "Zenoss.resmgr" and
>     add the value "global.conf.viptelahttpspolicy insecure". Any
>     change requires a restart of zenpython, zenmodeler, zminion
>     services to pick up that change.

#### [IP Address Selection](https://github.com/zenoss/ZenPacks.zenoss.PS.Viptela#id6){.external-link}

Selecting the proper IP address for SNMP monitoring is critical as most
interfaces on the devices will likely not be accessible from the Zenoss
collector.

The default is to select the address that closest matches the vManage
device, based on comparison of the network octets.

Optionally, the IP address can be targeted based on interface name for
the selected device types.

> -   zViptelaDeviceTypesSnmpIp(Default: "vsmart,vbond") Which device
>     types to apply interface matching against.
>
> -   zViptelaManageIpInterfaceNames:List of regex expressions to apply
>     on interface name. The name matched on first expression will be
>     used.

#### [DeviceClass mapping](https://github.com/zenoss/ZenPacks.zenoss.PS.Viptela#id7){.external-link}

Where to create Viptela device types

> -   zViptelaVEdgeDeviceClassdefault /Network/Viptela/VEdge
>
> -   zViptelaVSmartDeviceClassdefault /Network/Viptela/VSmart
>
> -   zViptelaVManageDeviceClassdefault /Network/Viptela/VManage
>
> -   zViptelaVBondDeviceClassdefault /Network/Viptela/VBond

#### [Device Discovery](https://github.com/zenoss/ZenPacks.zenoss.PS.Viptela#id8){.external-link}

During discovery unreachable devices may be skipped ('reachability'
value from api call "/dataservice/device")

> -   zViptelaIgnoreUnreachableDevice(Default: False) Whether or not to
>     discover unreachable device
>
> -   zViptelaIgnoreAFTypesList of interface AF Types to ignore during
>     discovery

### [Device SNMP Configuration](https://github.com/zenoss/ZenPacks.zenoss.PS.Viptela#id9){.external-link}

Typical SNMP device configuration is needed for Viptela devices. Set
this on the device classes so that added devices will pick up the
configuration.

### [ViptelaAlarmDataSource Configuration](https://github.com/zenoss/ZenPacks.zenoss.PS.Viptela#id10){.external-link}

> -   Query(default is Viptela alarms occurring in the last 3 hours)
>     Defines the value of the "query" parameter posted to
>     /dataservice/alarms. Refer to Viptela documentation on what Value
>     are acceptable to the Viptela API.
>
> -   Enable Debug Events(default is disabled) If enabled, creates an
>     event with Severity Debug listing Viptela Alarm Plugin Stats like
>     how many alarms were collected from Viptela endpoint, how many
>     were turned into events and how many were skipped.

##     Changelog

1.11.0

-   Model Interface Address Family Type in `ViptelaInterface` modeler
    plugin
-   Add `zViptelaIgnoreUnreachableDevice` to not discover unreachable
    device
-   Add `zViptelaIgnoreAFTypes` to not discover listed interface AF
    Types

1.10.6

-   Fix device class assignment bug in `ViptelaModelJob`

1.10.5

-   Fix encoding error in `ViptelaTunnel` modeler plugin
-   Update `ViptelaModelJob` to search for endpoint by id

1.10.4

-   Update `ViptelaModelJob` to support new version of zenjobs
-   Add `zViptelaManageIpInterfaceNames` for setting manage ip based on
    interface name
-   Update docs

1.10.3

-   Update https certificates verification

1.10.2

-   Add`endpoint_uuid`during device creation

1.10.1

-   Fix to handle correctly float 'timeout' value in easysnmp

1.10.0

-   Allow changing Viptela Device ID's without impacting Discovery from
    Endpoint Devices. Previously the Device IDs were used, causing
    Discovery to break if the Device ID was changed.

1.9.2

-   Add "Enable Debug Events" option to ViptelaAlarmDataSource
-   Add ability to ignore certificate checking on https connections to
    Viptela Endpoint

1.9.1

-   Create MIB Organizer "Viptela"

-   Add MIBs VIPTELA-APP-ROUTE, VIPTELA-BFD, VIPTELA-BRIDGE,
    VIPTELA-DOT1X, VIPTELA-GLOBAL, VIPTELA-HARDWARE, VIPTELA-OMP,
    VIPTELA-OPER-BGP, VIPTELA-OPER-MULTICAST, VIPTELA-OPER-OSPF,
    VIPTELA-OPER-SYSTEM, VIPTELA-OPER-VPN, VIPTELA-POLICY,
    VIPTELA-SECURITY, VIPTELA-TRAPS, VIPTELA-WLAN, VIPTELA-WWAN to
    Viptela MIB organizer

    Note: Dependent MIBs SNMPv2-SMI and SNMPv2-TC may need to be
    manually added

-   The query parameter sent to Viptela Alarms webservice is now
    configurable

-   New modeler zenoss.snmp.ViptelaDevice for modeling the vEdge device
    HW TotalMemory

1.9.0

-   Add SNMP modeling and monitoring for vedge devices
-   Discontinue using REST API except for Alarms and Device Discovery
-   Remove a viptela device if it was added by endpoint and is no longer
    included in the REST API results
-   Split vedge Interface graph into 3 graphs
-   Modernize to use ZenPackLib 2.0

1.7.0

-   Wrap modeler plugin and zenviptela doTask to generate events for
    uncaught exceptions
-   Change interface RRD type to GAUGE
-   Change zenviptela hub service base class to not inherit unneeded
    features from the collector framework
-   Hub service to cache proxies for up to 6 hours
-   Alarms include full data returned by vManage

1.6.0

-   Handle missing object ID
-   Change bulk stats look back to 30 minutes
-   Set RRD step for interface stats to 10 minutes
-   Replace CPU stats with load average
-   Set zenviptela RRD heartbeat to 6 \* step

1.5.0

-   Move all Viptela API calls to use bulk state and statistics APIs
-   Remove calls which lack bulk API calls:
    -   get_tunnels_stats
    -   get_tunnels
    -   get_hardware_health
    -   System Status mem_total
    -   BGP neighbor perf
    -   Hardware perf
-   Set manufacturer/product to Viptela/device-type
-   Use standard serial number field
-   Flatten device hierarchy and use "Endpoint" sub-class for vManage
    -   vManage devices still added as non-endpoints to /Network/Viptela

## Components Modeled

-   PS
-   ControlConnection
-   Tunnel
-   Temperature Sensor
-   Fan
-   Interface
-   BGP Neighbor

## Device Class Templates

### Devices/Network/Viptela/VBond

-   Orchestrator
    -   Graphs
        -   VBond Connections
    -   Thresholds
        -   VEdge Warning Count
    -   Datapoints
        -   vsmart_counts
        -   vmanage_counts
        -   vedge_counts

### Devices/Network/Viptela

-   VipBGPNeighbor
    -   Thresholds
        -   bgp state
    -   Datapoints
        -   bgpBgpNeighborState
        -   bgp_msg_rcvd
        -   bgp_msg_sent
        -   bgp_outQ
-   VipFan
    -   Thresholds
        -   fan state
    -   Datapoints
        -   hardwareEnvironmentStatus
-   VipSystemStatus
    -   Graphs
        -   Disk
        -   Load Average
        -   Memory
    -   Datapoints
        -   systemStatusMin15Avg
        -   systemStatusMemUsed
        -   systemStatusDiskAvail
        -   systemStatusMin1Avg
        -   systemStatusMemFree
        -   systemStatusMin5Avg
        -   systemStatusDiskUsed
-   VipInterface
    -   Graphs
        -   Drops and Errors
        -   Packets
        -   Octets
    -   Datapoints
        -   if-admin-status
        -   if-oper-status
        -   interfaceRxPackets
        -   interfaceTxPackets
        -   interfaceTxErrors
        -   interfaceRxOctets
        -   interfaceRxErrors
        -   interfaceRxDrops
        -   interfaceTxOctets
        -   interfaceTxDrops
-   VipTemperature
    -   Thresholds
        -   temperature state
    -   Datapoints
        -   hardwareEnvironmentStatus
-   VipConnection
    -   Thresholds
        -   control connection state
    -   Datapoints
        -   controlConnectionsState
-   VipTunnel
    -   Thresholds
        -   tunnel state
    -   Datapoints
        -   bfdSessionsListState
-   VipPS
    -   Thresholds
        -   ps state
    -   Datapoints
        -   hardwareEnvironmentStatus

## Attachments:

-   [viptela-logo.png](img/zenpack-viptela-logo.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/PS/zenoss-integration-services-ds.pdf){.external-link}
-   [viptela-logo.png](img/zenpack-viptela-logo.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/PS/zenoss-integration-services-ds.pdf){.external-link}
-   [viptela-logo.png](img/zenpack-viptela-logo.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/PS/zenoss-integration-services-ds.pdf){.external-link}
-   [viptela-logo.png](img/zenpack-viptela-logo.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/PS/zenoss-integration-services-ds.pdf){.external-link}
-   [viptela-logo.png](img/zenpack-viptela-logo.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/PS/zenoss-integration-services-ds.pdf){.external-link}
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/PS/zenoss-integration-services-ds.pdf){.external-link}


# Infoblox Integration Service

## [About](https://github.com/zenoss/ZenPacks.zenoss.PS.Infoblox#id1){.external-link}

This ZenPack provides the ability to model and monitor Infoblox
appliances.This ZenPack will automatically discover, model grid members
during the modeling of grid master device.

| Prerequisite       | Restriction                                                   |
|--------------------|---------------------------------------------------------------|
| Product            | Zenoss 6.x and higher                                         |
| Required ZenPacks  | ZenPacks.zenoss.ZenPackLib&gt;= 2.1.1 ZenPacks.zenoss.PS.Util |
| Other dependencies | None                                                          |

## [Installing](https://github.com/zenoss/ZenPacks.zenoss.PS.Infoblox#id2){.external-link}

After satisfying the dependency requirements above, install the ZenPack
via the command line as per the Zenoss Admin Guide matching your Zenoss
version.

## [Device Classes](https://github.com/zenoss/ZenPacks.zenoss.PS.Infoblox#id3){.external-link}

-   /Network/Infoblox

## [Components Modeled](https://github.com/zenoss/ZenPacks.zenoss.PS.Infoblox#id4){.external-link}

-   DHCP Network
-   DNS Zones
-   Fans
-   Grid
-   Nodes
-   PowerSupplies
-   Services
-   Networks

During modeling of grid master device, all grid member devices will be
automatically added to the zenoss. Due to the fact that only after
modeling devices the grid master will be determined, in order to enable
Network component grid master should be modeled twice.

## [Modelers](https://github.com/zenoss/ZenPacks.zenoss.PS.Infoblox#id5){.external-link}

-   Genericzenoss.snmp.InterfaceMapzenoss.snmp.DeviceMap

-   InfobloxDevicezenoss.snmp.InfoBloxGridMapzenoss.snmp.DnsZoneMapzenoss.cmd.InfobloxLicensezenoss.snmp.InfoBloxDHCPMapzenoss.snmp.InfoBloxNodeMapzenoss.snmp.InfobloxDevicezenoss.http.InfobloxNetwork

## [Device / Component Metrics](https://github.com/zenoss/ZenPacks.zenoss.PS.Infoblox#id6){.external-link}

-   InfobloxDevice DeviceCPU UsageMemory UsageDNS hit ratioDNS query
    rateLatency for DNS queries

-   DHCP NetworkDHCP Utilization

-   DnsZoneMapSuccessful responesDNS referralsDNS queries
    statisticsRecursive queriesFailed queries

-   FanStatus

-   NodeCPU TemperatureSystem TemperatureDisk UsageDatabase capacity
    usage

-   Power SupplyStatus

-   ServiceStatus

-   InfobloxNetworkIPAM Utilization

## [Thresholds](https://github.com/zenoss/ZenPacks.zenoss.PS.Infoblox#id7){.external-link}

-   CPUHigh CPU usage

-   MemoryHigh Memory usage

-   DnsZoneMaphigh_ibBindZoneSuccesshigh_ibBindZoneReferralhigh_ibBindZoneNxDomainhigh_ibBindZoneNxRRsethigh_ibBindZoneRecursionhigh_ibBindZoneFailure

-   Nodehigh_node_cpu_temphigh_node_temphigh_node_disk_usagehigh_node_database_capacity

-   DHCP Networkhigh_subnet_utilization

-   NetworkHigh utilization

## [Configuration](https://github.com/zenoss/ZenPacks.zenoss.PS.Infoblox#id8){.external-link}

Typical SNMP device configuration. Modeler
plugin `zenoss.cmd.InfobloxLicense` requires SSH credentials to be set
i.e: `zCommandUsername`, `zCommandPassword`. Networks are being
monitored via Infoblox WAPI,
so `zInfobloxWAPIUsername`, `zInfobloxWAPIPassword`, `zInfobloxWAPIUseHttps`, `zInfobloxWAPIPort` must
be set to correct values.

## [Change Log](https://github.com/zenoss/ZenPacks.zenoss.PS.Infoblox#id9){.external-link}

Release 1.0.3

-   Fixes

    -   Add check for existing grid members during grid members
        discovery

Release 1.0.2

-   Fixes

    -   Fix for InfoBloxGridMap modeler plugin to work with Version 6.4
        and higher

Release 1.0.1

-   Features

    -   Use new MibLoader for importing MIBs (required for Version 6.3)
        New Dependency: Requires ZenPacks.zenoss.PS.Util ZenPack

Release 1.0.0

-   Features
    -   Infoblox device modeling and monitoring
    -   DHCP Network, DNS Zones, Fans, Grid, Nodes, PowerSupplies,
        Services, Networks modeling and monitoring
    -   Grid members discovery



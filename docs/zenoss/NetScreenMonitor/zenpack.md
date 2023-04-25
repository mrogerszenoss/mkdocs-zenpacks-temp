# Juniper NetScreen

@lb[](img/zenpack-juniper-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.NetScreenMonitor

This ZenPack provides support for monitoring Juniper NetScreen devices.

## [Releases](#releases){.toc-backref}

**Version 2.2.3** [Download](https://zenoss.leapfile.net/){.external-link}:

    Released on 2017/01/12

    Compatible with Zenoss Resource Manager 4.2.5 - 5.1.x

    Summary of Changes:

    > -   Add monitoring and locking to VPN tunnels

**Version 2.2.2** [Download](https://zenoss.leapfile.net/){.external-link}:

    Released on 2016/09/16

    Compatible with Zenoss Resource Manager 4.2.5 - 5.1.x

    Summary of Changes:

    > -   Add common datapoint aliases

**Version 2.2.1** [Download](https://zenoss.leapfile.net/){.external-link}:

    Released on 2015/11/10

    Compatible with Zenoss Resource Manager 4.2.5 - 5.1.x

    Summary of Changes:

    > -   Add total memory modeling
    > -   Adjust free memory thresholds
    > -   Add common datapoint aliases

Contents

-   Releases
-   [Background](#background-this-zen-pa-ckmonitors-juniper-net-screen-devices-using-the-snmp-v2-protocol){.reference     .internal}
-   Features
-   Installation and
    Configuration
-   Changes

## [Background](#background){.toc-backref}

This ZenPack monitors Juniper NetScreen devices using the SNMP v2
protocol.

## [Features](#features){.toc-backref}

-   Overall statistics for interfaces, routes, and vpn tunnels

## Devices Monitored

This ZenPack monitors devices from Juniper's NetScreen line of products.
Models supported include:

-   Juniper SSG-140 version 6.2.0, Firewall+VPN
-   Juniper SSG-140 version 6.3.0, Firewall+VPN
-   Juniper SSG-320M version 6.3.0, Firewall+VPN
-   Juniper SSG-550 version 6.2.0, Firewall+VPN
-   Juniper SSG-550 version 6.3.0, Firewall+VPN
-   Juniper SSG20 version 6.2.0, Firewall+VPN
-   Juniper SSG20-WLAN version 6.3.0, Firewall+VPN
-   Juniper SSG5-Serial version 6.3.0, Firewall+VPN
-   Juniper SRX1500 internet router, kernel JUNOS 15.1X49-\*
-   NetScreenISG 1000 version 6.3.0, Firewall+VPN
-   NetScreenISG 2000 version 6.3.0, Firewall+VPN

## Modeler Plugins

-   snmp.netscreen.NetScreenDeviceMap
-   zenoss.snmp.DeviceMap
-   snmp.netscreen.InterfaceMap
-   zenoss.snmp.RouteMap
-   NetScreenVPN

## Datasource Types

-   SNMP

## Monitoring Templates

-   NetScreenDevice
-   VPNTunnel
-   netscreenInterface

## Device

-   Datapoints: (Format: \[datasource.point:     DatasourceType.DataPointType\]):
    -   cpuAvg.cpuAvg: SNMP.Gauge
    -   cpuLast1Min.cpuLast1Min: SNMP.Gauge
    -   cpuLast5Min.cpuLast5Min: SNMP.Gauge
    -   cpuLast15Min.cpuLast15Min: SNMP.Gauge
    -   freeMemory.freeMemory: SNMP.Gauge
    -   sessAllocate.sessAllocate: SNMP.Gauge
    -   sessMaximum.sessMaximum: SNMP.Gauge
    -   usedMemory.usedMemory: SNMP.Gauge

## Components

The following components are monitored:

### Interfaces

-   Datapoints: (Format: \[datasource.point:     DatasourceType.DataPointType\]):
    -   ifHCInOctets.ifHCInOctets: SNMP.Derive
    -   ifHCInUcastPkts.ifHCInUcastPkts: SNMP.Derive
    -   ifHCOutOctets.ifHCOutOctets: SNMP.Derive
    -   ifHCOutUcastPkts.ifHCOutUcastPkts: SNMP.Derive
    -   ifInOctets.ifInOctets: SNMP.Derive
    -   ifInUcastPackets.ifInUcastPackets: SNMP.Derive
    -   ifOutOctets.ifOutOctets: SNMP.Derive
    -   ifOutUcastPackets.ifOutUcastPackets: SNMP.Derive
-   Graphs:
    -   Throughput
    -   Packets
    -   Errors
-   Thresholds:
    -   High Utilization
    -   ifOperStatusChange

### Network Routes

Network Routes are provided by the native zenoss.snmp.RouteMap modeler
plugin and link to the Zenoss networking/routing facility.

-   Properties:
    -   Interface Description
    -   Address/Mask
    -   Device
    -   Interface
    -   Mac Address
    -   Ping Status
    -   SNMP Status

### VPN Tunnels

-   Datapoints: (Format: \[datasource.point:     DatasourceType.DataPointType\]):
    -   avail.avail: SNMP.Gauge
    -   bytesIn.bytesIn: SNMP.Counter
    -   bytesOut.bytesOut: SNMP.Counter
    -   delayAvg.delayAvg: SNMP.Gauge
    -   inSpi.inSpi: SNMP.Counter
    -   monState.monState: SNMP.Gauge
    -   outSpi.outSpi: SNMP.Counter
    -   p1State.p1State: SNMP.Gauge
    -   p2State.p2State: SNMP.Gauge
    -   packetsIn.packetsIn: SNMP.Counter
    -   packetsOut.packetsOut: SNMP.Counter
    -   tunnelState.tunnelState: SNMP.Gauge
-   Graphs:
    -   Throughput
    -   Packets
    -   SPI
-   Thresholds:
    -   Phase 1 Inactive
    -   Phase 2 Inactive
    -   Tunnel Down

## [Installation and Configuration](#installation-and-configuration){.toc-backref}

## ZenPack Installation

-   Install the NetScreenMonitor ZenPack as per Resource Manager
    documentation
-   Restart all required Zenoss Services as per Resource Manager
    documentation
-   Install the target device, as follows:

## Manual Target Device Installation

1.  Navigate to the Infrastructure and hit the + button to add a device
2.  Fill in the following entries:
    -   Hostname or IP Address
    -   Device Class: /Network/NetScreen
    -   Title
3.  Click "More" and fill in the following entries:
    -   Snmp Community
    -   Snmp Port (defaults to 161)
4.  Click Add
5.  Ensure zenperfsnmp is running
6.  Navigate to Graphs and you should see some placeholders for graphs.
    After approximately fifteen minutes you should see the graphs start
    to become populated with information.

## Batch Target Installation with **zenbatchload**

You can also add your devices in batch for convenience and automation.

-   Create a text file (filename: /tmp/netscreen.txt). Each server has
    an entry similar to:

    ~~~ literal-block
    /Devices/Network/NetScreen
    netscreen setManageIp='10.1.1.1', \
              zSnmpCommunity='public', \
              zSnmpVer='v2c'
    ~~~

-   Run the command on the terminal:

    ~~~ literal-block
    zenbatchload /tmp/netscreen.txt
    ~~~

## Model the Component

-   From the device view, select **Model Device** from the gear menu.

## [Changes](#changes){.toc-backref}

## 2.2.3

-   Add monitoring and locking to VPN tunnels (ZPS-603)

## 2.2.2

-   Add common datapoint aliases (ZEN-24619)

## 2.2.1

-   Add total memory modeling
-   Change free memory threshold to 10% of total
-   Add common datapoint aliases (ZEN-24619)

## Attachments:

-   [juniper-zenpack.png](img/zenpack-juniper-zenpack.png)
-   [juniper-zenpack.png](img/zenpack-juniper-zenpack.png)


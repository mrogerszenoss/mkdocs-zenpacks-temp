# Cumulus Integration Service

## Description

This ZenPack adds monitoring for Cumulus routers. Cumulus is a linux
distribution, specialized for network routing, which can run on general
purpose compute hardware.

## Prerequisites

<table>
<thead>
<tr markdown="1">
<th>Prerequisite</th>
<th>Restriction</th>
</tr>
</thead>
<tbody>
<tr markdown="1">
<td>Product</td>
<td>Zenoss 6.4 or higher</td>
</tr>
<tr markdown="1">
<td>Required ZenPacks</td>
<td><p>ZenPacks.zenoss.RoutingProtocols&gt;=1.7.0</p>
<p>ZenPacks.zenoss.ZenPackLib&gt;=2.1.1</p>
<p>ZenPacks.zenoss.PS.Util&gt;=1.10.0</p></td>
</tr>
<tr markdown="1">
<td>Other dependencies</td>
<td>None</td>
</tr>
</tbody>
</table>

## Configuration

This ZenPack supports SNMP for collecting modeling data and metrics for
the Cumulus devices.

SNMP polling is configurable with standard Zenoss functionality.

### Modeler Plugins

This ZenPack adds 5 new SNMP modeler plugins, and uses 5 standard SNMP
modeler plugins. The new modeler plugins that are added are:

> -   zenoss.snmp.CumulusRouterMapModels most of the physical entities
>     that make up the switch, including the chassis, fans, power
>     supplies and temperature sensors
>
> -   zenoss.snmp.CumulusBGPNeighborMapModels the BGP neighbors. Mostly
>     inherited from the RoutingProtocols ZenPack, but adjusted to use
>     the Cumulus-specific BGP neighbor table
>
> -   zenoss.snmp.CumulusProcessorMapModels the processors (CPUs) in the
>     physical chassis
>
> -   zenoss.snmp.CumulusInterfaceMapOverrides the existing InterfaceMap
>     plugin to allow the interface speed to be editable.
>
> -   zenoss.snmp.CumulusInterfaceAliasMapOverrides the existing
>     InterfaceAliasMap plugin to allow the interface speed to be
>     editable.

## Adding Devices

Add devices as you normally would to the /Network/Cumulus device class.
The SNMP credentials will need to be set on either the device or the
device class.

## Events

There are status thresholds for Fans, Power Supplies, Temperature
Sensors and Processors (CPUs). For Fans, Power Supplies and Temperature
Sensors, the mapping from the SNMP value to event severity is:

> -   SNMP value: 1, Event severity: 0 (Clear)Indicates the component is
>     working properly
>
> -   SNMP value: 2, Event severity: 3 (Warning)Indicates the status is
>     unknown
>
> -   SNMP value: 3, Event severity: 5 (Critical)Indicates the component
>     has failed

Processors have a different mapping:

> -   SNMP value: 1, Event severity: 3 (Warning)Indicates the status is
>     unknown
>
> -   SNMP value: 2, Event severity: 0 (Clear)Indicates the processor is
>     working properly
>
> -   SNMP value: 3, Event severity: 3 (Warning)Indicates that there has
>     been an error reported by the OS, but the processor is still
>     operational
>
> -   SNMP value: 4, Event severity: 3 (Warning)Indicates that the
>     processor is in the testing state
>
> -   SNMP value: 5, Event severity: 5 (Critical)Indicates that the
>     processor has failed

The monitoring template for interfaces is identical to the standard
ethernetCsmaCd template, with the exception of the threshold for
interface utilization. The default, used if the interface speed is
unknown, is 2 \*\* 64 - 1, which is the largest possible value for a 64
bit integer, instead of the previous default of 1e9 (1 Gbps). Since
these devices have 40Gbps physical interfaces, having logical interfaces
breach the threshold of 1 Gbps would cause too many unneccesary events.

## Changelog

1.0.0

> -   Initial release

1.0.1

-   SVC-3361 Prevent traceback when device doesn't report chassis info



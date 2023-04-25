# Aruba Integration Service

## [Description](https://github.com/zenoss/ZenPacks.zenoss.PS.Aruba#id1){.external-link}

This ZenPack is to monitor Aruba Network Devices and retrieve
information about the Access Points, Radios, and Clients connected to
them. Base hardware components(in case they are accessible) are
available as well: Fan, Storage, Processor, Memory, Power Supply.

| Prerequisite       | Restriction                                                             |
|--------------------|-------------------------------------------------------------------------|
| Product            | Zenoss 6.x and higher                                                   |
| Required ZenPacks  | ZenPacks.zenoss.ZenPackLib&gt;= 2.0, ZenPacks.zenoss.PS.Util&gt;= 1.1.1 |
| Other dependencies | None                                                                    |

## [Installing](https://github.com/zenoss/ZenPacks.zenoss.PS.Aruba#id2){.external-link}

After satisfying the dependency requirements above, install the ZenPack
via the command line as per the Zenoss Resource Manager Admin Guide
matching your Zenoss RM version.

## [Device Classes](https://github.com/zenoss/ZenPacks.zenoss.PS.Aruba#id3){.external-link}

These Device Classes are added for Devices:

-   /Network/Aruba/Controller
-   /Network/Aruba/Instant
-   /Network/Aruba/AMPSwitch
-   /Network/Aruba/HPSwitch
-   /Network/Aruba/CPPM
-   /Network/Aruba/AMS

## [Aruba Mobility Controllers](https://github.com/zenoss/ZenPacks.zenoss.PS.Aruba#id4){.external-link}

(/Network/Aruba/Controller)

For standalone Aruba Controllers, the following items are modeled as
components:

-   Connected APs
-   AP Radio Stats
-   Connected Stations (optional)
-   Interfering APs / Monitored APs (optional)
-   Users (optional)
-   Authentication Servers

## [Aruba Instant Virtual Controllers](https://github.com/zenoss/ZenPacks.zenoss.PS.Aruba#id5){.external-link}

(/Network/Aruba/Instant)

Rather than using a standalone controller, the Aruba Instant series
selects one of the Access Points in the network to be a Virtual
Controller. This AP then provides configuration and monitoring for the
network. Note that Access Points that are not currently selected as the
Virtual Controller provide much less data, none about other devices.
However, if the Virtual Controller changes this will be detected on the
next modeling of the devices.

-   Access Points connected to the Virtual Controller
-   Controller BSSIDs
-   Users (optional)

## [Aruba AMP Switches](https://github.com/zenoss/ZenPacks.zenoss.PS.Aruba#id6){.external-link}

(/Network/Aruba/AMPSwitch)

For standalone Aruba AMP Switches, the following items are modeled as
components:

-   Power supplies
-   Fans
-   Storages
-   Processors
-   Memory
-   Users
-   Authentication Servers

## [Aruba HP Switches](https://github.com/zenoss/ZenPacks.zenoss.PS.Aruba#id7){.external-link}

(/Network/Aruba/HPSwitch)

For standalone Aruba HP Switches, the following items are modeled as
components:

-   Power supplies
-   Fans
-   Storages
-   Memory
-   Users
-   Authentication Servers

## [Aruba AMS(Airwave Management System) & CPPM(ClearPass Policy Manager)](https://github.com/zenoss/ZenPacks.zenoss.PS.Aruba#id8){.external-link}

These device classes don't provide specific metrics for AMS/CPPM
devices, however templates from parent device classs can be leveraged.

## [Changelog](https://github.com/zenoss/ZenPacks.zenoss.PS.Aruba#id9){.external-link}

2.1.1

-   Fix value parsing for ArubaSwitchMemory Modeler
-   Cleanup display labels in component names

2.1.0

-   add new components: Power supply, Fan, Storage, Memory, Processor
-   add new device classes: AMS&HP Switch, AMS, CPPM.

2.0.0

-   transition to ZPL 2.0
-   Rename ZenPack to ZenPacks.zenoss.PS.Aruba

1.0.0

-   add /Network/Aruba/Controller and /Network/Aruba/Instant device
    classes
-   base zenpack definition



# Arista Integration Service

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

Arista Integration Service

**Version:**

1.4.0

This ZenPack adds Device monitoring for Arista Switches

## Adding Devices

Add Devices to the /Network/Switch/Arista DeviceClass. If necessary,
configure SNMP settings as with any SNMP monitored device. Once
configured, Model the device.

## Changes

Release 1.4.0

-   Features
    -   SVC-3041 Add thresholds for Temperature Sensors
    -   SVC-3055 Add Interface Utilization graphs to
        AristaInterfaceTemplate
    -   SVC-3056 Add UtilizationPercentage graph in AristaMemoryTemplate
    -   SVC-3060 Add default threshold in the AristaMemoryTemplate
    -   SVC-3078 Add support for VRF and for BGP where neighbors are
        inside of a VRF
    -   SVC-3096 Monitor BGP Peer State - Alert when changed from
        Established

Release 1.3.0

-   Features
    -   Replace AristaGenericSensorTemplate with individual templates
        for components
        -   AristaFanSensorTemplate
        -   AristaPowerSensorTemplate

Release 1.2.0

-   Features
    -   Enhanced Interface Statistics
        -   Add Graphs HighSpeed, HighSpeedOctets, and HighSpeedPackets
            based on OIDs in ifXTable from IF-MIB
        -   Add Graphs EtherOctets and EtherPackets based on OIDs in
            etherStatsTable from RMON-MIB
    -   Interface title / name value comes from ifXTable ifName
    -   Arista Device now impacted by Arista Interfaces
-   Bug fixes
    -   Fix broken Impact relations for chassis, fans, and powersupplies
    -   Change zPingMonitorIgnore from true to false

Release 1.1.0

-   Features
    -   Component Titles - Use snmpindex for generating component
        titles.
    -   Temperature Sensor - Add template and scale graphs to display
        degrees Celsius instead of tenths-degree.

Release 1.0.1

-   Features
    -   Interface - Title changed from "ifName + ifDescr" to "ifName"
        after remodel.

Release 1.0.0

-   Features

    -   New Device Arista - OS version, contact, description, location,
        serial number, manufacturer

    -   New Components

        -   BGPPeer - Admin status, operational state, peer description,
            local/remote AS, uptime/downtime in secondsValue Change
            Threshold on operational state datapointGraph of BGP Peers
            prefix counters using address family IPv4 unicast (AFI 1
            SAFI 1)

        -   Chassis - Description

        -   Cpu - DescriptionGraph of LoadNote: First CPU component is
            an average of subsequent cores

        -   Fan - Description, number of fan sensors

        -   Fan Sensor - Description, link to monitored fan, sensor
            type, sensor units, operation statusGraph of current reading

        -   Interface - Description, alias, admin status, operational
            statusGraph of Octets (In/Out)Graph of Packets (In/Out)Graph
            of Discards and Errors (In/Out)Graph of Speed

        -   Memory - Description, Total, UsedGraph of utilization

        -   Power Sensor - Description, sensor type, sensor units,
            operation statusGraph of current reading

        -   Power Supply - Description

        -   Temperature Sensor - Description, sensor type, sensor units,
            operation statusGraph of current reading



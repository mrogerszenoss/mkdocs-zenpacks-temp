# Cisco UCS Central

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.CiscoUCSCentral

### Applications Monitored:

Cisco UCS Central (1.3)

## Cisco UCS Central ZenPack

Cisco UCS Central Infrastructure monitoring.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 1.3.3- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2019/10/04:   Requires [PythonCollector ZenPack](http://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},[Cisco UCS ZenPack](http://help.zenoss.com/display/in/Cisco+UCS "ZenPack:Cisco UCS"){.external-link}:   Compatible with Zenoss 6.2 - 6.3 and Zenoss Cloud

<!-- -->

Version 1.2.0- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2015/12/11:   Requires [PythonCollector ZenPack](http://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},[CiscoUCS ZenPack](http://help.zenoss.com/display/in/ciscoucs-page-does-not-exist "ZenPack:CiscoUCS (page does not exist){.external-link}"){.external-link}:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x

<!-- -->

Version 1.0.0- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2015/07/09:   Requires [PythonCollector ZenPack](http://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},[Cisco UCS ZenPack](http://help.zenoss.com/display/in/Cisco+UCS "ZenPack:Cisco UCS"){.external-link}:   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x

## Background

This ZenPack provides support for monitoring the [Cisco UCS Central Infrastructure](http://www.cisco.com/c/en/us/products/servers-unified-computing/ucs-central-software/index.html){.external-link}
via the [Cisco UCS Central XML API](http://www.cisco.com/c/en/us/td/docs/unified_computing/ucs/ucs-central/api/b_UCSC_XML_API_book/b_UCSC_XML_API_book_chapter_01.html){.external-link}.

## Features

This ZenPack adds the following features to Zenoss.

-   Initial discovery and continual update of relevant components.
-   Event management. Integration of Cisco UCS Central faults into
    Zenoss event system.
-   Event subscription. Automatic updates for predefined components.

## Discovery

@lb[](img/zenpack-cisco_ucsc_model_yuml.png)

Model Diagram

The following components will be automatically discovered. The
properties and relationships will be periodically remodeled to provide
automatically up-to-date monitoring when the system configuration
changes.

@lb[](img/zenpack-cisco_ucsc_overview.png)

UCS Central Device

Cisco UCS Central Device:   Properties: Name, UCS Distinguished Name (DN), Mode, Uptime,
    Available Servers, Polling Interval, Total Servers:   Relationships: Domain Groups, UCS Domains, Servers, Global Service
    Profiles, Local Service Profiles, Global Service Profile Templates,
    Local Service Profile Templates

@lb[](img/zenpack-cisco_ucsc_domain_groups.png)

Domain Groups

Domain Groups:   Properties: Name, Distinguished Name (DN), Description:   Relationships: Cisco UCS Central Device, UCS Domains, Servers,
    Global Service Profiles, Local Service Profiles

@lb[](img/zenpack-cisco_ucsc_ucs_domains.png)

UCS Domains

UCS Domains:   Properties: Name, Domain Group, Platform, UCS Management IP, Total
    Servers, Free Servers, Inventory Status, Last Refresh, Grace Period
    Used, Connection State, License State, Oper State, Suspend State,
    Version, Owner:   Relationships: Cisco UCS Central Device, Domain Groups, Servers,
    Local Service Profiles

@lb[](img/zenpack-cisco_ucsc_servers.png)

Servers

Servers:   Properties: Name, UCS Manager Server, Server ID, Model, Oper State,
    Oper Power, Availability, Association, Operability:   Relationships: Cisco UCS Central Device, Domain Groups, UCS Domains,
    Global Service Profiles, Local Service Profiles

@lb[](img/zenpack-cisco_ucsc_global_service_profiles.png)

Global Service Profiles

Global Service Profiles:   Properties: Name, UCS Manager Global Service Profile, Assigned
    State, Associated State, Oper State, Config State:   Relationships: Cisco UCS Central Device, Domain Groups, Servers,
    Global Service Profile Templates

@lb[](img/zenpack-cisco_ucsc_local_service_profiles.png)

Local Service Profiles

Local Service Profiles:   Properties: Name, Distinguished Name (DN), Instantiation State, Oper
    State, Assigned State, Associated State, Config State, System Name,
    Description:   Relationships: Cisco UCS Central Device, Domain Groups, UCS Domains,
    Servers, Local Service Profile Templates

@lb[](img/zenpack-cisco_ucsc_global_service_profile_templates.png)

Global Service Profile Templates

Global Service Profile Templates:   Properties: Name, Distinguished Name (DN), Assigned State,
    Associated State, Config State:   Relationships: Cisco UCS Central Device, Global Service Profiles

@lb[](img/zenpack-cisco_ucsc_local_service_profile_templates.png)

Local Service Profile Templates

Local Service Profile Templates:   Properties: Name, Distinguished Name (DN), Instantiation State,
    Placement Count:   Relationships: Cisco UCS Central Device, Local Service Profiles

## Event Management

### Cisco UCS Central Faults

Zenoss periodically polls the UCS Central for faults and creates Zenoss
events when they occur. The UCS Central fault life-cycle closely matches
that of a Zenoss event. This means that corresponding Zenoss events will
automatically clear when their UCS Central fault counterparts clear.

**Note:** UCS Central fault events may reoccur in Zenoss if they're
closed in Zenoss, but not cleared on the UCS Central. For this reason it
is recommended that the UCS Central fault events are acknowledged in
Zenoss instead of closed until they are actually resolved on the UCS
Central system.

**Note:** Zenoss attempts to set the timestamp on fault events to the
timestamp the UCS Central reported their occurrence instead of the time
that Zenoss collected them. For this reason it is recommended that both
your UCS Centrals and Zenoss servers keep accurate time.

The following fields will be populated for each event.

<dl markdown="1">
<dt markdown="1">
Standard Zenoss Event Fields
</dt>
</dl>

-   device: UCS Central device in the */Devices/CiscoUCS/UCS-Central*
    device class.
-   component: Zenoss component related to the fault.
-   count: Occurrences or *occur* for the UCS Central fault.
-   eventKey: UCS Central distinguished name (DN) for the fault.
-   eventClassKey: *cisco-ucsc-fault-code* where code is the UCS Central
    fault code.
-   eventGroup: *cisco-ucsc-faultInst*.
-   summary: Description or *descr* for the UCS Central fault.
-   severity: Mapped from the UCS Central *severity* for the fault using
    the following table.
    -   UCS Central cleared = Zenoss Clear
    -   UCS Central info = Zenoss Info
    -   UCS Central condition = Zenoss Info
    -   UCS Central warning = Zenoss Warning
    -   UCS Central minor = Zenoss Warning
    -   UCS Central major = Zenoss Error
    -   UCS Central critical = Zenoss Critical

The following additional fields and potentially more will also be
populated for each event. These are the fields native to an Cisco UCS
Central fault. If a fault occurs that has other fields, those fields
will be added with the same *cisco.ucsc* prefix.

<dl markdown="1">
<dt markdown="1">
Additional Cisco UCS Central Fault Event Details
</dt>
</dl>

-   cisco.ucsc.ack
-   cisco.ucsc.cause
-   cisco.ucsc.code
-   cisco.ucsc.created
-   cisco.ucsc.descr
-   cisco.ucsc.dn
-   cisco.ucsc.highestSeverity
-   cisco.ucsc.id
-   cisco.ucsc.lastTransition
-   cisco.ucsc.occur
-   cisco.ucsc.origSeverity
-   cisco.ucsc.prevSeverity
-   cisco.ucsc.rule
-   cisco.ucsc.severity
-   cisco.ucsc.srcDme
-   cisco.ucsc.tags
-   cisco.ucsc.type

### Cisco UCS Central Event Subscription

Zenoss supports *Event Subscription* feature of Cisco UCS Central. It
provides a possibility to add/remove/update Zenoss components basing on
the incoming events from Cisco UCS Central.

The following components are affected by this feature:

-   UCS Domain
-   Global Service Profile
-   Local Service Profile
-   Global Service Profile Template
-   Local Service Profile Template

For *UCS Domain* component we accept updates only for the following
attributes:

-   Connection State
-   Oper State

Please check [Cisco UCS Central XML API](http://www.cisco.com/c/en/us/td/docs/unified_computing/ucs/ucs-central/api/b_UCSC_XML_API_book/b_UCSC_XML_API_book_chapter_01.html#concept_9D1F4E91BD6843C1B99547A5424184A6){.external-link}
for more details.

## Usage

### Adding a Cisco UCS Central Endpoint

Use the following steps to start monitoring a Cisco UCS Central using
the Zenoss web interface.

1.  Navigate to the Infrastructure page.

    @lb[](img/zenpack-cisco_ucsc_add_menu.png)

    Add Menu Item

2.  Choose *Add Cisco UCS Central Endpoint..* from the add device
    button.
3.  Fill out the form.

    @lb[](img/zenpack-cisco_ucsc_add_dialog.png)

    Add Dialog

    -   *Hostname or IP Address* must be resolvable and accessible from
        the collector server chosen in the *Collector* field.
    -   *Username* and *Password* are the same as what you'd use to
        login the Cisco UCS Central's web interface.
4.  Click *ADD*.

------------------------------------------------------------------------

Alternatively you can use zenbatchload to add Cisco UCS Central
Endpoints from the command line. To do this, you must create a file with
contents similar to the following. Replace all values in angle brackets
with your values minus the brackets. Multiple Cisco UCS Centrals can be
added under the same */Devices/CiscoUCS/UCS-Central* section.

    ''/Devices/CiscoUCS/UCS-Central''
    my-ucsc setManageIp='192.168.0.1', zCiscoUCSCentralUsername='admin', zCiscoUCSCentralPassword='changeme'

You can then load the devices(s) with the following command.

    zenbatchload <filename>

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Configuration Properties
</dt>
</dl>

-   zCiscoUCSCentralUsername: UCS Central username. Default is "admin".
-   zCiscoUCSCentralPassword: UCS Central password. Default is blank.
-   zCiscoUCSCentralPort: UCS Central XML API TCP port. Defaults to 443.
-   zCiscoUCSCentralUseSSL: UCS Central XML API SSL. Default is true.

<dl markdown="1">
<dt markdown="1">
Device Classes
</dt>
</dl>

-   /Devices/CiscoUCS/UCS-Central

<dl markdown="1">
<dt markdown="1">
Modeler Plugins
</dt>
</dl>

-   zenoss.ucsc.CiscoUCSCentralInstanceMap

<dl markdown="1">
<dt markdown="1">
Datasources
</dt>
</dl>

| Name             | Type                     | Plugin name |
|------------------|--------------------------|------------------------|
 | faults           | Cisco UCS Central Faults | FaultsDataSourcePlugin |
| modelChangeEvent | Python                   | EventSubscribeDSPlugin |

<dl markdown="1">
<dt markdown="1">
Event Classes
</dt>
</dl>

-   /Events/CiscoUCSCentral/Fault
-   /Events/CiscoUCSCentral/ModelChangeEvent

<dl markdown="1">
<dt markdown="1">
Event Class Mappings
</dt>
</dl>

-   /Events/CiscoUCSCentral/Fault/Cisco UCS Central Fault Default
    Mapping
-   /Events/CiscoUCSCentral/ModelChangeEvent/Cisco UCS Central Model
    Change Event Default Mapping

## Changes

**1.3.3**

-   Fix import errors in CiscoUCSCentral due to removed dependencies in
    CiscoUCS 3.0.2 (ZPS-6427)

**1.3.2**

-   Fix import errors from CiscoUCS 3.0.0. (ZPS-5865)

**1.3.1**

-   Add Cisco UCS Central to multi-device add wizard. (ZPS-1421)
-   Fix templates showing in service profiles list and vice versa.
    (ZPS-668)

**1.3.0**

-   Improved session handling with the UCS Central XML API. (ZEN-26322)

**1.2.0**

-   Show servers by type chart on overview. (ZEN-20849)

**1.1.0**

-   Remove unused "Software" from UCS Central view. (ZEN-18673)
-   Reduce number of UCS Central API sessions used. (ZEN-18959)
-   Add API support for launch-in-context from UCS Central UI.
-   Prevent adding duplicate UCS Central instance. (ZEN-19299)
-   Remove host firmware packages support. (ZEN-19890)
-   Add model number for servers. (ZEN-19893)
-   Add domain group column to domains grid. (ZEN-20186)
-   Combine service profile usages with service profiles. (ZEN-19891)
-   Updates to DynamicView support. (ZEN-20183)
-   Prevent adding invalid text as a UCS Central instance. (ZEN-20520)

**1.0.0**

-   Initial release.

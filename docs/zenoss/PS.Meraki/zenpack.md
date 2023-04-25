# Meraki Integration ZenPack

** @lb[](img/zenpack-meraki.png){.confluence-embedded-image .confluence-thumbnail width="200"}**

** **Subscription

This integration is a subscription-based Professional Services
engagement. Our Integration Services are offered as subscriptions in
order to provide initial setup and ongoing compatibility and
maintenance. All standard packages are renewable every 12 months from
the date of purchase. Contact Zenoss to request more information
regarding this or any other ZenPacks.

**Authors:**

Zenoss Inc.

**Maintainers:**

Zenoss Inc.

**Organization:**

Zenoss Inc.

**Name:**

Meraki Integration ZenPack

**Release:**

3.6.0

## Meraki Integration ZenPack

This ZenPack adds Discovery, Modeling, and Monitoring for Meraki Network
devices managed through the Meraki Dashboard API and SNMP Polling.

SNMP Polling can be enabled for the Dashboard devices (using the SNMP
connection information provided for the Organization) and for the
Network Devices, if enabled on individual Devices and network
connectivity exists between the collector and Device.

API Polling uses the same global API to monitor all devices, so should
be available regardless of the network connectivity between Zenoss and
the Network Devices.

## Prerequisites

| Prerequisite      | Restriction                                                                |
|-------------------|----------------------------------------------------------------------------|
| Product           | Zenoss 6.0 or higher                                                       |
| Required ZenPacks | ZenPacks.zenoss.PS.Util &gt;= 1.9.3 ZenPacks.zenoss.ZenPackLib &gt;= 2.1.1 |

## Sources of Data Used for this ZenPack

This ZenPack uses several sources of data for modeling and monitoring
Meraki Devices. How these are used may differ between Dashboard and
Network Devices.

### Meraki Dashboard REST API

The Dashboard REST API is used by both the Dashboard and Network Devices
for modeling and monitoring (see details in the modeler plugins and
configuration sections below).

### Meraki SNMP Proxy

The Meraki SNMP proxy is a cloud service that aggregates data from the
Network Devices and provides it through a unified SNMP endpoint.

This endpoint is polled from both Dashboard (the
meraki.snmp.DashboardDevices modeler) and Network Devices (the
meraki.snmp.DeviceInterfaces modeler).

NOTE: The Network Devices pull their SNMP connection information from
the zMerakiSnmpHost and zSnmpCommunity properties on the associated
Dashboard Device.

### Network Device SNMP

This is the traditional SNMP as used elsewhere in Zenoss, where the
Device's manageIp is polled directly via SNMP. Use of SNMP polling may
not be possible or practical depending on the network architecture. It
is expected that most use cases will not support this, but we include it
as a 'best effort' to try get as much data as possible from the devices.

The 'zenoss.snmp.InterfaceMap' modeler is included by default.

Connection information is configured with the typical zProperties on the
Devices.

### Network Device ICMP

The Meraki Network Devices are configured with a customized Ping
monitor. Rather than monitoring the manageIp as typical with Zenoss
devices, this ZenPack instead monitors the IP address of each of the
Uplink components.

## Configuration and Adding Dashboard Devices

Add a Meraki Dashboard device in Zenoss under the
/Network/Meraki/Dashboard Device Class. The hostname/IP for the device
is not used directly for modeling or polling, so can be set to any
unique value.

Each added Dashboard device monitors all Networks and Devices in a
single Meraki Organization. If multiple Organizations are to be
monitored, a Dashboard device will need to be added in Zenoss for each.

### SNMP Proxy Polling Configuration

Due to the Meraki SNMP Proxy using the same IP for multiple
Organizations, each Dashboard will need to be configured for it's unique
SNMP settings (available in the Meraki Dashboard under Organization &gt;
Settings &gt; SNMP).

Configure zMerakiSnmpHost and zSnmpCommunity with the settings provided
for the Organization in the Meraki Configuration interface.

zMerakiSnmpHost also specifies the port to use, for example:
"[snmp.meraki.com](http://snmp.meraki.com){.external-link}:16100"

SNMP Polling from the Dashboard provides the following Components and
Monitoring on the Dashboard Device.

-   Meraki Devices
    -   Num of Clients
    -   Device Status

Additionally this information is used on the Meraki Devices to model and
monitor

-   Device Interfaces

    -   Packet / Bytes Throughput

### SNMP Traps Configuration

SNMP Trap translation is provided by the ZenPack. Configure the Devices
to send SNMP Traps to Zenoss to create Events.

### API Configuration

Configure the following zProperties to enable the API communication:

-   zMerakiAPIBaseUrl
    -   Will likely always use the default:
        '<https://api.meraki.com/api>'
-   zMerakiAPIKey
    -   API Key for the monitoring user to use for API queries

In addition, the Organization ID will need to be set (editable on the
Device Overview page). If the ID is unknown, this can be left unset and
the 'meraki.rest.Organizations' modeling plugin will pull a list of the
Organizations the API user can access and display them on the Dashboard
Device Overview Page.

If manually adding end Devices (not using the built-in discovery) then
each Device will also need to be configured for the organizationId and
Device Serial Number.

### HTTP Proxy Configuration

If use of an HTTP Proxy is required to communicate with the Meraki
Dashboard API, the following zProperties will be used.

> -   zMerakiAPIProxyHost
>
>     -   (Optional) Hostname or IP of
>         the Proxy. If blank, no proxy will be configured.
>
> -   zMerakiAPIProxyPort
>
>     -   TCP Port of the Proxy
>         (default: 80)
>
> -   zMerakiAPIProxyUser
>
>     -   (Optional) Username for Basic
>         Authentication
>
> -   zMerakiAPIProxyPassword
>
>     -   (Optional) Password for Basic
>         Authentication

## Modeling

### Dashboard Devices

The following modeler plugins are provided for Dashboard Devices.

-   meraki.snmp.DashboardDevices
    -   Creates Device components for the Network Devices returned from
        the Meraki SNMP Proxy.
-   meraki.rest.Organizations
    -   Retrieves the list of Organizations that the configured API Key
        can be used to access and displays on the Dashboard Device
        Overview page. Note that only one Organization can be configured
        on each Dashboard device in Zenoss (zMerakiOrganizationId). This
        plugin allows auditing of the access provided to the user. In a
        shared environment, care should be taken to ensure the user is
        restricted to the proper Organizations.
-   meraki.rest.NetworksAndDevices
    -   Creates components for the Networks and Network Devices reported
        by the Dashboard API. Upon modeling, this plugin will create
        Devices in zMerakiDeviceClass corresponding to the Devices
        reported in the Dashboard. Devices no longer reported via the
        API will be removed. Networks that match
        zMerakiNetworkNamesIgnore will be excluded from modeling (see
        Discovery configuration section for more).

### Network Devices

-   zenoss.snmp.InterfaceMap
    -   If SNMP is configured, this plugin creates and monitors network
        interfaces on the Device.
-   meraki.rest.Device
    -   Model and monitor the following Device properties via the API.
        These are shown on the Device Overview page.
        -   name
        -   networkName
        -   organizationName
        -   lanIp
        -   mac
        -   model
        -   notes
        -   NOTE: 'name' is mapped to the Zenoss device Title - if the
            device name is set in Meraki then this will override the
            Title set on the device.
    -   meraki.rest.DeviceUplinks
        -   Model and monitor the Uplinks available on the Device via
            the API. Models both Uplinks (physical links) and Cellular
            Uplinks.
    -   meraki.snmp.DeviceInterfaces
        -   Create Device Interface components as reported by the Meraki
            SNMP Proxy. These are components polled from the SNMP
            settings configured on the Dashboard Device.

            There is also a 'speed' attribute on the DeviceInterface
            components. This is a user-editable attribute provided for
            convenience in tracking the available speed of links for use
            in reporting, but must be manually set by the customer as
            this information is not available in the Meraki API.

## Monitoring

### Dashboard Devices

-   Meraki Dashboard SNMP Proxy
    -   merakiDevTemplate: Monitors the Device components on the
        Dashboard device.
        -   Device Status
        -   Client Count

### Network Devices

-   SNMP (direct to devices, if enabled)
    -   zenoss.snmp.InterfaceMap Modeler plugin can be enabled to model
        and monitor Network Interfaces if direct SNMP polling is
        supported.
-   Meraki Dashboard SNMP Proxy
    -   merakiDevInterfaceTemplateMonitors the Device Interface
        components from the Meraki SNMP Proxy. Note this uses the SNMP
        connection settings from the associated Dashboard device.
-   Dashboard API
    -   DeviceMonitors the Device status via the Dashboard API.

    -   merakiDeviceLatencyThis template monitors Uplink components.
        Latency and Loss metrics are monitored via the API. If no
        metrics are reported for an Uplink, it is considered to be in an
        invalid state and an event is created with the
        'merakiUplinkLatency' eventClassKey.

    -   merakiCellularUplink:Template specific for monitoring Cellular
        Uplinks. Monitors Ping RTT (with ICMP as mentioned below),
        Latency, Loss, Status, and 'signalStat' metrics (rsrp, rsrq)
        from the API. The default template for Status Monitoring raises
        an event for any Status other than 'Ready'.
-   ICMP
    -   Monitors Ping RTT with ICMP for Uplinks with an assigned IP
        address. Note that this uses a custom monitor which ignores
        zPingMonitorIgnore. Use zPythonPingMonitorIgnore to disable Ping
        monitoring instead.

## Discovery

Discovery of Meraki Network Devices is provided by the
meraki.rest.NetworksAndDevices plugin on the Dashboard device.

The following zProperties control the Discovery behavior:

-   zMerakiDeviceClass:

    -   Device Class in Zenoss in which new Devices discovered from
        Meraki will be added. The default will work
        (/Network/Meraki/Device), but it is recommended to create a
        custom sub-class if monitoring templates will be customized.

-   zMerakiDeviceClassMapping:

    -   A list of mappings of device Model prefix to Device Class for
        newly discovered Devices. These model-specific mappings override
        the zMerakiDeviceClass default.

-   zMerakiCreateDevices:

    -   Whether to create new Meraki Network Devices that are discoverd
        through the Dashboard API by the meraki.rest.NetworksAndDevices
        modeler plugin.

-   zMerakiRemoveDevices:

    -   Whether to remove Meraki Network Devices that are no longer
        reported by the Dashboard API.

-   zMerakiAPIRequestRetries:

    -   The number of retries allowed if the Dashboard API rate-limiting
        blocks a request. An increasing backoff is applied and the
        request will be retried.

-   zMerakiAPIRequestRetriesBackOffFactor:
    -   This property will be used as a minimum retry-after time in
        case Meraki API doesn't send Retry-After time for 429 response.

-   zMerakiSkipDeviceIps:

    -   If set, don't add the device's Lan IP address to the newly
        created device. This will leave the manageIp unset, so SNMP and
        ICMP modeling/monitoring will be unavailable, but API monitoring
        will still function. Useful for networks where network space may
        overlap and IP address conflicts would exist.

-   zMerakiNetworkNamesIgnore:

    -   When modeling Networks from the Dashboard, any Network Names
        that match a regex provided in this zProperty will not be
        modeled. Any devices in these Networks will also be excluded.

-   zMerakiDefaultProdState:

    -   The default Production
        State to assign to created devices. NOTE: This is NOT
        automatically updated after creation, if devices are created
        with a non-production state, it will require a separate workflow
        to update these to production.

-   zMerakiAgentConnectTimeout:
    -   The amount of time
        (seconds) that HTTP Agent will wait for the peer to accept a
        connection.

-   zMerakiAgentPoolMaxPersistentConnections:
    -   The maximum number of
        cached persistent connections for a host. Need to be set only at
        the /Network/Meraki device class.

-   zMerakiAgentPoolCachedConnectionTimeout:
    -   Number of seconds a cached
        persistent connection will stay open before disconnecting. Need
        to be set only at the /Network/Meraki device class.

-   zMerakiClientCacheTTL:
    -   The amount of time
        (seconds) that Client will store cached data. It is recommended
        to set it the same for all devices belong to a single
        organisation.

**Note:** in order to apply new zMerakiClientCacheTTL,
zMerakiAgentPoolMaxPersistentConnections and
zMerakiAgentPoolCachedConnectionTimeout values, zenpython service need
to be restarted.

The Device Class used for new Devices is controlled with
zMerakiDeviceClass and zMerakiDeviceClassMapping. If the Products Model
matches a prefix specified in zMerakiDeviceClassMapping, the
corresponding Device Class will be used. If a matching prefix is not
found, the class in zMerakiDeviceClass will be used.

For example, the following entry will place MS-120-8 Devices in
/Network/Meraki/Device/Switch:

    MS:/Network/Meraki/Device/Switch

Events are created on the Dashboard device in Zenoss for auditing new or
removed Devices, using the eventClassKeys 'MerakiDeviceAdded' and
'MerakiDeviceRemoved'.

These Devices will then perform SNMP polling (if configured) and their
own API modeling and monitoring (against the same Dashboard API).

If Devices are removed from the Meraki Network, they will automatically
be removed from Zenoss during modeling (unless disabled with
zMerakiRemoveDevices).

## Scaling Issues

The Meraki Dashboard API enforces a rate limit of 5 requests per second.
To handle this limitation, requests from Zenoss are deduplicated and
cached as appropriate to minimize the total number of requests. Where
available, requests for device aggregated data are used to avoid a
separate requests per Device.

The update to the Dashboard v1 API reduces the total number of requests
needed to gather information, as endpoints now aggregate data from
multiple devices. However especially large Meraki organizations may
still encounter issues, or if there are other systems also using the API
that consume the available requests (which are enforced on a
per-organization basis, so any user will count toward this rate
limiting).

It may be necessary to reduce the cycleTime of template datasources if
ongoing issues are noticed (events will be raised warning of the
failures).

## Example Configuration - Monitoring the Cisco DevNet Sandbox

This configuration monitors the 'Meraki Always On' Sandbox Lab provided
at <https://devnetsandbox.cisco.com/> (The following credentials may
change, login to confirm the current settings).

-   Add a Dashboard Device under /Network/Meraki/Dashboard.

    -   Since this lab does not have SNMP support, the IP or hostname
        used does not matter.

    -   Title: Meraki DevNet

    -   zMerakiAPIKey: 6bec40cf957de430a6f1f2baa056b99a4fac9ea0

    -   zMerakiOrganizationId: 549236

-   Model the Device

-   New Devices should be available under /Network/Meraki/Device, and
    should appear in the System Organizer 'Meraki'.

-   Model the new Devices - again SNMP is disabled so we'll only have
    Uplink components for monitoring.

## Changes

Release 3.6.0

-   Fixes
    -   Reduce the occurrence and fix the event message for Intermittent
        Twisted Connection Lost Errors / Events

Release 3.5.2

-   Fixes
    -   Updated twisted client to use HTTP Connection Pool
    -   Added client cache and agent timeouts to configurations
    -   Added a millisecond wait before returning Client cache

Release 3.5.1

-   Fixes
    -   Remove default Device SNMP sysUpTime template for Dashboard
        Devices

Release 3.5.0

-   Features
    -   Add zMerakiDefaultProdState
-   Fixes
    -   Unicode encoding breaks ConfigurationManager integration.
    -   Some devices mapped to wrong Network in Systems organizers
    -   Fix DeviceUplinks modeler skipped when Organization has no
        Uplinks on any devices.

Release 3.4.2

-   Fixes
    -   Fix some requests caching to invalid Url, effectively skipping
        caching.

Release 3.4.1

-   Fixes
    -   Fix DeviceUplinks modeler processing skipped if no Device
        results.

Release 3.4.0

-   Features
    -   Increase internal response cache from 180 Seconds to 290 seconds
        (just under 5 minute cycle).
-   Fixes
    -   DeviceUplinks modeler previously would not update if there were
        no components, leaving any prior found components (especially an
        issue on Switch and Access Point devices which don't have
        Uplinks in Dashboard API v1).

Release 3.3.0

-   Features
    -   Remove Latency and Loss monitoring from Cellular components -
        data not provided in API
    -   Pull API connection details from Dashboard device, not end
        devices.
    -   API Client queueing update - previously API Requests from all
        Organizations shared the same queue, giving larger organizations
        more access since more devices added more tasks to the same
        queue. Now ensure equal access for all organizations to minimize
        the impact of a single large organization with failing requests
        blocking the queue with retries.
    -   Fix traceback in MerakiUplinkStatusDataSourcePlugin when missing
        Uplink data.

Release 3.2.0

-   Features
    -   Enable merakiUplinkStatus status monitoring template for
        'Uplink' components
    -   Add the /Network/Meraki/Device/Teleworker device class for Z
        series Gateways (the new default mapping adds
        'Z:/Network/Meraki/Device/Teleworker' but will not affect
        existing installs).
-   Fixes
    -   Fix tracebacks in Cellular Uplink monitoring when missing some
        fields in API.
    -   Remove Ping monitoring from Cellular Uplinks by default (the
        merakiPingStatus template can be added where needed).

Release 3.1.0

-   Features
    -   Add zMerakiNetworkNamesIgnore to ignore Networks by Names
    -   Add 'Cellular Uplink' components and monitoring.
-   Fixes
    -   Fix missing pagination in requests leading to missing components
        / monitoring.

Release 3.0.0

-   Features
    -   Switch to Dashboard API v1 endpoints
    -   Remove 'networkType' modeled attribute, no longer present in API
    -   Default Device ID no longer includes network name as device may
        be moved between networks.

Release 2.2.0

-   Fixes
    -   Missing 'devMac' causes a traceback in modeler
    -   MerakiUplinkLatencyDataSourcePlugin - separate events for
        missing datapoints and polling issues.

Release 2.1.2

-   Fixes
    -   Fix "NotFound is not defined" error when running jobs

Release 2.1.1

-   Fixes
    -   Index devices on creation to add to Catalog

Release 2.1.0

-   Features
    -   Add 'speed' attribute to Device Interface components for manual
        tracking.

Release 2.0.0

-   Features
    -   The Device Interfaces component is moved from the Dashboard
        Devices to the Network Devices. Note that existing components on
        the Dashboards may remain in place to preserve historical data.
        However, these will no longer be modeled or monitored, so they
        will need to be manually deleted if the data is no longer
        needed.

Release 1.7.1

-   Fixes
    -   Move Device Status event to /Status/Meraki/Device since events
        in /Status/Ping disable monitoring.

Release 1.7.0

-   Fixes
    -   Move Device Status event to /Status/Ping to provide availability
        for reporting.

Release 1.6.0

-   Fixes
    -   Add missing eventClass mappings causing events in /Unknown class
    -   Allow editing CycleTime in datasources.
    -   Include snmpindex in component details to be accessible through
        the API
    -   add zMerakiSkipDeviceIps to allow creating devices without
        manageIPs
    -   Update UplinkStatus monitoring to not use a separate API call,
        rather derive from Latency monitoring status.

Release 1.5.0

-   Features
    -   Add HTTP Proxy support

Release 1.4.3

-   Features
    -   Improved logging details for missing 'lanIp' on devices.

Release 1.4.2

-   Fixes
    -   Add migration to rebuild device relations.

Release 1.4.1

-   Fixes
    -   Remove port from zMerakiSnmpHost default - use zSnmpPort instead
    -   'Ready' is a valid status for merakiUplinkStatus
    -   Relationship for MerakiDevInterface to MerakiDevice

Release 1.4.0

-   Features
    -   Add zMerakiSnmpHost to override SNMP connection IP to connect to
        Meraki proxy.
    -   Now requires ZenPacks.zenoss.PS.Util &gt;= 1.7.0

Release 1.3.0

-   Features
    -   Add Uplink Ping Monitoring DataSource
    -   Model Meraki Device Name in meraki.rest.Device
    -   Now requires ZenPacks.zenoss.PS.Util &gt;= 1.3.0

Release 1.2.0

-   Features
    -   Disable Ping based monitoring by default, use device status from
        Meraki API.
    -   Split DeviceClasses based on zMerakiDeviceClassMapping

Release 1.1.1

-   Fixes
    -   Fix catalog load to create missing index.

Release 1.1.0

-   Features
    -   Remove the zMerakiOrganizationId zProperty, replace with a
        Device property and add to the Device Overview page.
    -   Discovery no longer depends on Device ID so that Devices can be
        created manually or the ID changed.
    -   Use the Device Name from the Meraki API for Device Title
    -   Update Device and Uplink Status Templates to set Event Class and
        Severity



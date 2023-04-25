# Cloudgenix Integration ZenPack

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

Cloudgenix Integration ZenPack

**Release:**

1.6.3

## Cloudgenix Integration ZenPack

## About

This ZenPack adds Discovery, Modeling, and Monitoring for CloudGenix
Network devices managed through the CloudGenix API and SNMP Polling of
Network Devices.

SNMP Polling (using the SNMP connection information obtained from the
CloudGenix API) is supported for the network devices is supported if
connectivity exists between the collector and Device.

API Polling uses the same global API to monitor all devices, so should
be available regardless of the network connectivity between Zenoss and
the Network Devices.

## Prerequisites

| Prerequisite       | Restriction                                                                |
|--------------------|----------------------------------------------------------------------------|
| Product            | Zenoss 6.0 or higher                                                       |
| Required ZenPacks  | ZenPacks.zenoss.PS.Util &gt;= 1.4.0 ZenPacks.zenoss.ZenPackLib &gt;= 2.1.1 |
| Other dependencies | None                                                                       |

## zProperties

CloudGenixAPIBaseUrl The API Endpoint for requests. The default
(<https://api.cloudgenix.com>) likely will not need to be changed.

CloudGenixAPIKey A static authentication token for API requests
generated from CloudGenix.

CloudGenixDeviceClass The default Device Class under which to create
Discovered Element Devices.

CloudGenixCreateDevices Whether to enable automatic device creation.

CloudGenixRemoveDevices Whether to enable automatic device removal.

CloudGenixDiscoveryIgnoreNames A Regex pattern for Element names to
ignore during Discovery when creating Elements from the Tenant device.

## Device Types

### Tenants

Tenants are the top-level object for companies in CloudGenix. The Zenoss
Tenant object manages device discovery and monitoring for Tenant-wide
objects.

### Elements

Elements are the network devices that make up the network. Elements can
be auto-discovered by the Tenant device and their SNMP configuration
will be automatically configured from the API details.

## Adding and Configuring Tenant Devices

Add a CloudGenix Tenant device in Zenoss under the
/Network/CloudGenix/Tenant Device Class. The Hostname of the Tenant is
unused, as all API polling is done through the zCloudGenixAPIBaseUrl
endpoint. However, a valid hostname must still be used to pass
validation to create the device.

Configure the zCloudGenixAPIKey and set the Tenant ID on the Device
Overview page and model the device.

If multiple Tenants are to be monitored, a Tenant device for each will
need to be created.

## Modeling

### Tenants

The following modeler plugins are provided for Tenant Devices.

-   cloudgenix.rest.Sites
    -   Model the Site, LAN Subnet, WAN Network, Site WAN Link, and VPN
        Link components on theTenant via the API (&lsquo;wannetworks&rsquo;,
        &lsquo;lannetworks&rsquo;, &lsquo;waninterfaces&rsquo;, and &lsquo;topology&rsquo; resources)
-   cloudgenix.rest.Elements
    -   Runs the device discovery, creates or removes Elements as
        controlled by zCloudGenixDeviceClass,zCloudGenixCreateDevices,
        and zCloudGenixRemoveDevices (via the API &lsquo;elements&rsquo; resource)
-   cloudgenix.rest.TenantId
    -   If the Tenant ID for the Device is unset, this plugin will query
        the Tenant ID from the API(&lsquo;profile&rsquo; resource) and and set to
        the Tenant ID associated with the API Key. Note that
        modelingwould need to run again for the other plugins to pick up
        the change.
-   cloudgenix.rest.Applications
    -   Model the applications on each site (via the API &lsquo;appdefs&rsquo; and
        &lsquo;sites&rsquo; resources).

### Elements

In addition to out-of-the-box modelers that are automatically added, the
following custom plugins are provided.

-   cloudgenix.rest.Element
    -   Models various properties of the Element device via the API
        (&lsquo;elements&rsquo; and &lsquo;sites&rsquo;
        resources).–softwareVersion–modelName–siteName–description–role–title
        (name)–serial number–Automatically controlled Systems organizer
-   cloudgenix.rest.ElementInterfaces
    -   Models the Device Interfaces presented through the API
        &lsquo;interfaces&rsquo; resource. (independent fromthough may duplicate
        data returned by SNMP polling).2
-   cloudgenix.rest.ElementSnmp
    -   Retrieves SNMP configuration (community string) from the
        CloudGenix API &lsquo;snmpagents&rsquo; resourceand applies it to the device
        in Zenoss.
-   zenoss.snmp.InterfaceMap
    -   Zenoss default plugin to model the &ldquo;Interface&rdquo; components via
        SNMP direct to the device.

## Monitoring

### Tenants

-   Sites
    -   Template: CloudGenixSiteStatus
        -   Monitors the State of
            the Site components via the API &lsquo;topology&rsquo; resource and
            raises Events ifnot Active
    -   Template: CloudGenixSiteMetrics
        -   Monitors metrics on the
            Site components via the API &lsquo;metrics_monitor&rsquo;
            resource.
            -   TCPFlowCount
            -   TCPConcurrentFlows
            -   UDPFlowCount
            -   UDPConcurrentFlows
    -   Template: CloudGenixSiteBandwidth
        -   Monitor Site Bandwidth
            usage via the API &lsquo;metrics_monitor&rsquo; resource.
            -   DirectInternet
            -   PrivateVPN
            -   PrivateWAN
            -   VPN
    -   Template: CloudGenixSiteTopApps
        -   Every 15 minutes, polls
            the Top 10 Applications from the &lsquo;topn_monitor&rsquo; API resource
            foreach Site,
            and updates ComponentGroups containing
            these. Applications are polled for various intervals
            -   Last Hour
            -   Last Day
            -   Last 7 Days
            -   Last 30 Days
        -   ComponentGroups are
            created in the format
            &ldquo;/ComponentGroups/CloudGenix/&lt;TenantId&gt;/&lt;siteId&gt;/&lt;intervalName&gt;&rdquo;
-   Links
    -   Template: CloudGenixLinkStatus
        -   Monitors the State of
            the Link via the API &lsquo;topology&rsquo; resource and raises Events
            if not &lsquo;up&rsquo;.Links are ignored if they&rsquo;re
            not in Admin Up state.
-   Applications
    -   Template: CloudGenixApplication
        -   Monitors the Bandwidth
            usage of the applications from each site via the API
            &lsquo;metrics_monitor&rsquo;resource.
-   Site WANs
    -   Template:
        CloudGenixSiteWan3
        -   Monitor Site Bandwidth
            Usage and Link Health of the SiteWAN Path via the API
            &lsquo;met-rics_monitor&rsquo;
            resource.

Elements

-   Device
    -   Template: Device
        -   Monitors the Device State and Connected status via the API
            &lsquo;elements&rsquo; resource. Raises Eventsif the state is not
            &lsquo;bound&rsquo;. Connected status is graphed for historical
            monitoring.
-   Element Interfaces
    -   Template: ElementInterface
        -   Monitors Interface State and Connected status via the API
            &lsquo;status_interfaces&rsquo; resource. Raisesevents if the state is
            not &lsquo;up&rsquo;. Connected status is graphed for historical
            monitoring.
-   Interfaces
    -   Built-in SNMP interface monitoring if SNMP interfaces have been
        modeled.

Discovery

Discovery of CloudGenix Elements is provided by the
cloudgenix.rest.Elements plugin on the Tenant device.

The zProperties zCloudGenixCreateDevices and zCloudGenixRemoveDevices
control whether to add or remove the devices automatically during
modeling.

Events are created on the Tenant device in Zenoss for auditing new or
removed Devices, using the eventClassKeys&lsquo;CloudGenixDeviceAdded&rsquo; and
&lsquo;CloudGenixDeviceRemoved&rsquo;.

If Devices are removed from the CloudGenix Tenant, they will
automatically be removed from Zenoss during modeling
if zCloudGenixRemoveDevices is configured.

If a Device name matches the pattern in zCloudGenixDiscoveryIgnoreNames,
it will be ignored when creating new devices.An example use is to avoid
creating Zenoss devices for Elements that are provisioned but not fully
deployed. Naming the device with the suffix &lsquo;-spare&rsquo; and specifying to
ignore with the same pattern.

API Versioning

This ZenPack will attempt to use the latest version of API resources
that are available since earlier versions are notmaintained by backward
compatibility. However, if the API response formats change then an error
is to be expected and will require a ZenPack update.The API is
bootstrapped by calling &lsquo;/v2.0/api/permissions&rsquo; to get the published
resource maps that are available in theversion associated with the
Tenant.

Changes

-   Release 1.6.3
    -   Fixes
        -   Fix invalid exception logging in cloudgenix.rest.Elements
            modeler plugin.
-   Release 1.6.2
    -   Fixes
        -   Gracefully handle ELEMENT_NOT_FOUND errors from the API
            during Elements modeling.
-   Release 1.6.1
    -   Fixes
        -   Don&rsquo;t remove existing SystemPaths when modeling Elements.
-   Release 1.6.0
    -   Features
        -   Dynamically build API Resource URIs from
            /v2.0/api/permissions maps.
-   Release 1.5.1
    -   Fixes
        -   Fix &lsquo;connected&rsquo; datapoint polling in
            ElementInterfaceStatusPlugin
-   Release 1.5.0
    -   Features
        -   ComponentGroup Creation for Top 10 Applications per Site
    -   Fixes
        -   Fix Link Monitoring in LinkStatusPlugin
-   Release 1.4.0
    -   Features
        -   Update component Labels to better match CloudGenix
        -   Remove LAN Monitoring Template
        -   Add Site name to VPN Link title
        -   Update Link components with relation to Sites
-   Release 1.3.0
    -   Features
        -   Model and Monitor LANs, WANs, and SiteWANs
-   Release 1.2.0
    -   Features
        -   Add zCloudGenixDiscoveryIgnoreNames zProperty for Discovery.
        -   Add Site Bandwidth and Flow Monitoring
        -   Ignore Links from Monitoring when not AdminUp
-   Release 1.1.1
    -   Fixes
        -   Fix Application metric monitoring by limiting size of
            requests.
        -   Fix event classifications.
-   Release 1.1.0
    -   Features
        -   Add Application modeling and Monitoring
        -   Add Link Status Monitoring
        -   Skip devices that have not been provisioned to a site during
            Discovery
        -   Add cloudgenix.rest.TenantId modeler plugin to automatically
            set the TenantID



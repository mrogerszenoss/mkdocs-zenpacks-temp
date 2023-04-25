# CMDB Integration Service

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

CMDB Integration Service

Version:

3.3.0

More
Information:

## CMDB Integration Service

This annual subscription service interfaces Zenoss software with the
CMDB. This integration is renewable every 12 months from the date of
purchase and is designed to offer ongoing compatibility between the
products.

## About

This ZenPack provides functionality
to talk via JSON interfaces to different CMDB products (eg Service Now)
or a custom SQL CMDB. If there are customizations required for any
particular customer site, a new ZenPack that inherits from the
ZenPacks.zenoss.CMDBIntegrationNG class will be required.

### Features

This ZenPack retrieves devices from an external CMDB system, and adds
them to Zenoss, in the /Discovered device class and adds a clickable
link for Configuration Item ID (CI ID) to the device overview page. If
the device already exists, it leaves the existing device in place, and
adds the clickable link for CI ID. If a device has components in the
CMDB, it will add a clickable link for the CI ID of the component to the
component details tab. The ZenPack will also optionally retrieve
location information for the devices, and add the locations to Zenoss
(if they don't already exist), and place the devices in those locations
(the string retrieved from the CMDB for locations will be used to match
the name of a location directly under /Locations). The ZenPack will also
optionally retrieve applications from the CMDB that are listed as
running on the device, and will create a System organizer for each
unique application, and place the appropriate devices in those System
organizers. This structure can be used to create Impact services (see
below).

The following CMDB products are supported:

-   `Service Now`: the ServiceNow CMDB system
-   `SQL`: Generic Support for an MSSQL or MySQL CMDB
-   `Atrium`: BMC Atrium CMDB

### Prerequisites

| Prerequisite       | Restriction                                                                                                         |
|--------------------|---------------------------------------------------------------------------------------------------------------------|
| Product            | Zenoss 6.4.1 or later                                                                                               |
| Required ZenPacks  | ZenPacks.zenoss.ZenSQLTx &gt;= 2.6.3 ZenPacks.zenoss.PS.QFramework &gt;= 1.1.1 ZenPacks.zenoss.PS.Util &gt;= 1.10.0 |
| Other dependencies | None                                                                                                                |

### Usage

The following common configuration fields are available:

-   Note that toggling the Enabled flag off will remove the existing CI
    IDs from all devices in the Zenoss system. Toggling it back on will
    not restore those IDs; the system will need to poll for all of the
    devices, and re-associate the CI IDs to the Zenoss devices.
-   Note that the option to migrate performance data has been removed
    throughout the product, so the option has been removed from the CMDB
    configuration.

### Device Field Mapping

In general, the Zenoss field in the mapping should fall into one of a
couple of patterns. The simplest are simply attributres of the device,
like 'manageIp'. The second are attributes of either the HW or OS
object. Those should be specified as, for example, 'os.version' or
'hw.tag'. The third are special fields that are not directly accessible
as attributes. This includes 'productionState', 'name',
'performanceMonitor', and 'devicePath'. The 'performanceMonitor' field
allows you to set the collector for a device. Use the name of the
collector, as you would see in the UI.

There MUST be a mapping for the 'productionState' field, because every
Zenoss device MUST have a valid production state. The value in whatever
field is mapped to productionState is first translated using the mapping
in the configuration item labeled "Mapping of production states from
CMDB to Zenoss".

The 'name' field is used for the Zenoss device id. Every device in
Zenoss MUST have an id, so you SHOULD make sure to map a value to name.
However, the system does have some logic that it uses to try to identify
a value for name if one is not provided. Specifically, the system will
use the value mapped to name, if there is one, and it is a non-empty
string. If not, then it checks to see if a value has been mapped to
title, and if so, and it is a non-empty empty string, then it will use
that. If that fails as well, then it checks to see if a value has been
provided for manageIp - if so, and it's a valid IP address, then it will
use that value for the name. If all of those fail, then the system will
log an error, create an event with the error, and not try to create the
device.

The 'devicePath' field allows you to put devices into a device class
other than '/Discovered'. The value mapped to this field MUST be a valid
device class path, beginning with the '/' character. An example would be
'/Server/SSH/Linux'. Any values that are not valid device class paths
will be ignored, and a log message will be generated. The 'devicePath'
field is only used on device creation; devices will not be moved from
one device class to another.

### Remove IP Below this Production State

When the CMDB integration is changing the production state of a device
to a value below this threshold, it will remove the manageIp value. With
the default threshold, this will only affect devices that are being
decommissioned, as the value for that production state is -1. Note that
the IP address is completely removed; it would not reappear if the
production state is reset, unless the CMDB integration is getting that
IP from the CMDB.

To disable this functionality, you can set the threshold to a value
lower than any production state you have defined. For the default set of
production states, setting this value to -1 or lower will prevent the
integration from removing the IP address.

The reason for this functionality is to prevent collisions between
decommissioned devices and new devices coming from the CMDB, when IP
addresses are re-used. You can keep the decommissioned device in Zenoss
to allow viewing historical data, while allowing the integration to
create a new device using the same IP address.

### Polling Interval

The Polling Interval, or 'cycletime', determines how often (in seconds)
the database is polled and checked for updates. This is configurable in
the service's configuration file, zencmdbpoll.conf.

In Zenoss v5, this is accessible by opening the zencmdbpoll Service in
Control Center, editing the Configuration file, and restarting the
Service.

Starting with version 2.0.0, the cycletime for zencmdbpoll is not used
to control the polling interval. Instead set the full and incremental
polling intervals in the CMDB configuration screen. A full run queries
everything from the CMDB that matches the filter, and an incremental run
only queries the CMDB for objects that have changed since the last run.
This obviously is much faster, since it only has to work with a subset
of the records from the CMDB. Objects in the CMDB that were not
associated with a device or component in Zenoss, and which have not
changed, will not be queried in an incremental run. In particular, if
you have added components to a device in the CMDB, but the CMDB does not
register that as a change to the device, those components would not be
linked to their counterparts in Zenoss. Note that changing the CMDB
configuration in Zenoss will trigger the next run to be a full, rather
than incremental, run, regardless of the poll cycle settings.

Note that the full polling interval in a production system should
generally be set to 0, which disables it. In a test system, where you
might be making changes that would require a full run to see the
results, it's OK to set this to a non-zero value to allow for easier and
faster testing.

### Test Access to CMDB

'Test Access' button can be used for
checking the connection to the CMDB system. You need to select a
Configuration Item and click the "Test Access" button. After that, the
result will be displayed in the pop-up dialog box.

### Services

This ZenPack installs three services
into the system. ZenCmdbPoll is responsible for querying the CMDB and
adding/updating devices in Zenoss. The ZenCmdbPush and ZenCmdbPushWorker
services are responsible for listening for changes to the model in
Zenoss, checking whether any of the fields that are configured to be
sent to the CMDB are different from what's currently in the CMDB,
compiling lists of components (if any the system is configured to send
any component types to the CMDB), prepping those updates, and sending
them to the CMDB. Not all implementations support this functionality,
but the services will be there regardless. If you are not configuring
the system to send any information to the CMDB, these services can
safely be disabled.

## Installing

Install the ZenPack via the command line and restart Zenoss

`zenpack --install ZenPacks.zenoss.CMDBIntegrationNG-<version>-py2.7.egg``zenoss restart`

## Removing

To remove the ZenPack, use the following command:

`zenpack --erase ZenPacks.zenoss.CMDBIntegrationNG``zenoss restart`

## Troubleshooting

The Zenoss support team will need the following output:

1.  Set the `zencmdbpoll`daemon into `DEBUG`level logging by
    typing `zencmdbpoll debug`from the command-line. This will ensure
    that we can see all activities in the `zencmdbpoll.log`file.

## Logging

Log files are kept in the following locations under
the`$ZENHOME/log/`directory:

| Source               | Log Location      |
|----------------------|-------------------|
| CMDB synchronization | `zencmdbpoll.log` |

## Changelog

3.3.0

Features:

-   SVC-3258 Add dry run option to CMDB Config dialog
-   SVC-3307 Validate that CMDB Application Relationships has all
    required fields
-   SVC-3353 Allow zencmdbpoll to create Systems as well as Groups
-   SVC-3389 Look for locations before creating or updating devices to
    support hierarchical locations

Fixes:

-   SVC-3008 Remove Migrate Performance Data When Automatically
    Re-Identifying Devices from CMDB
-   SVC-3311 Ensure dry run button does not save config
-   SVC-3316 CMDB ciid lost when moving device between deviceclasses
    with different python types
-   SVC-3343 CMDB zenpack documentation needs to state that it requires
    ps.util
-   SVC-3377 Streamline logic around when to run (and do full runs) in
    zencmdbpoll
-   SVC-3388 zencmdbpoll still missing heartbeats

3.2.0

Features:

-   SVC-2720 Add events for duplicated IP address and device id
-   SVC-2985 Added audit statements for device creation and renaming,
    production state changes, device priority change, location change,
    component updates
-   SVC-3105 Allow user to remove CI ID from a device in the UI
-   SVC-3158 Iterate through component CI IDs also to look for services
    in the CMDB
-   SVC-3217 Update ServiceNow information in docs

Fixes:

-   SVC-2397 Ensure failure of cmdb poll does not cause process to fail,
    and that we reset next run or next full run so we don't wait a full
    interval to try again.
-   SVC-3027 Ensure Test Access button gives correct results for all
    CMDB types
-   SVC-3171 Convert set of components to list to allow chunker to chunk
    the list to send to the CMDB
-   SVC-3173 Ensure we pass a list to the chunker function
-   SVC-3175 Fix traceback when querying CMDB for Impact information
-   SVC-3260 Exclude notification windows when caching maintenance
    windows

3.1.2

-   SVC-3169 Update change management calls in facade to end maintenance
    windows before deleting group, so devices aren't left in maintenance
    when window is cancelled during the window

3.1.1

-   SVC-3159 Don't automatically do a full sync when daemon restarts

3.1.0

-   SVC-2928 Moving Atrium to use newer PS.Util http client, and using
    plugin for auth
-   SVC-3046 Detect when credentials have changed and restart JsonApi
    object to pick up
-   SVC-3050 Update logging to ensure all configuration settings are
    logged in debug

3.0.0

-   Features
    -   SVC-2186: Implement a getSettings method for the CMDB config
    -   SVC-2261: Update documentation to fully describe effect of the
        Enable button
    -   SVC-2527: Heartbeat messags are not sent while poll is running
    -   SVC-2620: Use standard chunking function from PS.Util
    -   SVC-2627: Update to use PS.Util http_client
    -   SVC-2621: Make zencmdbpoll work better with twisted
    -   SVC-2808: Explicitly set last change on device after adding
    -   SVC-2962: Avoid unneccesary json encoding and decoding of body
        data for requests
    -   SVC-2847: Preserve CI ID when moving a device between classes
    -   SVC-2537: Add zing-connector healthcheck to zencmdbpoll
    -   SVC-2927: Remove IP address object if appropriate when
        decommissioning device
    -   SVC-2984: Prevent user from setting full run interval shorter
        than run interval
    -   SVC-2954: Add support for OAuth for ServiceNow to CMDB ZP

2.2.4

-   Fixes
    -   SVC-2916: Gracefully handle no group mappings.

2.2.3

-   Fixes
    -   SVC-2872: Prevent traceback error in transaction commit when no
        CMDB config is enabled

2.2.2

-   Fixes
    -   SVC-2857: Prevent tracebacks when no fields are going to be sent
        to CMDB to prevent stuck messages in queue

2.2.1

-   Features
    -   SVC-2810: Remove manageIp when decommissioning a device
-   Fixes
    -   SVC-2814: adapt zenjobs propertypatcher hook to work with either
        pre/post zenjobs rewrite

2.2.0

-   Features
    -   SVC-1961: Add the ability to map a CMDB field to Zenoss
        collector, and change collector if that changes
    -   SVC-2755: Add the ability to map a CMDB field to Zenoss device
        class to set device class on device creation
-   Fixes
    -   SVC-2518: Ensure all error and warning log messages also create
        events in the event console
    -   SVC-2230: Ensure errors updating CMDB fields are counted as
        errors for zencmdbpoll
    -   SVC-2628: Fix prodstate changes during maintenance windows
    -   SVC-2631: Fix cmdbClass not being reset by zencmdbpoll
    -   SVC-2771: Fix bad collector name causes \_checkDeviceExists to
        fail
    -   SVC-2780: Fix in zencmdbpoll, compare is broken for fields to
        send to CMDB
    -   SVC-2757: Clean up documentation

2.1.4

-   Fixes
    -   SVC-2762: fix issue where transaction post commit hook can fail
        under certain circumstances

2.1.3

-   Fixes
    -   fix CMDB config disappearing from Advanced Menu

2.1.2

-   Fixes
    -   fix zencmdbpushworker failures when a Device added/updated

2.1.1

-   Fixes
    -   Fix 'qualification' filter in Atrium

2.1.0

-   Fixes
    -   SVC-2486: fix CMDB config disappearing from Advanced Menu
    -   SVC-2185: add raw data to logging in case of error in
        nameFallThrough
    -   SVC-2572/SVC-2576: fix traceback on device/components removal
    -   SVC-2577: fix zenjobs hanging when CMDB installed

2.0.4

-   Fixes
    -   SVC-2560: fix to allow field updates to be pushed to CMDB when
        no components are being pushed

2.0.3

-   Fixes
    -   SVC-2547: Atrium: Update URL to use instances instead of
        instance
    -   SVC-2558: Atrium: Chunk IP addresses before query to avoid URI
        too long error messages
    -   SVC-2559: fix model event message monkeypatching so it only
        happens when it needs to

2.0.2

-   Fixes
    -   SVC-2535: update ciid index on guid change and add fallback for
        dmd value in case object is not yet persisted
    -   SVC-2513: check if component ciID exists
    -   SVC-2529: removed redundant compsToPushToCMDB definitions
    -   SVC-2534: Explicitly fire event so that property patching
        happens in the zencmdbpushworker process

2.0.1

-   Fixes
    -   SVC-2528: fix property patcher to avoid stale dmd reference

2.0.0

-   Features
    -   SVC-2182: Push limited component changes to CMDB
    -   SVC-2182/SVC-2425: Added metric instrumentation of cmdb daemons
    -   SVC-2182/SVC-2325: Improved logging and events
    -   SVC-2398: Added full and incremental poll cycle configuration
    -   SVC-2398/SVC-2221: Added force run button to config UI
-   Fixes
    -   SVC-2421: batch servicenow cmdb updates to avoid errors
    -   SVC-2417/SVC-2231: fixed inconsistent CIID index issues
    -   SVC-2417: improved duplicate CIID detection
    -   SVC-2417/SVC-2439: ensured poll does not stop on common errors
    -   SVC-2417: fixed 'Production States to Keep' functionality
    -   SVC-2417: fixed 'use CMDB Ip Address' functionality
    -   SVC-2425/SVC-2230: count cmdb update errors as errors

1.12.3

-   SVC-2402 SVC-2403 SVC-2404: fixes for discovered bugs/regressions
-   SVC-2400: reinstate createDevices control setting while ensuring
    lack of creation does not inhibit association or update of existing
    devices

1.12.2

-   hotfix 1.12.2: fix cmdbStatus migration so it commits

1.12.1

-   Fixes

<!-- -->

-   SVC-2375: fix productionState mapping
-   SVC-2381: fix default value for cmdbKeepProdStates and migrate
    existing configs
-   SVC-2367: add agent field to zencmdbpoll events
-   SVC-2368: log actual device id when changing device ids
-   SVC-2372: SNow: allow both the raw field and dv_field values to be
    mapped

Release 1.12.0

-   Features
    -   SVC-130: Add 'Test Access' button into UI
    -   SVC-2269: Add feature to map devices to Device Groups based on
        CMDB field contents
-   Fixes
    -   SVC-2252: fix improper and inefficient behaviour in change
        window setting
    -   SVC-2256: Patch properties onto device classes when zenjobs
        starts up
    -   SVC-2363: linking ci id to existing device if its ci id is not
        set
    -   SVC-2363: raising event for duplicate CI IDs

Release 1.11.0

-   Features

    -   SVC-2033 Add backend procesor to handle communications with RM
    -   SVC-2073 Implemented tests for associating ci's to devices and
        components, disassociating CIs from devices and components,
        decommissioning and deleting devices
    -   SVC-2084 Refactor zencmdbpoll to use new backend processor
    -   SVC-2184 Remove Additional Field Mappings, migrate any existing
        settings to the standard device field mappings
    -   SVC-2187 Fix undefined name errors caused by not importing all
        necessary modules
    -   SVC-2223 Ensure properties we are setting actually exist so we
        don't create unwanted attributes
    -   SVC-2224 Remove code that was made obsolete or redundant by the
        new backend processor

Release 1.10.1

-   Fixes
    -   Add zing-connector endpoint for Zenoss Cloud compatibility.

Release 1.10.0

-   Features
    -   ServiceNow add maxRequestLen to config to override default
-   Fixes
    -   Properly map SN
        '[dv\_](https://github.com/zenoss/ZenPacks.zenoss.CMDBIntegrationNG#id13){.external-link}'
        fields.

Release 1.9.1

-   Fixes
    -   Fix check for location in returned data

Release 1.9.0

-   Features
    -   added event generation for CMDB run
-   Fixes
    -   fixed setChangeControl to work correctly
    -   typo fixes

## Attachments:

-   [servicenow-logo-partner_0\_0.png](img/zenpack-servicenow-logo-partner_0_0.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/CMDBIntegrationNG/zenoss-integration-services-ds.pdf){.external-link}
-   [servicenow-logo-partner_0\_0.png](img/zenpack-servicenow-logo-partner_0_0.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/CMDBIntegrationNG/zenoss-integration-services-ds.pdf){.external-link}
-   [servicenow-logo-partner_0\_0.png](img/zenpack-servicenow-logo-partner_0_0.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/CMDBIntegrationNG/zenoss-integration-services-ds.pdf){.external-link}
-   [servicenow-logo-partner_0\_0.png](img/zenpack-servicenow-logo-partner_0_0.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/CMDBIntegrationNG/zenoss-integration-services-ds.pdf){.external-link}


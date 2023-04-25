# Incident Management Integration Service

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

Incident Management Integration Service - ServiceNow

### Version:

3.3.1

### More Information:

## Incident Management Integration Service

### About

This ZenPack provides functionality
to talk via web APIs to different workflow products (eg Remedy, Service
Now). Many customers will be able to utilize this ZenPack simply by
customizing the Notification configuration, though some customers may
need a new ZenPack that inherits from a
ZenPacks.zenoss.IncidentManagement class and is customized
further.

Two general types of notification are provided by this ZenPack.

-   Notification Action

    This type of notification provides a *one way* notification flow. A
    Zenoss event triggers the action to send a notification to an
    external system. The event will be updated with information about
    this action (date/time, name of notification/trigger, success
    indicator or error message) unless disabled (see notes below on
    sending multiple occurrences and disabling event updates)

    The following event notification actions have been added
    (integration-specific docs available below):

    -   `Slack`: post messages to a Slack channel for new Incidents
    -   `dpaste.com`: an example that writes event information to a
        popular site.
    -   `Debug`: creates random incident numbers and links for
        demonstration purposes.
    -   `HTTP`: forward events to an HTTP based API

-   Incident Integrate

    This type of notification provides a *bi-directional* incident
    integration. A Zenoss event triggers the integration to create an
    incident in an external system (the word incident will be used in
    this documentation to refer to external system's objects such as
    incidents, tickets, events or similar). The event will be updated
    with information about the created incident (date/time of
    notification, incident identifier/url, trigger/notification name) or
    error message, unless disabled (see notes below on sending multiple
    occurrences and disabling event updates). The created incident will
    be tracked and updates to the incident or event can trigger updates
    to the related object in the other system, including closing or
    acknowledging the event or incident and updating notes.

    The following event notification actions have been added
    (integration-specific docs available below):

    -   `Service Now`: the ServiceNow workflow system.
    -   `Jira`: Atlassian Jira Issue and project tracking system
    -   `Remedy ITSM`: the BMC Remedy IT Service Management workflow
        system.
    -   `Remedy Force`
    -   `CA Service Desk`
    -   `CA Service Manager`
    -   `OTRS`
    -   `HP Service Manager`

An additional button has been added to the Zenoss event console that
allows the user to manually trigger the notification based on a selected
event (or multiple selected events)

When attempting to create a new incident via trigger (not via the UI),
the ZenPack will first try to find an existing incident that is open and
associated with an event of the same `dedupid` as the new event. If
found, the ZenPack will associate the new event with the existing
incident.

A daemon `zenincidentpoll` will periodically connect to the remote
system to determine the status of incidents and perform actions (ie
close an event in Zenoss associated with an incident that is now closed
in the remote system).

These new fields are now available to be used in the Event Console:

-   `Incident`: the incident identifier from the remote system. This is
    clickable in the GUI and will take you to the remote system.
-   `Incident URL`: the URL used to construct the clickable link.
-   `Notification GUID`: an internal identifier to distinguish between
    multiple notification end-points.
-   `Incident Creation Time`: notes the time when the Incident was
    associated to the event. If an Event is associated to an existing
    Incident, then this time reflects the association time, not the time
    the existing Incident is created.
-   `Incident Trigger Name`: the name of the trigger that matched the
    event.
-   `Incident NotificationName`: the name of the notification that was
    triggered for the event.
-   `Incident Management Error`: short message if an error occurred
    while running the notification.
-   `Incident Management Error Detail`: detailed message if an error
    occurred while running the notification.

It is suggested that only the `Incident` field be added to Event
Consoles.

### Prerequisites

| Prerequisite       | Restriction                               |
|--------------------|-------------------------------------------|
| Product            | Zenoss 6.0.0 or higher                    |
| Required ZenPacks  | ZenPacks.zenoss.PS.QFramework &gt;= 1.4.0 |
| Other dependencies | None                                      |

### Usage

See the Zenoss Service Dynamics Administration Guide for more
information about triggers and notifications. Any issues detected during
the run of the notification will result in an event sent to the event
console as well as a message in the `zennotifyworker.log` file.

### Zopeurl

The *zopeurl* setting is used when generating event links in
notifications to set the external hostname that will be presented. This
is configured in the following config files on these services:

*NOTE*: The config file that is read for the *zopeurl* setting varies
per the list below. In general, automatic Incident creation from
Triggers will use the zennotify.conf file on the zenNotifyWorker
Service. For Incidents manually created from the Event Console, the
corresponding Zope services will use the zenactiond.conf file.

**Automatic Incident Generation** :widths: 15,54

| Service         | File           |
|-----------------|----------------|
| zenNotifyWorker | zennotify.conf |

**Manual Incident Generation** :widths: 15,54

| Service  | File            |
|----------|-----------------|
| Zope     | zenactiond.conf |
| zenapi   | zenactiond.conf |
| zendebug | zenactiond.conf |

A template zenactiond.conf file will be added to these services during
ZenPack installation, and set to the appropriate host automatically if
previously configured.

#### Configuration

The following common checkboxes are available:

| Default | Title                           | Description                                                                                                                                  |
|---------|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| True    | Enabled                         | Should the notification be used if triggered                                                                                                 |
| False   | Send Clear                      | Should we process the clear when a previously processed Event clears.                                                                        |
| True    | Send only on Initial Occurrence | Should ALWAYS be checked, otherwise may result in duplicate creates. Unchecking this will disable the updating of events with incident info. |

The following common checkboxes are available on the `Content` tab of
the `Edit Notification` window:

:widths: 4,20,45

| Default | Title                                                                                   | Description                                                                                                                                                                                                                                                          |
|---------|-----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| True    | Should event details and log be updated with success/fail info and incident number/url? | By default, events are updated when they are processed, indicating what trigger/notification processed them and including relevant information based on the success or failure of the notification. By setting this to False, no updates to the events will be made. |
| False   | Hide this notification from the event                                                   | If selected, hide this Notification from the Create Incident dropdown in the Event Console.                                                                                                                                                                          |
| False   | Acknowledge event on incident creation?                                                 | After creating an Incident, whether to acknowledge the Event in Zenoss                                                                                                                                                                                               |
| True    | One incident per event?                                                                 | When true, creating an incident in the event console results in one incident created for each selected event. When false, one incident is created for and associated with all selected events (applies only to manual Incident creation in the Event Console).       |

The following checkboxes are available on the `Content` tab of
the `Edit Notification` window for `Incident Integrate` type
notifications only:

:widths: 4,20,45

| Default | Title                                                                               | Description                                                                                                                                          |
|---------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| False   | Acknowledge event on incident assignment                                            | Whether to acknowledge the event in Zenoss when the incident has been assigned                                                                       |
| False   | Close event on incident resolution                                                  | Close the event if the incident is closed/resolved.                                                                                                  |
| True    | Close incident when the event is closed                                             | Update the incident to a closed state when the event is closed.                                                                                      |
| False   | Re-open incident when the event re-occurs                                           | Re-open the previously associated incident if a new event comes in that matches the deduplication id of an event that was associated to an incident. |
| True    | Re-open incident when the event is re-opened                                        | Re-open the previously associated incident if the event is manually re-opened in Zenoss.                                                             |
| True    | Assign incident again when the event is acknowledged                                | Update the incident when the event is assigned in Zenoss.                                                                                            |
| True    | Check to see if the incident is already closed before Assigning incidents to events | Polls the incident state before attempting to associate new events.                                                                                  |
| True    | Add notes added to the event to the incident                                        | Update the incident with Notes manually added to the event.                                                                                          |

#### Date Format Processing

There are two fields in the `Content` tab of all notifications provided
by the Incident Management ZenPack that deal with presentation of
date/time fields in data sent by the notification.

:widths: 15,20,34

| Default              | Title                      | Description                                                                                     |
|----------------------|----------------------------|-------------------------------------------------------------------------------------------------|
| %Y/%m/%d %H:%M:%S.%f | Date Time Format           | Format that date/time strings should use when being sent in notification data as strings.       |
| UTC                  | Date Time Format Time Zone | Timezone that date fields should be coerced to when being sent in notification data as strings. |

#### Associating to Existing Incidents

There are several controls that affect how and whether events get
associated to existing incidents. If "Check to see if the Incident is
already closed before assigning incidents to events" is not checked, new
events that come in with a deduplication signature matching an existing
event that has not yet aged out of the system will always be associated
to the incident that the matching event was associated to. If the
integration supports adding notes to an incident, this will cause a note
to be added to the incident saying "New event for existing incident",
along with the event id of the new event. If that box is checked, then
this association will only happen if the existing incident is still
open. However, if the "Re-open incident when the event re-occurs" is
also checked, then instead of simply associating to the existing
incident, that incident will, if the integration supports it, be
re-opened, regardless of whether the "Check to see if incident is
already closed..." is checked. If the integration does not support
re-opening, then a new incident will be opened, and a warning message
will be logged.

#### Field Mapping

Each integration builds a default dictionary of data used to create the
Incidents (as applicable to the individual integrations). The contents
of the fieldMapping configuration provides overrides to this data,
overriding default fields or adding in new fields. This allows
customizing the values sent to the ticketing system without modifying
code.

Each entry should be of the form **fieldname, value** with each entry on
a separate line. Example:

    Device, ${dev/title}
    comments, Created by Zenoss IncidentManagement

In addition to literals you can use TALES expressions for the value;
TALES processing for IncMan integrations supports Python expressions and
receives the following contexts:

evtThe EventdevThe Device associated with the eventcomponentThe
Component associated with the eventdmdProvides access to dmd for
advanced optionsurlsProvides access to several URLs related to the event
or device:eventUrlackUrlcloseUrldeviceUrleventsUrl (all events for the
device)reopenUrlbaseUrldefaultFieldsIntegration specific default fields
can be accessed via this context (see individual integration
documentation for available fields, if applicable)mappingUtilsProvide
access to Integration specific methods used to map or build field
values. These are typically used to build the default fields, available
in the defaultFields context.removeFieldA special flag that can be set
to delete a field from the field map sent to the external integration.
Typically used to delete a field from the defaults.jsonstringPasses data
through json.dumps() to output a JSON compatible string

The Zenoss Administration Guide contains more information on the
attributes available for Device and Event contexts.

##### mappingUtils Methods

These are the default methods available on the mappingUtils context. See
individual integrations for any custom methods added.

-   getDescription(event)

    > Builds a detailed description of the event details

-   getSevString(event)

    > Get the Zenoss Severity String (e.g., 'Clear', 'Error')
    > corresponding to an event.

##### Examples

Note that there may be many ways to accomplish the same thing, and this
is far from a comprehensive list:

-   Set a static value:

        comments, Created by Zenoss IncidentManagement

-   Set the field 'Device' to the associated Device title:

        Device, ${python: (dev.titleOrId())}
        - or -
        Device, ${dev/titleOrId}

-   Set the Comments with the Device URL:

        comments,Device: ${urls/deviceUrl}

-   Enforce a maximum Severity based on device Priority (must be a
    single line):

        severity,${python: '3' if hasattr(dev, 'getPriority') and int(dev.getPriority()) <= 800 and int(defaultFields.get('severity')) > 3 else defaultFields.get('severity')}

-   Using the mappingUtils method the create a new Description field:

        NewDescription,${python: mappingUtils.getDescription(evt)}

-   Remove the Description field from the Incident:

        description,${removeField}

-   Format a JSON data field (especially for use in the HTTP
    notification):

        {             "eventClass":${python: jsonstring(evt.eventClass)},
            "eventClassKey": ${python: jsonstring(evt.eventClassKey)}
        }

#### Create an Incident Manually

This assumes that notifications have already been created.

1.  Navigate to the event console.
2.  Select an event.
3.  Click on the `Create Incident` button at the top-right hand side and
    select the appropriate notification.

NOTE: In order for a manually created Incident to be updated when the
event clears or is acknowledged. The notification choosen must have the
following settings

1.  Send Clear in the Notification tab is checked
2.  There is an "Enabled" Trigger in that notification (also
    Notification tab)

#### Allow the `ZenOperator` Role to Create Incidents Manually

The `ZenOperator` ZenPack creates a new role to manage events. To enable
this new role to also be able to create an incident, follow these
actions for every notification to be displayed:

1.  Navigate to the event console.
2.  Click on the `Triggers` menu.
3.  On the left-hand side, click on the `Notifications` button.
4.  Double-click on the notification to edit it.
5.  Click on the `Subscribers` tab of the dialog box.
6.  From the pull-down menu, select the user or group to permit manual
    incident creation, and then click the `Add` button.
7.  Add all users and groups that require the permissions.
8.  Click on the `Submit` button to save the settings.

Now users should be able to refresh the event console to see the create
incident actions.

#### Associate Events with an Existing Incident

1.  Navigate to the event console.
2.  Select an event.
3.  Click on the `Create Incident` button at the top-right hand side
4.  *Right-click* the appropriate notification (as opposed to a
    left-click).
5.  An `Assign New Incident Number` dialog comes up. Type in the new
    incident number.
6.  Click on the `Okay` button.

NOTE: When associating events to an existing Incident, the Incident
Creation Time will reflect when the event was associated, not the
creation time of the existing Incident.

#### Notification Suppression

Suppression of incident creation can be enabled to avoid potential
floods.

1.  `zNotificationSuppressionThresholdNum`: The maximum number of
    notifications to create.
2.  `zNotificationSuppressionThresholdSecs`: The timeframe within which
    suppresion will be triggered by reaching the maximum.
3.  `zNotificationSuppressionDedupFormat`: The format for deduping
    events (default is `device|component|severity`).

Setting
either `zNotificationSuppressionThresholdNum` or `zNotificationSuppressionThresholdSecs` to `-1` will
disable suppression.

#### ZenPack Installation / Removal

Install or remove this ZenPack following the instructions in the Zenoss
Resource Manager Admin Guide matching your Zenoss RM version.

### Upgrading to IncidentManagement 3

IncidentManagement 3 introduces several major changes that may cause
issues when upgrading existing integrations. While out of the box
features should migrate without needing further configuration, any
customizations may require manual intervention to update.

It is recommended to test using a development system if possible, or
plan a maintenance window for troubleshooting should the need arise.
Recreating the Notifications may be necessary, so details of the
existing Notifications should be available, including any authentication
credentials that may need to be re-entered.

#### QFramework ZenPack

IncidentManagement now uses zenNotify provided by the QFramework
ZenPack. This is a replacement for zenactiond. This ZenPack must be
installed and zenactiond disabled before upgrading.

#### Customization ZenPacks

If you use a customization ZenPack to extend IncidentManagement
features, it may require updates to be compatible with this new version.
Contact Zenoss to review before proceeding.

#### ServiceNow Integration

The ServiceNow integration has been split into three Notification types:
Certified, ImportSet, and Legacy (see the ServiceNow specific
documentation for more details). Existing notifications will
automatically be migrated to one of these new Notifications.

The 'incident_state' field is now mapped within the Certified app
configuration. Users who had customized this should verify their
configuration.

The ServiceNow application (used for the Certified integration) must be
updated to version 2.0.15.

#### Slack Integration

The TALES processing for the messages has been updated to use the full
context available elsewhere in IncidentManagement (e.g., field
mappings). Existing use of '${evt/url}' will automatically be migrated
to '${urls/eventUrl}'.

#### Daemons

IncidentManagement actions may take place in these daemons:

-   zenactiondRuns any automatic actions, such as:Creating Incidents
    from TriggersUpdating Incidents when an Event clears

-   ZopeRuns most user-initiated actions, such as:Manually Creating
    Events from the Event ConsoleAssigning eventsRe-opening Events

-   zenincidentpollPeriodically checks the Incident status and updates
    the Event appropriately (if enabled in configuration).

#### Isolating Incident Management Traffic to a Specific Zope

For debugging purposes, it is sometimes useful to force the traffic to a
particular Zope in order to make use of a `pdb` debugger session, or to
more carefully observe the behavior of the system in isolation.

1.  Reduce Zope to a Single Instance

    > -   This is covered in the ZPL docs
    >     at <https://zenpacklib.zenoss.com/en/latest/development-environment-5.html>

2.  Attach to the zope service:

        serviced service attach zope

3.  change to user zenoss:

        su - zenoss

4.  Identify the `runzope` process currently running and get its pid
    (`ps -ef` or equivalent)

5.  Kill the currently-running process and start a new zope in the
    foreground in one line

    >     kill SIGTERM <zope-pid>; zopectl fg
    >
    > *Note: that last line is important to do all at once, otherwise
    > zope will be restarted in the background*

### Configuring zenincidentpoll

By default, zenincidentpoll checks existing Events every 60 seconds.
This can be modified similar to other services via Control Center:

-   open the zenincidentpoll service in Control Center
-   select 'Edit' for zenincidentpoll.conf
-   update the 'cycletime' property
-   restart the service once saved

### Related Daemons

| Type              | Name                        |
|-------------------|-----------------------------|
| Notification      | zenNotify / zenNotifyWorker |
| GUI               | Zope / zenapi / zendebug    |
| Event integration | zenincidentpoll             |

### Known Issues

| IncMan Versions | RM Versions | Issue                                                             | Workaround                                                          |
|-----------------|-------------|-------------------------------------------------------------------|---------------------------------------------------------------------|
| All             | 6.0 - 6.2.x | Password Fields Disappear when updating Notifications (ZEN-29814) | Password must be manually set each time the Notification is edited. |

### Change Log

Hotfix 3.3.1

-   Bug Fixes
    -   SVC-3383: Ensure zenincidentpoll checks the status of all
        incidents
    -   SVC-3381: ensure trigger info is available for clears as well
    -   SVC-3382: do not refresh clear from zep if not updating events
        with notificastion info
    -   SVC-3382: remove extra zep refresh when not updating events

Release 3.3.0

-   Bug Fixes
    -   SVC-2643: batch requests for zenincidentpoll for ServiceNow
    -   SVC-2643: Chunk requests in case we have too many incidents
    -   SVC-2837: add default values for Headers and Data fields in HTTP
        Notification, which includes setting user-agent
    -   SVC-3032: Changed closeCode field to configurable instead of
        hard code value
    -   SVC-3032: Added 'timeout' field to request, implemented handlers
        for different errors
    -   SVC-3032: made 'timeout' field provided by default visible
    -   SVC-3032: HTTP Notification Timeout made configurable
    -   SVC-3034: Remove cz0 prepend within fieldmapping context for
        smarViewUrl
    -   SVC-3320: check impactEvents exist before processing
    -   SVC-3319: dont update event if send_initial_occurence is false
    -   SVC-3323: update main documentation
    -   SVC-3323: formatting fixes to SNow docs
    -   SVC-2661: Change impact related event info from score to
        confidence rating to match data visible in UI
-   Features
    -   SVC-2660: Added additional fields for Impact events in order to
        be more user-readable.
    -   SVC-2660: Added getImpactDetails method in order to get correct
        Impact event details for each event.
    -   SVC-2660: added caching in order to prevent multiple calls of DB
    -   SVC-3121: Add detail fields for trigger and notification name,
        and populate when creating incident
    -   SVC-3122: triggerName and notificationName fieldmap for UI
        generated Incidents
    -   SVC-3122: add notification and trigger name to fieldmap using
        notification attributes
    -   SVC-3122: Unit test for Tal Context
    -   SVC-3122: use notification and trigger object in getTalcontext
    -   SVC-3122: add signal attributes for jira context test
    -   SVC-3319: Make updating events optional for IntegratorAction
    -   SVC-3323: update to use QFramework retry counter abstraction
    -   SVC-3323: rework HTTP notification and retry mechanisms; update
        docs
    -   SVC-3323: cleanup separation between Notification Action and
        Incident Integrate

#### Release 3.2.4

-   Bug Fixes
    -   Moved retry flow for HTTP notification actions to QFramework

#### Release 3.2.3

-   Bug Fixes
    -   Fixes HTTP notification won't send non-initial occurrences

#### Release 3.2.2

-   Bug Fixes
    -   Fixes tracebacks due to missing OAuth settings on non-supported
        integrations (problem introduced in 3.2.0)

#### Release 3.2.1

-   Bug Fixes
    -   Fixes an extra argument to a method call when processing HTTP
        Notifications, leading to tracebacks (problem introduced in
        3.2.0)

#### Release 3.2.0

-   Features
    -   ServiceNow log response details if hitting the REST API
        RateLimit
    -   Enable OAuth authentication for ServiceNow Import Set and
        Certified integrations.
    -   Added 'jsonstring' context for use in fieldMapping
        configurations

#### Release 3.1.1

-   Bug Fixes
    -   Allow ServiceNow Certified Notifications stateField to be
        customized.

#### Release 3.1.0

   Features

-   Added new contexts available in the fieldMapping configuration
    (defaultFields, mappingUtils,removeField)

   Bug Fixes

-   Prevent an event loop when processing errors if &ldquo;Send only on
    initial occurrence&rdquo; not selected(SVC-2666)
-   Don&rsquo;t add multiple zenactiond.conf config files (SVC-2664 /
    SVC-2602)

#### Release 3.0.4

-   SVC-2662: ignore suppression rules for events that have no device

#### Release 3.0.3

-   Add redis endpoint to zenincidentpoll service

#### Release 3.0.2

-   Fix &ldquo;403 Forbidden&rdquo; error when assigning an Incident when manually
    creating a ServiceNow incidentwhen REST API is used.

#### Release 3.0.1

-   Fix AddZenactiondConfToZope migration to support zopeurl configs
    with spaces (for when templating isused).

#### Release 3.0.0

-   Switch to using zenNotify (from QFramework) for processing instead
    of zenactiond
-   Add Incident Creation Time field to events.
-   Add SmartView Urls for supported systems (urls/smartViewUrl)
-   Fix invalid Device URLs generated for descriptions.
-   Attempt to automatically set zopeurl during installation
-   ZenNotify (QFramework) will create events for failed notifications.
-   ServiceNow: Split action types into Legacy, ImportSet, and Certified
-   ServiceNow: Remove Deprecated JSONv1 support
-   ServiceNow: Add REST API connection
-   ServiceNow: Support ImportSet API
-   ServiceNow: Remove invalid \[code\] links for URLs in descriptions
-   ServiceNow: The SN IncidentManagement Application updated to version
    2.0.11.
-   Slack: add Re-open support
-   Slack: TALES Processing for messages now supports the same options
    as the rest of IncMan
-   Slack: Fix NotImplementedError encountered during closing events
-   Slack: Fix &lsquo;double close&rsquo; messages during close/clear events.
-   Slack: Fix not creating new incidents due to incorrect deduplication
    rules.

Release 2.9.4

    Bug Fixes

-   Deleting a Notification leads to tracebacks during polling if open
    events existed

    Features

-   &lsquo;Re-open incident when the event re-occurs?&rsquo; configuration added to
    control re-open functionality.
-   ServiceNow &lsquo;Incident Final States&rsquo; configuration added (default &lsquo;7&rsquo;)
-   Extensive documentation updates.

Release 2.9.3

    Bug Fix

-   When more than one Notification is configured, Incident polling may
    have used the incorrect settings.

Release 2.9.2

    Bug Fix

-   Slack Integration now raises exception with details from invalid API
    responses.
-   Fix &lsquo;BadRequest&rsquo; Exception when creating Incidents manually from the
    Event Console.

Release 2.9.1

    Bug Fix

-   Fixes an exception from formattedDatetime after some upgrades to
    2.9.0

## Attachments:

-   [servicenow-logo-partner_0\_1.png](img/zenpack-servicenow-logo-partner_0_1.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/IncidentManagement/zenoss-integration-services-ds.pdf){.external-link}
-   [servicenow-logo-partner_0\_1.png](img/zenpack-servicenow-logo-partner_0_1.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/IncidentManagement/zenoss-integration-services-ds.pdf){.external-link}
-   [servicenow-logo-partner_0\_1.png](img/zenpack-servicenow-logo-partner_0_1.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/IncidentManagement/zenoss-integration-services-ds.pdf){.external-link}
-   [servicenow-logo-partner_0\_1.png](img/zenpack-servicenow-logo-partner_0_1.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/IncidentManagement/zenoss-integration-services-ds.pdf){.external-link}


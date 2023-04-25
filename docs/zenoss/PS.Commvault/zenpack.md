# CommVault Integration Service

@lb[](img/zenpack-zenpack-general.png)

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

CommVault Integration Service

**Release:**

2.1.2

### More Information:

## CommVault Integration Service

## About

An implementation of a Commvault API client, used to query a Commvault
system for backup job status and generate events for failed backups and
clears for completed backups.

Jobs associated with Client 0 and Subclient 0 are currently ignored, as
these are back-end Commvault jobs, not client backups.

All backup job related events generated via the API query will be placed
in the /Commvault EventClass. Errors from the API client will appear in
the /Status/Commvault EventClass.

This ZenPack also accepts SNMP traps from Commvault and translates them
into Zenoss events. SNMP trap events will be placed in the
/Perf/Commvault EventClass.

## Limitations

ZenPack is designed for support Commvault 10 and 11 for traps, and the
API client was written for API version 11SP16.

## Prerequisites

| Prerequisite       | Restriction                                                              |
|--------------------|--------------------------------------------------------------------------|
| Product            | Zenoss 6.1.0 or higher                                                   |
| Required ZenPacks  | ZenPacks.zenoss.ZenPackLib &gt;= 2.0 ZenPacks.zenoss.PS.Util &gt;= 1.9.0 |
| Other dependencies | None                                                                     |

## Features

### Device Classes

A new device class **/Storage/Commvault** will be added

-   /Storage/Commvault

### Configuration

Configuration of the API connection is via 3 mandatory and 3 optional
zProperties:

-   zCommvaultBaseUrl

    -   Base URL, including port and path, through which to connect to
        the Commvault API. This can be either a Commvault Web Server
        (eg.
        <http://server1.company.com:81/SearchSvc/CVWebService.svc/>) or
        a Commvault Web Console
        (eg. <http://webclient.company.com/webconsole/api/>)

-   zCommvaultUsername

    -   The name of the CommCell Console user. For Active Directory (AD)
        users, an email address can be used.

-   zCommvaultPassword

    -   Password for the specified user.

-   zCommvaultResponseTimeout

    -   Timeout in seconds for responses to Commvault REST API queries

-   zCommvaultValidateHttpsCert (default: True)

    -   Should HTTPS certificate be validated. Should be set to False
        for self-signed certificates.

-   zCommvaultDomain (optional)

    -   If the user logging in is a domain user, the domain parameter
        must be set to the domain associated with the user.

-   zCommvaultCommServer (optional)

    -   Optionally log in to a remote CommServe. If this parameter is
        blank, the user is logged in to the CommServe associated with
        the Web Server/Console specified in the BaseUrl.Use the
        following format:
        &lt;commserve_host_name&gt;\*&lt;commserve_name&gt; (literal
        asterisk between hostname and name)eg.
        [client.mydomain.com](http://client.mydomain.com){.external-link}\*testcs

Selection of jobs for event creation and clearing is via 3 zProperties:

-   zCommvaultJobIncludeStateList of all Commvault job state strings
    (exact match only) that should trigger an event if
    seenDefaultFailedCompletedCompleted with one or more errors

-   zCommvaultJobClearStatesList of Commvault job state strings (exact
    match only) that should generate a clear
    eventDefaultCompletedCompleted with one or more errors

-   zCommvaultJobIgnoreStatesList of job state strings (exact match
    only) to ignore if zCommvaultJobIncludeStates list is emptyDefault:
    empty list

### Trap Events

List of CommVault snmp traps

-   simpanaAlertAuxCopy
-   simpanaAlertCommcell
-   simpanaAlertDataAging
-   simpanaAlertDataProt
-   simpanaAlertDataRecov
-   simpanaAlertDataVerifi
-   simpanaAlertDeviceStatus
-   simpanaAlertEraseData
-   simpanaAlertFLRJob
-   simpanaAlertFTPDownload
-   simpanaAlertLibrary
-   simpanaAlertLibraryManagement
-   simpanaAlertMediaAgents
-   simpanaAlertOfflineContentIndexing
-   simpanaAlertSchedules
-   simpanaAlertStoragePol
-   simpanaAlertVaultTracker
-   simpanaAlertExpRecov
-   simpanaAlertMediaInvent
-   simpanaAlertMediaErase
-   simpanaAlertClients
-   simpanaAlertClientDist
-   simpanaAlertAppExchange
-   simpanaAlertDownloadAvail
-   simpanaAlertAppFLR
-   simpanaAlertUpgrUpdates
-   simpanaAlertSharepoint
-   simpanaAlertSRM
-   simpanaAlertReport
-   simpanaAlertInfoManagement:

## Changelog

2.1.2

-   Bug FixesSVC-2702: doc updatesSVC-2700 Add clear event on success
    CommvaultJobPlugin runSVC-3390: set instanceName to UnknownInstance
    if not returned

2.1.1

-   Bug FixesSVC-3075: fix compatibility with PS.Util 1.9.4+, add
    default responseTimeout

2.1.0

-   FeaturesSVC-2618: update test data, expand job query to include
    synthfullSVC-2618: allow for self-signed https certs, update docs

2.0.1

-   FeaturesSVC-2618: add event details to zep for trigger functions and
    grid display

2.0.0

-   FeaturesSVC-2495: use Commvault API to retrieve backup job status
    and create events

1.0.1

-   Bug FixesSVC-2227: expose some previously debug logging

1.0.0

-   Initial release for SNMP trap reception

## Attachments:

-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/PS/zenoss-integration-services-ds.pdf){.external-link}


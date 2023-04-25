# PureStorage Integration ZenPack

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

PureStorage Integration ZenPack

**Release:**

2.2.2

## PureStorage Integration ZenPack

This ZenPack is designed to monitor Pure Storage FlashArray devices.
Currently only the Pure Storage REST API v1.4 and 1.18 are supported.

## Prerequisites

The table lists the Zenpack dependencies.

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
<td>Zenoss 6.0.0 or higher</td>
</tr>
<tr markdown="1">
<td>Required ZenPacks</td>
<td><ul>
<li>ZenPacks.zenoss.PythonCollector &gt;=1.10.0</li>
<li>ZenPacks.zenoss.ZenPacklib &gt;=2.1.0</li>
<li>ZenPacks.zenoss.PS.Util &gt;=1.9.4</li>
</ul></td>
</tr>
<tr markdown="1">
<td>Other dependencies</td>
<td>None</td>
</tr>
</tbody>
</table>

## Usage:

PureStorage devices should be added under the "*/Storage/PureStorage*"
deviceClass. Connectivity & polling is configured via the following
zProperties:

-   zPureStorage_API_key

    -   Function: The API key to access the Purity API.

    -   Default: none

    -   Notes: This property must be set in order to access the API.

-   zPureStorageVolumeIgnoreNames

    -   Function: Sets a regular expression of Volume names to ignore
        during modeling.

    -   Default: empty

-   zPureStorageUrlBase

    -   Function: Sets the PureStorage base API URL.

    -   Default: 'https://${here/manageIp}/'

-   zPureStorageAPITimeout:

    -   Function: Purestorage REST API response timeout

    -   Default: 5

-   zPureStorageValidateSSLCert

    -   Function: Validate PureStorage HTTP SSL Certificate

    -   Default: true

### Legacy zProperties

If '**zPureStorageUrlBase**' has a value, it will override these legacy
zProperties.

> -   zPureStorage_port
>
>     -   Function: The port on the target to send HTTP requests to.
>
>     -   Default: 443
>
>     -   Notes: The default should always work on real devices. Assumes
>         URL hostwill be the device's managedIP.
>
> -   zPureStorage_use_https
>
>     -   Function: Whether to use HTTPS. If false, HTTP will be used.
>
>     -   Default: true
>
>     -   Notes: The default should always work on real devices. Assumes
>         URL host will be the device's managedIP.

## Changelog

2.2.2

       SVC-3004: Update to support new API response, "versions"
SVC-3092: Improve API handling between API versions

       SVC-2943: ShelfController handling

2.2.1

      SVC-2765 Fix HostGroup modeler API data consolidation None/Value
scenario SVC-2766 Backward api 1.4 compatibility fixes

2.2.0

      SVC-2435:

-   Overhaul of the API client
-   Add support for PureStorage API version 1.18
-   New zProperties: zPureStorageUrlBase & zPureStorageAPITimeout
-   New components: Drive, Fan, PowerSupply, & TemperatureSensor
-   Separate out monolithic modeler plugin into separate modeler plugins
-   Added NetworkInterface component polling and graphs
-   New Host component relationships: Port & Volume
-   UI cleanup, removing fields from grid display

     SVC-2497 FIX: changing modeled attributes to numeric values

-   networkInterface component 'speed' attribute
-   volume component 'size' attribute
-   snapshot component 'size' attribute

2.1.2

     SVC-1996:

-   Updated to support ZPL v2.0
-   Update to Volume metric polling

2.1.1

     SVC-1240 Fix: Handle 0 value in scaling causing traceback

2.1.0

     SVC-1103 Enhancement, configureable method to ignore by Volume
names

2.0.1

     Fix: Handle Hosts without detailed Status during Modeling

2.0.0

     SVC-653: The first generic release of the PS.PureStorage ZPL



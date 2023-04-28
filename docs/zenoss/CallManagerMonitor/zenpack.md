# Cisco Unified Communications Manager

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.CallManagerMonitor

### Applications Monitored:

Cisco Unified Communications Manager (5-10)

Cisco CallManager (5-10)

## Cisco Unified Communications Manager ZenPack

Allows collection of metrics from Cisco Unified Communications Manager
using the AXL-Serviceability APIs.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 4.3.0- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2016/04/08:   Compatible with Zenoss Resource Manager 4.1.x, Zenoss Resource
    Manager 4.2.x, Zenoss Resource Manager 5.x

<!-- -->

Version 4.2.3- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2014/10/23:   Compatible with Zenoss Resource Manager 4.1.x, Zenoss Resource
    Manager 4.2.x

## Background

This ZenPack provides support for monitoring Cisco Unified
Communications Manager and other Cisco Unified Communications
applications by interfacing with the [Cisco AXL-Serviceability APIs](http://developer.cisco.com/web/axl){.external-link} to collect
metrics through the *PerfmonPort* API, and modeling registered phones
through the *Real-Time Information or RisPort* API.

Support also exists for simulating the phone login process to a CUCM.

## Monitoring CUCM Metrics

The ZenPack installs an example monitoring template named *CallManager*.
This monitoring template contains the following datasources and
datapoints.

-   axl (CiscoAxlPerf Datasource)
    -   CallsAttempted
    -   CallManager HeartBeat
    -   CallsActive
    -   CallsCompleted
    -   CallsInProgress
    -   InitializationState
    -   MTPOutOfResources
    -   MTPResourceActive
    -   MTPResourceAvailable
    -   MTPResourceTotal
    -   RegisteredHardwarePhones
-   registeredPhones (SNMP Datasource)
    -   registeredPhones

To monitor these metrics on a CUCM server you must bind the
*CallManager* monitoring template to the server, or the server's device
class. You must also properly configure the zAxlUsername and
zAxlPassword for the server. If the server knows itself by a different
name than Zenoss knows it by, you must also configure the zAxlHostname
to be the name by which the server knows itself.

To monitor additional performance metrics beyond what's included in the
default monitoring template, you must add new CiscoAxlPerf datasources.
To do this you first have to know what metrics you want to monitor, and
on what object they exist. You can find this information from a Cisco
document named *Cisco Unified Real-Time Monitoring Tool Administration
Guide*. There will be a version of this document for every Cisco Unified
Communications release, and the relevant performance object and counter
information can be found in one of the *Performance Counters and Alerts*
appendices. See the following link for an example of one of these
appendices.

[Performance Objects and Counters for Cisco Unified CM Version 8.6(1)](http://www.cisco.com/en/US/docs/voice_ip_comm/cucm/service/8_6_1/rtmt/rtpmcm.html){.external-link}

To add monitoring for the *PRIChannelsActive* and *VideoCallsActive*
counters on the *Cisco CallManager* object mentioned in that document,
you would use the following steps.

1.  Add a new CiscoAxlPerf datasource to a new or existing monitoring
    template
2.  Set the datasource's Performance Object field to *Cisco CallManager*
3.  Add *PRIChannelsActive* and *VideoCallsActive* to the Counters
    field. One per line.
4.  Add datapoints named *PRIChannelsActive* and *VideoCallsActive* to
    the datasource
5.  Add thresholds or graphs for the new datapoints as desired

Note that you can collect one or all of the counters within a single
performance object using a single datasource, but it requires one
datasource per performance object if you need to collect from multiple
objects. For this reason, a good convention is to name the datasource
after the performance object it will be querying.

## Simulating a Phone Login

The ZenPack installs an example monitoring template named
*CiscoIPPhone*. This monitoring template contains the following
datasources and datapoints.

-   ipPhone (CiscoIPPhone Datasource)
    -   loginTime
    -   logoutTime

To test phone login to your CUCM you must bind the *CiscoIPPhone*
monitoring template to the CUCM server, or to the server's device class.
You must also double-click the datasource to set or verify the following
fields.

-   IP Phone
    -   Password (Sequence)
    -   Device Name
    -   Username (UserID)
    -   Model
    -   SDK Version
    -   Display
-   CallManager
    -   Hostname

All fields except Password, Device Name and Username have default values
that should work in most cases.

## Modeling Registered Phones

The ZenPack adds a modeled plugin named *zenoss.axl.RegisteredPhoneMap*
that is not enabled by default for any device classes. If you want to
model an inventory of the phones registered to CUCM servers, you must
perform the following steps.

1.  Create a new device class for CUCM servers such as
    /Server/Linux/CUCM
2.  Change the zPythonClass configuration property of the new device
    class to *ZenPacks.zenoss.CallManagerMonitor.CallManager*
3.  Enable the *zenoss.axl.RegisteredPhoneMap* modeler plugin for the
    new device class
4.  Move CUCM servers into the new device class
5.  Verify that the zAxlUsername, zAxlPassword and zAxlHostname
    configuration properties are set for the individual CUCM servers
6.  Remodel the CUCM servers

There is currently a limitation that prevents more than 200 registered
phones from being modeled for a single CUCM server.

## Prerequisites

The following conditions must be met for this ZenPack to function. These
conditions are in addition to the Zenoss platform version and any other
ZenPack dependencies called out for each release.

Running processes:

-   The zencommand process must be running for any configure
    CiscoAxlPerf or CiscoIPPhone datasources to be collected.
-   The zenperfsnmp process must be running for any configured SNMP
    datasources to be collected.
-   The zenmodeler process must be running for phones to be periodically
    remodeled on CUCM devices. This is only necessary if the
    zenoss.axl.RegisteredPhoneMap modeler plugin has been enabled for
    one or more devices.

Network access:

-   Collector server to either 8443/tcp, 443/tcp or 80/tcp depending on
    the CUCM version being monitored. It is recommended that all of
    these ports be opened to allow for faster automatic identification
    of the CUCM version.

## Troubleshooting

If the SNMP based values on the *CallManager* graphs are seen as *nan*,
please check that:

-   *zenperfsnmp* process is running.
-   *zSnmpCommunity* is set to the community permitted and the *Cisco
    CallManager SNMP Service* is activated on the CUCM server.

## Installed Items

Installing the ZenPack will add the following items to Zenoss.

Configuration properties:

-   zAxlHostname
-   zAxlPassword
-   zAxlUsername

Datasource types:

-   CiscoAxlPerf
-   CiscoIPPhone

Monitoring templates:

-   CallManager (in /Devices)
-   CiscoIPPhone (in /Devices)

Modeler plugins:

-   zenoss.axl.RegisteredPhoneMap

Event classes:

-   /Perf/CallManager
-   /Status/CallManager

## Changes

**4.3.0** (2016-04-08)

-   Compatibility with Zenoss 5.x.
-   Fix missed relations from CallManager to IP Phones (ZEN-22781).

**4.2.3** (2014-10-21)

-   Fix issue with modeling of zero devices (phones).
-   Add troubleshooting section to documentation.

**4.2.2** (2013-11-21)

-   Strip invalid XML responses and handle alternate successful login.

**4.2.1** (2013-05-06)

-   Request all counters used in datapoints.
-   Fix stacking on MTP Resources graph.
-   Restore compatibility with Zenoss 4.1 and earlier.

**4.2.0** (2013-03-08)

-   Remove dependency on ZenPacks.zenoss.CiscoMonitor.
-   Remove /Server/Linux/CallManager device class.
-   Remove site-specific default thresholds.
-   Add "Cisco UC" category to zAxl\* configuration properties.
-   Documentation and code cleanup for general availability.

**4.1.2** (2013-01-25)

-   Add zAxlHostname configuration property.
-   Fix support for UC9.

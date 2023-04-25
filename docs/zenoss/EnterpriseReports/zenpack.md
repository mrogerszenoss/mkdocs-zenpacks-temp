# Enterprise Reports

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.EnterpriseReports

## Enterprise Reports ZenPack

The EnterpriseReports ZenPack adds new reports to the standard Resource
Manager reports

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.EnterpriseReports ZenPack adds a variety of reports
to Zenoss platform.

Reports include:

-   Organizer Availability
-   Organizer Graphs
-   95th Percentile
-   Users Group Membership
-   Maintenance Windows
-   Notifications and Triggers by Recipient
-   Interface Volume
-   Event Time to Resolution
-   User Event Activity
-   Datapoints per Collector
-   Interface Utilization
-   Data Sources in Use
-   Defined Thresholds
-   Network Topology
-   Customized Performance Templates
-   Cisco Inventory
-   Guest to Datapools

To access the reports, select Reports from the Navigation bar. The
reports appear in the left panel.

## Prerequisites

|                   |                                   |
|-------------------|-----------------------------------|
| Prerequisite      | Restriction                       |
| Product           | Zenoss platform 6.x or higher     |
| Required ZenPacks | ZenPacks.zenoss.EnterpriseReports |

## Organizer Availability

Provides the availability percentage of all network organizers in the
system. This report can be filtered by organizer, event class,
component, and date.

You can report on the availability of device classes, locations,
systems, or groups within a defined time frame. This report offers two
reporting modes:

-   **Averaged** - Defines the organizer as available for the average
    availability time for all devices contained in it.
-   **Coalesced** - Defines the organizer as available only if all
    devices are available during a certain time period.

Two modes of operation: Averaged - defines the organizer as available
for the average availability time for all the devices contained within
it. Coalesced - defines availability of the organizer as the available
only if all devices are available during a certain time period.

## 95th Percentile

The 95th Percentile report provides details about all network interfaces
in the system, sorted by highest utilization.

95th percentile is a widely used mathematical calculation that evaluates
the regular and sustained utilization of a network connection. The 95th
percentile method more closely reflects the needed capacity of the link
in question than other methods (such as mean or maximum rate).

This report is useful for network capacity planning and billing for
either average or 95th percentile bandwidth utilization.

You can filter this report by device name. Enter a complete or partial
name (using \* (asterisk) for matching), and then click **Update** to
filter the report.

To change the reporting time period, enter Start and End dates (or click
**Select** to select dates from a calendar). Click **Update** to refresh
the report.

## Users Group Membership

Shows all users and the groups to which they belong.

## Maintenance Windows

The Maintenance Windows report shows all defined windows that are active
during a selected time period.

To change the reporting time period, enter Start and End dates (or click
**Select** to select dates from a calendar). Click **Update** to refresh
the report.

## Interface Volume

The Interface Volume report shows network interface volume. It reports
on all network interfaces in the system, sorted by highest utilization.
Volume is defined as the total number of bytes transferred during a
specific reporting period.

This report is useful for determining billing on total bandwidth
consumption.

To change the reporting time period, enter Start and End dates (or click
**Select** to select dates from a calendar). Click **Update** to refresh
the report.

## Event Time to Resolution

The Event Time to Resolution report shows, for each user, the total time
taken to acknowledge or clear events. Results are organized by event
severity.

This report is helpful for tracking response time SLAs in a NOC-type
environment.

## User Event Activity

Reports the total number of events acknowledged and cleared, on a
per-user basis, during the reporting period.

This report is helpful for tracking operator activity in a NOC-type
environment.

## Datapoints Per Collector

Shows the number of devices and data points per collector, which is
useful for gauging how much monitoring load is on each collector.

## Defined Thresholds

The Defined Thresholds report provides details about all thresholds
defined in the system. The report links to the target of each threshold.
The target can be a device class, individual device, or individual
component.

This report is useful for administering the system. You can use it to
quickly identify which threshold events can occur within the system, and
the severity of those events.

## Network Topology

Shows the layout of the network, according to the routes that Zenoss
platform understands, starting from the collector and ending at the
remote devices associated with the collector.

The report does not return data if the host on which the Zenoss platform
collector is running does not have a device created in the DMD. Create a
device representing the collector in the DMD, and then run report again.

An invalid route entry (for example, 'Missing link here' value in the
Route column) indicates that Zenoss platform cannot determine how to
route from one device to another. Correct this by adding a network
interface to the model (no new hardware required) and then adding a new
route entry from the last device in the route to the device (the IP
address shown at the far right of the table).

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)


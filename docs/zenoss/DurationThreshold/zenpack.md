# Duration Threshold

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.DurationThreshold

## Duration Threshold ZenPack

This ZenPack adds the *DurationThreshold* threshold, which will apply
the threshold comparison value against specified datapoints over a
specific time range, and send an event when a certain percentage of the
values violate the threshold. This can be used to create an event when a
condition appears and clears over a particular time range.

## Releases

Version 2.0.5 [Download](https://delivery.zenoss.com/){.external-link}:   Released: 2018-04-06:   Compatible with Zenoss 4.2.X - 6.1.X

<!-- -->

Version 2.0.4 [Download](https://delivery.zenoss.com/){.external-link}:   Released: 2017-05-01:   Compatible with Zenoss 4.2.X - 5.2.X

## Features

A new threshold, *DurationThreshold*, that allows the following to be
specified.

-   Time period of how far back the values should be evaluated.
-   A percentage number that allows for the threshold to be violated a
    number of times before causing an exception.

Note that *NaN* values are ignored, and so are empty RRD files in Zenoss
4.x.x.

## Usage

Follow these steps to monitor the values of a datapoint collected over a
period of time.

1.  Navigate to device Configuration Properties
2.  Navigate to the desired Monitoring Template.
3.  In the right-hand pane, click on the ''+'' button to add a
    threshold.
4.  Select the ''DurationThreshold'' option from the ''Type'' field,
    type in a name for the threshold and then click on the ''Add''
    button.
5.  Click on the newly added threshold.
6.  Enter information into the dialog box about the threshold.
    -   Datapoints: select the datapoints to which this threshold should
        apply.
    -   Severity: choose the appropriate severity.
    -   Enabled: should this threshold be used or not?
    -   Minimum Value: create an event if values fall below this value
    -   Maximum Value: create an event if values fall above this value
    -   Event Class: What event class to which events will be
        associated.
    -   Escalate Count: after this number of threshold events created,
        increase the severity by one (eg Error -&gt; Critical). The
        severity does not increase further after the initial escalation.
    -   Time period: provide a time period using time operators like
        ''month'', ''weeks'', ''day'', ''hours'', ''minutes'',
        ''seconds'', or just the number of seconds. An example: ''1 hour
        5 minutes 10 seconds''
    -   Percentage of violations to trigger an event: a number from 0
        (any violation triggers an event) to 100 (all values must
        violate the threshold)
7.  Click on the \`\`Save\`\` button to save the changes.

Alternatively Custom Properties can be defined and used for time period
and percentage of violations. Consult the Custom Properties section of
Administrator Guide for details.

## Caveats

The follow caveats apply to this ZenPack.

### Zenoss 5.0.x Caveats

The DurationThreshold requires access to the Zenoss CentralQuery service
when used with Zenoss versions 5 or later. In Zenoss 5.0.x only (not
Zenoss 5.1.x or later) the collector services do not have access to
CentralQuery by default.

Follow these steps to allow Zenoss 5.0.x to allow DurationThreshold to
work. These steps are not necessary on Zenoss versions 5.1 or later.

The following steps use the zencommand collector service as an example.
You would need to edit every collector service that might need to
evaluate a DurationThreshold.

1.  Log into the Zenoss master host.

2.  sudo serviced service edit zencommand

3.  search the word "Endpoints". Endpoints is an array of objects. Add
    the following object to Endpoints:

        {             "Name": "zproxy",             "Purpose": "import",             "Protocol": "tcp",             "PortNumber": 8080,             "PortTemplate": "",             "VirtualAddress": "",             "Application": "zproxy",             "ApplicationTemplate": "zproxy",             "AddressConfig": {                 "Port": 0,                 "Protocol": ""             },
            "VHosts": null,
            "AddressAssignment": {                 "ID": "",                 "AssignmentType": "",                 "HostID": "",                 "PoolID": "",                 "IPAddr": "",                 "Port": 0,                 "ServiceID": "",                 "EndpointName": ""             }
        },

4.  Save the file.

5.  sudo serviced service restart zencommand

6.  Repeat above steps for all Zenoss collector hosts.

## Changes

**2.0.5**

-   Add component_guid to Duration Threshold events. (ZPS-1940)
-   Fix memory leaks. (ZPS-1966)
-   Tested with Zenoss Resource Manager 4.2.5 RPS 743, 5.3.3, and 6.1.2

**2.0.4**

-   Encode self.TimePeriod in checkRaw() into an ascii string.
    (ZPS-1420)

**2.0.3**

-   Restore event.current field to be current value of datapoint.
    (ZPS-1223)
-   Clear misconfiguration events when configuration is fixed. (ZPS-675)

**2.0.2**

-   Fix error when using multiple duration thresholds on same datapoint.
    (ZPS-1133)
-   Support new contextMetric capability in Zenoss 5.2.3. (ZEN-27018)

**2.0.1**

-   Prevent excessive authorization calls slowing Zenoss UI. (ZPS-548)
-   Evaluate thresholds in real time instead of one cycle delayed.
-   Fix event summaries to no longer refer to "High Queue Latency".
    (ZPS-671)
-   Support multiple datapoints in the same duration threshold.

**2.0.0**

-   Allow Custom Properties for time period and violation threshold and
    their use in duration threshold UI.
-   Re-format event messages.
-   Generate event if neither maximum threshold nor minimum threshold is
    defined.
-   Zenoss 5.x.x compatibility.

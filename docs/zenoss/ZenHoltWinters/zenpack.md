# Holt-Winters Threshold

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.ZenHoltWinters

## Holt-Winters Threshold ZenPack

The ZenHoltWinters ZenPack adds the ability to create threshold events
when a device exceeds cyclical predicted values. The Holt-Winters
exponential smoothing algorithm is used for this prediction.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.ZenHoltWinters ZenPack adds the ability to create
threshold events when a device exceeds cyclical predicted values.

The
[Holt-Winters](http://en.wikipedia.org/wiki/Holt-Winters){.external-link}
exponential smoothing algorithm is used for predictiond. For more
information on RRD and Holt-Winters, refer to the
[rrdcreate](http://oss.oetiker.ch/rrdtool/doc/rrdcreate.en.html#IAberrant_Behavior_Detection_with_Holt_Winters_Forecasting){.external-link}
command.

Warning: This ZenPack is not compatible with Zenoss 5 and later.

Warning: Zenoss platform relies on the existence of Holt-Winters RRAs
within an RRD file. After adding Holt-Winters thresholds, the RRD files
will need to be re-created so that the new configuration can occur. You
will have to remove any existing RRD files so that new files can be
created.

Removing RRD files will remove all historical information associated
with these RRD files.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.2 or higher |
| Required ZenPacks | ZenPacks.zenoss.ZenHoltWinters            |

## Add a Predictive Threshold

1.  Navigate to the template that you want to modify.

2.  From the Thresholds area, click (Add Threshold).

3.  Provide a name for the new threshold and select the
    `HoltWintersFailure` threshold type, and then click **Add**.

4.  Choose the data source to which the threshold should be applied.

5.  Specify the parameters for the prediction engine.

    Predictive Threshold Data Source Threshold Options
    |        |                                                                                                         |
    |--------|---------------------------------------------------------------------------------------------------------|
    | Name   | Description                                                                                             |
    | Rows   | The number of points to use for predictive purposes.                                                    |
    | Alpha  | A number from 0 to 1 that controls how quickly the model adapts to unexpected values.                   |
    | Beta   | A number from 0 to 1 that controls how quickly the model adapts to changes in unexpected rates changes. |
    | Season | The number of primary data points in a season. Note that Rows must be at least as large as Season.      |

6.  Click Save to save your changes.

7.  Remove the RRD file or files that correspond to the data source
    selected in a previous step.

        cd $ZENHOME/perf/Devices
        rm device_names/DataSource_DataPoint.rrd

    Note: Removing the RRD files does result in a loss of historical
    information.

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


# Cloud View

## CloudView ZenPack

This ZenPack defines reports for
Cloud related technologies including Serverless functions.

## Releases

@lb[](img/zenpack-image2019-10-24_12-11-20.png)

Version 1.0.0 [Download](https://delivery.zenoss.com/){.external-link}
      Released: 2019-10-23
      Compatible with Zenoss 6.3+ and Zenoss Cloud

  Requires: [ZenPackLib](https://help.zenoss.com/in/zenpack-catalog/open-source/zenpacklib){.external-link}

### Features

The following features are added by this ZenPack:

-   Reports with graphs for serverless function usage from AWS, Azure,
    GCP:
    -   Total functions counts per provider (AWS, Azure, and GCP)
    -   Top Functions by Invocation Count
    -   Top Functions by Average Duration
    -   Top Functions by Errors Rate
    -   Top Accounts by Functions Count

### Requirements

At very least, one of the following ZenPacks, should be installed and
modeled with related Cloud Functions:

-   Microsoft.Azure ZenPack &gt;= 2.1.0
-   GoogleCloudPlatform ZenPack &gt;= 1.1.0
-   AWS ZenPack &gt;= 5.0.0

### Usage

In order to generate a report, relevant configuration options have to be
defined. These options include:

-   Providers: AWS, GCP, Azure. Functions of which providers will be
    displayed on graphs. It can be selected either one or more.
-   Time Range: Metrics will be collected to display graphs for the
    given time period selected.  Time can be selected either from a
    predefined date ranges or a custom time range.

### Troubleshooting

General troubleshooting steps:

1\. Verify that at least one device of provider (AWS, GCP, Azure) is
modeled with Cloud Functions.
2. Verify that Cloud Functions metrics are successfully collecting
(especially: *invocations*, *execution time*, and *errors*).

### Serverless Report

The following graphs as a report are included with this ZenPack. It can
be found in the Cloud View report organizer.

-   Total functions counts per provider (AWS, Azure, and GCP).
    @lb[](img/zenpack-providers_graph.png){.confluence-embedded-image width="600"}
-   Top Functions by Invocation Count: Shows top 10 functions by
    invocation count, with the information about provider and account of
    function.
    @lb[](img/zenpack-invocations_graph.png){.confluence-embedded-image width="600"}
-   Top Functions by Average Duration: Shows top 10 functions by average
    duration, with the information about provider and account of
    function. Units of time - seconds.

@lb[](img/zenpack-duration_average_graph.png){.confluence-embedded-image width="600"}

-   Top Functions by Errors Rate: Shows top 10 functions by error rates,
    with the information about provider, account, errors and invocations
    count of function. Units of rate - percent.
    @lb[](img/zenpack-error_rates_graph.png){.confluence-embedded-image width="600"}
-   Top Accounts by Functions Count: Shows top 10 accounts by functions
    count, with the information about the provider of account.

@lb[](img/zenpack-accounts_graph.png){.confluence-embedded-image width="600"}

### Changes

**1.0.0**

-   Initial release.
-   Tested with Zenoss 6.4.1 and Zenoss
    Cloud.

# Enterprise Collector

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.EnterpriseCollector

## Enterprise Collector ZenPack

The Enterprise Collector ZenPack allows collector daemons to start and
monitor devices, even if a connection to ZenHub is not available when
the daemon starts.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.EnterpriseCollector ZenPack allows several collector
daemons to start and to monitor devices, even if a connection to zenhub
is not available when a collector daemon starts.

With this ZenPack, the following collector daemons gain configuration
caching:

-   zenwin
-   zeneventlog
-   zenwinperf
-   zenprocess

Data and events are cached locally and are sent to zenhub as needed
after a connection is re-established. Cached configuration data is
stored in $ZENHOME/perf/Daemons/MonitorName/DaemonName-*Suffix*, where
*Suffix* is one of:

-   configs.db
-   properties.pickle
-   threshold-classes.pickle
-   thresholds.pickle

For example:

    [zenoss@zenosst zenpacks]$ ls $ZENHOME/perf/Daemons/localhost/zeneventlog*
    /opt/zenoss/perf/Daemons/localhost/zeneventlog-configs.db
    /opt/zenoss/perf/Daemons/localhost/zeneventlog-properties.pickle
    /opt/zenoss/perf/Daemons/localhost/zeneventlog-threshold-classes.pickle
    /opt/zenoss/perf/Daemons/localhost/zeneventlog-thresholds.pickle

Each time a collector daemon successfully retrieves configuration
information from zenhub, it updates the cached files. This happens at
startup, and then every 20 minutes to 6 hours (depending on the daemon
and its configuration). A collector daemon must successfully connect
once before it can use the cached files if zenhub is not available.

The cached files are considered transient, and can be deleted without
harm.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.5 or higher |
| Required ZenPacks | ZenPacks.zenoss.EnterpriseCollector       |

## Configuration Options

These options apply to all collector daemons and control how those
daemons request configurations from zenhub daemons:

-   **configsipsize** -- If set to a non-zero value, the collector
    daemon requests *n* device configurations from its zenhub daemon
    (where *n* is the value for configsipsize). The default value is 25.
    By requesting device configurations in batches, the option allows
    the collector daemon to start monitoring devices as the device
    configuration is loaded. Also, the smaller batches prevent zenhub
    daemons from locking up a process for long periods of time. If set
    to a value of 0, then all configurations are downloaded at once;
    monitoring does not commence until all configurations have been
    loaded by the collector. On systems with a large number of devices,
    the collector may be waiting a long time to download all the
    configurations.
-   **configsipdelay** -- Controls how many seconds (at most) to wait
    between making device configuration requests. This option is ignored
    if the value of configsipsize is 0. The default value is 1.

<!-- -->

    --configsipsize=CONFIGSIPSIZE
                            Max number of device configurations to load at once,
                            default 25 (0 == all devices)

    --configsipdelay=CONFIGSIPDELAY
                            Delay in seconds between device configurations
                            loading, default 1

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


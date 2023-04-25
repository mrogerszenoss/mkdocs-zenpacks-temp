# EMC Unity Integration ZenPack

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

EMC Unity Integration ZenPack

**Release:**

1.1.0

## EMC Unity Integration ZenPack

## About

This ZenPack provides modeling, monitoring of EMC Unity devices via REST
API Connectivity.

## Prerequisites

| Prerequisite       | Restriction                            |
|--------------------|----------------------------------------|
| Product            | Zenoss 6.4 or higher                   |
| Required ZenPacks  | ZenPacks.zenoss.ZenPackLib &gt;= 2.1.1 |
| Other dependencies | None                                   |

### Usage

Devices should be added to the "**/Storage/EMC/Unity**" Zenoss
DeviceClass. The polling is performed via REST API.

**Datasources**

*EMCUnityHistorical*

A DataSource that polls the EMC Unity REST API according to metricPath
and convert it to base units according to scaling factor.

Possible Scaling factor values:

| Scaling factor | Multiplier |
|----------------|------------|
| "NoScaling"    | 1          |
| "Micro"        | 10 \*\* -6 |
| "Milli"        | 10 \*\* -3 |
| "Kilo"         | 2 \*\* 10  |
| "Mega"         | 2 \*\* 20  |
| "Giga"         | 2 \*\* 30  |
| "Tera"         | 2 \*\* 40  |
| "Peta"         | 2 \*\* 50  |

### Device Classes

A new device class **/Storage/EMC/Unity** will be added

### Configuration properties

REST API Credentials must be provided in:

> -   zEMCUnityUsername
> -   zEMCUnityPassword
> -   zEMCUnityPort
> -   zEMCUnityConcurrency
>     -   The number of concurrent API Requests. (Note: the limit is
>         enforced per-process, so Modeling and Collection may both hit
>         this limit.)
> -   zEMCUnityVerifyCertificate
>     -   This property controls certificate verification. If this
>         property is set to *true* certificate verification takes
>         place, if not - system skips certificate verification.

### Impact diagram

EMC Unity internal impact diagram(EMC Unity device and components)

\[EMCUnityDevice\]-impacts&gt;\[DAE\]

\[EMCUnityDevice\]-impacts&gt;\[FCPort\]

\[EMCUnityDevice\]-impacts&gt;\[DPE\]

\[EMCUnityDevice\]-impacts&gt;\[StoragePool\]

\[EMCUnityDevice\]-impacts&gt;\[IsciInterface\]

\[EMCUnityDevice\]-impacts&gt;\[Disk\]

\[EMCUnityDevice\]-impacts&gt;\[StorageProcessor\]

\[Disk\]-impacts&gt;\[StoragePool\]

\[Disk\]-impacted by&gt;\[EMCUnityDevice\]

\[Disk\]-impacted by&gt;\[DAE\]

\[DAE\]-impacts&gt;\[Disk\]

\[DAE\]-impacted by&gt;\[EMCUnityDevice\]

\[DPE\]-impacts&gt;\[StorageProcessor\]

\[DPE\]-impacted by&gt;\[EMCUnityDevice\]

\[FileSystem\]-impacted by&gt;\[StoragePool\]

\[FileSystem\]-impacted by&gt;\[StorageProcessor\]

\[Lun\]-impacted by&gt;\[StoragePool\]

\[Lun\]-impacted by&gt;\[StorageProcessor\]

\[StoragePool\]-impacts&gt;\[Lun\]

\[StoragePool\]-impacts&gt;\[FileSystem\]

\[StoragePool\]-impacted by&gt;\[EMCUnityDevice\]

\[StoragePool\]-impacted by&gt;\[Disk\]

\[StorageProcessor\]-impacts&gt;\[FileSystem\]

\[StorageProcessor\]-impacts&gt;\[Lun\]

\[StorageProcessor\]-impacted by&gt;\[EMCUnityDevice\]

\[StorageProcessor\]-impacted by&gt;\[DPE\]

\[IsciInterface\]-impacted by&gt;\[EMCUnityDevice\]

\[IsciInterface\]-impacted by&gt;\[EthernetPort\]

\[EthernetPort\]-impacts&gt;\[IsciInterface\]

\[FCPort\]-impacted by&gt;\[EMCUnityDevice\]

### Changelog

1.0.0

Initial zenpack release

-   Storage component modeling & monitoring
-   EMCUnityHistorical datasource

1.1.0

Added Impact adapters, fix certificate validation issue for Zenoss 6.5



# HP 3Par Integration ZenPack

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

HP 3Par Integration ZenPack

**Release:**

1.0.2

## HP 3Par Integration ZenPack

## About

This ZenPack is to provide modeling and monitoring for HP 3PAR/3PAR
StoreServe via SMI-S CIM Application Programming Interface and receive
events as SNMP traps.

## Prerequisites

| Prerequisite      | Restriction                                                            |
|-------------------|------------------------------------------------------------------------|
| Product           | Zenoss 6.0 or higher                                                   |
| Required ZenPacks | ZenPacks.zenoss.WBEM&gt;= 2.1.0 ZenPacks.zenoss.ZenPackLib &gt;= 2.0.0 |

## Configuration

### zProperties

These zProperties are used to configure the connection

-   zWBEMPort
-   zWBEMUsername
-   zWBEMPassword
-   zWBEMUseSSL

## Changes

Release 1.0.2

-   Fixes

    > -   Compatibility with ZenPacks.zenoss.WBEM 3.0

Release 1.0.1

-   Fixes

    > -   Turn off debug during yaml loading. Fix wrong import

Release 1.0.0

-   Features

    > -   Initial release. Modeling and monitoring for HP 3PAR/3PAR
    >     StoreServe via SMI-S CIM



# EMC ECS Integration Service

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

EMC ECS Integration Service

**Release:**

1.0.2

### More Information:

## EMC ECS Integration Service

## About

This ZenPack provides the capability to model and monitor Dell EMC ECS
cluster using ECS Management API and adapt Alerts raised by the ECS
system to Zenoss events.

## Prerequisites

| Prerequisite       | Restriction                                                              |
|--------------------|--------------------------------------------------------------------------|
| Product            | Zenoss 6.0.1 or higher                                                   |
| Required ZenPacks  | ZenPacks.zenoss.PS.Util &gt;= 1.9.6 ZenPacks.zenoss.ZenPackLib &gt;= 2.0 |
| COMPAT_ZENOSS_VERS | &gt;=6.0.1                                                               |
| Other dependencies | None                                                                     |

## Usage

Add EMC ECS VDC Device to the "**/Storage/EMC/ECS**" Zenoss DeviceClass.
The device IP should be IP address of FQDN of an ECS node.

## API Configuration

Configure the following zProperties to enable the API communication and
successfully access the EMC ECS platform:

-   zECSAPIUserUser to access EmcEcs RestAPI. This is the user id of an
    ECS Management.

-   zECSAPIPasswordPassword to access EmcEcs RestAPI. This is the
    password for the ECS Management User.

-   zECSAPIPortThis is usually "4443" which is the ECS Management API
    port user.

-   zECSAPIUseSSLThis is usually true which is "https" Protocol.

-   zECSAPIResponseTimeoutThe number of seconds to wait for a HTTP
    response from the ECS API

## Components Modeled

To add relationship between all Components the EMC ECS VDC should be
modeled twice.

## EMC ECS Monitoring Notes

EMC ECS Management API returns "Transaction Read/Write Bandwidth" and
"Transaction Read/Write Latency" only as historical values with time
delay of 15 minutes. So, these metrics are monitored every 5 minutes(by
default), but displayed on graphs with a delay of 15 minutes.

## Change Log

1.0.2

     SVC-2736 Update to new PS.Util HTTP net_client logging standard

1.0.1

     SVC-2736 HTTP API response timeout configurable

1.0.0

     Initial release. Initial modeling and monitoring EMC ECS storage
infrastructure via REST API

## Attachments:

-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/PS/zenoss-integration-services-ds.pdf){.external-link}


# Amazon Web Services (Commercial)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.AWS

### Applications Monitored:

This ZenPack provides support for monitoring [Amazon Web Services](https://aws.amazon.com/){.external-link}.

## Releases

Version 5.2.0 -
[Download](https://delivery.zenoss.com/){.external-link}
           Released on 2022/12/01
           Requires PythonCollector ZenPack (&gt;=1.11.0), ZenPackLib
ZenPack (&gt;=2.1.0)
           Compatible with Zenoss 6.4 - 6.7 and Zenoss Cloud

Version 5.1.1 - [Download](https://delivery.zenoss.com/){.external-link}

   Release on 2021/03/26

   Requires PythonCollector ZenPack (&gt;=1.11.0), ZenPackLib ZenPack
(&gt;=2.1.0)
   Compatible with Zenoss 6.4 - 6.7 and Zenoss Cloud

## Background

This ZenPack provides support for monitoring Amazon Web Services (AWS).
Monitoring for the following EC2, VPC, RDS, CloudFormation, ECS, ElastiCache
and S3 entities is provided through a combination of the AWS EC2, RDS,
CloudFormation, ECS, ElastiCache
and CloudWatch APIs.

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Discovery of EC2, VPC, RDS, ECS, ElastiCache,
    CloudFormation, Auto Scaling Groups, Application and Network Load
    Balancers, and S3 entities.
-   Monitoring of CloudWatch metrics.
-   Monitoring of Region, S3Bucket and Subnet components.
-   Event management and monitoring.
-   Optional auto-discovery and monitoring of instance guest operating
    systems.
-   Optional service impact with the addition of Zenoss Service Dynamics
    product.
-   Monitoring of estimated charges for Amazon services.
-   Expense Analysis is broken down by tag filters and service.
-   Optional SQS Queues listening and consuming.

### Discovery

The following entities will be automatically discovered through an
account name, access key and secret key you provide. The attributes,
tags and collections will be updated on Zenoss' normal remodeling
interval which defaults to every 12 hours.

Regions:   Attributes: ID:   Collections: VPCs, Subnets, Zones, Instances, Volumes, Images,
    Snapshots, Gateways, Reservations, Elastic IPs, SQS Queues, CF
    Stacks, ECS Clusters, ElastiCache
    clusters

Zones:   Attributes: ID, Region, State:   Collections: Instances, Volumes,
    Subnets, Auto Scaling Groups, RDS Instances,  Reserved Instances, ECS Container
    Instances, Load Balancers, ElastiCache
    Nodes

VPCs:   Attributes: ID, Region, CIDR Block, State:   Tags: Name, CollectorCollections: VPCs,
:   Collections: Subnets, Instances, ElastiCache
    Nodes

Subnets:   Attributes: ID, Region, VPC, Zone, State, CIDR Block, Available IP
    Address Count, Zone Default, Auto-Public IP:   Tags: Name:   Collections: Instances

Instances:   Attributes: ID, Region, VPC, Zone, Image, Subnet, State, Instance
    ID, Tag, Instance Type, Instance Type Details, Platform, Public DNS
    Name, Private IP Address, Public IP, Launch Time, Guest Device:   Tags: Name:   Collections: Volumes:   Other: Guest Device (if monitored by Zenoss)

Volumes:   Attributes: ID, Region, Zone, Instance, Type, Created Time, Size,
    IOPS, Status, Attach Data Status, Attach Data Device:   Tags: Name:   Collections: Snapshots

Elastic IPs:   Attributes: ID, Region, Public IP, Private IP, Instance ID, Domain,
    Network interface ID, Network interface owner ID:   Tags: Name

SQS Queues:   Attributes: ID, Region:   Tags: Name

S3 Buckets:   Attributes: ID, Creation date:   Tags: Name

Snapshots:   Attributes: ID, Region, Volume, Volume size in Bytes, Progress,
    Started, Description:   Tags: Name

VPN Gateways:   Attributes: ID, Region, Gateway type, State:   Tags: Name

Images:   Attributes: ID, Region, Status, Location, Owner ID, Architecture,
    Image type, Kernel ID, Ramdisk ID, Description, Block device
    mapping, Root device type, Root device name, Virtualization type,
    Hypervisor:   Tags: Name

Reserved Instances:   Attributes: ID, Region, Zone, State, Instance Type, Reserved
    Instance ID:   Tags: Name

RDS Instances:   Attributes: ID, Region, Zone, State, Instance ID, Instance Type,
    Parameters Groups, Security Groups, Engine, Engine Version, VPC, VPC
    Subnets:   Tags: Name

RDS Security Group:   Attributes: ID, Region, Owner ID, Description, EC2 Groups, IP Ranges:   Tags: Name

CF Stacks:   Attributes: ID, Description, Creation Time, Disable Rollback,
    Notification ARNs, Capabilities, Tags, Status, Status Reason,
    Timeout, Policy, Template, Parameters, Outputs:   Tags: Name:   Collections: CF Resources

CF Resources:   Attributes: ID, Resource Type, Timestamp, Description, Logical
    Resource ID, Physical Resource ID, Status, Status Reason:
:   Tags: Name

Auto Scaling Groups:   Attributes: ID, Region, Zones, Created Time, Capacity, Default
    Cooldown, Health Check Grace Period, Health Check Type, Launch
    Configuration, Launch Template, Enabled Metrics, Protected From
    Scale In, Placement Group, VPC Zone Identifier:   Tags: Name:   Collections: Instances

Load Balancers (Application and Network):   Attributes: ID, Region, Availability Zones, ARN, Canonical Hosted
    Zone Id, Type, Created Time, DNS Name, Scheme, State, IP Address
    Type, VPC Zone Identifier:   Tags: Name:   *Note*: Classic Load Balancers are not supported

Target Groups:   Attributes: ID, Region, Zones, ARN, Protocol, Port, Target Type,
    Health Check, Unhealthy Threshold Count, Health Check Path, Matcher,
    VPC Zone Identifier:   Tags: Name:   Collections: Instances

Lambda Functions

  Attributes:
FunctionName, Description, FunctionArn, Handler, CodeSize, LastModified,
Role, Alias, Memory, Runtime, Version, Timeout, Security Group

Tags: Name

ECS Clusters

  Attributes: Name, Region, Status,
Active Services, Running Tasks, Pending Tasks, Registered Container
Instances, ECS Container Instances, ECS Schedule Rules

  Tags: Name

  Collections: ECS Container Instances, ECS Services, ECS Schedule
Rules

ECS Container Instances

  Attributes: Name, Region, ECS Cluster, EC2 Instance, Status,
Registered CPU, Remaining CPU, Registered Memory, Remaining Memory,
Running Tasks, Pending Tasks

  Tags: Name

ECS Schedule Rules

  Attributes: Name, Region, ECS Cluster, Schedule Expression, Event Bus
Name, State, ECS Scheduled Tasks

  Collections: ECS Scheduled Tasks

ECS Scheduled Tasks

  Attributes: Name, Region, ECS Cluster, ECS Schedule Rule, Launch Type,
Tasks, Subnets

ECS Services

  Attributes: Name, Region, ECS Cluster, Status, Desired Tasks, Running
Tasks, Pending Tasks, Launch Type

  Tags: Name
  Collections: ECS Tasks

**Note**: For ECS Tasks that are hosted directly on the ECS Cluster
additional 'virtual' ECS Service will be added to contain those tasks

ECS Tasks

  Attributes: Name, Region, ECS Cluster, ECS Service, ECS Container
Instance, Availability Zone, Last Status, Desired Status, ECS Containers

  Tags: Name
  Collections: ECS Containers

ECS Containers

  Attributes: Name, Region, ECS Cluster, ECS Service, ECS Container
Instance, Availability Zone, Last Status, Desired Status

ElastiCache Cluster

  Attributes: Name, Region, Cluster Description, Cache Cluster Status,
Cluster Mode, ElastiCache Nodes, Snapshotting Node Id, Automatic
Failover, Number of Shards, Number of Cache Nodes, Cache Node Type,
Cluster ARN, Snapshot Retention Limit, Snapshot Window, Transit
Encryption Enabled, At Rest Encryption Enabled

  Tags: Name

  Collections: ElastiCache Nodes

ElastiCache Node

  Attributes: Name, Region, Availability Zone, ElastiCache Cluster, VPC,
Subnets, Cache Node Status, Cache Node Type, Engine, Engine Version,
Node Arn, Node Creation Time, Preferred Maintenance Windows, Parameter
Group Name, Cache Subnet Group Name, Replication Group Id, Snapshot
Retention Limit, Snapshot Window, Auto Minor Version Upgrade, Role,
Address, Port, Shard

  Tags: Name

### Modeling

Starting from AWS ZP 5.0, the modeling was changed. The first modeling
starts right after the AWS device has been added. After that, the AWS
device will be modeled every 12 hours by default.

Note: Right now we use only one \`aws.Base\` plugin in 'Modeler Plugins'
and new \`zAWSEnabledPlugins\` property in the Configuration Properties'
was added to control a list of AWS modeler sub-plugins.

If you model the device directly by pressing the 'Model Device' button,
changes will not be applied instantly after modeling is done. It will
take some time to apply all new data to your device.

There are two datsources in the
EstimatedCharges template. AWSModelRunPlugin is responsible for starting
a special server on zenpython's side to listen for requests from
zenmodeler, when modeling is
performed. AWSQueueProcessingPlugin periodically checks the internal
queue on zenpython's side and sends datamaps contained to zenhub.

### Modeling and zAWSEnabledPlugins property

`zAWSEnabledPlugins` controls a list of AWS modeler sub-plugins, such
as:

-   EC2
-   RDS
-   S3Buckets
-   CloudFormation
-   AutoScalingGroups
-   LoadBalancers
-   LambdaFunctions
-   ECS
-   ElastiCache

### Monitoring

The following metrics will be collected every 5 minutes by default. Any
other CloudWatch metrics can also be collected by adding them to the
appropriate monitoring template. The *Average* statistic is collected,
and the graphed value is per second for anything that resembles a rate.

Account:   Metrics: EstimatedCharges, EC2EstimatedCharges, S3EstimatedCharges,
    RDSEstimatedCharges, DynamoDBEstimatedCharges,
    LightsailEstimatedCharges, RedshiftEstimatedCharges,
    SESEstimatedCharges, SNSEstimatedCharges,
    CloudTrailEstimatedCharges, DataTransferEstimatedCharges,
    QueueServiceEstimatedCharges,
    KmsEstimatedCharges, ECSEstimatedCharges, ElastiCacheEstimatedCharges

Regions:   Metrics: CPUUtilization, DiskReadOps, DiskWriteOps, DiskReadBytes,
    DiskWriteBytes, NetworkIn, NetworkOut

**Note**: These metrics aggregated only for EC2 Instances with detailed monitoring enabled

Instances:   Metrics: CPUUtilization, DiskReadOps, DiskWriteOps, DiskReadBytes,
    DiskWriteBytes, NetworkIn, NetworkOut, StatusCheckFailed_Instance,
    StatusCheckFailed_System, CheckReserved

Volumes:   Metrics: VolumeReadBytes, VolumeWriteBytes, VolumeReadOps,
    VolumeWriteOps, VolumeTotalReadTime, VolumeTotalWriteTime,
    VolumeIdleTime, VolumeQueueLength:   Provisioned IOPS Metrics: VolumeThroughputPercentage,
    VolumeReadWriteOps

S3 Buckets:   Metrics: BucketTotalSize, BucketKeysCount

RDS Instances:   Metrics: CPUUtilization, FreeableMemory, FreeStorageSpace,
    SwapUsage, ReadIOPS, WriteIOPS, DatabaseConnections, DiskQueueDepth,
    ReplicaLag

SQSQueue:   Metrics: NumberOfMessagesSent, NumberOfMessagesDeleted,
    ApproximateNumberOfMessagesVisible

Auto Scaling Groups:   Metrics: GroupInServiceInstances, GroupPendingInstances,
    GroupStandbyInstances, GroupTerminatingInstances,
    GroupTotalInstances

Application Load Balancers:

:   Metrics:  ActiveConnectionCount, NewConnectionCount,
    RejectedConnectionCount, TargetConnectionErrorCount, ELBAuthError,
    ELBAuthFailure, TargetResponseTime, TargetTLSNegotiationErrorCount,
    ClientTLSNegotiationErrorCount, HTTPCode_ELB_3XX_Count,
    TPCode_ELB_4XX_Count, HTTPCode_ELB_5XX_Count,
    HTTPCode_ELB_500_Count, HTTPCode_ELB_502_Count,
    HTTPCode_ELB_503_Count, HTTPCode_ELB_504_Count,
    HTTPCode_Target_2XX_Count, HTTPCode_Target_3XX_Count,
    HTTPCode_Target_4XX_Count, HTTPCode_Target_5XX_Count,
    ProcessedBytes, ConsumedLCUs, RequestCount, RuleEvaluations:   **Note**: Depending on the Load Balancer configuration, some metrics
    might be unavailable.

Network Load Balancers:
:   Metrics: ActiveFlowCount, NewFlowCount

Network Target Groups:

  Metrics: HealthyHostCount, UnHealthyHostCountApplication Target
Groups:  Metrics: HealthyHostCount, UnHealthyHostCount

ECS Clusters:

  Metrics: CPUUtilization, MemoryUtilization, CPUReservation,
MemoryReservation, NetworkRxBytes, NetworkTxBytes, StorageWriteBytes,
StorageReadBytes
**Note**: Enable Container Insights to monitor Network and Storage
metrics

ECS Service:

  Metrics: CPUUtilization, MemoryUtilization, NetworkRxBytes,
NetworkTxBytes, StorageWriteBytes, StorageReadBytes

**Note**: Enable Container Insights to monitor Network and Storage
metrics

ElastiCache
Cluster:
          Metrics:
CacheClusterStatus
ElastiCache
Cluster:  *
   *       Metrics: EngineCPUUtilization, CPUUtilization,
DatabaseMemoryUsagePercentage, SwapUsage, MemoryFragmentationRatio,
ReplicationLag, CurrConnections, Evictions, NetworkBytesIn,
NetworkBytesOut, CacheNodeStatus

The *Amazon CloudWatch* datasource type also allows for the collection
of any other CloudWatch metric.

Besides CloudWatch metrics, the following metrics will also be collected
every 5 minutes by default.

Subnets:   Metrics: Available IP Addresses count

Monitoring large cloud may require contacting AWS support with a request
to increase the CloudWatch API requests limit. An appropriate events
will be created in Zenoss in case the limit for CloudWatch requests has
been exceeded.

CloudWatch datasources utilize multithreading for better performance. It
is possible to increase speed by setting `twistedthreadpoolsize` the
value in the configuration of `zenpython` daemon. Please note that
setting a higher value will result also in bigger memory usage.

Collection interval may be changed using the
`zAWSCloudWatchCollectionInterval` property. By default, it is set to
300 seconds. This will affect most Amazon CloudWatch datasources and may
help in reducing monitoring costs. It doesn't change the interval of
datapoints on the graphs, but only changes the frequency Zenoss performs
API calls to CloudWatch.

!!! note
    By default, `CloudFormation`, `ECS` and `ElastiCache`
    modeler sub-plugins are not enabled. Users need to add them manually and
    initiate the modeling for those components to be modeled and
    monitored. For AutoScalingGroup monitoring to become working, the user
    needs to enable the monitoring on the AWS console for the specific
    AutoScalingGroups.

### SQS Queue Messages Monitoring

Users may configure Zenoss to consume specific SQS Queues, parse and
convert messages to Zenoss events.

SQS Events generated might be delayed in their creation due to Amazon's
use of short polling by default.

If configured to not delete messages (listen), events will be sent only
for messages created after the previous monitoring cycle. This prevents
flooding Zenoss Events console with historical SQS messages.

### CloudFormation Events Monitoring

The monitoring plugin collects CloudFormation Events for each CF Stack
and shows them as Zenoss Events at the same time. Also, it updates the
status of the CF Stack or CF Resource component it belongs.

Standard Zenoss Event Fields:

-   device (set to EC2Account)
-   component (CF Stack)
-   summary
-   severity
-   eventClassKey (set to *CFStackEvents*)
-   eventKey (for de-duplication and auto-clear fingerprinting)

Additional Fields:

-   aws.cf.event_id
-   aws.cf.logical_resource_id
-   aws.cf.physical_resource_id
-   aws.cf.resource_properties
-   aws.cf.resource_status
-   aws.cf.resource_status_reason
-   aws.cf.resource_type
-   aws.cf.stack_id
-   aws.cf.stack_name

`CREATE_FAILED` and `DELETE_FAILED` events have *CRITICAL* severity, all
others *INFO* one.

By default, all generated events are mapped to `/AWS/CloudFormation`
event class.

!!! note
    Once the event is sent, it will not be sent again. If the
    user clears the event, it will not reappear again.

In case `zAWSCloudFormationEventsAutoClear` zProperty set to True for
each `CREATE_COMPLETE` and `DELETE_COMPLETE` corresponding auto-clear
event will be generated to clear previous *CRITICAL* ones.

### ElastiCache Events monitoring

The monitoring
plugin collects ElastiCache Events for each ElastiCache Cluster and Node
and shows them as Zenoss Events at the same time.

Standard Zenoss Event Fields:

-   device (set to EC2Account)
-   component (ElastiCache Cluster/ElastiCache Node)
-   summary
-   severity
-   eventClassKey (set to `ElastiCacheEvents`)
-   eventKey (for de-duplication and auto-clear fingerprinting)

Additional Fields:

-   aws.elasticache.sourcetype
    (replication-group/cache-cluster)

`CREATE_FAILED` and `DELETE_FAILED` events have *CRITICAL* severity, all
others *INFO* one.

By default,
all generated events are mapped to \`/AWS/ElastiCache\` event
class.

!!! note
    Once the event is sent, it will not be sent again. If the
    user clears the event, it will not reappear again.

### Zenoss Notifications with SES

Notifications for events now have the option to be sent by email using
Amazon SES.

In addition to the standard email notification fields, you will need to
fill out the following additional fields.

-   AWS Account Name
-   AWS Region
-   AWS Access key
-   AWS Secret key

The senders' email and the email of the subscribers must be verified
within SES for the target region.

### Soft Limits Monitoring

The following resource counts subject to the soft limits will be
collected every 5 minutes and when any of these metrics approaches a
soft limit threshold, a Zenoss event will be triggered.

Regions:   Soft Limit Metrics: Elastic IPs count, Instances count, Subnets
    count, VPC Security Groups count, VPC Security Groups Rules max,
    Volumes count

The thresholds are set to the default limit values. If you changed this
limit for your account, you should manually change the Max threshold
value using the following steps:

1.  Select the AWS device on *Infrastructure* page.
2.  Navigate to *Regions* component and select region.
3.  Click *Display* and select `Templates`.
4.  Press *Create Local Copy* button (The template will be changed for
    the current region only).
5.  On the *Thresholds* panel choose the resource count to be changed.
6.  Double-click on the resources count and change the value in the
    *Maximum Value* field.

### Guest Device Discovery

You can optionally configure each monitored AWS account to attempt to
discover and monitor the guest Linux or Windows operating systems
running within each EC2 instance when specific Tags are present. This
requires that your Zenoss system has the network and server access it
needs to monitor the guest operating system. VPC and non-VPC modes are
supported.

The guest operating system devices' life-cycle is managed along with the
instance. For example, the guest operating system device is set to a
decommissioned production state when the EC2 instance is stopped, and
the guest operating system device is deleted when the EC2 instance is
destroyed.

### Service Impact

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact capability for services running on AWS. The
following service impact relationships are automatically added. These
will be included in any services that contain one or more of the
explicitly mentioned entities.

Service Impact Relationships

-   Account access failure impacts all regions.
-   Region failure affects all
    VPCs, ElastiCache
    Clusters,  ECS Clusters and zones in the affected
    region.
-   VPC failure affects all related subnets.
-   Zone failure affects all related subnets, instances, RDS
    Instances, Auto Scaling Groups,
    Load Balancers,  ECS Container Instances
    and Volumes.
-   Subnet failure affects all instances on the affected subnet.
-   Subnet failure affects all
    functions on the affected subnet.
-   Subnet failure affects ECS
    Container Instances and ECS Scheduled Tasks on the affected
    subnet.
-   Volume failure affects any attached instance.
-   Instance failure affects the guest operating system device and
    Target Groups instance belongs to.
-   SQSQueue, VPNGateway, or EC2ElasticIP failure affects any related
    region.
-   S3Bucket failure affects related account.
-   Each component affects the corresponding CF Resource if it has
    any related
    region.
-   CF Resource failure affects CF Stack.
-   Auto Scaling Group affects related EC2 Instances.
-   Target Group affects related Load Balancers.
-   ECS Cluster affects ECS
    Services, ECS Container Instances and ECS Schedule Rules.
-   ECS Container Instance affects
    ECS Tasks.
-   ECS Schedule Rule affects ECS
    Scheduled Tasks.
-   ECS Service affects ECS
    Tasks.
-   ECS Tasks affect ECS
    Containers.
-   ElastiCache
    Cluster affects ElastiCache Nodes.

### Tag Filters

The ZenPack now provides a way to group and collect AWS components on an
account based on AWS Tags. You can define a tag filter by navigating to
your AWS account device and selecting "Add AWS Tag Filter" from the "+"
menu in the lower left corner of the screen. On the dialog that pops up,
give your Tag Filter a name, and select the tag you want to track. You
can combine multiple tags with the AND and OR operators. You can also
generate a Component Group based on the Tag Filter. Click Submit when
finished.

The Tag Filter will be visible in the the navigation bar area, and the
"AWS Tag Filters" section. This will allow you to view all components of
any type matched by the filter, along with their graphs.

In addition, you can use this Tag Filter to view billing information for
the group of components in the Expenses Analysis section (see [Expense Analysis](#expense-analysis)).

The AWS Tag Filters use a special monitoring template, TagFilter, which
is not visible in the device-level monitoring template section, but is
visible if you go to Advanced > Monitoring Templates. From here, you
can add modify the template, should you need to do so.

### Estimated charges monitoring

To turn on monitoring of charges for Amazon services one should enable
*EstimatedCharges* monitoring template for AWS device. This will add
graphs with billing information to the device overview page and on
the *Expenses Analysis* page.

@lb[](img/zenpack-aws_account_billing.png)

Account Billing Overview

To control spendings limit `zAWSBillingCostThreshold` zProperty should
be used. It is set to 1000 by default. This property sets threshold for
bullet-like billing graph to turn red and used in "Billing Cost"
threshold as well. Event is generated if spending goes over its value.

Billing graphs shows estimated charges for whole account and detailed
charges per service. Top 10 services displayed on pie chart.

This ZenPack uses linear interpolation to predict total per month
charges and this information is displayed on the device overview page
and on the `Total Estimated Charge` graph as new a datapoint in
`Expense Analysis`.

### Expense Analysis

You can track AWS usage charges for a given tag or tag group, and group
by specific services. In order to set this up, you must create a Tag
Filter to match the tag or tags in which you are interested. And then
you must configure detailed billing reports in your AWS account. See
[Configuring Charges Per Tags Monitoring](#configuring-cha-rgesperta-gsmonitoring)
for details.

@lb[](img/zenpack-aws_expenses_analysis.png)

Expenses Analysis

### Cloudwatch API Cost

This ZenPack uses the Amazon Cloudwatch API to collect metric data. The
first 1,000,000 calls to this API each month are free, and then
additional calls are charged at a rate of $0.01 per 1,000 calls. For
specific pricing questions, see [AWS Cloudwatch Pricing](https://aws.amazon.com/cloudwatch/pricing/){.external-link}.

A report is provided (Reports > AWS Reports > Monitoring Costs)
to provide a detailed breakdown of API calls and estimated cost per
monitoring template on each monitored EC2 Account.

### CloudFormation Stacks Blueprints

CloudFormation Stacks Blueprints provides a graphical representation of
all Stacks templates. The same way as it's done in AWS Console.

@lb[](img/zenpack-aws_blueprint.png)

Stacks Blueprints

At start, only stacks are shown. Double click on the node expands stacks
and shows its resources. Also, buttons for quick expanding and
collapsing all visible stacks are available.

The set of visible stacks can be narrowed down by regions and stack name
filters. The stack name filter sets the fragment that needs to be
present in the stack's name. After setting filters *Refresh* button
should be pressed to apply changes.

Each node in the stack is a resource defined in the template. The first
row of text specifies the name of the resource defined in the template,
the second one is a type of resource and the last is the id of deployed
AWS entity.

By default diagram only shows resources that were deployed, to show all
resources *Show Undeployed Resources* checkbox can be used.

Links represent dependencies between resources (e.g. EC2 Instances refer
to Security Groups).

There also are separate blueprints for each CF Stack component.

### Configuring ECS Schedule Rules discovery

`zAWSECSEventBuses` contains names of AWS Event Bridge Event Buses which
are used for ECS Schedule Rules discovery.
By default Event Bus with the name `default` is used. If you use a
custom Event Bus for ECS Schedule Rules, you will need to add its name
to `zAWSECSEventBuses` manually.

## Usage

### Adding AWS Accounts

Use the following steps to start monitoring EC2 using the Zenoss web
interface.

1.  Navigate to the Infrastructure page.
2.  Choose *Add EC2 Account* from the add device button.
3.  Enter your AWS account id, account name, access key and secret key.
4.  Optionally choose a collector other than the default *localhost*.
5.  Click *Add*.

Alternatively, you can use `zenbatchload` to add accounts from the command
line. To do this, you must create a file with contents similar to the
following. Replace all values in angle brackets with your values minus
the brackets. Multiple accounts can be added under the same
`/Device/AWS/EC2` section.

```
/Devices/AWS/EC2 loader='ec2account', loader_arg_keys=['accountid', 'devicename', 'accesskey', 'secretkey', 'devicePath', 'collector'] <devicename> accountid='accountid', devicename='devicename', accesskey='accesskey', secretkey='secretkey', devicePath='/Devices/AWS/EC2', collector='localhost'
```

You can then load the account(s) with the following command:

    $ zenbatchload <filename>

### Configuring filter for modeler plugin

Use `zAWSRegionToModel` property to narrow components modeled. By
default it has an empty value, so all EC2 regions and its child
components will be discovered. Specify the EC2 region name, or multiple
names separated by a comma in it. This will be used as a filter and may
help with large AWS accounts.

Some regions (such as 'ap-east-1'
(Hong Kong)) may be disabled by default, on the AWS console. In this
case, a message about skipping it will be shown while modeling.

### Configuring Guest Device Discovery

Use the following steps to configure instance guest device discovery.
Guest device discovery must be configured individually for each EC2
account.

1.  Navigate to one of the EC2 accounts.
2.  Click the edit link beside *Device Class for Discovered Linux
    Instances*
3.  Choose the device class for Linux and/or Windows instances.
4.  Navigate to the *Configuration Properties* panel and in the
    `zAWSDiscover` property specify the instances' tags and values (e.g.
    `<tag:value>;`).
5.  Verify that appropriate SSH, SNMP or Windows credentials are
    configured for the chosen device class(es).
6.  To choose private or public IP address will be used for creating
    guest devices, and change the `zAWSGuestUsePublicIPs` property.
7.  To specify device classes for guest devices based on AWS tags from the
    instance, set the tag `key=value` in the `zAWSGuestDeviceClassTags`.
    For example: in EC2 Console it is a tag `app=1`, then use `app=1`
    and `/Server/Linux` in `zAWSGuestDeviceClassTags` property edit
    window.
8.  Like specifying guest device classes from AWS tags, Zenoss Group &
    System membership can be configured via
    `zAWSGuestDeviceGroupingTags`. The tag definition works exactly as
    it does in `zAWSGuestDeviceClassTags`.
    **Note:** you will need to restart zproxy service in Control Center, to
    have a proper UI window for this zProperty after installation.
9.  Remodel the EC2 account by choosing *Model Device* from its menu.

@lb[](img/zenpack-zawsguestdeviceclasstags.png)
zAWSGuestDeviceClassTags Property

Please note: `zAWSDiscover` defines a filter for guest devices discovery
and used before `zAWSGuestDeviceClassTags`. A list of tags in
`zAWSGuestDeviceClassTags` used from top to bottom, so first matching
key=value will apply. Also, property `zAWSGuestDeviceClassTags` takes
precedence over Device Overview configured classes.

`zAWSDiscover` also supports complex tags in the format
`<some:long:key:value>;` Multiply colons are allowed in the
`key` name only (`key:key:value`).

If your instances are VPC instances and are in a different VPC than the
Zenoss server that's monitoring the EC2 account, you must add a
*Collector* tag containing VPC with the value set to the name of the
Zenoss collector to which discovered guest devices should be assigned.

Example:

1.  If `zAWSDiscover` was filled with the value `Test:test;` after
    modeling all the devices with the tag `Test:test` will be discovered
2.  If `zAWSDiscover` was filled with the value
    `Test1:test1;Test2:test2` after modeling all the devices with either
    of the tag will be discovered

### Configuring Remote Collector for Guest Devices

You can optionally configure an alternate remote collector for the
devices created from AWS Instances with the following configuration
properties:

`zAWSGuestCollector` This property allows you to specify the name of the collector all
    discovered devices for this AWS device will use.

`zAWSResetGuestCollector` Setting this property to *false* on a guest device (not an EC2
    Account) will tell AWS not to change the collector if you have set
    it manually.

### Configuring closing events on guest device deletion.

New `zAWSCloseGuestEvents` property added. If set to true, all open events
for guest device will be closed when the guest device is deleted.

### Find Missing Guest Devices

Guest devices should be discovered automatically during modeling.
However, if an error occurs during modeling or some other unexpected
event, it is possible for guest devices to be skipped. If some guest
devices appear to be missing, you can force the discovery process to be
repeated.

In the Zenoss UI, navigate to your AWS EC2 Account device, and find the
gear icon menu in the bottom left corner of the window. Under this menu,
click the option labeled "Find Missing Guest Devices." This will
schedule a job for immediate execution, which will clear the guest ID
cache and run the discovery process for each instance. Existing guest
devices will remain, but any devices previously missed will be detected.
You can monitor the progress of this job in the Jobs section of the UI,
under the Advanced Tab.

### Reasons a Guest Device Fails to be Discovered

Several criteria must be met in order for a guest device to be
discovered by the AWS ZenPack. Those requirements are as follows:

-   The instance must contain a tag listed in the `zAWSDiscover`
    configuration property.
-   Guest device classes must be defined. See the "Device Class for
    Discovered Linux Instances" and "Device Class for Discovered Windows
    Instances" fields on the Device Overview page.
-   The guest must have a valid collector, either from the EC2
    Instance's VPC, from the `zAWSGuestCollector`, or the default
    collector for the AWS account device.
-   The guest must have a valid `manageIP`, either the EC2 Instance's
    private IP, public IP, or its DNS name.
-   The EC2 Instance `guest` property must be set. This should be set
    automatically. If you believe it is set improperly, use the Find
    Missing Guest Devices feature described above.
-   The EC2 Instance `_has_guest` must be false. This should be set
    automatically. If you believe it is set improperly, use the Find
    Missing Guest Devices feature described above.
-   The guest device ID must not be previously cached in the AWS
    account's guest device ID cache. This should be handled
    automatically. If you believe it is set improperly, use the Find
    Missing Guest Devices feature described above.

If all the criteria above are met by the EC2 Instance, and an existing
device with an ID or title matching the EC2 Instance's ID exists, or an
existing device has a matching IP address, the EC2 Instance will be
linked to that existing device.

If no existing device matches the EC2 Instance, but the criteria above
are met, a new device will be created in the Linux or Windows device
class configured for the account.

Note that guest device creation is triggered during modeling, but is
queued as a job to be run later. Thus a guest device will not show up
until after modeling has been completed, and the corresponding scheduled
job has been completed.

If a device link appears to be missing, double-check the criteria above,
and run the Find Missing Guest Devices task described in the preceding
section.

When creating guest devices a job should be scheduled for each guest
device to be created. If a job was created for the guest device, but the
guest device was not created, you can check the job output in the Jobs
section of Zenoss.

If a job was not created, you can try running the modeler in debug mode
to see why guest device creation was skipped.

### Configuring Instances Remodeling

You can optionally configure your monitored AWS account, so that the
newly added or recently dropped instances are automatically reflected on
Zenoss UI during monitoring:

1.  Navigate to the *Configuration Properties* panel.
2.  Enable the `zAWSRemodelEnabled` property.

If `zAWSRemodelEnabled` is false, only the instance state will be
updated on existing instances. If set to true, then all instance
properties will be updated on existing instances, and new instances will
be added to the model.

### Configuring Auto Change of the Production State for EC2 Instances

You can disable auto change of the production state for EC2 Instances,
for this purpose you have to:

1.  Click on the *Infrastructure* tab.
2.  Select discovered EC2 Instances or the appropriate device classes,
    in case you want to change the behavior for a group of underlying
    EC2 instances.
3.  Navigate to the *Configuration Properties* panel.
4.  Change the `zAWSAutoChangeProdState` property (default is *true*).

By default, the production state is changed to 'Production' (1000) for
running EC2 instances, and to 'Decommissioned' (-1) for stopped ones.
These states may be customized by specifying the desired production
state IDs (numbers) in `zAWSAutoChangeProdStateRunning` and
`zAWSAutoChangeProdStateStopped`.

If the user changes the production state for some guest device manually,
this state will be used for this guest device when the EC2 instance
switches to a running state.

### PEM file

Use the following steps to specify the PEM file to the region for use in
auto-discovering instance guest operating systems:

1.  Navigate to the *Configuration Properties* panel.
2.  Set region name and path to PEM file in the appropriate fields of
    `zAWSRegionPEM` property (see image below).

@lb[](img/zenpack-zawsregionpem_property.png)

zAWSRegionPEM Property

### Disable AWS Snapshot Monitoring

In some cases, you may have a large quantity of AWS Snapshots in your
environment, which can slow down the performance of the modeler. If you
do not need to model them, you can disable the collection of snapshots
by setting the `zAWSEnableSnapshotCollection` property to *false*. This
will prevent the modeler from collecting and modeling snapshots in the
future. It will also cause current snapshot components to be removed
from Zenoss the next time the model is updated.

If you have already modeled your AWS snapshots, and the count is high,
removing them can cause the modeler to timeout. If this occurs, you can
remove them manually by running the included dmd script
`delete_all_snapshot_components` from the zope container.

*Note*: The `delete_all_snapshot_component` script will delete **all**
AWS snapshot components from **all** AWS devices without prompting for
confirmation. If you have multiple AWS devices and only want to delete
snapshots from some devices, use `zendmd`.

### Configuring Charges Per Tags Monitoring

If you use tag filters to organize your modeled AWS components, you may
also want to enable monitoring charges per tag filter added to Zenoss.
This will require configuration on both AWS and Zenoss sides.

To process Cost and Usage reports AWS Athena service is used, so please
expect some extra costs for the service usage.

Configuration on the AWS side (you may use a different account to
collect billing data from the account being used for monitoring, by
using `zAWSBillingAccessKey` and `zAWSBillingSecretKey` zProperties):

1.  Activate User-Defined Cost Allocation Tags according to [AWS documentation](http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/activating-tags.html){.external-link}.
    Choose tags you use to filter components.
2.  Turn on the AWS Cost and Usage report according to [AWS documentation](http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-reports-gettingstarted-turnonreports.html){.external-link}.
    There is no need to enable Redshift or QuickSight manifests.
3.  Grant read permissions for S3 bucket reports to be delivered to the
    AWS account configured in Zenoss.
4.  Grant AWS user used in Zenoss access to use AWS Athena service.
    Please see the details in the
    [documentation](http://docs.aws.amazon.com/athena/latest/ug/access.html#managed-policies){.external-link}.

*Note*: It can take up to 24 hours for AWS to start delivering reports
to your S3 bucket.

For configuration on Zenoss side set the following zProperties:

-   `zAWSBillingReportS3Bucket`: S3 Bucket name of Cost and Usage
    reports being delivered (e.g. `aws-billing-master`).
-   `zAWSBillingReportPrefix`: Report path prefix prepended to reports.
    Can be empty.
-   `zAWSBillingReportName`: Report name
-   `zAWSBillingAthenaResultsS3Bucket`: S3 Bucket AWS Athena will use to
    store query results. For details please check [AWS documentation](http://docs.aws.amazon.com/athena/latest/ug/querying.html){.external-link}.
-   `zAWSBillingAthenaRegion`: Region which will be used to run AWS
    Athena. To avoid extra charges for cross-region data transfer, it's
    recommended to use the same region as S3 Bucket with Cost and Usage
    reports.

If Cost and Usage reports are stored on a separate account,
`zAWSBillingAccessKey` and `zAWSBillingSecretKey` zProperties should be
set to access and secret keys of this account. If these properties are
empty, access and a secret key from the device will be used.

If a tag is used for Tag Filter but is missing in Cost and Usage
reports, billing data will not be collected for such Tag Filter and a
corresponding *Info* event with a list of missing tags will be
generated.

### Configuring HTTP Proxies

If necessary, this zenpack can query AWS through an HTTP proxy. This is
configured in the usual way, by setting the `*_proxy` environment
variables. Because of this, the setting is global for a particular
Zenoss process. It is therefore important to be aware that, for
instance, enabling proxying for zenpython may cause it to be used for
other service monitoring beyond just AWS.

To configure these environment variables, edit the service definitions
(via `serviced service edit` or the Control Center UI) for the
zenpython, zenmodeler, and zenjobs containers as follows:

Change

```
"Environment": null,
```

to:

```
"Environment": [ "http_proxy=http://[proxy host]:[proxy port]", "https_proxy=http://[proxy host]:[proxy port]", "no_proxy=localhost" ],
```

Note that both `http_proxy` and `https_proxy` values must begin with
`http://`. The `no_proxy` variable is required so that communication
with other zenoss services is not impacted.

**Note:** Do not add this to the zope container.

### Configuring SQS Queue Messages Monitoring

To control SQS Queue Messages Monitoring `zAWSSQSQueues` zProperty
should be used. It defines a list of queue name RegEx patterns and
Zenoss event generation configuration.

@lb[](img/zenpack-zawssqsqueues_property.png)

zAWSSQSQueues Property

-   *Queue Name RegEx*: RegEx to look for any match in the SQS queue
    name. (*Note*: empty expression matches all queue names.)
-   *Parser*: Parser name to process messages
-   *Event Class Key*: Optional field with Event Class Key for generated
    events
-   *Delete*: Defines whether to delete the processed message from the
    queue

For each SQS queue, the list of patterns is checked from top to bottom,
and the first queue name match will define a configuration. In case of
no match, the queue will be not listened to.

Messages from the queue will be consumed, and parsed with one of the
following message types:

**simple**

Uses message body as subject/message for Zenoss events. The severity
will be *Info*.

**sns_topic**

There is a possibility to attach SQS Queues to SNS Topics. The parser
Zenoss will decode the message and use the "Subject" and "Message"
fields to set corresponding Zenoss event fields. Event severity will be
*Info*.

**zenoss_json**

Zenoss will expect the message body to be in JSON format, decode and
treat it as an already formed Zenoss event. The next fields will be
extracted:

-   message (at least one of summary or message should be present)
-   summary
-   eventKey (optional)
-   severity (optional, will be *Info* as default)
-   rcvtime (optional, if omitted current timestamp will be used)
-   eventClassKey (optional, if omitted configured will be used)
-   eventClass (optional)

For all parsers the generated events will have the next fields:

-   device (set to EC2Account)
-   component (SQS Queue)

If the event class or event class key is not defined in the event,
`AWSSQSMessages` event class key (mapped to `/AWS/SQSMessage`) will be
used.

### Configuring and Testing CloudWatch Datasources

You can get namespaces and metrics available on the selected device, for
this purpose you have to: 1. In the CloudWatch datasource edit window
click on the dropdown button in `Namespace` or `Metric Name` input
fields. 2. In the new window select `Device`, then `Region` and a list
of available Namespaces and Metrics for that region will appear.

@lb[](img/zenpack-aws_cloudwatch_datasource_helper.png)

CloudWatch Datasource Helper

Before testing datasource (using the button `Test` in datasource edit
window) you may set a valid device name in `Device Name` input field.

### Adding Custom AWS CloudWatch Datasources

Sometimes you may need to monitor some AWS CloudWatch metrics which are
not defined in AWS ZP. In case AWS ZP already models components you need
to add metric you may just update provided template (create a new one
with`-addition`suffix to avoid template overriding during the AWS ZP
upgrade) and add a new datasource with corresponding graphs. You will
need an Amazon CloudWatch datasource with `Namespace and`
 `Metric Name`fields populated.

If there is no component you want to monitor you may create a graph on
the device level. But you will need a separate datasource for each
component instance.

Here is an example of how to add monitoring of AWS ECS:

1.  Create a separate monitoring template in Advanced > Monitoring
    Templates tab under`/AWS/EC2`device class.
2.  Create a new data source for the template created above using the
    Amazon CloudWatch type. Add a datapoint with the same name as
    datasource.
3.  Edit datasource created above and
    populate `Namespace` and `Metric Name` fields. Change the `Region` field
    and set the actual region where your ECS cluster is located.
    In `Dimension` put the string in format
    `ServiceName=<service_name>;ClusterName=<cluster_name>`
    (e.g.`ServiceName=web;ClusterName=test-ec2-cluster`).
4.  You can add the datapoints you created to a graph for visualization.
5.  Open your AWS device bind template you just created.
6.  You may see your graphs on the Graphs page.

### Enabling incremental modeling for ECS Components

To enable incremental modeling for ECS Components you will need to
select any Region component, switch to the Templates in the drop-down
menu and enable the ECSWatch datasource.
This datasource is disabled by default. The collection interval can be
changed by using the Cycletime property of the ECSWatch datasource.

### @lb[](img/zenpack-aws_ecs_components.png){.confluence-embedded-image width="700"}

ECS incremental modeling

### Changing maximum retries while making API call to AWS

`zAWSMaxCallRetries` with a default value of 4 is responsible for the
number of maximum retries per call to AWS API. You can increase it if
you have throttling issues with AWS API. Setting this property to high
values may cause too long calls and delays.

### Using `zAWSUseNewIds` property

This property is applied for AutoScalingGroups, LambdaFunctions,
LoadBalancers, and TargetGroups. After changing this property and
remodeling - device historical data for that components will be lost. By
default, this property is enabled for a fresh install for AWS ZP 5.1.0
and disabled for an upgrade to AWS ZP 5.1.0.

This property uses AWS ARN as `id ` for AutoScalingGroups,
LambdaFunctions, LoadBalancers and TargetGroups to handle a case, when
some component was created on the AWS, deleted and recreated with the
same name. On the AWS side - these are two different components. On
Zenoss's side, this was the same component for AutoScalingGroups,
LambdaFunctions, LoadBalancers and TargetGroups. Setting
`zAWSUseNewIds` to *true* and remodeling will fix this issue.

### Configuring retries delay for Lambda Functions, ECS Services and Load Balancers

Sometimes throttling error `Rate exceeded` may happen during
modeling Lambda Functions, ECS Services and Load Balancers while getting
tags info and ECS List of Services. Properties `zAWSLambdaFunctionsRetriesDelay`,
`zAWSECSRetriesDelay` and `zAWSLoadBalancersRetriesDelay`
set base delay in seconds for retries.

Also, `zAWSLoadBalancersMaxARNsCount`
and
`zAWSECSListServicesMaxResults`
were added for
API calls count configuring. These zProperties should be used to reduce
or increase API call count to prevent throttling and timeout
exceptions.

### Configuring exponential backoff and retries delay for SQS Queues

Sometimes
connecting cancelled error `ConnectingCancelledError` may happen during
collection of SQS Queues messages. zProperty `zAWSConnectingCancelledRetriesDelay`
set base delay in seconds for retries. These zProperty should be used to
prevent connecting cancelled errors and timeout exceptions for SQS
Queues.

### Additional SQS Queues discovery

If you have more than 1000 SQS Queues in one region, only 1000 will be
discovered. To handle this case you may use the `zAWSSQSQueuesPrefix`
property. Add prefixes to specify
SQS Queues you want to model additionally. Only strings should be used,
regexes are not supported. SQS Queues that are collected using
`zAWSSQSQueuesPrefix` are also limited
to 1000 Queues per prefix.

### Filter EC2 Instances by name

You may filter
EC2 instances by name with `zAWSEC2Allowed` and `zAWSEC2Denied`
properties.
They contain a list of regexes to allow/deny EC2 instances modeling. At
first we apply `zAWSEC2Allowed` propery, if it
is empty - we modell all EC2 instances. Then we skip instances which
match `zAWSEC2Denied` regexes.

### Overwrite default AWS events transformation

Default event
mapping is the following:

`if getattr(evt, 'eventKey', None) in ('|StatusCheckFailed_Instance_StatusCheckFailed_Instance|StatusCheckFailed_Instance', '|StatusCheckFailed_System_StatusCheckFailed_System|StatusCheckFailed_System'):`
`evt.eventClass = '/Status'`
`if evt.severity == 0:`
`evt.summary = evt.message = 'Status Check is ok'`
`else:`
`evt.summary = evt.message = 'Status Check has failed'`

If you want to
overwrite the default event transformation you should do the
following:

1.  Go to the \`Events Console\` tab;
2.  Then go to the \`Events Classes\` tab;
3.  Select the \`AWS\` events tab;
4.  Chose \`Mapping Instances\` from the drop-down if not already
    chosen;
5.  Double-click on \`AWS Default Mapping\`;
6.  Select \`Transforms\` tab.

After that,
you can write and apply your own AWS event transformation for specific
events.

**Note:** Do
not forget to click the *Save Transform*
button.

@lb[](img/zenpack-aws_default_events_transformation.png){.confluence-embedded-image width="700"}

AWS default
events transformation

### CloudFormation Stacks and Resources discovery and monitoring on highly scalable environment

If you have a large amount of CloudFormation Stacks and Resources on
your EC2 Account you may face "timeout" events for
data sources responsible for data collection for these components. This
cause no status and events collection for CloudFormation components.
In order to avoid "timeout" events and collect all data correctly, you
should increase the "cycletime" property for events,
the data source for CF Stacks, and "CFResourceState" for CF Resources
on appropriate monitoring templates.

**Note:** In case when you have around 2000 CloudFormation Stacks the
appropriate cycletime for events and CFResourceState data
sources is 1200 seconds.

Sometimes throttling error "Rate exceeded" may happen during modeling
and monitoring CloudFormation Stacks and
Resources. zProperty `zAWSCloudFormationRetriesDelay` set base delay
in seconds for retries.
This zProperty should be used to prevent throttling errors and timeout
exceptions for CloudFormation Stacks and Resources.

**Note:** Starting from the 5.2.0 version the attributes `Stack
Template`and `Stack Policy` are no longer discovered during
device modeling. These components were moved to a separate
`CFStackDetails` data source under CF Stack components and will be
discovered after 12 hours from the initial device modeling. The
CloudFormation components are collecting with a Zenoss' normal
remodeling interval which defaults to every 12 hours.

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

Device Classes

-   /AWS
-   /AWS/EC2

Configuration Properties

-   zAWSDiscover
-   zAWSRegionPEM
-   zAWSRemodelEnabled
-   zAWSAutoChangeProdState
-   zAWSAutoChangeProdStateRunning
-   zAWSAutoChangeProdStateStopped
-   zAWSGuestCollectorTroubleshooting
-   zAWSResetGuestCollector
-   zAWSGuestUsePublicIPs
-   zAWSRegionToModel
-   zAWSCloudWatchSSL
-   zAWSCloudWatchMaxParallel
-   zAWSCloudWatchMaxRetries
-   zAWSBillingCostThreshold
-   zAWSCloudFormationEventsAutoClear
-   zAWSCloudFormationRetriesDelay
-   zAWSEnableSnapshotCollection
-   zAWSEnabledPlugins
-   zAWSGuestDeviceTitleTag
-   zAWSGuestDeviceClassTags
-   zAWSBillingAccessKey
-   zAWSBillingSecretKey
-   zAWSBillingReportS3Bucket
-   zAWSBillingReportPrefix
-   zAWSBillingReportName
-   zAWSBillingAthenaResultsS3Bucket
-   zAWSBillingAthenaRegion
-   zAWSCloudWatchCollectionInterval
-   zAWSSQSQueues
-   zAWSCloseGuestEvents
-   zAWSLambdaFunctionsRetriesDelay
-   zAWSMaxCallRetries
-   zAWSECSEventBuses
-   zAWSUseNewIds
-   zAWSSQSQueuesPrefix
-   zAWSGuestDeviceGroupingTags
-   zAWSEC2Allowed
-   zAWSEC2Denied
-   zAWSLoadBalancersRetriesDelay
-   zAWSECSRetriesDelay
-   zAWSECSListServicesMaxResults
-   zAWSLoadBalancersMaxARNsCount
-   zAWSConnectingCancelledRetriesDelay

Modeler Plugins

-   aws.Base

Datasource Types

-   Amazon CloudWatch
-   AWSDataSource
-   Tag Filter Billing Report
-   ECSWatchDataSource

Monitoring Templates

-   EstimatedCharges (in /AWS/EC2)
-   EC2Region (in /AWS/EC2)
-   EC2Instance (in /AWS/EC2)
-   EC2Instance-Detailed (in /AWS/EC2)
-   EC2Volume (in /AWS/EC2)
-   EC2Volume-IOPS (in /AWS/EC2)
-   EC2Image (in /AWS/EC2)
-   EC2VPC (in /AWS/EC2)
-   EC2VPCSubnet (in /AWS/EC2)
-   EC2Snapshot (in /AWS/EC2)
-   EC2Zone (in /AWS/EC2)
-   S3Bucket (in /AWS/EC2)
-   SQSQueue (in /AWS/EC2)
-   EC2ReservedInstance (in /AWS/EC2)
-   VPNGateway (in /AWS/EC2)
-   RDSInstance (in /AWS/EC2)
-   CFStack (in /AWS/EC2)
-   TagFilter (in /AWS/EC2)
-   AutoScalingGroup (in /AWS/EC2)
-   ApplicationLoadBalancer (in /AWS/EC2)
-   NetworkLoadBalancer (in /AWS/EC2)
-   LambdaFunction (in
    /AWS/EC2)
-   ApplicationTargetGroup (in /AWS/EC2)
-   NetworkTargetGroup (in /AWS/EC2)
-   TargetGroup (in /AWS/EC2)
-   ECSCluster (in /AWS/EC2)
-   ECSContainerInstance (in
    /AWS/EC2)
-   ECSService (in /AWS/EC2)
-   ECSTask (in /AWS/EC2)
-   ECSContainer (in
    /AWS/EC2)
-   ElastiCacheCluster
    (in /AWS/EC2)
-   ElastiCacheNode
    (in /AWS/EC2)

Device Types

-   EC2Account (in /AWS/EC2)

Component Types

-   EC2Region (on EC2Account)
-   EC2VPC (on EC2Region)
-   EC2VPCSubnet (on EC2Region)
-   EC2Zone (on EC2Region)
-   EC2Instance (on EC2Region)
-   EC2Volume (on EC2Region)
-   EC2Image (on EC2Region)
-   EC2Snapshot (on EC2Region)
-   SQSQueue (on EC2Region)
-   VPNGateway (on EC2Region)
-   EC2ReservedInstance (on EC2Region)
-   S3Bucket (on EC2Account)
-   Elastic IP (on EC2Region)
-   RDSInstance (on EC2Region)
-   RDSSecurityGroup (on EC2Region)
-   CFStack (on EC2Region)
-   CFResource (on CFStack)
-   AutoScalingGroup (on EC2Region)
-   LoadBalancer (on EC2Region)
-   TargetGroup (on EC2Region)
-   LambdaFunction (on
    EC2Region)
-   ECSCluster (on EC2Region)
-   ECSContainerInstance (on
    ECSCluster)
-   ECSService (on
    ECSCluster)
-   ECSTask (on ECSService)
-   ECSContainer (on ECSTask)
-   ECSScheduleRule (on
    ECSCluster)
-   ECSScheduledTask (on
    ECSScheduleRule)
-   ElastiCacheCluster
    (on EC2Region)
-   ElastiCacheNode
    (on ElastiCacheCluster)

Event Classes

-   /AWS/SQSMessage
-   /AWS/Suggestion
-   /AWS/CloudFormation
-   /AWS/ElastiCache

Event Class Mapping

-   AWS Default Mapping (on /AWS)

Reports

-   /AWS Reports/Monitoring Costs

## Required Daemons

Modeler:

-   zenmodeler
-   zenpython

Performance Collector:

-   zenpython

## IAM Permissions

    { "Version": "2012-10-17", "Statement": [ { "Effect": "Allow", "Action": [ "autoscaling:DescribeAutoScalingGroups", "cloudformation:Describe*", "cloudformation:GetStackPolicy", "cloudformation:GetTemplate", "cloudformation:ListStackResources", "cloudwatch:GetMetricStatistics", "cloudwatch:ListMetrics", "ec2:Describe*",      "ecs:Describe*",      "ecs:List*",      "events:ListRules",      "events:ListTargetsByRule",      "elasticloadbalancing:Describe*", "lambda:ListAliases", "lambda:ListFunctions", "lambda:ListTags", "rds:DescribeDBInstances", "rds:DescribeDBSecurityGroups", "rds:ListTagsForResource", "s3:GetBucketLocation", "s3:ListAllMyBuckets", "ses:SendEmail", "sqs:DeleteMessageBatch", "sqs:GetQueueAttributes", "sqs:GetQueueUrl", "sqs:ListQueues", "sqs:ReceiveMessage", "sts:GetCallerIdentity",                    "elasticache:DescribeReplicationGroups",                     "elasticache:DescribeCacheClusters",                     "elasticache:DescribeEvents" ], "Resource": "*" } ] }

## Troubleshooting

If modeling is not working and the following message is present in the
modeling log:

    No suitable AWS Modeler Server instance found. Please check in zenpython log if it's running.

Check if monitoring template`EstimatedCharges` is available on device
level with `AWSModelRunPlugin` and `AWSQueueProcessingPlugin`
datasources inside it. If not, add them from Advanced - Monitoring
Templates - EstimatedCharges. Then restart zenpython and look into
zenpython.log for the message - `AWS Modeler Server is up.` It should
appear before regular collecting process starts.

During monitoring AWS Account such error events might be created:

```
During processing ... datapoints in ... an error occured: SignatureDoesNotMatch: The request signature we calculated does not match the signature you provided. Check your AWS Secret Access Key and signing method. An error occurred (SignatureDoesNotMatch) when calling the GetQueueUrl operation: The request signature we calculated does not match the signature you provided. Check your AWS Secret Access Key and signing method. Consult the service documentation for details. An error occurred (AuthFailure) when calling the DescribeReservedInstances operation: AWS was not able to validate the provided access credentials.
```

These errors mean that Zenoss could not connect to AWS API due to the
wrong access token. It might be caused by:

1. Wrong AWS credentials. Please check EC2 Access and Secret Keys.

2. Wrong time on collector host. Please adjust the system clock on
collector hosts. Consider using NTP daemon to automatically adjust the
host's clock.

The next error occurs during gathering billing data for tags and means
that `zAWSBillingAccessKey` and `zAWSBillingSecretKey` need to be
checked:

```
Could not fetch billing data. Check your zAWSBilling* properties: An error occurred (SignatureDoesNotMatch) when calling the GetObject operation: The request signature we calculated does not match the signature you provided. Check your key and signing method.
```

## Upgrade

The AWS Zenpack of versions 2.0.0 / 2.1.0 can be upgraded. To upgrade
the ZenPack, install the latest version over the existing one. There is
no action for the user to migrate the data. The performance data and
events of the old ZenPack are retained as per the retention policy
settings.

During the upgrade from version 2.x to 3.0.0 and above all performance
data for S3 Buckets will be lost.

When upgrading from 3.x to 4.x, tags are structured differently. Devices
must be remodeled to handle tags properly.

In the case of using a local copy of `EstimatedCharges` template on the
AWS device, after upgrading to 5.x and above, the bound local template
needs to be synced with ZenPack's one manually. There are new
datasources `AWSModelRunPlugin` and `AWSQueueProcessingPlugin` need to
be copied to the local template.

In the 5.0.0 version modeling CloudFormation components was enabled by
default. This was fixed in version 5.0.1. If the new device was added in
version 5.0.0, recheck *`zAWSEnabledPlugins`* for enabling/disabling
CloudFormation modeling.

## Limitations

After upgrading to 4.1.1 performance data for LoadBalancers and Target
Groups components, (which were introduced in 4.1.0) will be lost.

Starting from version 4.1.0 AWS ZenPack is no longer supported on Zenoss
4.x.

When upgrading from versions 4.0.2, you may see errors regarding
`default_value`. Those errors will be cleared automatically within the
next monitoring cycles. If those events are not cleared, close them
manually.

In the current version of Zenpack monitoring of large AWS accounts
(e.g. >1000 EC2 instances and volumes) may cause performance issues:

-   The limit for datapoints processed by `zenpython` daemon may be
    exceeded. This will result in gaps in graphs.
-   The monitoring cycle may not fit into default value of 5 minutes.
    This will result in some points on graphs to be not aligned by 5
    minutes interval.
-   Having more than one AWS account added to Zenoss may lead to the
    issues described above.
-   `zenpython` may consume more memory than allocated in Control Center
    for its service. That will require increasing
    RAM Requested parameter on Control Center UI.

It is possible to reduce the number of datapoints collected by disabling
monitoring templates you don't need.

## Known Issues

ZPS-1533

-   "TypeError" flare may be shown when attempting to add a device after
    upgrading from an older version of the ZenPack on Zenoss 5.x
-   If this error is encountered, restarting the zproxy service (by
    restarting) top-level "Zenoss.resmgr" application in Control Center.
    It is not necessary to restart the child services.

ZPS-7015

-   if incremental modeling for ECS
    is turn on, there may be warning in `zenpython` log that
    ECSWatchDataSourcePlugin is blocked for some amount of time in
    collect. This doesn't affect incremental modelling, unless the blocking
    time is longer than 30 seconds.
-   if the ECSWatch datasource is
    blocked, it will remain permanently blocked until its name is
    removed from `/var/zenoss/zenpython.blocked` on Zenoss Cloud and
    Zenoss 6. The zenpython service must be restarted after manual
    modifications to this file.

ZPS-7541

-   Spaces are not trimmed in
    `zAWSGuestDeviceClassTags` and `zAWSGuestDeviceGroupingTags`
    properties.

## Changes

**5.2.0**

-   Add support for Amazon ElastiCache Clusters and Nodes (ZPS-8295)
-   Add the possibility to control which EC2 Instances to model based on
    naming rule/filter (ZPS-7487)
-   Made ECS Service discovering scalable for large EC2 Accounts
    (ZPS-7852)
-   Made SQS Queues events collection scalable for large EC2 Accounts
    (ZPS-8357)
-   Made CloudWatch Namespace collection on UI scalable for large EC2
    Account (ZPS-8055)
-   Made CloudFormation Stacks and Resources discovering scalable for
    large EC2 Accounts (ZPS-8440)
-   Fixed selected region modeling for Lambda Functions (ZPS-8170)
-   Tested with Zenoss Resource Manager 6.7.0, Zenoss Cloud, and Service
    Impact 5.5.5

**5.1.1**

-   Define Group & System membership by Tag in Guest Device Discovery
    (ZPS-7228)
-   Tested with Zenoss Resource Manager 6.5.0, Zenoss Cloud and Service
    Impact 5.5.3

**5.1.0**

-   Add support (with optional incremental modeling) for AWS ECS
-   Make possible modeling more than 1000 of SQS Queues per one region
    (ZPS-7094)
-   Support complex AWS tags in zAWSDiscover (ZPS-7033)
-   Add new datapoints to AWS ApplicationLoadBalancer Monitoring
    Template (ZPS-6964)
-   Add zAWSUseNewIds property to switch to new IDs for some components
    (ZPS-6911)
-   Fix AWS Zenpack Lambda Rate Exceeded Error (ZPS-6856)
-   Add new AWS Target Group
    Monitoring Templates (ZPS-7219)
-   Add new datapoint for billing predicted charges (ZPS-7002)
-   Tested with Zenoss Resource
    Manager 6.4.1, Zenoss Resource Manager 6.5.0, Zenoss Cloud and
    Service Impact 5.5.2

**5.0.1**

-   Fix Lambda functions modeling, add retries to handle Rate Exceeded
    Error (ZPS-6639)
-   Fix Load Balancers discovery (ZPS-6641)
-   Add possibility to close guest device events while deleting guest
    device (ZPS-6643)
-   Tested with Zenoss Resource Manager 6.4.1, Zenoss Cloud and Service
    Impact 5.5.1

**5.0.0**

-   Move modeling from zenmodeler to zenpython (ZPS-6117)
-   Support AWS Serverless technologies (ZPS-5717)
-   Fix endpoints generating heavy invalidations load (ZPS-5880)
-   Fix cloudwatch CreateDatasource "NameSpaces" field doesn't load
    (ZPS-5914)
-   Add eu-north-1 region modeling (ZPS-5818)
-   Fix tagsCatalog indexing (ZPS-5998)
-   Tested with Zenoss Resource Manager 6.4.1, Zenoss Cloud and Service
    Impact 5.5.1

**4.1.1**

-   Added aws.AutoScalingGroup, aws.LoadBalancers modeler plugins
    (ZPS-5088)
-   Fix conflict in Dynamic View groups (ZPS-5187)
-   Fix linking of ELBs and target Groups and case when these entities
    have same names on Amazon side (ZPS-5251)
-   Make CloudWatch datasource helper to be created on-demand (ZPS-5562)
-   Remove a restriction of 20 ELBs modeled in one account (ZPS-5117)
-   Added links to Azure and Kubernetes instances (ZPS-5080)
-   Tested with Zenoss Resource Manager 6.3.2, Zenoss Cloud and Service
    Impact 5.3.4

**4.1.0**

-   Add possibility to use Amazon CloudWatch datasource on SQS Queues
    (ZPS-3955)
-   Update zAWSAutoChangeProdState to not change the production state of
    a guest device during a maintenance window (ZPS-3489)
-   Fix guest device productionState is not always updated with
    zAWSAutoChangeProdState enabled (ZPS-3477)
-   Upgrade to botocore 1.7.84 / boto3 1.10.84
-   Update component group when linked tag filter is changed (ZPS-4309)
-   Re-design SQS-based event monitoring (ZPS-3061)
-   Added zAWSGuestDeviceClassTags property to specify guest device
    classes mapped from EC2 instance tags (ZPS-5005)
-   Auto Scaling Groups modeling and monitoring (ZPS-4474)
-   Added "Treat missing data as" field to Amazon CloudWatch datasource
    to set the default value for metric when no data returned from AWS
-   Application and Network Load Balancers modeling and monitoring
    (ZPS-38)
-   Add link from EC2 Instance if it is part of Kubernetes cluster to
    Kubernetes node. Requires Kubernetes ZP version greater then 1.0.1
    (ZPS-4777)
-   Tested with Zenoss Resource Manager 5.3.3, Zenoss Resource Manager
    6.3.1, Zenoss Cloud and Service Impact 5.3.4

**4.0.2**

-   Handle CloudFormation templates where a stack output has no
    description (ZPS-3181)
-   Upgrade to botocore 1.8.41 / boto3 1.5.27
-   Fix type of the ec2secretkey property (ZEN-29852)
-   AWS Prediction charges time is 'undefined' on overview page
    (ZEN-30367)
-   Styling updates and fixes for Zenoss Cloud
-   Change event class for Billing Cost threshold (ZPS-3838)
-   Handle Cloud Formation Stack Outputs witout a 'Description' field
    (ZPS-3181)
-   Updated documentation with IAM permissions required to model SQS
    successfully (ZPS-3268)
-   Tested with Zenoss Cloud, Zenoss Resource Manager 6.2.0, 5.3.3 and
    Service Impact 5.3.1

**4.0.1**

-   Avoid duplicate events created from SQS messages by querying based
    on timestamp. (ZPS-2364)
-   Update botocore endpoint list to reflect new regions and AWS
    services (ZPS-3037)
-   Tested with Zenoss Resource Manager 4.2.5 RPS 743, Zenoss Resource
    Manager 5.3.3, Zenoss Resource Manager 6.1.0 and Service Impact
    5.2.3.

**4.0.0**

-   Allow filtering of components by AWS tags.
-   Optionally populate Component Groups based on tag filters
-   Monitoring billing information aggregated by tags
-   Added zAWSCloudWatchCollectionInterval (default to 300) to simplify
    configuration of default collection interval for all Amazon
    CloudWatch datasources
-   Fixed incorrectly scaled percentage values in the Volume 'Time'
    graph. (ZPS-2247)
-   Improve the managing of guest device production states when
    zAWSAutoChangeProdState is enabled. When an instance is restarted,
    restore its previous production state. (ZPS-1865)
-   Add support for CloudFormation YAML templates (ZPS-2201)
-   Converted to use ZPL and updated to Boto v3
-   SSL error fixed (ZPS-1739)
-   Added report "Monitoring Costs" to check estimated charges for AWS
    devices monitoring
-   Tested with Zenoss Resource Manager 5.3.2, Zenoss Resource Manager
    4.2.5 RPS 743 and Service Impact 5.1.7

**3.0.3**

-   Specify dmd to use for device facade in unit test (ZEN-28777)
-   Internal-only release. No changes to production code, only unit
    tests

**3.0.2**

-   Fixed crochet requirement for unit tests, to allow platform build
    tests to run (ZEN-28777)
-   Internal-only release. No changes to production code, only unit
    tests

**3.0.1**

-   Fixed SSL error in S3 modeling when using proxy
-   Added zAWSEnableSnapshotCollection (default to false) to allow
    disabling collection of Snapshots, in order to improve modeling
    performance
-   Added gear menu option and job to find missing guest devices
-   Added zAWSGuestDeviceTitleTag (default to empty) to allow guest
    device titles to be populated based on AWS tag from instance
-   Moved guest device deletion to scheduled job to improve modeling
    performance and reduce database conflicts due to long transactions

**3.0.0**

-   CloudFormation and RDS support
-   Estimated charges monitoring
-   Add support for GovCloud (us-gov-west-1) region
-   Migrate S3 Bucket monitoring to use AWS CloudWatch

**2.4.6**

-   Fix broken AWS monitoring when a proxy is being used (ZPS-1260)

**2.4.5**

-   Update boto version shipped with the ZenPack to support new
    "eu-west-2" region.
-   Updated AmazonCloudWatchDataSource to use txboto.
-   Usage of AmazonCloudWatchDataSource on device level is now allowed.

**2.4.4**

-   Update boto version shipped with the ZenPack to support new
    "us-east-2" region.

**2.4.3**

-   Fix Region and S3 Buckets graphs inconsistencies (ZEN-17242)
-   Fix ZenPack failing on model [New Region in Mumbai] (ZEN-23892)
-   AWS ZenPack is able to collect and consume data from demo
    environment (ZEN-24089)
-   Proper handling for ConnectionLost, TimeoutError and other
    exceptions (ZEN-23901)
-   Fix EC2RegionPlugin's traceback events (ZEN-23174)
-   Fix S3 bucket lookup / get_bucket broken for eu-central-1
    (ZEN-23044)
-   Fix S3BucketPlugin's traceback events when S3 bucket's region is EU
    (ZEN-23236)
-   Account ID field is added to 'Add EC2 Account' dialog (ZEN-21880)
-   Add `zAWSAutoChangeProdState` property to have more control over EC2
    Instance's production state (ZEN-23427)

**2.4.2**

-   Fix intermittent graph gaps (ZEN-22337)

  **2.4.1**

-   Fix errors encountered during monitoring of Reserved Instances
    (ZEN-22379)

**2.4.0**

-   Update boto version shipped with the ZenPack to support new
    "ap-northeast-2" region.
-   Improve HTTP errors and warnings.
-   Added `zAWSCloudWatchMaxParallel` property to configure number of
    concurrent cloudwatch calls.
-   Make the number of retries for cloudwatch calls configurable
    (`zAWSCloudWatchMaxRetries` property).
-   Allow modeler to set it Region explicitlty, and ignore unmodeled
    buckets.
-   Added path reporter for EC2Snapshots

**2.3.1**

-   Ignore reserved instances with a null id. (ZEN-17556).
-   Added `zAWSRegionToModel` property to tell RM what to model
    (ZEN-17374)
-   Improved `zAWSRemodelEnabled` and `zAWSResetGuestCollector`
    properties

**2.3.0**

-   Add ability for instances into VPC to use public IP address for
    guest device
-   Add parallel processing for CloudWatch datasources using
    multithreading. For large AWS installation it can be boosted by
    setting bigger value for "twistedthreadpoolsize" setting of
    PythonCollector.

**2.2.2**

-   Add support for Zenoss 5x.
-   Add ability for user to specify an alternate remote collector for
    discovered devices.
-   Update boto version shipped with the ZenPack to support signature
    v4.

**2.2.1**

-   Add support for SQS Messages, S3 Buckets, Reserved Instances,
    Elastic IPs, Images, VPN Gateways, Snapshots.
-   Discover instances via Layer 3 when specific Tags are present on the
    instance.
-   Add ability for user to upload PEM file to region for use in
    auto-discovering instance guest operating systems.
-   Add ability for user to enable reflecting new instances on Zenoss UI
    during monitoring.
-   Support multiple IP addresses per instance and add instance type
    details.
-   Monitor AWS Soft Limits and VPC Subnet available IP address count.
-   Update component statuses during monitoring.

**2.1.0**

-   Support CloudWatch metrics with multiple indexes.
-   Add "Amazon Email Host" notification type for SES notifications.

**2.0.0**

-   Add support for regions, zones, VPCs, subnets and volumes.
-   Add support for custom CloudWatch metrics.
-   Complete rewrite.

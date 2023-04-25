# Amazon Web Services (Open Source)

@lb[](img/zenpack-aws-logo-partner_2_2.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.zenoss.AWS

### Devices Monitored:

[Amazon Web Services](https://aws.amazon.com/){.external-link}

## Amazon Web Services ZenPack (Open Source)

The Amazon Web Services™ ZenPack allows you to monitor AWS
infrastructure.

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

This ZenPack provides support for monitoring [Amazon Web Services™](https://aws.amazon.com/){.external-link}.

*\*[AWS 3.X](https://help.zenoss.com/display/in/Amazon+Web+Services+-+Commercial){.external-link}
release and future AWS ZenPack releases are Commercial ZenPacks
(ZenPacks developed by Zenoss Inc. which are closed source, and require
a license to access).*

*The AWS 2.X release is still available as an Open Source ZenPacks
(ZenPacks developed by Zenoss, Inc. which are open source and freely
available).\**

## Releases

Version 2.4.6 - [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.AWS/2.4.6/ZenPacks.zenoss.AWS-2.4.6.egg){.external-link}:   Release on 2017/04/03:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss Core
    5.1.x, Zenoss Resource Manager 4.2.x, Zenoss Resource Manager 5.0.x,
    Zenoss Resource Manager 5.1.x, Zenoss Resource Manager 5.x.x

Version 2.4.5 - [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.AWS/2.4.5/ZenPacks.zenoss.AWS-2.4.5.egg){.external-link}:   Release on 2017/02/14:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss Core
    5.1.x, Zenoss Resource Manager 4.2.x, Zenoss Resource Manager 5.0.x,
    Zenoss Resource Manager 5.1.x

Version 2.4.4 - [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.AWS/2.4.4/ZenPacks.zenoss.AWS-2.4.4.egg){.external-link}:   Release on 2016/12/12:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss Core
    5.1.x, Zenoss Resource Manager 4.2.x, Zenoss Resource Manager 5.0.x,
    Zenoss Resource Manager 5.1.x

Version 2.4.3 - [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.AWS/2.4.3/ZenPacks.zenoss.AWS-2.4.3.egg){.external-link}:   Release on 2016/08/01:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss Core
    5.1.x, Zenoss Resource Manager 4.2.x, Zenoss Resource Manager 5.0.x,
    Zenoss Resource Manager 5.1.x

Version 2.4.2 - [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.AWS/2.4.2/ZenPacks.zenoss.AWS-2.4.2.egg){.external-link}:   Release on 2016/03/25:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss
    Resource Manager 4.2.x, Zenoss Resource Manager 5.0.x, Zenoss
    Resource Manager 5.1.x

Version 2.4.1 - [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.AWS/2.4.1/ZenPacks.zenoss.AWS-2.4.1.egg){.external-link}:   Release on 2016/03/09:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss
    Resource Manager 4.2.x, Zenoss Resource Manager 5.0.x

Version 2.4.0 - [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.AWS/2.4.0/ZenPacks.zenoss.AWS-2.4.0.egg){.external-link}:   Release on 2016/03/04:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector){.external-link}:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x, Zenoss
    Resource Manager 4.2.x, Zenoss Resource Manager 5.0.x

## Background

This ZenPack provides support for monitoring Amazon Web Services (AWS).
Monitoring for the following EC2, VPC, and S3 entities is provided
through a combination of the AWS EC2,  and CloudWatch APIs.

This ZenPack supersedes the older ZenAWS (ZenPacks.zenoss.ZenAWS)
ZenPack that was installed by default on versions of Zenoss prior to
4.2.4. Please remove ZenAWS before installing this ZenPack. This will
remove the `/EC2` device class and the EC2Manager device within. After
installing this ZenPack, you will be able to add a new EC2 Account with
much greater functionality.

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Discovery of EC2, VPC, and S3 entities.
-   Monitoring of CloudWatch metrics.
-   Monitoring of Region, S3Bucket and Subnet components.
-   Event management and monitoring.
-   Optional auto-discovery and monitoring of instance guest operating
    systems.
-   Optional service impact with addition of Zenoss Service Dynamics
    product.
-   Monitoring of estimated charges for Amazon services

### Discovery

The following entities will be automatically discovered through an
account name, access key and secret key you provide. The attributes,
tags and collections will be updated on Zenoss' normal remodeling
interval which defaults to every 12 hours.

Regions:   Attributes: ID:   Collections: VPCs, Subnets, Zones, Instances, Volumes, Images,
    Snapshots, Gateways, Reservations, Elastic IPs, SQS Queues, CF
    Stacks

Zones:   Attributes: ID, Region, State:   Collections: Instances, Volumes, Subnets

VPCs:   Attributes: ID, Region, CIDR Block, State:   Tags: Name, Collector:   Collections: Subnets, Instances

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

### Monitoring

The following metrics will be collected every 5 minutes by default. Any
other CloudWatch metrics can also be collected by adding them to the
appropriate monitoring template. The *Average* statistic is collected,
and the graphed value is per second for anything that resembles a rate.

Regions:   Metrics: CPUUtilization, DiskReadOps, DiskWriteOps, DiskReadBytes,
    DiskWriteBytes, NetworkIn, NetworkOut:   *Note*: These metrics aggregated only for EC2 Instances with
    detailed monitoring enabled

Instances:   Metrics: CPUUtilization, DiskReadOps, DiskWriteOps, DiskReadBytes,
    DiskWriteBytes, NetworkIn, NetworkOut, StatusCheckFailed_Instance,
    StatusCheckFailed_System, CheckReserved

Volumes:   Metrics: VolumeReadBytes, VolumeWriteBytes, VolumeReadOps,
    VolumeWriteOps, VolumeTotalReadTime, VolumeTotalWriteTime,
    VolumeIdleTime, VolumeQueueLength:   Provisioned IOPS Metrics: VolumeThroughputPercentage,
    VolumeReadWriteOps

S3 Buckets:   Metrics: BucketTotalSize, BucketKeysCount

The *Amazon CloudWatch* datasource type also allows for the collection
of any other CloudWatch metric.

Besides CloudWatch metrics, the following metrics will also be collected
every 5 minutes by default.

Subnets:   Metrics: Available IP Adresses count

Monitoring large cloud may require to contact AWS support with request
to increase CloudWatch API requests limit. Appropriate event will be
created in Zenoss in case limit for CloudWatch requests has been
exceeded.

CloudWatch datasources utilize multithreading for better performance. It
is possible to increase speed by setting `twistedthreadpoolsize` value
in configuration of `zenpython` daemon. Please note that setting higher
value will result also in bigger memory usage.

### Soft Limits Monitoring

The following resource counts subject to the soft-limits will be
collected every 5 minutes and when any of these metrics approaches a
soft limit threshold, a Zenoss event will be triggered.

Regions:   Soft Limit Metrics: Elastic IPs count, Instances count, Subnets
    count, VPC Security Groups count, VPC Security Groups Rules max,
    Volumes count

The thresholds are set to the default limit values. If you changed this
limit for your account, you should manually change the Max threshold
value using the following steps:

1.  Navigate to *Monitoring Templates* (*Advanced* panel).
2.  Click *EC2Region* and find *RegionsSoftLimits* among Data Sources.
3.  On the *Thresholds* panel choose the resources count to be changed.
4.  Double click on the resources count and change the value in the
    *Maximum Value* field.

### Guest Device Discovery

You can optionally configure each monitored AWS account to attempt to
discover and monitor the guest Linux or Windows operating systems
running within each EC2 instance, when specific Tags are present. This
requires that your Zenoss system has the network and server access it
needs to monitor the guest operating system. VPC and non-VPC modes are
supported.

The guest operating system devices' life-cycle are managed along with
the instance. For example, the guest operating system device is set to a
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
-   Region failure affects all VPCs and zones in affected region.
-   VPC failure affects all related subnets.
-   Zone failure affects all related subnets, instances, and volumes.
-   Subnet failure affects all instances on affected subnet.
-   Volume failure affects any attached instance.
-   Instance failure affects the guest operating system device.
-   SQSQueue, VPNGateway, or EC2ElasticIP failure affects any related
    region.
-   S3Bucket failure affects related account.

## Usage

### Adding AWS Accounts

Use the following steps to start monitoring EC2 using the Zenoss web
interface.

1.  Navigate to the Infrastructure page.
2.  Choose *Add EC2 Account* from the add device button.
3.  Enter your AWS account id, account name, access key and secret key.
4.  Optionally choose a collector other than the default *localhost*.
5.  Click *Add*.

Alternatively you can use zenbatchload to add accounts from the command
line. To do this, you must create a file with contents similar to the
following. Replace all values in angle brackets with your values minus
the brackets. Multiple accounts can be added under the same
`/Devices/AWS/EC2` section.

    /Devices/AWS/EC2 loader='ec2account', loader_arg_keys=['accountid', 'devicename', 'accesskey', 'secretkey', 'collector'] <devicename> accountid='accountid', devicename='devicename', accesskey='accesskey', secretkey='secretkey', collector='localhost'

You can then load the account(s) with the following command:

    $ zenbatchload <filename>

### Configuring filter for modeler plugin

Use `zAWSRegionToModel` property to narrow components modeled. By
default it has empty value, so all EC2 regions and it's child components
will be discovered. Specify EC2 region name, or multiple names separated
by comma in it. This will be used as a filter and may help with large
AWS accounts.

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
    guest device, change the `zAWSGuestUsePublicIPs` property.
7.  Remodel the EC2 account by choosing *Model Device* from its menu.

If your instances are VPC instances, and are in a different VPC than the
Zenoss server that's monitoring the EC2 account, you must add a
*Collector* tag to containing VPC with the value set to the name of the
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

zAWSGuestCollector:   This property allows you to specify the name of the collector all
    discovered devices for this AWS device will use.

zAWSResetGuestCollector:   Setting this property to *false* on guest device (not EC2 Account)
    will tell AWS not to change the collector if you have set it
    manually.

### Configuring Instances Remodeling

You can optionally configure your monitored AWS account, so that the
newly added or recently dropped instances are automatically reflected on
Zenoss UI during monitoring:

1.  Navigate to the *Configuration Properties* panel.
2.  Enable the `zAWSRemodelEnabled` property (set it to *true*, this
    field is not case sensitive).

### Configuring Auto Change of the Production State for EC2 Instances

You can disable auto change of the production state for EC2 Instances,
for this purpose you have to:

1.  Click on the *Infrastructure* tab.
2.  Select discovered EC2 Instances or the appropriate device classes,
    in case you want to change the behaviour for a group of underlying
    EC2 instances.
3.  Navigate to the *Configuration Properties* panel.
4.  Change the `zAWSAutoChangeProdState` property (default is *true*).

By default, the production state is changed to 'Production' (1000) for
running EC2 instances, and to 'Decommissioned' (-1) for stopped ones.
These states may be customized by specifying the desired production
state IDs (numbers) in zAWSAutoChangeProdStateRunning and
zAWSAutoChangeProdStateStopped.

### PEM file

Use the following steps to specify the PEM file to region for use in
auto-discovering instance guest operating systems:

1.  Navigate to the *Configuration Properties* panel.
2.  Set region name and path to PEM file in the appropriate fields of
    `zAWSRegionPEM` property (see zAWSRegionPEM Propery).

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
-   zAWSGuestCollector
-   zAWSResetGuestCollector
-   zAWSGuestUsePublicIPs
-   zAWSRegionToModel
-   zAWSCloudWatchSSL
-   zAWSCloudWatchMaxParallel
-   zAWSCloudWatchMaxRetries

Modeler Plugins

-   aws.EC2
-   aws.S3Buckets

Datasource Types

-   Amazon CloudWatch
-   AWSDataSource

Monitoring Templates

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

Event Classes

-   /AWS/SQSMessage
-   /AWS/Suggestion

## Required Daemons

| Type                  | Name        |
|-----------------------|-------------|
| Modeler               | zenmodeler  |
| Performance Collector | zenpython   |

## IAM Permissions

    {   "Statement": [     {       "Action": [         "autoscaling:Describe*",         "cloudformation:DescribeStacks",         "cloudformation:DescribeStackEvents",         "cloudformation:DescribeStackResources",         "cloudformation:GetTemplate",         "cloudformation:GetStackPolicy",         "cloudfront:Get*",         "cloudfront:List*",         "cloudwatch:Describe*",         "cloudwatch:Get*",         "cloudwatch:List*",         "directconnect:Describe*",         "dynamodb:GetItem",         "dynamodb:BatchGetItem",         "dynamodb:Query",         "dynamodb:Scan",         "dynamodb:DescribeTable",         "dynamodb:ListTables",         "ec2:Describe*",         "elasticache:Describe*",         "elasticbeanstalk:Check*",         "elasticbeanstalk:Describe*",         "elasticbeanstalk:List*",         "elasticbeanstalk:RequestEnvironmentInfo",         "elasticbeanstalk:RetrieveEnvironmentInfo",         "elasticloadbalancing:Describe*",         "iam:List*",         "iam:Get*",         "route53:Get*",         "route53:List*",         "rds:Describe*",         "s3:Get*",         "s3:List*",         "sdb:GetAttributes",         "sdb:List*",         "sdb:Select*",         "ses:Get*",         "ses:List*",         "sns:Get*",         "sns:List*",         "sqs:GetQueueAttributes",         "sqs:ListQueues",         "sqs:ReceiveMessage",         "storagegateway:List*",         "storagegateway:Describe*"       ],       "Effect": "Allow",       "Resource": "*"     }   ] }

## Upgrade

The AWS Zenpack of versions 2.0.0 / 2.1.0 can be upgraded. To upgrade
the ZenPack, install the latest version over the existing one. There is
no action for the user to migrate the data. The performance data and
events of old ZenPack are retained as per the retain policy settings.

## Limitations

In the current version of Zenpack monitoring of large AWS account (e.g.
&gt;1000 EC2 instances and volumes) may cause performance issues:

-   Limit for datapoints processed by `zenpython` daemon may be
    exceeded. This will result in gaps in graphs.
-   Monitoring cycle may not fit into default value of 5 minutes. This
    will result for some points on graphs to be not aligned by 5 minutes
    interval.
-   Having more than one AWS account added into Zenoss may lead to
    issues described above.
-   `zenpython` may consume more memory than allocated in Control Center
    for its service. What will require to increase RAM Requested
    parameter on Control Center UI.

It is possible to reduce number of datapoints collected by disabling
monitoring templates you don't need.

## Known Issues

ZPS-1533

-   "TypeError" flare may be shown when attempting to add a device after
    upgrading from an older version of the zenpack on Zenoss 5.x
-   If this error is encountered, restarting the zproxy service (by
    restarting) top-level "Zenoss.resmgr" application in Control Center.
    It is not necessary to restart the child services.

ZPS-1510

-   "No such file or directory" error event may appear in Events console
    after upgrading from an older version of the zenpack on Zenoss 4.2.x
    / 5.x.
-   If this event is present, close it manually.

## Changes

2.4.6

-   Fix broken AWS monitoring when a proxy is being used (ZPS-1260)

2.4.5

-   Update boto version shipped with the ZenPack to support new
    "eu-west-2" region.
-   Updated AmazonCloudWatchDataSource to use txboto.
-   Usage of AmazonCloudWatchDataSource on device level is now allowed.

2.4.4

-   Update boto version shipped with the ZenPack to support new
    "us-east-2" region.

2.4.3

-   Fix Region and S3 Buckets graphs inconsistencies (ZEN-17242)
-   Fix ZenPack failing on model \[New Region in Mumbai\] (ZEN-23892)
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

2.4.2

-   Fix intermittent graph gaps (ZEN-22337)

2.4.1

-   Fix errors encountered during monitoring of Reserved Instances
    (ZEN-22379)

2.4.0

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

2.3.1

-   Ignore reserved instances with a null id. (ZEN-17556).
-   Added `zAWSRegionToModel` property to tell RM what to model
    (ZEN-17374)
-   Improved `zAWSRemodelEnabled` and `zAWSResetGuestCollector`
    properties

2.3.0

-   Add ability for instances into VPC to use public IP address for
    guest device
-   Add parallel processing for CloudWatch datasources using
    multithreading. For large AWS installation it can be boosted by
    setting bigger value for "twistedthreadpoolsize" setting of
    PythonCollector.

2.2.2

-   Add support for Zenoss 5x.
-   Add ability for user to specify an alternate remote collector for
    discovered devices.
-   Update boto version shipped with the ZenPack to support signature
    v4.

2.2.1

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

2.1.0

-   Support CloudWatch metrics with multiple indexes.
-   Add "Amazon Email Host" notification type for SES notifications.

2.0.0

-   Add support for regions, zones, VPCs, subnets and volumes.
-   Add support for custom CloudWatch metrics.
-   Complete rewrite.

## Attachments:

-   [AWS_Account_Overview.png](img/zenpack-aws_account_overview+A.png)
-   [AWS_Add_EC2_Account_Dialog.png](img/zenpack-aws_add_ec2_account_dialog.png)
-   [AWS_Add_EC2_Account_Menu_Item.png](img/zenpack-aws_add_ec2_account_menu_item.png)
-   [AWS_Impact.png](img/zenpack-aws_impact.png)
-   [AWS_Instance_Graphs.png](img/zenpack-aws_instance_graphs.png)
-   [AWS_Region_Graphs.png](img/zenpack-aws_region_graphs+A.png)
-   [AWS_Region_Instances.png](img/zenpack-aws_region_instances+A.png)
-   [AWS_S3Bucket_Graphs.png](img/zenpack-aws_s3bucket_graphs.png)
-   [AWS_Subnet_Graphs.png](img/zenpack-aws_subnet_graphs+A.png)
-   [AWS_Volume_Graphs.png](img/zenpack-aws_volume_graphs.png)
-   [AWS_VPC_Subnets.png](img/zenpack-aws_vpc_subnets+A.png)
-   [AWS_Zone_Volumes.png](img/zenpack-aws_zone_volumes+A.png)
-   [aws-logo-partner_2\_2.png](img/zenpack-aws-logo-partner_2_2.png)
-   [ZAWSRegionPEM_Property.png](img/zenpack-zawsregionpem_property.png)
-   [AWS_Account_Overview.png](img/zenpack-aws_account_overview.png)
-   [AWS_Add_EC2_Account_Dialog.png](img/zenpack-aws_add_ec2_account_dialog.png)
-   [AWS_Add_EC2_Account_Menu_Item.png](img/zenpack-aws_add_ec2_account_menu_item.png)
-   [AWS_Impact.png](img/zenpack-aws_impact.png)
-   [AWS_Instance_Graphs.png](img/zenpack-aws_instance_graphs.png)
-   [AWS_Region_Graphs.png](img/zenpack-aws_region_graphs.png)
-   [AWS_Region_Instances.png](img/zenpack-aws_region_instances.png)
-   [AWS_S3Bucket_Graphs.png](img/zenpack-aws_s3bucket_graphs.png)
-   [AWS_Subnet_Graphs.png](img/zenpack-aws_subnet_graphs.png)
-   [AWS_Volume_Graphs.png](img/zenpack-aws_volume_graphs.png)
-   [AWS_VPC_Subnets.png](img/zenpack-aws_vpc_subnets.png)
-   [AWS_Zone_Volumes.png](img/zenpack-aws_zone_volumes.png)
-   [aws-logo-partner_2\_2.png](img/zenpack-aws-logo-partner_2_2.png)
-   [ZAWSRegionPEM_Property.png](img/zenpack-zawsregionpem_property.png)
-   [AWS_Account_Overview.png](img/zenpack-aws_account_overview.png)
-   [AWS_Add_EC2_Account_Dialog.png](img/zenpack-aws_add_ec2_account_dialog.png)
-   [AWS_Add_EC2_Account_Menu_Item.png](img/zenpack-aws_add_ec2_account_menu_item.png)
-   [AWS_Impact.png](img/zenpack-aws_impact.png)
-   [AWS_Instance_Graphs.png](img/zenpack-aws_instance_graphs.png)
-   [AWS_Region_Graphs.png](img/zenpack-aws_region_graphs.png)
-   [AWS_Region_Instances.png](img/zenpack-aws_region_instances.png)
-   [AWS_S3Bucket_Graphs.png](img/zenpack-aws_s3bucket_graphs.png)
-   [AWS_Subnet_Graphs.png](img/zenpack-aws_subnet_graphs.png)
-   [AWS_Volume_Graphs.png](img/zenpack-aws_volume_graphs.png)
-   [AWS_VPC_Subnets.png](img/zenpack-aws_vpc_subnets.png)
-   [AWS_Zone_Volumes.png](img/zenpack-aws_zone_volumes.png)
-   [ZAWSRegionPEM_Property.png](img/zenpack-zawsregionpem_property.png)
-   [aws-logo-partner_2\_2.png](img/zenpack-aws-logo-partner_2_2.png)

# CloudFoundry

@lb[](img/zenpack-cloudfoundry-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.zenoss.CloudFoundry

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.CloudFoundry.git){.external-link}

### Applications Monitored:

CloudFoundry

## CloudFoundry ZenPack

CloudFoundry monitoring.

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 1.0.4- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.CloudFoundry/1.0.4/ZenPacks.zenoss.CloudFoundry-1.0.4.egg){.external-link}:   Released on 2013/04/01:   Compatible with Zenoss Core 3.1.x, Zenoss Core 3.2.x, Zenoss Core
    4.2.x, Zenoss Resource Manager 4.1.x, Zenoss Resource Manager 4.2.x

## Background

Please watch the \[<http://www.youtube.com/watch?v=uDUUVTWXCPE> Monitoring Cloud Foundry\] video for a quick introduction that covers
most of the details below.

This ZenPack makes it possible to monitor the capacity and performance
of applications running on a Cloud Foundry platform. This works for
applications hosted in a local micro-cloud or a hosted environment such
as the one offered by VMware at cloudfoundry.com.

[Cloud Foundry](http://www.cloudfoundry.com/){.external-link} is an open
PAAS (Platform as a Service) project initiated by
[VMware](http://www.vmware.com/){.external-link}.

## Usage

Once the CloudFoundry ZenPack is installed you can add endpoints by
going to the infrastructure screen and clicking the normal button for
adding devices. You will find a new option labeled, "Add CloudFoundry
Endpoint."

Choose that option and you'll be presented with a dialog asking for the
following inputs.

1.  Target - An example would be api.cloudfoundry.com or api.vcap.me.
2.  Email - The email address you used to register.
3.  Password

Once you click Add Zenoss will contact the target and get all of the
operationally interesting information that exists. Once it is complete
you'll find a new device in the /CloudFoundy device class with the same
name as the target you entered into the dialog. Click into this new
device to see everything that was discovered.

The following elements are discovered:

-   Frameworks
    -   Runtimes
    -   App Servers
-   System Services
-   Provisioned Services
-   Apps
    -   App Instances

The following performance metrics are collected:

-   Per-Endpoint (target)
    -   Limits
        -   App URIs
        -   Apps
        -   Memory
        -   Services
    -   Usage
        -   App URIs
        -   Apps
        -   App Instances
        -   Running App Instances
        -   Memory
        -   Services
    -   Utilization
        -   App URIs
        -   Apps
        -   Memory
        -   Services
-   Per-App
    -   Resources
        -   Memory
        -   Disk
    -   Usage
        -   CPU (average across instances)
        -   Memory
        -   Disk
    -   Utilization
        -   Memory
        -   Disk
    -   Instances
        -   Total
        -   Running
    -   Services
    -   URIs
-   Per-App Instance
    -   Quota
        -   Memory
        -   Disk
    -   Usage
        -   CPU
        -   Memory
        -   Disk
    -   Utilization
        -   Memory
        -   Disk

The following default thresholds are configured:

-   Over 99% utilization of..
    -   Endpoint App URIs
    -   Endpoint Apps
    -   Endpoint Memory
    -   Endpoint Services
    -   App CPU (average across instances)
    -   App Memory
    -   App Disk
    -   App Instance CPU
    -   App Instance Memory
    -   App Instance Disk
-   Less than 1 running instance per App

## Attachments:

-   [cloudfoundry-zenpack.png](img/zenpack-cloudfoundry-zenpack.png)
-   [cloudfoundry-zenpack.png](img/zenpack-cloudfoundry-zenpack.png)
-   [cloudfoundry-zenpack.png](img/zenpack-cloudfoundry-zenpack.png)


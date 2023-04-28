# Microsoft Message Queueing (MSMQ)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.zenoss.Microsoft.MSMQ

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.Microsoft.MSMQ){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.Microsoft.MSMQ.git){.external-link}

### Applications Monitored:

Microsoft Message Queueing (MSMQ)

## Microsoft Message Queueing (MSMQ) ZenPack

Monitoring for Microsoft Message Queueing (MSMQ).

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 1.3.2- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2017/11/29:   Compatible with Zenoss 4.2.x - 6.0.x:   Requires [Microsoft Windows ZenPack](https://help.zenoss.com/display/in/Microsoft+Windows "ZenPack:Microsoft Windows"){.external-link}

<!-- -->

Version 1.3.1- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2017/10/31:   Compatible with Zenoss 4.2.x - 5.3.x:   Requires [Microsoft Windows ZenPack](https://help.zenoss.com/display/in/Microsoft+Windows "ZenPack:Microsoft Windows"){.external-link}

<!-- -->

Version 1.3.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.Microsoft.MSMQ/1.3.0/ZenPacks.zenoss.Microsoft.MSMQ-1.3.0.egg){.external-link}:   Released on 2014/06/13:   Compatible with Zenoss 4.2.x - 5.1.x:   Requires [Microsoft Windows ZenPack](https://help.zenoss.com/display/in/Microsoft+Windows "ZenPack:Microsoft Windows"){.external-link}

## Background

The ZenPacks.zenoss.Microsoft.MSMQ ZenPack uses WinRM to automatically
discover Microsoft Message Queue (MSMQ) queues, and monitor the number
of messages queued in each.

The following description of Microsoft Message Queue (MSMQ) can be found
on Microsoft's MSMQ product page.

"Microsoft Message Queue (MSMQ) technology enables applications running
at different times to communicate across heterogeneous networks and
systems that may be temporarily offline. MSMQ provides guaranteed
message delivery, efficient routing, security, and priority-based
messaging. It can be used to implement solutions for both asynchronous
and synchronous messaging scenarios."

## Configuration

To monitor MSMQ queues, set up proper credentials so that Zenoss
platform can remotely monitor the target Windows servers.

This ZenPack supports two approaches to enable MSMQ queue monitoring, as
detailed in the next sections.

### Automatically Monitor Queues on All Servers

The easiest way to configure Zenoss platform to monitor your queues is
to enable queue discovery for the entire /Server/Microsoft/Windows
device class. Within 12 hours Zenoss platform will have automatically
discovered all of the queues available to be monitored and begun
monitoring how many messages are in each queue and creating threshold
events if they exceed 10,000 messages.

Perform the following steps to enable queue discovery for all Windows
servers.

1.  Navigate to the /Server/Microsoft/Windows device class.

<!-- -->

1.  Click **Details**.

<!-- -->

1.  Select Modeler Plugins from the left panel.

<!-- -->

1.  Click Add Fields.

<!-- -->

1.  Drag zenoss.winrm.MSMQQueueMap from the available fields to the list
    of plugins.

<!-- -->

1.  Click Save.

<!-- -->

1.  Wait about 12 hours for all Windows servers to be remodeled.

### Monitor Queues on Specific Servers

If you do not want Zenoss platform automatically monitoring queues on
all of your Windows servers and would rather point it to specific
servers you can do so by performing the following steps on each server
you're interested in.

1.  Navigate to the device.

<!-- -->

1.  Select Modeler Plugins from the left panel.

<!-- -->

1.  Click Add Fields.

<!-- -->

1.  Drag zenoss.winrm.MSMQQueueMap from the available fields to the list
    of plugins.

<!-- -->

1.  Click Save.

<!-- -->

1.  Select Model Device from the Action menu.

### Fine-Tuning Queue Monitoring

By default Zenoss platform will automatically monitor all queues on a
server that is running the MSMQ services. Each queue will also have a
default 10,000 maximum threshold applied to it. This means that an event
will be created when the number of messages in a single queue exceeds
10,000.

Note:

By default queues with names beginning with **tcp** will not be
discovered. You can change this behavior with the zMSMQIgnoreQueues
property. This property is a regular expression and any queues that
match it will not be discovered.

You can change the maximum messages threshold on a per-queue basis by
changing the Queues Messages Threshold property. Leaving this value
blank will have the result of no threshold being applied.

## Daemons

| Type                  | Name       |
|-----------------------|------------|
| Modeler               | zenmodeler |
| Performance Collector | zenpython  |

## Known Issues

-   No monitoring for MS Queues if Windows ZenPack 2.8.1 is installed,
    resolved in Windows ZenPack 2.8.2.

## Changes

**1.3.2**

-   Add support of system queues. (ZPS-2605)
-   Ensure relations are preserved on upgrade. (ZPS-2618)
-   Tested with Zenoss Resource Manager 6.0.1, Zenoss Resource Manager
    5.3.3, Zenoss Resource Manager 4.2.5 RPS 743 and Service Impact
    5.2.2.

**1.3.1**

-   Model queues that aren't in use or haven't passed messages yet.
    (ZPS-1690)
-   Remove outdated Modifications view from MSMQQueue/Details panel.
    (ZPS-2366)
-   Tested with Zenoss Resource Manager 5.3.2 and Zenoss Resource
    Manager 4.2.5 RPS 743.

# Nimble

@lb[](img/zenpack-nimble-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Jane Curry

### Maintainers:

Jane Curry

### Organization:

Skills 1st

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.community.Nimble

### More Information:

[GitHub page/HomePage](https://github.com/jcurry/ZenPacks.community.Nimble){.external-link}

### Link To More Docs:

[View Documentation](https://github.com/jcurry/ZenPacks.community.Nimble){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/jcurry/ZenPacks.community.Nimble){.external-link}

## Nimble ZenPack

This ZenPack is to manage Nimble storage arrays using the SNMP protocol.
A new nimble device type is created with a new component type to
represent volumes.

The ZenPack provides a modeler plugin to discover all volumes for a
Nimble device.

It also provides device classes of /Storage and /Storage/Nimble.

A performance template is provided to gather and graph the scalar data
listed above. The ZenPack binds this template to the /Storage/Nimble
device class.

A component performance template is provided to gather data for volume
usage and graph that data. Note that component templates must not be
manually bound - they bind automatically to the object type that exactly
matches the name of the template.

The two Nimble MIBs are included in the ZenPack.

A new event is raised on volume performance thresholds. This event
includes a transform to improve the summary field of the event.

Because this ZenPack needs to perform functions on SNMP values in
performance templates, the Zenoss Calculated Performance ZenPack is a
prerequisite, which itself has a prerequisite of the Python Collector
ZenPack. Objects

A new device object class - NimbleDevice - with a relationship of
nimbleVolume (note capitalisation) A new component object class for a
NimbleDevice - NimbleVolume - with a relationship nimbleDevice Modeler
Plugins

A modeler plugin - NimbleVolumeMap - which gathers id, name, various
sizes, online status and number of connections. The three sets of size
data are in 2 MIB values - high 32 bits and low 32 bits. The modeler
combines these values to present a single value in the NimbleVolume
object. We believe that the raw SNMP data is in MB. The modeler divides
this by 1024 to present values as GB.

The NimbleVolumeMap plugin is assigned to the /Storage/Nimble device
class by the ZenPack. Templates

Device-level template - NimbleGlobalStats - is available for device
classes from /Storage/Nimble. It is bound to this device class in the
ZenPack. It gathers and graphs ioreads/writes, ioSeqReads/Writes and
ioNonSeqReadHits.

Component template NimbleVolume (note the name exactly matches the new
object class), is available for device classes from /Storage/Nimble. It
must not be manually bound. It gathers volUsageHigh and volUsageLow SNMP
tables. To convert these values into a single datapoint, the Zenoss
Calculated Performance ZenPack is used to create a new datapoint of
volUsage. These values are all in MB.

Two thresholds are supplied for "30 percent used" and "90 percent used".
They access the object's value for VolSize (ie the maximum size of the
volume) and then threshold the VolUsage datapoint at the respective
percentages. The threshold value is multiplied by 1024 (as the VolSize
object data delivered by the modeler is given in GB). They generate a
/Perf/Nimble event if the threshold is breached.

Graphs are delivered of volUsageLow and volUsage. Note that the volUsage
datapoint in the VolUsage graph has been modified with an RPN (Reverse
Polish Notation) formula of 1024,\*,1024,\* . This does not affect the
value stored in the rrd datafile but does ensure that graph actually
shows bytes, rather than MB. The autoscaling of the rrdgraph utility
then automatically applies appropriate M / G / T on the labels.
zProperties

This ZenPack introduces no new zProperties but it does set the
zPythonClass property to ZenPacks.community.Nimble.NimbleDevice for the
device class /Storage/Nimble. MIBs

Two MIBs are supplied with this ZenPack:

           NIMBLE-TRAP-MIB
           NIMBLE-MIB

Events

The performance template has a threshold which generates an event of
class /Perf/Nimble. The event has a transform which improves the output
of the summary field. The event is included in the ZenPack.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.0.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.Nimble/1.0.1/ZenPacks.community.Nimble-1.0.1.egg){.external-link}:   Released on 2015/04/28:   Compatible with Zenoss Core 4.2.x, Zenoss Resource Manager 4.1.x,
    Zenoss Resource Manager 4.2.x

## Background

This ZenPack has 2 prerequisites:

           ZenPacks.zenoss.PythonCollector at least 1.6
           ZenPacks.zenoss.CalculatedPerformance 2.0.4 or higher

## Attachments:

-   [nimble-zenpack.png](img/zenpack-nimble-zenpack.png)
-   [nimble-zenpack.png](img/zenpack-nimble-zenpack.png)
-   [nimble-zenpack.png](img/zenpack-nimble-zenpack.png)


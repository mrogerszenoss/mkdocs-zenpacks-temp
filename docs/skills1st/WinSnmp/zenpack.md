# WinSnmp

@lb[](img/zenpack-microsoft-zenpack.png)

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

ZenPacks.skills1st.WinSnmp

### More Information:

[GitHub page/HomePage](https://github.com/jcurry/ZenPacks.skills1st.WinSnmp){.external-link}

### Link To More Docs:

[View Documentation](https://github.com/jcurry/ZenPacks.skills1st.WinSnmp){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/jcurry/ZenPacks.skills1st.WinSnmp){.external-link}

### Applications Monitored:

Microsoft Windows Services

## WinSnmp ZenPack

This ZenPack serves two purposes. One is to manage Windows devices via
the SNMP protocol; the second is to demonstrate examples of using the
Python Collector ZenPack.

The ZenPack is based on two earlier ZenPacks by Ryan Matte:

           ZenPacks.Nova.Windows.SNMPPerfMonitor is available at http://wiki.zenoss.org/ZenPack:Windows_SNMP_Performance_Monitor_%28Advanced%29
           ZenPacks.Nova.WinServiceSNMP can be found on the Zenoss wiki at http://wiki.zenoss.org/ZenPack:Windows_SNMP_Service_Monitor.

ZenPacks.Nova.Windows.SNMPPerfMonitor monitors cpu, memory, paging and
processes; ZenPacks.Nova.WinServiceSNMP has a modeler to gather Windows
Services components and a template to then gather operational status
data.

This ZenPack combines the functionality into one ZenPack and changes the
data collection method from using commands to using SNMP. This ZenPack
can coexist with Ryan's ZenPacks. In general, names have had "Python"
appended to them to make similar objects distinct from Ryan's.

The ZenPack introduces a new device class of /Server/Windows/Snmp and
then adds subclasses for different numbers of processors, whereas Ryan's
ZenPack works directly with devices under /Server/Windows.

To determine which group to place a server in perform an snmpwalk
command for hrProcessorLoad as follows:

snmpwalk -v1 -c &lt;snmp string&gt; &lt;host&gt; hrProcessorLoad

The number of lines corresponds to the number of CPUs.

Unlike Ryan's ZenPack, I have NOT provided exhaustive templates for each
different number of processors. A sample is provided; please expand the
templates to suit your own device requirements.

During installation and removal the ZenPack rebuilds device relations
for all devices within the /Server/WindowsSnmp device class. Depending
on the number of devices that you have in that class, it can take a long
time. You will notice some errors in the UI while the relations are
being rebuilt, which is normal. Please be patient and allow it to
complete. After the relations have been rebuilt Zenoss should be
restarted.

Make sure that you lock the services to prevent them from being removed
during a remodel while a service is down. Modeling will only pick up
services that are running. zProperties

           zWinServiceSNMPIgnoreNames: Place the full names of any services that you want to ignore in this line by line.
           zWinServiceSNMPMonitorNames: Place the full names of any services which you explicitly want to monitor (ignoring all others) in this line by line.
           zWinServiceSNMPMonitorNamesEnable: This enables/disables the use of zWinServiceSNMPMonitorNames

Note that you need to remodel your devices for the above to take effect.

Keep in mind that zWinServiceSNMPIgnoreNames is constantly in use. If
you put the same service name in both zWinServiceSNMPIgnoreNames and
zWinServiceSNMPMonitorNames it will be ignored. Templates

           PyTestSnmpCpu monitors CPU utilisation for each processor and the average total. Uses Python to drive SNMP
           PyTestSnmpMem monitors memory and paging using Python to drive SNMP
           PyTestCmdMemCpu monitors cpu and memory / paging using Python to drive commands. This template is not bound by default.
           PyTestSnmpServProc monitors number of processes and number of services. Uses Python to drive SNMP.
           WinServiceSNMPPython in /Server/Windows/Snmp: This template is required for monitoring services. Do not bind this template to the device. Make sure the template is in the class that the device is in (or a higher class). The template will automatically be used for the windows services components.

Modeler Plugins

community.snmp.WinServiceMap: This plugin is required during modeling.
It currently is based on the standard SnmpPlugin. Events

This ZenPack ships 2 events that are used with thresholds and templates.
Both have transforms.

           /Perf/Memory/Snmp

/Status/WinServiceSNMPPython

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.0.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.skills1st.WinSnmp/1.0.1/ZenPacks.skills1st.WinSnmp-1.0.1.egg){.external-link}:   Released on 2015/02/12:   Compatible with Zenoss Core 4.2.x, Zenoss Resource Manager 4.1.x,
    Zenoss Resource Manager 4.2.x

## Background

This ZenPack has a prerequisite of ZenPacks.zenoss.PythonCollector
&gt;=1.6

This ZenPack was developed partly as an illustration of using the Python
Collector ZenPack.

There is a draft document available that discusses this usage at
<http://www.skills-1st.co.uk/papers/jane/PythonZenPacks.pdf>

## Attachments:

-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)
-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)
-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)


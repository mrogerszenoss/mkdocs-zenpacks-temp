# IBM 3584

@lb[](img/zenpack-ibm-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Josh Baird

### Maintainers:

Josh Baird

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.community.IBM3584Mon

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.community.IBM3584Mon){.external-link}

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-3577){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.community.IBM3584Mon.git){.external-link}

We want to update this ZenPack and need your help!

@lb[](img/zenpack-ugly_car.png)

This ZenPack needs updating to run on the latest versions of Zenoss, and
to update it, we need an SNMP walk of a live device. If you have this
device in your datacenter, you can help! See [Using snmpwalk](https://help.zenoss.com/Using_snmpwalk "Using snmpwalk"){.external-link} for
more information

## IBM 3584 ZenPack

The main purpose of this ZenPack is to model IBM 3584 inventory
information (serial numbers, models) and monitor status of the library
via SNMP traps and status indicators.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Background

This ZenPack provides monitoring and modeling support for the IBM
TS3500/3584 Tape Library. Many thanks to Egor Puzanov for his generous
help in building and testing this ZenPack. Without his help, his
examples and time this ZenPack would not have been possible. Also,
thanks to Eric Edgar for his examples and help.

### Device Class

Upon installing the ZenPack a new device class named
/Devices/Storage/IBM/TapeLibrary is created. Add your tape library
device to this class.

### Modeled Information

The following information is modeled from the 3584:

zenoss.community.IBM3584Mon.IBM3584DeviceMap:   models the library model, serial number, product keys

zenoss.community.IBM3584Mon.IBM3584FrameMap:   models information about the library frames including model, serial
    mumber, type, status

zenoss.community.IBM3584Mon.IBM3584ChangerDevice:   models information about logical libaries including name,
    description, status

zenoss.community.IBM3584Mon.IBM3584AccessDevice:   models information about media access devices (tape drives)
    including name, type, model, firmware, serial number, cleaning
    status, status

To view the modeled information, click on the "Hardware" tab of the
device.

### Performance Graphs

Unfortunately, there is not a lot of performance data that is available
via SNMP on the 3584. For this reason, the main purpose of this ZenPack
is to model inventory information (serial numbers, models) and monitor
status of the library via SNMP traps and status indicators. 3 very
generic performance graphs are included with the ZenPack -- number of
changer devices/logical libaries, number of tapes, number of tape
drives.

### Event Parsing

This ZenPack includes pre-defined event mappings for SNMP traps located
in */Events/HW/Backup/Tape Library*. Alerts will be generated and
transformed when a SNMP trap is received from the tape library. You can
use the "Send Test SNMP Trap" function on your 3584 to test this
functionality.

## MIBs

This ZenPack includes all of the MIBs from IBM for the 3584.

## Prerequisites

<dl markdown="1">
<dt markdown="1">
Zenoss Version
</dt>
<dd markdown="1">
2.3
</dd>
<dt markdown="1">
ZenPack Dependencies
</dt>
<dd markdown="1">
[Advanced Device Details](https://help.zenoss.com/display/in/Advanced+Device+Details "ZenPack:Advanced Device Details"){.external-link}
</dd>
<dt markdown="1">
External Dependencies
</dt>
<dd markdown="1">
A working SNMPD on your 3584. This should be verified using snmpwalk
from your ZenOSS server:

    snmpwalk -v2c -c [community] [hostname]

</dd>
<dt markdown="1">
Installation
</dt>
</dl>

-   Create */Mibs/IBM subfolder*
-   Create */Devices/Storage device class*

## Attachments:

-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)
-   [Ugly_car.png](img/zenpack-ugly_car.png)
-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)
-   [Ugly_car.png](img/zenpack-ugly_car.png)
-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)
-   [Ugly_car.png](img/zenpack-ugly_car.png)


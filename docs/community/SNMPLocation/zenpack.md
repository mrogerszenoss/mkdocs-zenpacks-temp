# SNMP Location (RackSlot)

@lb[](img/zenpack-zenpack-general.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Daniel Robbins

### Maintainers:

Daniel Robbins

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.community.SNMPLocation

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.community.SNMPLocation){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.community.SNMPLocation.git){.external-link}

## SNMP Location (RackSlot) ZenPack

This ZenPack will automatically add devices to Location organizers based
on their SNMP location OID (sysLocation). Locations will be created
automatically as necessary. Special code to initialize rackSlot values
has been added.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 2.1.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.SNMPLocation/2.1.0/ZenPacks.community.SNMPLocation-2.1.0.egg){.external-link}:   **Summary of changes:** Initial RackSlot enhancement release.
:   Released on 2013/03/27:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.1.x, Zenoss Core
    3.2.x, Zenoss Core 4.2.x, Zenoss Resource Manager 4.1.x, Zenoss
    Resource Manager 4.2.x

## Background

This ZenPack configures Zenoss to automatically put devices into
location organizers based on each device's SNMP Location (ie.
sysLocation in snmpd.conf.) If a location organizer does not exist, it
will be created, and updated device sysLocation values will result in
devices moving into an updated location after remodel. It is based on
the vanilla [SNMP Location ZenPack](https://help.zenoss.com/display/in/snmp-location-page-does-not-exist "ZenPack:SNMP Location (page does not exist){.external-link}").
Heirarchies of devices are supported by using a "/" within the
sysLocation value.

Special modifications have been made to this "RackSlot" version of the
ZenPack to initialize the device's rackSlot value (visible on the
*Overview* page) in certain cases:

-   *RU support*: Albuquerque/Citylink-25 will result in the location
    being set to Albuquerque/Citylink and rackSlot initialized to
    rh=1,ru=25
-   *rear RU support*: Albuquerque/Citylink-r25 (use "r" or "R") will
    result in the location being set to Albquerque/Citylink and rackSlot
    initialized to rh=1,split=rear,ru=25
-   *side/rear support*: Albuquerque/Citylink-rl will result in the
    location being set to Albuquerque/Citylink and the rackSlot
    initialized to split=left/rear. Use Citylink-rr for
    split=right/rear.
-   *side support*: Albuquerque/Citylink-r wil result in the location
    being set to Albuquerque/Citylink and the rackSlot initialized to
    split=right. Use Citylink-l for split=left.

**Note:** The split syntax used for rackSlot will be supported by an
upcoming RackView ZenPack release.

If no -\[SUFFIX\] is appended to the sysLocation, then the rackSlot will
not be initialized. In addition, the sysLocation will be checked at
every device remodel (by default every 12 hours) for any updates. User
modifications to rackSlot made in the Zenoss user interface will be
preserved as long as the sysLocation does not change. If the sysLocation
changes, then in addition to moving the device into the new location
organizer setting, the rackSlot will be re-initialized or cleared (if no
-SUFFIX) as per the above rules upon remodel. Just changing the -SUFFIX
in the sysLocation will also cause the device's rackSlot value to be
re-initialized as per the above rules.

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


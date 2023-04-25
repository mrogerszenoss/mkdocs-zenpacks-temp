# Device Access Control Lists

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Name:

ZenPacks.zenoss.ZenDeviceACL

## Device Access Control Lists ZenPack

The Device Access Control List (ACL) Enterprise ZenPack (ZenDeviceACL)
adds fine-grained security controls to Resource Manager.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.ZenDeviceACL ZenPack adds fine-grained device access
controls (ACLs) to Zenoss platform.

You can use ACLs to limit user access to data, such as limiting access
to certain departments within a large organization, or limiting a
customer of a service provider to see only his own data.

A user with limited access to objects also has a more limited view of
features within the system. Most global views, such as the network map,
event console, and all types of class management, are not available. The
Device List is available, as are the device organizers Systems, Groups,
and Locations. A limited set of reports can also be accessed.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.2 or higher |
| Required ZenPacks | ZenPacks.zenoss.ZenDeviceACL              |

## Permissions and Roles

Actions in Zenoss platform are assigned permissions. For example, to
access the device edit screen you must have the &ldquo;Change Device&rdquo;
permission. Permissions are not assigned directly to a user, but granted
to roles, which are then assigned to a user. A common example is the
ZenUser role. Its primary permission is &ldquo;View,&rdquo; which grants read-only
access to all objects.

ZenManagers have additional permissions, such as &ldquo;Change Device,&rdquo; which
grants users with this role access to the device edit screen. When you
assign a role to a user (using the Roles field on the Edit tab), it is
assigned globally. When creating a restricted user you may not want to
give that user a global role.

For more information about Zenoss platform roles, refer to <cite>Zenoss
Service Dynamics Resource Management Administration</cite>.

## Administered Objects

Device ACLs provide limited control to various objects in the system.
Administered objects are the same as device organizers (groups, systems,
locations, and devices). If access is granted to any device organizer,
it extends to all devices in that organizer.

To assign access to objects for a restricted user, you must be assigned
the Manager or ZenManager role. Zenoss platform grants access to objects
by using the &ldquo;Administered Objects&rdquo; selection for a user or user group.
To limit access, you must not assign a &ldquo;global&rdquo; role to the user or
group.

## Users and Groups

Users and user groups work exactly as they would normally. For more
information about managing users and groups, <cite>Zenoss Service
Dynamics Resource Management Administration</cite>.

## Assigning Administered Object Access

For each user or group there is selection called "Administered Objects."
The Action menu has an "Add" item for each type of administered object.
Adding an object will bring up a dialog box with live search on the
given type of object.

After adding an object, you can assign it to a role. Roles can be
different for each object. For example, a user or group might have the
ZenUser role assigned to a particular device but the ZenManager role
assigned to a location organizer. If multiple roles are granted to a
device though direct assignment and organizer assignment, the resulting
permissions will be additive. For the previously cited example, if the
device is within the organizer the user will inherit the ZenManager role
on the device.

## Restricted Screen Functionality

### Dashboard

By default, the dashboard is configured with three portlets:

-   Object Watch List
-   Device Issues
-   Production State

These have content that are restricted to objects for a given user.

### Device List

The device list is automatically filtered to devices of a restricted
user, scoped to accessible devices. There are no menu items available.

### Device Organizers

Device organizers control groups of devices for a restricted user. Each
device added to the group will be accessible to the user. Permissions
are inherited through multiple tiers of a device organizer.

### Reporting

Reports are limited to device reports and performance reports.

### Viewing Events

A user in restricted mode does not have access to the global event
console. The available events for the user can be seen under his
organizers.

## Create a User Restricted to Specific Devices

1.  As admin or any user account with Manager or ZenManager role, create
    a user named acltest. Set a password for the user.
2.  From the user&rsquo;s Edit page, make sure that no role is assigned.
3.  Select the user&rsquo;s Administered Objects page.
4.  From the Action menu, select the &ldquo;Add Device…&rdquo; item and add an
    existing device to that user. The device&rsquo;s role defaults to ZenUser.
5.  Log out of your browser, or open a second browser and then log in as
    acltest.
6.  Go to Infrastructure &gt; Devices. You should see only the device
    you assigned to acltest.
7.  Navigate to the device and notice that the Edit selection is not
    available. This is because you are in read-only mode for this
    device.

## Create a Manager Restricted to Specific Devices

Following the previous example:

1.  Go back to the acltest user's Administered Objects and set the role
    on the device to ZenManager.
2.  As acltest, navigate to the device. You now have access to the Edit
    page.

## Adding Device Organizers

1.  Go to the Groups root and create a group called &ldquo;RestrictGroup."
2.  Go to the acltest user&rsquo;s Administered Objects and add the group to
    the user.
3.  Logged in as acltest, notice that the Navigation menu has the Groups
    item. Group can be added to a user.
4.  Place a device within this group and as acltest you should not only
    see the device within the group but also in the device list.

## Restricted User Organizer Management

1.  Assign the acltest user the ZenManager role on your restricted
    group.
2.  As acltest, you can now add sub-organizers under the restricted
    group.

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


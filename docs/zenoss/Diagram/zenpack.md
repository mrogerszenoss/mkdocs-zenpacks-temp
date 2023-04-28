# Datacenter View

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.Diagram

## Datacenter View ZenPack

Datacenter view provides a top-down floorplan of devices in a
datacenter, as well as a front and back-of-rack view.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.Diagram ZenPack enables a visual representation of
devices (such as servers or blades) and device containers (such as racks
or chassis).

With this feature, you can create a custom view that represents a
physical space (such as a data center) by customizing the view
background. You can then overlay this view with active representations
of your devices and device containers.

Custom View

@lb[](img/zenpack-(diagram)datacenterview.diagram_custom_view.png)

For each device or device container, the system can generate a rack
view, which diagrams the physical location of devices in a chassis or
rack. Each represented device provides at-a-glance information about its
status.

Rack View

@lb[](img/zenpack-(diagram)datacenterview.diagram_rack_view.png)

## Prerequisites

| Prerequisite      | Restriction             |
|-------------------|-------------------------|
| Product           | Zenoss platform 4.x     |
| Required ZenPacks | ZenPacks.zenoss.Diagram |

Before a device or sub-location can appear in Datacenter View:

-   At least one organizer must be configured
-   At least one device or sub-organizer must be included in a location

To see the auto-generated rack view, you must set a rack slot value for
the device. (*Activating the Auto-Generated Rack View*.)

## Configuring

Before a device or sub-location can appear in Datacenter View:

-   At least one organizer must be configured
-   At least one device or sub-organizer must be included in a location

To see the auto-generated rack view, you must set a rack slot value for
the device.

## Working with the List View

The List View provides a view of your devices (or, if configured, the
Rack View).

Follow these steps to access the List View:

1.  From the interface, select Infrastructure.
2.  In the devices hierarchy, select a location, group, or system.
3.  Click **Details**.
4.  Select Datacenter View. The List View appears. Note: After you
    create a Custom View, that view appears by default.

## Working with the Custom View

The Custom View lets you create a visual representation of your physical
space (such as a data center).

To access the Custom View, from the Diagram selection, click Custom
View.

You can edit the Custom View to:

-   Add or change a background image
-   Move or resize device images
-   Remove the view

### Adding a Background Image to the Custom View

Follow these steps to create a custom view and add a background image to
the view:

1.  From the Datacenter View page (accessed from the Diagram selection),
    click **Custom View**.
2.  Click **Edit** to enable edit mode. The Edit button highlights to
    indicate that it is active, and Options selections become available.
3.  Select Options &gt; Change Background. The Change Background dialog
    appears.
4.  Select Background Image from URL from the list of options.
5.  Enter an image location in the Image URL field, and then click
    **Save**. Any image format and size supported by your browser can be
    used. Change Background ![](http://help.zenoss.com/plugins/servlet/confluence/placeholder/unknown-attachment?locale=en_US&version=2){.confluence-embedded-image     .confluence-external-resource .external-link}

#### Removing the Custom View Background Image

To remove the current background image from the Custom View:

1.  From the Custom View area, click Edit.
2.  Select Options &gt; Change Background.
3.  In the Change Background dialog, select No background image from the
    list of options.
4.  Click **Save**. The image no longer appears in the view.

### Working with Devices in the Custom View

Devices in the custom view can be moved and resized. To work with
devices in this view, click **Edit**. You can then drag devices to a
specific location in the view, and resize them to accurately represent
your physical space.

You also can view device details from this view. Click the device to go
to its Status page.

Note: To access device status, you cannot be in edit mode.

### Removing the Custom View

Removing the custom view removes the view and custom background image,
if any. To remove a custom view:

1.  From the Datacenter View page (accessed from the Diagram selection),
    click **Custom View**.
2.  Click Edit to enable edit mode.
3.  Select Options &gt; Remove Custom View. The custom view no longer
    appears by default. If you select Custom View, devices still appear
    in the view; however, they are reset to default positions and sizes.

## Activating the Auto-Generated Rack View

First, ensure that the device is included in a location. Then follow
these steps to make devices visible in Datacenter View.

1.  Edit the device you want to make visible. From the list of Devices,
    select a device (in the illustration, beta.zenoss.loc), click
    **Details**, and then select Edit.

2.  Enter values for Rack Slot, in the format: ru=*n*,rh=*n*,st=*n*
    where:

    -   ru=*n* sets the value for rack unit (the lowest unit used by the
        device)
    -   rh=*n* sets the value for rack height (the number of units the
        device uses in the rack)
    -   st=*n* sets the value for rack slot
    -   sc=*n* sets the value for slot capacity (set only for chassis
        devices)

    For example, values of:

    ru=2,rh=1

    establishes a device visually in the rack as shown in this
    illustration:

    Setting Rack Slot Value

    @lb[](img/zenpack-(diagram)datacenterview.diagram_set_rack_slot.png)

    Note: In the example, a rack slot value is not needed, as there is
    only one device.

3.  Click **Save**.

The device appears in Datacenter View. In the List View, it appears as
part of a rack illustration. (The rack illustration is now the default
image in the List View.)

In the Custom View, it appears as a single device image.

Note: You can customize this device image by modifying the zIcon
configuration property in the device class.

# VMware vCloud

@lb[](img/zenpack-vmware-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.vCloud

### Applications Monitored:

VMware vCloud (1.0, 1.5, 5.1, 5.5)

## VMware vCloud ZenPack

The VMware vCloud ZenPack enables Resource Manager to use VMware's Cloud
Director native management API to extend in-depth availability,
performance, and event monitoring into the vCloud platform.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 1.4.9- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2014/08/15:   Compatible with Zenoss Resource Manager 4.1.x, Zenoss Resource
    Manager 4.2.x

## Background

The ZenPacks.zenoss.vCloud ZenPack monitors virtual infrastructure
services that are managed by VMware vCloud Suite platforms.

VMware vCloud acts as a cloud layer on top of one or more vSphere
virtual infrastructures. It allows for easy deployment of public or
private clouds with required concepts, such as a self-service portal
with built-in multi-tenancy. vCloud enables you to allocate your vSphere
resources as desired to provide abstracted compute (CPU and memory) and
storage resources to internal or external customers.

You can find more information about cloud computing and vCloud at the
VMware site:

<http://www.vmware.com>

This ZenPack uses VMware's Cloud Director native management API to
extend in-depth availability and performance monitoring into the vCloud
platform. If you provide the vCloud service, you can use the vCloud
administrator perspective to gain a complete view of the entire cloud
architecture. Or, as a vCloud consumer, you can use the user perspective
to obtain organization-specific information.

## Adding a Cell

A *cell* (also known as the cloud director or self-service portal) is
the service to which Zenoss platform connects to perform all discovery
and monitoring. Follow these steps to use Zenoss platform to discover
the cloud and all available details:

1.  From the Zenoss platform user interface, select Infrastructure &gt;
    Devices. The device list appears.
2.  Click the Add Device menu, and then select Add vCloud Cell. The Add
    vCloud Cell dialog appears. Add vCloud Cell ![](plugins/servlet/confluence/placeholder/unknown-attachment "%28vCloud%29VMwarevCloud.Add_vCloud_Cell_Dialog.png"){.confluence-embedded-image}
3.  Enter information in the dialog to add the vCloud cell:
    -   **Hostname or IP Address** - Enter the host name or IP address
        for the cell.
    -   **Port \#** - Enter the cell port number.
    -   **Username** - Enter the user name, in the form
        *username*@*organization*. For example, if you are the cell
        administrator, enter `administrator@system`. Alternatively, if
        you user name is Joe and you are part of the ACME organization,
        enter `Joe@ACME`.
    -   **Password** - Enter the password for username.
4.  Click **Add**. A dialog appears with the option to view the job log
    of the cell being discovered. Select the option to view the job log
    and monitor the job's completion.

## Monitoring

The zenvcloud daemon uses the VMware Cloud Director API to perform a
range of monitoring tasks. After your cell is added to Zenoss platform,
monitoring begins automatically.

## Performance

Zenoss platform collects these metrics directly from the cell for each
vDC, irrespective of whether you have administrator or user credentials:

-   CPU Limit, Allocated and Used
-   Memory Limit, Allocated and Used
-   Storage Limit, Allocated and Used

Zenoss platform collects these metrics directly from the cell for each
Provider vDC if you have administrator credentials:

-   CPU Capacity, Allocation and Free
-   Memory Capacity, Allocation and Free
-   Storage Capacity, Allocation and Free

## Changes

<dl markdown="1">
<dt markdown="1">
1.4.9
</dt>
</dl>

-   Allow component monitoring to be disabled and enabled. (ZEN-13166)

<dl markdown="1">
<dt markdown="1">
1.4.8
</dt>
</dl>

-   Fix modeling vCloud 5.1 using tenant credentials. (ZEN-10762)
-   Fix "dnd" error in web interface. (ZEN-10761)

<dl markdown="1">
<dt markdown="1">
1.4.7
</dt>
</dl>

-   Fix vCloud VM service impact issue introduced in 1.4.5.

<dl markdown="1">
<dt markdown="1">
1.4.6
</dt>
</dl>

-   Remove DynamicView and ZenVMware ZenPack requirements.

<dl markdown="1">
<dt markdown="1">
1.4.5
</dt>
</dl>

-   Support new MAC address index for faster modeling.

<dl markdown="1">
<dt markdown="1">
1.4.4
</dt>
</dl>

-   Fix error that could appear in device overview "Links" area.

<dl markdown="1">
<dt markdown="1">
1.4.3
</dt>
</dl>

-   Add support for vCloud 1.5 and 5.1.

## Attachments:

-   [(vCloud)VMwarevCloud.Add_vCloud_Cell_Dialog.png](img/zenpack-vmwarevcloud.add_vcloud_cell_dialog.png)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)
-   [(vCloud)VMwarevCloud.Add_vCloud_Cell_Dialog.png](img/zenpack-vmwarevcloud.add_vcloud_cell_dialog.png)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)
-   [(vCloud)VMwarevCloud.Add_vCloud_Cell_Dialog.png](img/zenpack-vmwarevcloud.add_vcloud_cell_dialog.png)


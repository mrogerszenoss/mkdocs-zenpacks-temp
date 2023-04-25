# VMware ESX Server Monitor

@lb[](img/zenpack-vmware-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.EsxTop

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-9384){.external-link}

### Applications Monitored:

VMWare ESX Server

## VMware ESX Server Monitor ZenPack

The VMWare ESX Server ZenPack for Core allows you to monitor ESX hosts
and guests via VMWares EsxTop utility. The ZenPack uses the resxtop
command to gather performance information about VMware Infrastructure™
ESX™ servers.

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Background

This ZenPack uses the VMware `resxtop` command to gather performance
information about VMware ESX servers. NOTE: This ZenPack is deprecated;
use ZenPacks.zenoss.vSphere instead.

This ZenPack can be used alone, or with one of the other VMware
ZenPacks. When used alone, a basic modeler creates virtual machines
under the /Devices/Server/Virtual Hosts/EsxTop device class for any host
device that is added and modeled. Otherwise, performance data can be
collected for the ESX hosts modeled by the other ZenPacks.

## Prerequisites

<table>
<colgroup>
<col />
<col />
</colgroup>
<tbody>
<tr markdown="1">
<th width="50%">Prerequisite</th>
<th width="50%">Restriction</th>
</tr>

<tr markdown="1">
<td>Product</td>
<td>Zenoss platform 4.x</td>
</tr>
<tr markdown="1">
<td>Required ZenPacks</td>
<td>ZenPacks.zenoss.ZenossVirtualHostMonitor v2.3.5
<p>ZenPacks.zenoss.EsxTop</p></td>
</tr>
<tr markdown="1">
<td>Required Software (on collectors)</td>
<td>OpenSSL development package v0.9.7
<p>VMware vSphere CLI v4.1</p></td>
</tr>
</tbody>
</table>

## Installing Prerequisite Libraries

The VMware vSphere CLI is required for access to the `resxtop` command,
which enables Zenoss platform to model and gather performance
information about individual ESX servers.

Follow these steps to install the CLI and required software:

1.  If you have not yet installed it, install the OpenSSL development
    package. For example, for an RPM-based system, enter:

        yum install openssl-devel

2.  From your VMware account, download the VMware vSphere CLI. Note: For
    downloads and documentation, go to:
    <http://downloads.vmware.com/d/details/vcli41/ZHcqYmRoaCpiZHRAag==>

3.  Copy the package to each Zenoss platform collector.

4.  For each collector:
    1.  Expand the package file.

    2.  Run the following command to install the package:

            ./vmware-install.pl

    3.  As the zenoss user, run the following command to verify
        successful installation:

            resxtop --server myESXServer --user userOnRemoteEsxServerAllowedToUseEsxTop -b -n 1 -a

        The `resxtop` command prompts for a password.

    4.  Enter the password for a user with permissions on the remote ESX
        server. If the command is working correctly, then a screen
        displays with several pages of command output.

    5.  Create a symbolic link from the location that the `resxtop`
        command was installed into the $ZENHOME/libexec directory. This
        allows the `check_esxtop` command to automatically determine
        which binary to run. For example:

            cd $ZENHOME/libexec
            ln -s PathToResxtop

    6.  Test the `check_esxtop` command by showing the VMs on the remote
        server:

            $ZENHOME/ZenPacks/Ze*EsxTop*/Z*/z*/E*/libexec/check_esxtop --server=myEsxserver \
             --user=userOnRemoteEsxServerAllowedToUseEsxTop --password=password --showvms

## Enabling the ZenPack

Follow these steps to enable this ZenPack. From the Zenoss platform
interface, add a host:

1.  From Infrastructure &gt; Devices, navigate to the
    /Devices/Server/Virtual Hosts/EsxTop device class.
2.  From the Add Device menu, select Add a Single Device. The Add a
    Single Device dialog appears.
3.  Enter a host name or IP address.
4.  De-select the Model Device option.
5.  Click **Add**.
6.  Select the newly added device in the list. The device overview
    appears.
7.  Click **Details**, and then select Configuration Properties in the
    left panel.
8.  Enter login credentials for the zCommandUsername and
    zCommandPassword configuration properties, and then click **Save**.
9.  If the device has an SNMP agent installed, update the ESX device
    configuration with the appropriate SNMP configuration information,
    and then add any desired modeler plugins.
10. From the Action menu, select Model device.

## Daemons

|                       |            |
|-----------------------|------------|
| Type                  | Name       |
| Modeler               | zenmodeler |
| Performance Collector | zencommand |

## Attachments:

-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)


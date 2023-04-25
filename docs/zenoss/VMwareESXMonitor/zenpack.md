# VMware ESX SNMP (Commercial)

@lb[](img/zenpack-vmware-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.VMwareESXMonitor

## VMware ESX SNMP (Commercial) ZenPack

Monitoring for VMware ESX hosts. Uses SNMP.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.VMwareESXMonitor ZenPack monitors VMware ESX hosts
and their guests, using SNMP.

Note: This ZenPack is deprecated; see ZenPacks.zenoss.vSphere.

With this ZenPack, the zenmodeler daemon can discover guests running on
ESX hosts, and provide screens and templates for collecting and
displaying resources allocated to guests.

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
<td>ZenPacks.zenoss.VMwareESXMonitor,
<p>ZenPacks.zenoss.ZenossVirtualHostMonitor</p></td>
</tr>
</tbody>
</table>

## Monitoring VMware ESX Servers

To monitor VMware ESX servers:

1.  Make sure you have SNMP connectivity to your ESX 3 servers.
2.  Create your ESX services using the /Servers/Virtual Hosts/ESX device
    class. Note: If you have already modeled these servers, then remove
    and recreate them under the ESX device class. Do not move them.
3.  Select the Guest menu and ensure that the guest hosts were found
    when the devices were added.
4.  Using the VMware vSphere client, add Zenoss platform to the list of
    destinations for SNMP traps. (See Administration &gt;
    vCenterServerSettings &gt; SNMP.) For information about configuring
    traps for a stand-alone ESX 3 server, see "About SNMP and VMware
    Infrastructure" at:
    <http://www.vmware.com/pdf/vi3_35/esx_3/r35u2/vi3_35_25_u2_admin_guide.pdf>

Notes:

-   There is a link to the VMware Web interface on each ESX server
    Status page.
-   If the name of the Guest under ESX is the same as the name of a
    device being monitored directly by Zenoss platform, a link is
    provided to take you directly to that device from the Guest list.

## Enabling SNMP Subagents

ESX servers (Version 4.x and higher) contain an SNMP subagent from
VMware. This subagent provides all information related to VMware (such
as virtual machines and their status). By default, the subagent is
disabled.

The VMware SNMP subagent does not provide information about the ESX
server itself (such as processes, memory, CPU, or performance data).

Note: The VMware SNMP subagent cannot share port 161. If any other agent
is using that port (usually the NET-SNMP agent), the subagent cannot
start.

To fully monitor the ESX machine on your Zenoss platform server, you
must enable both SNMP agents (NET-SNMP and the VMware subagent). Follow
these steps to enable both agents using an SNMP proxy:

1.  Stop the snmpd service through the service console (via SSH) on the
    ESX host:

        service snmpd stop

2.  Add a proxy line to the /etc/snmp/snmpd.conf file:

        proxy -v 1 -c public udp:127.0.0.1:171 .1.3.6.1.4.1.6876

    This line will use the snmpd service to access the VMware MIB on the
    subagent running at port 171.

3.  Using the VMware vSphere CLI (command line interface), bind the
    VMware SNMP agent to port 171, and then enable the subagent by using
    these commands:

        vicfg-snmp.pl --server <hostname|IP address> --username  --password  -c \
         public --port 171
        vicfg-snmp.pl --server <hostname|IP address> --username  --password  -E

4.  Via SSH, go back to the ESX host. Restart the mgmt-vmware service
    (hostd) and the snmp service. On the ESX host from the service,
    enter:

        service mgmt-vmware restart
        service snmpd restart

## Daemons

|                       |             |
|-----------------------|-------------|
| Type                  | Name        |
| Modeler               | zenmodeler  |
| Performance Collector | zenperfsnmp |

## Attachments:

-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)


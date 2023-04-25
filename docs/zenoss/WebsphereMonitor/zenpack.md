# IBM WebSphere

@lb[](img/zenpack-ibm-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.WebsphereMonitor

### Applications Monitored:

IBM WebSphere

## IBM WebSphere ZenPack

This ZenPack allows Resource Manager to monitor IBM WebSphere
Application Servers (WAS).

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 1.2.2- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2016/01/15:   Requires [ZenPacks.zenoss.ZenWebTx ZenPack](https://help.zenoss.com/display/in/zenpackszenosszenwebtx-page-does-not-exist "ZenPack:ZenPacks.zenoss.ZenWebTx (page does not exist){.external-link}"):   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.x.x:   Compatible with WebSphere 5 & 6

## Background

The ZenPacks.zenoss.WebsphereMonitor ZenPack monitors IBM WebSphere
Application Servers (WAS).

## Configure WAS for Monitoring

To successfully monitor WebSphere, you must have the Performance
Monitoring Infrastructure (PMI) servlet installed and enabled on your
WebSphere instance. For more information, please see the [IBM WebSphere documentation.](http://publib.boulder.ibm.com/infocenter/tivihelp/v3r1/topic/com.ibm.itcamwas.doc_6.1/itcam_61_4_was_dc_zos_install_guide69.htm#customizepmizosdc){.external-link}

## Configure Zenoss platform

1.  Navigate to the device or device class under the
    /Devices/Server/Tomcat device class in the Zenoss platform
    interface.
    -   If applying changes to a device class:
        1.  Select the class in the devices hierarchy.
        2.  Click **Details**.
        3.  Select Configuration Properties.
    -   If applying changes to a device:
        1.  Click the device in the device list.
        2.  Select Configuration Properties.
2.  Edit the appropriate configuration properties for the device or
    devices.

    WebSphere Configuration Properties
    <table>
    <colgroup>
    <col />
    <col />
    </colgroup>
    <tbody>
    <tr markdown="1">
    <th width="50%">Property</th>
    <th width="50%">Description</th>
    </tr>

    <tr markdown="1">
    <td>zWebsphereURLPath</td>
    <td>Path to the PMI servlet on a WebSphere instance.
    <p>The default value is the default path on a WebSphere installation:</p>
    <p>wasPerTool/servlet/perfservlet</p></td>
    </tr>
    <tr markdown="1">
    <td>zWebsphereUser</td>
    <td>Used for HTTP basic authentication. This field is not required, and is empty by default.</td>
    </tr>
    <tr markdown="1">
    <td>zWebspherePassword</td>
    <td>Used for HTTP basic authentication. This field is not required, and is empty by default.</td>
    </tr>
    <tr markdown="1">
    <td>zWebsphereAuthRealm</td>
    <td>Used for HTTP basic authentication. This field is not required, and is empty by default.</td>
    </tr>
    <tr markdown="1">
    <td>zWebsphereServer</td>
    <td>Used by the provided template to build the xpath queries for the data to collect. You must supply a value for this field. There is no default value.</td>
    </tr>
    <tr markdown="1">
    <td>zWebsphereNode</td>
    <td>Used by the provided template to build the queries for the data to collect. You must supply a value for this field.</td>
    </tr>
    </tbody>
    </table>

3.  Click Save to save your changes.
4.  Select Device under Monitoring Templates in the left panel.
5.  From the Action menu, select Bind Templates. The Bind Templates
    dialog appears.
6.  Move the Websphere template from the Available list to the Selected
    list, and then click **Save**. The Websphere template should now be
    displayed under the Monitoring Templates for Device. You will now be
    able to start collecting the WebSphere metrics from this device.
7.  Navigate to Graphs and you should see some place holders for graphs.
    After approximately 15 minutes you should see the graphs start to
    become populated with information.

## Examples

Once the PMI module has been installed into WAS, you can generate the
PMI XML file. You then can use this file to complete the monitoring
template.

This example shows how to obtain the configuration properties required
for basic monitoring functionality. It further shows how to add other
metrics to be monitored.

You can generate the PMI XML file by browsing to this URL:

http://*WASserver*/wasPerfTool/servlet/perfservlet

Note: This is the default WAS server location. The URL should match the
configuration property setting used in the template.

where *WASserver* is the WAS server's host name or IP address.

The following example XML file results:

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE PerformanceMonitor SYSTEM "/wasPerfTool/dtd/performancemonitor.dtd">
    <PerformanceMonitor responseStatus="success" version="6.1.0.21">
      <Node name="serverA">
        <Server name="serverAB">
          <Stat name="serverABC">
    ...
            <Stat name="Dynamic Caching">
              <Stat name="Object: ws/WSSecureMap">
                <Stat name="Object Cache">
                  <Stat name="Counters">
      <CountStatistic ID="21" count="0" lastSampleTime="1242827146039" name="HitsInMemoryCount" \
        startTime="1242827146039" unit="N/A"/>
      <CountStatistic ID="28" count="5" lastSampleTime="1243610826245" name="MissCount" \
        startTime="1242827146039" unit="N/A"/>
                  </Stat>
                 </Stat>
               </Stat>
             </Stat>
    ...
           </Stat>
        </Server>
      </Node>
    </PerformanceMonitor>

In the previous example, configuration properties settings are:

-   zWebsphereNode: serverA
-   zWebsphereServer: serverAB

You might want to add counters beyond the standard counters. For
example, you might want to add the HitsInMemoryCount and MissCount
counters (related to dynamic caching). To do this, you would add the
following Twill commands to the Script tab of your WebSphere data
source:

    xpathextract HitsInMemoryCount '/PerformanceMonitor/Node[@name="${here/zWebsphereNode}"]/\
    Server[@name="${here/zWebsphereServer}"]/Stat[@name="server"]/Stat[@name="Dynamic Caching"]/\
    Stat[@name="Object: ws/WSSecureMap"]/Stat[@name="Object Cache"]/Stat[@name="Counters"]/\
    CountStatistic[@name="HitsInMemoryCount"]/attribute::count' xpathextract MissCount \
    '/PerformanceMonitor/Node[@name="${here/zWebsphereNode}"]/\
    Server[@name="${here/zWebsphereServer}"]/Stat[@name="server"]/Stat[@name="Dynamic Caching"]/\
    Stat[@name="Object: ws/WSSecureMap"]/Stat[@name="Object Cache"]/Stat[@name="Counters"]/\
    CountStatistic[@name="MissCount"]/attribute::count'

After adding these commands, you would then add the data points for
HitsInMemoryCount and MissCount, and then add the data points to a
graph.

## Daemons

|                       |          |
|-----------------------|----------|
| Type                  | Name     |
| Performance Collector | zenwebtx |

## Changes

<dl markdown="1">
<dt markdown="1">
1.2.2
</dt>
</dl>

-   Added support for Zenoss 5.x

## Attachments:

-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)
-   [ibm-zenpack.png](img/zenpack-ibm-zenpack.png)


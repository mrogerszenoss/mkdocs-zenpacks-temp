# HTTP Monitor

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.HttpMonitor

### Git Sources (For Cloning):

[HTTP Monitor](https://github.com/zenoss/ZenPacks.zenoss.HttpMonitor){.external-link}

## HTTP Monitor ZenPack

This ZenPack provides status and response time monitoring of HTTP URLs.

## Releases

Version 3.1.2-[Download](https://delivery.zenoss.com/){.external-link}:   Released on 2022/06/20:   Requires [PythonCollector ZenPack](http://zenoss.com/product/zenpacks/pythoncollector){.external-link}:   Compatible with Zenoss 6.x and Zenoss Cloud

Version 3.1.1-[Download](https://delivery.zenoss.com/){.external-link}:   Released on 2022/05/05:   Requires [PythonCollector ZenPack](http://zenoss.com/product/zenpacks/pythoncollector){.external-link}:   Compatible with Zenoss 6.x and Zenoss Cloud

## Background

The ZenPacks.zenoss.HttpMonitor ZenPack monitors the response times of
HTTP server connection requests, and determines whether specific content
exists on a Web page.

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Gallery

@lb[](img/zenpack-defaultconfiguration.png)
@lb[](img/zenpack-examplegraph.png)
@lb[](img/zenpack-proxyconfiguration.png)
@lb[](img/zenpack-proxyport8080.jpg)
@lb[](img/zenpack-proxyport8080andsiteport8888.jpg)
@lb[](img/zenpack-proxywithauth.png)

## Features

HttpMonitor features include:

-   Monitors HTTP response time
-   Monitors HTTP page size
-   Monitors HTTP response code
-   Monitors HTTP through Proxy server
-   Monitors HTTP with Basic access authentication
-   Monitors HTTP specific content on the Web page

## Enable Monitoring

Follow these steps to enable monitoring:

-   Select Infrastructure from the navigation bar.
-   Click the device name in the device list. The device overview page
    appears.
-   Expand Monitoring Templates, and then select Device from the left
    panel.
-   Select Bind Templates from the Action menu. The Bind Templates
    dialog appears.
-   Add the HttpMonitor template to the list of selected templates, and
    then click Submit.

The HttpMonitor template is added to the list of monitoring templates.
You can now begin collecting Web server metrics from the device.

## Check for a Specific URL or Specify Security Settings

-   Select Infrastructure from the navigation bar.
-   Click the device name in the device list. The device overview page
    appears.
-   Select the 'Gear' icon on the bottom panel and select the "Override
    Template Here" option.
-   Choose "HttpMonitor (/)" template and select "Submit". This will
    create a local copy of the default HttpMonitor template for only
    this device.
-   Select the newly created "HttpMonitor (Locally Defined)" template.
-   Select the HttpMonitor data source, and then select View and Edit
    Details from the Action menu. The Edit Data Source dialog appears.
-   Change data source options as needed, and then click Save.

## HttpMonitor Content Checking Data Source Options

<table data-border="2">
<colgroup>
<col />
<col />
</colgroup>
<thead>
<tr markdown="1">
<th>Option</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr markdown="1">
<td>Port</td>
<td>The port to connect to HTTP server (default <code>80</code>).</td>
</tr>
<tr markdown="1">
<td>Use SSL</td>
<td>Use SSL for the connection (default <code>False</code>).</td>
</tr>
<tr markdown="1">
<td>URL</td>
<td>Address of the web page (default <code>/</code>).</td>
</tr>
<tr markdown="1">
<td>Basic Auth User</td>
<td>If the website requires credentials, specify the username here (default <code>None</code>).</td>
</tr>
<tr markdown="1">
<td>Basic Auth Password</td>
<td>Password for the user (default <code>None</code>).</td>
</tr>
<tr markdown="1">
<td>Redirect Behavior</td>
<td>If the web site returns an HTTP redirect, should the probe follow the redirect or create an event? (default <code>follow</code>)<br />
<u>ok</u> - Do not follow the redirect and return a positive response<br />
<u>fail</u> - Do not follow the redirect and return a negative response<br />
<u>follow</u> - Follow redirection<br />
<u>stickyhost</u> - Use original hostname (or IP address) on redirect<br />
<u>stickyhostport</u> - Use original hostname and port on redirect</td>
</tr>
<tr markdown="1">
<td>Event class</td>
<td>(default /Status/HTTP)</td>
</tr>
</tbody>
</table>

## Tuning for Site Responsiveness

-   Select Infrastructure from the navigation bar.
-   Click the device name in the device list. The device overview page
    appears.
-   Select the 'Gear' icon on the bottom panel and select the "Override
    Template Here" option.
-   Choose "HttpMonitor (/)" template and select "Submit". This will
    create a local copy of the default HttpMonitor template for only
    this device.
-   Select the newly created "HttpMonitor (Locally Defined)" template.
-   Select the HttpMonitor data source, and then select View and Edit
    Details from the Action menu. The Edit Data Source dialog appears.
-   Change data source options as needed, and then click Save.

| Option               | Description                                                                |
|----------------------|----------------------------------------------------------------------------|
| Timeout (seconds)    | Seconds before connection times out (default: 60)                          |
| Cycle Time (seconds) | Number of seconds between collection cycles (default: 300 or five minutes) |

## Check for Specific Content on the Web Page

This procedure allows Zenoss platform to create an event if content at
the web page does not match the expected output.

-   Select Infrastructure from the navigation bar.
-   Click the device name in the device list. The device overview page
    appears.
-   Select the 'Gear' icon on the bottom panel and select the "Override
    Template Here" option.
-   Choose "HttpMonitor (/)" template and select "Submit". This will
    create a local copy of the default HttpMonitor template for only
    this device.
-   Select the newly created "HttpMonitor (Locally Defined)" template.
-   Select the HttpMonitor data source, and then select View and Edit
    Details from the Action menu. The Edit Data Source dialog appears.
-   Change data source options as needed, and then click Save.

**HttpMonitor Content Checking Data Source Options**

| Option             | Description                                                                                                                |
|--------------------|----------------------------------------------------------------------------------------------------------------------------|
| Regular Expression | A Python regular expression to match text in the web page.                                                                 |
| Case Sensitive     | Is the regular expression case-sensitive or not?                                                                           |
| Invert Expression  | If you would like to test to see if the web page does not contain content matched by a regular expression, check this box. |

## Configuration to Monitor HTTP Through a Proxy Server

Example configuration of HttpMonitor to check a website through a Proxy
Server when you have a proxy server with an IP address: 192.168.100.10
on port: 8080 and you have a device on /Devices/HTTP with a name
google.com

| Option                      | Example value                  |
|-----------------------------|--------------------------------|
| HostName                    | ${dev/id}                      |
| IP Address or Proxy Address | 192.168.100.10                 |
| Port                        | 8080                           |
| URL                         | /                              |
| Proxy User                  | (empty for if proxy anonymous) |
| Proxy Password              | (empty for if proxy anonymous) |

Example configuration of HttpMonitor to check a website through a Proxy
Server when you have a proxy server with an IP address: 192.168.100.10
on port: 8080 and you have a device on /Devices/HTTP with a name
google.com and HTTP port 8888

| Option                      | Example value              |
|-----------------------------|----------------------------|
| HostName                    | (empty)                    |
| IP Address or Proxy Address | 192.168.100.10             |
| Port                        | 8080                       |
| URL                         | http://google.com:8888/    |
| Proxy User                  | (empty if proxy anonymous) |
| Proxy Password              | (empty if proxy anonymous) |

Example configuration of HttpMonitor to check a website through a Proxy
Server when you have a proxy server with an IP address: 192.168.100.127
on port: 8080 and Username: proxy, Password: myproxypassword, and you
have a device on /Devices/HTTP with a name example.org and HTTP port
8888

| Option                      | Example value            |
|-----------------------------|--------------------------|
| HostName                    | (empty)                  |
| IP Address or Proxy Address | 192.168.100.127          |
| Port                        | 8080                     |
| URL                         | http://example.org:8081/ |
| Proxy User                  | proxy35                  |
| Proxy Password              | mypproxpassword          |

## Proxy usage logic

HttpMonitor uses the address in the `IP Address or Proxy Address` field
as a proxy server if the IP address for resolve in the field `URL` and
`Host Name` and `IP Address or Proxy Address` do not match

## Daemons

| Type                  | Name      |
|-----------------------|-----------|
| Performance Collector | zenpython |

## Changes

**3.1.2**

-   Improve compatibility with new Python libraries
-   Tested with Zenoss Cloud, Zenoss 6.6.0, Zenoss 6.7.0

**3.1.1**

-   Make use of value configured in Datasource "Component" field
    (ZPS-6133)
-   Tested with Zenoss Cloud, Zenoss 6.6.0, Zenoss 6.7.0

**3.1.0**

-   Fix infinity redirection in the case with not full URI path in
    header Location (ZPS-4904)
-   Fix issue when HttpMonitor doesn't check response and doesn't handle
    either (ZPS-4998)
-   Fix crashes of PythonCollector in the case with blank IP Address or
    Proxy Address fields (ZPS-4986)
-   Fix collection of datapoints for component-level datasources
    (ZPS-5550)
-   Provides details on Proxy usage with examples (ZPS-4912)
-   Tested with 6.3.2 and Zenoss Cloud

**3.0.4**

-   Fix issue with locally defined monitoring templates after upgrade
    (ZPS-3817)
-   Fix handles bad proxy hostnames (ZPS-3819)
-   Adds unittests for regular expression and redirect behavior
-   Adds **`Case sensitive/Invert Expression/Regular Expression`**
    properties into DataSource configuration (ZPS-3867)
-   Adds **`Redirect Behavior`** options
    **`ok/fail/follow/sticky/stickyport`** (ZPS-3867)
-   Tested with Zenoss Resource Manager 6.2.0, Zenoss Resource Manager
    5.3.3

**3.0.0**

-   Removes **`Case sensitive/Invert Expression/Regular Expressions`**
    zProperties from DataSource configuration
-   Changes **`Redirect Behavior`** list to checkbox
-   Removes dependency library **`check_http`** from Nagios Plugins
-   Adds unittests

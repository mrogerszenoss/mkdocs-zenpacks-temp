# Apache HTTP Server

@lb[](img/zenpack-apache-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.ApacheMonitor

### Applications Monitored:

Apache HTTP Server

## Apache HTTP Server ZenPack

This ZenPack provides performance monitoring of the Apache HTTP Server.

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Background

The ZenPacks.zenoss.ApacheMonitor ZenPack monitors Apache HTTP Server by
collecting metrics through the `mod_status` module.

The following metrics are collected and graphed for Apache HTTP Server.

-   Requests per Second
-   Throughput (Bytes/sec and Bytes/request)
-   CPU Utilization of the HTTP server and all worker processes or
    threads
-   Slot Usage (Open, Waiting, Reading Request, Sending Reply,
    Keep-Alive DNS Lookup, and Logging)

## Prerequisites

| Prerequisite      | Restriction                                           |
|-------------------|-------------------------------------------------------|
| Product           | Zenoss platform 4.x, Zenoss 5.x, Zenoss 2.2 or higher |
| Required ZenPacks | ZenPacks.zenoss.ApacheMonitor                         |

## Display the Status Page in Apache Version 1.3 or Higher

1.  On the Apache server, locate the httpd.conf file. Generally, this
    file is located at /etc/httpd/httpd.conf or
    /etc/httpd/conf/httpd.conf; however, other locations are possible
    depending on your operating system and setup. If you cannot locate
    the configuration file, use your system's search facilities to
    locate it. For Windows, use the Search button of the Windows
    Explorer tool. For Unix, try the following command:

    ```
    find / -name httpd.conf
    ```

2.  Check to see that the following line is not commented out and is
    available in httpd.conf or /etc/apache/modules.conf:

    ```
    LoadModule status_module /usr/lib/apache/1.3/mod_status.so
    ```

    !!! note
        You may have to search in alternate locations to find the
        mod_status.so file. Also, the syntax may differ depending on your
        configuration.

3.  Turn the ExtendedStatus option on in the httpd.conf file. This
    option is typically commented out. You can enable it by uncommenting
    it or ensuring that it is defined.

    ```
    #ExtendedStatus on
    ```

    becomes:

    ```
    ExtendedStatus on
    ```

4.  Enable the /server-status location in the httpd.conf file.
    Typically, this option exists but is commented out.

    ```
    #
    #    SetHandler server-status
    #    Order deny,allow
    #    Deny from all
    #    Allow from .example.com
    #
    ```

    becomes:

    ```
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from zenoss.example.com
    ```

    Note: Your Zenoss platform server or servers must be able to connect
    to your Apache server. Ensure that it is listed here or is part of
    the network specified in this chunk of configuration.

    To specify multiple servers, separate the entries with spaces. If
    you specify an IP address range rather than a destination, be sure
    to add a network mask to the end of the IP address range.

    The following example allows a server called
    externalzenoss.example.com, as well as all servers that start with
    192.168.10, in their addresses:

    ```
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from externalzenoss.example.com 192.168.10.0/24
    ```

5.  Save the httpd.conf file with these changes and verify that the
    configuration file is correct. This can be accomplished with
    following command.

    ```
    apachectl -t
    ```

    Correct any issues before restarting Apache.

6.  Restart the Web server (`httpd`). This can be accomplished with
    following command.

    ```
    apachectl restart
    ```

## Display the Status Page in Apache Version 2.x

1.  On the Apache server, find the httpd.conf file. This is usually
    /etc/apache2/apache2.conf or /etc/apache2/conf/httpd.conf; however,
    other locations are possible depending on your operating system and
    setup. If you are unsure about where your configuration file is
    located, use your system;s search facilities to locate this file.
    Under Windows, use the Search button of the Windows Explorer tool.
    Under Unix, try the following command:

    ```
    find / -name httpd.conf
    ```

2.  Verify that the `mod_status` module is loaded.

    ```
    apache% apachec2ctl -M 2<&1 | grep status
    status_module (shared)
    ```

    The previous output indicates that the module is loaded and no
    further configuration is necessary. If there is no output, then copy
    the mods-available/status.load to the mods-enabled directory, and
    then run:

    ```
    apache% /etc/init.d/apache2 force-reload
    ```

3.  Turn the ExtendedStatus option on in the httpd.conf file. This
    option is typically commented out. You can enable it by uncommenting
    it or ensuring that it is defined.

    ```
    #ExtendedStatus on
    ```

    becomes:

    ```
    ExtendedStatus on
    ```

4.  Enable the /server-status location in the httpd.conf file. This is
    another option that typically already exists but is commented out.

    ```
    #
    #    SetHandler server-status
    #    Order deny,allow
    #    Deny from all
    #    Allow from .example.com
    #
    ```

    becomes:

    ```
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from zenoss.example.com
    ```

    Note: Your Zenoss platform server or servers must be able to connect
    to your Apache server so you must ensure that it is either listed
    here or is a part of the network specified in this chunk of
    configuration.

    To specify multiple servers, separate the entries with spaces. If
    you would like to specify an IP address range rather than a
    destination, be sure to add a network mask to the end of the IP
    address range. The following example allows a server called
    externalzenoss.example.com as well as all servers that start with
    '192.168.10' in their addresses:

    ```
    SetHandler server-status
    Order deny,allowDeny from all
    Allow from externalzenoss.example.com 192.168.10.0/24
    ```

5.  Save the httpd.conf file with these changes and verify that the
    configuration file is correct. This can be accomplished with
    following command.

    ```
    apache2ctl -t
    ```

    Correct any issues before restarting Apache.

6.  Restart the webserver (`httpd`). This can be accomplished with
    following command.
    ```
    apache2ctl restart
    ``` 

## Verifying Your Apache Configuration

Once Apache has been configured, you should verify that it is working
correctly. To verify your Apache server, point your Web browser to your
Apache server at the appropriately modified URL:

`http://your-apache-server/server-status?auto`

This is an example of what you might see:

```
Total Accesses: 1
Total kBytes: 2
Uptime: 43
ReqPerSec: .0232558
BytesPerSec: 47.6279
BytesPerReq: 2048
BusyWorkers: 1
IdleWorkers: 5
Scoreboard: _W____................................
```

If there is a configuration issue, you should see an error message
telling you that the page is forbidden.

Note: Your Zenoss platform server or servers must be able to connect to
your Apache server by using HTTP to receive information. This means that
the Zenoss platform server must be permitted not only by the Apache
configuration settings, but also by any firewalls or proxies between the
Zenoss platform server and the Apache server, including any firewall on
the Apache server. If there are any proxies, they must be configured to
allow the Zenoss platform HTTP traffic through. Consult your network
administrator and security officer to verify the firewall configuration
and your site's policies.

Further note that the name or IP address that your server has behind a
firewall may be different than the IP address (some form of Network
Address Translation (NAT)) or name resolution (the way that the external
server resolves names may be through an Internet-visible DNS system
rather than an intranet-only DNS system).

## Configure Zenoss platform to Monitor the Web Server

Once the Apache server is configured to allow Zenoss platform to access
the extended status, you can add Apache monitoring to the device within
Zenoss platform by binding the Apache template to the device.

1.  Select Infrastructure from the navigation bar.
2.  Click the device name in the device list. The device overview page
    appears.
3.  In the left panel, expand Monitoring Templates, and then select
    Device.
4.  Select Bind Templates from the Action menu. The Bind Templates
    dialog appears.
5.  Add the Apache template to the list of templates, and then click
    **Save**. The Apache template is added. The system can now begin
    collecting the Apache server metrics from this device.

## Daemons

| Type                  | Name       |
|-----------------------|------------|
| Performance Collector | zencommand |

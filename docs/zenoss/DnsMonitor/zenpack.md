# DNS Monitor

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.DnsMonitor

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-3511){.external-link}

## DNS Monitor ZenPack

This ZenPack provides status and response time monitoring of resolution
against DNS servers.

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Background

The ZenPacks.zenoss.DnsMonitor ZenPack monitors the response time of DNS
requests.

This ZenPack uses the check_dns Nagios plugin to collect data, which in
turn uses the nslookup command.

## Prerequisites

| Prerequisite      | Restriction                |
|-------------------|----------------------------|
| Product           | Zenoss platform 4.2.x, 5.x |
| Required ZenPacks | ZenPacks.zenoss.DNSMonitor |

## Enable Monitoring

To enable monitoring by the system:

1.  Select Infrastructure from the navigation bar.
2.  Click the device name in the device list. The device overview page
    appears.
3.  Expand Monitoring Templates in the left panel, and then select
    Device.
4.  Select Bind Templates from the Action menu. The Bind Templates
    dialog appears.
5.  Add the DNSMonitor template to the list of selected templates, and
    then click **OK**. The DNSMonitor template appears under Monitoring
    Templates.
6.  Select the DNSMonitor template in the left panel, and change options
    as needed.

    DNSMonitor Data Source Options

    | Option              |Description                                          |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|    
    | DNS Server          | Name server against which the nslookup command should be run. If empty (the default), the default DNS server or servers in /etc/resolve.conf are used. |
    | Port                | Port on which the name server is listening. This is normally port 53.                                                                                  |
    | Host Name           | Host name to resolve. The default is the device ID.                                                                                                    |
    | Expected IP Address | IP address to which the host name is expected to resolve.                                                                                              |

## Daemons

| Type                  | Name       |
|-----------------------|------------|
| Performance Collector | zencommand |

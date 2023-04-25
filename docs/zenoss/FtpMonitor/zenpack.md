# FTP Monitor

@lb[](img/zenpack-zenpack-general.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.Zenoss.FtpMonitor

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.FtpMonitor){.external-link}

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-3446){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.FtpMonitor.git){.external-link}

### Applications Monitored:

FTP

## FTP Monitor ZenPack

The FTPMonitor ZenPack monitors connection response time to an FTP
server.

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Background

The ZenPacks.zenoss.FtpMonitor ZenPack monitors the response times of
File Transfer Protocol (FTP) server connection requests.

## Prerequisites

|                   |                            |
|-------------------|----------------------------|
| Prerequisite      | Restriction                |
| Product           | Zenoss platform 4.2.x, 5.x |
| Required ZenPacks | ZenPacks.zenoss.FtpMonitor |

## Enable Monitoring

To enable monitoring of the device:

1.  Select Infrastructure from the navigation bar.
2.  Click the device name in the device list. The device overview page
    appears.
3.  Expand Monitoring Templates in the left panel, and then select
    Device.
4.  Select Bind Templates from the Action menu. The Bind Templates
    dialog appears.
5.  Select the FTPMonitor template and move it to the list of selected
    templates.
6.  Click **Save**. The FTPMonitor template appears under Monitoring
    Templates.
7.  Select the FTPMonitor template and change options as needed.

    FTPMonitor Basic Data Source Options
    |               |                                                                                                                                                            |
    |---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Option        | Description                                                                                                                                                |
    | Port          | The port to connect to FTP server (default 21)                                                                                                             |
    | Send String   | Command string to send to the server                                                                                                                       |
    | Expect String | A string to expect in server response                                                                                                                      |
    | Mismatch      | If the expected string does not match the string returned from the remote server, create an event with one of these states: ok, warn, crit (default: warn) |
    | Quit String   | Command to send to the remote server to end the session                                                                                                    |

## Enable Secure Site Monitoring

To enable secure site monitoring:

1.  Select Infrastructure from the navigation bar.
2.  Click the device name in the devices list. The device overview page
    appears.
3.  Expand Monitoring Templates in the left panel.
4.  Select the FTPMonitor template and change options as needed.

    FTPMonitor Secure Data Source Options
    |             |                                                 |
    |-------------|-------------------------------------------------|
    | Option      | Description                                     |
    | Port        | The port to connect to FTP server (default 21). |
    | Certificate | Minimum days for which a certificate is valid   |
    | Use SSL     | Use SSL for the connection                      |

## Tuning for Site Responsiveness

1.  Select Infrastructure from the navigation bar.
2.  Click the device name in the devices list. The device overview page
    appears.
3.  Expand Monitoring Templates in the left panel.
4.  Select the FTPMonitor template and change options as needed.

    FTPMonitor Tunables Data Source Options
    |                                  |                                                                                                                                                                                   |
    |----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Option                           | Description                                                                                                                                                                       |
    | Timeout                          | Seconds before connection times out (default: 60)                                                                                                                                 |
    | Refuse                           | If a TCP/IP connection to the remote service is refused (ie no program is listening at that port) send an event with one of these severity states: ok, warn, crit (default: crit) |
    | Max Bytes                        | Close the connection once more than this number of bytes are received.                                                                                                            |
    | Delay                            | Seconds to wait between sending string and polling for response                                                                                                                   |
    | Warning response time (seconds)  | Response time to result in a warning status.                                                                                                                                      |
    | Critical response time (seconds) | Response time to result in critical status                                                                                                                                        |

## Daemons

|                       |            |
|-----------------------|------------|
| Type                  | Name       |
| Performance Collector | zencommand |

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


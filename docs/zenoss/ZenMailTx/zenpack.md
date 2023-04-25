# Mail Transactions

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.ZenMailTx

## Mail Transactions ZenPack

The ZenMailTx ZenPack allows you to monitor round-trip email delivery.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.ZenMailTx ZenPack allows you to monitor round-trip
email delivery.

## Events

There are several situations in which this ZenPack creates events. The
component will be `zenmailtx`, the eventGroup will be `mail` and the
eventClass will be /Status. These situations are:

-   The SMTP server name or the POP server name cannot be resolved.
-   The SMTP server or the POP server is down or unavailable.
-   The timeout (specified on the Data Source tab) is exceeded for the
    SMTP or POP server.
-   Authentication (if specified) with the SMTP or POP server fails.
-   A threshold defined for one of the data points in this data source
    is exceeded. Thresholds are defined in the monitoring template that
    contains the data source.

Once an email has successfully made a trip back and forth, a clear event
is created that clears any failure events.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.2 or higher |
| Required ZenPacks | ZenPacks.zenoss.ZenMailTx                 |

## Enable Monitoring

1.  Click the device in the device list.

2.  From the left panel, select the Device template under Monitoring
    Templates.

3.  Select Add Local Template from the Action menu.

4.  Enter an identifier for the template (such as ZenMailTx), and then
    click **Submit** to create the template.

5.  Click the newly created ZenMailTx template.

6.  In the Data Sources area, click Add to add a data source.

7.  Enter a name for the data source (MailTx), select MAILTX as the
    type, and then click **Submit**.

8.  Change options as needed.

    Mail Transactions Basic Data Source Options
    |              |                                                                                |
    |--------------|--------------------------------------------------------------------------------|
    | Option       | Description                                                                    |
    | To Address   | The recipient e-mail address. This should be the same as the POP Username.     |
    | From Address | The e-mail address that will appear in the From: field in the generated e-mail |
    | SMTP Host    | The e-mail server used by Zenoss platform to send the email                    |
    | POP Host     | The email server where you will retrieve your test message                     |

    Tip: Any of the `MAILTX fields` can take TAL expressions, including
    the password fields.

9.  Click Save to save your changes.

10. Navigate to Graphs and you should see some place holders for graphs.
    After approximately fifteen minutes you should see the graphs begin
    populating with information.

## Daemons

|                       |           |
|-----------------------|-----------|
| Type                  | Name      |
| Performance Collector | zenmailtx |

## Managing the Collector Daemon

The zenmailtx daemon:

-   Sends the test email message via the specified SMTP server
-   Retrieves the email message from the specified POP server
-   Sends the following information to Zenoss platform:
    -   Time taken to send
    -   Time taken to fetch
    -   Total time

This daemon appears on the Zenoss platform Daemons page and can be
started, stopped and restarted from there.

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


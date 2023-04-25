# LDAP Monitor (Core)

@lb[](img/zenpack-zenpack-general.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.LDAPMonitor

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-3422){.external-link}

## LDAP Monitor (Core) ZenPack

LDAPMonitor monitors the response time of an LDAP server (in
milliseconds).

## Support

This ZenPack is part of Zenoss Core. Open Source users receive community
support for this ZenPack via our online forums. Enterprise support for
this ZenPack is provided to Zenoss customers with an active
subscription.

## Background

The ZenPacks.zenoss.LDAPMonitor ZenPack monitors the response time of
Lightweight Directory Access Protocol (LDAP) servers.

The response time unit of measurement is milliseconds.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.2 or higher |
| Required ZenPacks | ZenPacks.zenoss.LDAPMonitor               |

## Enable monitoring for a device

Note: The LDAPServer template must be bound to the device class or
device you want to monitor.

1.  Select Infrastructure from the navigation bar.

2.  Click the device name in the device list. The device overview page
    appears.

3.  Select Configuration Properties from the left panel.

4.  Modify configuration property values as needed for your environment.
    Check with your LDAP administrator for more information.

    LDAPServer Configuration Properties
    |                   |                                                                                                                                      |
    |-------------------|--------------------------------------------------------------------------------------------------------------------------------------|
    | Property          | Description                                                                                                                          |
    | zLDAPBaseDN       | The Base Distinguished Name for your LDAP server. Typically this is the organization's domain name (for example, `dc=foobar,dc=com)` |
    | zLDAPBindDN       | The Distinguished Name to use for binding to the LDAP server, if authentication is required                                          |
    | zLDAPBindPassword | The password to use for binding to the LDAP server, if authentication is required                                                    |

5.  Click **Save**.

6.  Expand Monitoring Templates, and then select Device from the left
    panel.

7.  Select Bind Templates from the Action menu. The Bind Templates
    dialog appears.

8.  Add the LDAPServer template to the list of selected templates, and
    then click **Submit**. The LDAPServer template is added to the list
    of monitoring templates.

9.  Select the LDAPServer template and change options as needed.

    LDAPServer Basic Data Source Options
    |                         |                                                  |
    |-------------------------|--------------------------------------------------|
    | Option                  | Description                                      |
    | Port                    | The port to connect to LDAP server (default 389) |
    | Base Distinguished Name | Defaults to `${here/zLDAPBaseDN}`                |
    | Bind Password           | Defaults to `${here/zLDAPBindPassword}`          |
    | Use SSL                 | Use SSL for the connection                       |

    Note: If your LDAP servers require SSL or a custom port, select the
    ldap data source, and then change the Use SSL and Port fields as
    needed.

10. Validate your configuration by running zencommand. Verify that the
    check_ldap or check_ldaps command correctly connects to your LDAP
    server:

        zencommand run -v10 -d yourdevicenamehere

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
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


# MS SQL Database Monitor

@lb[](img/zenpack-microsoft-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Egor Puzanov

### Maintainers:

Egor Puzanov

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.community.MsSQLMon

### More Information:

[GitHub page/HomePage](http://community.zenoss.org/docs/DOC-3391){.external-link}

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-3391){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/epuzanov/ZenPacks.community.MsSQLMon.git){.external-link}

### Applications Monitored:

MS SQL (Multiple)

## MS SQL Database Monitor ZenPack

This ZenPack provides monitoring of MS SQL databases.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 3.3- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.MsSQLMon/3.3/ZenPacks.community.MsSQLMon-3.3.egg){.external-link}:   **Summary of changes:** fix sysperfinfo query and modeler plugin:   Requires [RDBMS Monitoring ZenPack](https://help.zenoss.com/display/in/RDBMS+Monitoring "ZenPack:RDBMS Monitoring"){.external-link},[SQL Data Source ZenPack](https://help.zenoss.com/display/in/SQL+Data+Source "ZenPack:SQL Data Source"){.external-link}:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.2.x

<!-- -->

Version 3.2- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.MsSQLMon/3.2/ZenPacks.community.MsSQLMon-3.2.egg){.external-link}:   **Summary of changes:** switch from ODBC data source to SQL data
    source:   Requires [RDBMS Monitoring ZenPack](https://help.zenoss.com/display/in/RDBMS+Monitoring "ZenPack:RDBMS Monitoring"){.external-link},[SQL Data Source ZenPack](https://help.zenoss.com/display/in/SQL+Data+Source "ZenPack:SQL Data Source"){.external-link}:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.2.x

<!-- -->

Version 3.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.MsSQLMon/3.1/ZenPacks.community.MsSQLMon-3.1.egg){.external-link}:   **Summary of changes:** zMsSqlConnectionString (UID, PWD and SERVER
    options) overrides zWinUser, zWinPassword and manageIp values by
    modeling:   Requires [RDBMS Monitoring ZenPack](https://help.zenoss.com/display/in/RDBMS+Monitoring "ZenPack:RDBMS Monitoring"){.external-link},[SQL Data Source ZenPack](https://help.zenoss.com/display/in/SQL+Data+Source "ZenPack:SQL Data Source"){.external-link}:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.2.x

## Background

This ZenPack provides monitoring of MS SQL databases. There are
**MsSqlDatabase** and **MsSqlSrvInst** database component templates and
a **community.sql.MsSqlDatabaseMap** zCollectorPlugin that the device
will need to use. Use **zMsSqlSrvInstances** zProperty to specify list
of MS SQL Server Instances.

## Attachments:

-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)
-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)
-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)


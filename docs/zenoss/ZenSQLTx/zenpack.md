# SQL Transactions

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Name:

ZenPacks.zenoss.ZenSQLTx

### Applications Monitored:

MySQL

Sybase

Microsoft SQL Server

## SQL Transactions ZenPack

The ZenSQLTx ZenPack allows you to test the availability and performance
of MySQL, Sybase and Microsoft SQL servers. It provides a SQL data
source where user-defined SQL queries can be executed against a
database.


## Releases

Version 2.7.2 - [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2023/01/17:   Compatible with Zenoss Resource Manager 6.x and Zenoss Cloud

## Usage

### Enable SQL Server Monitoring

Ensure that your Microsoft SQL Server authentication mode is set to "SQL
Server and Windows Authentication mode". For more information about this
setting and how to change it, refer to [MSDN Documentation: Change Server Authentication Mode](http://msdn.microsoft.com/en-us/library/ms188670.aspx){.external-link}.

1.  Click the device in the device list.

2.  Select Device under Monitoring Templates in the left panel.

3.  Select Add Local Template from the Action menu.

4.  Enter the name of the template, and then click *Submit*.

5.  Click the newly created template in the left panel.

6.  In the Data Sources area, click Add.

7.  Enter a name for the data source, select *SQL* as the type, and then
    click *Submit*.

8.  Double-click the newly created data source.

9.  Change options as needed.

    | Option        | Description                                                                                                                                           |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|    
    | Database Type | Enter *MS SQL*                                                                                                                                        |
    | Host Name     | Set the hostname on which the database is located. This field accepts a TALES expression, such as `${here/id}` or `${here/getManageIp}`               |
    | Port          | Set the port on which the database server is listening. If you don't specify a port number, then the default port for the database is used.           |
    | Database Name | Specify the name of the database (required).                                                                                                          |
    | User          | Specify a user name with permission to connect to the database and run queries.                                                                       |
    | Password      | Specify the user password.                                                                                                                            |
    | SQL Queries   | Specify the SQL queries that this data source should execute. A summary of MS SQL syntax is available in the documentation accompanying the software. |

10. Click *Save* to save your changes.

11. Click *Test* to verify that the database connection can be completed
    and that the data returned from the queries are correct.

### Enable Sybase Server Monitoring

1.  Click the device in the device list.

2.  Select Device under Monitoring Templates in the left panel.

3.  Select Add Local Template from the Action menu.

4.  Enter the name of the template, and then click *Submit*.

5.  Click the newly created template in the left panel.

6.  In the Data Sources area, click Add.

7.  Enter a name for the data source, select *SQL* as the type, and then
    click *Submit*.

8.  Double-click the newly created data source.

9.  Change options as needed.

    | Option        | Description                                                                                                                                                                                             |
    |---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|    
    | Database Type | Enter *Sybase*                                                                                                                                                                                          |
    | Host Name     | Set the hostname on which the database is located. This field accepts a TALES expression, such as `${here/id}` or `${here/getManageIp}`                                                                 |
    | Port          | Set the port on which the database server is listening. If you don't specify a port number, then the default port for the database is used.                                                             |
    | Database Name | Specify the name of the database (required).                                                                                                                                                            |
    | User          | Specify a user name with permission to connect to the database and run queries.                                                                                                                         |
    | Password      | Specify the user password.                                                                                                                                                                              |
    | SQL Queries   | Specify the SQL queries that this data source should execute. A summary of Sybase syntax is available at the [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp){.external-link} Web site. |

10. Click on the *Save* button to save your changes.

11. Click *Test* to verify that the database connection can be completed
    and that the data returned from the queries are correct.

### Enable MySQL Server Monitoring

1.  Click the device in the device list.

2.  Select Device under Monitoring Templates in the left panel.

3.  Select Add Local Template from the Action menu.

4.  Enter the name of the template, and then click *Submit*.

5.  Click the newly created template in the left panel.

6.  In the Data Sources area, click Add.

7.  Enter a name for the data source, select *SQL* as the type, and then
    click *Submit*.

8.  Double-click the newly created data source.

9.  Change options as needed.

    | Option        | Description                                                                                                                                                                                                    |
    |---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Database Type | Enter *MySQL*                                                                                                                                                                                                  |
    | Host Name     | Set the hostname on which the database is located. This field accepts a TALES expression, such as `${here/id}` or `${here/getManageIp}`                                                                        |
    | Port          | Set the port on which the database server is listening. If you don't specify a port number, then the default port for the database is used.                                                                    |
    | Database Name | Specify the name of the database (required).                                                                                                                                                                   |
    | User          | Specify a user name with permission to connect to the database and run queries.                                                                                                                                |
    | Password      | Specify the user password.                                                                                                                                                                                     |
    | SQL Queries   | Specify the SQL queries that this data source should execute. A summary of MySQL syntax is available at: [MySQL SQL Statement Syntax](https://dev.mysql.com/doc/refman/5.7/en/sql-syntax.html){.external-link} |

10. Click on the Save button
    to save your changes.

11. Click *Test* to verify that the database connection can be completed
    and that the data returned from the queries are correct.

### Storing Query Results

If any data is retrieved from the database that can be interpreted as a
number, that number can be used as a data point. In select statements in
which a column name is used, that column name becomes the name of the
data point. In select statements in which no column name is specified
(for example, aggregate functions such as `count(*)`, `sum()`, or
`min()`), the data point name returned is database-dependent:

-   **MySQL**: The column name can be controlled with an 'AS' clause in
    the query. If used, then the column name is the "cleaned up" result
    of the 'AS' clause; otherwise, it uses the format: 'q' + query
    number (beginning with 0) + '\_' + column number in the query
    (beginning with 0).
-   **Other Databases**: The column name uses the format: 'q' + query
    number (beginning with 0) + '\_' + column number in the query
    (beginning with 0).

Non-alphanumeric characters (\[^za-zA-Z0-9\_\]) are removed from the
column name to produce the data point name. Any query results that
cannot be interpreted as a number are ignored, and the query numbers
will not change.

For example, the queries:

     select count(*) from Users;select UserName from Users; select count(*) * 4 from Users

Returns these results:

     Queries completed successfully. | totalTime=2.13289260864 count=3.0 count4=12.0

**Note**: To use multiple queries (such as in the preceding example),
they must be separated with a semicolon.

This example demonstrates multiple results from a single query:

     select count(*) as count1, count(*)-1001 from history;

Returns these results:

     Queries completed successfully. | totalTime=72.6099014282 count1=99894.0 count1001=98893.0

Notes:

-   For SQL Server, use the format `q*_*` if no column name is found.
-   The SQL 'as' renaming capability can be used to control the name of
    the data point.

## Troubleshooting

To verify any queries, as well as any permissions or authentication
issues, run the `zensql.py` command from the command line. Here's an
example against the MySQL database on a Zenoss server:

     cd $ZENHOME/ZenPacks/*ZenSQLTx*/Z*/z*/Z* ./zensql.py -t mysql -H localhost -u zenoss -p zenoss -d events 'select \* from events.log;' Queries completed successfully. | totalTime=54.5899868011

**Note**: Single quotes (') are required around the SQL statement. Any
wild card characters (such as \*) must be escaped, as shown in the
previous example.

For the *zensql.py* command, the database types understood are shown in
the following table.

| Name   | Database Type |
|--------|---------------|
| mssql  | MS SQL Server |
| sybase | Sybase        |
| mysql  | MySQL Server  |

## Caveats

### GLIBC Version Error on Zenoss 4.x

When Sybase database type is used in a ZenSQLTx datasource, the
following error \`/lib64/libc.so.6: version \`GLIBC_2.14' not found\`
might be observed in zencommand log files or when you're trying to test
the datasource on the UI. It happens because your current GNU C Library
version is lower than the required version.

To check the currently installed GNU C Library version on your Zenoss
instance use `ldd --version` command.

You cannot update the GNU C Library on a Zenoss instance safely,
therefore, the Sybase database monitoring is not supported on Zenoss
4.x.

## Services

The following Zenoss services are required to be running by this
ZenPack.

| Type                  | Name       |
|-----------------------|------------|
| Performance Collector | zencommand |

## Supported Databases

The following databases are officially supported. Other databases may
also be supported, especially derivatives of MS SQL, MySQL and Sybase.

| Type                                 | Version |
|--------------------------------------|---------|
| Microsoft SQL Server                 | 2016    |
| Microsoft SQL Server                 | 2019    |
| MySQL Community Server               | 5.7.19  |
| SAP ASE (Adaptive Server Enterprise) | 15      |
| SAP ASE (Adaptive Server Enterprise) | 16      |

## Changes

**2.7.2**

-   Add encrypted server connection support for MSSQL Server 2019
    (ZPS-5518)
-   Fix SQL Data Source password exposing in the traceback (ZPS-7545)
-   Fix the test button on SQL datasource when a domain user is used
    (ZPS-3291)
-   Tested with Zenoss Resource Manager 6.7.0 and Zenoss Cloud.

**2.7.1**

-   Fix an error when cycle time in ZenSQLTx Data Source is empty
    (ZEN-29196)

**2.7.0**

-   Add the "Caveat" section to the documentation and update it with the
    "GLIBC Version Error on Zenoss 4.x" topic (ZPS-2209)
-   The timeout parameter doesn't cause Sybase calls to fail (ZPS-2196)
-   Add cycle time to ZenSQLTx Data Source (ZPS-2119)
-   Change ZenSQLDataSource password type and hide the password on
    Zenoss UI for security (ZPS-2133)
-   Fix monitoring of MSSQL databases (ZPS-1826)
-   Fix broken ZenSQLTx monitoring (ZPS-1657)
-   Fix monitoring of Sybase databases (ZPS-513)
-   Tested with Zenoss Resource Manager 5.3.2 and Zenoss Resource
    Manager 4.2.5 RPS 743

**2.6.6**

-   Fix SQL datasource test to test from an appropriate collector
    (ZEN-22199)

**2.6.5**

-   Fix the traceback associated with errorLog (ZEN-24736)

**2.6.4**

-   Fix the broken "timeout" field in SQL datasource edit dialog
    (ZEN-22955)
-   Make SQL libraries importable by other ZenPacks (ZEN-23722)

**2.6.3**

-   Added support for Zenoss 5.x
-   Fixed issue with not secure password on monitoring template

# SAP HANA Integration Service

@lb[](img/zenpack-sap-logo.png)

## Subscription

This integration is a subscription-based Professional Services
engagement. Our Integration Services are offered as subscriptions in
order to provide initial setup and ongoing compatibility and
maintenance. All standard packages are renewable every 12 months from
the date of purchase. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks.

### Authors:

Zenoss Inc.

### Maintainers:

Zenoss Inc.

### Organization:

Zenoss Inc.

### Name:

SAP HANA Integration Service

### Link To More Docs:

## SAP HANA Integration Service

This service provides modeling and monitoring of SAP HANA instances
within the Zenoss software platform. It is an annual subscription
service renewable every 12 months from the date of purchase and is
designed to offer ongoing compatibility between the platforms as
described below.

**Features:**

-   A new device class \`\`/Devices/HANA\`\` is added to the system.
-   The following components are modeled and monitored:
    -   HANA Endpoint(the HANA system as a whole)
    -   HANA Hosts
    -   HANA Disks
    -   HANA Services
-   Endpoint Data Sources are included to provide the following
    information:
    -   Count of the number of current connections to HANA
    -   Create Zenoss events from HANA Alerts
    -   Ability to run a generic query with results stored and available
        for threshold
    -   Current memory usage and limit for licensing purposes
    -   Ability to capture/measure the response time of generic SQL
        query
    -   Ability to monitor and alert on Nameserver or Indexserver role
        changes
    -   Ability to count the number of currently running queries
-   Host Data Sources
    -   All metrics from the M_HOST_RESOURCE_UTILIZATION table
-   Disk Data Sources
    -   Ability to store and threshold on disk total and used sizes
-   Service Data Sources
    -   Measure Heap utilization of a service
    -   All metrics from the M_SERVICE_MEMORY table
    -   All metrics from the M_SERVICE_STATISTICS table

**Prerequisites:**

<table data-align="left" data-border="0" data-cellpadding="1" data-cellspacing="1">
<colgroup>
<col />
<col />
<col />
</colgroup>
<thead>
<tr markdown="1">
<th scope="row">PREREQUISITE</th>
<th scope="col">RESTRICTION</th>
<th scope="col">MIN. VERSION</th>
</tr>
</thead>
<tbody>
<tr markdown="1">
<th scope="row">Product</th>
<td>Zenoss Resource Manager</td>
<td>4.2.4</td>
</tr>
<tr markdown="1">
<th scope="row"><br />
</th>
<td>Zenoss Analytics</td>
<td>4.3.0</td>
</tr>
<tr markdown="1">
<th scope="row"><br />
</th>
<td>Zenoss Service Impact</td>
<td>4.2.6</td>
</tr>
<tr markdown="1">
<th scope="row">ZenPacks</th>
<td>ZenPacks.zenoss.PythonCollector</td>
<td>1.4.0</td>
</tr>
<tr markdown="1">
<th scope="row"><br />
</th>
<td>ZenPacks.zenoss.CalculatedPerformance</td>
<td>2.0.1</td>
</tr>
<tr markdown="1">
<th scope="row">Other Dependencies</th>
<td>unixODBC.x86_64</td>
<td>2.0.1</td>
</tr>
<tr markdown="1">
<th scope="row"><br />
</th>
<td>Installed SAP ODBC driver***</td>
<td><br />
</td>
</tr>
</tbody>
</table>

*\*\*\*NOTE: This ZenPack uses ODBC to connect to the HANA instance.
Therefore, each collector collecting for HANA systems must have the
unixODBC package installed as well as the SAP HANA ODBC driver
(libodbcHDB.so). Additionally, /etc/odbc.ini must be configured with the
location of the library and a DSN.*

## Deliverable 1 - Zenoss SAP HANA ZenPack

Zenoss will install, set up and configure the Zenoss SAP HANA ZenPack.
This effort will be performed with client staff to provide knowledge
transfer and acceptance review.

*NOTE: Any requested modifications to the ZenPack code will require a
development SOW.*

## Acceptance 1 - SAP HANA ZenPack

-   The ZenPack is installed
-   A user is able to add a HANA endpoint
-   A user is able to see the new device in Infrastructure /devices/HANA
-   A user is able to see that components are created after modeling has
    run
-   A user is able to see the monitored data in graphs
-   A user is able to create and modify a threshold against monitored
    data
-   A user is able add the HANA endpoint to an Impact service\*
-   A user is able to see HANA data in Analytics\*\*

*\*Requires client to have Zenoss Impact installed and running
\*\*Requires client to have Zenoss Analytics installed and running*

## Attachments:

-   [SAP-Logo.png](img/zenpack-sap-logo.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/HANA/zenoss-integration-services-ds.pdf){.external-link}
-   [SAP-Logo.png](img/zenpack-sap-logo.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/HANA/zenoss-integration-services-ds.pdf){.external-link}
-   [SAP-Logo.png](img/zenpack-sap-logo.png)
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/HANA/zenoss-integration-services-ds.pdf){.external-link}
-   [zenoss-integration-services-ds.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/HANA/zenoss-integration-services-ds.pdf){.external-link}


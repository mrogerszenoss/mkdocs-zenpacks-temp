# Microsoft Exchange

@lb[](img/zenpack-microsoft-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.Microsoft.Exchange

## Releases

Version 1.1.2- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2019/01/17:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},
    [ZenPackLib ZenPack](https://help.zenoss.com/display/in/ZenPackLib "ZenPack:ZenPackLib"){.external-link},
    [Microsoft Windows ZenPack](https://help.zenoss.com/display/in/Microsoft+Windows "ZenPack:MicrosoftWindows"){.external-link}:   Compatible with Zenoss Resource Manager 6.x and Zenoss Cloud

Version 1.0.6- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2016/07/13:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},
    [ZenPackLib ZenPack](https://help.zenoss.com/display/in/ZenPackLib "ZenPack:ZenPackLib"){.external-link},
    [Microsoft Windows ZenPack](https://help.zenoss.com/display/in/Microsoft+Windows "ZenPack:MicrosoftWindows"){.external-link}:   Compatible with Zenoss Core 4.2.5, Zenoss Core 5.0.x, Zenoss Core
    5.1.x, Zenoss Core 5.2.x, Zenoss Resource Manager 4.2.5, Zenoss
    Resource Manager 5.0.x, Zenoss Resource Manager 5.1.x, Zenoss
    Resource Manager 5.2.x

## Microsoft Exchange ZenPack

Monitoring for Microsoft Exchange Server Devices.

## Contents

[1 Releases](#releases)

[1 Microsoft Exchange ZenPack](#microsoft-exchange-zenpack)

[1.1 Background](#background)

[1.2 Features](#features)

[1.2.1 Discovery](#discovery)

[1.2.2 Performance Monitoring](#performance-monitoring)

[2 Thresholds](#thresholds)

[2.1 Usage](#usage)

[2.1.1 Configuration Options](#configuration-options)

[2.2 Limitations of Current Release](#limitations-of-current-release)

[2.3 Troubleshooting](#troubleshooting)

[2.4 Zenoss Analytics](#zenoss-analytics)

[2.4.1 Domains](#domains)

[2.5 Service Impact](#service-impact)

[2.6 Installed Items](#installed-items)

[2.7 Changes](#changes)

## Background

This ZenPack provides support for monitoring Microsoft Exchange Server.
Monitoring is performed using the Windows Remote Management (WinRM) to
collect Perfmon data.

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Discovery of Exchange components
-   Performance monitoring
-   Service monitoring

### Discovery

The following components will be automatically discovered through the
Windows server address, username and password you provide. The
properties and relationships will be periodically updated by modeling.

Exchange Server:   **Attributes:** Name, Version, Is Client Access Role, Is Mailbox
    Role, Is Hub Transport Role:   **Relationships:** Mailbox Databases

Mailbox Database:   **Attributes:** Name, Is Mailbox Database, Is Public Folder Database:   **Relationships:** Exchange Server

### Performance Monitoring

Performance counters are collected using the PowerShell Get-Counter
Cmdlet within a remote shell (WinRS). The following metrics will be
collected every 5 minutes by default. Any other Windows Perfmon counters
can also be collected by adding them to the appropriate monitoring
template.

ClientAccessRole:   \\ASP.NET\\Application Restarts:   \\ASP.NET\\Request Wait Time:   \\ASP.NET\\Worker Process Restarts:   \\MSExchangeAB\\NSPI Connections Current:   \\MSExchangeAB\\NSPI Connections/sec:   \\MSExchangeAB\\NSPI RPC Browse Requests Average Latency:   \\MSExchangeAB\\NSPI RPC Requests Average Latency:   \\MSExchangeAB\\NSPI RPC Requests/sec:   \\MSExchangeAB\\Referral RPC Requests Average Latency:   \\MSExchangeAB\\Referral RPC Requests/sec:   \\MSExchangeAutodiscover\\Requests/sec:   \\MSExchange Availability Service\\Availability Requests (sec):   \\MSExchange Availability Service\\Average Time to Process a Free
    Busy Request:   \\MSExchange ActiveSync\\Current Requests:   \\MSExchange ActiveSync\\Ping Commands Pending:   \\MSExchange ActiveSync\\Requests/sec:   \\MSExchange ActiveSync\\Sync Commands Pending:   \\MSExchange ActiveSync\\Sync Commands/sec:   \\MSExchange Control Panel\\ASP.Net Request Failures/sec:   \\MSExchange Control Panel\\Explicit Sign-On Inbound Proxy
    Requests/sec:   \\MSExchange Control Panel\\Explicit Sign-On Inbound Proxy
    Sessions/sec:   \\MSExchange Control Panel\\Explicit Sign-On Outbound Proxy
    Requests/sec:   \\MSExchange Control Panel\\Explicit Sign-On Outbound Proxy
    Sessions/sec:   \\MSExchange Control Panel\\Explicit Sign-On Standard RBAC
    Requests/sec:   \\MSExchange Control Panel\\Explicit Sign-On Standard RBAC
    Sessions/sec:   \\MSExchange Control Panel\\Inbound Proxy Requests/sec:   \\MSExchange Control Panel\\Inbound Proxy Sessions/sec:   \\MSExchange Control Panel\\Outbound Proxy Requests/sec:   \\MSExchange Control Panel\\Outbound Proxy Requests - Average
    Response Time:   \\MSExchange Control Panel\\Outbound Proxy Sessions/sec:   \\MSExchange Control Panel\\PowerShell Runspaces - Activations/sec:   \\MSExchange Control Panel\\PowerShell Runspaces - Average Active
    Time:   \\MSExchange Control Panel\\PowerShell Runspaces/sec:   \\MSExchange Control Panel\\RBAC Sessions/sec:   \\MSExchange Control Panel\\Requests - Activations/sec:   \\MSExchange Control Panel\\Requests - Average Response Time:   \\MSExchange OWA\\Average Search Time:   \\MSExchange OWA\\Current Unique Users:   \\MSExchange OWA\\Requests/sec:   \\MSExchange RpcClientAccess\\User Count:   \\MSExchange RpcClientAccess\\Active User Count:   \\MSExchange RpcClientAccess\\Connection Count:   \\MSExchange RpcClientAccess\\RPC Averaged Latency:   \\MSExchange RpcClientAccess\\RPC Operations/sec:   \\MSExchange RpcClientAccess\\RPC Requests:   \\MSExchangeWS\\Requests/sec:   \\Web Service(\_Total)\\Connection Attempts/sec:   \\Web Service(\_Total)\\Current Connections:   \\Web Service(\_Total)\\Other Request Methods/sec

ClientAccessRole-2010:   \\MSExchangeFDS:OAB(\_Total)\\Download Tasks Completed:   \\MSExchangeFDS:OAB(\_Total)\\Download Task Queued

;MailboxRole:   \\MSExchange Database(Information Store)\\Log Record Stalls/sec:   \\Process(MSExchangeMailboxAssistants)\\% Processor Time:   \\MSExchange Calendar Attendant\\Average Calendar Attendant
    Processing time:   \\MSExchange Calendar Attendant\\Requests Failed:   \\MSExchange Database(information store)\\I/O Log Reads Average
    Latency:   \\MSExchange Database(information store)\\I/O Database Reads
    (Attached) Average Latency:   \\MSExchange Database(information store)\\I/O Database Reads
    (Recovery) Average Latency:   \\MSExchange Database(information store)\\I/O Database Writes
    (Attached) Average Latency:   \\MSExchange Database(information store)\\I/O Database Writes
    (Recovery) Average Latency:   \\MSExchange Database(information store)\\I/O Log Writes Average
    Latency:   \\MSExchange Database(Information Store)\\Database Page Fault
    Stalls/sec:   \\MSExchange Database(Information Store)\\Database Cache % Hit:   \\MSExchange Database(Information Store)\\Database Cache Size (MB):   \\MSExchange Database(Information Store)\\Log Bytes Write/sec:   \\MSExchange Database(Information Store)\\Log Threads Waiting:   \\MSExchange Database(Information Store)\\Version buckets allocated:   \\MSExchange Resource Booking\\Average Resource Booking Processing
    Time:   \\MSExchange Resource Booking\\Requests Failed:   \\MSExchange Store Interface(\_Total)\\RPC Requests outstanding

;MailboxRole-2010:   \\MSExchange Search Indices(\_Total)\\Average Document Indexing Time:   \\MSExchange Search Indices(\_Total)\\Average Latency of RPCs Used
    to Obtain Content:   \\MSExchangeIS Mailbox(\_Total)\\Messages Delivered/sec:   \\MSExchangeIS Mailbox(\_Total)\\Messages Queued for Submission:   \\MSExchangeIS Mailbox(\_Total)\\Messages Sent/sec:   \\MSExchangeIS Mailbox(\_Total)\\Messages Submitted/sec:   \\MSExchangeIS Mailbox(\_Total)\\Search Task Rate:   \\MSExchangeIS Mailbox(\_Total)\\Slow Findrow Rate:   \\MSExchangeIS Public(\_Total)\\Messages Queued for Submission:   \\MSExchangeIS Public(\_Total)\\Replication Receive Queue Size:   \\MSExchangeIS\\Client: RPCs Failed/sec:   \\MSExchangeIS\\RPC Averaged Latency:   \\MSExchangeIS\\RPC Client Backoff/sec:   \\MSExchangeIS\\Slow QP Threads:   \\MSExchangeIS\\Slow Search Threads:   \\MSExchangeIS\\User Count:   \\Process(Microsoft.Exchange.Search.ExSearch)\\% Processor time:   \\Process(msftesql)\\% Processor Time

;TransportRole:   \\MSExchangeTransport Queues(\_total)\\Active Mailbox Delivery Queue
    Length:   \\MSExchangeTransport Queues(\_total)\\Active Non-Smtp Delivery
    Queue Length:   \\MSExchangeTransport Queues(\_total)\\Messages Completed Delivery
    Per Second:   \\MSExchangeTransport Queues(\_total)\\Messages Queued for Delivery
    Per Second:   \\MSExchangeTransport Queues(\_total)\\Messages Submitted Per Second:   \\MSExchangeTransport Queues(\_total)\\Poison Queue Length:   \\MSExchangeTransport Queues(\_total)\\Retry Mailbox Delivery Queue
    Length:   \\MSExchangeTransport Queues(\_total)\\Retry Non-Smtp Delivery Queue
    Length:   \\MSExchangeTransport Queues(\_total)\\Submission Queue Length:   \\MSExchangeTransport Queues(\_total)\\Unreachable Queue Length:   \\MSExchangeTransport SmtpReceive(\_total)\\Average bytes/message:   \\MSExchangeTransport SmtpReceive(\_total)\\Messages Received/sec:   \\MSExchangeTransport SmtpSend(\_total)\\Messages Sent/sec

;TransportRole-2010:   \\MSExchange Store Driver\\Inbound: LocalDeliveryCallsPerSecond:   \\MSExchange Store Driver\\Inbound: MessageDeliveryAttemptsPerSecond:   \\MSExchange Store Driver\\Inbound: Recipients Delivered Per Second:   \\MSExchange Store Driver\\Outbound: Submitted Mail Items Per Second:   \\MSExchangeTransport Dumpster\\Dumpster Deletes/sec:   \\MSExchangeTransport Dumpster\\Dumpster Inserts/sec:   \\MSExchangeTransport Dumpster\\Dumpster Item Count:   \\MSExchangeTransport Dumpster\\Dumpster Size:   \\MSExchangeTransport Queues(\_total)\\Active Remote Delivery Queue
    Length:   \\MSExchangeTransport Queues(\_total)\\Aggregate Delivery Queue
    Length (All Queues):   \\MSExchangeTransport Queues(\_total)\\Largest Delivery Queue Length:   \\MSExchangeTransport Queues(\_total)\\Retry Remote Delivery Queue
    Length

;MailboxDatabase:   \\MSExchange Assistants - Per
    Database(msexchangemailboxassistants-)\\Average Event Processing
    Time in Seconds:   \\MSExchange Assistants - Per
    Database(msexchangemailboxassistants-)\\Events in queue:   \\MSExchange Assistants - Per
    Database(msexchangemailboxassistants-)\\Events Polled/sec:   \\MSExchange Assistants - Per
    Database(msexchangemailboxassistants-)\\Mailboxes Processed/sec:   \\MSExchange Replication(\_total)\\CopyQueueLength:   \\MSExchange Replication(\_total)\\ReplayQueueLength

;MailboxDatabase-2010:   \\MSExchange Assistants - Per
    Database(msexchangemailsubmission-)\\Average Event Processing Time
    in Seconds:   \\MSExchange Assistants - Per
    Database(msexchangemailsubmission-)\\Events Polled/sec:   \\MSExchange Assistants - Per
    Database(msexchangemailsubmission-)\\Events in queue:   \\MSExchange Assistants - Per
    Database(msexchangemailsubmission-)\\Mailboxes Processed/sec:   \\MSExchange Database ==&gt; Instances(Information Store/)\\I/O
    Database Reads Average Latency:   \\MSExchange Database ==&gt; Instances(Information Store/)\\I/O
    Database Writes Average Latency:   \\MSExchange Database ==&gt; Instances(Information Store/)\\Log
    Generation Checkpoint Depth:   \\MSExchange Search Indices()\\Average Document Indexing Time:   \\MSExchange Search Indices()\\Average Latency of RPCs Used to
    Obtain Content:   \\MSExchange Search Indices()\\Full Crawl Mode Status:   \\MSExchangeIS Mailbox()\\Search Task Rate:   \\MSExchangeIS Mailbox()\\Slow Findrow Rate

The following services will be monitored:

:   IISADMIN:   MSExchangeIS:   MSExchangeADTopology:   MSExchangeMailboxAssistants:   MSExchangeSearch:   MSExchangeServiceHost:   MSExchangeMonitoring:   MSExchangeSA:   MSExchangeMailSubmission:   MSExchangeTransportLogSearch:   msftesql-Exchange:   W3SVC:   MSExchangeFDS

## Thresholds

There are thresholds associated with several of the collected counters
in the above templates.

ClientAccessRole:   activesync_current_requests - Between 50 and 100:   address_book_referral_rpc_requests_latency - Less than 1000:   address_book_rpc_browse_requests_latency - Less than 1000:   address_book_rpc_requests_latency - Less than 1000:   asp_application_restarts - Less than 0:   asp_request_wait_time - Less than 0:   asp_worker_process_restarts - Less than 0:   availability_service_time - Less than 5:   control_panel_outbound_proxy_requests_response_time - Less than 6000:   control_panel_requests_response_time - Less than 6000:   owa_average_search_time - Less than 5000:   rpc_client_access_rpc_averaged_latency - Less than 250:   rpc_client_access_rpc_requests - Less than 40

ClientAccessRole-2010:   oab_download_tasks_queued - Less than 0

MailboxRole:   calendar_attendant_requests_failed - Less than 0:   mailbox_database_cache_size - At least 2 GB free:   mailbox_database_page_flush - Less than 0:   mailbox_log_bytes_write - Less than 10000000:   mailbox_log_read_latency - Less than 200:   mailbox_log_stalls - Less than 10:   mailbox_log_threads_waiting - Less than 10:   mailbox_read_attached_latency - Less than 20:   mailbox_read_recovery_latency - Less than 20:   mailbox_version_buckets - Less than 12000:   resource_booking_requests_failed - Less than 0:   rpc_latency_average - Less than 100:   rpc_requests_outstanding - Less than 0

MailboxRole-2010:   mailbox_average_document_indexing_time - Less than 30000:   mailbox_client_rpc_fails - Less than 0:   mailbox_messages_queued - Less than 50:   mailbox_public_message_queued - Less than 20:   mailbox_slow_qp_threads - Less than 10:   mailbox_slow_search_threads - Less than 10:   replication_receive_queue_size - Less than 100

TransportRole:   active_mailbox_delivery_queue_length - Less than 250:   active_non_smtp_delivery_queue_length - Less than 250:   poison_queue_length - Less than 0:   retry_mailbox_delivery_queue_length - Less than 100:   retry_non_smtp_delivery_queue_length - Less than 100:   submission_queue_length - Less than 100:   unreachable_queue_length - Less than 100

TransportRole-2010:   active_remote_delivery_queue_length - Less than 250:   largest_delivery_queue_length - Less than 200:   retry_remote_delivery_queue_length - Less than 100:   total_delivery_queue_length - Between 3000 and 5000

## Usage

To use the ZenPack, add the zenoss.winrm.WinExchange modeler plugin to
an existing Windows device and run the modeler. For a new device, follow
the directions for adding a new device using the Microsoft Windows
ZenPack

Note: The monitoring user must be a domain user.

Note: If monitoring Exchange with a non-administrator user, the user
must be a member of the Active Directory group "View Only Organization
Management" for 2010 and later installations.

### Configuration Options

-

    zExchangeUser:   If the NETBIOS domain name for the Exchange Server is different
        than the domain name used in the zWinRMUser property, enter that
        information here in either ''netbios'' or ''user@netbios''
        format. This can also be used if a different user account needs
        to be used to model the Exchange Server.

-

    zExchangePassword:   Enter the password of the above account here. It can be left
        blank if it is the same as zWinRMPassword.

-

    zExchangeNoProxy:   Defines whether Session Option NoProxyServer should be added to
        the PowerShell command during modeling device or not.

## Limitations of Current Release

-   Support for Exchange Server 2010, 2013 and 2016 only. Support for
    future versions of Exchange will be added when they are released by
    Microsoft.
-   Exchange Server 2016 will use the same templates as Exchange Server
    2013
-   There are three duplicate counters being collected for Exchange
    Server in the Windows ZenPack. There is a fix available in v2.8.4 of
    the Microsoft.Windows ZenPack which will allow viewing of these
    counters across multiple graphs.

## Troubleshooting

The first step in troubleshooting any monitoring issues is to scan the
zenpython log for errors. Most issues can be solved by troubleshooting
the Windows ZenPack.

> There are currently no logon servers available to service the logon
> request

If you see this error during modeling, check the NETBIOS name against
the users domain name. If they are not the same then use the
zExchangeUser/zExchangePassword configuration options.

> The WinRM client received an HTTP status code of 403 from the remote
> WS-Management service

If you use WinHTTP proxy on your exchange server and see this error
during modeling, check zExchangeNoProxy property and set it to true.

## Zenoss Analytics

This ZenPack provides additional support for Zenoss Analytics. Perform
the following steps to install extra reporting resources into Zenoss
Analytics after installing the ZenPack.

1.  Copy analytics-bundle.zip from
    $ZENHOME/ZenPacks/ZenPacks.zenoss.Microsoft.Exchange/ZenPacks/zenoss/Microsoft/Exchange/analytics/
    on your Zenoss server.
2.  Navigate to Zenoss Analytics in your browser.
3.  From the Zenoss Instance list of options, select Internal
    Authentication.
4.  Login as an Analytics user with superuser privileges.
5.  Remove any existing *Microsoft Exchange ZenPack* folder.
    1.  Choose *Repository* from the *View* menu at the top of the page.
    2.  Expand *Public* in the list of folders.
    3.  Right-click on *Microsoft Exchange ZenPack* folder and choose
        *Delete*.
    4.  Confirm deletion by clicking *OK*.
6.  Add the new *Microsoft Exchange ZenPack* folder.
    1.  Choose *Server Settings* from the *Manage* menu at the top of
        the page.
    2.  Choose *Import* in the left page.
    3.  Remove checks from all check boxes.
    4.  Click *Choose File* to import a data file.
    5.  Choose the analytics-bundle.zip file copied from your Zenoss
        server.
    6.  Click *Import*.

You can now navigate back to the *Microsoft Exchange ZenPack* folder in
the repository to see the following resources added by the bundle.

##### Domains: Microsoft Exchange Domain

Domains can be used to create Ad Hoc views using the following steps.

1.  Choose ''Ad Hoc View'' from the ''Create'' menu.
2.  Click ''Domains'' at the top of the data chooser dialog.
3.  Expand ''Public'' then ''Microsoft Exchange ZenPack''.
4.  Choose the ''Microsoft Exchange Domain'' domain

## Service Impact

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact capability for services running on
Microsoft Windows. The following service impact relationships are
automatically added. These will be included in any services that contain
one or more of the explicitly mentioned entities.

Service Impact Relationships:   The Windows server is impacted by the Exchange Server.

:   The Exchange Server is impacted by the Mailbox Databases.

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

Modeler Plugins:   zenoss.winrm.WinExchange

Monitoring Templates:   ClientAccessRole (in /Server/Microsoft):   ClientAccessRole-2010 (in /Server/Microsoft):   IISADMIN (in /Server/Microsoft):   MSExchangeADTopology (in /Server/Microsoft):   MSExchangeFDS (in /Server/Microsoft):   MSExchangeIS (in /Server/Microsoft):   MSExchangeMailSubmission (in /Server/Microsoft):   MSExchangeMailboxAssistants (in /Server/Microsoft):   MSExchangeMonitoring (in /Server/Microsoft):   MSExchangeSA (in /Server/Microsoft):   MSExchangeSearch (in /Server/Microsoft):   MSExchangeServiceHost (in /Server/Microsoft):   MSExchangeTransportLogSearch (in /Server/Microsoft):   MailboxDatabase (in /Server/Microsoft):   MailboxDatabase-2010 (in /Server/Microsoft):   MailboxRole (in /Server/Microsoft):   MailboxRole-2010 (in /Server/Microsoft):   TransportRole (in /Server/Microsoft):   TransportRole-2010 (in /Server/Microsoft):   W3SVC (in /Server/Microsoft):   msftesql-Exchange (in /Server/Microsoft)

## Changes

1.1.2

-   Fix MicrosoftExchange - N/A for some graphs of Exchange Server
    component and on Graphs tab (ZPS-2197)
-   Fix Azure ZenPack and Exchange Installation Conflict (ZPS-4417)
-   Fix Exchange: Modeler script passes password in plain text
    (ZPS-3482)
-   Tested with Zenoss Resource Manager 6.3.1 and Zenoss Cloud

1.1.1

-   Fix Unable to model due to Exchange Server missing Mailbox role
    (ZPS-2641)
-   Fix The WinRM client received an HTTP status code of 403 from the
    remote WS-Management service (ZPS-2378)
-   Testing was provided on Zenoss Resource Manager: 4.2.5; 5.3.3. and
    6.1.0 and Serevice Impact 5.2.3

1.1.0

-   Use Microsoft Windows ZenPack 2.7.0 session management (ZPS-1227)
-   Fix \[Microsoft Exchange\] Netbios username function fails to
    account for subdomains (ZPS-1942)
-   Make use of new ZenPackLib ZenPack
-   Fix password in log when powershell error occurs during modeling
    (ZPS-1766)
-   Fix MicrosoftExchange - Exchange services are monitored but State is
    'Unknown' (ZPS-2202)
-   Fix Mailbox Databases Discovered Under Device Not Hosting the
    Database (ZPS-1477)
-   Verify support for Exchange 2016 (ZPS-2214)

1.0.5

-   Fix Exchange 2013 Missing Counter Events

1.0.4

-   Fix zenpacks.zenoss.microsoft.windows 2.6.0 missing hardware
    relations (ZEN-23968)

1.0.3

-   Fix impact to be compatible with Windows ZenPack version 2.6.0

1.0.2

-   Fix Exchange ZenPack: WinRM error during modeling (ZEN-23351)
-   Fix Microsoft Exchange modeler type mismatch (ZEN-23317)
-   Update zenpacklib.py to 1.0.12

1.0.1

-   Fix Exchange modeler plugin gets unauthorized error (ZEN-22314)

1.0.0

-   Inital release of Exchange ZenPack

## Attachments:

-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)
-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)


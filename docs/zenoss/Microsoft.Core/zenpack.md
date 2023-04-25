# Microsoft Core

@lb[](img/zenpack-microsoft-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.Microsoft.Core

## Microsoft.Core ZenPack

Monitoring for Microsoft Hyper-V devices using Windows Remote
Management.

## Background

This ZenPack provides the base support for monitoring Microsoft based
devices using Windows Remote Management and Windows Remote Shell using
.Net Core 2.1.

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 1.1.1 - [Download](https://delivery.zenoss.com/){.external-link}
[Download install-zendotnet-v1.1.1.run](https://delivery.zenoss.com/){.external-link}
Released: 2020/09/08
Compatible with Zenoss 5.3.x - 6.5.x and Zenoss Cloud
Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector){.external-link}, [ZenPackLib ZenPack](https://help.zenoss.com/display/in/ZenPackLib){.external-link}, [Microsoft Windows ZenPack](https://help.zenoss.com/display/in/Microsoft+Windows){.external-link}

Version 1.0.0 - [Download](https://delivery.zenoss.com/){.external-link}:   [Download install-zendotnet-v1.0.0.run](https://delivery.zenoss.com/){.external-link}:   Released: 2018/08/10:   Compatible with Zenoss 5.3.x - 6.2.x and Zenoss Cloud:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector){.external-link},
    [ZenPackLib ZenPack](https://help.zenoss.com/display/in/ZenPackLib){.external-link},
    [Microsoft Windows ZenPack](https://help.zenoss.com/display/in/Microsoft+Windows){.external-link}

## Installation and Upgrade Guide

### Prepare to install/upgrade

Before installing or upgrading, you will need to first download the
`install-zendotnet-v*.run` file from [Zenoss Delivery](https://delivery.zenoss.com/){.external-link}, replacing \*
with the current version of the ZenPack. This will install the zendotnet
docker image into the local docker repository. On the master host,
navigate to the directory where you downloaded the egg and run files and
execute the following commands as root:

    chmod +x ./install-zendotnet-*.run yes | ./install-zendotnet-*.run serviced docker sync

Note: The zenoss/zendotnet image **must** be installed before
proceeding. To ensure that it is, run the following:

    docker images | grep zenoss/zendotnet

### Installation

On the master host, navigate to the directory where the Microsoft.Core
ZenPack is located and run:

    serviced service run zope zenpack-manager install ZenPacks.zenoss.Microsoft.Core-*

Assuming successful installation, restart Zenoss

    serviced service restart Zenoss.resmgr/zenoss

Once Zenoss is running, ensure zendotnet image is the latest for
`localhost:5000/<zenoss.resmgr id>/zendotnet` for all collectors using

    docker images | grep zendotnet

The *IMAGE ID* should match for both `zenoss/zendotnet` and
`localhost:5000/<zenoss.resmgr id>/zendotnet`.

### Upgrade

On the master host, navigate to the directory where the Microsoft.Core
ZenPack is located and run the following:

    unzip -p ZenPacks.zenoss.Microsoft.Core-<CHANGE THIS TO VERSION>-py2.7.egg ZenPacks/zenoss/Microsoft/Core/upgrade/service_upgrade.sh > upgrade.sh chmod +x upgrade.sh ./upgrade.sh

Install the new ZenPack:

    serviced service run zope zenpack-manager install ZenPacks.zenoss.Microsoft.Core-*

Assuming successful installation, restart Zenoss

    serviced service restart Zenoss.resmgr/zenoss

Once Zenoss is running, check if zendotnet image is the latest for
`localhost:5000/<zenoss.resmgr id>/zendotnet` for all collectors using

    docker images | grep zendotnet

The *IMAGE ID* should match for both `zenoss/zendotnet` and
`localhost:5000/<zenoss.resmgr id>/zendotnet`.

## Removal

On master host

    serviced service run zope zenpack-manager uninstall ZenPacks.zenoss.Microsoft.Core

Assuming successful removal, restart zenoss

    serviced service restart Zenoss.resmgr/zenoss

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Base Device to be used across all Microsoft devices for uniformity
-   Python based txwinrm module
-   .NET based Zenoss service for winrm communication
-   The zMicrosoftTxRx property to choose between Python/.NET winrm
    communication
-   Base modeler plugin on which other Microsoft ZenPack modeler plugins
    should be based
-   Base Python DataSource on which other Microsoft ZenPack DataSources
    should be based
-   JSONParser useful for custom WinRS commands with JSON formatted
    output

### txwinrm module

This module is the same as found in the Microsoft.Windows ZenPack. It
makes use of the twisted deferred classes to asynchronously collect data
from Microsoft winrm based devices.

It is being moved here in order that all Microsoft communications
mechanisms are centralized and any changes necessary can be shipped more
efficiently.

### zendotnet Service

This zendotnet service uses the .NET Core runtime environment to
communicate with Microsoft devices. The **zendotnet** service resides in
Control Center under **collection** for each collector. You will be able
to access specific configuration information, graphs, and logs just as
you would other Zenoss services.

#### Data collection

The zendotnet service runs a .NET Core based library that collects WMI
data through WinRM (Windows Remote Management) and executes commands and
PowerShell scripts through WinRS (Windows Remote Shell).

#### Custom configuration

In ControlCenter you can control how **zendotnet** behaves in various
ways to achieve the most desirable results. You can change different
entries such as, but not limited to:

-   Thread limit
-   In-Memory Log archive size
-   Log verbosity level
-   Devices updates interval
-   Monitoring halt interval
-   Metrics shipping interval
-   Devices WSMAN connections and remote shells getting retries count

The zendotnet log can be accessed via the service URI path /log. This
log is kept in-memory of the service and is per-instance, meaning
restarting the service will reset the log. All log data is captured in
kibana for permenent storage and should be referenced for service
history.

### JSONParser

JSONParser (placed under
*ZenPacks.zenoss.Microsoft.Core.parsers.JSONParser*) is useful when WinRS output has JSON
format. This parser is more general in comparison to platform JSON
parser. The last requires placing result under "values" and
"&lt;component id&gt; or &lt;device id&gt;" keys, whereas first one
expects keys as datapoint names.

### Configuration Options

The following configuration property can be used to support monitoring
Microsoft environments.

-

    zMicrosoftTxRx:   This option controls the mechanism by which zenoss will connect
        to a Microsoft Device in order to collect data. The default is
        to use the zendotnet service. To use txwinrm for a device or
        device class, change the value to 'txwinrm'.

-

    zWinRMUser:   The syntax used for zWinRMUser controls whether Zenoss will
        attempt Windows local authentication or domain (kerberos)
        authentication. If the value of zWinRMUser is *username*, local
        Windows authentication will be used. If zWinRMUser is
        *username@example.com*, domain authentication will be used. The
        zWinKDC and potentially the zWinRMServerName properties become
        important.

-

    zWinRMPassword:   Password for user defined by *zWinRMUser*.

-

    zWinKDC:   The zWinKDC property must be set if domain authentication is
        used. It must be the IP address or resolvable name of a valid
        Windows domain controller. To use multiple KDCs, you can enter a
        comma separated list of valid addresses or supply different KDCs
        across different Device Classes. See the Kerberos Tickets
        section for more information.

-

    zWinTrustedRealm:   Enter the name of the domain which is trusted by the user's
        domain. This can be a child or other domain which has a trust
        relationship with the user's domain. For example, if zWinRMUser
        is *username@example.com*, and austin.example.com is a child of
        the example.com domain, enter *austin.example.com* into
        zWinTrustedRealm.

-

    zWinTrustedKDC:   This property must be set if zWinTrustedRealm is set. It must be
        the IP address or resolvable name of a valid Windows domain
        controller for the trusted realm. You may also enter a comma
        separated list of kdc addresses.

-

    zWinRMServerName:   This property should only be used in conjunction with domain
        authentication when the DNS PTR record for a monitored server's
        managed IP address does not resolve to the name by which the
        server is known in Active Directory. For example, if myserver1
        is known as myserver1.ad.example.com by Active Directory and is
        being managed by IP address 192.51.100.21, but 192.51.100.21
        resolves to myserver1.example.com, you will have to set
        zWinRMServerName to *myserver1.ad.example.com* for domain
        authentication to work.
    :   If many Windows servers in your environment don't have DNS PTR
        records that match Active Directory, it is recommended that you
        set the name of the Zenoss device's to be the fully-qualified
        Active Directory name and set zWinRMServerName to
        *${here/titleOrId}* at the /Server/Microsoft/Windows device
        class. This avoids the necessity of setting zWinRMServerName on
        every device.
    :   If the server name cannot be resolved and you are using domain
        authentication, it is recommended that you set the Id of the
        device to the IP address and the Title to the server name it is
        known by in Active Directory. Then use *${here/title}* for
        zWinRMServerName. This situation can occur when no DNS server is
        available. Kerberos always performs a reverse lookup when
        obtaining a ticket to use a service on a computer. If your
        servers are known by multiple names, the reverse lookup may
        return the wrong name and you will see "Server not found in
        kerberos database" errors. See the troubleshooting section on
        this topic for a solution.

-

    zWinScheme:   This must be set to either *http* or *https*. The default is
        *http*.

-

    zWinUseWsmanSPN:   If the HTTP/HTTPS service principals are exclusively in use for
        a particular service account, such as on an IIS server, set this
        option to true to use the WSMAN service principal name. You can
        use this option for all domain joined Windows Servers that are
        using a domain monitoring account.
    :   A domain controller may need &ldquo;Validated write to service
        principal name&rdquo; permission for the NETWORK SERVICE account in
        order for the WSMAN service principal name to be used.

-

    zWinRMKrb5includedir:   Optional directory which contains one or more kerberos
        configuration files. This is useful when extra kerberos options
        are needed, such as disabling reverse dns lookup. See [MIT krb5.conf](http://web.mit.edu/kerberos/krb5-devel/doc/admin/conf_files/krb5_conf.html){.external-link}
        for a description of *includedir* and krb5.conf options
        available. The directory must exist and contain only kerberos
        configuration files. If the directory contains non-kerberos
        configuration files, it will be ignored.

-

    zWinRMDisableRDNS:   Kerberos always performs a reverse lookup when obtaining a
        ticket to use the HTTP/HTTPS/WSMAN service principal. If there
        are multiple names by which servers are known in your
        organization, or if you do not want to use reverse lookups, set
        this value to True. Because this is a kerberos property, it can
        only be set one way or another. You cannot mix and match this
        value and only the top level value at /Server/Microsoft will be
        honored.

-

    zWinRMKRBErrorThreshold:   Having a poor network connection can cause erroneous kerberos
        error events to be sent which could cause confusion or false
        alarms. The default value is 1, which will always send an event
        on the first occurrence of an error. You can increase this value
        to send an event only when there have been x amount of
        occurrences of an error during collection, where x denotes the
        threshold number.

-

    zWinKeyTabFilePath:   This property is currently used and reserved for future use when
        keytab files are supported.

-

    zWinRMPort:   The port on which the Windows server is listening for *WinRM* or
        *WS-Management* connections. The default is *5985*. It is
        uncommon for this to be configured as anything else.

-

    zWinPerfmonInterval:   The default interval in seconds at which *Windows Perfmon*
        datapoints will be collected. The default is *300* seconds or 5
        minutes. It is also possible to override the collection interval
        for individual counters.

-

    zWinRMEnvelopeSize:   This property is used when the winrm configuration setting for
        MaxEnvelopeSizekb exceeds the default of 512k. Some WMI queries
        return large amounts of data and this envelope size may need to
        be enlarged. A possible symptom of this is seeing an xml parsing
        error during collection or "Check WMI namespace and DCOM
        permission" returned from the OperatingSystem modeler plugin.

-

    zWinRSCodePage:   The code page which is in use on the Windows Server for the
        monitoring user account. The default is to use 65001, the
        identifier for unicode. The full list is
        [here](https://msdn.microsoft.com/en-us/library/windows/desktop/dd317756(v=vs.85){.external-link}.aspx){.external-link}.
        To determine the code page in use on a Windows server, run
        `chcp` at a command prompt.

## Troubleshooting

Please refer to the Zenoss Service Dynamics documentation if you run
into any of the following problems:

-   ZenPack will not install
-   Adding a device fails
-   Don't understand how to add a device
-   Don't understand how to model a device

If you cannot find the answer in the documentation, then Resource
Manager (Service Dynamics) users should contact [Zenoss Customer Support](https://support.zenoss.com){.external-link}. Core users can use
the \#zenoss IRC channel or the community.zenoss.org forums (there is a
forum specific to Windows monitoring).

### Troubleshooting Windows

If you see 100% CPU usage on a domain controller and your forest
functional level is Windows 2003 or Windows 2008, you could be missing
the WinRMRemoteWMIUsers\_\_ security group. Adding this group to your
domain should fix this problem. It is a known error from Microsoft, [kb 3118385](https://support.microsoft.com/en-us/kb/3118385){.external-link}.

### Troubleshooting Kerberos Error Messages

`Cannot determine realm for numeric host address`

-   If you enter an IP address for the device id, make sure that the
    address is resolvable to a name. Common solutions to this is to use
    the zWinRMServerName property.

`Server not found in Kerberos database`

-   More often than not, this error indicates a DNS issue in which the
    domain controller is unable to locate the specified server by either
    IP address or name. The best solution varies over different domains
    and it is left to the user to decide which is best for their
    environment.

-   One solution is to disable reverse DNS lookups for kerberos. This
    can be achieved by setting the zWinRMDisableRDNS property to True.
    If you use this option, you *MUST* only set it in at the
    /Server/Microsoft device class level.

-   You should also ensure that the correct name is returned for
    lookups.

`Preauthentication failed while getting initial credentials.`

-   This typically indicates a bad or expired password.

`Realm not local to KDC while getting initial credentials`

-   This indicates that one or more of the defined KDCs for a domain are
    incorrect. Add a *-* to the beginning of the errant KDC address to
    the beginning of the incorrect address in the zWinKDC property to
    remove it from the list of KDCs for a domain.

`No accept token received from <service-SPN-name>@<server-FQDN> for <client-SPN-name>@<domain-name>`

-   This is often connected with WinRM configuration on a target
    device. Make sure that WinRM is properly configured and *WSMAN* SPN
    (Service Principal Name) is enabled on a target device.

### Troubleshooting Kerberos Authentication with Wireshark

There are many reasons for kerberos authentication not to work, and a
lot of them result in the following unhelpful error message.

`kerberos authGSSClientStep failed (None)`

While Zenoss is unable to extract a useful error message when this
occurs, it turns out that Wireshark can get useful errors by looking at
the kerberos packets sent between Zenoss, your domain controller
(*zWinKDC*) and the monitored Windows server. Let's walk through an
example of using [Wireshark](http://www.wireshark.org/){.external-link}
to resolve an *authGSSClientStep failed* error.

First install Wireshark on your system. It's GUI is easier to use than
the command line equivalent.

Next you will need to create a packet capture file on your Zenoss
server. Assuming the Windows server you're trying to monitor is
*192.0.2.101* and the domain controller (*zWinKDC*) is *203.0.113.10*,
you would run the following command as the root user on your Zenoss
server.

    tcpdump -s0 -iany -w kerberdebug.pcap host 192.0.2.101 or host 203.0.113.10

This will start capturing all packets to or from those two IP addresses.
It will continue to capture these packets until you type *CTRL-C*.

Now you should attempt to remodel the Windows server where you're
encountering the error. Once it completes, and fails, again you should
go back to the terminal where tcpdump is running and type *CTRL-C*. You
will now have a *kerberdebug.pcap* file in the directory where you ran
the command.

Copy *kerberdebug.pcap* to your system where you installed Wireshark.
Start Wireshark and open *kerberdebug.pcap*. You should see something
like the following.

@lb[](img/zenpack-windows-kerberos-wireshark.png)

You'll see that there's a *KRB5KRB_AP_ERR_SKEW* error. Searching for
this specific error code will quickly show that it occurs when the
kerberos client and server don't have their time's synchronized. There's
a tolerance for some difference, but in this case it was a big
difference due to misconfiguration.

There are some kerberos errors you'll see in the packets that a
completely normal part of negotiation and won't lead to any problems.
You should ignore the following errors shown in Wireshark:

-   *KRB5KRB_API_ERR_TKT_EXPIRED*: Zenoss will subsequently request a
    new ticket when this occurs.
-   *KRB5KRB_ERR_PREAUTH_REQUIRED*: This is a normal part of kerberos
    negotiation.
-   *KRB5KRB_ERR_RESPONSE_TOO_BIG*: Most requests won't fit in UDP.
    Zenoss will automatically switch to TCP.

You'll also see other kerberos messages that are normal. You should
ignore these kerberos messages shown by Wireshark:

-   *TGS-REQ*
-   *AS-REQ*

The following are the most common errors: - *KRB5KRB_AP_ERR_SKEW*: - As
shown in the above example. A clock synchronization issue. -
*KRB5KDC_ERR_S\_PRINCIPAL_UNKNOWN* - This can happen if
*zWinRMServerName* resolves to the server's IP address, but is not the
name the server is known by in Active Directory. This will also be the
error if you don't enter a *zWinRMServerName* and the reverse resolution
of the device's manage IP address resolves to a name that doesn't match
the server's name in Active Directory. Typical solutions to this are to
add the name to the /etc/hosts file or to directly use the IP address of
the server.

### Troubleshooting zendotnet

The zendotnet service implements a REST api on ports
5001(http)/5050(https) of the collector. This api can be curled from
inside the *zenpython*, *zenmodeler*, *zminion*, *zenjobs*, and *Zope*
containers. It can also be viewed from a browser by creating a public
endpoint using the collector's IP address or hostname.

To create the endpoint:

1.  Open Control Center and navigate to the zendotnet service page.
2.  Click the Add Public Endpoint button.
3.  Select the Port option.
4.  Ensure that the correct zendotnet "Service - Endpoint" is selected,
    e.g. "zendotnet - localhost_zendotnet".
5.  Enter the IP address or hostname of the collector.
6.  Enter a number other than 5001 or 5050 for the port. These two ports
    are reserved for the zendotnet service and will not work.
7.  Select either HTTP or HTTPS for the endpoint.
8.  Click the Add button.

After the endpoint has started, you can view logs, devices, kerberos
configuration, and statistics using the following example urls:

-   https://192.168.1.55:5432/log: Displays the current in-memory log
    with most recent entries at the top.
-   https://192.168.1.55:5432/log/deviceid: Displays the current
    in-memory log for only the device specified.
-   https://192.168.1.55:5432/log?level=Debug?duration=600: Enables
    debug logging for 10 minutes. Valid levels are Fatal, Critical,
    Exception, Error, Audit, Warning, Info, General, Verbose, and Debug.
    Audit is the default level, but can be changed in zendotnet.conf
    using ZenDotNetLogDefaultLevel.
-   https://192.168.1.55:5432/wsman: Displays a list of the current
    devices.
-   https://192.168.1.55:5432/wsman/deviceid: Displays the settings of
    the device specified.
-   https://192.168.1.55:5432/wsman/deviceid/resourceid: Displays the
    current results of the resourceid's query.
-   https://192.168.1.55:5432/krb5: Displays the kerberos
    configuration(krb5.conf) file.
-   https://192.168.1.55:5432/krb5/log:
    Displays the zerberos log. Add "?level=7" to set the log level to
    the highest, Debug.
-   https://192.168.1.55:5432/krb5/stats: Displays statistics of
    encrypted/decrypted data sent and received in kilobytes.
-   https://192.168.1.55:5432/krb5/kinit:
    Runs `kinit` command.
-   https://192.168.1.55:5432/krb5/klist:
    Runs `klist` command.

If using curl inside a valid container, replace
`https://192.168.1.55:5432` with `localhost:5001`. For example,
`curl localhost:5001/wsman/deviceid | jq`.

Note: Because this is the mechanism by which we collect data from
devices, we recommend that you do not send POST requests as it could
interfere with stable collection. Enabling the public endpoint should
only be used for troubleshooting, so you should Stop the endpoint under
normal operation.

## Limitations of Current Release

The current release is known to have the following limitations.

-   The zendotnet service is a new infrastructure service which
    implements Windows Remote Management and Shell using Microsoft's
    .NET Core SDK. It is set as the default collection mechanism for
    Microsoft winrm based devices. This ZenPack also provides 'txwinrm',
    which uses twisted python to collect from Microsoft winrm based
    devices.
-   Currently the HyperV ZenPack is the only Microsoft ZenPack making
    use of Microsoft.Core. The Windows, Exchange, MSMQ, and Lync
    ZenPacks have not been converted to use this ZenPack.
-   zWinRSCodePage is currently only used in the txwinrm module.
-   zendotnet currently only works with a single domain user. Trusted
    domains can be used with the zWinTrustedRealm/zWinTrustedKDC
    properties.
-   Currently zendotnet works only with *WSMAN* SPN (Service principal
    name) when domain (kerberos) authentication is used. This ignores
    the value of zWinUseWsmanSPN property.

## Changes

1.1.1

-   Corrected update process to replace the runtime image. (ZPS-7324)

1.1.0

-   Add JSON parser to process data in more user-friendly format.
    (ZPS-7146)
-   Add possibility to run 'Command' requests both for txwinrm and
    zendotnet clients. (ZPS-7143)
-   Add zendotnet service metrics to be shown in RMMonitor. (ZPS-4971)
-   Fix 'ConnectionLost' error when device is remodeled few times in a
    row. (ZPS-4049)
-   Fix issues which leads to numerous error events. (ZPS-6794)
-   Fix modeling fail while getting initial credentials using zendotnet.
    (ZPS-6621)
-   Fix zendotnet and libzerberos crash with wrong principle. (ZPS-7248)
-   Fix zerberos segmentation fault which leads to zendotnet restarts.
    (ZPS-4188)
-   Improve collection stability when using zendotnet with low
    collection interval. (ZPS-4114)
-   Tested with Zenoss Resource Manager 6.4.1, Zenoss Resource Manager
    6.5.0, Zenoss Cloud and Service Impact 5.5.2

1.0.1

-   Update txwinrm to latest version

1.0.0

-   Initial release of Microsoft Core
-   Tested with Zenoss Cloud, Zenoss Resource Manager 6.2.0, Zenoss
    Resource Manager 5.3.3 with Service Impact 5.3.1 and Analytics 5.1.0

## Attachments:

-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)
-   [windows-kerberos-wireshark.png](img/zenpack-windows-kerberos-wireshark.png)
-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)
-   [windows-kerberos-wireshark.png](img/zenpack-windows-kerberos-wireshark.png)
-   [microsoft-zenpack.png](img/zenpack-microsoft-zenpack.png)


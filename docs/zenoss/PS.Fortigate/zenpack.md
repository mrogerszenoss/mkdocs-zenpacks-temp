# Fortinet Fortigate Integration Service

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

Fortigate Integration Service
**Version:**
1.1.0

## **Fortinet Fortigate ZenPack**

**Description**

This ZenPack provides the capability to model and monitor Fortinet
Fortigate devices.

**Prerequisites**

Prerequisite Restriction

ProductZenoss Zenoss 6.0 or higher

Required ZenPacks
ZenPacks.zenoss.ZenPackLibZenPacks.zenoss.PS.Util

Other dependencies None

**Device Classes**

This Device Class is added for Devices:

-   /Network/Fortinet/Fortigate

**Changes**

Release 1.1.0

-   Features–Add Manufacturer / Model OID support.

**Modeler Plugins**

-   snmp.InterfaceMap
-   snmp.DeviceMap
-   snmp.FGDevice
-   snmp.FGVirtualDomain
-   snmp.FGVirtualDomainWebFilter
-   snmp.FGVirtualDomainFortiGuard
-   snmp.FGVirtualDomainVpn

**Components Modeled**

-   Virtual Domain
-   SSL VPN1
-   FortiGuard
-   WebFilter

**Device Class Templates**

Devices/Network/Fortinet/Fortigate

-   FortigateDevice
    -   Graphs
        -   Disk Usage
        -   Uptime
        -   Session Count
        -   Memory Usage
        -   CPU Usage
        -   LowMem Usage
    -   Thresholds
        -   90 percent memory utilization
        -   90 percent hard disk usage
        -   90 percent CPU usage
    -   Datapoints
        -   sysDiskUsage
        -   sysMemUsage
        -   sysUpTime
        -   sysCpuUsage
        -   sysSesCount
        -   sysLowMemUsage

-   FortigateVirtualDomainWebFilter
    -   Graphs
        -   ActiveX Downloads Blocked
        -   Sessions Blocked
        -   Applets Blocked
        -   HTTP Cookies Blocked
        -   URLs Blocked
    -   Datapoints
        -   wfHTTPSBlocked
        -   wfAppletBlocked
        -   wfHTTPBlocked
        -   wfActiveXBlocked
        -   wfCookieBlocked
        -   wfHTTPURLBlock
        -   wfHTTPSURLBlock

-   FortigateVirtualDomainVpnSsl
    -   Graphs
        -   Logged In Users
        -   Active SSL web sessions
        -   Active SSL tunnels
    -   Thresholds
        -   VpnSslState
    -   Datapoints2
        -   fgVpnState
        -   fgVpnLoginUsers
        -   fgVpnWebSession
        -   fgVpnTunnels

-   FortigateVirtualDomain
    -   Graphs
        -   Memory Usage
        -   CPU Usage
        -   Active Sessions
        -   Session Rate
    -   Thresholds
        -   VdEntHaState
    -   Datapoints
        -   vdEntCpuUsage
        -   vdEntHaState
        -   vdEntSesCount
        -   vdEntSesRate
        -   vdEntMemUsage

-   FortigateVirtualDomainFortiGuard
    -   Graphs
        -   Requests Allowed
        -   Requests Logged
        -   Requests Examined
        -   Requests Blocked
        -   Requests Overridden
    -   Datapoints
        -   fgHTTPOverride
        -   fgHTTPExamined
        -   fgHTTPSLogged
        -   fgHTTPLogged
        -   fgHTTPSExamined
        -   fgHTTPSBlocked
        -   fgHTTPBlocked
        -   fgHTTPSAllowed
        -   fgHTTPSOverride
        -   fgHTTPAllowed



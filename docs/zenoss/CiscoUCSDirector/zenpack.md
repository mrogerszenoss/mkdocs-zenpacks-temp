# Cisco UCS Director

@lb[](img/zenpack-cisco-zenpack.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.CiscoUCSDirector

### Applications Monitored:

Cisco UCS Director (5.3)

## Cisco UCS Director ZenPack

Impact Modeling for Cisco UCS Director topologies

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 1.0.2- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2015/08/14:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},[vSphere ZenPack](https://help.zenoss.com/display/in/vsphere-page-does-not-exist "ZenPack:VSphere (page does not exist){.external-link}"):   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x

<!-- -->

Version 1.0.0- [Download](https://zenoss.leapfile.net/){.external-link}:   Released on 2015/05/08:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},[vSphere ZenPack](https://help.zenoss.com/display/in/vsphere-page-does-not-exist "ZenPack:VSphere (page does not exist){.external-link}"):   Compatible with Zenoss Resource Manager 4.2.x, Zenoss Resource
    Manager 5.0.x

## Background

This ZenPack provides support for modeling the Impact Relationships of
[UCS Director](http://www.cisco.com/c/en/us/products/servers-unified-computing/ucs-director/index.html){.external-link},
specifically Tenants, Virtual Datacenters, and VMWare Virtual Machines.

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.\* Initial discovery and modeling of
Tenants and vDCs.\* Event management.\* Service impact and root cause
analysis. (Requires Zenoss Service Dynamics)

### Discovery

The following components will be automatically discovered through the
UCS-D connection info you provide. The properties and relationships will
be continually maintained by periodically checking the UCS-D API.

Tenants

-   Attributes: None
-   Relationships: Virtual Datacenters belong to a single Tenant

Virtual Data Centers (vDC)

-   Attributes: None
-   Relationships: Virtual Datacenters belong to a single Tenant and can
    contain many Virtual Machines.

Virtual Machine

-   Attributes: Corresponding VMWare VM
-   Relationships: Virtual Machines belong to a single vDC

### Event Management

Events are created for success or failure while collecting information
from the UCS-D host

### Service Impact and Root Cause Analysis

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact and root cause analysis capabilities for
UCS topologies, including vSphere Virtual Machines.

Internal Impact Relationships

-   vDC failure impacts the parent Tenant
-   VM failure impacts the parent vDC

External Impact Relationships

-   vSphere VM failure impacts the related VM

## Usage

### Adding UCS Director Endpoint

Use the following steps to start monitoring UCS Director using the
Zenoss web interface.

1.  Navigate to the Infrastructure page.
2.  Choose *Add UCS Director Endpoint* from the add device button.
3.  Fill out the form.
    -   *Name* can be anything you want.
    -   *Port* is the http port used to access the UCS Director
        Dashboard, probably 80.
    -   *API Key* is the UCS Director admin API Key.
4.  Click *ADD*.

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

**Configuration Properties**

-   zCiscoUCSDHostname: Hostname of the UCS-D Instance
-   zCiscoUCSDAPIKey: Admin API Key for the UCS-D Instance
-   zCiscoUCSDPolicyTrigger: Service Impact Policy for Availability and
    Performance
-   zCiscoUCSDPort: HTTP port of the UCS-D instance
-   zCiscoUCSDRefresh

**Device Classes**

-   /CiscoUCS/UCS-Director

**Modeler Plugins**

-   CiscoUCSDirector.Director

## Changes

<dl markdown="1">
<dt markdown="1">
1.0.0
</dt>
</dl>

-   Initial release.

## Attachments:

-   [cisco-zenpack.png](img/zenpack-cisco-zenpack.png)


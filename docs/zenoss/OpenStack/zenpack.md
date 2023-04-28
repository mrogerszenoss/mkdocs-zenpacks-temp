# OpenStack (Tenant View)

## OpenStack (Tenant View) ZenPack

This ZenPack allows for monitoring of OpenStack tenants. This means that
you can monitor the flavors, images and servers from a tenant
perspective.

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

### Version 1.3.2 [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.OpenStack/1.3.2/ZenPacks.zenoss.OpenStack-1.3.2.egg){.external-link}

Summary of changes:

-   Support for Twisted library update
-   Compatibility fixes for Impact 5.5

Released on 2020/06/05

Tested with Zenoss Resource Manager 6.4.1, Zenoss Cloud and Service
Impact 5.5.1

### Version 1.2.3 [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.OpenStack/1.2.3/ZenPacks.zenoss.OpenStack-1.2.3.egg){.external-link}

Summary of changes:

-   Move devices from /Devices/OpenStack to /Dev0ices/OpenStack/User
-   Support new [OpenStack Infrastructure ZenPack](http://help.zenoss.com/display/in/){.external-link}
-   Drop support for Compute API v1.x

<dl markdown="1">
<dt markdown="1">
Released on 2014/10/09
Compatible with Zenoss 4.2 - 5.x
</dt>
</dl>

## Background

This ZenPack allows for monitoring of OpenStack. This means that you can
monitor the flavors, images and servers from a tenant perspective.

## Usage

Once the OpenStack ZenPack is installed you can begin monitoring by
going to the infrastructure screen and clicking the normal button for
adding devices. You'll find a new option labeled, "Add OpenStack
Endpoint (User)'".

Choose that option and you'll be presented with a dialog asking for the
following inputs.

1.  Device To Create - non-empty, non-ip, non-dns, unique name to use
    for this device in Zenoss. *See note below*.
2.  Auth URL - A keystone URL, such as <http://10.0.0.1:5000/v2.0/>
3.  Username - Same username used to login to OpenStack web interface
4.  Password / API Key - Password to use
5.  Project/Tenant ID
6.  Region Name - choose the correct region from the drop-down.

Most of these parameters can be be found by going to "Your Account/API
Access" in the OpenStack web interface, or from the corresponding
environment variables for the OpenStack command line tools.

Once you click Add, Zenoss will contact the OpenStack API and discover
servers, images and flavors. Once it is complete you'll find a new
device in the OpenStack device class with the same name as the hostname
or IP you entered into the dialog. Click into this new device to see
everything that was discovered.

The following types of elements are discovered.

-   Servers
-   Images
-   Flavors

The following metrics are collected.

-   Total Servers and Servers by State
    -   States: Active, Build, Rebuild, Suspended, Queue Resize, Prep
        Resize, Resize, Verify Resize, Password, Rescue, Reboot, Hard
        Reboot, Delete IP, Unknown, Other
-   Total Images and Images by State
    -   States: Active, Saving, Preparing, Queued, Failed, Unknown,
        Other
-   Total Flavors

Status monitoring is performed on servers and images with the following
mapping of state to Zenoss event severity.

Servers State to Severity Mapping:   Reboot, Hard Reboot, Build, Rebuild, Rescue, Unknown == Critical:   Resize == Error:   Prep Resize, Delete IP == Warning:   Suspended, Queue Resize, Verify Resize, Password == Info:   Active == Clear

<!-- -->

Images State to Severity Mapping:   Failed, Unknown == Critical:   Queued, Saving, Preparing == Info:   Active == Clear

If you are also using Zenoss to monitor the guest operating system
running within the server Zenoss will present the graphs for that
operating system when the graphs option is chosen for the OpenStack
server.

## Changes

**1.3.2**

-   Add support for Twisted library update (ZPS-7071)

**1.3.1**

-   Address compatibility issues with Impact 5.5

**1.3.0**

-   Change "add" form to more closely resemble the one used for
    OpenStackInfrastructure
-   Require user to name the device, rather than using the manageIp
-   No longer use manageIp at all. This allows for multiple user devices
    to contact the same openstack install.
-   Drop novaclient dependency and adopt OSI txapiclient code
-   Tested with Zenoss Cloud and Zenoss Resource Manager 6.3.2

**1.2.4**

-   zOpenStackInsecure option added to skip SSL certificate
    verification, which allows self-signed or third-party certificates.
    (ZEN-23460)

**1.2.3**

-   Move devices from /Devices/OpenStack to /Devices/OpenStack/User
-   Support new OpenStackInfrastructure ZenPack
-   Drop support for Compute API v1.x

**1.2.2**
-   Fix bug that could prevent data collection.

**1.2.1**

-   Fix bug in handling of flavor ID. (ZEN-10333)

**1.2.0**

-   Add support for compute API versions 2 and 3. Still support
    version 1.
-   Add zOpenstackComputeApiVersion configuration property.
-   Update python-novaclient to 2.15.0.
-   Support uuid format for image identifier.

| **ZenPack Classification**    |                                                                                                                                                                                                                                                                                                                                                                   |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Open Source**               | This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link} to view all available Zenoss Open Source ZenPacks. |
| **Organization**              | Zenoss, Inc.                                                                                                                                                                                                                                                                                                                                                      |
| **License**                   | GNU General Public License, Version 2, or later                                                                                                                                                                                                                                                                                                                   |
| **Name**                      | ZenPacks.zenoss.OpenStack                                                                                                                                                                                                                                                                                                                                         |
| **More Information**          | [GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.WBEM){.external-link}                                                                                                                                                                                                                                                                            |
| **Git Sources (For Cloning)** | [Link](https://github.com/zenoss/ZenPacks.zenoss.OpenStack.git){.external-link}                                                                                                                                                                                                                                                                                   |
| **Applications Monitored**    | OpenStack Cloud Computing                                                                                                                                                                                                                                                                                                                                         |

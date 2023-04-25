# AWS RDS Monitoring

@lb[](img/zenpack-aws-logo-partner_2_0.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Jerome C. Ortega

### Maintainers:

Jerome C. Ortega

### Organization:

Cascadeo

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.Cascadeo.ZenRDS

### More Information:

[GitHub page/HomePage](https://github.com/cascadeo/ZenPacks.Cascadeo.ZenRDS){.external-link}

### Link To More Docs:

[View Documentation](https://github.com/cascadeo/ZenPacks.Cascadeo.ZenRDS){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/cascadeo/ZenPacks.Cascadeo.ZenRDS.git){.external-link}

## AWS RDS Monitoring ZenPack

AWS RDS Monitoring

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Background

The ZenRDS ZenPack provides monitoring for AWS RDS instances without
installing Zenoss AWS ZenPack. It provides the following performance
metrics through CloudWatch API.

"CPUUtilization", "DatabaseConnections", "FreeableMemory",
"FreeStorageSpace", "ReadIOPS", "ReadLatency", "ReadThroughput",
"SwapUsage", "WriteIOPS", "WriteLatency", "WriteThroughput"

To use Cascadeo ZenRDS Zenpack:

## Install Python-Boto on Zenoss Python environment

SSH in to Zenoss and login as zenoss user (important) Download Python
Boto library from <http://boto.googlecode.com/files/> Untar and install
it using python setup tools. python setup.py install

## Install Zenpack Code from GitHub

On the zenoss host, clone the latest ZenRDS code Change directory to the
zenpack's root dir. Create egg package by executing python setup.py
bdist_egg Install the generated egg package/zenpack under dist
directory. zenpack --install &lt;Zenpackname.egg&gt; Restart the zopectl
and zeoctl daemons, or the whole zenoss stack. Wait for a few seconds
and reload the Zenoss UI,

## Add your devices to /Server/RDS

The Zenpack will create /Server/RDS device class. Put all RDS intances
you want to monitor in /Server/RDS (under infrastructure tab) Disable
Ping and SNMP monitoring for the device class.

## Configure instance names and secret keys

Go to the "Configuration Properties" for the devie Set the following
fields: zRDSIdentity (your AWS identity number), zRDSKey (your AWS
secret key), zRDSInstance (the instance name of the RDS) and zRDSRegion
(region where the instance is us-east-1, us-west-1, etc). Make sure that
the key has at least read-only privilge to the RDS instance. Wait for
the data to come in. Run zencommand to force collection, if necessary.
Configure threshold levels according to your need in the ZenRDS
monitoring template.

## Known Issues/Errors

Error importing Boto module. This is a pre-requisite. \*\* Make sure
that zenoss' python environment has access to the Boto library.

Request has expired. Timestamp date: x-x-x-x \*\* Make sure that system
time is accurate AWS RDS

## Attachments:

-   [aws-logo-partner_2\_0.png](img/zenpack-aws-logo-partner_2_0.png)
-   [aws-logo-partner_2\_0.png](img/zenpack-aws-logo-partner_2_0.png)
-   [aws-logo-partner_2\_0.png](img/zenpack-aws-logo-partner_2_0.png)
-   [aws-logo-partner_2\_0.png](img/zenpack-aws-logo-partner_2_0.png)


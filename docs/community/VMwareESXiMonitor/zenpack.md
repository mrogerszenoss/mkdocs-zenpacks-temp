# VMware ESXi Monitor

@lb[](img/zenpack-vmware-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Eric Enns

Matthias Kittl

### Maintainers:

Eric Enns

Matthias Kittl

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.community.VMwareESXiMonitor

### More Information:

[GitHub page/HomePage](https://github.com/ericenns/ZenPacks.community.VMwareESXiMonitor){.external-link}

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-10225){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/ericenns/ZenPacks.community.VMwareESXiMonitor.git){.external-link}

### Applications Monitored:

VMware (ESXi)

## VMware ESXi Monitor ZenPack

This ZenPack monitors general ESXi host and vm stats such as CPU,
memory, and storage. Now you can watch and assure your virtual
infrastructure with Zenoss.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.2- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.VMwareESXiMonitor/1.2/ZenPacks.community.VMwareESXiMonitor-1.2.egg){.external-link}:   **Summary of changes:** initial release:   Requires [VMWare Data Source ZenPack](https://help.zenoss.com/display/in/VMware+Data+Source "ZenPack:VMWare Data Source"){.external-link},[Virtual Host Monitor ZenPack](https://help.zenoss.com/display/in/Virtual+Host+Monitor "ZenPack:Virtual Host Monitor"){.external-link}:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.2.x

<!-- -->

Version 2.0.3- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.VMwareESXiMonitor/2.0.3/ZenPacks.community.VMwareESXiMonitor-2.0.3.egg){.external-link}:   **Summary of changes:** Adds checks to ensure data structure exists
    before accessing value, prevents get_info from failing silently:   Released on 2015/01/29:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x

<!-- -->

Version 2.0.4- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.VMwareESXiMonitor/2.0.4/ZenPacks.community.VMwareESXiMonitor-2.0.4.egg){.external-link}:   **Summary of changes:** Added performance metrics for ESXi Host,
    added thresholds for CPU and Memory usage

Notice: You'll have to delete the existing Monitoring Templates
(ESXiDatastore, ESXiHost, ESXiVM) when upgrading from a previous version
of this ZenPack.

<dl markdown="1">
<dd markdown="1">
Released on 2015/03/28
</dd>
<dd markdown="1">
Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x
</dd>
</dl>

Version 2.0.5- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.VMwareESXiMonitor/2.0.5/ZenPacks.community.VMwareESXiMonitor-2.0.5.egg){.external-link}:   **Summary of changes:** Fixed Error: "TypeError: a float is
    required"
:   Released on 2015/04/17:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x

<!-- -->

Version 2.0.6- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.VMwareESXiMonitor/2.0.6/ZenPacks.community.VMwareESXiMonitor-2.0.6.egg){.external-link}:   **Summary of changes:** Fixed Error: "TypeError: not enough
    arguments for format string"
:   Released on 2015/05/07:   Compatible with Zenoss Core 4.2.x, Zenoss Core 5.0.x

## Background

This ZenPack allows Zenoss to monitor VMware ESXi Hosts and VMs via the
vSphere SDK for Perl.
It creates the /Server/VMware/ESXi Device Class. All ESXi Hosts have to
be added to this Device Class.

## Zenoss 4.2.x Installation

##### Install the required perl packages:

yum -y install perl perl-XML-LibXML glibc.i686 e2fsprogs e2fsprogs-devel
libuuid-devel libxml2-devel

##### Install the vSphere SDK for Perl:

Extract the archive (tar xzf
VMware-vSphere-Perl-SDK-&lt;version&gt;.x86_64.tar.gz)
Cd into the newly created directory (vmware-vsphere-cli-distrib)
Run the installer (vmware-install.pl)

##### Follow the instructions in the Zenoss Admin Guide to install the ZenPack.

## Zenoss 5+ Installation

##### Please follow the following instructions to install the vSphere SDK for Perl in the zenhub container.

##### Start a new shell in the running zenhub service and save the service instance with a new name:

serviced service shell -s VMware_vSphere_SDK -i zenhub bash

##### Install the required perl packages:

yum -y install perl perl-XML-LibXML perl-Crypt-SSLeay
perl-ExtUtils-MakeMaker e2fsprogs e2fsprogs-devel openssl-devel
libxml2-devel

##### Remove the data cached by yum:

yum clean all

##### Downgrade the following two perl packages manually (this is required, because the vSphere SDK for Perl has not yet been officially released for CentOS 7):

Download "Net-HTTP-6.03.tar.gz" and "libwww-perl-6.03.tar.gz"
Extract the archive (e.g. tar xzf Net-HTTP-6.03.tar.gz)
Cd into the newly created directory (e.g. Net-HTTP-6.03)
Run:
perl Makefile.PL
make
make test
make install

##### Install the vSphere SDK for Perl:

Extract the archive (tar xzf
VMware-vSphere-Perl-SDK-&lt;version&gt;.x86_64.tar.gz)
Cd into the newly created directory (vmware-vsphere-cli-distrib)
Run the installer (vmware-install.pl)

##### Fix "length() used on @array (did you mean "scalar(@array)"?)" error:

Copy the following file into a temporary directory:
"/usr/lib64/perl5/IO/Compress/Zlib/Extra.pm"
Change the permission to give yourself write privileges (e.g. 644)
Search for the following line: "for (my $ix = 0; $ix &lt;=
length(@$data) -1; $ix += 2)"
replace it with: "for (my $ix = 0; $ix &lt;= @$data -1; $ix += 2)"
Change the permissions back (444)
Copy the file back into the original directory

##### Complete the modification of the service instance:

Exit the shell
Commit the changes you have made: "serviced snapshot commit
VMware_vSphere_SDK"

##### Follow the instructions in the Zenoss Admin Guide to install the ZenPack.

## zProperties

##### The ZenPack will add two zProperties:

-   zVSphereUsername: Name of a User that has read-only access to the
    ESXi Host
-   zVSpherePassword: The corresponding Password

## Screenshots

@lb[](img/zenpack-esxi_host_overview.jpg)

@lb[](img/zenpack-esxi_host_graph.jpg)

@lb[](img/zenpack-esxi_datastore.jpg)

@lb[](img/zenpack-esxi_vm.jpg)

@lb[](img/zenpack-esxi_interface.jpg)

@lb[](img/zenpack-esxi_report.jpg)

## Attachments:

-   [ESXi_Datastore.jpg](img/zenpack-esxi_datastore.jpg)
-   [ESXi_Host_Graph.jpg](img/zenpack-esxi_host_graph.jpg)
-   [ESXi_Host_Overview.jpg](img/zenpack-esxi_host_overview.jpg)
-   [ESXi_Interface.jpg](img/zenpack-esxi_interface.jpg)
-   [ESXi_Report.jpg](img/zenpack-esxi_report.jpg)
-   [ESXi_VM.jpg](img/zenpack-esxi_vm.jpg)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)
-   [ESXi_Datastore.jpg](img/zenpack-esxi_datastore.jpg)
-   [ESXi_Host_Graph.jpg](img/zenpack-esxi_host_graph.jpg)
-   [ESXi_Host_Overview.jpg](img/zenpack-esxi_host_overview.jpg)
-   [ESXi_Interface.jpg](img/zenpack-esxi_interface.jpg)
-   [ESXi_Report.jpg](img/zenpack-esxi_report.jpg)
-   [ESXi_VM.jpg](img/zenpack-esxi_vm.jpg)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)
-   [ESXi_Datastore.jpg](img/zenpack-esxi_datastore.jpg)
-   [ESXi_Host_Graph.jpg](img/zenpack-esxi_host_graph.jpg)
-   [ESXi_Host_Overview.jpg](img/zenpack-esxi_host_overview.jpg)
-   [ESXi_Interface.jpg](img/zenpack-esxi_interface.jpg)
-   [ESXi_Report.jpg](img/zenpack-esxi_report.jpg)
-   [ESXi_VM.jpg](img/zenpack-esxi_vm.jpg)
-   [vmware-zenpack.png](img/zenpack-vmware-zenpack.png)


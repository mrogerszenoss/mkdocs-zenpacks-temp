# OpenStack (Provider View)

@lb[](img/zenpack-openstack-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.zenoss.OpenStackInfrastructure

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.OpenStackInfrastructure){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.OpenStackInfrastructure.git){.external-link}

### Applications Monitored:

OpenStack Cloud Computing

## OpenStack (Provider View) ZenPack

This ZenPack provides monitoring of OpenStack from a service provider
perspective. In addition to the user-oriented components (instances,
flavors, images), the underlying OpenStack servers and software are
monitored.

## Features

Monitors overall OpenStack state, including all tenants.

Monitors Nova, Neutron and Cinder health

Models and monitors Nova Services and components

Models and monitors Neutron Agents and components

Models and monitors Cinder Services and components

Impact and Root-Cause (Requires Zenoss Service Dynamics)

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

OpenStackInfrstructure 4.0.0 Supports Queens, Rocky, Ussuri, Train,
Victoria and Red Hat OpenStack Platform (RHOSP) version 13, 14 and 16

OpenStackInfrstructure 3.0.0 supports only Pike, Queens, and Rocky
releases of OpenStack.
OpenStack releases, prior to the Pike release, are not verified to work
with the OpenStackInfrastrucure 3.0.0 ZenPack.
Although the 3.0.0 ZenPack will work with the older AMQP based
Ceilometer integration, those versions of Ceilometer are not supported
by Zenoss.

## Releases

Version
4.0.0-[Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.OpenStackInfrastructure/4.0.0/ZenPacks.zenoss.OpenStackInfrastructure-4.0.0.egg){.external-link}

-   Released on 2021/08/05
-   Requires
    [PythonCollector](/zenoss/PythonCollector/zenpack.html), [OpenStack - Tenant View](/zenoss/OpenStack/zenpack.html), [Linux Monitor](/zenoss/LinuxMonitor/zenpack.html)
-   Compatible with Zenoss Cloud and Zenoss 6.5.0, 6.6.0

Version 3.0.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.OpenStackInfrastructure/3.0.1/ZenPacks.zenoss.OpenStackInfrastructure-3.0.1.egg){.external-link}:   Released on 2020/06/05:   Requires PythonCollector ZenPack,OpenStack (Tenant View)
    ZenPack,Linux Monitor ZenPack:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},[OpenStack     (Tenant View){.external-link}     ZenPack](https://help.zenoss.com/display/in/OpenStack+-+Tenant+View "ZenPack:OpenStack (Tenant View){.external-link}"),[Linux Monitor ZenPack](https://help.zenoss.com/display/in/Linux+Monitor "ZenPack:Linux Monitor"){.external-link}:   Compatible with Zenoss Cloud and Zenoss 6.4.1

Version 2.4.2- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.OpenStackInfrastructure/2.4.2/ZenPacks.zenoss.OpenStackInfrastructure-2.4.2.egg){.external-link}:   Released on 2018/08/15:   Requires PythonCollector ZenPack,OpenStack (Tenant View)
    ZenPack,Linux Monitor ZenPack:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},[OpenStack     (Tenant View){.external-link}     ZenPack](https://help.zenoss.com/display/in/OpenStack+-+Tenant+View "ZenPack:OpenStack (Tenant View){.external-link}"),[Linux Monitor ZenPack](https://help.zenoss.com/display/in/Linux+Monitor "ZenPack:Linux Monitor"){.external-link}:   Compatible with Zenoss 4.2 - 6.2

-   Contents
    -   [Gallery](#gallery)
    -   [Prerequisites](#prerequisites)
        -   [Supported OpenStack Releases](#supported-open-stack-releases)
    -   [Restricted Users](#restricted-users)
    -   [Organizational Elements](#organizational-elements)
        -   [Metrics](#metrics)
    -   [Installed Items](#installed-items)
        -   [Daemons](#daemons)
        -   [Configuration Properties](#configuration-properties)
        -   [Device Classes](#device-classes)
        -   [Modeler Plugins](#modeler-plugins)
        -   [Datasources](#datasources)
        -   [Monitoring Templates](#monitoring-templates)
        -   [Event Classes and Mappings](#event-classes-and-mappings)
        -   [Processes](#processes)
    -   [Zenpack Installation](#zenpack-installation)
        -   [First-Time Installation](#time-installation)
        -   [Upgrades from 2.4.x](#)
        -   [Post-ZenPack Installation](#zenpack-installation)
    -   [Device Setup](#devices-etup)
        -   [Device Setup via UI](#devices-etup-via-ui)
        -   [Device Setup via Zenbatchload](#devices-etup-via-zenbatchload)
        -   [Host Identification](#host-identification)
        -   [Modeling Containerized Environments](#modeling-containerized-environments)
    -   [OpenStack Configuration](#open-stack-configuration)
        -   [OpenStack Ceilometer Configuration](#open-stack-ceilometer-configuration)
    -   [Zenoss Analytics](#zenoss-analytics)
    -   [Service Impact and Root Cause Analysis](#service-impact-and-root-cause-analysis)
        -   [Recommended Impact Setup](#recommended-impact-setup)
        -   [Impact Relations](#impact-relations)
        -   [Examples](#examples)
    -   [Integration with other ZenPacks](#integration-with-other-zenpacks)
    -   [Known Issues](#known-issues)
    -   [Changes](#changes)
-   Gallery

<table>
<colgroup>
<col />
<col />
<col />
</colgroup>
<tbody>
<tr markdown="1">
<td>
<p><img src="img/zenpack-regions.png" /></p>
<p>Region</p>
</td>
<td>
<p><img src="img/zenpack-tenants.png" /></p>
<p>Tenants</p>
</td>
<td>
<p><img src="img/zenpack-availabilityzones.png" /></p>
<p>Availability Zones</p>
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-devicegraphs.png" /></p>
<p>Device Graphs</p>
</td>
<td><br />
</td>
<td>
<p><img src="img/zenpack-openstackcomponentview.png" /></p>
<p>Component View</p>
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-hosts.png" /></p>
<p>Hosts</p>
</td>
<td>
<p><img src="img/zenpack-hypervisors.png" /></p>
<p>Hypervisors</p>
</td>
<td>
<p><img src="img/zenpack-images.png" /></p>
<p>Images</p>
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-novaapis.png" /></p>
<p>Nova APIs</p>
</td>
<td>
<p><img src="img/zenpack-novaservices.png" /></p>
<p>Nova Services</p>
</td>
<td>
<p><img src="img/zenpack-neutronagents.png" /></p>
<p>Neutron Agents</p>
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-instances.png" /></p>
<p>Instances</p>
</td>
<td>
<p><img src="img/zenpack-vnics.png" /></p>
<p>vNICs</p>
</td>
<td><br />
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-networks.png" /></p>
<p>Networks</p>
</td>
<td>
<p><img src="img/zenpack-ports.png" /></p>
<p>Ports</p>
</td>
<td><br />
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-floatingips.png" /></p>
<p>Floating IPs</p>
</td>
<td>
<p><img src="img/zenpack-routers.png" /></p>
<p>Routers</p>
</td>
<td>
<p><img src="img/zenpack-subnets.png" /></p>
<p>Subnets</p>
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-cinderservices.png" /></p>
<p>Cinder Services</p>
</td>
<td>
<p><img src="img/zenpack-volumes.png" /></p>
<p>Volumes</p>
</td>
<td>
<p><img src="img/zenpack-volsnapshots.png" /></p>
<p>Volume Snapshots</p>
</td>
</tr>
</tbody>
</table>

-   Prerequisites
-   A supported OpenStack version (see below)
-   Administrative credentials for your OpenStack environment
    -   Username, password, keystone URL, Region
-   SSH access and credentials to the Linux devices in your OpenStack
    environment (See [Post-ZenPack-Installation Notes](#zenpack-installation-1))
-   Supported OpenStack Releases
-   2.3.x supports Mitaka
-   2.4.x supports Mitaka, Newton, and Ocata
-   3.0.0 supports Pike, Queens, Rocky, and Red Hat OpenStack Platform
    (RHOSP) version 13 and 14
-   Note: We denote Pike, Queens, and Rocky, RHOSP 13 and 14 as
    **Pike+**
-   Restricted Users
-   Restricted (non-administrator) users can also model and monitor
    OpenStack devices, with access to those devices consistent with that
    user&rsquo;s privileges. In other words, you should expect reduced
    visibility for restricted users.
-   A restricted should expect to see:
-   Fewer modeled components
-   Reduced monitored metrics
-   Absent events for missing components
-   In particular, restricted users can see diminished components and
    metrics for:
-   Cinder Pools
-   Cinder Services
-   Cinder Volumes
-   Hypervisors
-   Neutron Agents
-   Nova Services
-   Tenants
-   Any API item that requires administrator access
-   If you believe a user should have more access to data, it is your
    responsibility to adjust the user&rsquo;s access level on OpenStack.
-   Organizational Elements
-   The following organizational elements are discovered:
-   Regions
-   Availability Zones
-   Tenants
-   API Endpoints
-   The following virtual-machine elements are discovered:
-   Nova Services (processes supporting nova servers)
-   Instances (Servers)
-   Hosts
-   Hypervisors
-   Images
-   Flavors
-   The following network elements are discovered:
-   Neutron Agents
-   Networks
-   Subnets
-   Routers
-   Ports
-   Floating-Ips
-   vNICs
-   The following block storage elements are discovered:
-   Cinder Services (processes supporting block storage)
-   Volumes
-   Volume Snapshots
-   Volume Types
-   Storage Pools
-   Cinder Quotas
-   Metrics
-   The following component level metrics are collected:
-   Instances
-   CPU Utilization (percent)
-   Disk Requests (requests/sec)
-   Disk IO Rate (bytes/sec)
-   vNICs
-   Network Packet Rate (packets/sec)
-   Network Throughput (bytes/sec)
-   Hosts
-   Load Average (processes)
-   CPU Utilization (percent)
-   Free Memory (bytes)
-   Free Swap (bytes)
-   IO (sectors/sec)
-   Nova Services
-   CPU Utilization (percent)
-   Memory Utilization (bytes)
-   Process Count (processes)
-   Neutron Agents
-   CPU Utilization (percent)
-   Memory Utilization (bytes)
-   Process Count (processes)
-   Cinder Services
-   CPU Utilization (percent)
-   Memory Utilization (bytes)
-   Process Count (processes)
-   Volumes
-   Storage Utilization (percent)
-   Operation Throughput (operations/sec)
-   Merge Rate (merged/sec)
-   Sector Throughput (sectors/sec)
-   IO Operations (operations)
-   IO Utilization (percent)
-   Weighted IO Utilization (weighted percent)
-   Volume Snapshots
-   Storage Utilization (percent)
-   Operation Throughput (operations/sec)
-   Merge Rate (merged/sec)
-   Sector Throughput (sectors/sec)
-   IO Operations (operations)
-   IO Utilization (percent)
-   Weighted IO Utilization (weighted percent)
-   The following device level metrics are collected:
-   Flavors
-   Total (count)
-   Images
-   Total (count)
-   Total count per image state
-   Servers
-   Total (count)
-   Total count per server state
-   Queues
-   Event (count)
-   Performance (count)
-   Agents
-   Total (count)
-   Total count per agent type
-   Networks
-   Total (count)
-   Total count per network state
-   Routers
-   Total (count)
-   Total count per router state
-   Volumes
-   Total (count)
-   Total count per volume state
-   Volume Snapshots
-   Total (count)
-   Total count per volume snapshot state
-   Volume Pool
-   Total (count)
-   Total count per volume pool state
-   Installed Items
-   Once installed, the ZenPack installs the following properties and
    components.
-   Daemons
-   The following daemons are installed:

| Type                  | Name                                                    |
|-----------------------|---------------------------------------------------------|
| Modeler               | zenmodeler                                              |
| Performance Collector | zencommand, zenpython, zenopenstack, proxy-zenopenstack |

-   Configuration Properties

-   zOpenStackAuthUrl: The URL of the Identity endpoint.

-   zOpenStackExtraHosts: The list of extra hosts that will be added to
    the system once OpenStack Infrastructure device is modeled.

-   zOpenStackExtraApiEndpoints: A list of URLs to monitor for OpenStack
    APIs. Format is &lt;service type&gt;:&lt;full URL&gt; for each.

-   zOpenStackHostDeviceClass: Used as a default device class for
    defined hosts in zOpenStackExtraHosts and zOpenStackNovaApiHosts
    properties. Default is /Server/SSH/Linux/NovaHost.

-   zOpenStackNovaApiHosts: The list of hosts upon which nova-api runs.
    This is required when the IP address in the nova API URL does not
    match any known host.

-   zOpenStackCinderApiHosts: The list of hosts upon which cinder-api
    runs. This is required when the IP address in the cinder API URL
    does not match any known host.

-   zOpenStackHostMapToId: A list of &lt;name&gt;=&lt;id&gt;, used to
    force a host referred to by OpenStack with the given name to be
    represented in Zenoss as a host component with the given ID. (this
    is not commonly used)

-   zOpenStackHostMapSame: A list of &lt;name1&gt;=&lt;name2&gt;, used
    to inform the modeler that the same host may be referred to with an
    alternate name by some part of OpenStack. (this is not commonly
    used)

-   zOpenStackNeutronConfigDir: Path to directory that contains Neutron
    configuration files. Default is /etc/neutron.

-   zOpenStackProjectId: Corresponds to tenant name, project to work on.

-   zOpenStackRegionName: The name of the OpenStack Region to use.
    Regions are autonomous OpenStack clouds joined together through
    shared Keystone identity server and managed through a common
    interface.

-   zOpenStackRunNovaManageInContainer,
    zOpenStackRunVirshQemuInContainer,
    zOpenStackRunNeutronCommonInContainer: Used when OpenStack processes
    are running inside of docker containers. Provide the container names
    (or a pattern to match them) here, or leave blank in a
    non-containerized OpenStack environment.

-   zOpenStackHostLocalDomain: When OpenStack hosts report names ending
    in .localdomain, replace domain with this value.

-   zOpenStackAMQPUsername: Username for Ceilometer AMQP integration.

-   zOpenStackAMQPPassword: Password for Ceilometer AMQP integration.

-   zOpenStackProcessEventTypes: List of OpenStack event types to pass
    to Zenoss event system. (Other event types may be processed for
    model changes, but will not be stored as events in Zenoss)

-   zOpenStackIncrementalShortLivedSeconds: Incremental Modeling - Delay
    component creation this period of time until no deletions are
    detected. (seconds)

-   zOpenStackIncrementalBlackListSeconds: Incremental Modeling - Once a
    component is deleted, wait this interval between attempts to remodel
    same component to avoid flapping. (seconds)

-   zOpenStackIncrementalConsolidateSeconds: Incremental Modeling - Wait
    this amount of time to aggregate components&rsquo; properties before
    updating a component map. Ignored by deletions. (seconds)

-   zOpenStackUserDomainName: Domain name containing opentstack user for
    authorization scope.

-   zOpenStackProjectDomainName: Domain name containing opentstack
    project for authorization scope.

-   Device Classes

-   /OpenStack: Root OpenStack device class. Typically, devices should
    not be put in this device class.

-   /OpenStack/Infrastructure: Device class for OpenStack Infrastructure
    endpoints.

-   /Server/SSH/Linux/NovaHost: Device class for Nova host instances.

-   Modeler Plugins

-   zenoss.OpenStackInfrastructure: Main modeler plugin- Queries the
    OpenStack APIs to populate the zenoss model.

-   zenoss.cmd.linux.openstack.hostfqdn: Used to get OpenStack host
    FQDN.

-   zenoss.cmd.linux.openstack.inifiles: Used to gather neutron.conf and
    ml2_conf.ini files.

-   zenoss.cmd.linux.openstack.libvirt: Used to get OpenStack instance
    virtual NIC information using libvert.

-   zenoss.cmd.linux.openstack.nova: Used to get installed OpenStack
    version.

-   Datasources

-   ApiEndpointStatusDataSource: Checks that API endpoints are
    available.

-   CinderServiceStatusDataSource: Checks the status of Cinder services
    via the Cinder API.

-   EventsAMQPDataSource: Stores events received from OpenStack
    Ceilometer via AMQP.

-   NeutronAgentStatusDataSource: Checks the status of Neutron agents
    via the Neutron API.

-   NovaServiceStatusDataSource: Checks the status of Nova services via
    the Nova API.

-   PerfAMQPDataSource: Stores performance data received from OpenStack
    Ceilometer.

-   QueueSizeDataSource: Checks the number of unprocessed messages in
    Ceilometer AMQP queues.

-   Notes

-   As of the Pike+ (Late 2017) OpenStack release, the dispatcher
    mechanism previously used by this zenpack is no longer supported by
    Ceilometer. Because of this, the &ldquo;heartbeat&rdquo; mechanism that was
    previously used to verify connectivity between Ceilometer and Zenoss
    is no longer possible, and /Status/Heartbeat events will not be
    created if Zenoss stops receiving data from Ceilometer.

    Connectivity problems between Ceilometer and Zenoss will still be
    reported in the Ceilometer agent-notification.log file on the
    OpenStack hosts.

-   All `OpenStack Ceilometer Perf AMQP` datasources&rsquo; *cycletime*
    parameter will not work in Pike+ . Cycletime must be regulated in
    OpenStack itself. The *cycletime* setting is still present for
    backward compatibility with Ocata and prior versions, but has no
    effect.

-   Monitoring Templates

-   /OpenStack/Infrastructure/
    -   Endpoint
    -   Instance
    -   vNIC

-   Event Classes and Mappings

-   /OpenStack
    -   OpenStack Events Default

-   /OpenStack/Cinder

-   /OpenStack/Cinder/Snapshot
    -   Cinder Snapshot default mapping

-   /OpenStack/Cinder/Volume
    -   cinder.volume default mapping

-   /OpenStack/compute

-   /OpenStack/compute/instance
    -   compute.instance default mapping
    -   compute.instance.create.error
    -   compute.instance.exists
    -   compute.instance.exists.verified.old

-   /OpenStack/dhcp_agent
    -   dhcp_agent default mapping

-   /OpenStack/firewall
    -   firewall default mapping

-   /OpenStack/firewall_policy
    -   firewall_policy default mapping

-   /OpenStack/firewall_rule
    -   firewall_rule default mapping

-   /OpenStack/floatingip
    -   floatingip default mapping

-   /OpenStack/network
    -   network default mapping

-   /OpenStack/port
    -   port default mapping

-   /OpenStack/router
    -   router default mapping

-   /OpenStack/security_group
    -   security_group default mapping

-   /OpenStack/security_group_rule
    -   security_group_rule default mapping

-   /OpenStack/subnet
    -   subnet default mapping

-   /Status
    -   openStackCinderServiceStatus
    -   openStackIniFileAccess
    -   openStackIniFileOptionParsing
    -   openStackNeutronAgentStatus
    -   openStackNovaServiceStatus
    -   openStackApiEndpointStatus

-   Processes

-   /OpenStack

-   /OpenStack/ceilometer-agent-central

-   /OpenStack/ceilometer-agent-compute

-   /OpenStack/ceilometer-agent-notification

-   /OpenStack/ceilometer-alarm-evaluator

-   /OpenStack/ceilometer-alarm-notifier

-   /OpenStack/ceilometer-api

-   /OpenStack/ceilometer-collector

-   /OpenStack/ceilometer-polling

-   /OpenStack/cinder-api

-   /OpenStack/cinder-backup

-   /OpenStack/cinder-scheduler

-   /OpenStack/cinder-volume

-   /OpenStack/glance-api

-   /OpenStack/glance-registry

-   /OpenStack/gnocchi-metricd

-   /OpenStack/gnocchi-statsd

-   /OpenStack/keystone-admin

-   /OpenStack/keystone-all

-   /OpenStack/keystone-main

-   /OpenStack/neutron-dhcp-agent

-   /OpenStack/neutron-l3-agent

-   /OpenStack/neutron-lbaas-agent

-   /OpenStack/neutron-metadata-agent

-   /OpenStack/neutron-metering-agent

-   /OpenStack/neutron-openvswitch-agent

-   /OpenStack/neutron-server

-   /OpenStack/nova-api

-   /OpenStack/nova-cert

-   /OpenStack/nova-compute

-   /OpenStack/nova-conductor

-   /OpenStack/nova-consoleauth

-   /OpenStack/nova-network

-   /OpenStack/nova-scheduler

-   /OpenStack/rabbitmq-server

-   Zenpack Installation

-   First-Time Installation

-   If you are installing the ZenPack for the first time, install as per
    usual ZenPack installation, and continue to *Post-ZenPack
    Installation*.

-   Upgrades from 2.4.x

-   If this is the first time you are upgrading to 3.0.0+ from a version
    of the zenpack 2.4.0 or earlier, there are no special steps
    required, nor any changes required on the OpenStack side.

-   When upgrading from 2.4.x on a system with multiple collectors, you
    may see warnings such as &ldquo;ERRO\[0000\] Could not update proxy&rdquo;, as
    described in [ZPS-4689](#known-issues-1).
    These can be safely ignored.

-   If you are using the *ceilometer_zenoss* dispatcher mechanism (with
    RabbitMQ) for integrating older versions of openstack with zenoss,
    this will still function with 3.0.0. Note that this is only
    supported as a bridge for old openstack environment which have not
    yet been upgraded to a supproted version of OpenStack. All currently
    supported versions use the *http publisher* mechanism to integrate
    with zenoss, rather than RabbitMQ.

-   Post-ZenPack Installation

-   Because the zenopenstack and RabbitMQ-Ceilometer services run on
    each collector, in order for openstack ceilometer to send messages
    to them, they need to be assigned a specific IP address. These
    services will be unable to start until IP assignment is completed.
    (The error &lsquo;service is missing an address assignment&rsquo; will be
    displayed if you try to start the service)

-   The IP assignment may be performed via the Control Center UI or
    command-line.

-   To use the UI:

-   Log into the Control Center UI.

-   Click the Zenoss.resmgr name to display the
    Applications/Zenoss.resmgr page.

-   Scroll down the page to the IP Assignments section and click
    &lsquo;Assign&rsquo; next

-   to each line for the proxy-openstack and RabbitMQ-Ceilometer
    services:

-   @lb[](img/zenpack-ip_assignment.png)

-   To use the command-line:

-   ~~~ sourceCode
    serviced service assign-ip RabbitMQ-Ceilometer serviced service assign-ip proxy-zenopenstack
    ~~~

-   If you have multiple collectors, specify the collector name for each
    service and repeat for each collector:

-   ~~~ sourceCode
    serviced service assign-ip collector1/RabbitMQ-Ceilometer serviced service assign-ip collector1/proxy-zenopenstack serviced service assign-ip collector2/RabbitMQ-Ceilometer serviced service assign-ip collector2/proxy-zenopenstack
    ~~~

-   Once the zenpack is installed, provide SSH credentials to the Linux
    devices in your OpenStack environment before adding any devices. \*
    Configure the zCommandUsername/zCommandPassword/zKeyPath properties
    on the /Devices/Server/SSH/Linux/NovaHost device class. \* If your
    OpenStack nodes are already managed under Zenoss, move them into
    /Devices/Server/SSH/Linux/NovaHost

-   Device Setup

-   Device Setup via UI

-   Once the OpenStack ZenPack is installed and you can begin monitoring
    by going to the infrastructure screen and clicking the normal button
    for adding devices. You&rsquo;ll find a new option labeled, &ldquo;Add OpenStack
    Endpoint (Infrastructure).&rdquo;

-   Choose that option and you&rsquo;ll be presented with a dialog asking for
    the following inputs.

-   Device To Create - non-empty, non-ip, non-dns, unique name to use
    for this device in Zenoss. &lsquo;&rsquo;See note below&rsquo;&rsquo;.

-   Auth URL - A keystone URL. For Keystone&rsquo;s v3 API, it should look
    like `http://<hostname>:5000/v3/`.
    For Keystone&rsquo;s v2 API, it should look like
    `http://<hostname>:5000/v2.0/`. To have the ZenPack choose the
    newest supported API version, leave the path off, like
    `http://<hostname>:5000/` (sets zOpenStackAuthUrl).

-   Username: Enter your OS_USERNAME (sets zCommandUsername).

-   Password: Enter your OS_PASSWORD (sets zCommandPassword).

-   User Domain Name: Enter the user domain name per OS_USER_DOMAIN_NAME
    (sets zOpenStackUserDomainName).

-   Project Domain Name: Enter the project domain name per
    OS_PROJECT_DOMAIN_NAME (sets zOpenStackDomainName).

-   Region Name - choose the correct region from the drop-down. You may
    only choose one, so each region you wish to manage must be
    registered as a separate endpoint in Zenoss (sets
    zOpenStackRegionName).

-   Once you click Add, Zenoss will contact the OpenStack API and
    discover servers, images and flavors. Once it is complete you&rsquo;ll
    find a new device in the OpenStack device class with the same name
    as the hostname or IP you entered into the dialog. Click into this
    new device to see everything that was discovered.

-   NOTE: The &lsquo;Device name&rsquo; should be a non-empty, non-hostname, non-IP,
    since that name will be used when the host is registered as a Linux
    device. The name should be unique within the Zenoss environment.
    This is especially important if you are adding another device that
    share the same IP address or hostname that already exist on another
    device. Not doing this may result in devices with the same name
    conflicting with each other. (e.g. attempting to model device would
    show modeling results that belong to another device OR device would
    show relations that do not belong to that device)

-   Device Setup via Zenbatchload

-   You can setup the device using *zenbatchload* as follows:

-   ~~~ sourceCode
    zenbatchload <filename>
    ~~~

-   where `<filename>` should have the form:

-   `/Devices/OpenStack/Infrastructure loader='openstackinfrastructure',\ loader_arg_keys=['deviceName', 'username', 'api_key', 'project_id, 'user_domain_name', 'project_domain_name', 'auth_url', 'region_name', 'collector'] <devicename> username='<username>', api_key='<password>', project_id='<tenant ID>', user_domain_name='default', \ project_domain_name='default', auth_url='http://<ip address>:5000/v2.0/', region_name='RegionOne' /Devices/Server/SSH/Linux/NovaHost zCommandUsername='myusername', zCommandPassword='mypassword'`

-   As mentioned before, zCommandUsername and zCommandPassword
    properties must be set for /Devices/Server/SSH/Linux/NovaHost
    devices (and vNICs) to be correctly modeled.

-   Host Identification

-   The OpenStack APIs do not contain an authoritative list of hosts
    with unique IDs. Instead, various APIs show hosts by name or IP.
    There zenpack does its best to identify IPs and names that refer to
    the same host, and represent them as a single host component. In
    some cases, though, it can&rsquo;t tell, and the same host may be modeled
    twice, or with an incorrect name.

-   Two zProperties are provided to override the default behavior of the
    zenpack when this happens.

-   zOpenStackHostMapSame

    Specifies that two names refer to the same host. It is a list of
    entries of the form: `<name1>=<name2>` For example,

        my.example.com=myothername.example.com my.example.com=10.1.1.1

    This means that any time the host &ldquo;my.example.com&rdquo;,
    &ldquo;myothername.example.com&rdquo;, or &ldquo;10.1.1.1&rdquo; is encountered, they will
    be considered to be the same host, rather than separate ones.

-   zOpenStackHostMapToId

    It is also possible to specify not only that the devices are the
    same, but that they should be identified with one specific
    identifier (otherwise, one may be chosen at random). In this case, a
    list of entries of the form `<name>=<id>` may be provided in the
    zOpenStackHostMapToId zProperty. For example,
    `myothername.example.com=my.example.com 10.1.1.1=my.example.com`
    This would cause &ldquo;my.example.com&rdquo;, &ldquo;myothername.example.com&rdquo;, or
    &ldquo;10.1.1.1&rdquo; to all be definitely identified as &ldquo;my.example.com&rdquo;,
    without the ambiguity that could exist if zOpenStackHostMapSame were
    used.

-   zOpenStackHostLocalDomain

    In some environments (in particular, the Red Hat OpenStack
    Platform), hosts are assigned names that end in &lsquo;.localdomain&rsquo;. This
    would cause problems for Zenoss, because it is not possible to
    create a device in Zenoss with such a name, as they all resolve to
    127.0.0.1, rather than their actual IP.

    The default value of zOpenStackHostLocalDomain is a blank string,
    meaning that the &lsquo;.localdomain&rsquo; suffix will be stripped from host
    names, and devices will be created in Zenoss with those shortened
    names. If those names do not resolve in DNS, they will be created
    without IPs, and will not be modeled. You would need to manually set
    their management IPs so that they can be modeled.

    Alternatively, if you already have these hostnames in dns, but just
    with a different domain name than &ldquo;.localdomain&rdquo;, you may specify
    this domain name here, and it will be substituted for localdomain,
    and the devices will model automatically, based on the IPs returned
    from DNS.

-   Modeling Containerized Environments

-   If the target OpenStack environment runs processes inside of docker
    containers, it is necessary to configure several zProperties before
    modeling will succeed.

-   zOpenStackRunNovaManageInContainer: Container to run &ldquo;nova-manage&rdquo;
    in

-   zOpenStackRunVirshQemuInContainer: Container to run &ldquo;virsh&rdquo; in

-   zOpenStackRunNeutronCommonInContainer: Container to access neutron
    configuration files in.

-   These should be set to container names or substrings of the
    container names. These can be set on the /Server/SSH/Linux/NovaHost
    device class or specific devices within it, as necessary.

-   NOTE: These zProperties must be set on the Linux devices, not the
    OpenStack (/OpenStack/Infrastructure) devices.

-   OpenStack Configuration

-   Before event and performance data can be collected, the following
    steps must be performed. That these steps are only tested with
    currently-supported versions of OpenStack (Pike and higher).

-   OpenStack Ceilometer Configuration

-   Ceilometer is a component of openstack which, through a combination
    of polling and notifications from the openstack message bus, collect
    a variety of metric and event data from the openstack environment
    and forwards it to external services, including Zenoss, for
    processing.

-   @lb[](img/zenpack-ceilometer_arch.png)

-   Ceilometer&rsquo;s polling agent and other openstack services (nova-api,
    for instance) send notifications through an internal notification
    bus, which are received by the ceilometer notification agent. It
    then passes these notifications through configurable &ldquo;pipelines&rdquo;,
    which ultimately deliver the data through publishers.

-   In 2.4.x of this ZenPack, a custom ceilometer plugin called
    &lsquo;ceilometer_zenoss&rsquo; was used to send the data to zenoss through the
    RabbitMQ-Ceilometer service.

-   This approach was no longer practical with current versions of
    OpenStack, so the collection mechanism was changed to use
    ceilometer&rsquo;s built-in http publisher, rather than AMQP. Since the
    http publisher is part of ceilometer, there is no need to install
    additional software on the OpenStack environment to use this
    mechanism. It is only necessary to configure it correctly, as
    described below.

-   Ceilometer must be configured to send data to the correct Zenoss
    collector, using a device-specific URL.

-   The OpenStack environment will therefore need https access to the
    zenoss collector, and the Zenoss collector IP must be configured as
    described in the [Post-ZenPack-Installation Notes](#zenpack-installation-1).

-   Once the device is added, and its collector&rsquo;s proxy-zenopenstack
    service has an assigned IP, the following two URLs will be displayed
    at the bottom of the device&rsquo;s overview page:

-   @lb[](img/zenpack-ceilometer_urls.png)

-   These URLs will be required to configure ceilometer on the OpenStack
    environment to send data to Zenoss. There are two ways to configure
    ceilometer:

-   RHOSP Configuration using TripleO (RedHat OpenStack Platform
    Director)

-   This is the best way to configure the Redhat OpenStack Platform.

-   Add the following to your environment template:

-   `ManagePipeline: true PipelinePublishers: - *Zenoss Samples Publisher URL* - <other_pipeline_publishers> ManageEventPipeline: true EventPipelinePublishers: - *Zenoss Events Publisher URL* - <other_event_pipeline_publishers>`

-   Where the publisher URLs are device-specific, and copied from the
    device overview page shown above. For example:

-   `ManagePipeline: true PipelinePublishers: - https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack?verify_ssl=False ManageEventPipeline: true EventPipelinePublishers: - https://1.2.3.4:8342/ceilometer/v1/events/myopenstack?verify_ssl=False`

-   If desired, multiple publisher URLs may be specified, for instance
    to publish to more than one zenoss instance, or to other openstack
    systems such as gnocchi or panko. Note, however, that ceilometer
    will publish data to every publisher sequentially, so if one of the
    URLs is timing out, it will block ceilometer and slow down the
    publishing of data to Zenoss. Therefore, it is advisable to make
    sure that the URLs specified are valid and functioning.

-   This template must be ***rendered*** into your templates before you
    initiate a deployment from Undercloud.
    For more information on RHOSP template management, see RedHat&rsquo;s
    [Including Environment Files in Overcloud Creation](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/13/html-single/advanced_overcloud_customization/index#sect-Including_Environment_Files_in_Overcloud_Creation){.external-link}.

-   After deployment is complete, go to the undercloud, SSH into
    controller and go to `/etc/ceilometer` in
    ceilometer_agent_notification container to check if `pipeline.yaml`
    and `event_pipeline.yaml` file is updated:

         ssh heat-admin@<controller ip> sudo su - sudo docker exec --user 0 -it ceilometer_agent_notification /bin/bash # Ensure your configuration had the right publishers

-   Add Zenoss specific extensions to the Ceilometer event definitions:

    Edit `/etc/ceilometer/event_definitions.yaml` and add the contents
    of
    [zenoss_additions.yaml](https://raw.githubusercontent.com/zenoss/ZenPacks.zenoss.OpenStackInfrastructure/master/event_definitions/zenoss_additions.yaml){.external-link}
    to the bottom of the file.

-   Restart the ceilometer-notification service on all controller nodes.

-   Manual Configuration

-   When RedHat OpenStack Platform is not being used, you will need to
    update the affected configuration files directly. The following
    modifications are required on every controller node where ceilometer
    is running:

-   Add Zenoss specific extensions to the Ceilometer event definitions:

    Edit `/etc/ceilometer/event_definitions.yaml` and add the contents
    of
    [zenoss_additions.yaml](https://raw.githubusercontent.com/zenoss/ZenPacks.zenoss.OpenStackInfrastructure/master/event_definitions/zenoss_additions.yaml){.external-link}
    to the bottom of the file.

-   The /etc/ceilometer/event_pipeline.yaml file contains one sink,
    named `event_sink`. In its publishers section, add the event URL
    from above:

    For example:

        --- sources: - name: event_source events: - "*" sinks: - event_sink sinks: - name: event_sink transformers: triggers: publishers: - https://1.2.3.4:8342/ceilometer/v1/events/myopenstack?verify_ssl=False - <some_other_publisher>

-   The /etc/ceilometer/pipeline.yaml add the samples URL to the publish
    sections for the three sinks, cpu_sink, disk_sink, and network_sink:

    For example:

        --- sources: - name: meter_source meters: - "*" sinks: - meter_sink ... etc ... sinks: - name: meter_sink transformers: publishers: - https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack?verify_ssl=False - <some_other_publisher> - name: cpu_sink transformers: - name: "rate_of_change" parameters: target: name: "cpu_util" unit: "%" type: "gauge" max: 100 scale: "100.0 / (10**9 * (resource_metadata.cpu_number or 1))" publishers: - https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack?verify_ssl=False - <some_other_publisher> - name: disk_sink transformers: - name: "rate_of_change" parameters: source: map_from: name: "(disk\\.device|disk)\\.(read|write)\\.(bytes|requests)" unit: "(B|request)" target: map_to: name: "\\1.\\2.\\3.rate" unit: "\\1/s" type: "gauge" publishers: - https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack?verify_ssl=False - <some_other_publisher> - name: network_sink transformers: - name: "rate_of_change" parameters: source: map_from: name: "network\\.(incoming|outgoing)\\.(bytes|packets)" unit: "(B|packet)" target: map_to: name: "network.\\1.\\2.rate" unit: "\\1/s" type: "gauge" publishers: - https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack?verify_ssl=False - <some_other_publisher>

-   Make sure you restart ceilometer-notification service whenever you
    change `pipeline.yaml` or `event_pipeline.yaml`.

-   Configure nova to send events to ceilometer when instance state
    changes occur. (This step is optional, but recommended.) Add the
    following settings to `/etc/nova/nova.conf` on all compute nodes:

        [notifications] notify_on_state_change=vm_and_task_state [oslo_messaging_notifications] driver = messagingv2

-   Configure neutron to send events for ceilometer to forward to
    zenoss. Add the following settings to `/etc/neutron/neutron.conf`:

        [oslo_messaging_notifications] driver = messagingv2 topics = notifications

-   Ceilometer Troubleshooting

-   A variety of errors can be returned by zenopenstack to ceilometer.
    Here are the most common ones.

-   The errors would be found in
    `/var/log/ceilometer/agent-notification.log` on the OpenStack
    controller nodes.

-   Connection Refused

        ERROR ceilometer.pipeline.sample ConnectionError: HTTPSConnectionPool(host='1.2.3.4', port=8342): Max retries exceeded with url: /ceilometer/v1/samples/myopenstack (Caused by NewConnectionError('<requests.packages.urllib3.connection.VerifiedHTTPSConnection object at 0x7f80d1e89590>: Failed to establish a new connection: [Errno 111] Connection refused',))

    Verify that the IP address is correct and that the
    proxy-zenopenstack service is running.

-   Network Connectivity

        ERROR ceilometer.pipeline.event ConnectTimeout: HTTPSConnectionPool(host='1.2.3.4', port=8342): Max retries exceeded with url: /ceilometer/v1/events/myopenstack (Caused by ConnectTimeoutError(<requests.packages.urllib3.connection.VerifiedHTTPSConnection object at 0x7f4307dc94d0>, 'Connection to 1.2.3.4 timed out. (connect timeout=5)')) ERROR ceilometer.pipeline.event ConnectionError: HTTPSConnectionPool(host='1.2.3.4', port=8342): Max retries exceeded with url: /ceilometer/v1/events/myopenstack (Caused by NewConnectionError('<requests.packages.urllib3.connection.VerifiedHTTPSConnection object at 0x7f0b78e686d0>: Failed to establish a new connection: [Errno 113] No route to host',))

    Ensure that the correct IP was specified and that it is reachable
    from the OpenStack hosts.

-   Bad Gateway

        ERROR ceilometer.publisher.http HTTPError: 502 Server Error: Bad Gateway for url: https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack

    In general, this indicates that proxy-zenopenstack is running, but
    zenopenstack is not.
    This can be normal during a zenoss restart, but if it does not
    resolve, check the status of the zenopenstack service.

-   404 Errors (Not Found)

        ERROR ceilometer.publisher.http HTTPError: 404 Client Error: Not Found for url: https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack

    This usually indicates that the device ID found in the url is not
    recognized. Check the URL and make sure the device ID is correct.

    This can be normal during zenopenstack restarts, since it will not
    know about devices to be monitored until it lots the configuration
    from zenhub. If this is the case, it will resolve in a few minutes.

    It is also possible to get a 404 error because of a typo in the URL
    unrelated to the device ID.

-   422 Errors (Unprocessable Entity)

        ERROR ceilometer.publisher.http HTTPError: 422 Client Error: Unknown Status for url: https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack

    This error indicates that the payload of the http request sent to
    zenoss was not in the expected format. The most common cause for
    this is putting the samples url in event_pipeline.json, or the
    events url in pipeline.json.
    Ensure that the correct URL was put in the right file.

-   Additional zenopenstack debugging is possible through the
    &ldquo;zenopenstack diagnostics&rdquo; link under &ldquo;show links&rdquo; on the device&rsquo;s
    detail page. This link connects your browser directly to
    zenopensatck and provides detailed debugging information, including
    request rates and a log of all recently received http messages. Note
    that this option requires that your browser have https connectivity
    to the Zenoss collector.

-   General Notes

-   In prior versions of this zenpack, all events from ceilometer were
    forwarded to zenoss under /OpenStack. Since most events were not
    actionable, they were used to update the model (for instance, a new
    instance is created), but were immedaitely archived. In version
    3.0.0, these events are still used for incremental model updates,
    but are not stored in zenoss as events any more (since they placed
    additional load on zenoss for no benefit).

    If there is a ceilometer event type which is actually useful to
    track in zenoss as an event, that capability still exists, however.
    The list of event types to be exposed to zenoss are configurable in
    `zOpenStackProcessEventTypes`.

    By default, this only contains `compute.instance.create.error`, but
    other types may be added if desired.

-   The Instance metrics for *Disk IO Rate* are deprecated in OpenStack
    version Queens and later. Collection for those metrics will be
    missing. Future OpenStack releases will remove these metrics and
    graphs completely.

    In the meantime, if you still require these metrics, you can edit
    the OpenStack Ceilometer configuration /etc/ceilometer/polling.yaml
    and add the following to the *meters* section:

         - disk.read.bytes - disk.read.requests - disk.write.bytes - disk.write.requests

    After editing this file, ensure the resulting YAML syntax is valid
    and restart the ceilometer-polling service.

    Finally, note that these metrics ARE deprecated and will be removed
    in future releases of OpenStack itself.

-   The OpenStack ZenPack relies upon standard zenoss Linux Monitoring
    for some functions, including process monitoring and the modeling of
    vNICs. This means that the Zenoss collectors require SSH access to
    the NovaHost devices. In some OpenStack deployments (including
    RHOSP&rsquo;s overcloud), external SSH access may not be available by
    default, and additional configuration may be required to achieve it.

-   Zenoss Analytics

-   This ZenPack provides additional support for Zenoss Analytics.
    Perform the following steps to install extra reporting resources
    into Zenoss Analytics after installing the ZenPack.

1.  Copy vsphere-analytics.zip from
    `$ZENHOME/ZenPacks/ZenPacks.zenoss.OpenStackInfrastructure*/ZenPacks/zenoss/OpenStackInfrastructure/analytics/`
    on your Zenoss server.
2.  Navigate to Zenoss Analytics in your browser.
3.  Login as superuser.
4.  Remove any existing *OpenStackInfrastructure ZenPack* folder.
    1.  Choose *Repository* from the *View* menu at the top of the page.
    2.  Expand *Public* in the list of folders.
    3.  Right-click on *OpenStackInfrastructure ZenPack* folder and
        choose *Delete*.
    4.  Confirm deletion by clicking *OK*.
5.  Add the new *OpenStackInfrastructure ZenPack* folder.
    1.  Choose *Server Settings* from the &lsquo;&rsquo;Manage&rsquo; menu at the top of
        the page.
    2.  Choose *Import* in the left page.
    3.  Remove checks from all check boxes.
    4.  Click *Choose File* to import a data file.
    5.  Choose the OpenStackInfrastructure-analytics.zip file copied
        from your Zenoss server.
    6.  Click *Import*.

-   You can now navigate back to the &lsquo;&rsquo;OpenStackInfrastructure ZenPack&rsquo;&rsquo;
    folder in the repository to see the following resources added by the
    bundle.
-   Domains
    -   OpenStackInfrastructure Domain
-   Ad Hoc Views
    -   OpenStack Instance List
-   The OpenStackInfrastructure Domain can be used to create ad hoc
    views using the following steps.

1.  Choose *Ad Hoc View* from the *Create* menu.
2.  Click *Domains* at the top of the data chooser dialog.
3.  Expand *Public* then *OpenStackInfrastructure ZenPack*.
4.  Choose the *OpenStackInfrastructure Domain* domain

-   Service Impact and Root Cause Analysis
-   When combined with the Zenoss Service Dynamics product, this ZenPack
    adds built-in service impact and root cause analysis capabilities
    for OpenStack infrastructure and instances. The service impact
    relationships shown in the diagram and described below are
    automatically added. These will be included in any services that
    contain one or more of the explicitly mentioned components.
-   @lb[](img/zenpack-impact.png)
-   Recommended Impact Setup
-   Since most components will be related to Tenants and Region we
    recommend:
-   Navigate to Services (Impact)
-   Add a Dynamic Service to your Services tab
-   Add all Tenants to the Dynamic Service
-   Add all Regions to the Dynamic Service
-   Impact Relations
-   Component failures will affect Impact as follows:
-   Internal Impact Relationships
-   OpenStack API endpoint impacts all Hosts
-   Availability zone impacts associated Region
-   Host impacts associated Hypervisors, Nova Services, Cells, Nova
    Apis, Neutron Agents, and Cinder Services
-   Hypervisor impacts the resident Instances (VMs)
-   Nova Service affects the Availability Zone or Region that it
    supports
-   Instance impacts the associated Tenant
-   vNIC impacts the related Instance.
-   Port impacts associated Instance
-   Subnet impacts associated Ports and Tenants
-   Floating-IP impacts associated Port
-   Network impacts associated Subnets and Tenants
-   Router impacts associated Subnets and Floating-ips
-   Neutron Agent impacts associated Networks, Subnets and Routers
-   volume impacts Instances (VMs), Volume Snapshots
-   External Impact Relationships
-   Instance impacts guest operating system device.
-   Cisco UCS vNIC impacts related host&rsquo;s underlying Linux device NIC.
-   Cisco UCS service profile impacts host&rsquo;s underlying Linux device.
-   Host impacted by associated Linux device.
-   OS Processes on an underlying Linux device impact corresponding Nova
    APIs, Nova Services, Neutron Agents and Cinder Services on Host.
-   Examples

<table>
<colgroup>
<col />
<col />
</colgroup>
<tbody>
<tr markdown="1">
<td>
<p><img src="img/zenpack-impact_instance.png" /></p>
<p>Impact (Instance)</p>
</td>
<td>
<p><img src="img/zenpack-impact_ports.png" /></p>
<p>Impact (Network)</p>
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-impact_region.png" /></p>
<p>Impact (Region)</p>
</td>
<td>
<p><img src="img/zenpack-impact_tenant.png" /></p>
<p>Impact (Tenant)</p>
</td>
</tr>
</tbody>
</table>

-   Integration with other ZenPacks

-   In some cases, the underlying network or storage technology is
    monitored by a different zenpack. The OpenStackInfrastructure
    zenpack is able to integrate with the following ZenPacks to provide
    component-level linkage and impact model integration:

-   Neutron OpenvSwitch ml2 plugin &lt;-&gt;
    [OpenvSwitch](https://help.zenoss.com/display/in/OpenvSwitch){.external-link}
    ZenPack

-   Neutron APIC ml2 plugin &lt;-&gt; [Cisco APIC](https://help.zenoss.com/display/in/Cisco+APIC){.external-link} ZenPack

-   Neutron NSX ml2 plugin &lt;-&gt; [VMWare NSX](https://help.zenoss.com/display/in/VMware+NSX){.external-link} ZenPack

-   Cinder LVM logical volumes &lt;-&gt; [Linux Monitor](https://help.zenoss.com/display/in/Linux+Monitor){.external-link} ZenPack
    (&gt;= 2.0.0)

-   Ceph RBD volumes &lt;-&gt;
    [Ceph](https://help.zenoss.com/display/in/Ceph){.external-link} ZenPack

-   Known Issues

-   [ZEN-17905](https://jira.zenoss.com/browse/ZEN-17905){.external-link}:
    Nova APIs component: Grey icons for Enabled and State after
    model/monitor.

    -   OpenStack nova service API does not provide information about
        Nova-API, so its status is, in fact, unknown.

-   [ZPS-1762](https://jira.zenoss.com/browse/ZPS-1762){.external-link}:
    When using OpenvSwitch integration, the Linux devices must be added
    to the system first (normally through automatic discovery by the
    OpenStackInfrastructure ZenPack) before the corresponding
    OpenvSwitch devices are registered. This is because the two devices
    use the same management IP address, and a special exclusion is in
    place for OpenvSwitch devices, allowing them to be added after the
    Linux device, but not the other way around.

-   [ZPS-2004](https://jira.zenoss.com/browse/ZPS-2004){.external-link}:
    When adding an OSI device, if the same host is already added as a
    generic device (such as /SSH/Linux), the host device&rsquo;s device class
    will be changed, and an error generated, preventing modeling. As a
    workaround, remove the Linux device before adding the OSI device.

-   [ZPS-4742](https://jira.zenoss.com/browse/ZPS-4742){.external-link}:
    Networking functions through SR-IOV and OVS-DPDK used in NFV like
    setups are not supported. Ceilometer is not able to collect
    monitoring data for these interfaces and hence Zenoss doesn&rsquo;t have
    any insight into these interfaces. This is because legacy Ceilometer
    only supports traditional OpenvSwitch networking, where a TAP
    interface is created through libvirt.

-   [ZPS-5468](https://jira.zenoss.com/browse/ZPS-5468){.external-link}:
    Newly deployed RabbitMQ-Ceilometer service can fail to start, with
    an error `badmatch,{error,{no_such_vhost,<<"/">>}}`. When this
    occurs, all health checks for the service will fail.

    If this error is encountered, the simplest fix seems to be to attach
    to the affected container, then run:

         rm -rf /var/lib/rabbitmq/mnesia*/rabbit@rbt-ceil0

    and restart the service.

-   [ZPS-4689](https://jira.zenoss.com/browse/ZPS-4689){.external-link}:
    During upgrades you can see an error like:

         ERRO[0000] Could not update proxy

    You can safely ignore this error, which should stop after the
    upgrade is completed.

-   Changes

-   3.0.1

-   Add support for Twisted library update (ZPS-6975)

-   Tested with Zenoss Resource Manager 6.4.1, Zenoss Cloud and Service
    Impact 5.5.1

-   3.0.0

-   Add support for Keystone Domains (ZPS-3850)

-   Add support for Pike, Rocky, Queens, RHOSP 13-14 versions of
    OpenStack

-   Add support for multiple Zenoss instances (ZPS-1598)

-   Add support for restricted (non-administrator) users (ZPS-3851,
    ZPS-5043)

-   Exclude erroneous &lsquo;hostgroup&rsquo; host components (ZPS-4914)

-   Fix KeyError in PerfAMQPDataSource vNIC discovery (ZPS-4661)

-   Guard against missing tenant quota. (ZPS-4627)

-   Refactor Ceilometer introducing zenopenstack service to simplify
    collection

-   Allow temporary legacy metrics for &lsquo;Disk IO Rate&rsquo; and &lsquo;Disk
    Requests&rsquo; (ZPS-5205)

-   The HeartBeat datasource was removed as heartbeats are no longer
    supported by OpenStack (ZPS-1984)

-   2.4.2

-   Avoid nameconfict for proxy devices and be more flexible in linking
    to existing devices when appropriate (ZPS-3991)

-   Prevent modeling invalid host components for Ceph storage backend
    and API endpoints (ZPS-3751, ZPS-3971, ZPS-4183)

-   When mapping hostnames, treat all host references in
    case-insensitive manner (ZPS-3989)

-   Fix hostfqdn modeler plugin for systems where the &lsquo;dnsdomainname&rsquo;
    command is not available (ZPS-4083)

-   expected_ceilometer_heartbeats includes additional possible names
    for a host, based on hostmap, proxy device, and the host&rsquo;s local
    &lsquo;hostname&rsquo; (ZPS-4082)

-   Fix for &ldquo;OpenStack Component View&rdquo; option missing in left-hand nav
    (ZPS-3927)

-   Corrected URL escaping in modeler plugin to avoid receiving 400
    error when a proxy is in front of nova-api services (ZPS-3894)

-   Tested with Zenoss Resource Manager 6.2.0, Zenoss Resource Manager
    5.3.3 and Service Impact 5.3.1

-   2.4.1

-   Disallow spaces in device IDs in the &lsquo;Add OpenStack Endpoint&rsquo; dialog
    (ZPS-2583)

-   Remove certain warnings related to port update events (ZPS-2606)

-   Eliminate warnings when running tests under 6.x (ZPS-2574)

-   Support for self-signed certificates which include an IP address as
    a subjectAltName (ZPS-2056)

-   Fix situation where certain errors are reported as TimeoutError
    instead of the actual error message (ZPS-2039)

-   Fix for errors when modeling when the hosts already exist in a
    different device class (ZPS-2004)

-   2.4.0

-   Added support for Newton and Ocata

-   Added support for Keystone v3 authentication

-   Model API endpoints (currently only the public keystone API
    endpoint). Allow user to specify additional ones via
    zOpenStackExtraApiEndpoints. Supported API services are included in
    the provided ApiEndpoint monitoring template.

-   Removed zOpenStackCeilometerUrl zProperty, which was unused

-   Added descriptions for OpenStack configuration properties (ZPS-1590)

-   Tested with Zenoss Resource Manager 5.2.6, Zenoss Resource Manager
    4.2.5 RPS 743 and Service Impact 5.1.5

-   2.3.3 - Fix error in modeler when neutron agent extension is not
    available (ZPS-1243) - Fix certain problems modeling OpenStack
    environments where hosts have .localdomain names (ZPS-1244)

-   2.3.2

-   Wrap brain.getObject() into try/except block (ZPS-442)

-   2.3.1

-   Upgrade txsshclient to fix critical change in twisted.conch
    (ZEN-25870)

-   2.3.0

-   Added support for Mitaka.

-   Provide various host-checking fixes: (ZEN-24803, ZEN-25262)

-   Prevent queues from being deleted when device is removed/re-added
    (ZEN-24803)

-   Use publicURL if adminURL not working: (ZEN-24546)

-   Upgrade ZenPackLib to 1.1.0 to fix Liberty/Mitaka status:
    (ZEN-24464)

-   2.2.0

-   Added Cinder block storage components.

-   Added LVM, Ceph block storage integration via LinuxMonitor and Ceph
    ZenPacks.

-   Various bug fixes

-   2.1.3

-   Fix malformed hostnames in the F5 LBAAS plugin (ZEN-22126)

-   2.1.2

-   Remove deprecated ceilometer-agent-notification heartbeats

-   2.1.1

-   Various bug fixes

-   Add meta.zcml feature tags for Neutron Integration

-   2.1.0

-   Added Neutron network components

-   Update Impact models for Neutron

-   Update multiple UI interfaces

-   Upgrade to ZenPackLib 1.0.1

-   Add ML2 Plugin Capability

-   2.0.0

-   Initial Release

@lb[](img/zenpack-openstack-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.zenoss.OpenStackInfrastructure

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.OpenStackInfrastructure){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.OpenStackInfrastructure.git){.external-link}

### Applications Monitored:

OpenStack Cloud Computing

## OpenStack (Provider View) ZenPack

This ZenPack provides monitoring of OpenStack from a service provider
perspective. In addition to the user-oriented components (instances,
flavors, images), the underlying OpenStack servers and software are
monitored.

## Features

-   Monitors overall OpenStack state, including all tenants.
-   Monitors Nova, Neutron and Cinder health
-   Models and monitors Nova Services and components
-   Models and monitors Neutron Agents and components
-   Models and monitors Cinder Services and components
-   Impact and Root-Cause (Requires Zenoss Service Dynamics)

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

OpenStackInfrstructure 3.0.0 supports only Pike, Queens, and Rocky
releases of OpenStack.
OpenStack releases, prior to the Pike release, are not verified to work
with the OpenStackInfrastrucure 3.0.0 ZenPack.
Although the 3.0.0 ZenPack will work with the older AMQP based
Ceilometer integration, those versions of Ceilometer are not supported
by Zenoss.

## Releases

Version 3.0.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.OpenStackInfrastructure/3.0.1/ZenPacks.zenoss.OpenStackInfrastructure-3.0.1.egg){.external-link}:   Released on 2020/06/05:   Requires PythonCollector ZenPack,OpenStack (Tenant View)
    ZenPack,Linux Monitor ZenPack:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},[OpenStack     (Tenant View){.external-link}     ZenPack](https://help.zenoss.com/display/in/OpenStack+-+Tenant+View "ZenPack:OpenStack (Tenant View){.external-link}"),[Linux Monitor ZenPack](https://help.zenoss.com/display/in/Linux+Monitor "ZenPack:Linux Monitor"){.external-link}:   Compatible with Zenoss Cloud and Zenoss 6.4.1

Version 2.4.2- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.OpenStackInfrastructure/2.4.2/ZenPacks.zenoss.OpenStackInfrastructure-2.4.2.egg){.external-link}:   Released on 2018/08/15:   Requires PythonCollector ZenPack,OpenStack (Tenant View)
    ZenPack,Linux Monitor ZenPack:   Requires [PythonCollector ZenPack](https://help.zenoss.com/display/in/PythonCollector "ZenPack:PythonCollector"){.external-link},[OpenStack     (Tenant View){.external-link}     ZenPack](https://help.zenoss.com/display/in/OpenStack+-+Tenant+View "ZenPack:OpenStack (Tenant View){.external-link}"),[Linux Monitor ZenPack](https://help.zenoss.com/display/in/Linux+Monitor "ZenPack:Linux Monitor"){.external-link}:   Compatible with Zenoss 4.2 - 6.2

## Contents

-   [Gallery](#gallery)
-   [Prerequisites](#prerequisites)
    -   [Supported OpenStack Releases](#supported-open-stack-releases)
-   [Restricted Users](#restricted-users)
-   [Organizational Elements](#organizational-elements)
    -   [Metrics](#metrics)
-   [Installed Items](#installed-items)
    -   [Daemons](#daemons)
    -   [Configuration Properties](#configuration-properties)
    -   [Device Classes](#device-classes)
    -   [Modeler Plugins](#modeler-plugins)
    -   [Datasources](#datasources)
    -   [Monitoring Templates](#monitoring-templates)
    -   [Event Classes and Mappings](#event-classes-and-mappings)
    -   [Processes](#processes)
-   [Zenpack Installation](#zenpack-installation)
    -   [First-Time Installation](#time-installation)
    -   [Upgrades from 2.4.x](#)
    -   [Post-ZenPack Installation](#zenpack-installation)
-   [Device Setup](#devices-etup)
    -   [Device Setup via UI](#devices-etup-via-ui)
    -   [Device Setup via Zenbatchload](#devices-etup-via-zenbatchload)
    -   [Host Identification](#host-identification)
    -   [Modeling Containerized Environments](#modeling-containerized-environments)
-   [OpenStack Configuration](#open-stack-configuration)
    -   [OpenStack Ceilometer Configuration](#open-stack-ceilometer-configuration)
-   [Zenoss Analytics](#zenoss-analytics)
-   [Service Impact and Root Cause Analysis](#service-impact-and-root-cause-analysis)
    -   [Recommended Impact Setup](#recommended-impact-setup)
    -   [Impact Relations](#impact-relations)
    -   [Examples](#examples)
-   [Integration with other ZenPacks](#integration-with-other-zenpacks)
-   [Known Issues](#known-issues)
-   [Changes](#changes)

## Gallery

<table>
<colgroup>
<col />
<col />
<col />
</colgroup>
<tbody>
<tr markdown="1">
<td>
<p><img src="img/zenpack-regions.png" /></p>
<p>Region</p>
</td>
<td>
<p><img src="img/zenpack-tenants.png" /></p>
<p>Tenants</p>
</td>
<td>
<p><img src="img/zenpack-availabilityzones.png" /></p>
<p>Availability Zones</p>
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-devicegraphs.png" /></p>
<p>Device Graphs</p>
</td>
<td><br />
</td>
<td>
<p><img src="img/zenpack-openstackcomponentview.png" /></p>
<p>Component View</p>
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-hosts.png" /></p>
<p>Hosts</p>
</td>
<td>
<p><img src="img/zenpack-hypervisors.png" /></p>
<p>Hypervisors</p>
</td>
<td>
<p><img src="img/zenpack-images.png" /></p>
<p>Images</p>
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-novaapis.png" /></p>
<p>Nova APIs</p>
</td>
<td>
<p><img src="img/zenpack-novaservices.png" /></p>
<p>Nova Services</p>
</td>
<td>
<p><img src="img/zenpack-neutronagents.png" /></p>
<p>Neutron Agents</p>
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-instances.png" /></p>
<p>Instances</p>
</td>
<td>
<p><img src="img/zenpack-vnics.png" /></p>
<p>vNICs</p>
</td>
<td><br />
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-networks.png" /></p>
<p>Networks</p>
</td>
<td>
<p><img src="img/zenpack-ports.png" /></p>
<p>Ports</p>
</td>
<td><br />
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-floatingips.png" /></p>
<p>Floating IPs</p>
</td>
<td>
<p><img src="img/zenpack-routers.png" /></p>
<p>Routers</p>
</td>
<td>
<p><img src="img/zenpack-subnets.png" /></p>
<p>Subnets</p>
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-cinderservices.png" /></p>
<p>Cinder Services</p>
</td>
<td>
<p><img src="img/zenpack-volumes.png" /></p>
<p>Volumes</p>
</td>
<td>
<p><img src="img/zenpack-volsnapshots.png" /></p>
<p>Volume Snapshots</p>
</td>
</tr>
</tbody>
</table>

## Prerequisites

-   A supported OpenStack version (see below)
-   Administrative credentials for your OpenStack environment
    -   Username, password, keystone URL, Region
-   SSH access and credentials to the Linux devices in your OpenStack
    environment (See [Post-ZenPack-Installation Notes](#zenpack-installation-1))

### Supported OpenStack Releases

-   2.3.x supports Mitaka
-   2.4.x supports Mitaka, Newton, and Ocata
-   3.0.0 supports Pike, Queens, Rocky, and Red Hat OpenStack Platform
    (RHOSP) version 13 and 14

Note: We denote Pike, Queens, and Rocky, RHOSP 13 and 14 as **Pike+**

## Restricted Users

Restricted (non-administrator) users can also model and monitor
OpenStack devices, with access to those devices consistent with that
user&rsquo;s privileges. In other words, you should expect reduced visibility
for restricted users.

A restricted should expect to see:

-   Fewer modeled components
-   Reduced monitored metrics
-   Absent events for missing components

In particular, restricted users can see diminished components and
metrics for:

-   Cinder Pools
-   Cinder Services
-   Cinder Volumes
-   Hypervisors
-   Neutron Agents
-   Nova Services
-   Tenants
-   Any API item that requires administrator access

If you believe a user should have more access to data, it is your
responsibility to adjust the user&rsquo;s access level on OpenStack.

## Organizational Elements

The following organizational elements are discovered:

-   Regions
-   Availability Zones
-   Tenants
-   API Endpoints

The following virtual-machine elements are discovered:

-   Nova Services (processes supporting nova servers)
-   Instances (Servers)
-   Hosts
-   Hypervisors
-   Images
-   Flavors

The following network elements are discovered:

-   Neutron Agents
-   Networks
-   Subnets
-   Routers
-   Ports
-   Floating-Ips
-   vNICs

The following block storage elements are discovered:

-   Cinder Services (processes supporting block storage)
-   Volumes
-   Volume Snapshots
-   Volume Types
-   Storage Pools
-   Cinder Quotas

### Metrics

The following component level metrics are collected:

#### Instances

-   CPU Utilization (percent)
-   Disk Requests (requests/sec)
-   Disk IO Rate (bytes/sec)

#### vNICs

-   Network Packet Rate (packets/sec)
-   Network Throughput (bytes/sec)

#### Hosts

-   Load Average (processes)
-   CPU Utilization (percent)
-   Free Memory (bytes)
-   Free Swap (bytes)
-   IO (sectors/sec)

#### Nova Services

-   CPU Utilization (percent)
-   Memory Utilization (bytes)
-   Process Count (processes)

#### Neutron Agents

-   CPU Utilization (percent)
-   Memory Utilization (bytes)
-   Process Count (processes)

#### Cinder Services

-   CPU Utilization (percent)
-   Memory Utilization (bytes)
-   Process Count (processes)

#### Volumes

-   Storage Utilization (percent)
-   Operation Throughput (operations/sec)
-   Merge Rate (merged/sec)
-   Sector Throughput (sectors/sec)
-   IO Operations (operations)
-   IO Utilization (percent)
-   Weighted IO Utilization (weighted percent)

#### Volume Snapshots

-   Storage Utilization (percent)
-   Operation Throughput (operations/sec)
-   Merge Rate (merged/sec)
-   Sector Throughput (sectors/sec)
-   IO Operations (operations)
-   IO Utilization (percent)
-   Weighted IO Utilization (weighted percent)

The following device level metrics are collected:

#### Flavors

-   Total (count)

#### Images

-   Total (count)
-   Total count per image state

#### Servers

-   Total (count)
-   Total count per server state

#### Queues

-   Event (count)
-   Performance (count)

#### Agents

-   Total (count)
-   Total count per agent type

#### Networks

-   Total (count)
-   Total count per network state

#### Routers

-   Total (count)
-   Total count per router state

#### Volumes

-   Total (count)
-   Total count per volume state

#### Volume Snapshots

-   Total (count)
-   Total count per volume snapshot state

#### Volume Pool

-   Total (count)
-   Total count per volume pool state

## Installed Items

Once installed, the ZenPack installs the following properties and
components.

### Daemons

The following daemons are installed:

| Type                  | Name                                                    |
|-----------------------|---------------------------------------------------------|
| Modeler               | zenmodeler                                              |
| Performance Collector | zencommand, zenpython, zenopenstack, proxy-zenopenstack |

### Configuration Properties

-   zOpenStackAuthUrl: The URL of the Identity endpoint.
-   zOpenStackExtraHosts: The list of extra hosts that will be added to
    the system once OpenStack Infrastructure device is modeled.
-   zOpenStackExtraApiEndpoints: A list of URLs to monitor for OpenStack
    APIs. Format is &lt;service type&gt;:&lt;full URL&gt; for each.
-   zOpenStackHostDeviceClass: Used as a default device class for
    defined hosts in zOpenStackExtraHosts and zOpenStackNovaApiHosts
    properties. Default is /Server/SSH/Linux/NovaHost.
-   zOpenStackNovaApiHosts: The list of hosts upon which nova-api runs.
    This is required when the IP address in the nova API URL does not
    match any known host.
-   zOpenStackCinderApiHosts: The list of hosts upon which cinder-api
    runs. This is required when the IP address in the cinder API URL
    does not match any known host.
-   zOpenStackHostMapToId: A list of &lt;name&gt;=&lt;id&gt;, used to
    force a host referred to by OpenStack with the given name to be
    represented in Zenoss as a host component with the given ID. (this
    is not commonly used)
-   zOpenStackHostMapSame: A list of &lt;name1&gt;=&lt;name2&gt;, used
    to inform the modeler that the same host may be referred to with an
    alternate name by some part of OpenStack. (this is not commonly
    used)
-   zOpenStackNeutronConfigDir: Path to directory that contains Neutron
    configuration files. Default is /etc/neutron.
-   zOpenStackProjectId: Corresponds to tenant name, project to work on.
-   zOpenStackRegionName: The name of the OpenStack Region to use.
    Regions are autonomous OpenStack clouds joined together through
    shared Keystone identity server and managed through a common
    interface.
-   zOpenStackRunNovaManageInContainer,
    zOpenStackRunVirshQemuInContainer,
    zOpenStackRunNeutronCommonInContainer: Used when OpenStack processes
    are running inside of docker containers. Provide the container names
    (or a pattern to match them) here, or leave blank in a
    non-containerized OpenStack environment.
-   zOpenStackHostLocalDomain: When OpenStack hosts report names ending
    in .localdomain, replace domain with this value.
-   zOpenStackAMQPUsername: Username for Ceilometer AMQP integration.
-   zOpenStackAMQPPassword: Password for Ceilometer AMQP integration.
-   zOpenStackProcessEventTypes: List of OpenStack event types to pass
    to Zenoss event system. (Other event types may be processed for
    model changes, but will not be stored as events in Zenoss)
-   zOpenStackIncrementalShortLivedSeconds: Incremental Modeling - Delay
    component creation this period of time until no deletions are
    detected. (seconds)
-   zOpenStackIncrementalBlackListSeconds: Incremental Modeling - Once a
    component is deleted, wait this interval between attempts to remodel
    same component to avoid flapping. (seconds)
-   zOpenStackIncrementalConsolidateSeconds: Incremental Modeling - Wait
    this amount of time to aggregate components&rsquo; properties before
    updating a component map. Ignored by deletions. (seconds)
-   zOpenStackUserDomainName: Domain name containing opentstack user for
    authorization scope.
-   zOpenStackProjectDomainName: Domain name containing opentstack
    project for authorization scope.

### Device Classes

-   /OpenStack: Root OpenStack device class. Typically, devices should
    not be put in this device class.
-   /OpenStack/Infrastructure: Device class for OpenStack Infrastructure
    endpoints.
-   /Server/SSH/Linux/NovaHost: Device class for Nova host instances.

### Modeler Plugins

-   zenoss.OpenStackInfrastructure: Main modeler plugin- Queries the
    OpenStack APIs to populate the zenoss model.
-   zenoss.cmd.linux.openstack.hostfqdn: Used to get OpenStack host
    FQDN.
-   zenoss.cmd.linux.openstack.inifiles: Used to gather neutron.conf and
    ml2_conf.ini files.
-   zenoss.cmd.linux.openstack.libvirt: Used to get OpenStack instance
    virtual NIC information using libvert.
-   zenoss.cmd.linux.openstack.nova: Used to get installed OpenStack
    version.

### Datasources

-   ApiEndpointStatusDataSource: Checks that API endpoints are
    available.
-   CinderServiceStatusDataSource: Checks the status of Cinder services
    via the Cinder API.
-   EventsAMQPDataSource: Stores events received from OpenStack
    Ceilometer via AMQP.
-   NeutronAgentStatusDataSource: Checks the status of Neutron agents
    via the Neutron API.
-   NovaServiceStatusDataSource: Checks the status of Nova services via
    the Nova API.
-   PerfAMQPDataSource: Stores performance data received from OpenStack
    Ceilometer.
-   QueueSizeDataSource: Checks the number of unprocessed messages in
    Ceilometer AMQP queues.

#### Notes

-   As of the Pike+ (Late 2017) OpenStack release, the dispatcher
    mechanism previously used by this zenpack is no longer supported by
    Ceilometer. Because of this, the &ldquo;heartbeat&rdquo; mechanism that was
    previously used to verify connectivity between Ceilometer and Zenoss
    is no longer possible, and /Status/Heartbeat events will not be
    created if Zenoss stops receiving data from Ceilometer.

    Connectivity problems between Ceilometer and Zenoss will still be
    reported in the Ceilometer agent-notification.log file on the
    OpenStack hosts.

-   All `OpenStack Ceilometer Perf AMQP` datasources&rsquo; *cycletime*
    parameter will not work in Pike+ . Cycletime must be regulated in
    OpenStack itself. The *cycletime* setting is still present for
    backward compatibility with Ocata and prior versions, but has no
    effect.

### Monitoring Templates

-   /OpenStack/Infrastructure/
    -   Endpoint
    -   Instance
    -   vNIC

### Event Classes and Mappings

-   /OpenStack
    -   OpenStack Events Default
-   /OpenStack/Cinder
-   /OpenStack/Cinder/Snapshot
    -   Cinder Snapshot default mapping
-   /OpenStack/Cinder/Volume
    -   cinder.volume default mapping
-   /OpenStack/compute
-   /OpenStack/compute/instance
    -   compute.instance default mapping
    -   compute.instance.create.error
    -   compute.instance.exists
    -   compute.instance.exists.verified.old
-   /OpenStack/dhcp_agent
    -   dhcp_agent default mapping
-   /OpenStack/firewall
    -   firewall default mapping
-   /OpenStack/firewall_policy
    -   firewall_policy default mapping
-   /OpenStack/firewall_rule
    -   firewall_rule default mapping
-   /OpenStack/floatingip
    -   floatingip default mapping
-   /OpenStack/network
    -   network default mapping
-   /OpenStack/port
    -   port default mapping
-   /OpenStack/router
    -   router default mapping
-   /OpenStack/security_group
    -   security_group default mapping
-   /OpenStack/security_group_rule
    -   security_group_rule default mapping
-   /OpenStack/subnet
    -   subnet default mapping
-   /Status
    -   openStackCinderServiceStatus
    -   openStackIniFileAccess
    -   openStackIniFileOptionParsing
    -   openStackNeutronAgentStatus
    -   openStackNovaServiceStatus
    -   openStackApiEndpointStatus

### Processes

-   /OpenStack
-   /OpenStack/ceilometer-agent-central
-   /OpenStack/ceilometer-agent-compute
-   /OpenStack/ceilometer-agent-notification
-   /OpenStack/ceilometer-alarm-evaluator
-   /OpenStack/ceilometer-alarm-notifier
-   /OpenStack/ceilometer-api
-   /OpenStack/ceilometer-collector
-   /OpenStack/ceilometer-polling
-   /OpenStack/cinder-api
-   /OpenStack/cinder-backup
-   /OpenStack/cinder-scheduler
-   /OpenStack/cinder-volume
-   /OpenStack/glance-api
-   /OpenStack/glance-registry
-   /OpenStack/gnocchi-metricd
-   /OpenStack/gnocchi-statsd
-   /OpenStack/keystone-admin
-   /OpenStack/keystone-all
-   /OpenStack/keystone-main
-   /OpenStack/neutron-dhcp-agent
-   /OpenStack/neutron-l3-agent
-   /OpenStack/neutron-lbaas-agent
-   /OpenStack/neutron-metadata-agent
-   /OpenStack/neutron-metering-agent
-   /OpenStack/neutron-openvswitch-agent
-   /OpenStack/neutron-server
-   /OpenStack/nova-api
-   /OpenStack/nova-cert
-   /OpenStack/nova-compute
-   /OpenStack/nova-conductor
-   /OpenStack/nova-consoleauth
-   /OpenStack/nova-network
-   /OpenStack/nova-scheduler
-   /OpenStack/rabbitmq-server

## Zenpack Installation

### First-Time Installation

If you are installing the ZenPack for the first time, install as per
usual ZenPack installation, and continue to *Post-ZenPack Installation*.

### Upgrades from 2.4.x

If this is the first time you are upgrading to 3.0.0+ from a version of
the zenpack 2.4.0 or earlier, there are no special steps required, nor
any changes required on the OpenStack side.

When upgrading from 2.4.x on a system with multiple collectors, you may
see warnings such as &ldquo;ERRO\[0000\] Could not update proxy&rdquo;, as described
in [ZPS-4689](#known-issues-1). These can be
safely ignored.

If you are using the *ceilometer_zenoss* dispatcher mechanism (with
RabbitMQ) for integrating older versions of openstack with zenoss, this
will still function with 3.0.0. Note that this is only supported as a
bridge for old openstack environment which have not yet been upgraded to
a supproted version of OpenStack. All currently supported versions use
the *http publisher* mechanism to integrate with zenoss, rather than
RabbitMQ.

### Post-ZenPack Installation

Because the zenopenstack and RabbitMQ-Ceilometer services run on each
collector, in order for openstack ceilometer to send messages to them,
they need to be assigned a specific IP address. These services will be
unable to start until IP assignment is completed. (The error &lsquo;service is
missing an address assignment&rsquo; will be displayed if you try to start the
service)

The IP assignment may be performed via the Control Center UI or
command-line.

To use the UI:

-   Log into the Control Center UI.
-   Click the Zenoss.resmgr name to display the
    Applications/Zenoss.resmgr page.
-   Scroll down the page to the IP Assignments section and click
    &lsquo;Assign&rsquo; next
-   to each line for the proxy-openstack and RabbitMQ-Ceilometer
    services:

@lb[](img/zenpack-ip_assignment.png)

To use the command-line:

~~~ sourceCode
serviced service assign-ip RabbitMQ-Ceilometer serviced service assign-ip proxy-zenopenstack
~~~

If you have multiple collectors, specify the collector name for each
service and repeat for each collector:

~~~ sourceCode
serviced service assign-ip collector1/RabbitMQ-Ceilometer serviced service assign-ip collector1/proxy-zenopenstack serviced service assign-ip collector2/RabbitMQ-Ceilometer serviced service assign-ip collector2/proxy-zenopenstack
~~~

Once the zenpack is installed, provide SSH credentials to the Linux
devices in your OpenStack environment before adding any devices. \*
Configure the zCommandUsername/zCommandPassword/zKeyPath properties on
the /Devices/Server/SSH/Linux/NovaHost device class. \* If your
OpenStack nodes are already managed under Zenoss, move them into
/Devices/Server/SSH/Linux/NovaHost

## Device Setup

### Device Setup via UI

Once the OpenStack ZenPack is installed and you can begin monitoring by
going to the infrastructure screen and clicking the normal button for
adding devices. You&rsquo;ll find a new option labeled, &ldquo;Add OpenStack
Endpoint (Infrastructure).&rdquo;

Choose that option and you&rsquo;ll be presented with a dialog asking for the
following inputs.

-   Device To Create - non-empty, non-ip, non-dns, unique name to use
    for this device in Zenoss. &lsquo;&rsquo;See note below&rsquo;&rsquo;.
-   Auth URL - A keystone URL. For Keystone&rsquo;s v3 API, it should look
    like `http://<hostname>:5000/v3/`.
    For Keystone&rsquo;s v2 API, it should look like
    `http://<hostname>:5000/v2.0/`. To have the ZenPack choose the
    newest supported API version, leave the path off, like
    `http://<hostname>:5000/` (sets zOpenStackAuthUrl).
-   Username: Enter your OS_USERNAME (sets zCommandUsername).
-   Password: Enter your OS_PASSWORD (sets zCommandPassword).
-   User Domain Name: Enter the user domain name per OS_USER_DOMAIN_NAME
    (sets zOpenStackUserDomainName).
-   Project Domain Name: Enter the project domain name per
    OS_PROJECT_DOMAIN_NAME (sets zOpenStackDomainName).
-   Region Name - choose the correct region from the drop-down. You may
    only choose one, so each region you wish to manage must be
    registered as a separate endpoint in Zenoss (sets
    zOpenStackRegionName).

Once you click Add, Zenoss will contact the OpenStack API and discover
servers, images and flavors. Once it is complete you&rsquo;ll find a new
device in the OpenStack device class with the same name as the hostname
or IP you entered into the dialog. Click into this new device to see
everything that was discovered.

NOTE: The &lsquo;Device name&rsquo; should be a non-empty, non-hostname, non-IP,
since that name will be used when the host is registered as a Linux
device. The name should be unique within the Zenoss environment. This is
especially important if you are adding another device that share the
same IP address or hostname that already exist on another device. Not
doing this may result in devices with the same name conflicting with
each other. (e.g. attempting to model device would show modeling results
that belong to another device OR device would show relations that do not
belong to that device)

### Device Setup via Zenbatchload

You can setup the device using *zenbatchload* as follows:

~~~ sourceCode
zenbatchload <filename>
~~~

where `<filename>` should have the form:

     /Devices/OpenStack/Infrastructure loader='openstackinfrastructure',\ loader_arg_keys=['deviceName', 'username', 'api_key', 'project_id, 'user_domain_name', 'project_domain_name', 'auth_url', 'region_name', 'collector'] <devicename> username='<username>', api_key='<password>', project_id='<tenant ID>', user_domain_name='default', \ project_domain_name='default', auth_url='http://<ip address>:5000/v2.0/', region_name='RegionOne' /Devices/Server/SSH/Linux/NovaHost zCommandUsername='myusername', zCommandPassword='mypassword'

-   As mentioned before, zCommandUsername and zCommandPassword
    properties must be set for /Devices/Server/SSH/Linux/NovaHost
    devices (and vNICs) to be correctly modeled.

### Host Identification

The OpenStack APIs do not contain an authoritative list of hosts with
unique IDs. Instead, various APIs show hosts by name or IP. There
zenpack does its best to identify IPs and names that refer to the same
host, and represent them as a single host component. In some cases,
though, it can&rsquo;t tell, and the same host may be modeled twice, or with
an incorrect name.

Two zProperties are provided to override the default behavior of the
zenpack when this happens.

-   zOpenStackHostMapSame

    Specifies that two names refer to the same host. It is a list of
    entries of the form: `<name1>=<name2>` For example,

        my.example.com=myothername.example.com my.example.com=10.1.1.1

    This means that any time the host &ldquo;my.example.com&rdquo;,
    &ldquo;myothername.example.com&rdquo;, or &ldquo;10.1.1.1&rdquo; is encountered, they will
    be considered to be the same host, rather than separate ones.

-   zOpenStackHostMapToId

    It is also possible to specify not only that the devices are the
    same, but that they should be identified with one specific
    identifier (otherwise, one may be chosen at random). In this case, a
    list of entries of the form `<name>=<id>` may be provided in the
    zOpenStackHostMapToId zProperty. For example,
    `myothername.example.com=my.example.com 10.1.1.1=my.example.com`
    This would cause &ldquo;my.example.com&rdquo;, &ldquo;myothername.example.com&rdquo;, or
    &ldquo;10.1.1.1&rdquo; to all be definitely identified as &ldquo;my.example.com&rdquo;,
    without the ambiguity that could exist if zOpenStackHostMapSame were
    used.

-   zOpenStackHostLocalDomain

    In some environments (in particular, the Red Hat OpenStack
    Platform), hosts are assigned names that end in &lsquo;.localdomain&rsquo;. This
    would cause problems for Zenoss, because it is not possible to
    create a device in Zenoss with such a name, as they all resolve to
    127.0.0.1, rather than their actual IP.

    The default value of zOpenStackHostLocalDomain is a blank string,
    meaning that the &lsquo;.localdomain&rsquo; suffix will be stripped from host
    names, and devices will be created in Zenoss with those shortened
    names. If those names do not resolve in DNS, they will be created
    without IPs, and will not be modeled. You would need to manually set
    their management IPs so that they can be modeled.

    Alternatively, if you already have these hostnames in dns, but just
    with a different domain name than &ldquo;.localdomain&rdquo;, you may specify
    this domain name here, and it will be substituted for localdomain,
    and the devices will model automatically, based on the IPs returned
    from DNS.

### Modeling Containerized Environments

If the target OpenStack environment runs processes inside of docker
containers, it is necessary to configure several zProperties before
modeling will succeed.

-   zOpenStackRunNovaManageInContainer: Container to run &ldquo;nova-manage&rdquo;
    in
-   zOpenStackRunVirshQemuInContainer: Container to run &ldquo;virsh&rdquo; in
-   zOpenStackRunNeutronCommonInContainer: Container to access neutron
    configuration files in.

These should be set to container names or substrings of the container
names. These can be set on the /Server/SSH/Linux/NovaHost device class
or specific devices within it, as necessary.

NOTE: These zProperties must be set on the Linux devices, not the
OpenStack (/OpenStack/Infrastructure) devices.

## OpenStack Configuration

Before event and performance data can be collected, the following steps
must be performed. That these steps are only tested with
currently-supported versions of OpenStack (Pike and higher).

### OpenStack Ceilometer Configuration

Ceilometer is a component of openstack which, through a combination of
polling and notifications from the openstack message bus, collect a
variety of metric and event data from the openstack environment and
forwards it to external services, including Zenoss, for processing.

@lb[](img/zenpack-ceilometer_arch.png)

Ceilometer&rsquo;s polling agent and other openstack services (nova-api, for
instance) send notifications through an internal notification bus, which
are received by the ceilometer notification agent. It then passes these
notifications through configurable &ldquo;pipelines&rdquo;, which ultimately deliver
the data through publishers.

In 2.4.x of this ZenPack, a custom ceilometer plugin called
&lsquo;ceilometer_zenoss&rsquo; was used to send the data to zenoss through the
RabbitMQ-Ceilometer service.

This approach was no longer practical with current versions of
OpenStack, so the collection mechanism was changed to use ceilometer&rsquo;s
built-in http publisher, rather than AMQP. Since the http publisher is
part of ceilometer, there is no need to install additional software on
the OpenStack environment to use this mechanism. It is only necessary to
configure it correctly, as described below.

Ceilometer must be configured to send data to the correct Zenoss
collector, using a device-specific URL.

The OpenStack environment will therefore need https access to the zenoss
collector, and the Zenoss collector IP must be configured as described
in the [Post-ZenPack-Installation Notes](#zenpack-installation-1).

Once the device is added, and its collector&rsquo;s proxy-zenopenstack service
has an assigned IP, the following two URLs will be displayed at the
bottom of the device&rsquo;s overview page:

@lb[](img/zenpack-ceilometer_urls.png)

These URLs will be required to configure ceilometer on the OpenStack
environment to send data to Zenoss. There are two ways to configure
ceilometer:

#### RHOSP Configuration using TripleO (RedHat OpenStack Platform Director)

This is the best way to configure the Redhat OpenStack Platform.

-   Add the following to your environment template:

<!-- -->

     ManagePipeline: true PipelinePublishers: - *Zenoss Samples Publisher URL* - <other_pipeline_publishers> ManageEventPipeline: true EventPipelinePublishers: - *Zenoss Events Publisher URL* - <other_event_pipeline_publishers>

Where the publisher URLs are device-specific, and copied from the device
overview page shown above. For example:

     ManagePipeline: true PipelinePublishers: - https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack?verify_ssl=False ManageEventPipeline: true EventPipelinePublishers: - https://1.2.3.4:8342/ceilometer/v1/events/myopenstack?verify_ssl=False

If desired, multiple publisher URLs may be specified, for instance to
publish to more than one zenoss instance, or to other openstack systems
such as gnocchi or panko. Note, however, that ceilometer will publish
data to every publisher sequentially, so if one of the URLs is timing
out, it will block ceilometer and slow down the publishing of data to
Zenoss. Therefore, it is advisable to make sure that the URLs specified
are valid and functioning.

-   This template must be ***rendered*** into your templates before you
    initiate a deployment from Undercloud.
    For more information on RHOSP template management, see RedHat&rsquo;s
    [Including Environment Files in Overcloud Creation](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/13/html-single/advanced_overcloud_customization/index#sect-Including_Environment_Files_in_Overcloud_Creation){.external-link}.

-   After deployment is complete, go to the undercloud, SSH into
    controller and go to `/etc/ceilometer` in
    ceilometer_agent_notification container to check if `pipeline.yaml`
    and `event_pipeline.yaml` file is updated:

         ssh heat-admin@<controller ip> sudo su - sudo docker exec --user 0 -it ceilometer_agent_notification /bin/bash # Ensure your configuration had the right publishers

-   Add Zenoss specific extensions to the Ceilometer event definitions:

    Edit `/etc/ceilometer/event_definitions.yaml` and add the contents
    of
    [zenoss_additions.yaml](https://raw.githubusercontent.com/zenoss/ZenPacks.zenoss.OpenStackInfrastructure/master/event_definitions/zenoss_additions.yaml){.external-link}
    to the bottom of the file.

-   Restart the ceilometer-notification service on all controller nodes.

#### Manual Configuration

When RedHat OpenStack Platform is not being used, you will need to
update the affected configuration files directly. The following
modifications are required on every controller node where ceilometer is
running:

-   Add Zenoss specific extensions to the Ceilometer event definitions:

    Edit `/etc/ceilometer/event_definitions.yaml` and add the contents
    of
    [zenoss_additions.yaml](https://raw.githubusercontent.com/zenoss/ZenPacks.zenoss.OpenStackInfrastructure/master/event_definitions/zenoss_additions.yaml){.external-link}
    to the bottom of the file.

-   The /etc/ceilometer/event_pipeline.yaml file contains one sink,
    named `event_sink`. In its publishers section, add the event URL
    from above:

    For example:

        --- sources: - name: event_source events: - "*" sinks: - event_sink sinks: - name: event_sink transformers: triggers: publishers: - https://1.2.3.4:8342/ceilometer/v1/events/myopenstack?verify_ssl=False - <some_other_publisher>

-   The /etc/ceilometer/pipeline.yaml add the samples URL to the publish
    sections for the three sinks, cpu_sink, disk_sink, and network_sink:

    For example:

        --- sources: - name: meter_source meters: - "*" sinks: - meter_sink ... etc ... sinks: - name: meter_sink transformers: publishers: - https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack?verify_ssl=False - <some_other_publisher> - name: cpu_sink transformers: - name: "rate_of_change" parameters: target: name: "cpu_util" unit: "%" type: "gauge" max: 100 scale: "100.0 / (10**9 * (resource_metadata.cpu_number or 1))" publishers: - https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack?verify_ssl=False - <some_other_publisher> - name: disk_sink transformers: - name: "rate_of_change" parameters: source: map_from: name: "(disk\\.device|disk)\\.(read|write)\\.(bytes|requests)" unit: "(B|request)" target: map_to: name: "\\1.\\2.\\3.rate" unit: "\\1/s" type: "gauge" publishers: - https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack?verify_ssl=False - <some_other_publisher> - name: network_sink transformers: - name: "rate_of_change" parameters: source: map_from: name: "network\\.(incoming|outgoing)\\.(bytes|packets)" unit: "(B|packet)" target: map_to: name: "network.\\1.\\2.rate" unit: "\\1/s" type: "gauge" publishers: - https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack?verify_ssl=False - <some_other_publisher>

-   Make sure you restart ceilometer-notification service whenever you
    change `pipeline.yaml` or `event_pipeline.yaml`.

-   Configure nova to send events to ceilometer when instance state
    changes occur. (This step is optional, but recommended.) Add the
    following settings to `/etc/nova/nova.conf` on all compute nodes:

        [notifications] notify_on_state_change=vm_and_task_state [oslo_messaging_notifications] driver = messagingv2

-   Configure neutron to send events for ceilometer to forward to
    zenoss. Add the following settings to `/etc/neutron/neutron.conf`:

        [oslo_messaging_notifications] driver = messagingv2 topics = notifications

#### Ceilometer Troubleshooting

A variety of errors can be returned by zenopenstack to ceilometer. Here
are the most common ones.

The errors would be found in
`/var/log/ceilometer/agent-notification.log` on the OpenStack controller
nodes.

-   Connection Refused

        ERROR ceilometer.pipeline.sample ConnectionError: HTTPSConnectionPool(host='1.2.3.4', port=8342): Max retries exceeded with url: /ceilometer/v1/samples/myopenstack (Caused by NewConnectionError('<requests.packages.urllib3.connection.VerifiedHTTPSConnection object at 0x7f80d1e89590>: Failed to establish a new connection: [Errno 111] Connection refused',))

    Verify that the IP address is correct and that the
    proxy-zenopenstack service is running.

-   Network Connectivity

        ERROR ceilometer.pipeline.event ConnectTimeout: HTTPSConnectionPool(host='1.2.3.4', port=8342): Max retries exceeded with url: /ceilometer/v1/events/myopenstack (Caused by ConnectTimeoutError(<requests.packages.urllib3.connection.VerifiedHTTPSConnection object at 0x7f4307dc94d0>, 'Connection to 1.2.3.4 timed out. (connect timeout=5)')) ERROR ceilometer.pipeline.event ConnectionError: HTTPSConnectionPool(host='1.2.3.4', port=8342): Max retries exceeded with url: /ceilometer/v1/events/myopenstack (Caused by NewConnectionError('<requests.packages.urllib3.connection.VerifiedHTTPSConnection object at 0x7f0b78e686d0>: Failed to establish a new connection: [Errno 113] No route to host',))

    Ensure that the correct IP was specified and that it is reachable
    from the OpenStack hosts.

-   Bad Gateway

        ERROR ceilometer.publisher.http HTTPError: 502 Server Error: Bad Gateway for url: https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack

    In general, this indicates that proxy-zenopenstack is running, but
    zenopenstack is not.
    This can be normal during a zenoss restart, but if it does not
    resolve, check the status of the zenopenstack service.

-   404 Errors (Not Found)

        ERROR ceilometer.publisher.http HTTPError: 404 Client Error: Not Found for url: https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack

    This usually indicates that the device ID found in the url is not
    recognized. Check the URL and make sure the device ID is correct.

    This can be normal during zenopenstack restarts, since it will not
    know about devices to be monitored until it lots the configuration
    from zenhub. If this is the case, it will resolve in a few minutes.

    It is also possible to get a 404 error because of a typo in the URL
    unrelated to the device ID.

-   422 Errors (Unprocessable Entity)

        ERROR ceilometer.publisher.http HTTPError: 422 Client Error: Unknown Status for url: https://1.2.3.4:8342/ceilometer/v1/samples/myopenstack

    This error indicates that the payload of the http request sent to
    zenoss was not in the expected format. The most common cause for
    this is putting the samples url in event_pipeline.json, or the
    events url in pipeline.json.
    Ensure that the correct URL was put in the right file.

Additional zenopenstack debugging is possible through the &ldquo;zenopenstack
diagnostics&rdquo; link under &ldquo;show links&rdquo; on the device&rsquo;s detail page. This
link connects your browser directly to zenopensatck and provides
detailed debugging information, including request rates and a log of all
recently received http messages. Note that this option requires that
your browser have https connectivity to the Zenoss collector.

#### General Notes

-   In prior versions of this zenpack, all events from ceilometer were
    forwarded to zenoss under /OpenStack. Since most events were not
    actionable, they were used to update the model (for instance, a new
    instance is created), but were immedaitely archived. In version
    3.0.0, these events are still used for incremental model updates,
    but are not stored in zenoss as events any more (since they placed
    additional load on zenoss for no benefit).

    If there is a ceilometer event type which is actually useful to
    track in zenoss as an event, that capability still exists, however.
    The list of event types to be exposed to zenoss are configurable in
    `zOpenStackProcessEventTypes`.

    By default, this only contains `compute.instance.create.error`, but
    other types may be added if desired.

-   The Instance metrics for *Disk IO Rate* are deprecated in OpenStack
    version Queens and later. Collection for those metrics will be
    missing. Future OpenStack releases will remove these metrics and
    graphs completely.

    In the meantime, if you still require these metrics, you can edit
    the OpenStack Ceilometer configuration /etc/ceilometer/polling.yaml
    and add the following to the *meters* section:

         - disk.read.bytes - disk.read.requests - disk.write.bytes - disk.write.requests

    After editing this file, ensure the resulting YAML syntax is valid
    and restart the ceilometer-polling service.

    Finally, note that these metrics ARE deprecated and will be removed
    in future releases of OpenStack itself.

-   The OpenStack ZenPack relies upon standard zenoss Linux Monitoring
    for some functions, including process monitoring and the modeling of
    vNICs. This means that the Zenoss collectors require SSH access to
    the NovaHost devices. In some OpenStack deployments (including
    RHOSP&rsquo;s overcloud), external SSH access may not be available by
    default, and additional configuration may be required to achieve it.

## Zenoss Analytics

This ZenPack provides additional support for Zenoss Analytics. Perform
the following steps to install extra reporting resources into Zenoss
Analytics after installing the ZenPack.

1.  Copy vsphere-analytics.zip from
    `$ZENHOME/ZenPacks/ZenPacks.zenoss.OpenStackInfrastructure*/ZenPacks/zenoss/OpenStackInfrastructure/analytics/`
    on your Zenoss server.
2.  Navigate to Zenoss Analytics in your browser.
3.  Login as superuser.
4.  Remove any existing *OpenStackInfrastructure ZenPack* folder.
    1.  Choose *Repository* from the *View* menu at the top of the page.
    2.  Expand *Public* in the list of folders.
    3.  Right-click on *OpenStackInfrastructure ZenPack* folder and
        choose *Delete*.
    4.  Confirm deletion by clicking *OK*.
5.  Add the new *OpenStackInfrastructure ZenPack* folder.
    1.  Choose *Server Settings* from the &lsquo;&rsquo;Manage&rsquo; menu at the top of
        the page.
    2.  Choose *Import* in the left page.
    3.  Remove checks from all check boxes.
    4.  Click *Choose File* to import a data file.
    5.  Choose the OpenStackInfrastructure-analytics.zip file copied
        from your Zenoss server.
    6.  Click *Import*.

You can now navigate back to the &lsquo;&rsquo;OpenStackInfrastructure ZenPack&rsquo;&rsquo;
folder in the repository to see the following resources added by the
bundle.

-   Domains
    -   OpenStackInfrastructure Domain
-   Ad Hoc Views
    -   OpenStack Instance List

The OpenStackInfrastructure Domain can be used to create ad hoc views
using the following steps.

1.  Choose *Ad Hoc View* from the *Create* menu.
2.  Click *Domains* at the top of the data chooser dialog.
3.  Expand *Public* then *OpenStackInfrastructure ZenPack*.
4.  Choose the *OpenStackInfrastructure Domain* domain

## Service Impact and Root Cause Analysis

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact and root cause analysis capabilities for
OpenStack infrastructure and instances. The service impact relationships
shown in the diagram and described below are automatically added. These
will be included in any services that contain one or more of the
explicitly mentioned components.

@lb[](img/zenpack-impact.png)

### Recommended Impact Setup

Since most components will be related to Tenants and Region we
recommend:

-   Navigate to Services (Impact)
-   Add a Dynamic Service to your Services tab
-   Add all Tenants to the Dynamic Service
-   Add all Regions to the Dynamic Service

### Impact Relations

Component failures will affect Impact as follows:

Internal Impact Relationships

-   OpenStack API endpoint impacts all Hosts
-   Availability zone impacts associated Region
-   Host impacts associated Hypervisors, Nova Services, Cells, Nova
    Apis, Neutron Agents, and Cinder Services
-   Hypervisor impacts the resident Instances (VMs)
-   Nova Service affects the Availability Zone or Region that it
    supports
-   Instance impacts the associated Tenant
-   vNIC impacts the related Instance.
-   Port impacts associated Instance
-   Subnet impacts associated Ports and Tenants
-   Floating-IP impacts associated Port
-   Network impacts associated Subnets and Tenants
-   Router impacts associated Subnets and Floating-ips
-   Neutron Agent impacts associated Networks, Subnets and Routers
-   volume impacts Instances (VMs), Volume Snapshots

External Impact Relationships

-   Instance impacts guest operating system device.
-   Cisco UCS vNIC impacts related host&rsquo;s underlying Linux device NIC.
-   Cisco UCS service profile impacts host&rsquo;s underlying Linux device.
-   Host impacted by associated Linux device.
-   OS Processes on an underlying Linux device impact corresponding Nova
    APIs, Nova Services, Neutron Agents and Cinder Services on Host.

### Examples

<table>
<colgroup>
<col />
<col />
</colgroup>
<tbody>
<tr markdown="1">
<td>
<p><img src="img/zenpack-impact_instance.png" /></p>
<p>Impact (Instance)</p>
</td>
<td>
<p><img src="img/zenpack-impact_ports.png" /></p>
<p>Impact (Network)</p>
</td>
</tr>
<tr markdown="1">
<td>
<p><img src="img/zenpack-impact_region.png" /></p>
<p>Impact (Region)</p>
</td>
<td>
<p><img src="img/zenpack-impact_tenant.png" /></p>
<p>Impact (Tenant)</p>
</td>
</tr>
</tbody>
</table>

## Integration with other ZenPacks

In some cases, the underlying network or storage technology is monitored
by a different zenpack. The OpenStackInfrastructure zenpack is able to
integrate with the following ZenPacks to provide component-level linkage
and impact model integration:

-   Neutron OpenvSwitch ml2 plugin &lt;-&gt;
    [OpenvSwitch](https://help.zenoss.com/display/in/OpenvSwitch){.external-link}
    ZenPack
-   Neutron APIC ml2 plugin &lt;-&gt; [Cisco APIC](https://help.zenoss.com/display/in/Cisco+APIC){.external-link} ZenPack
-   Neutron NSX ml2 plugin &lt;-&gt; [VMWare NSX](https://help.zenoss.com/display/in/VMware+NSX){.external-link} ZenPack
-   Cinder LVM logical volumes &lt;-&gt; [Linux Monitor](https://help.zenoss.com/display/in/Linux+Monitor){.external-link} ZenPack
    (&gt;= 2.0.0)
-   Ceph RBD volumes &lt;-&gt;
    [Ceph](https://help.zenoss.com/display/in/Ceph){.external-link} ZenPack

## Known Issues

-   [ZEN-17905](https://jira.zenoss.com/browse/ZEN-17905){.external-link}:
    Nova APIs component: Grey icons for Enabled and State after
    model/monitor.

    -   OpenStack nova service API does not provide information about
        Nova-API, so its status is, in fact, unknown.

-   [ZPS-1762](https://jira.zenoss.com/browse/ZPS-1762){.external-link}:
    When using OpenvSwitch integration, the Linux devices must be added
    to the system first (normally through automatic discovery by the
    OpenStackInfrastructure ZenPack) before the corresponding
    OpenvSwitch devices are registered. This is because the two devices
    use the same management IP address, and a special exclusion is in
    place for OpenvSwitch devices, allowing them to be added after the
    Linux device, but not the other way around.

-   [ZPS-2004](https://jira.zenoss.com/browse/ZPS-2004){.external-link}:
    When adding an OSI device, if the same host is already added as a
    generic device (such as /SSH/Linux), the host device&rsquo;s device class
    will be changed, and an error generated, preventing modeling. As a
    workaround, remove the Linux device before adding the OSI device.

-   [ZPS-4742](https://jira.zenoss.com/browse/ZPS-4742){.external-link}:
    Networking functions through SR-IOV and OVS-DPDK used in NFV like
    setups are not supported. Ceilometer is not able to collect
    monitoring data for these interfaces and hence Zenoss doesn&rsquo;t have
    any insight into these interfaces. This is because legacy Ceilometer
    only supports traditional OpenvSwitch networking, where a TAP
    interface is created through libvirt.

-   [ZPS-5468](https://jira.zenoss.com/browse/ZPS-5468){.external-link}:
    Newly deployed RabbitMQ-Ceilometer service can fail to start, with
    an error `badmatch,{error,{no_such_vhost,<<"/">>}}`. When this
    occurs, all health checks for the service will fail.

    If this error is encountered, the simplest fix seems to be to attach
    to the affected container, then run:

         rm -rf /var/lib/rabbitmq/mnesia*/rabbit@rbt-ceil0

    and restart the service.

-   [ZPS-4689](https://jira.zenoss.com/browse/ZPS-4689){.external-link}:
    During upgrades you can see an error like:

         ERRO[0000] Could not update proxy

    You can safely ignore this error, which should stop after the
    upgrade is completed.

## Changes

4.0.0

-   Add support for OSP 16.x
-   Increased Read timeout (ZPS-7352)
-   Modeling needs to succeed when cinder service is not available.
    (ZPS-7362)
-   Host name is constructed with informative string unique to the
    endpoint and host combination (ZPS-7318)
-   Supports Queens, Rocky, Ussuri, Train, Victoria and Red Hat
    OpenStack Platform (RHOSP) version 13, 14 and 16
-   Tested with Zenoss Resource Manager 6.5.0, 6.6.0, Zenoss Cloud and
    Service Impact 5.5.3

3.0.1

-   Add support for Twisted library update (ZPS-6975)
-   Tested with Zenoss Resource Manager 6.4.1, Zenoss Cloud and Service
    Impact 5.5.1

3.0.0

-   Add support for Keystone Domains (ZPS-3850)
-   Add support for Pike, Rocky, Queens, RHOSP 13-14 versions of
    OpenStack
-   Add support for multiple Zenoss instances (ZPS-1598)
-   Add support for restricted (non-administrator) users (ZPS-3851,
    ZPS-5043)
-   Exclude erroneous &lsquo;hostgroup&rsquo; host components (ZPS-4914)
-   Fix KeyError in PerfAMQPDataSource vNIC discovery (ZPS-4661)
-   Guard against missing tenant quota. (ZPS-4627)
-   Refactor Ceilometer introducing zenopenstack service to simplify
    collection
-   Allow temporary legacy metrics for &lsquo;Disk IO Rate&rsquo; and &lsquo;Disk
    Requests&rsquo; (ZPS-5205)
-   The HeartBeat datasource was removed as heartbeats are no longer
    supported by OpenStack (ZPS-1984)

2.4.2

-   Avoid nameconfict for proxy devices and be more flexible in linking
    to existing devices when appropriate (ZPS-3991)
-   Prevent modeling invalid host components for Ceph storage backend
    and API endpoints (ZPS-3751, ZPS-3971, ZPS-4183)
-   When mapping hostnames, treat all host references in
    case-insensitive manner (ZPS-3989)
-   Fix hostfqdn modeler plugin for systems where the &lsquo;dnsdomainname&rsquo;
    command is not available (ZPS-4083)
-   expected_ceilometer_heartbeats includes additional possible names
    for a host, based on hostmap, proxy device, and the host&rsquo;s local
    &lsquo;hostname&rsquo; (ZPS-4082)
-   Fix for &ldquo;OpenStack Component View&rdquo; option missing in left-hand nav
    (ZPS-3927)
-   Corrected URL escaping in modeler plugin to avoid receiving 400
    error when a proxy is in front of nova-api services (ZPS-3894)
-   Tested with Zenoss Resource Manager 6.2.0, Zenoss Resource Manager
    5.3.3 and Service Impact 5.3.1

2.4.1

-   Disallow spaces in device IDs in the &lsquo;Add OpenStack Endpoint&rsquo; dialog
    (ZPS-2583)
-   Remove certain warnings related to port update events (ZPS-2606)
-   Eliminate warnings when running tests under 6.x (ZPS-2574)
-   Support for self-signed certificates which include an IP address as
    a subjectAltName (ZPS-2056)
-   Fix situation where certain errors are reported as TimeoutError
    instead of the actual error message (ZPS-2039)
-   Fix for errors when modeling when the hosts already exist in a
    different device class (ZPS-2004)

2.4.0

-   Added support for Newton and Ocata
-   Added support for Keystone v3 authentication
-   Model API endpoints (currently only the public keystone API
    endpoint). Allow user to specify additional ones via
    zOpenStackExtraApiEndpoints. Supported API services are included in
    the provided ApiEndpoint monitoring template.
-   Removed zOpenStackCeilometerUrl zProperty, which was unused
-   Added descriptions for OpenStack configuration properties (ZPS-1590)
-   Tested with Zenoss Resource Manager 5.2.6, Zenoss Resource Manager
    4.2.5 RPS 743 and Service Impact 5.1.5

2.3.3 - Fix error in modeler when neutron agent extension is not
available (ZPS-1243) - Fix certain problems modeling OpenStack
environments where hosts have .localdomain names (ZPS-1244)

2.3.2

-   Wrap brain.getObject() into try/except block (ZPS-442)

2.3.1

-   Upgrade txsshclient to fix critical change in twisted.conch
    (ZEN-25870)

2.3.0

-   Added support for Mitaka.
-   Provide various host-checking fixes: (ZEN-24803, ZEN-25262)
-   Prevent queues from being deleted when device is removed/re-added
    (ZEN-24803)
-   Use publicURL if adminURL not working: (ZEN-24546)
-   Upgrade ZenPackLib to 1.1.0 to fix Liberty/Mitaka status:
    (ZEN-24464)

2.2.0

-   Added Cinder block storage components.
-   Added LVM, Ceph block storage integration via LinuxMonitor and Ceph
    ZenPacks.
-   Various bug fixes

2.1.3

-   Fix malformed hostnames in the F5 LBAAS plugin (ZEN-22126)

2.1.2

-   Remove deprecated ceilometer-agent-notification heartbeats

2.1.1

-   Various bug fixes
-   Add meta.zcml feature tags for Neutron Integration

2.1.0

-   Added Neutron network components
-   Update Impact models for Neutron
-   Update multiple UI interfaces
-   Upgrade to ZenPackLib 1.0.1
-   Add ML2 Plugin Capability

2.0.0

-   Initial Release

## Attachments:

-   [availabilityzones.png](img/zenpack-availabilityzones.png)
-   [ceilometer_arch.png](img/zenpack-ceilometer_arch.png)
-   [ceilometer_urls.png](img/zenpack-ceilometer_urls.png)
-   [cinderservices.png](img/zenpack-cinderservices.png)
-   [devicegraphs.png](img/zenpack-devicegraphs.png)
-   [flavors.png](img/zenpack-flavors.png)
-   [floatingips.png](img/zenpack-floatingips.png)
-   [hosts.png](img/zenpack-hosts.png)
-   [hypervisors.png](img/zenpack-hypervisors.png)
-   [images.png](img/zenpack-images.png)
-   [impact_instance.png](img/zenpack-impact_instance.png)
-   [impact_ports.png](img/zenpack-impact_ports.png)
-   [impact_region.png](img/zenpack-impact_region.png)
-   [impact_tenant.png](img/zenpack-impact_tenant.png)
-   [impact.png](img/zenpack-impact.png)
-   [instances.png](img/zenpack-instances.png)
-   [ip_assignment.png](img/zenpack-ip_assignment.png)
-   [networks.png](img/zenpack-networks.png)
-   [neutronagents.png](img/zenpack-neutronagents.png)
-   [novaapis.png](img/zenpack-novaapis.png)
-   [novaservices.png](img/zenpack-novaservices.png)
-   [openstack-zenpack.png](img/zenpack-openstack-zenpack.png)
-   [overview.png](img/zenpack-overview.png)
-   [openstackcomponentview.png](img/zenpack-openstackcomponentview.png)
-   [ports.png](img/zenpack-ports.png)
-   [regions.png](img/zenpack-regions.png)
-   [routers.png](img/zenpack-routers.png)
-   [subnets.png](img/zenpack-subnets.png)
-   [tenants.png](img/zenpack-tenants.png)
-   [vnics.png](img/zenpack-vnics.png)
-   [volsnapshots.png](img/zenpack-volsnapshots.png)
-   [volumes.png](img/zenpack-volumes.png)
-   [availabilityzones.png](img/zenpack-availabilityzones.png)
-   [ceilometer_arch.png](img/zenpack-ceilometer_arch.png)
-   [ceilometer_urls.png](img/zenpack-ceilometer_urls.png)
-   [cinderservices.png](img/zenpack-cinderservices.png)
-   [devicegraphs.png](img/zenpack-devicegraphs.png)
-   [flavors.png](img/zenpack-flavors.png)
-   [floatingips.png](img/zenpack-floatingips.png)
-   [hosts.png](img/zenpack-hosts.png)
-   [hypervisors.png](img/zenpack-hypervisors.png)
-   [images.png](img/zenpack-images.png)
-   [impact_instance.png](img/zenpack-impact_instance.png)
-   [impact_ports.png](img/zenpack-impact_ports.png)
-   [impact_region.png](img/zenpack-impact_region.png)
-   [impact_tenant.png](img/zenpack-impact_tenant.png)
-   [impact.png](img/zenpack-impact.png)
-   [instances.png](img/zenpack-instances.png)
-   [ip_assignment.png](img/zenpack-ip_assignment.png)
-   [networks.png](img/zenpack-networks.png)
-   [neutronagents.png](img/zenpack-neutronagents.png)
-   [novaapis.png](img/zenpack-novaapis.png)
-   [novaservices.png](img/zenpack-novaservices.png)
-   [openstack-zenpack.png](img/zenpack-openstack-zenpack.png)
-   [openstackcomponentview.png](img/zenpack-openstackcomponentview.png)
-   [ports.png](img/zenpack-ports.png)
-   [regions.png](img/zenpack-regions.png)
-   [routers.png](img/zenpack-routers.png)
-   [subnets.png](img/zenpack-subnets.png)
-   [tenants.png](img/zenpack-tenants.png)
-   [vnics.png](img/zenpack-vnics.png)
-   [volsnapshots.png](img/zenpack-volsnapshots.png)
-   [volumes.png](img/zenpack-volumes.png)
-   [impact_instance.png](img/zenpack-impact_instance.png)
-   [overview.png](img/zenpack-overview.png)
-   [volumes.png](img/zenpack-volumes.png)
-   [availabilityzones.png](img/zenpack-availabilityzones.png)
-   [ceilometer_arch.png](img/zenpack-ceilometer_arch.png)
-   [ceilometer_urls.png](img/zenpack-ceilometer_urls.png)
-   [cinderservices.png](img/zenpack-cinderservices.png)
-   [devicegraphs.png](img/zenpack-devicegraphs.png)
-   [flavors.png](img/zenpack-flavors.png)
-   [floatingips.png](img/zenpack-floatingips.png)
-   [hosts.png](img/zenpack-hosts.png)
-   [hypervisors.png](img/zenpack-hypervisors.png)
-   [images.png](img/zenpack-images.png)
-   [impact_instance.png](img/zenpack-impact_instance.png)
-   [impact_ports.png](img/zenpack-impact_ports.png)
-   [impact_region.png](img/zenpack-impact_region.png)
-   [impact_tenant.png](img/zenpack-impact_tenant.png)
-   [impact.png](img/zenpack-impact.png)
-   [instances.png](img/zenpack-instances.png)
-   [ip_assignment.png](img/zenpack-ip_assignment.png)
-   [networks.png](img/zenpack-networks.png)
-   [neutronagents.png](img/zenpack-neutronagents.png)
-   [novaapis.png](img/zenpack-novaapis.png)
-   [novaservices.png](img/zenpack-novaservices.png)
-   [openstack-zenpack.png](img/zenpack-openstack-zenpack.png)
-   [openstackcomponentview.png](img/zenpack-openstackcomponentview.png)
-   [overview.png](img/zenpack-overview.png)
-   [ports.png](img/zenpack-ports.png)
-   [regions.png](img/zenpack-regions.png)
-   [routers.png](img/zenpack-routers.png)
-   [subnets.png](img/zenpack-subnets.png)
-   [tenants.png](img/zenpack-tenants.png)
-   [vnics.png](img/zenpack-vnics.png)
-   [volsnapshots.png](img/zenpack-volsnapshots.png)
-   [volumes.png](img/zenpack-volumes.png)
-   [availabilityzones.png](img/zenpack-availabilityzones.png)
-   [ceilometer_arch.png](img/zenpack-ceilometer_arch.png)
-   [ceilometer_urls.png](img/zenpack-ceilometer_urls.png)
-   [cinderservices.png](img/zenpack-cinderservices.png)
-   [flavors.png](img/zenpack-flavors.png)
-   [devicegraphs.png](img/zenpack-devicegraphs.png)
-   [hosts.png](img/zenpack-hosts.png)
-   [floatingips.png](img/zenpack-floatingips.png)
-   [hypervisors.png](img/zenpack-hypervisors.png)
-   [images.png](img/zenpack-images.png)
-   [impact_instance.png](img/zenpack-impact_instance.png)
-   [impact_ports.png](img/zenpack-impact_ports.png)
-   [impact_region.png](img/zenpack-impact_region.png)
-   [impact_tenant.png](img/zenpack-impact_tenant.png)
-   [impact.png](img/zenpack-impact.png)
-   [instances.png](img/zenpack-instances.png)
-   [ip_assignment.png](img/zenpack-ip_assignment.png)
-   [neutronagents.png](img/zenpack-neutronagents.png)
-   [networks.png](img/zenpack-networks.png)
-   [novaapis.png](img/zenpack-novaapis.png)
-   [novaservices.png](img/zenpack-novaservices.png)
-   [openstack-zenpack.png](img/zenpack-openstack-zenpack.png)
-   [openstackcomponentview.png](img/zenpack-openstackcomponentview.png)
-   [overview.png](img/zenpack-overview.png)
-   [ports.png](img/zenpack-ports.png)
-   [regions.png](img/zenpack-regions.png)
-   [routers.png](img/zenpack-routers.png)
-   [subnets.png](img/zenpack-subnets.png)
-   [tenants.png](img/zenpack-tenants.png)
-   [volsnapshots.png](img/zenpack-volsnapshots.png)
-   [vnics.png](img/zenpack-vnics.png)
-   [volumes.png](img/zenpack-volumes.png)

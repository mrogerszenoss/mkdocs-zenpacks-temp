# Docker

@lb[](img/zenpack-docker-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.zenoss.Docker

### Link To More Docs:

[View Documentation](https://github.com/zenoss/ZenPacks.zenoss.Docker){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.Docker.git){.external-link}

### Applications Monitored:

Docker (1.6 and later)

Podman (2.2.1 and later)

## Docker ZenPack

This ZenPack
provides support for
monitoring [Docker](https://www.docker.com/){.external-link}
and [Podman](https://podman.io){.external-link} containers
running on Linux devices.

Docker
versions through 20.10.2 and
Podman versions through 3.4.2 are known to be
supported in Docker
ZenPack as of March, 2022.

## Releases

Version 2.1.1 [Download](https://delivery.zenoss.com/){.external-link}:   Released: 2022-06-08:   Compatible with Zenoss Cloud,  6.x:   Requires: [ZenPackLib ZenPack](https://help.zenoss.com/display/in/ZenPackLib){.external-link}

<!-- -->

Version 2.1.0 [Download](https://delivery.zenoss.com/){.external-link}
           Released: 2022-03-18
           Compatible with Zenoss Cloud, 6.x
           Requires:[ZenPackLib ZenPack](https://help.zenoss.com/display/in/ZenPackLib){.external-link}

Version 2.0.5 [Download](https://delivery.zenoss.com/){.external-link}:   Released: 2020-10-20:   Compatible with Zenoss Cloud,  6.x:   Requires: [ZenPackLib ZenPack](https://help.zenoss.com/display/in/ZenPackLib){.external-link}

<!-- -->

Version 1.1.0 [Download](https://delivery.zenoss.com/){.external-link}:   Released: 2015-04-15:   Compatible with Zenoss 4.2 - 5.0:   No additional requirements.

## Contents

1.  [Features](#features)
    1.  [Discovery](#discovery)
    2.  [Monitoring](#monitoring)
        1.  [Docker Status Monitoring](#docker-status-monitoring)
        2.  [Podman Status Monitoring](#podman-status-monitoring)
        3.  [Container Status Monitoring](#container-status-monitoring)
        4.  [Container Statistics Monitoring](#container-statistics-monitoring)
    3.  [Service Impact](#service-impact)
2.  [Usage](#usage)
    1.  [SSH Configuration](#ssh-configuration)
    2.  [sudo Configuration](#sudo-configuration)
3.  [Services](#services)
4.  [Installed Items](#installed-items)
5.  [Changes](#changes)

## Features

The features added by this ZenPack can be summarized as follows. They
are each detailed further below.

-   Discovery and periodic remodeling of Docker and
    Podman containers.
-   Optional status and performance monitoring of Docker and
    Podman containers.
-   Service impact and root cause analysis. (Requires Zenoss Service
    Dynamics)

### Discovery

The following components and properties will be automatically discovered
when the *DockerCollector* modeler plugin is enabled for Linux devices
running Docker.

@lb[](img/zenpack-docker_container_details.png){.confluence-embedded-image width="843"}

Docker Host (Linux Device):   **Properties**: Docker Version:   **Relationships**: Docker Containers

<!-- -->

Docker Container:   **Properties**: ID, Title (Name), Image, Command, Ports, Created

This information is obtained by running the following commands on the
Linux device via SSH.

-   docker -v
-   sudo docker ps -a --no-trunc
-   cat
    /proc/self/mountinfo

The following
components and properties will be automatically discovered when
the *PodmanCollector *modeler plugin is enabled for Linux devices
running Podman.

@lb[](img/zenpack-podman_container_details.png){.confluence-embedded-image width="843"}

Podman Host
(Linux Device)
           **Properties:** Podman
Version
           **Relationships**: Podman Containers

Podman Container
**            Properties:** ID, Title (Name), Image, Command, Ports,
Created

This
information is obtained by running the following commands on the Linux
device via SSH.

-   podman -v
-   sudo podman ps -a --no-trunc
-   cat
    /proc/self/mountinfo

As with all SSH modeling, the *zCommandUsername*, *zCommandPassword*,
and *zKeyPath* configuration properties are used to establish the SSH
connection. For password authentication, zCommandUsername and
zCommandPassword must be set. For public key authentication,
zCommandUsername and zKeyPath must be set. The value of zCommandPassword
will be used as the passphrase if the key file provided by zKeyPath
requires a passphrase.

**Note**: The *DockerCollector* and *PodmanCollector* modeler plugins
are not enabled by default for any device classes. Typically you
would add it to the /Server/SSH/Linux device class so all Linux devices
being monitoring via SSH will have any containers discovered.
Alternatively you could create a /Server/SSH/Linux/Docker or
*/Server/SSH/Linux/Podman * device class under which you placed
all of your Linux devices that operate as Docker or Podman hosts, and
only add the *DockerCollector/PodmanCollector* modeler plugin for it.

### Monitoring

Three types of monitoring are performed for all discovered Docker and Podman
containers:
Status, Statistics, and
Size. The monitoring of
each of these aspects has been separated so that you can choose which
you are interested in monitoring more easily.

**Note**: The default value of *zCommandCommandTimeout* is 15 seconds.
This may not be long enough for the monitoring commands detailed below
to execute. It is recommended that this value be increased to 60 seconds
if status and statistics monitoring are enabled. It is recommended that
this value be increased to 600 seconds if size monitoring is enabled.

#### Docker Status Monitoring

When either zDockerMonitorContainerStatus or zDockerMonitorContainerSize
are enabled, the status of the docker daemon will be checked once per
minute (for zDockerMonitorContainerStatus) or once every ten minutes
(for zDockerMonitorContainerSize) by running one of the following
commands respectively.

-   /usr/bin/env sudo docker ps -a --no-trunc
-   /usr/bin/env sudo docker ps -a -s --no-trunc

An error event such as the following will be created if either of these
commands results in an error instead of a list of containers.

Docker Error Event:   **summary**: received unexpected output from docker ps:   **severity**: error (4):   **eventClassKey**: docker-ps-status:   **eventKey**: docker-ps-status:   **component**: docker (unlinked):   **device**: example-device-id:   **docker_command**: &lt;docker command that resulted in an error&gt;
:   **docker_output**: &lt;docker command output&gt;

A clear event such as the following will be created if the above
commands properly result in a list of containers.

Docker Clear Event:   **summary**: received expected output from docker ps:   **severity**: clear (0):   **eventClassKey**: docker-ps-status:   **eventKey**: docker-ps-status:   **component**: docker (unlinked):   **device**: example-device-id:   **docker_command**: &lt;docker command that resulted in an list of
    containers&gt;
:   **docker_output**: &lt;docker command output&gt;

The ZenPack installs a docker-ps-status event class mapping into the
/Status event class to handle these events by default. You can create an
alternative mapping for the docker-ps-status eventClassKey with a lower
sequence number if you wish th handle these events differently.

#### Podman Status Monitoring

When either
zPodmanMonitorContainerStatus or zPodmanMonitorContainerSize are
enabled, the status of the Podman will be checked once per minute (for
zPodmanMonitorContainerStatus) or once every ten minutes (for
zPodmanMonitorContainerSize) by running one of the following commands
respectively.

-   /usr/bin/env sudo podman ps -a --no-trunc
-   /usr/bin/env sudo podman ps -a -s --no-trunc

An error event such as the following will be created if either of these
commands results in an error instead of a list of containers.

Podman Error Event:   **summary**: received unexpected output from podman ps:   **severity**: error (4):   **eventClassKey**: podman-ps-status:   **eventKey**: podman-ps-status:   **component**: podman (unlinked):   **device**: example-device-id:   **podman_command**: &lt;podman command that resulted in an error&gt;
:   **podman_output**: &lt;podman command output&gt;

A clear event such as the following will be created if the above
commands properly result in a list of containers.

Podman Clear Event:   **summary**: received expected output from podman ps:   **severity**: clear (0):   **eventClassKey**: podman-ps-status:   **eventKey**: podman-ps-status:   **component**: podman (unlinked):   **device**: example-device-id:   **podman_command**: &lt;podman command that resulted in an list of
    containers&gt;
:   **podman_output**: &lt;podman command output&gt;

The ZenPack installs a podman-ps-status event class mapping into the
/Status event class to handle these events by default. You can create an
alternative mapping for the podman-ps-status eventClassKey with a lower
sequence number if you wish to handle these events differently.

#### Container Status Monitoring

@lb[](img/zenpack-docker_container_events.png){.confluence-embedded-image width="843"}

@lb[](img/zenpack-podman_container_events.png){.confluence-embedded-image width="843"}

When zDockerMonitorContainerStatus or
zPodmanMonitorContainerStatus is enabled, the status of each
Docker/Podman container
will be checked once per minute by running the following commands.

-   /usr/bin/env sudo docker ps -a --no-trunc for Docker
    Containers status
-   /usr/bin/env sudo podman ps -a --no-trunc for Podman
    Containers status

Containers with any status other than "Up" or "Created" will result in a
critical event being created for the container with the following
example fields.

Docker Clear Down Event:   **summary**: container status: exited (0) 31 minutes ago:   **severity**: critical (5):   **eventClassKey**: dockerContainerStatus:   **eventKey**: dockerContainerStatus:   **component**: docker-container-id:   **device**: example-device-id

<!-- -->

Podman Clear Down Event:   **summary**: container status: exited (0) 31 minutes ago:   **severity**: critical (5):   **eventClassKey**: podmanContainerStatus:   **eventKey**: podmanContainerStatus:   **component**: podman-container-id:   **device**: example-device-id

Containers with an "Up" or "Created" status will result in a clear event
being created for the container with the following example fields.

Docker Container Up Event:   **summary**: container status: up:   **severity**: clear (0):   **eventClassKey**: dockerContainerStatus:   **eventKey**: dockerContainerStatus:   **component**: docker-container-id:   **device**: example-device-id

<!-- -->

Podman Container Up Event:   **summary**: container status: up:   **severity**: clear (0):   **eventClassKey**: podmanContainerStatus:   **eventKey**: podmanContainerStatus:   **component**: podman-container-id:   **device**: example-device-id

The ZenPack
installs a dockerContainerStatus and podmanContainerStatus event class
mapping into the /Status event class to handle these events by default.
You can create an alternative mapping for the dockerContainerStatus or
podmanContainerStatus eventClassKey with a lower sequence number if you
wish to handle these events differently.

**Note**: Container status
monitoring is disabled by default because container down events will
only auto-clear if the same container is restarted. If the container is
left in a non-running state, or if is removed, its event must be
manually cleared. If auto-clearing is important you may want to consider
using Zenoss' normal process monitoring support to monitor the
process(es) running within the container instead of monitoring the
container.

#### Container Statistics Monitoring

When zDockerMonitorContainerStats or
zPodmanMonitorContainerStats is enabled, the statistics of each
Docker/Podman container
will be collected once every five minutes by running the following
commands.

-   /usr/bin/env sudo find /sys/fs/cgroup/cpuacct/ -printf "\\n%p\\n"
    -exec cat {} 2&gt;/dev/null \\;
-   /usr/bin/env sudo find /sys/fs/cgroup/memory/ -printf "\\n%p\\n"
    -exec cat {} 2&gt;/dev/null \\;
-   /usr/bin/env sudo find /sys/fs/cgroup/blkio/ -printf "\\n%p\\n"
    -exec cat {} 2&gt;/dev/null \\;

These three commands capture the cgroup CPU, memory, and IO usage
respectively. They will work regardless of whether the cgroupfs or
systemd driver are used.

The following datapoints are parsed from the results of these commands.

cpuacct_usage:   **Description**: Total usage include user and system time.
:   **Provenance**: Value of cpuacct.usage for container divided by
    number of CPUs found in cpuacct.usage_percpu, divided by 10,000,000
    to convert from nanoseconds to centiseconds. Presented as a rate.
:   **Units**: ticks per second (works out to a 0-100/sec rate):   **Aliases**: cpu\_\_ticks

<!-- -->

cpuacct_usage_user:   **Description**: User time.
:   **Provenance**: Value of user in cpuacct.stat divided by number of
    CPUs found in cpuacct.usage_percpu. Presented as a rate.
:   **Units**: ticks per second (works out to 0-100/sec rate):   **Aliases**: cpu_user\_\_ticks

<!-- -->

cpuacct_usage_system:   **Description**: System time.
:   **Provenance**: Value of system in cpuacct.stat divided by number of
    CPUs found in cpuacct.usage_percpu. Presented as a rate.
:   **Units**: ticks per second (works out to 0-100/sec rate):   **Aliases**: cpu_system\_\_ticks

<!-- -->

cpuacct_processes:   **Description**: Number of processes running in container.
:   **Provenance**: Value in cgroup.procs for container.
:   **Units**: process count

<!-- -->

memory_limit:   **Description**: Memory usage limit for container. (n/a indicates no
    limit):   **Provenance**: Value in memory.limit_in_bytes for container.
:   **Units**: bytes or n/a

<!-- -->

memory_usage:   **Description**: Memory usage for container.
:   **Provenance**: Value in memory.usage_in_bytes for container.
:   **Units**: bytes:   **Aliases**: mem_usage\_\_bytes

<!-- -->

blkio_bytes_total:   **Description**: Rate of IO read and write bytes for container.
:   **Provenance**: Sum of total value in
    blkio.io_service_bytes_recursive and
    blkio.throttle.io_service_bytes. Presented as a rate.
:   **Units**: bytes per second

<!-- -->

blkio_bytes_read:   **Description**: Rate of IO read bytes for container.
:   **Provenance**: Sum of read value in
    blkio.io_service_bytes_recursive and
    blkio.throttle.io_service_bytes. Presented as a rate.
:   **Units**: bytes per second

<!-- -->

blkio_bytes_write:   **Description**: Rate of IO write bytes bytes for a container.
:   **Provenance**: Sum of write value in
    blkio.io_service_bytes_recursive and
    blkio.throttle.io_service_bytes. Presented as a rate.
:   **Units**: bytes per second

<!-- -->

blkio_io_total:   **Description**: Rate of IO read and write operations for container.
:   **Provenance**: Sum of total value in blkio.io_serviced_recursive
    and blkio.throttle.io_service_bytes. Presented as a rate.
:   **Units**: operations per second

<!-- -->

blkio_io_read:   **Description**: Rate of IO read operations for container.
:   **Provenance**: Sum of read value in blkio.io_serviced_recursive and
    blkio.throttle.io_service_bytes. Presented as a rate.
:   **Units**: operations per second

<!-- -->

blkio_io_write:   **Description**: Rate of IO write operations for container.
:   **Provenance**: Sum of write value in blkio.io_serviced_recursive
    and blkio.throttle.io_service_bytes. Presented as a rate.
:   **Units**: operations per second

The following graphs are built using these datapoints.

@lb[](img/zenpack-docker_container_cpu_usage.png)

CPU Usage (percent):   Total:   User:   System

@lb[](img/zenpack-docker_container_memory_usage.png)

Memory Usage (bytes):   Limit:   Used

@lb[](img/zenpack-docker_container_io_rate.png)

IO Rate (operations/sec):   Total:   Read:   Write

@lb[](img/zenpack-docker_container_io_throughput.png)

IO Throughput (bytes/sec):   Total:   Read:   Write

#### Container Size Monitoring

When zDockerMonitorContainerSize or
zPodmanMonitorContainerSize is enabled, the real size and virtual
size of each Docker/Podman container
will be monitored once every ten minutes by running the following
command.

-   /usr/bin/env
    sudo docker ps -a -s --no-trunc 2 &gt;
    /dev/null
    for Docker Containers size
-   /usr/bin/env
    sudo podman ps -a -s --no-trunc 2&gt;/dev/null
    for Podman Containers size

**Note**: zDockerMonitorContainerSize and
zPodmanMonitorContainerSize are not enabled by default. The
reason for this is that adding *-s* flag to *docker ps* or *podman
ps *can result in the command taking a very long time to run when many
containers, or large containers are used. It is recommended
that you attempt to run the command on your Docker /Podman hosts manually and
see that it takes less than 10 minutes to execute before enabling
zDockerMonitorContainerSize
or
zPodmanMonitorContainerSize.

**Note**:Older versions of Docker only report real size, not virtual
size. The exact version cut-off isn't known, but Docker 1.6.2 as known
to not report virtual size.

The following datapoints are parsed from the results of this command.

size_size:   **Description**: Actual space used by this specific container.
:   **Provenance**: First number in the SIZE column of ''docker/podman
    ps -s'' converted to bytes.
:   **Units**: bytes

<!-- -->

size_size_virtual:   **Description**: Virtual size of container including image layers
    that may be shared with other containers.
:   **Provenance**: Parenthetical number in the SIZE column of
    *docker/podman ps -s* converted to bytes:   **Units**: bytes

The following graph is build using these datapoints.

@lb[](img/zenpack-docker_container_storage_usage.png)

Storage Usage:   Size:   Virtual Size

### Service Impact

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact capability for Docker Containers and Podman
Containers. The following service impact relationships are
automatically added. These will be included in any services containing
one or more of the explicitly mentioned entities.

@lb[](img/zenpack-docker_container_dynamicview.png){.confluence-embedded-image width="843"}

@lb[](img/zenpack-podman_container_dynamicview.png){.confluence-embedded-image width="843"}
Service Impact Relationships:   Device affects related Docker Containers.
    Device
    affects related Podman Containers.

@lb[](img/zenpack-docker_container_impact.png){.confluence-embedded-image width="843"} @lb[](img/zenpack-podman_container_impact.png){.confluence-embedded-image width="843"}

## Usage

To begin
discovering and monitoring Docker and Podman
containers you
must start by deciding what kind of monitoring you want to perform.
There are three configuration properties for Docker
containers and three configuration properties for Podman
containers that will control
how container monitoring is performed.

Configuration properties for Docker containers:

-   zDockerMonitorContainerStatus
-   zDockerMonitorContainerStats
-   zDockerMonitorContainerSize

Configuration properties for Podman containers:

-   zPodmanMonitorContainerStatus
-   zPodmanMonitorContainerStats
-   zPodmanMonitorContainerSize

You can refer to the various container monitoring sections above to
understand exactly what the implications of each of these properties
are. By default only *zDockerMonitorContainerStatus* and
*zDockerMonitorContainerStats* are enabled. This is due to a potential
performance consideration when monitoring container sizes. See the note
above in the [Container Size Monitoring](#container-size-monitoring) section.

After setting
these configuration properties to the desired values and depends on
container engine type, you must enable
the *DockerCollector* or *PodmanCollector *modeler plugin for the
device class(es) or device(s) for which you want to discover running
containers. One possibility would be to create a
*/Server/SSH/Linux/Docker* or */Server/SSH/Linux/Podman* device class,
and add *DockerCollector/PodmanCollector* to the list of modeler plugins
it will inherit from the */Server/SSH/Linux* device class.

### SSH Configuration

Docker container discovery and monitoring will occur by running commands
on the monitored device with SSH. This SSH connectivity will use the
same SSH configuration that is used for normal Linux device monitoring.
The following configuration properties can be used to control SSH
access.

-   zCommandUsername
-   zCommandPassword
-   zKeyPath
-   zCommandCommandTimeout

See the *Discovery* section for more information on how
*zCommandUsername*, *zCommandPassword*, and *zKeyPath* are used. See the
[Monitoring](#monitoring-1) section for a special note on
*zCommandCommandTimeout*.

### sudo Configuration

In addition to SSH access, this ZenPack executes specific commands via
*sudo* both during discovery and monitoring. This means that *sudo* must
be installed on the monitored system, and if *zCommandUsername* is not
root, sudo must be configured to allow the user specified in
*zCommandUsername* permission to run the following commands without
specifying a password.

Docker Containers Discovery:
:   sudo docker ps -a --no-trunc

<!-- -->

If zDockerMonitorContainerStatus is enabled:
:   /usr/bin/env sudo docker ps -a --no-trunc

<!-- -->

If zDockerMonitorContainerSize is enabled:
:   /usr/bin/env sudo docker ps -a -s --no-trunc

<!-- -->

If *zDockerMonitorContainerStats* is enabled:
:   /usr/bin/env sudo find /sys/fs/cgroup/cpuacct/ -printf "\\n%p\\n"
    -exec cat {} 2&gt;/dev/null \\;
:   /usr/bin/env sudo find /sys/fs/cgroup/memory/ -printf "\\n%p\\n"
    -exec cat {} 2&gt;/dev/null \\;
:   /usr/bin/env sudo find /sys/fs/cgroup/blkio/ -printf "\\n%p\\n"
    -exec cat {} 2&gt;/dev/null \\;

<!-- -->

Podman Containers Discovery:
:   sudo podman ps -a --no-trunc

<!-- -->

If zPodmanMonitorContainerStatus is enabled:
:   /usr/bin/env sudo podman ps -a --no-trunc

<!-- -->

If zPodmanMonitorContainerSize is enabled:
:   /usr/bin/env sudo podman ps -a -s --no-trunc

<!-- -->

If *zPodmanMonitorContainerStats* is enabled:
:   /usr/bin/env sudo find /sys/fs/cgroup/cpuacct/ -printf "\\n%p\\n"
    -exec cat {} 2&gt;/dev/null \\;
:   /usr/bin/env sudo find /sys/fs/cgroup/memory/ -printf "\\n%p\\n"
    -exec cat {} 2&gt;/dev/null \\;
:   /usr/bin/env sudo find /sys/fs/cgroup/blkio/ -printf "\\n%p\\n"
    -exec cat {} 2&gt;/dev/null \\;

It is also important that sudo be configured to allow running commands
without a tty. Specifically this means that a line such as the following
in sudoers (*visudo*) can prevent discovery and monitoring.

    Defaults requiretty

You can resolve this by disabling the requiretty option for all users by
changing the above line to the following:

    Defaults !requiretty

You can also selectively disable requiretty just for the user configured
in Zenoss' *zCommandUsername* configuration property. Assuming that
username was *zenmonitor*, this is how that would look.

    Defaults requiretty
    Defaults:zenmonitor !requiretty

## Services

This ZenPack requires the following services (daemons) to be running.

zenmodeler:   **Purpose**: Modeling Docker/Podman version and containers.
:   **Location**: All collectors expected to be modeling Docker/Podman.

<!-- -->

zencommand:   **Purpose**: Monitoring Docker/Podman containers status, statistics,
    and size.
:   **Location**: All collectors expected to be monitoring
    Docker/Podman.

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system.

@lb[](img/zenpack-docker_configuration_properties.png){.confluence-embedded-image width="843"}

Configuration Properties:   zDockerMonitorContainerStatus:   zDockerMonitorContainerStats:   zDockerMonitorContainerSize:   zPodmanMonitorContainerStatus:   zPodmanMonitorContainerStats:   zPodmanMonitorContainerSize

<!-- -->

Modeler Plugins:   DockerCollector:   PodmanCollector

<!-- -->

Monitoring Templates:   DockerContainer-Status (/Devices):   DockerContainer-Stats (/Devices):   DockerContainer-Size (/Devices):   PodmanContainer-Status (/Devices):   PodmanContainer-Stats (/Devices):   PodmanContainer-Size (/Devices)

<!-- -->

Event Class Mappings:   docker-ps-status (/Status):   dockerContainerStatus (/Status):   podman-ps-status (/Status):   podmanContainerStatus (/Status)

<!-- -->

Component Types:   DockerContainer (on related device):   PodmanContainer (on related device)

## Changes

### 2.1.1

-   Improved error handling to support Podman Containers.
-   Tested with Zenoss 6.6.0, Zenoss Cloud and Service Impact 5.5.5.0.0

### 2.1.0

-   Added support for Podman Containers. (ZPS-7870)
-   Added Impact and DynamicView relations for Podman Containers.
    (ZPS-8022)
-   Tested with Zenoss 6.6.0, Zenoss Cloud and Service Impact 5.5.5.0.0

### 2.0.5

-   Docker Size and Virtual Size are now parsed correctly (ZPS-7037)

-   Updated regex data parsing for better compatibility with differing
    linux distributions (ZPS-7037)

-   Fix monitoring on linux that have custom cgroup (ZPS-3483)

-   ~~~ c-mrkdwn__pre
    Tested with Zenoss Cloud, Zenoss Resource Manager 6.4.1 and Zenoss Resource Manager 6.5.0
    ~~~

### 2.0.4

-   Ignore the new plugin_name attribute in datamaps
-   Tested with Zenoss 5.3.3. 6.1.0, and 6.1.1

### 2.0.3

-   Update to ZenPackLib v2 to address bugs in v1. (ZPS-2934)
-   Fix collection of metrics from Kubernetes containers. (ZPS-2935)
-   Tested with Zenoss 4.2.5, 5.3.3. 6.1.0, and 6.1.1

### 2.0.2

-   Fix disabling of Dynamic View of non-Docker components. (ZPS-703)

### 2.0.1

-   Disable container status monitoring by default. (ZEN-24043)

### 2.0.0

-   Transparently support cgroupfs and systemd cgroup drivers.
-   Add zDockerMonitor(Status\|Stats\|Size) configuration properties.
-   Replace root file system monitoring with Docker's container size
    monitoring.
-   Drop support for Docker versions earlier than 1.6.
-   Support Dynamic View.

### 1.0.0

-   Initial release.

## Attachments:

-   [Docker_configuration_properties.png](img/zenpack-docker_configuration_properties.png)
-   [Docker_container_cpu_usage.png](img/zenpack-docker_container_cpu_usage.png)
-   [Docker_container_details.png](img/zenpack-docker_container_details.png)
-   [Docker_container_dynamicview.png](img/zenpack-docker_container_dynamicview.png)
-   [Docker_container_events.png](img/zenpack-docker_container_events.png)
-   [Docker_container_io_rate.png](img/zenpack-docker_container_io_rate.png)
-   [Docker_container_io_throughput.png](img/zenpack-docker_container_io_throughput.png)
-   [Docker_container_memory_usage.png](img/zenpack-docker_container_memory_usage.png)
-   [Docker_container_storage_usage.png](img/zenpack-docker_container_storage_usage.png)
-   [docker-zenpack.png](img/zenpack-docker-zenpack.png)
-   [Docker_configuration_properties.png](img/zenpack-docker_configuration_properties.png)
-   [Docker_container_cpu_usage.png](img/zenpack-docker_container_cpu_usage.png)
-   [Docker_container_details.png](img/zenpack-docker_container_details.png)
-   [Docker_container_dynamicview.png](img/zenpack-docker_container_dynamicview.png)
-   [Docker_container_events.png](img/zenpack-docker_container_events.png)
-   [Docker_container_io_rate.png](img/zenpack-docker_container_io_rate.png)
-   [Docker_container_io_throughput.png](img/zenpack-docker_container_io_throughput.png)
-   [Docker_container_memory_usage.png](img/zenpack-docker_container_memory_usage.png)
-   [Docker_container_storage_usage.png](img/zenpack-docker_container_storage_usage.png)
-   [docker-zenpack.png](img/zenpack-docker-zenpack.png)
-   [Docker_configuration_properties.png](img/zenpack-docker_configuration_properties.png)
-   [Docker_container_cpu_usage.png](img/zenpack-docker_container_cpu_usage.png)
-   [Docker_container_details.png](img/zenpack-docker_container_details.png)
-   [Docker_container_dynamicview.png](img/zenpack-docker_container_dynamicview.png)
-   [Docker_container_events.png](img/zenpack-docker_container_events.png)
-   [Docker_container_io_rate.png](img/zenpack-docker_container_io_rate.png)
-   [Docker_container_io_throughput.png](img/zenpack-docker_container_io_throughput.png)
-   [Docker_container_memory_usage.png](img/zenpack-docker_container_memory_usage.png)
-   [Docker_container_storage_usage.png](img/zenpack-docker_container_storage_usage.png)
-   [docker-zenpack.png](img/zenpack-docker-zenpack.png)
-   [Docker_configuration_properties.png](img/zenpack-docker_configuration_properties.png)
-   [README.html](attachments/14848504/34668856.html)
-   [podman_container_dynamicview.png](img/zenpack-podman_container_dynamicview.png)
-   [podman_container_events.png](img/zenpack-podman_container_events.png)
-   [podman_container_impact.png](img/zenpack-podman_container_impact.png)
-   [Docker_configuration_properties.png](img/zenpack-docker_configuration_properties.png)


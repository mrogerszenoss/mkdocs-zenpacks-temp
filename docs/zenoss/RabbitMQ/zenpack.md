# RabbitMQ

@lb[](img/zenpack-rabbitmq-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.zenoss.RabbitMQ

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.RabbitMQ.git){.external-link}

### Applications Monitored:

RabbitMQ

## RabbitMQ ZenPack

This ZenPack monitors the RabbitMQ AMQP messaging software.

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 1.0.10- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.RabbitMQ/1.0.10/ZenPacks.zenoss.RabbitMQ-1.0.10.egg){.external-link}
          Released on 2021/09/09
          Compatible with Zenoss Resource Manager 6.5-6.6 and Zenoss Cloud

Version 1.0.9- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.RabbitMQ/1.0.9/ZenPacks.zenoss.RabbitMQ-1.0.9.egg){.external-link}:   Released on 2019/31/10:   Compatible with Zenoss Resource
    Manager 5.3-6.4 and Zenoss Cloud

## Background

This ZenPack allows for monitoring of RabbitMQ. See the Usage section
for details on what is monitored. You can watch the [Monitoring RabbitMQ](http://www.youtube.com/watch?v=CAak2ayFcV0){.external-link}
video for a quick introduction that covers most of the details below.

## Related ZenPacks

There already exist at least two community Zenpacks that provide
monitoring for RabbitMQ.

-   *ZenPacks.dnalley.AMQPEventMonitor* by David Nalley: Very different
    functionality than what's provided by this ZenPack. It allows you to
    pull messages from a defined queue and automatically turn them into
    Zenoss events.

<!-- -->

-   *ZenPacks.community.RabbitMQ* by Greg Guthe: More similar to this
    ZenPack in its functionality. Global metrics for queued messages and
    rates. It appears to require that the HTTP management API plugin be
    installed into your RabbitMQ instances, and that a Net-SNMP
    extension also written by Greg Guthe be installed.

The major differences between the ZenPacks.community.RabbitMQ and this
pack are that this pack simply runs various rabbitmqctl commands over
SSH both to model the node, vhosts, exchanges and queues; as well as to
monitor connection, channel and per-queue metrics. So you don't need to
install anything extra on your RabbitMQ server, and you get more
granularity on the monitoring.

In the future this pack might be extended to also support RabbitMQ's
HTTP management API plugin in addition to the SSH method.

## Usage

Installing the ZenPack will add the following objects to your Zenoss
system.

<dl markdown="1">
<dt markdown="1">
Modeling Plugins
</dt>
</dl>

-   zenoss.ssh.RabbitMQ

<dl markdown="1">
<dt markdown="1">
Monitoring Templates
</dt>
</dl>

-   RabbitMQNode in /Devices
-   RabbitMQQueue in /Devices

<dl markdown="1">
<dt markdown="1">
Event Classes
</dt>
</dl>

-   /Status/RabbitMQ
-   /Perf/RabbitMQ

<dl markdown="1">
<dt markdown="1">
Configuration Properties
</dt>
</dl>

-   zRabbitMQAdminUser
-   zRabbitMQAdminPassword

<dl markdown="1">
<dt markdown="1">
Command Parsers
</dt>
</dl>

-   ZenPacks.zenoss.RabbitMQ.parsers.RabbitMQCTL
-   ZenPacks.zenoss.RabbitMQ.parsers.RabbitMQAdmin

These monitoring templates should not be bound directly to any devices
in the system.

To start monitoring your RabbitMQ server you will need to setup SSH
access so that your Zenoss collector server will be able to SSH into
your RabbitMQ server(s) as a user who has permission to run the
*rabbitmqctl* command. This almost always means the root user. See the
*Using a Non-Root User* section below for instructions on allowing
non-root users to run *rabbitmqctl*. To do this you need to set the
following zProperties for the RabbitMQ devices or their device class in
Zenoss.

-   zCommandUsername
-   zCommandPassword
-   zKeyPath

The zCommandUsername property must be set. To use public key
authentication you must verify that the public portion of the key
referenced in zKeyPath is installed in the \`~/.ssh/authorized_keys\`
file for the appropriate user on the RabbitMQ server. If this key has a
passphrase you should set it in the zCommandPassword property. If you'd
rather use password authentication than setup keys, simply put the
user's password in the zCommandPassword property.

You should then add the zenoss.ssh.RabbitMQ modeler plugin to the
device, or device class containing your RabbitMQ servers and remodel the
device(s). This will automatically find the node, vhosts, exchanges and
queues and begin monitoring them immediately for the following metrics.

<dl markdown="1">
<dt markdown="1">
Node Values
</dt>
</dl>

-   Status - Running or not? Generates event on failure.
-   Open Connections & Channels
-   Sent & Received Packets Rate
-   Sent & Received Bytes Rate
-   Depth of Send Queue
-   Consumers
-   Unacknowledged & Uncommitted Messages

<dl markdown="1">
<dt markdown="1">
Queue Values
</dt>
</dl>

-   Ready, Unacknowledged & Total Messages
-   Memory Usage
-   Consumers
-   Incoming & Outgoing Message Rates

There is a default threshold of 1,000,000 messages per queue. This is
almost certainly an absurdly high threshold that shouldn't trip in
normal systems. However, by clicking into the details of any individual
queue you can set the per-queue threshold to a more reasonable value
that makes sense for a given queue.

<dl markdown="1">
<dt markdown="1">
RabbitMQAdmin Update
</dt>
</dl>

Version 1.0.7+ of this ZenPack adds two additional zProperties as well
as an additional parser and provides the ability to monitor incoming and
outgoing message rates per queue using rabbitmqadmin.

For detailed instructions on configuring and using rabbitmqadmin, please
refer to the **Using RabbitMQAdmin** section, below.

### Using a Non-Root User

This ZenPack requires the ability to run the *rabbitmqctl* command
remotely on your RabbitMQ server(s) using SSH. By default, the
*rabbitmqctl* command is only allowed to be run by the **root** and
**rabbitmq** users. Furthermore, this ZenPack expects the *rabbitmqctl*
command be in the user's path. Normally this is only true for the root
user.

**Note:** There's a very good reason for this restriction. Once a user
is allowed to execute the \`\`rabbitmqctl\`\` command, they are able to
perform the following actions.

-   Stop, Start or Reset RabbitMQ
-   Control a RabbitMQ Cluster
-   Close Open Connections
-   Manage Users and Security
-   Manage VHosts

In a nutshell, this means that any user with permission to run
*rabbitmqctl* can wreak total havoc on your RabbitMQ server if they had
the intent to do so.

Assuming that you've created a user named **zenmonitor** on your
RabbitMQ servers for monitoring purposes, you can follow these steps to
allow the **zenmonitor** user to run *rabbitmqctl*.

1.  Install the **sudo** package on your server.
2.  Make sudo not require a TTY. This allows sudo to be run via ssh.
    1.  Run *visudo* as root.
    2.  Find a line containing *Defaults requiretty* and comment it out
        by prefixing the line with a *\#*.
    3.  Type *ESC* then *:wq* to save the sudo configuration.
3.  Allow the \*zenmonitor\* user to run rabbitmqctl.
    1.  Run *visudo* as root.
    2.  Add the following line to the bottom of the file.
        <dl markdown="1">
        <dd markdown="1">
        zenmonitor ALL=(ALL) NOPASSWD: /usr/sbin/rabbitmqctl
        </dd>
        </dl>
    3.  Type *ESC* then *:wq* to save the sudo configuration.
4.  Alias rabbitmqctl for the **zenmonitor** user.
    1.  Add the following lines to */home/zenmonitor/.bashrc*.
        <dl markdown="1">
        <dd markdown="1">
        shopt -s expand_aliases
        </dd>
        <dd markdown="1">
        alias rabbitmqctl="sudo /usr/sbin/rabbitmqctl"
        </dd>
        </dl>

### Using RabbitMQAdmin

Rabbitmqadmin is a script provided by RabbitMQ included with the
rabbitmq_management plugin. Rabbitmqadmin can perform a variety of tasks
and provide performance statistics for RabbitMQ. To install
**rabbitmqadmin**, the following conditions must be met on each RabbitMQ
server you want to monitor:

1.  **Erlang R14B** or greater must installed
2.  A RabbitMQ user with **administrator** tags must be used (will be
    stored in zProperties)
3.  The **rabbitmq_management** plugin must be enabled
4.  The **rabbitmqadmin** script must be saved to the RabbitMQ server
    filesystem

<dl markdown="1">
<dt markdown="1">
1\. Erlang
</dt>
</dl>

If the installed version of Erlang on each RabbitMQ server is &lt; R14B,
Erlang must first be updated. Please follow whatever requirements are
needed to update Erlang for each RabbitMQ server(s). On RHEL/CentOS, for
instance, you can check the installed version of Erlang with the command
**rpm -qa \| grep -i erlang**.

If you are updating Erlang on a RHEL/CentOS server (with or without
Zenoss):

    * Download an updated Erlang version for your platform - we recommend version R15B03 (wget http://packages.erlang-solutions.com/site/esl/esl-erlang/FLAVOUR_1_general/esl-erlang_15.b.3-1~centos~6_amd64.rpm)
    * Download an Erlang compat RPM (wget https://github.com/jasonmcintosh/esl-erlang-compat/blob/master/rpmbuild/RPMS/noarch/esl-erlang-compat-R14B-1.el6.noarch.rpm?raw=true --no-check-certificate)
    * If zenoss is present:  service zenoss stop
    * service rabbitmq-server stop
    * Remove your previous version of Erlang - if your version of Erlang is R12B, you can use the command: rpm -e erlang-R12B --nodeps
    * yum localinstall esl-erlang_15.b.3-1~centos~6_amd64.rpm
    * yum localinstall esl-erlang-compat-R14B-1.el6.noarch.rpm
    * service rabbitmq-server start
    * If zenoss is present: service zenoss start

<dl markdown="1">
<dt markdown="1">
2\. Give a RabbitMQ user administrator tags (and configure needed
zProperties)
</dt>
</dl>

Rabbitmqadmin uses a user to authenticate with Rabbit for performing
operations. If you are using a non-root user or have additional RabbitMQ
users that you will use for rabbitmqadmin monitoring, you must give them
rabbitmq adminstrator permissions. In the example below, we will be
using the "zenoss" RabbitMQ user to run rabbitmqadmin commands (replace
as appropriate):

    * rabbitmqctl set_user_tags zenoss administrator
    * In the Zenoss UI, for your RabbitMQ device, change the Configuration Property zSshConcurrentSessions to 1
    * In the Zenoss UI, for your RabbitMQ device, set your zRabbitMQAdminUser and zRabbitMQAdminPassword appropriately

<dl markdown="1">
<dt markdown="1">
3\. Enable the RabbitMQ management plugin
</dt>
</dl>

    * rabbitmq-plugins enable rabbitmq_management
    * service rabbitmq-server restart

<dl markdown="1">
<dt markdown="1">
4\. Download the rabbitmqadmin script
</dt>
</dl>

1\. Download the rabbitmqadmin script to /usr/local/bin/:

    * cd /usr/local/bin
    * RabbitMQ 2.x: wget http://{your-rabbitmq-server}:55672/cli/rabbitmqadmin --user {your-rabbitmq-user} --password {your-rabbitmq-user-password}
    * RabbitMQ 3.x: wget http://{your-rabbitmq-server}:15672/cli/rabbitmqadmin --user {your-rabbitmq-user} --password {your-rabbitmq-user-password}

2\. Make the rabbitmqadmin file executable and update ownership:

    * chmod +x /usr/local/bin/rabbitmqadmin
    * If you are running the SSH commands as a non-root user, chown (your user):(your group) /usr/local/bin/rabbitmqadmin

## Change Log

<dl markdown="1">
<dt markdown="1">

1.0.10

</dt>
<dd markdown="1">

-   (ZPS-6912) Fix Traceback generated when no queries are being
    returned for the vhost name
-   (ZPS-6937) Fix RabbitMQ 3.8.x targets break parsing
-   Tested with Zenoss Cloud, Zenoss 6.6.0, Zenoss 6.5.0 and Service
    Impact 5.5.3

</dd>
<dt markdown="1">
1.0.9
</dt>
</dl>

-   (ZPS-2772) Fix modeler omission of RabbitMQ nodes from rabbitmqctl
    status
-   Tested with Zenoss Resource Manager 6.4.1 and Zenoss Cloud

<dl markdown="1">
<dt markdown="1">
1.0.8
</dt>
</dl>

-   (ZEN-20898) Support for Federation Plugin
-   Parser improvements and bug fixes

<dl markdown="1">
<dt markdown="1">
1.0.7
</dt>
</dl>

-   (ZEN-11451) Zenoss should track and present event processing rates

<dl markdown="1">
<dt markdown="1">
1.0.6
</dt>
</dl>

-   (ZEN-5533) /Status/RabbitMQ for queues don't auto-clear when
    resolved

<dl markdown="1">
<dt markdown="1">
1.0.5
</dt>
</dl>

-   (ZEN-3526) RabbitMQ: No data returned for command

## Attachments:

-   [Rabbitmq_components.png](img/zenpack-rabbitmq_components.png)
-   [Rabbitmq_exchanges.png](img/zenpack-rabbitmq_exchanges.png)
-   [Rabbitmq_nodes_channels.png](img/zenpack-rabbitmq_nodes_channels.png)
-   [Rabbitmq_nodes_throughput.png](img/zenpack-rabbitmq_nodes_throughput.png)
-   [Rabbitmq_nodes.png](img/zenpack-rabbitmq_nodes.png)
-   [Rabbitmq_queues_metrics.png](img/zenpack-rabbitmq_queues_metrics.png)
-   [Rabbitmq_queues.png](img/zenpack-rabbitmq_queues.png)
-   [Rabbitmq_vhosts.png](img/zenpack-rabbitmq_vhosts.png)
-   [rabbitmq-zenpack.png](img/zenpack-rabbitmq-zenpack.png)
-   [Rabbitmq_components.png](img/zenpack-rabbitmq_components.png)
-   [Rabbitmq_exchanges.png](img/zenpack-rabbitmq_exchanges.png)
-   [Rabbitmq_nodes_channels.png](img/zenpack-rabbitmq_nodes_channels.png)
-   [Rabbitmq_nodes_throughput.png](img/zenpack-rabbitmq_nodes_throughput.png)
-   [Rabbitmq_nodes.png](img/zenpack-rabbitmq_nodes.png)
-   [Rabbitmq_queues_metrics.png](img/zenpack-rabbitmq_queues_metrics.png)
-   [Rabbitmq_queues.png](img/zenpack-rabbitmq_queues.png)
-   [Rabbitmq_vhosts.png](img/zenpack-rabbitmq_vhosts.png)
-   [rabbitmq-zenpack.png](img/zenpack-rabbitmq-zenpack.png)
-   [Rabbitmq_components.png](img/zenpack-rabbitmq_components.png)
-   [Rabbitmq_exchanges.png](img/zenpack-rabbitmq_exchanges.png)
-   [Rabbitmq_nodes_channels.png](img/zenpack-rabbitmq_nodes_channels.png)
-   [Rabbitmq_nodes_throughput.png](img/zenpack-rabbitmq_nodes_throughput.png)
-   [Rabbitmq_nodes.png](img/zenpack-rabbitmq_nodes.png)
-   [Rabbitmq_queues_metrics.png](img/zenpack-rabbitmq_queues_metrics.png)
-   [Rabbitmq_queues.png](img/zenpack-rabbitmq_queues.png)
-   [Rabbitmq_vhosts.png](img/zenpack-rabbitmq_vhosts.png)
-   [rabbitmq-zenpack.png](img/zenpack-rabbitmq-zenpack.png)
-   [Rabbitmq_components.png](img/zenpack-rabbitmq_components.png)
-   [Rabbitmq_exchanges.png](img/zenpack-rabbitmq_exchanges.png)
-   [Rabbitmq_nodes_channels.png](img/zenpack-rabbitmq_nodes_channels.png)
-   [Rabbitmq_nodes_throughput.png](img/zenpack-rabbitmq_nodes_throughput.png)
-   [Rabbitmq_nodes.png](img/zenpack-rabbitmq_nodes.png)
-   [Rabbitmq_queues_metrics.png](img/zenpack-rabbitmq_queues_metrics.png)
-   [Rabbitmq_queues.png](img/zenpack-rabbitmq_queues.png)
-   [Rabbitmq_vhosts.png](img/zenpack-rabbitmq_vhosts.png)
-   [rabbitmq-zenpack.png](img/zenpack-rabbitmq-zenpack.png)


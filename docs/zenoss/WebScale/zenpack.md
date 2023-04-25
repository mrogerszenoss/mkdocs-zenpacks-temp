# WebScale

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.WebScale

## WebScale ZenPack

The WebScale ZenPack enhances Web-based performance of Zenoss.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.WebScale ZenPack adds the zenwebserver daemon, to
deploy and manage multiple Zope instances.

With this ZenPack, Zenoss platform replaces zopectl with the nginx load
balancer.

## Prerequisites

|                   |                          |
|-------------------|--------------------------|
| Prerequisite      | Restriction              |
| Product           | Zenoss platform 4.1.1    |
| Required ZenPacks | ZenPacks.zenoss.WebScale |

## Installation notes

-   The installation process replaces zopectl in the startup script (or
    in the $ZENHOME/etc/daemons.txt file) with zenwebserver. Use
    zenwebserver to manage the application server.
-   If you have multiple Zope instances deployed behind a custom load
    balancer, installing this ZenPack will not install zenwebserver as
    your control script. You must install it manually after determining
    and executing your migration strategy.

## Usage

zenwebserver Command (Option) Target

### Command

-   **run** - Starts Zope in the foreground, on the port normally used
    by the load balancer. Neither the load balancer nor other Zope
    servers are used.

-   **start** - Starts the load balancer and Zope servers. If any are
    running already, they are ignored.

-   **stop** - Stops the load balancer and Zope servers. If any are
    stopped already, they are ignored.

-   **restart** - Stops and then restarts the load balancer and Zope
    servers. To minimize downtime, the load balancer is restarted first,
    and then each Zope server in turn. This ensures that the Zope server
    pool is never empty.

-   **status** - Provides status information. It prints the status of
    the load balancer, including its PID.

-   **deploy** - Creates or destroys Zope instances. It adds or removes
    instances from the server pool and updates the load balancer to
    reference the altered server pool. If the load balancer is running
    already, then its configuration is reloaded without stopping it.

-   **reload** - Reloads the load balancer configuration. For example,
    if you make a change to the nginx configuration to listen at a
    different port, reload it to use the new port without restarting.

-   **attach** - Returns a detached Zope server to the server pool and
    updates the load balancer.

-   **detach** - Removes a Zope server from the server pool and updates
    the load balancer. (Zope continues to run, but does not get traffic
    from the load balancer.)

-   **debug** - Deploys a Zope server without adding it to the server
    pool, starting it immediately in the foreground. This server can
    only be accessed directly. The server is automatically destroyed
    upon exiting the process.

-   **help** - Returns command usage information.

-   **configure** - Generates a new nginx.conf file, based on properties
    in $ZENHOME/etc/zenwebserver.conf. The properties and their defaults
    are shown in the following table.

    |           |                            |                                                                                |
    |-----------|----------------------------|--------------------------------------------------------------------------------|
    |  Property | Default Value              | Description                                                                    |
    | httpPort  | 8080                       | Specifies the port to accept the HTTP request.                                 |
    | useSSL    | False                      | Specifies whether SSL config should be used. Set to a value of True to enable. |
    | sslPort   | 443                        | Specifies the port to use if useSSL is set.                                    |
    | sslCert   | ZENHOME/etc/ssl/zenoss.crt | Specifies the path to the SSL certificate if useSSL is set.                    |
    | sslKey    | ZENHOME/etc/ssl/zenoss.key | Specifies the path to the SSL key if useSSL is set.                            |

    The generated configuration should not be edited. Use the properties
    in $ZENHOME/etc/zenwebserver.conf to customize generation of the
    nginx.conf file.

    After running zenwebserver configure, you must reload (zenwebserver
    reload) or restart (zenwebserver restart) for the new configuration
    to take effect.

### Option

-   **-v** - Prints more information, including the status of each Zope
    server, the ports at which the processes are listening, and the
    servers currently detached from the server pool.

### Target

Several commands accept one or more targets against which the command
should be executed. If you do not specify a target, the command runs the
action against all targets.

-   **loadbalancer** - Load balancer. Alternatively, you can specify:

        ngnix

-   **servers** - All Zope servers.

-   **server***n* - Specific Zope server, where *n* is the server
    number. Alternatively, you can specify just a server number or
    numbers. For example, both of the following commands stop Zope
    servers 2 and 3:

        zenwebserver stop server2 server3

        zenwebserver stop 2 3

### Examples

#### Status

zenwebserver status \[-v\]

#### Start, Stop, and Restart

zenwebserver {stop\|start\|restart} \[-v\] \[*Targets*\]

#### Manage the Number of Zope Servers

zenwebserver deploy {n\|-n\|+n}

**Examples:**

-   zenwebserver deploy 5 \# Ensures that exactly 5 Zope servers are
    running.
-   zenwebserver deploy +1 \# Deploys one additional Zope server,
    regardless of the current number.
-   zenwebserver deploy -3 \# Destroys up to 3 Zope servers (as long as
    the minimum of 1 is maintained).

#### Manage the Server Pool

zenwebserver {attach\|detach} *Targets*

Detaching a target is useful when you want to isolate a Zope server and
access it via its direct port to ensure that your requests are the only
ones being handled by that server.

#### Start an Independent Instance

zenwebserver debug

### Configuring the Load Balancer

The load balancer configuration file (nginx.conf) is generated from the
template in $ZENHOME/etc/nginx.conf.template. This template includes a
number of variables that can be substituted by providing values in the
zenwebserver.conf file.

Custom configurations also can be included in the http and server blocks
of the nginx configuration. By default, configuration files in
$ZENHOME/etc are included if they match one of these patterns:

-   nginx-custom-http-\*.conf
-   nginx-custom-server-\*.conf

Values that can be substituted are:

-   Number of worker_processes for nginx to use

        #worker_processes 4

-   Paths for nginx var directories

        #proxy_cache_path $ZENHOME/var/nginx/cache
        #proxy_temp_path $ZENHOME/var/nginx/tmp/proxy
        #client_body_temp_path $ZENHOME/var/nginx/tmp/client_body

-   Custom includes, which include any configuration files that match
    the pattern.
    -   customHttpInclude allows configurations to be added to the http
        block in the nginx configuration:

            #customHttpInclude $ZENHOME/etc/nginx-custom-http-*.conf

    -   customServerInclude allows configurations to be added to the
        server block in the nginx configuration:

            #customServerInclude $ZENHOME/etc/nginx-custom-server-*.conf

-   Default error log level

        #error_log_level warn

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


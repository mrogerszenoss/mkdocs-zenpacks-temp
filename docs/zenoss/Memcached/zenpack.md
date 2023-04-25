# Memcached

@lb[](img/zenpack-memcached-zenpack.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.zenoss.Memcached

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.Memcached.git){.external-link}

### Applications Monitored:

Memcached

## Memcached ZenPack

Monitoring for memcached.

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 1.0.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.Memcached/1.0.0/ZenPacks.zenoss.Memcached-1.0.0.egg){.external-link}:   Released on 2012/02/07:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.1.x, Zenoss Core
    3.2.x, Zenoss Core 4.2.x, Zenoss Resource Manager 4.1.x, Zenoss
    Resource Manager 4.2.x, Zenoss Resource Manager 5.x

## Background

This ZenPack allows for monitoring of memcached. See the Usage section
for details on what is monitored. This ZenPack previously existed as a
commercial-only extension to Zenoss called
ZenPacks.zenoss.MemcachedMonitor. Upon being released as open source its
name was changed to better match today's standards.

There already exists a very good community ZenPack for memcached by
braudel. As far as I can see there is no compelling reason to use this
version over that. Ultimately I'd like to see the ZenPacks come together
to reduce confusion. At the time that this ZenPack was originally
written, the community version didn't exist.

## Usage

Installing the ZenPack will add a sample monitoring template called
"memcached" in the root of your device class tree. This makes it
available to be bound to any device in the system.

Assuming that you're running memcached on the standard port (11211/tcp),
you only need to go to the device class containing your memcached
servers, or to the individual device and bind the memcached template.

If you run memcached on a different port, you will either want to edit
the command template in the datasource within the memcached monitoring
template to change the port number.

<dl markdown="1">
<dt markdown="1">
The following graphs and their included metrics will be monitored on
each device the template is bound to.
</dt>
</dl>

-   memcached - CPU Utilization (rusage_system, rusage_user)
-   memcached - Memory Utilization (bytes, limit_maxbytes)
-   memcached - Cache Efficiency (get_hits, get_misses)
-   memcached - Requests (cmd_get, cmd_set, evictions)
-   memcached - Items Cached (curr_items, total_items)
-   memcached - Connections (curr_connections, total_connections,
    connection_structures)
-   memcached - Throughput (bytes_read, bytes_written)

## Attachments:

-   [Memcached\_-\_Graphs_1.png](img/zenpack-memcached_-_graphs_1.png)
-   [Memcached\_-\_Graphs_2.png](img/zenpack-memcached_-_graphs_2.png)
-   [Memcached\_-\_Graphs_3.png](img/zenpack-memcached_-_graphs_3.png)
-   [memcached-zenpack.png](img/zenpack-memcached-zenpack.png)
-   [Memcached\_-\_Graphs_1.png](img/zenpack-memcached_-_graphs_1.png)
-   [Memcached\_-\_Graphs_2.png](img/zenpack-memcached_-_graphs_2.png)
-   [Memcached\_-\_Graphs_3.png](img/zenpack-memcached_-_graphs_3.png)
-   [memcached-zenpack.png](img/zenpack-memcached-zenpack.png)
-   [Memcached\_-\_Graphs_1.png](img/zenpack-memcached_-_graphs_1.png)
-   [Memcached\_-\_Graphs_2.png](img/zenpack-memcached_-_graphs_2.png)
-   [Memcached\_-\_Graphs_3.png](img/zenpack-memcached_-_graphs_3.png)
-   [memcached-zenpack.png](img/zenpack-memcached-zenpack.png)
-   [Memcached\_-\_Graphs_1.png](img/zenpack-memcached_-_graphs_1.png)
-   [Memcached\_-\_Graphs_2.png](img/zenpack-memcached_-_graphs_2.png)
-   [memcached-zenpack.png](img/zenpack-memcached-zenpack.png)
-   [Memcached\_-\_Graphs_3.png](img/zenpack-memcached_-_graphs_3.png)


# AutoTune

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.AutoTune

## AutoTune ZenPack

The AutoTune ZenPack enables the ZenTune "tuning advisor" feature in
Resource Manager. ZenTune analyzes your system configuration and makes
recommendations for better performance.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

This ZenPack provides the ZenTune "tuning advisor" feature of Zenoss
platform.

This ZenPack analyzes your system configuration and makes
recommendations for better performance.

## Prerequisites

| Prerequisite      | Restriction              |
|-------------------|--------------------------|
| Product           | Zenoss platform 4.2      |
| Required ZenPacks | ZenPacks.zenoss.AutoTune |

## Configuring ZenTune

You can set values for several options in the zentune.conf configuration
file (or when running ZenTune from the command line) to configure
behavior.

When setting up ZenTune, you can define options to send a test event
through the lifecycle to make sure that Zenoss is processing events
before the timeout. If it fails to process in time, an email can be sent
out.

-   testevent-enable -- When testevent-enable is present in the
    zentune.conf file, a test event will be sent. If it is not present
    or commented out, no test event is sent.
-   testevent-email *ValidEmailAddress* -- If testevent-enable is
    present and the test event times out, an email will be sent to the
    defined email address.

ZenTune can perform an analysis one or more times each day, depending on
the values of these two options:

-   tune-offset *Value* -- Sets the number of minutes after midnight
    when the ZenTune will first run. By default, the value is 0.
-   tune-interval *Value* -- Sets the number of minutes to wait before
    running ZenTune again. By default, the value is 0, which is
    equivalent to 1440 (24 hours).

So, for example, if you want ZenTune to run twice each day, set the
value of tune-offset to 0 and the value of tune-interval to 720.

### Configuring ZenTune for Remote Databases

If you have installed the Zenoss DataStore on a server other than your
master server, then you must set additional configuration options. Set
the following options in the $ZENHOME/etc/zentune.conf file of the
master server:

Remote Database Configuration Options

| Option                               | Description                                                                         |
|--------------------------------------|-------------------------------------------------------------------------------------|
| mysqltuner-zodb-forcemem *MegaBytes* | Sets the amount of memory available on the server running the ZODB database server. |
| mysqltuner-zep-forcemem *MegaBytes*  | Sets the amount of memory available on the server running the ZEP database server.  |

## Using ZenTune

To access ZenTune, select Advanced &gt; Tuning from the Zenoss platform
interface.

ZenTune

![](plugins/servlet/confluence/placeholder/unknown-attachment "%28AutoTune%29ZenTune.tuning_advisor.png"){.confluence-embedded-image}

To run ZenTune, click **Update** (located at the bottom left of the
page). ZenTune may require several minutes to run.

Note: To check the update status, refresh the browser page and then
check the "Update at" value for any watched items.

ZenTune returns information about current and optimal values for several
configuration parameters. Click + to the left of each item to display
recommendations, if any, for configuration changes.

ZenTune Issue Detail

![](plugins/servlet/confluence/placeholder/unknown-attachment "%28AutoTune%29ZenTune.tuning_advisor_detail.png"){.confluence-embedded-image}

To refresh the view, click **Refresh**. (This does not run ZenTune
again.)

To filter the list of displayed items, select Not Acknowledged,
Acknowledged, or both in the Acknowledge column. To acknowledge one or
more items, select the option in the Acknowledge column.

You also can filter the display by severity, host, and description.

### Running ZenTune from the Command Line

You can run ZenTune from the command line. On the master server, use the
command:

    zentune run

To run ZenTune on a remote hub or collector, prefix the command with the
name of the hub or collector, followed by an underscore. For example, if
the remote collector name is centos6-coll, then run the command as:

    centos6-coll_zentune run

This generates a report to the console output. If you additionally
specify the --events option, events are instead issued (the same events
issued by the zentune daemon). The results appear on the Tuning page of
the Zenoss platform interface.

## Tuneable Items

The following table lists included tuneable items.

<table>
<colgroup>
<col />
<col />
<col />
</colgroup>
<tbody>
<tr markdown="1">
<th width="33%">Name</th>
<th width="33%">Group</th>
<th width="33%">Description</th>
</tr>

<tr markdown="1">
<td>zeneventd workers</td>
<td>Events</td>
<td>ZenTune monitors the number of incoming events to the zeneventd daemon. If the number of incoming events exceeds the configured threshold per worker, then a tuning event is generated. If the threshold is exceeded only during peak load times, a WARNING severity tuning event is generated. If it is exceeded more often, an ERROR severity tuning event is generated.
<p>The threshold checked is controlled by these configuration options on the zentune daemon:</p>
<ul>
<li>zeneventd-worker-events-per-second</li>
<li>zeneventd-worker-count-max-recommended</li>
</ul>
<p>For detailed information about each of these options, run this command on any Zenoss platform server:</p>
<p>zentune run --help</p></td>
</tr>
<tr markdown="1">
<td>zeneventserver</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver age-eligible events</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver archive-eligible events</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver processed events</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver deduped events</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver dropped events</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver cleared events</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver archived events</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver aged events</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver summary queue length</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver archive queue length</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver summary index size</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver archive index size</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver summary index doc count</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver archive index doc count</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>age eligible event count</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>archive eligible event count</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver summary queue length</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventserver archive queue length</td>
<td>Events</td>
<td></td>
</tr>
<tr markdown="1">
<td>zeneventd object cache</td>
<td>Global</td>
<td>The zeneventd zodb-cachesize configuration setting controls the number of objects that zeneventd will store locally to avoid querying ZODB. Zenoss platform expects this value to be between certain thresholds, proportional to the size of the global catalog. If any of these thresholds are violated, then a WARNING or ERROR severity tuning event is generated, depending on the configured thresholds.
<p>The thresholds checked are controlled by the following configuration options on the zentune daemon:</p>
<ul>
<li>zeneventd-obj-cache-bad</li>
<li>zeneventd-obj-cache-warn</li>
</ul>
<p>For detailed information about each of these options, run this command on any Zenoss platform server:</p>
<p>zentune run --help</p></td>
</tr>
<tr markdown="1">
<td>ZODB cache servers</td>
<td>Global</td>
<td>Zenoss platform expects at least one memcached server to be configured for its use as a ZODB cache. If this is not the case, then an ERROR severity tuning event is generated.
<p>Memcached is a third-party object caching system used by Zenoss platform to improve performance for daemons that connect to Zope and ZODB. It is not required for Zenoss platform to function, but it is highly recommended.</p>
<p>More information on memcached can be found here:</p>
<p><a href="http://memcached.org/" class="external-link">http://memcached.org/</a></p></td>
</tr>
<tr markdown="1">
<td>globalConfig</td>
<td>Global</td>
<td></td>
</tr>
<tr markdown="1">
<td>Global config sip size</td>
<td>Global</td>
<td>The configsipsize global configuration setting controls the number of device configuration objects that a collector daemon will receive in a single request. A setting of 0 implies that all device configurations will be requested at once. Combined with the configsipdelay option, this effectively controls the traffic to collector daemons.</td>
</tr>
<tr markdown="1">
<td>Global config sip delay</td>
<td>Global</td>
<td>The configsipdelay global configuration setting controls the number of seconds between requests for device configuration objects that a collector daemon will make. Combined with the configsipsize option, this effectively controls the traffic to collector daemons.</td>
</tr>
<tr markdown="1">
<td>Event flush chunk size</td>
<td>Global</td>
<td>The eventflushchunksize global configuration setting controls the number of events a collector daemon will send to zenhub at one time. Each collector daemon will periodically flush its outgoing event queue and send events to zenhub until the queue is empty.</td>
</tr>
<tr markdown="1">
<td>Maximum queue length</td>
<td>Global</td>
<td>The maxqueuelen global configuration setting controls the number of events a collector daemon can store in its outgoing event queue before it must start dropping events.</td>
</tr>
<tr markdown="1">
<td>IO CPU Wait Time</td>
<td>IO</td>
<td>ZenTune monitors iostat statistics, and if any device causes wait times exceeding the configured threshold in more than 5% of cases, then an ERROR severity tuning event is generated. The threshold checked is controlled by the following configuration option on the zentune daemon:
<ul>
<li>iostat-wait-threshold</li>
</ul>
<p>For detailed information about each of these options, run this command on any Zenoss platform server:</p>
<p>zentune run --help</p>
<p>The iostat utility is a third-party program that provides statistics on the time the CPU spends waiting for I/O requests from various devices. More information on iostat can be found here:</p>
<p><a href="http://en.wikipedia.org/wiki/Iostat" class="external-link">http://en.wikipedia.org/wiki/Iostat</a></p></td>
</tr>
<tr markdown="1">
<td>Cache miss percentage</td>
<td>Memcached</td>
<td>Memcached is a third-party object caching system used by Zenoss platform to improve performance for daemons that connect to Zope and ZODB. It is not required for Zenoss platform to function, but it is highly recommended.
<p>More information on memcached can be found here:</p>
<p><a href="http://memcached.org/" class="external-link">http://memcached.org/</a></p></td>
</tr>
<tr markdown="1">
<td>Maximum size</td>
<td>Memcached</td>
<td>Memcached is a third-party object caching system used by Zenoss platform to improve performance for daemons that connect to Zope and ZODB. It is not required for Zenoss platform to function, but it is highly recommended.
<p>More information on memcached can be found here:</p>
<p><a href="http://memcached.org/" class="external-link">http://memcached.org/</a></p></td>
</tr>
<tr markdown="1">
<td>Cache eviction rate</td>
<td>Memcached</td>
<td>Memcached is a third-party object caching system used by Zenoss platform to improve performance for daemons that connect to Zope and ZODB. It is not required for Zenoss platform to function, but it is highly recommended.
<p>More information on memcached can be found here:</p>
<p><a href="http://memcached.org/" class="external-link">http://memcached.org/</a></p></td>
</tr>
<tr markdown="1">
<td>Cache servers</td>
<td>Memcached</td>
<td>Zenoss platform expects at least one memcached server to be configured for its use. If this is not the case, then an INFO severity tuning event is generated. Zenoss platform also expects all configured memcached servers to be available and responding to connection attempts using the standard memcached client. If this is not the case, then an ERROR severity tuning event is generated.
<p>Memcached is a third-party object caching system used by Zenoss platform to improve performance for daemons that connect to Zope and ZODB. It is not required for Zenoss platform to function, but it is highly recommended.</p>
<p>More information on memcached can be found here:</p>
<p><a href="http://memcached.org/" class="external-link">http://memcached.org/</a></p></td>
</tr>
<tr markdown="1">
<td>Cache size</td>
<td>Memcached</td>
<td>Zenoss platform expects the use of each memcached server to conform to certain performance thresholds. Specifically, the utilization level and eviction rate of each memcached server are checked. If any of these thresholds are violated, then a WARNING or ERROR severity tuning event is generated, depending on the configured thresholds. The thresholds checked are controlled by the following configuration options on the zentune daemon:
<ul>
<li>memcache-size-high-warn</li>
<li>memcache-size-high-bad</li>
<li>memcache-size-low-warn</li>
<li>memcache-size-low-bad</li>
<li>memcache-size-evictions-warn</li>
<li>memcache-size-evictions-bad</li>
</ul>
<p>For detailed information about each of these options, run this command on any Zenoss platform server:</p>
<p>zentune run --help</p>
<p>Memcached is a third-party object caching system used by Zenoss platform to improve performance for daemons that connect to Zope and ZODB. It is not required for Zenoss platform to function, but it is highly recommended.</p>
<p>More information on memcached can be found here:</p>
<p><a href="http://memcached.org/" class="external-link">http://memcached.org/</a></p></td>
</tr>
<tr markdown="1">
<td>MySqlTuner script</td>
<td>Resources</td>
<td>ZenTune expects the mysqltuner.pl utility to be installed and available for its use to enable more detailed tuning advice. The mysqltuner.pl utility is a third-party tuning script that provides advanced statistics on MySQL. More information on mysqltuner.pl can be found here:
<p><a href="http://mysqltuner.pl/help" class="external-link">http://mysqltuner.pl/help</a></p>
<p>MySQL is a third-party, open-source relational database. Zenoss platform uses MySQL as the backing data store for ZODB, as well as directly to store events and user sessions. More information on MySQL can be found here:</p>
<p><a href="http://www.mysql.com/" class="external-link">http://www.mysql.com/</a></p></td>
</tr>
<tr markdown="1">
<td>iostat Utility</td>
<td>Resources</td>
<td>ZenTune expects the iostat utility to be installed and available for its use to enable more detailed tuning advice. The iostat utility is a third-party program that provides statistics on the time the CPU spends waiting for I/O requests from various devices. More information on iostat can be found here:
<p><a href="http://en.wikipedia.org/wiki/Iostat" class="external-link">http://en.wikipedia.org/wiki/Iostat</a></p></td>
</tr>
<tr markdown="1">
<td>Memory</td>
<td>Resources</td>
<td>This tuning item provides information about the total amount of RAM installed in the Zenoss platform master server.</td>
</tr>
<tr markdown="1">
<td>Processes</td>
<td>Resources</td>
<td>This tuning item provides advice on the distribution of CPU-intensive Zenoss platform processes according to the number of cores available on the Zenoss platform server. If any of the thresholds are violated, a WARNING or ERROR severity tuning event will be generated, depending on the configured thresholds. The thresholds checked are controlled by the following configuration options on the zentune daemon:
<ul>
<li>resources-available-cores-warn</li>
<li>resources-available-cores-bad</li>
</ul>
<p>For detailed information about each of these options, run this command on any Zenoss platform server:</p>
<p>zentune run --help</p></td>
</tr>
<tr markdown="1">
<td>MySQL Version</td>
<td>MySQL Database</td>
<td>Zenoss platform expects that at least a specific, minimum version of MySQL is installed and available for its use. Earlier versions may not support all the features that Zenoss platform requires, or may have hidden incompatibilities. If this minimum threshold is violated, then an ERROR severity tuning event is generated, depending on the configured threshold. The threshold checked is controlled by the following configuration option on the zentune daemon:
<ul>
<li>mysql-recommended-version</li>
</ul>
<p>For detailed information about this option, run this command on any Zenoss platform server:</p>
<p>zentune run --help</p>
<p>MySQL is a third-party, open-source relational database. Zenoss platform uses MySQL as the backing data store for ZODB, as well as directly to store events and user sessions. More information on MySQL can be found here:</p>
<p><a href="http://www.mysql.com/" class="external-link">http://www.mysql.com/</a></p></td>
</tr>
<tr markdown="1">
<td>InnoDB buffer pool size</td>
<td>MySQL Database</td>
<td>If the mysqltuner.pl script recommends increasing the amount of memory available to InnoDB, then an ERROR level tuning event is generated. More information on the innodb_buffer_pool_size configuration setting can be found here:
<p><a href="http://dev.mysql.com/doc/refman/5.5/en/innodb-parameters.html#sysvar_innodb_buffer_pool_size" class="external-link">http://dev.mysql.com/doc/refman/5.5/en/innodb-parameters.html\#sysvar_innodb_buffer_pool_size</a></p>
<p>MySQL is a third-party, open-source relational database. Zenoss platform uses MySQL as the backing data store for ZODB, as well as directly to store events and user sessions. More information on MySQL can be found here:</p>
<p><a href="http://www.mysql.com/" class="external-link">http://www.mysql.com/</a></p></td>
</tr>
<tr markdown="1">
<td>Table sizes</td>
<td>MySQL Database</td>
<td>This tuning item provides information about the total size and number of tables in each MySQL instance configured for Zenoss platform. MySQL is a third-party open-source relational database. Zenoss uses MySQL as the backing data store for ZODB, as well as directly to store events and user sessions. More information on MySQL can be found here: <a href="http://www.mysql.com/" class="external-link">http://www.mysql.com/</a>
<p>MySQL is a third-party, open-source relational database. Zenoss platform uses MySQL as the backing data store for ZODB, as well as directly to store events and user sessions. More information on MySQL can be found here:</p>
<p><a href="http://www.mysql.com/" class="external-link">http://www.mysql.com/</a></p></td>
</tr>
<tr markdown="1">
<td>Table fragmentation</td>
<td>MySQL Database</td>
<td>If the mysqltuner.pl script recommends de-fragmenting the tables in a MySQL instance, then an ERROR level tuning event is generated.
<p>MySQL is a third-party, open-source relational database. Zenoss platform uses MySQL as the backing data store for ZODB, as well as directly to store events and user sessions. More information on MySQL can be found here:</p>
<p><a href="http://www.mysql.com/" class="external-link">http://www.mysql.com/</a></p></td>
</tr>
<tr markdown="1">
<td>Thread cache</td>
<td>MySQL Database</td>
<td>If the mysqltuner.pl script recommends increasing the number of threads cached for reuse by MySQL, then an ERROR level tuning event will be generated. More information on the thread_cache_size configuration setting can be found here: <a href="http://dev.mysql.com/doc/refman/5.5/en/server-system-variables.html#sysvar_thread_cache_size" class="external-link">http://dev.mysql.com/doc/refman/5.5/en/server-system-variables.html#sysvar_thread_cache_size</a>
<p>MySQL is a third-party, open-source relational database. Zenoss platform uses MySQL as the backing data store for ZODB, as well as directly to store events and user sessions. More information on MySQL can be found here:</p>
<p><a href="http://www.mysql.com/" class="external-link">http://www.mysql.com/</a></p></td>
</tr>
<tr markdown="1">
<td>Version</td>
<td>rabbitmq</td>
<td></td>
</tr>
<tr markdown="1">
<td>Hub</td>
<td>Hubs</td>
<td></td>
</tr>
<tr markdown="1">
<td>zenhub workers</td>
<td>Hubs</td>
<td></td>
</tr>
<tr markdown="1">
<td>Check interval</td>
<td>Zope</td>
<td></td>
</tr>
<tr markdown="1">
<td>Object cache</td>
<td>Zope</td>
<td></td>
</tr>
<tr markdown="1">
<td>RelStorage cache</td>
<td>Zope</td>
<td></td>
</tr>
<tr markdown="1">
<td>Pool size</td>
<td>Zope</td>
<td></td>
</tr>
<tr markdown="1">
<td>Cache servers</td>
<td>Zope</td>
<td></td>
</tr>
<tr markdown="1">
<td>Maximum number of session objects</td>
<td>Zope</td>
<td></td>
</tr>
<tr markdown="1">
<td>Debug mode</td>
<td>Zope</td>
<td></td>
</tr>
<tr markdown="1">
<td>Application server processes</td>
<td>Zope</td>
<td></td>
</tr>
<tr markdown="1">
<td>Application server threads</td>
<td>Zope</td>
<td></td>
</tr>
<tr markdown="1">
<td>Request latency</td>
<td>Zope</td>
<td></td>
</tr>
</tbody>
</table>

## Daemons

| Type                  | Name    |
|-----------------------|---------|
| Performance Collector | zentune |

## Attachments:

-   [(AutoTune)ZenTune.tuning_advisor_detail.png](img/zenpack-zentune.tuning_advisor_detail.png)
-   [(AutoTune)ZenTune.tuning_advisor.png](img/zenpack-zentune.tuning_advisor.png)
-   [(AutoTune)ZenTune.tuning_advisor_detail.png](img/zenpack-zentune.tuning_advisor_detail.png)
-   [(AutoTune)ZenTune.tuning_advisor.png](img/zenpack-zentune.tuning_advisor.png)
-   [(AutoTune)ZenTune.tuning_advisor.png](img/zenpack-zentune.tuning_advisor.png)
-   [(AutoTune)ZenTune.tuning_advisor_detail.png](img/zenpack-zentune.tuning_advisor_detail.png)
-   [(AutoTune)ZenTune.tuning_advisor.png](img/zenpack-zentune.tuning_advisor.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [(AutoTune)ZenTune.tuning_advisor_detail.png](img/zenpack-zentune.tuning_advisor_detail.png)
-   [(AutoTune)ZenTune.tuning_advisor.png](img/zenpack-zentune.tuning_advisor.png)
-   [(AutoTune)ZenTune.tuning_advisor_detail.png](img/zenpack-zentune.tuning_advisor_detail.png)

# HP-UX Monitor (SSH)

@lb[](img/zenpack-hp-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

David Andino

### Maintainers:

David Andino

### Organization:

andinod

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.andinod.HPUXMonitor

### More Information:

[GitHub page/HomePage](https://github.com/andinod/ZenPacks.andinod.HPUXMonitor.git){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/andinod/ZenPacks.andinod.HPUXMonitor.git){.external-link}

### Applications Monitored:

HP-UX (11.31)

## HP-UX Monitor (SSH) ZenPack

HP-UX Monitoring Through SSH

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 0.1.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.andinod.HPUXMonitor/0.1.0/ZenPacks.andinod.HPUXMonitor-0.1.0.egg){.external-link}:   Released on 2013/08/26:   Requires [Linux Monitor ZenPack](https://help.zenoss.com/display/in/Linux+Monitor "ZenPack:Linux Monitor"){.external-link}:   Compatible with Zenoss Core 4.2.x

<!-- -->

Version 0.2.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.andinod.HPUXMonitor/0.2.1/ZenPacks.andinod.HPUXMonitor-0.2.1.egg){.external-link}:   **Summary of changes:** Cleaned directories, serial and uptime
    plugins were deleted:   Released on 2013/08/27:   Requires [Linux Monitor ZenPack](https://help.zenoss.com/display/in/Linux+Monitor "ZenPack:Linux Monitor"){.external-link}:   Compatible with Zenoss Core 4.2.x

<!-- -->

Version 0.2.2- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.andinod.HPUXMonitor/0.2.2/ZenPacks.andinod.HPUXMonitor-0.2.2.egg){.external-link}:   **Summary of changes:** systemscan plugin was adapted to recognize
    HPVM virtual machines:   Released on 2013/08/27:   Requires [Linux Monitor ZenPack](https://help.zenoss.com/display/in/Linux+Monitor "ZenPack:Linux Monitor"){.external-link}:   Compatible with Zenoss Core 4.2.x

## Background

This Zenpack was created by the need to monitor HP-UX 11.31 servers with
Zenoss. Some HP-UX 11.31 servers have serious problems with the snmpd
daemon, which in some cases reaches loads up to 90% of CPU. So that is
the reason to make this Zenpack for every Unix administrator that have
this problem.

This Zenpack will create:

-   New Organizer: Devices -&gt; Server -&gt; SSH -&gt; HPUX
-   This Organizer will provide:
    -   Template HPUXSSHMonitor
    -   HPUX Filesystem Template
    -   HPUXEthernet Template
    -   Plugins: bdf, lanscan, memory, systemscan and zenoss.cmd.uname.
    -   Additional plugins:model, uname_a are not necessary because
        systemscan do their job, but they are provided only for debug
        purposes.

CONFIGURATIONS:

-   After installing this Zenpack, restart zope, zenhub and zencommand:
    (with user zenoss)
    -   zopectl restart; zenhub restart; zencommand restart
-   For security reason configure ssh key for zenoss account to your
    server.
    -   On Zenoss server with zenoss account do: ssh-keygen, Press Enter
        to all
    -   Go to .ssh
    -   Copy the information contained in id_rsa.pub
    -   Paste the information in the remote server's monitor user (for
        example root) in ~/.ssh/authorized_keys file
    -   Test the trust connection without password from Zenoss server to
        the remote host (You don't have to be asked for password).
-   In Configuration Properties edit if is necessary:
    -   zKeyPath
    -   zCommandUsername
-   Add your Server.

RECOMENDATIONS

-   This Zenpack is recommended for HP-UX 11.31 but could be compatible
    with older versions 11.11 and 11.23
-   Change values in /opt/ssh/etc/sshd_config to:
    -   MaxSessions 10

## Attachments:

-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)
-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)
-   [hp-zenpack.png](img/zenpack-hp-zenpack.png)


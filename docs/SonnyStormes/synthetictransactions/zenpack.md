# Synthetic Web Transactions

@lb[](img/zenpack-zenpack-general.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Sonny Stormes

### Maintainers:

Sonny Stormes

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.SonnyStormes.synthetictransactions

### More Information:

[GitHub page/HomePage](http://community.zenoss.org/docs/DOC-3757){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/sstormes/ZenPack.synthetictransactions.git){.external-link}

## Synthetic Web Transactions ZenPack

This ZenPack provides monitoring of multi-step web transactions. The
ZenPack leverages Twill scripts to monitor websites.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 2.1- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.SonnyStormes.synthetictransactions/2.1/ZenPacks.SonnyStormes.synthetictransactions-2.1.egg){.external-link}:   Compatible with Zenoss Core 2.5.x, Zenoss Core 3.2.x

## Background

This ZenPack provides monitoring of multi-step web transactions. The
ZenPack leverages Twill scripts to monitor websites.

After installing the ZenPack (noting the dependencies), add the desired
website as a device making sure your "discovery protocol" is set to None
and that SNMP monitoring is disabled (zSnmpMonitorIgnore = 'True').

To monitor a site, you need to create a twill script - To learn how to
create a twill script, visit: twill dot idyll dot org (very simple to
do! Hint: use the twill-sh interactive prompt to step through the
transaction you wish to perform on your website) Make sure the name of
this script matches the name of your device. (i.e. if you are monitoring
www.zenoss.com - name the script www.zenoss.com and save it as a text
file)

Helpful commands to use in twill:

    showforms
    show
    follow <link name>

Which would log into slashdot with the username and password provided
and check to see what the return code is. You can continue adding to
this script by adding lines like "follow &lt;link name&gt;, or formvalue
1 &lt;field&gt; &lt;value to add to form&gt;, etc....

To get the best test, make sure you perform many operations within your
twill script to verify the accuracy of the synthetic transaction. Click
around, fill out forms, post information, and log out to make sure
everything is working end-to-end on your site. The more detailed your
transaction, the more accurate your test.

### Setup

Copy your twill script to the scripts directory of the ZenPack -
$ZENHOME/ZenPacks/ZenPacks.SonnyStormes.synthetictransactions-2.0-py2.6.egg/ZenPacks/SonnyStormes/synthetictransactions/scripts

Bind template to a device created with the FQDN of the site you wish to
test.

If everything is in working order, bind the template to the devices.

As an example, I have included a small script that uses www.zenoss.org
to get you started on your twill script creation.

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


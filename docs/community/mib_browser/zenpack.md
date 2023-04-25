# MIB Browser

@lb[](img/zenpack-zenpack-general.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Jane Curry

### Maintainers:

Jane Curry

### Organization:

Skills 1st

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.community.mib_browser

### More Information:

[GitHub page/HomePage](https://github.com/jcurry/ZenPacks.community.mib_browser/tree/5.x){.external-link}

### Link To More Docs:

[View Documentation](http://community.zenoss.org/docs/DOC-10321){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/jcurry/ZenPacks.community.mib_browser.git){.external-link}

## MIB Browser ZenPack

This is Kells Kearney's ZenPack.community.mib_utils ZenPack, updated to
work with Zenoss 3. Version 2.2 of the ZenPack now tested with Zenoss
Core 5.1.5.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 2.2- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.mib_browser/2.2/ZenPacks.community.mib_browser-2.2.egg){.external-link}:   **Summary of changes:** Tested with Zenoss Core 5.1.5

Test Settings permits SNMP version specification Test Settings performs
ZODB database lookup of SNMP parameters if community field blank.

<dl markdown="1">
<dd markdown="1">
Released on 2016/09/23
</dd>
<dd markdown="1">
Compatible with Zenoss Core 3.2.x, Zenoss Core 4.2.x, Zenoss Core 5.0.x,
Zenoss Core 5.1.x
</dd>
<dd markdown="1">
Incompatible with Zenoss Core 2.5.x, Zenoss Core 3.1.x
</dd>
</dl>

Version 1.2- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.community.mib_browser/1.2/ZenPacks.community.mib_browser-1.2.egg){.external-link}:   **Summary of changes:** Supports 3.1 directly. Can be made to work
    with 3.2 and 4.1 - see below.
:   Released on 2012/11/01:   Compatible with Zenoss Core 3.1.x, Zenoss Core 4.2.x, Zenoss
    Resource Manager 4.1.x

## Background

This is Kells Kearney's ZenPack.community.mib_utils ZenPack, updated to
work with Zenoss 3. It has been tested with Zenoss 3.1 and with Firefox
3.6.13 and 4.0b12. No functional enhancements have been made and the
testing emphasis has been on the MIB Browser functionality, rather than
any other features.

To make this ZenPack work with Zenoss 3.2 or Zenoss 4.2 you need to
reverse some standard code "updates":

I have just upgraded from 4.2.3 to 4.2.4 without de-installing the fixed
MIB Browser ZenPack. The manual changes of the 4 files have been
overwritten (though my backup .orig files are still present).
Re-replacing these 4 files again makes it work again with 4.2.4. Read
the README on GitHub for Zenoss 5 details.

I believe I have a way to make this ZenPack work with 3.2.x. Basically
you revert 4 Core files back to the 3.1 level of code. Zenoss
development kindly provided a patch to do this but I have found that
their 3.2.1 patch didn't work on my system - I think it was built from a
slightly later build. I will provide their patches and also document
here what actually needs to change in case the patches don't work for
you either. The manual patch also worked for me on Core 4.2. See the
documentation page for this ZenPack for the oldmib_3.2.1.patch and
oldmib.patch.

oldmib.patch worked for me on a 3.2.0 system. oldmib_3.2.1.patch did NOT
work for me on a 3.2.1 system (neither did the oldmib.patch)

If you want to try the patches, copy them to $ZENHOME and change
directory there. Run:

patch -p 0 &lt; oldmib.patch

to apply a patch. To undo it and restore to original, use:

patch -R -p 0 &lt; oldmib.patch

You will need to completely restart Zenoss and make sure your browser
cache is cleared out.

If you need to make manual changes, this is what you need (all
directories under $ZENHOME):

Products/ZenUI3/browser/backcompat.py

###### ==================

Comment out the lines at the end defining MibClass

+\#def MibClass(ob): +\# id = '/'.join(ob.getPhysicalPath()) +\# return
'/zport/dmd/mibs\#mibtree:' + id

If there are also similar lines for MibNode and MibNotification, comment
them out too

Products/ZenUI3/browser/navigation.zcml

###### ====================

Around line 247, change the url line to be
url="/zport/dmd/Mibs/mibOrganizerOverview" - url="/zport/dmd/mibs" +
url="/zport/dmd/Mibs/mibOrganizerOverview"

Note carefully the case sensitivity on mibs / Mibs

Products/ZenUI3/browser/backcompat.zcml

###### ====================

Around line 355 comment out lines for the adapter for
"Products.ZenModel.MibOrganizer.MibOrganizer" If adapter stanzas also
exist for MibNode, MibNotification and MibModule, comment them out too

Products/ZenModel/skins/zenmodel/viewMibModule.pt

###### =============================

Change the template in the first line to be &lt;tal:block
metal:use-macro="here/page_macros/old-new"&gt;

-&lt;tal:block metal:use-macro="here/templates/macros/page2"&gt;
+&lt;tal:block metal:use-macro="here/page_macros/old-new"&gt;

This should not be tried on a production system but if anyone can help
verify this on a development system, I would be grateful.

I am going to petition Zenoss to restore this code to the 3.1 level as I
do not believe that the 3.2 code adds any benefit and it breaks this
ZenPack. My understanding is that Zenoss Core 4.?? is NOT planning to
incorporate mib browsing as part of the base product.

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


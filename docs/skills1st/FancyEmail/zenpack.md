# FancyEmail

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

ZenPacks.skills1st.FancyEmail

### More Information:

[GitHub page/HomePage](https://github.com/jcurry/ZenPacks.skills1st.FancyEmail){.external-link}

### Link To More Docs:

[View Documentation](https://github.com/jcurry/ZenPacks.skills1st.FancyEmail){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/jcurry/ZenPacks.skills1st.FancyEmail.git){.external-link}

## FancyEmail ZenPack

The ZenPack provides a new Notification type, FancyEmail, which is based
on the standard Email notification but whose body and clear_body contain
html formatting rather than simple text. They also include image
banners.

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.1.0- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.skills1st.FancyEmail/1.1.0/ZenPacks.skills1st.FancyEmail-1.1.0.egg){.external-link}:   **Summary of changes:** HTML emails, including table format and
    banner images:   Released on 2014/11/18:   Compatible with Zenoss Core 4.2.x, Zenoss Resource Manager 4.2.x

## Background

See the README.rst for details. Don't forget to restart zenactiond after
installing the ZenPack. If you already have a FancyEmail notification
and you modify / reinstall the ZenPack, the existing notification will
not have the benefit of any changes so always remember to create a new
notification to test.

The ZenPack introduces non-standard event fields which need to be set in
the transform of the top-level eventClass. Code is included in
root_transform.txt.

Minor update 21st Nov 2014 to add utf-8 charset flag - no
version/release update - sha updated

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


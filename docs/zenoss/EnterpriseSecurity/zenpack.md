# Enterprise Security

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.EnterpriseSecurity

## Enterprise Security ZenPack

The EnterpriseSecurity ZenPack enhances Resource Manager security by
enabling password encryption.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.EnterpriseSecurity ZenPack enhances Zenoss platform
security by encrypting stored passwords.

Zenoss platform stores the passwords it uses to remotely access hosts in
a Zope Object Database (ZODB). After enabling this feature, these
passwords are encrypted according to the Advanced Encryption Standard
(AES), with 256-bit key sizes.

By using the password encryption feature, you can help prevent an
attacker from accessing your managed systems if he gains access to a
backup copy of your ZODB.

## Prerequisites

|                   |                                           |
|-------------------|-------------------------------------------|
| Prerequisite      | Restriction                               |
| Product           | Zenoss platform 4.x, Zenoss 2.5 or higher |
| Required ZenPacks | ZenPacks.zenoss.EnterpriseSecurity        |

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


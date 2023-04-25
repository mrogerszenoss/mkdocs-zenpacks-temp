# Postfix

@lb[](img/zenpack-postfix-zenpack.png)

## Community

This ZenPack is developed and supported by the Zenoss User Community.
[Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1021){.external-link} to
view all available Zenoss Community ZenPacks.

### Authors:

Andrew D Kirch

### Maintainers:

Andrew D Kirch

### Organization:

Community

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.trelane.Postfix

### More Information:

[GitHub page/HomePage](https://github.com/trelane/ZenPacks.trelane.Postfix){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/trelane/ZenPacks.trelane.Postfix){.external-link}

## Postfix ZenPack

Basic monitoring of Postfix queues and logged throughput

## Support

This ZenPack is developed by the Zenoss user community and supported via
our online forums. Zenoss, Inc. does not provide direct support for this
ZenPack.

## Releases

Version 1.0.5- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.trelane.Postfix/1.0.5/ZenPacks.trelane.Postfix-1.0.5.egg){.external-link}:   **Summary of changes:** ZenPack now honors zCommandUsername:   Released on 2015/03/23:   Compatible with Zenoss Core 4.2.x

## Background

## Notes

This pack relies on parsing log output. Various distributions customize
or change the log output, and formatting of various daemons, especially
core daemons like Postfix. This ZenPack has been tested against the
logging in CentOS 6 only (to date). Please e-mail me for more/other
support. If you need more log parsing, I will need a fairly large ~10mb
mail log.

## Usage

Accept your postfix server's ssh fingerprint if you have not, and create
an ssh key with no password to automate logins. Add this template to
your Linux server running postfix.

## Features

|            |                                           |
|------------|-------------------------------------------|
| Data Point | Description                               |
| Queue      | Length of Queue from 'postqueue -p'       |
| Sent       | E-mails sent from the mail server         |
| Received   | E-mails received by the mail server       |
| Spam       | e-mails marked as spam by the mail server |

## Bugs/Feature Requests

e-mail akirch at zenoss dot com

## Attachments:

-   [postfix-zenpack.png](img/zenpack-postfix-zenpack.png)
-   [postfix-zenpack.png](img/zenpack-postfix-zenpack.png)
-   [postfix-zenpack.png](img/zenpack-postfix-zenpack.png)


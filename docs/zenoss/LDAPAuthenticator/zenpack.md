# LDAP Authentication

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.LDAPAuthenticator

## LDAP Authentication ZenPack

The LDAPAuthenticator ZenPack allows Resource Manager to use your
existing LDAP authentication infrastructure, such as Active Directory or
OpenLDAP, to enable single sign-on to the Resource Manager interface.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

The ZenPacks.zenoss.LDAPAuthenticator ZenPack enables pass-through
authentication to external LDAP-based servers such as Microsoft Active
Directory or OpenLDAP.

This capability allows users to sign on to the Zenoss platform user
interface with the same credentials they use to log in to their
workstations. This saves you from having to manually create user
accounts and maintain passwords in Zenoss platform.

Among the benefits of using a service like LDAP to maintain user
accounts and privileges are:

-   Users do not have to remember another password. This decreases
    support and maintenance requirements.
-   Centralized management of each user's privileges. This enables
    easier security auditing and SOX reporting.

Authentication logging is stored in the $ZENHOME/log/event.log file.

## Prerequisites

|                   |                                   |
|-------------------|-----------------------------------|
| Prerequisite      | Restriction                       |
| Product           | Zenoss platform 4.x, 5.x          |
| Required ZenPacks | ZenPacks.zenoss.LDAPAuthenticator |

## LDAP Configuration

Before configuring LDAP authentication, you should gather the following
information from your LDAP or Active Directory administrator:

-   Host name or IP address of an Active Directory global catalog server
    (for Active Directory authentication)
-   Host name or IP address of an LDAP server (for other LDAP server
    authentication)
-   User's base distinguished name (DN)
-   Manager DN
-   Manager password
-   Groups base DN
-   Optionally, list of Active Directory groups to map to Zenoss
    platform roles

### Configuring LDAP Authentication

You can configure LDAP authentication at initial setup, or from the
Settings area of the interface:

-   While in the setup wizard, at Step 2: Specify or Discover Devices to
    Monitor, click **LDAP Setup** (located at the bottom right of the
    wizard panel).
-   From the interface, select Advanced &gt; Settings, and then select
    LDAP in the left panel.

The first panel (Add LDAP Servers) of the LDAP Configuration wizard
appears.

LDAP Configuration Wizard (Add LDAP Servers)

![](plugins/servlet/confluence/placeholder/unknown-attachment "%28LDAPAuthenticator%29LDAPAuthentication.LDAP_Configuration_Wizard_1.png"){.confluence-embedded-image}

1.  Enter information and make selections in the LDAP Servers area:
    -   **Host** - Enter the host name or IP address of an Active
        Directory global catalog server (for Active Directory
        authentication) or the host name or IP address of an LDAP server
        (for Other LDAP server types).
    -   **Port** - Optionally, change the server port number. By
        default, the port number is 389.
    -   **SSL** - Select if using SSL. When you select this option, the
        default port number adjusts to 636.
2.  Optionally, click **Add Server** to add another LDAP server. To
    remove a server from the list, click **Remove**.
3.  Enter information and make selections:
    -   **Server Type** - Select a server type (Active Directory or
        Other LDAP).

    -   **Manager DN** - Enter the distinguished name of a user in the
        domain administrators group. An example that follows the user's
        base DN is:

            cn=admin,cn=users,dc=example,dc=com

    -   **Manager Password** - Enter the password for the Manager DN.
4.  Click **Validate** to ensure your setup is valid.
5.  Click **Next**. The second panel (Configure LDAP Plugin) of the LDAP
    Configuration wizard appears. LDAP Configuration Wizard (Configure
    LDAP Plugin) ![](plugins/servlet/confluence/placeholder/unknown-attachment "%28LDAPAuthenticator%29LDAPAuthentication.LDAP_Configuration_Wizard_2.png"){.confluence-embedded-image}
6.  Enter information and make selections:
    -   **Login Name Attribute** - Select the LDAP record attribute used
        as the user name. Note: You can edit the list of selections by
        adding attributes on the Mappings page of the LDAP configuration
        area (Advanced &gt; Settings &gt; LDAP).

    -   **Users Base DN** - Enter the user's base distinguished name.
        For example, if your domain is ad.zenoss.com, then your user's
        base DN might be:

            dc=Users,dc=ad,dc=com

    -   **Groups Base DN** - Enter the DN for the branch of your LDAP
        database that contains group records. These group records are of
        the LDAP class "groupOfUniqueNames," and the entry CN attribute
        constitutes the group name.

    -   **User Filter** - Specify a free-form LDAP filter expression to
        be added to the default user search filter. The default user
        search filter and this additional search filter are combined as
        an AND expression. Records must satisfy both filters to be found
        using the various user searches. Any value specified in this
        field must follow correct LDAP search filter syntax.

    -   **Default User Roles** - Specify one or more roles (in a
        comma-delimited list) to be given to all users authenticated
        from your LDAP tree. Zope expects all users - anonymous as well
        as authenticated - to have the role Anonymous.
7.  Click **Next**. The third panel (Map LDAP Groups to Local Groups) of
    the LDAP Configuration wizard appears. LDAP Configuration Wizard
    (Map LDAP Groups to Local Groups) ![](plugins/servlet/confluence/placeholder/unknown-attachment "%28LDAPAuthenticator%29LDAPAuthentication.LDAP_Configuration_Wizard_3.png"){.confluence-embedded-image}
8.  Enter information and make selections:
    -   **Map LDAP Groups to Roles** - Select this option if you want to
        control user roles within the Zenoss platform Web interface by
        using Active Directory groups, instead of controlling the roles
        directly from within Zenoss platform. Note: If you choose to use
        this option, then you should add the following groups to LDAP:
        -   Zenoss platform Managers
        -   Zenoss platform Users
    -   **LDAP Group** - Select the LDAP group to map to a Zenoss
        platform role.
    -   **Maps to Role** - Select the Zenoss platform role to map the
        LDAP group.
9.  Optionally, click **Add Group Mapping** to map another group. To
    remove a mapped group, click **Remove**.
10. Click **Finish** to complete LDAP configuration.

## Verifying Connectivity and Credentials Outside of Zenoss platform

You can verify that your credential information is valid from the Zenoss
platform server by using the ldapsearch command. To install this
command, use the following for RPM-based systems:

    # yum -y install openldap-clients

as the zenoss user on the Zenoss platform server:

    ldapsearch -LLL -x -b 'BaseDN' -D 'Bind DN' -W -H ldap://LDAP_server-name \
    "sAMAccountName=*" member

## Configuring Local Authentication as a Fallback

You can use local authentication as a fallback in the event that the
LDAP server is unreachable. The local authentication plugin is called
userManager.

1.  Verify that the userManager plugin is available:
    1.  Go to the following URL to access the Zope Management Interface
        (ZMI): http://YourZenossSystem:8080/zport/acl_users/manage
    2.  In the Name column, click **Plugins**.
    3.  Click **Authentication Plugins**.
    4.  Make sure that your LDAP plugin is first in the list of Active
        Plugins. (The userManager plugin must be below it.)
        Authentication Plugins ![](plugins/servlet/confluence/placeholder/unknown-attachment "%28LDAPAuthenticator%29LDAPAuthentication.ListOfActivePlugins.png"){.confluence-embedded-image}
2.  Create a user with fallback capabilities. For example, to allow an
    LDAP user named "zenoss-user" to log in when the LDAP server is
    down:
    1.  Go to Advanced &gt; Settings &gt; Users &gt; Add New User.
    2.  Create a user named "zenoss-user." Note: You must create this
        account before the user logs in with the LDAP credentials. The
        password defined when creating the account in Zenoss platform
        will be valid even when the LDAP server is down.

## Attachments:

-   [(LDAPAuthenticator)LDAPAuthentication.LDAP_Configuration_Wizard_1.png](img/zenpack-ldapauthentication.ldap_configuration_wizard_1.png)
-   [(LDAPAuthenticator)LDAPAuthentication.LDAP_Configuration_Wizard_2.png](img/zenpack-ldapauthentication.ldap_configuration_wizard_2.png)
-   [(LDAPAuthenticator)LDAPAuthentication.LDAP_Configuration_Wizard_3.png](img/zenpack-ldapauthentication.ldap_configuration_wizard_3.png)
-   [(LDAPAuthenticator)LDAPAuthentication.ListOfActivePlugins.png](img/zenpack-ldapauthentication.listofactiveplugins.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [(LDAPAuthenticator)LDAPAuthentication.LDAP_Configuration_Wizard_3.png](img/zenpack-ldapauthentication.ldap_configuration_wizard_3.png)
-   [(LDAPAuthenticator)LDAPAuthentication.LDAP_Configuration_Wizard_1.png](img/zenpack-ldapauthentication.ldap_configuration_wizard_1.png)
-   [(LDAPAuthenticator)LDAPAuthentication.LDAP_Configuration_Wizard_2.png](img/zenpack-ldapauthentication.ldap_configuration_wizard_2.png)
-   [(LDAPAuthenticator)LDAPAuthentication.ListOfActivePlugins.png](img/zenpack-ldapauthentication.listofactiveplugins.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [(LDAPAuthenticator)LDAPAuthentication.LDAP_Configuration_Wizard_1.png](img/zenpack-ldapauthentication.ldap_configuration_wizard_1.png)
-   [(LDAPAuthenticator)LDAPAuthentication.LDAP_Configuration_Wizard_3.png](img/zenpack-ldapauthentication.ldap_configuration_wizard_3.png)
-   [(LDAPAuthenticator)LDAPAuthentication.LDAP_Configuration_Wizard_2.png](img/zenpack-ldapauthentication.ldap_configuration_wizard_2.png)
-   [(LDAPAuthenticator)LDAPAuthentication.ListOfActivePlugins.png](img/zenpack-ldapauthentication.listofactiveplugins.png)


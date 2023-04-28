# Single Sign-On - SSO SAML Authenticator Integration Service

## Subscription

This integration is a subscription-based Professional Services
engagement. Our Integration Services are offered as subscriptions in
order to provide initial setup and ongoing compatibility and
maintenance. All standard packages are renewable every 12 months from
the date of purchase. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks.

### Authors:

Zenoss Inc.

### Maintainers:

Zenoss Inc.

### Organization:

Zenoss Inc.

### Name:

Single Sign-On (SSO) SAML Authenticator Integration Service

### Release:

1.6.0

### More Information:

## Single Sign-On SSO SAML Authenticator Integration Service

## About:

This ZenPack provides SAML authentication support for Zenoss. See Tested
SAML Identity Providers for a list of what this has been tested with.

## Prerequisites

| Prerequisite       | Restriction                        |
|--------------------|------------------------------------|
| Product            | Zenoss 6.x or higher               |
| Required ZenPacks  | ZenPack.zenoss.PS.Util &gt;= 1.1.0 |
| Other dependencies | xmlsec1 and xmlsec1-openssl        |

## SAML IdP Requirements

1.  Metadata must contain:
    1.  HTTP-Redirect SingleSignonService URL
    2.  X509 key for verifying SAMLResponse messages
2.  SAMLResponse messages must be signed, but not encrypted
3.  Accept signed, unsigned and unencrypted AuthnRequest messages

## Installation

1.  Install `xmlsec1` and `xmlsec1-openssl` RPMs
    1.  Zenoss 5 requires them to be installed in the container,
        something like...
    2.  serviced service shell -s xmlsecinstall -i Zope yum install -y
        xmlsec1 xmlsec1-openssl
    3.  serviced snapshot commit xmlsecinstall
    4.  serviced service restart Zope
2.  Install `ZenPacks.zenoss.SAMLAuthenticator-\*-py2.7.egg`
3.  Restart Zope

NOTE: Newer versions of Zenoss may have different Zope instances for
reporting, API, etc... and these may need to be restarted as well as any
UI facing services like Zauth, zenjobs, and zenjsserver.

## Configuration

1.  Log in to Resource Manager as a user with ZenManager or Manager role
2.  Navigate to Advanced -&gt; SAML Authentication
3.  Enter a value in EntityID, this value should also be set in your IdP
    and will be used by Zenoss to identify itself in SAML AuthnRequests.
    Per SAML documentation (8.3.6)... The syntax of such an identifier
    is a URI of not more than 1024 characters in length. It is
    RECOMMENDED that a system entity use a URL containing its own domain
    name to identify itself.
4.  Enter Paste SAML IdP entity identifier and metadata
5.  Optionally specify an alternative XPath expression for determining
    login.
    Ex: `*//saml:Attribute[@Name='uid']/saml:AttributeValue/text()`
6.  Optionally specify Name ID Policy format. Different IdPs want
    different values, this allows Zenoss to be configured based on what
    the IdP wants in the AuthnRequest. This has no effect on Zenoss SAML
7.  If your IdP requires signed AuthnRequests select "Sign AuthN
    request". Private key and certificate can be supplied or generated
    with the "Generate Self Signed Key/Cert

## Usage

Any users attempting to access Zenoss will be redirected to the
configured 'IdP URL'. To bypass SAML authentication, navigate to Zenoss
with a query string of 'saml=0':
'[https:/](https://github.com/){.external-link}/&lt;zenoss-host&gt;/zport/dmd?saml=0'.

NOTE 1: If you logged in using the IdP then the bypass won't work. You
will have to logout of the IdP and wait for Zenoss session to expire (or
use a different browser or remove the Zenoss session cookie) before you
can use the bypass successfully.

NOTE 2: If you logged in using the SAML bypass, clicking the logout link
will cause you to be redirected to the configured 'IdP URL'. You can
bypass this with the the path 'logoutUser':
'[https:/](https://github.com/){.external-link}/&lt;zenoss-host&gt;/zport/dmd/logoutUser'.

## Logs

SAML errors will be logged in Zope's /opt/zenoss/log/event.log

## Tested SAML Identify Providers

-   SimpleSAMLphp
-   SalesForce
-   OpenAM
-   OneLogin
-   Azure AD
-   ADFS
-   Ping Identity
-   SSO Circle

## Implementation Details

### Overview

When a user attempts to access a resource requiring authorization (e.g.,
permission zenoss.View), SAMLAuthenticator's challenge implementation
will redirect the user to the configured SAML IdP. When the IdP has
authenticated the user, the browser is directed to post a hidden form
(via JavaScript) containing a Base64-encoded SAMLResponse to be POSTed
to Zenoss.

The SAMLAuthenticator plugin decodes the response via its
authenticateCredentials implementation and attempts to validate its
signature using the configured IdP's certificate. If the SAMLResponse is
valid, the username is extracted and stored as a session variable.

When a user attempts to access a resource requiring authorization after
their Zenoss session has expired, they are again redirected to the
configured SAML IdP.

### Tracking Initial URL

The SAMLAuthenticator sends the initial URL to the IdP using RelayState.
It is expected that the IdP will return RelayState unmodified.

## Change Log

**1.4.1**

-   Features
    -   Expose ability to logout and be directed to the Zenoss login
        page (NOT be forwarded to the IdP)
-   Bug fixes
    -   When logged in through SAML remove prompt for password on the
        Settings and User Settings page

**1.4.0**

-   Features
    -   Support for Single Logout (SLO) added
    -   Improved integration with Zenoss Analytics
    -   Use RelayState to persist original url request rather than
        session

**1.5.0**

-   Features
    -   Support for signed AuthNRequest
    -   Add possibility to configure SLO Response Redirect URL
    -   move common code to PS.util ZenPack

**1.6.0**

-   Features
    -   Add config entry for user ID field
-   Bug fixes
    -   Fix hardcoded NameIDFormat for service provider metadata

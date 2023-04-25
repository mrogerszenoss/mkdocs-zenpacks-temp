# Web Transactions

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.PS.WebTransaction

**ZenPacks.zenoss.PS.WebTransaction**

Contents

-   [About](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions#about){.external-link}
-   [Prerequisites](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions#prerequisites){.external-link}
-   [Usage:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions#usage){.external-link}
    -   [Datasource Recipes:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions#datasource-recipes){.external-link}
    -   [Web Transaction Success Validation:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions#web-transaction-success-validation){.external-link}
    -   [Custom Recipe:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions#custom-script-methods){.external-link}
        -   Examples
    -   [Troubleshooting / Debugging Transactions:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions#troubleshooting-debugging-transactions){.external-link}
-   [Selenium Grid Transaction Execution:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions#selenium-grid-transaction-execution){.external-link}
-   Changelog

**[About](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions#id1){.external-link}**

A **Web Transaction** is an interaction, of one or multiple steps,
between a web browser & server. A web transaction example could be the
submission of authentication credentials and validating the expected
page shows after login.

**Releases:**

1.0.1 - Automated build fixes \[SVC-3399\]

1.0.0 - Initial Release

-   SVC-3360 Datasource UI enhancements
-   SVC-3218 Datasource UI
-   SVC-3152 Build testing/polling infrastructure & framework

**What this ZenPack delivers**:

1.  Use an actual Web Browser to perform Web Transactions
2.  Perform simple static, scripted transaction testing of web
    applications
3.  Perform web transaction testing from a Zenoss Collector or Selenium
    Grid Instance
4.  Web Transaction testing results of:
    1.  Metric for time taken to perform the full transaction
    2.  Events for failed web page element location and validation of
        web page element values and/or attribute values

**What this ZenPack does not intend to be**:

1.  Multiple location Web Transaction testing platform
2.  Multiple browser Web Transaction testing platform
3.  A complex Web Transaction tester
4.  An extractor of values from web pages to Datapoints

## [Prerequisites](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions/blob/master/ZenPacks/zenoss/PS/WebTransactions/README.rst#id2){.external-link}

The table lists the Zenpack dependencies.

| Prerequisite       | Restriction                                                                                                                |
|--------------------|----------------------------------------------------------------------------------------------------------------------------|
| Product            | Zenoss 6.2.1 or higher                                                                                                     |
| Required ZenPacks  | ZenPacks.zenoss.ZenPackLib &gt;= 2.1.2, ZenPacks.zenoss.PythonCollector &gt;= 1.11.0, ZenPacks.zenoss.PS.Util &gt;= 1.11.2 |
| Other dependencies | Selenium Grid, Chromium Web Browser                                                                                        |

## [Installation:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions/blob/master/ZenPacks/zenoss/PS/WebTransactions/README.rst#id3){.external-link}

Non-Cloud Zenoss users should be aware that docker images will also need
to be installed with the ZenPack. Installation instructions and files
should be provided with the ZenPack.

## [Usage:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions/blob/master/ZenPacks/zenoss/PS/WebTransactions/README.rst#id4){.external-link}

The goal of this ZenPack is to provide a method to perform a known,
defined test against web applications in order validate and monitor
health and performance. Using the concept of a recipe to encapsulate a
defined Web Transaction test for easy re-use. These recipes are
selectable and configured from the "*Web Transaction*" datasource.

This ZenPack delivers Web Transaction monitoring using Selenium Grid.
"*Selenium Grid allows the execution of WebDriver scripts on remote
machines by routing commands sent by the client to remote browser
instances*" \[<https://www.selenium.dev/documentation/grid/>\]. By using
Selenium, Web Transactions are run through an actual Web Browser. This
ZenPack currently makes exclusive use of the Chromium browser.

### [Datasource Recipes:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions/blob/master/ZenPacks/zenoss/PS/WebTransactions/README.rst#id5){.external-link}

-   **HTTP - Get** - Perform a simple HTTP Get request and optional
    content verification.
-   **Login - Basic Auth** - Perform a simple Basic Auth test and
    optional content verification.
-   **Login - Form** - Perform authentication by submitting login
    credentials via a web form. This is achieved by providing the form
    elements locator information and data to submit, in the recipe
    configuration.
-   **Custom** - Not a specific recipe, allows you use python and Web
    Transaction methods to define a customized Web Transaction test.

### [Web Transaction Success Validation:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions/blob/master/ZenPacks/zenoss/PS/WebTransactions/README.rst#id6){.external-link}

To validate the success of a Web Transaction, use the Datasource Recipe
verify fields. All Web Transaction Recipes have the same four
verification fields: "*Verify Element*", "*Verify Text Value*", "*Verify
Element Attribute*", "*Verify Element Attr Value*". An element is a part
of a web page, which can be seen by looking at the web page source. The
verify Element value can be a HTML tag name, tag 'id' attribute value,
HTML DOM XPath, or tag class value. If content validation is desired,
the "*Verify Element*" will be a required field while the remaining
verify fields are not all required.

Web Transaction recipes that interact with an element (e.g. filling an
input box, clicking) follow the same logic as "*Verify Element*".

Recipe fields that define a "*Value*" to be verified, can also use
zProperty or cProperty fields (e.g. `${here/cWebTransactionPassword}`).
This is especially useful for password type values or re-use of
monitoring templates by not hardcoding values into the template.

**NOTE**: Transaction validation does not include SSL certificate
validation. All certificate errors are ignored.

### [Custom Recipe:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions/blob/master/ZenPacks/zenoss/PS/WebTransactions/README.rst#id7){.external-link}

When there is not a Recipe that fits the testing need, there is the
"Custom" Recipe option. A Custom recipe is basically using the special
methods in a python script. These methods are special in that they
combine and/or enhance the basic capability provided by the
selenium-python driver.

Before any Custom Recipe script is performed, the maximum wait time for
a web page to load is set to the "*zPageLoadTimeout*" value and
a `driver.get()` is performed on the URL defined in the datasource
configuration. The defined custom recipe actions are then performed.

ZenPack provided methods:

-   **findElement** - Find the first matching element in the HTML DOM.
    Search by tag name, tag 'id' attribute value, XPath, tag class.
    Timeout to find element, defined in the "*zFindElementTimeout*"
    property (*default value is 10*). Elements can be interacted with in
    a number of ways; click(), send_keys(), etc.
    (Reference: <https://www.selenium.dev/documentation/webdriver/elements/interactions/>)
-   **verifyElement** - uses "*findElement*" and then verifies one or
    both of element's text or attribute value. Some element values do
    change dynamically after initial page load and this method will wait
    to match desired result. Timeout to match element's value is defined
    in the "*zVerifyElementValueTimeout*" property (*default is 10
    seconds*).
-   **clickElement** - uses "*findElement*" and then waits until the
    element is clickable. The click wait re-uses the timeout defined in
    the "*zFindElementTimeout*" property.

Exposed Selenium-python Objects/Methods:

-   **driver** - selenium web driver. The above methods should provide
    all the functionality required for a Web Transaction test. But if
    they do not, the selenium-python webdriver is exposed here. Usage
    and its methods are outside the scope of this document but can be
    found
    at <https://selenium-python.readthedocs.io/getting-started.html>.

**NOTE**: XPath, also known as XML Path, is one of the most commonly
used locators in Selenium WebDriver that can help you navigate through
the HTML structure of a page. It can be used for HTML and XML documents
to locate any element in a web page using HTML DOM structure. How to use
or define an XPath to locate an element is beyond the scope of this
document.

#### [Examples](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions/blob/master/ZenPacks/zenoss/PS/WebTransactions/README.rst#id8){.external-link}

The examples provided are more snippets to highlight the use of the Web
Transaction methods in a Custom Recipe. They should not be seen as
best-practice examples.

**Web Login Form** Example

This example is what the "Login - Form" recipe would be as a Custom
Recipe.

    findElement('username').send_keys('${here/cWebTransactionUser}')
    findElement('passwrd').send_keys('${here/cWebTransactionPassword}')
    clickElement('loginButton')
    verifyElement('TITLE', verifyText='Logged In')

"*username*", "*passwrd*", & "*loginButton*" are the 'id' attribute
values for HTML "INPUT" tags. Refer to the "*findElement*" info above
for more info on what is used to locate web page elements.

"TITLE" is the HTML tag to be found and then verify that its text value
is 'Logged In'. The "*verifyElement*" method can take up to four
parameters; **ElementToFind**, **verifyText**, **verifyAttr**,
and **verifyAttrVal**. The verify parameters are optional but at least
one needs to be defined.

    # Verify the Element's Text value:
    # e.g. <TITLE>Logged In</TITLE>
    verifyElement('TITLE', verifyText='Logged In')

    # Verify an Element's attribute value
    # e.g. <DIV id="header" description="Tuna Harvest Table">Charlie Tuna</DIV>
    verifyElement('DIV', verifyAttr='description', verifyAttrVal='Tuna Harvest Table')

    # Very both the Element's Text & Attribute value
    # e.g. <TABLE><TR id="firstRow"><TD id="exTarget" descr="Apples">Applesauce</TD>.....
    verifyElement('exTarget', verifyText='Applesauce', verifyAttr='descr', verifyAttrVal='Apples')

**Conditional action/verify** Example

    nfStatus = findElement('//div[@class="down-notification-content"]/h2')
    if nfStatus.get_attribute('textContent') == 'Service is up!':
      findElement('//a[text()="sign in"]').click()
      verifyElement('//h1[@data-uia="login-page-title"]', verifyText='Sign In')

**Multi-Step Transaction** Example

    findElement("username").send_keys("${here/cWebTransactionUser}")
    findElement("passwrd").send_keys("${here/cWebTransactionPassword}")
    findElement("loginButton").click()
    verifyElement("TITLE", verifyText="\n Zenoss:\n Dashboard\n        ")
    findElement("Infrastructure-nav-button").click()
    verifyElement("device_panel_header-inputEl", "/Devices")
    findElement("sign-out-link").click()
    verifyElement("TITLE", verifyText="Login")

A multi-step transaction script could be considered as a 'complex' test,
which this ZenPack does not aspire to deliver or support. This example
is more of an interesting case to test and push the limits of what is
possible.

### [Troubleshooting / Debugging Transactions:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions/blob/master/ZenPacks/zenoss/PS/WebTransactions/README.rst#id9){.external-link}

The best method for debugging Web Transaction scripts or recipes is to
spin up a dedicated debug Selenium Grid instance. Then set its address
in the datasource's "*Command Executor*" configuration parameter or as
the device's "*zSeleniumGridCmdExecutor*" property. Using a dedicated
Selenium Grid instance allows for a variety of different debug options,
e.g. connecting to the Node's VNC port and watching the Web Transaction
play out in the browser. For more information, reference Selenium's
website.

## [Selenium Grid Transaction Execution:](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions/blob/master/ZenPacks/zenoss/PS/WebTransactions/README.rst#id10){.external-link}

This ZenPack bundles a Selenium Grid & Chromium Node services that run
at the collector level. Web Transactions can also be run from external
Selenium Grid instances using the "*zSeleniumGridCmdExecutor*"
zProperty. Its default value being the Zenoss Collector Selenium Grid
address.

The "*SeleniumGridNodeChrome*" service is configured via its service
environmental variables. To modify, use the command line
of `serviced service edit SeleniumGridNodeChrome` and update the
"*Environment*" section. Zenoss Selenium Node's default values are:

    "Environment": [         "SE_EVENT_BUS_HOST=127.0.0.1",         "SE_EVENT_BUS_PUBLISH_PORT=4442",         "SE_EVENT_BUS_SUBSCRIBE_PORT=4443",         "SE_START_XVFB=false",         "SE_NODE_HOST=nc{{ plus 1 .InstanceID }}",
        "JAVA_OPTS=-Dwebdriver.chrome.whitelistedIps=",
        "SE_NODE_MAX_SESSIONS=2",
        "SE_NODE_SESSION_TIMEOUT=30"
    ],

**Note**: You should not change the first 6 options.

Option details:

> "**JAVA_OPTS=-Dwebdriver.chrome.whitelistedIps=**" - to prevent
> container error messages
> of `[SEVERE]: bind() failed: Cannot assign requested address (99)`
>
> "**SE_NODE_MAX_SESSIONS=2**" - maximum transaction sessions that can
> run concurrently
>
> "**SE_NODE_SESSION_TIMEOUT=30**" - Maximum time a transaction may run.
> zProperty timeouts should not be greater than this value. This is the
> hard limit for how long a Web Transaction test may take to complete.

For more information,
reference <https://github.com/SeleniumHQ/docker-selenium#configuring-the-containersbleck>

## [Changelog](https://github.com/zenoss/ZenPacks.zenoss.PS.WebTransactions/blob/master/ZenPacks/zenoss/PS/WebTransactions/README.rst#id11){.external-link}

1.0.1 - Automated build fixes \[SVC-3399\]

1.0.0 - Initial Release

-   SVC-3360 Datasource UI enhancements
-   SVC-3218 Datasource UI
-   SVC-3152 Build testing/polling infrastructure & framework



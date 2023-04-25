# Web-Based Synthetic Transactions

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.ZenWebTx

## Web-Based Synthetic Transactions ZenPack

The ZenWebTx ZenPack allows you to test the availability and performance
of Web sites by performing some of the same activities performed by your
user community.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 3.0.5 [Download](https://delivery.zenoss.com/){.external-link}
            Released on 2021/12/01
            Tested with Zenoss
Resource Manager 6.6.0 and Zenoss Cloud 7.0.20

Version 3.0.4 [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2021/03/31:   Tested with Zenoss Resource Manager 6.5.0 and Zenoss Cloud

## Background

The ZenPacks.zenoss.ZenWebTx ZenPack adds the zenwebtx daemon, which
enables availability and performance monitoring of web sites through
synthetic HTTP transactions.

Synthetic transactions perform some of the same activities performed by
your user community. You create one or more tests that mimic user
actions in a Web browser. Zenoss platform then performs these tests
periodically, creating events when a test fails or exceeds a time
threshold.

Additionally, Zenoss platform can record data for each test run, such
as:

-   Time required for the test to execute
-   Time taken for any portion of the test to complete
-   Values extracted from Web pages during the test

This ZenPack uses a scripting language called twill to describe the
steps of a test. These steps include actions such as:

-   Clicking a link
-   Completing form fields
-   Assertions, which check for the presence or absence of text on a
    page. In addition, you can extract data from the Web page and record
    the numeric values that are a part of these patterns
-   Descriptions of data to collect during the test

You can write twill commands manually. You also can use a Firefox add-on
called TestGen4Web to record a browser session that this ZenPack then
translates into twill commands. The zenwebtx daemon processes the twill
commands periodically, recording data and creating events as
appropriate.

## Configuration Properties

The ZenPack introduces the following zProperties:

-   zWebTxAgent - User agent. Default is 'ZenWebTx'.
-   zWebTxUser - Valid WebTx user name. Default is blank.
-   zWebTxPassword - Valid WebTx password. Default is blank.
-   zWebTxRealm - Initial authentication realm. Default is blank.
-   zWebTxGetComponentConfigs - The property used to avoid a performance
    bottleneck when the zenwebtx service tries to get components
    configs. In a case when you don't have any WebTX data sources on
    components, you can disable the property to improve the
    performance. Default is False(disabled).

## Data Points

Data produced by any Zenoss platform data source are called data points.
`WebTx` data sources contain two default data points:

-   **totalTime** – Number of seconds taken to complete the entire
    transaction.
-   **success** – Returns 1 (success) or 0 (failure), depending on
    whether or not the transaction succeeded.

You can create other data points by using the extract and printTimer
twill commands, which output data values when the twill commands are
run. You must create new data points with the same name you used in
those commands to bring that data into Zenoss platform.

The zenwebtx daemon supports XPath queries to extract data from XML
documents.

## Event Generation

There are several situations in which this ZenPack creates events in
Zenoss platform. These events use the component and event class
specified on the Data Source tab. These situations are:

-   The zenwebtx daemon is unable to retrieve a page during the
    transaction.
-   One of the twill commands fails, such as finding text that does not
    exist or following a link that does not exist.
-   The timeout (specified on the Data Source tab) is exceeded.
-   A threshold defined for one of the data points in this data source
    is exceeded. Thresholds are defined in the monitoring template that
    contains the data source.

## Enable Monitoring

To create a `WebTx` data source:

1.  From the data sources area, click Add Data Source.

2.  In the Create Data Source dialog, enter the name of the new data
    source, and then select the data source type `WebTx`.

3.  Click Submit.

4.  Select the data source to edit it. Enter information or make
    selections to specify how and when this data source's Web
    transactions are performed, and which data should be collected:
    WebTx Data Source Options

    <table>
    <tbody>
    <tr markdown="1">
    <th>Option</th>
    <th>Description</th>
    </tr>

    <tr markdown="1">
    <td>Name</td>
    <td>Displays the name of the data source that you specified in the Create Data Source dialog. This name is used in thresholds and graph definitions to refer to the data collected by this data source.</td>
    </tr>
    <tr markdown="1">
    <td>Source Type</td>
    <td>Set to <samp>WebTx</samp>, indicating that this is a synthetic Web transaction data source. You cannot edit this selection.</td>
    </tr>
    <tr markdown="1">
    <td>Enabled</td>
    <td>Set to True (the default) to collect information from this data source. You may want to set this value to False to disable data sources when developing the data source, or when making changes to the Web application being tested.</td>
    </tr>
    <tr markdown="1">
    <td>Component</td>
    <td>Any time the Web transaction fails, Zenoss platform generates an event. Use this field to set the Component field of the generated event.</td>
    </tr>
    <tr markdown="1">
    <td>Event Class</td>
    <td>Select the event class of the event generated by this data source. Normally, this is set to /Status/Web (according to the value set on the data source).</td>
    </tr>
    <tr markdown="1">
    <td>Timeout</td>
    <td>Specify the number of seconds that zenwebtx will attempt to execute this data source's commands before it generates an error event.</td>
    </tr>
    <tr markdown="1">
    <td>Cycle Time</td>
    <td>Specify the number of seconds that zenwebtx will wait between the start of one test run and the start of the next.</td>
    </tr>
    <tr markdown="1">
    <td>User Agent</td>
    <td>Specify the text that zenwebtx will present to target Web sites to identify itself.</td>
    </tr>
    <tr markdown="1">
    <td>Disable SSL Verification </td>
    <td><p>Set to False (the default) to collect information from this data source with enabled SSL verification.  You may want to set this value to True to disable SSL verification while collecting information from this data source. </p>
    <p>CAUTION! This action is security risking. Disable SSL verification only if you TOTALLY sure that data source is trusted. For example, when you use self-signed SSL certificate for testing purposes.</p></td>
    </tr>
    </tbody>
    </table>

5.  Click Save to save the specified settings.

6.  Select Script. From here, you will specify the details of the
    transaction. Information here also helps you debug twill commands
    when setting up the data source.

7.  Note: If you provide values for Initial User, Initial Password, and
    Initial Authentication Realm, Zenoss platform will use these
    credentials before accessing the URL specified for Initial URL. All
    three (Initial User, Initial Password, and Initial Authentication
    Realm) must be present; otherwise, the values are ignored. Enter
    information or make selections: WebTx Script Settings

    <table>
    <tbody>
    <tr markdown="1">
    <th width="50%">Option</th>
    <th width="50%">Description</th>
    </tr>

    <tr markdown="1">
    <td>Initial URL</td>
    <td>Specify the URL of the page where the transaction will start. This field frequently contains a TALES expression to refer to a device's ID or IP address, such as <samp>http://${dev/id}</samp> or <samp>http://${dev/manageIp}</samp>.</td>
    </tr>
    <tr markdown="1">
    <td>Initial User</td>
    <td>Specify the user name for authentication.</td>
    </tr>
    <tr markdown="1">
    <td>Initial Password</td>
    <td>Specify the user password for authentication.</td>
    </tr>
    <tr markdown="1">
    <td>Initial Authentication Realm</td>
    <td>Specify the basic HTTP authentication realm.</td>
    </tr>
    <tr markdown="1">
    <td>TestDevice</td>
    <td>Use this field to test and debug twill commands. Enter the ID of a device, and then click Test Twill Commands to execute the twill commands against the device. If you do not specify a device, then Zenoss platform will select a device for you.</td>
    </tr>
    <tr markdown="1">
    <td>Upload Recording</td>
    <td>Upload a Web session recording generated by the Firefox TestGen4Web add-on. Enter or browse to the recording location.
    <p>If you specify a file here, and then click Save, Zenoss platform translates the file to twill commands and replaces the contents of the Twill Commands field with the newly translated commands.</p></td>
    </tr>
    <tr markdown="1">
    <td>Twill Commands</td>
    <td>Specify the number of seconds that zenwebtx will wait between the start of one test run and the start of the next.
    <p>Enter twill commands that Zenoss platform will execute to produce values and events for the data source.</p>
    <p>If you select this action, then the current contents of the Twill Commands field is completely replaced. Zenoss platform does not save the replaced information.</p></td>
    </tr>
    </tbody>
    </table>

8.  Click Save to save the data source.

## Creating twill Commands

This ZenPack uses twill to specify the steps of a Web test. Each `WebTx`
data source has a field that contains the twill commands that describe a
Web transaction. You can create this list of twill commands manually, or
you can record a session in a browser and use that as the basis for your
data source.

Some twill commands specify an action, such as following a specific link
on a page or entering data in a form field. Other twill commands specify
a test, such as searching for specific text on a page or making sure the
title does not contain specific text.

## Creating twill Commands from TestGen4Web

**Attention: TestGen4Web was deleted from Firefox
store. **You can use this section only if you have saved session files,
created by TestGen4Web Firefox add-on.

The TestGen4Web Firefox add-on allows you to record browser sessions.
This ZenPack can take these sessions and convert them to twill, creating
a starting point for developing WebTx data sources.

Follow these general steps to
convert a TestGen4Web session:

1.  From the Script page of a WebTx
    data source in Zenoss platform, browse to and select your saved
    session file.
2.  Click Save to convert the
    TestGen4Web session to twill. The newly converted commands appear in
    the Twill Commands field on the page, replacing any previous twill
    commands in that area.

## Creating twill Commands Manually

Even if you use TestGen4Web to initially create twill commands, you will
frequently want to edit these commands manually to add data points or
additional content checks. The Test Twill Commands button on the Script
page is helpful when testing twill commands as you create or edit them.

You also can execute twill commands interactively by using the twill-sh
program from the command line. This program lets you enter commands one
at a time and then inspect the pages that come back.

With Zenoss 5.x you will want to do this from inside the zenwebtx
container, on the specific collector if it applies, and switch to the
zenoss user with su - zenoss.

Invoke twill-sh with:

    PYTHONPATH=$PYTHONPATH:$ZENHOME/ZenPacks/ZenPacks.zenoss.ZenWebTx-3.0.0-py2.7.egg/ZenPacks/zenoss/ZenWebTx/lib
    $ZENHOME/ZenPacks/ZenPacks.zenoss.ZenWebTx-3.0.0-py2.7.egg/ZenPacks/zenoss/ZenWebTx/bin/twill-sh

Within twill-sh, use the help command to list available commands and see
a command descriptions. Of particular interest are these commands:

-   showforms – Lists the forms on the page and the fields within each.
-   showlinks – Lists the links on the page.
-   show – Lists the source HTML from the page.
-   exit – Quits the twill-sh program.

Often the most convenient way to use twill-sh is to create a text file
that contains your twill commands. You can then specify that file on the
command line when you invoke twill-sh. This lets you analyze problems
that occur.

Invoke twill-sh with a text file as such:

    PYTHONPATH=$PYTHONPATH:$ZENHOME/ZenPacks/ZenPacks.zenoss.ZenWebTx-3.0.0-py2.7.egg/ZenPacks/zenoss/ZenWebTx/lib
    $ZENHOME/ZenPacks/ZenPacks.zenoss.ZenWebTx-3.0.0-py2.7.egg/ZenPacks/zenoss/ZenWebTx/bin/twill-sh -i myTwillCommands.txt

The `-i` option instructs twill-sh to stay in the twill shell rather
than exiting when it finishes running the commands in the
myTwillCommands.txt file.

## Monitoring through Proxy Servers

The zenwebtx daemon can access Web servers through HTTP proxy servers
and non-authenticating HTTPS proxy servers.

To configure the zenwebtx daemon to use a proxy, you must define the
http_proxy and https_proxy environment variables.

1.  Open the ~zenoss/.bashrc file.

2.  Add the following lines:

        export http_proxy=http://Address:Port/
        export https_proxy=http://Address:Port/

    where `Address` is the address of your HTTP or HTTPS proxy server,
    and `Port` is the port on which your proxy server listens.

## Example Proxy Setup

HTTP and HTTPS proxies frequently listen on port 3128. If your proxy
server is "my.proxyserver.loc" and it uses port 3128, then add these two
lines to the ~zenoss/.bashrc file:

    export http_proxy=http://my.proxyserver.loc:3128/
    export https_proxy=http://my.proxyserver.loc:3128/

## Testing the Proxy Setup

You can test the proxy setup by using twill-sh, the twill interpreter
shell.

After setting up the proxy information in the ~zenoss/.bashrc file,
follow these steps to test your setup:

1.  Make sure http_proxy and https_proxy are defined in your current
    shell:

        $ source ~zenoss/.bashrc

2.  Launch the twill shell:

        PYTHONPATH=$PYTHONPATH:$ZENHOME/ZenPacks/ZenPacks.zenoss.ZenWebTx/ZenPacks/zenoss/ZenWebTx/lib
        $ZENHOME/ZenPacks/ZenPacks.zenoss.ZenWebTx/ZenPacks/zenoss/ZenWebTx/bin/twill-sh

3.  Try to retrieve a URL through HTTP or HTTPS. For example, to
    retrieve the Zenoss platform home page, enter:

        go http://www.zenoss.com

    You should see a message similar to this:

        current page: http://www.zenoss.com

    If an error message appears, then your proxy may not be correctly
    configured in the ~zenoss/.bashrc file.

4.  Exit the twill shell:

        exit

## Known Issues

-   ZPS-7555 - Unable to monitor WebTx datasource with local address
    through UI on CZ (WebTx timed out). This is related to the testing
    datasource from UI, regular collection works fine.
-   ZPS-7945 - Unable to upload Web
    session recording generated by the Firefox TestGen4Web
    add-on. TestGen4Web add-on was removed completely from store by it's
    developers.

## Changes

3.0.5

-   Add a checkbox in the datasource
    to toggle cert validation (ZPS-6994)
-   Tested with Zenoss Resource
    Manager 6.6.0 and Zenoss Cloud 7.0.20

3.0.4

-   Fix Webtx checks failing silently (ZPS-7534)
-   Fix UI bug on the Webtx datatsource (ZPS-7538)
-   Tested with Zenoss Resource Manager 6.5.0 and Zenoss Cloud

<dl markdown="1">
<dt markdown="1">
3.0.3
</dt>
</dl>

-   Use zWebTxAgent zProperty value as the user agent for all WebTx
    datasources. (ZPS-1419)
-   Fix performance bottleneck when zenwebtx service tries to get
    components configs. (ZPS-1606)
-   Recover zenwebtx OS process. (ZPS-3168)
-   Tested with Zenoss Resource Manager 6.1.2, Zenoss Resource Manager
    5.3.3, Zenoss Resource Manager 4.2.5.

3.0.1

-   Initial password is not displayed in ZenWebTx datasource. (ZPS-1289)

<dl markdown="1">
<dt markdown="1">
3.0.0
</dt>
</dl>

-   Added compatibility with Zenoss 5.x for metric publishing

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


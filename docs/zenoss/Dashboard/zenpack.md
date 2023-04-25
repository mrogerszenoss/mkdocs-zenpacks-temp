# Dashboard

@lb[](img/zenpack-zenpack-general.png)

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks){.external-link} to view all
available Zenoss Open Source ZenPacks.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2, or later

### Name:

ZenPacks.zenoss.Dashboard

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.Dashboard){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.Dashboard.git){.external-link}

## Dashboard ZenPack

A Javascript widget framework for creating portlets and sharing
dashboards

## Support

This is an Open Source ZenPack developed by Zenoss, Inc. Enterprise
support for this ZenPack is available to commercial customers with an
active subscription.

## Releases

Version 1.3.12- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2021/02/08:   Compatible with Zenoss Resource Manager 6.5.0 and Zenoss Cloud

<!-- -->

Version 1.3.11- [Download](https://delivery.zenoss.com/){.external-link}:   Released on 2020/12/10:   Compatible with Zenoss Resource Manager 6.5.0 and Zenoss Cloud

<!-- -->

Version 1.0.6- [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.Dashboard/1.0.6/ZenPacks.zenoss.Dashboard-1.0.6.egg){.external-link}:   Released on 2015/08/20:   Compatible with Zenoss Resource Manager 5.x

## Background

This ZenPack introduces a new widget framework for creating portlets and
sharing dashboards. Users may define any number of portlets and
dashboards, which may be shared globally or with specific groups.

## Sharing Dashboards

By default, a dashboard has three levels of visibility:

1.  Owner
2.  Group
3.  Global

These levels allow a dashboard to remain private during development, and
then published to a wider audience upon completion. This ZenPack adds
the dashboard relationship to the following objects:

1.  UserSettings - private dashboards
2.  GroupSettings - group dashboards
3.  UserSettingsManager - global dashboards

Changing the visibility of a dashboard object moves it from one
relationship to another. For example, the primary path of a private
dashboard named "Test" is
"/zport/dmd/ZenUsers/&lt;USERID&gt;/dashboards/Test". Promoting the
dashboard to global changes the primary path to
"/zport/dmd/ZenUsers/dashboards/Test".

**Note**: Dashboard names must be unique in each relationship context.
You can not promote a private dashboard named "Test" to global if a
global dashboard named "Test" already exists.

## Portlets

The following, default portlets are defined by this ZenPack:

-   Site Window - Displays an iframe on the dashboard
-   Device Chart (5.x only) - Displays a chart with devices from a
    specific device class and graph point
-   Device Issues - Shows devices which currently have events
-   Production State - Shows which devices are in specified production
    states
-   Network Map - D3-forced layout view of the network map
-   Open Events Chart - Shows open events grouped by severity
-   Google Maps - Enables selecting a location, at which the event
    severities at that location are displayed
-   And more...

## Permissions

-   There are no owner-level permissions associated with dashboard
    objects. Any user may edit a dashboard if they have "Change Device"
    permission.
-   Users with "Add DMD Objects" permission may add a dashboard.
-   User with "Delete Objects" permission may remove a dashboard.
-   Permissions are checked both on the client and server.
-   If the Audit ZenPack is installed, all operations on dashboards are
    audited.

The "Add DMD Objects" and "Delete Objects" permissions are are global
roles; the context of dashboard objects can not have permissions applied
to them.

## Writing a new Portlet

Portlets are written in Javascript using ExtJS. A portlet consist of one
ExtJs class that descends from "Zenoss.Dashboard.view.Portlet". The
following example shows a portlet definition.

        /** * A simple portlet that lets users define custom HTML to be displayed * on the application dashboard. This will execute any javascript that is * written. **/
        //1. The portlet must be in the Zenoss.Dashboard.portlets namespace, in which everything is assumed to be a portlet.
        Ext.define
                          ('Zenoss.Dashboard.portlets.HTMLPortlet'
                          , {             extend: 'Zenoss.Dashboard.view.Portlet'                           ,             //2. An alias (required) is used to instantiate the portlet when the dashboard is rendered alias: 'widget.htmlportlet'                           ,             height: 100,             //3. The default title displays on the dropdown of available Portlets title: 'HTML Portlet'                           ,                   //4. All default config properties of portlets should be defined on the class content: "<h1>Blank HTMLPortlet</h1>"                           ,             initComponent: function                           ()                           {                       Ext.apply                           (this, {                     html: this.content                 });

                this.callParent
                          (arguments);
            },
            //5. getConfig is called when serializing portlets. It returns the options that are saved on the portlet.
            // height and refresh rate are included from the parent class
            getConfig: function
                          () {                 return {                     html: this.content                 };
            },
            //6. applyConfig is where you apply the configuration to the portlet. This can include updating stores and content.
            applyConfig: function
                          (config) {                 if (config.html && config.html != this.content) {                     this.content = config.html;                     this.update                           (config.html, true);                 }
                this.callParent
                          ([config]);
            },
            //7. Template method for what happens when a portlet refresh is requested.
            onRefresh: function
                          () {                   },
            //8. Any custom configuration fields for your portlet are defined here. The caller expects an array in return.
            getCustomConfigFields: function
                          () {                 var fields = [                           {                     xtype: 'textarea'                           ,                     fieldLabel: _t('Content'),                     name: 'html'                           ,                     value: this.content,                     allowBlank: false,                     height: 100,                     width: 200                 }
                          ]
                          ;
                return fields;
            }
        });

## Known Issues

The following issues have been identified in the most recent release of
this ZenPack.

1. When the visibility of a dashboard is changed, the dashboard name is
not checked for uniqueness in the new context.

## Changes

<dl markdown="1">
<dt markdown="1">
1.3.12
</dt>
</dl>

-   fix a template to make it compatible with newer version of zope

<dl markdown="1">
<dt markdown="1">
1.3.11
</dt>
</dl>

-   fixed Open Events Chart portlet shows incorrect events for the last
    x days
-   added check whether portlet is locked on the backend side during
    update

<dl markdown="1">
<dt markdown="1">
1.0.6
</dt>
</dl>

-   Added Event Line Chart Portlet
-   Ability to fullscreen a portlet

<dl markdown="1">
<dt markdown="1">
1.0.5
</dt>
</dl>

-   Added searching and devices to the Watch List Portlet

<dl markdown="1">
<dt markdown="1">
1.0.4
</dt>
</dl>

-   Now includes the Impact portlet

<dl markdown="1">
<dt markdown="1">
1.0.3
</dt>
</dl>

-   Users without a global role could not access the dashboard

<dl markdown="1">
<dt markdown="1">
1.0.2
</dt>
</dl>

-   The refresh interval wasn't being updated properly

<dl markdown="1">
<dt markdown="1">
1.0.1
</dt>
</dl>

-   Now works on IE10 and IE11

<dl markdown="1">
<dt markdown="1">
1.0.0
</dt>
</dl>

-   Initial Release

## Attachments:

-   [Add_portlet.png](img/zenpack-add_portlet.png)
-   [Default_dashboard.png](img/zenpack-default_dashboard.png)
-   [Edit_dashboard.png](img/zenpack-edit_dashboard.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [Add_portlet.png](img/zenpack-add_portlet.png)
-   [Default_dashboard.png](img/zenpack-default_dashboard.png)
-   [Edit_dashboard.png](img/zenpack-edit_dashboard.png)
-   [Separate_dashboard.png](img/zenpack-separate_dashboard.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [Add_portlet.png](img/zenpack-add_portlet.png)
-   [Default_dashboard.png](img/zenpack-default_dashboard.png)
-   [Edit_dashboard.png](img/zenpack-edit_dashboard.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [Separate_dashboard.png](img/zenpack-separate_dashboard.png)


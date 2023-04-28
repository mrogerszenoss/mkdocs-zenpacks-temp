# WSMAN Support

## Open Source

This ZenPack is developed and supported by Zenoss Inc. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact/){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1091){.external-link}
to view all available Zenoss Open Source ZenPacks.

### Maintainers:

Zenoss

Inc.

### Organization:

Zenoss, Inc.

### License:

GNU General Public License, Version 2

### Name:

ZenPacks.zenoss.WSMAN

### More Information:

[GitHub page/HomePage](https://github.com/zenoss/ZenPacks.zenoss.WSMAN){.external-link}

### Git Sources (For Cloning):

[Link](https://github.com/zenoss/ZenPacks.zenoss.WSMAN.git){.external-link}

## WSMAN ZenPack

This ZenPack provides a new *WSMAN* data source type that makes it easy
to collect metrics from a WSMAN provider. It also provides a new
*WSMANPlugin* modeler plugin base class that simplifies modeling devices
and applications that support WSMAN.

## Releases

Version 1.0.5 [Download](https://storage.googleapis.com/zenpacks/ZenPacks.zenoss.WSMAN/1.0.5/ZenPacks.zenoss.WSMAN-1.0.5.egg){.external-link}:   Released: 2019-10-28:   Compatible with Zenoss Cloud, 5.3 - 6.2:   Requires: [PythonCollector ZenPack](http://help.zenoss.com/display/in/PythonCollector){.external-link}

## Features

The following features are available to help you model and monitor
information available via WSMAN.

### WSMAN Datasource Type

The *WSMAN* data source type added by this ZenPack allows you to add a
WSMAN datasource with the following new new data source properties.

Namespace:   The WSMAN namespace. This must be specified and there is no default
    value. A common example would be root/dcim.

CIM Class:   The CIM Class to query. This must be specified and there is no
    default value.

Query:   Optional. The query to execute that will return the desired
    record(s). This must be specified and there is no default value.

Result Component Key:   Optional. Only used in cases where the WSMAN data source is in a
    monitoring template that gets bound to components. In this case
    *Result Component Key* should be set to the attribute or column name
    that contains the component identifier in the result set of the
    Query.

Result Component Value:   Optional. Only used in cases where the WSMAN data source is in a
    monitoring template that gets bound to components. In this case
    *Result Component Value* is the value that gets mapped to values in
    the *Result Component Key* column of the result set. Typically this
    takes the form of a TALES expression such as ${here/id} or
    ${here/wsmanInstanceId} if wsmanInstanceID was modeled on your
    component.

Result Timestamp Key:   Optional. Used in both device- and component-bound monitoring
    templates when the query result set has a column noting the time the
    data was originally collected. Like the *Result Component Key* this
    should be the name of an attribute or column name in the results. By
    default this will default to NOW as the collection time.

### WSMANPlugin Modeler Plugin

The *WSMANPlugin* modeler plugin base class allows you to create modeler
plugins that do something with data that is returned from a WSMAN
Enumerate call.

See the following example of a modeler plugin.

     '''Description of what MyWSMANPlugin does.''' from ZenPacks.zenoss.WSMAN.modeler.WSMANPlugin import WSMANPlugin class MyWSMANPlugin(WSMANPlugin): modname = 'ZenPacks.example.MyZenPack.MyChassis' relname = 'mychassis' wsman_queries = { 'DCIM_EnclosureView': '', 'DCIM_SystemView': '', } def process(self, device, results, log): log.info('Modeler %s processing data for device %s', self.name(), device.id) enclosureView = results.get('DCIM_EnclosureView') systemView = results.get('DCIM_SystemView') rm = self.relMap() for inst in SystemView: om = self.objectMap({ 'id': self.prepId(str(inst['ChassisName'])), 'model': inst['Model'], }) rm.append(om) return rm

## Installed Items

### Configuration Properties

-   zWSMANCollectionInterval: Default interval (in seconds) between
    WSMAN datasource collections. (Default: 300)
-   zWSMANMaxObjectCount: Elements returned from the API per request.
    (Default: 50)
-   zWSMANPassword: Password for remote WSMAN service.
-   zWSMANPort: TCP Port of WSMAN service. (Default: 443)
-   zWSMANUsername: Username for remote WSMAN service. (Default: root)
-   zWSMANUseSSL: Use SSL for remote WSMAN service. (Default: true)

## Troubleshooting

-   Incase iDRAC monitoring returns "WSMAN: running timeout", please
    increase zWSMANCollectionInterval value

## Changes

**1.0.5**

-   WSMAN events don't clear.
    (ZPS-4958)
-   Tested with Zenoss Cloud and Zenoss Resource Manager 6.4.1.

**1.0.4**

-   Introduce zWSMANMaxObjectCount zProperty to control the amount of
    returned elements per a request. (ZPS-4484)
-   Prevent the spreading of new connections per a collection cycle.
    (ZPS-4641)
-   Tested with Zenoss Cloud, Zenoss Resource Manager 6.2.1, and Zenoss
    Resource Manager 5.3.3.

**1.0.3**

-   Use datasource severity for events. (ZPS-3563)
-   Add zWSMANCollectionInterval zProperty for WSMAN datasources.
    (ZPS-4013)
-   Tested with Zenoss Cloud, Zenoss Resource Manager 6.2.1, and Zenoss
    Resource Manager 5.3.3.

**1.0.2**

-   Prevent DEBUG txwsman logs when not at DEBUG log level. (SVC-920)
-   Add ability to configure Event Class for WSMAN Data Source.
    (ZPS-3371)
-   Tested with Zenoss Resource Manager 6.1.2.

**1.0.1**

-   Fix "CIMCLass" typo in WSMANDataSource.

**1.0.0**

-   Initial release.

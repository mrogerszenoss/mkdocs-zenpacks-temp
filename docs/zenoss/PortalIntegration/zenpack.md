# Portal Integration

@lb[](img/zenpack-zenpack-general.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Organization:

Zenoss, Inc.

### Name:

ZenPacks.zenoss.PortalIntegration

## Portal Integration ZenPack

Extends Zenoss JSON API to better support integration in external
portals.

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Background

This ZenPack provides JSON API extensions commonly needed for
integration with external portals. Search, identity resolution, and
fetching performance data, events, and status are available.

## Prerequisites

ZenPack has the following dependencies:
:   Zenoss 6.2.1 or higher:   ZenPacks.zenoss.EnterpriseReports, ZenPacks.zenoss.AdvancedSearch

## Installation

Version 1.2.2 submits a job to zenJobs to build new Device indexes. It
is important to stop the *zenjobs* service before performing the ZenPack
install. The job will run after the normal platform restart after ZP
install. If the *zenjobs* service is left accidentally running. Stop it
and reinstall the zenpack.

## Features

### IdentificationRouter

The following JSON API methods are available in the
*IdentificationRouter* router:

`listResolvers`:   Return the list of available device/component name resolution
    schemes.

<!-- -->

`resolve`:   Return the resolved device/component for the id specification using
    the specified `idScheme`.

#### Resolve method idSchemes

The following `idShemes`  available in the `IdentificationRouter`
resolve method

`UidResolver`:   Given an `uid`  (path to an object from `/zport` ), return the
    object.

<!-- -->

`UuidResolver`:   Given an `uuid`  (Universally Unique ID aka guid), return the
    object.

<!-- -->

`GlobalCatalogResolver`:   Query the Zenoss global catalog for an object, using the indices
    available from `dmd.global_catalog.getIndexes()`. Not all fields
    are required.

<!-- -->

`SearchResolver`:   Use the same search method used by the search bar at the top
    right-hand side of the Zenoss user interface to find the object.
    This searches not only the global catalog but also the other
    catalogs.

<!-- -->

`DeviceOrComponentResolver`:   Given a `device`  (name or IP address of a device) and (optionally)
    `component`  (the modeled id of a device's component), return the
    object.

<!-- -->

`ModeledResolver`:   Time value query against a device's "Model Time" or "Last Changed".
    Can be used to find devices that have had a recent model change.

### PortalRouter

The following JSON API methods are available in the router:

`fetchMetricValues`:   Return the raw metric values for the time range for the requested
    metrics.

<!-- -->

`fetchEvents`:   Return the event information for the time range for the requested
    filters.

<!-- -->

`fetchThresholds`:   Fetch events matching the specified query and timeframe.

## Usage

There are older example scripts located in the ZenPack's bin directory.
It is suggested to interact with the Zenoss API via your HTTP API REST
client/library of choice.

### IdentificationRouter

**EndPoint:** `/zport/dmd/id_router`

**Headers:** `Content-Type: application/json`

`listResolvers`:   Method Parameters: None:   HTTP POST Body:
:

    ```sh
    {
       "action": "IdentificationRouter",
       "method": "listResolvers",
       "data": [],
       "tid": 1
    }
    ```

:   API Response:
:

    ```sh
    {
       "uuid": "07fc8148-e394-40b7-9c70-a201928ac5e7",
       "action": "IdentificationRouter",
       "result": {
          "resolvers": [
                "search",
                "global_catalog",
                "uid",
                "modeled",
                "component",
                "uuid"
          ],
          "success": true
       },
       "tid": 1,
       "type": "rpc",
       "method": "listResolvers"
    }
    ```

<!-- -->

`resolve`  - uid resolver:   Resolver 'id' Parameters: uid:
:   HTTP POST Body:
:

    ```sh
    {
       "action": "IdentificationRouter",
       "method": "resolve",
       "data": [
          {
                "id": {
                   "uid": "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev02.zenoss.lab"
                },
                "idScheme": "uid",
                "allowMultiple": true
          }
       ],
       "tid": 1
    }
    ```

:   API Response:
:

    ```sh
    {
       "uuid": "ce12820b-03fd-41a7-bb7f-1b7bb0351427",
       "action": "IdentificationRouter",
       "result": {
          "uids": [
                "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev02.zenoss.lab"
          ],
          "success": true
       },
       "tid": 1,
       "type": "rpc",
       "method": "resolve"
    }
    ```

<!-- -->

`resolve`  - uuid resolver:   Resolver 'id' Parameters: uuid:   HTTP POST Body:
:

    ```sh
    {
       "action": "IdentificationRouter",
       "method": "resolve",
       "data": [
          {
                "id": {
                   "uuid": "aceebacd-0cab-47ec-b52c-c7dac73fc601"
                },
                "idScheme": "uuid",
                "allowMultiple": true
          }
       ],
       "tid": 1
    }
    ```

:   API Response:
:

    ```sh
    {
       "uuid": "801f77cc-0a37-47a5-bf38-34836b599a09",
       "action": "IdentificationRouter",
       "result": {
          "uids": [
                "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev02.zenoss.lab"
          ],
          "success": true
       },
       "tid": 1,
       "type": "rpc",
       "method": "resolve"
    }
    ```

<!-- -->

`resolve`  - global_catalog resolver (using wildcard):   Resolver 'id' Parameters: monitor, id, name, collectors,
    searchKeywords, allowedRolesAndUsers, meta_type, path,
    objectImplements, ipAddress, productKeys, uid:   HTTP POST Body:
:

    ```sh
    {
       "action": "IdentificationRouter",
       "method": "resolve",
       "data": [
          {
                "id": {
                   "query": {
                      "meta_type": ["LinuxFileSystem"],
                      "uid": "/zport/dmd/Devices/Server/SSH/Linux/*/-"
                   }
                },
                "idScheme": "global_catalog",
                "allowMultiple": true
          }
       ],
       "tid": 1
    }
    ```

:   API Response:
:

    ```sh
    {
       "uuid": "b001aeef-3319-497f-a5f0-5d97fdcfc383",
       "action": "IdentificationRouter",
       "result": {
          "uids": [
                "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev02.zenoss.lab/os/filesystems/-",
                "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-stg.zenoss.lab/os/filesystems/-",
                "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev03/os/filesystems/-"
          ],
          "success": true
       },
       "tid": 1,
       "type": "rpc",
       "method": "resolve"
    }
    ```

<!-- -->

`resolve`  - search resolver:   Resolver 'id' Parameters: searchTerm, category:   HTTP POST Body:
:

    ```sh
    {
       "action": "IdentificationRouter",
       "method": "resolve",
       "data": [
          {
                "id": {
                   "searchTerm": "lab",
                   "category": "Device"
                },
                "idScheme": "search",
                "allowMultiple": true
          }
       ],
       "tid": 1
    }
    ```

:   API Response:
:

    ```sh
    {
       "uuid": "f1b915b5-a203-4578-82f2-5f420822d08e",
       "action": "IdentificationRouter",
       "result": {
          "uids": [
                "/zport/dmd/Devices/Groups/sma/devices/lab1",
                "/zport/dmd/Devices/Groups/sma/devices/lab2",
                "/zport/dmd/Devices/Groups/sma/devices/lab3",
                "/zport/dmd/Devices/Groups/sma/devices/lab4"
          ],
          "success": true
       },
       "tid": 1,
       "type": "rpc",
       "method": "resolve"
    }
    ```

<!-- -->

`resolve`  - device or component resolver:   Resolver 'id' Parameters: device, component:   HTTP POST Body:
:

    ```sh
    {
       "action": "IdentificationRouter",
       "method": "resolve",
       "data": [
          {
                "id": {
                   "device": "sma-dev02.zenoss.lab",
                   "component": "ens32"
                },
                "idScheme": "component",
                "allowMultiple": true
          }
       ],
       "tid": 1
    }
    ```

:   API Response:
:

    ```sh
    {
       "uuid": "3f7b555e-33f5-42b6-8f58-5b63c40d7d76",
       "action": "IdentificationRouter",
       "result": {
          "uids": [
                "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev02.zenoss.lab/os/interfaces/ens32"
          ],
          "success": true
       },
       "tid": 1,
       "type": "rpc",
       "method": "resolve"
    }
    ```

<!-- -->

`resolve`  - modeled resolver:   Resolver 'id' Parameters: modeledKeyword, modeledOperator,
    modeledValue:   HTTP POST Body:
:

    ```sh
    {
       "action": "IdentificationRouter",
       "method": "resolve",
       "data": [{
          "id": {
                "modeledKeyword": "_lastChange",
                "modeledOperator": ">",
                "modeledDateValue": "24h ago"
          },
          "idScheme": "modeled",
          "allowMultiple": true
       }],
       "tid": 1
    }
    ```

:   API Response:
:

    ```sh
    {
       "uuid": "8aece433-83f9-44e9-8769-8c7a224b5199",
       "action": "IdentificationRouter",
       "result": {
          "uids": [
                "/zport/dmd/Devices/Network/Cisco/Nexus/5000/devices/nexus-5k.zenoss.loc",
                "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev03"
          ],
          "success": true
       },
       "tid": 1,
       "type": "rpc",
       "method": "resolve"
    }
    ```

### PortalRouter

**EndPoint:** `/zport/dmd/portal_router`

**Headers:** `Content-Type: application/json`

fetchMetricValues:   Method Parameters: startTime, endTimem, specs (metricIds,
    returnProperties (optional), allowMultiple, echoInput):   HTTP POST Body:
:

    ```sh
    {
       "action": "PortalRouter",
       "method": "fetchMetricValues",
       "data": [
          {
                "startTime": "15m-ago",
                "endTime": "5m-ago",
                "specs": [
                   {
                      "id": {
                            "uid": "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev03"
                      },
                      "idScheme": "uid",
                      "allowMultiple": true,
                      "echoInput": false,
                      "metricIds": ["ssCpuIdlePerCpu", "MemFree", "laLoadInt1"]
                   }
                ]
          }
       ],
       "tid": 1
    }
    ```

:   API Response:
:

    ```sh
    {
       "uuid": "08922cae-c569-4243-96d0-8c2e126073bb",
       "action": "PortalRouter",
       "result": {
          "data": [
                {
                   "metrics": {
                      "ssCpuIdlePerCpu": {
                            "firstTime": 1654115846,
                            "lastTime": 1654116746,
                            "values": [
                               null,
                               76.34667205810547,
                               81.46843719482422
                            ],
                            "interval": 300
                      },
                      "MemFree": {
                            "firstTime": 1654115846,
                            "lastTime": 1654116746,
                            "values": [
                               null,
                               8019558400.0,
                               9436848128.0
                            ],
                            "interval": 300
                      },
                      "laLoadInt1": {
                            "firstTime": 1654115846,
                            "lastTime": 1654116746,
                            "values": [
                               null,
                               1.6699999570846558,
                               2.5
                            ],
                            "interval": 300
                      }
                   },
                   "input": {
                      "allowMultiple": true,
                      "metricIds": [
                            "ssCpuIdlePerCpu",
                            "MemFree",
                            "laLoadInt1"
                      ],
                      "echoInput": false,
                      "id": {
                            "uid": "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev03"
                      },
                      "idScheme": "uid"
                   },
                   "uuid": "d1fa058c-03d7-4c78-b1fa-088b2898c016",
                   "success": true,
                   "properties": {}
                }
          ],
          "success": true
       },
       "tid": 1,
       "type": "rpc",
       "method": "fetchMetricValues"
    }
    ```

<!-- -->

fetchEvents:   Method Parameters: startTime, endTime, specs (criteria (optional),
    maxEvents (optional), allowMultiple, echoInput):   HTTP POST Body:
:

    ```sh
    {
       "action": "PortalRouter",
       "method": "fetchEvents",
       "data": [{
          "startTime": "6h-ago",
          "specs": [{
                "idScheme": "uid",
                "id": {
                   "uid": "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev03"},
                "criteria": {
                   "event_class": "/Status/OSProcess",
                   "status": 1
                }
          }]
       }],
       "tid": 1
    }
    ```

:   API Response:
:

    ```sh
    {
       "uuid": "cefe3b09-f7ab-45e2-ab39-a5f537cc28eb",
       "action": "PortalRouter",
       "result": {
          "data": [
                {
                   "input": {
                      "id": {
                            "uid": "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev03"
                      },
                      "idScheme": "uid",
                      "criteria": {
                            "status": 1,
                            "element_title": "sma-dev03",
                            "event_class": "/Status/OSProcess"
                      }
                   },
                   "uuid": "d1fa058c-03d7-4c78-b1fa-088b2898c016",
                   "success": true,
                   "events": [
                      {
                            "prodState": "Production",
                            "firstTime": 1647618686,
                            "evid": "0242ac11-001a-9044-11ec-a6d34723ede6",
                            "device_uuid": "d1fa058c-03d7-4c78-b1fa-088b2898c016",
                            "eventClassKey": null,
                            "component": "zport_dmd_Processes_Zenoss_osProcessClasses_zenmodeler_e30c534a85f0e417b34ca6a4a272de61",
                            "DeviceClass": [
                               {
                                  "uid": "/zport/dmd/Devices/Server/SSH/Linux",
                                  "name": "/Server/SSH/Linux"
                               }
                            ],
                            "agent": "zencommand",
                            "clearid": null,
                            "dedupid": "sma-dev03|zport_dmd_Processes_Zenoss_osProcessClasses_zenmodeler_e30c534a85f0e417b34ca6a4a272de61|/Status/OSProcess|zport_dmd_Processes_Zenoss_osProcessClasses_zenmodeler_e30c534a85f0e417b34ca6a4a272de61|4",
                            "owner": "zenoss",
                            "Location": [],
                            "eventGroup": "Process",
                            "ntevid": null,
                            "component_url": null,
                            "device": "sma-dev03",
                            "stateChange": 1647618907,
                            "eventClass": "/Status/OSProcess",
                            "Systems": [],
                            "component_title": "",
                            "monitor": "localhost",
                            "count": 112,
                            "device_title": "sma-dev03",
                            "DevicePriority": "Normal",
                            "severity": 4,
                            "message": "Process set contains 0 running processes: /opt/zenoss/bin/python /opt/zenoss/Products/DataCollector/zenmodeler.py --configfile /opt/zenoss/etc/zenmodeler.conf --now -d sma-dev03 --monitor localhost --collect=\n   Using regex '.*zenmodeler.py.*' \n   All Processes have stopped since the last model occurred. Last Modification time (2022/03/18 15:50:01)",
                            "facility": null,
                            "eventClass_url": "/zport/dmd/Events/Status/OSProcess",
                            "DeviceGroups": [],
                            "summary": "Process set contains 0 running processes: /opt/zenoss/bin/python /opt/zenoss/Products/DataCollector/zenmodeler.py --configfile /opt/zenoss/etc/zenmodeler.conf --now -d sma-dev03 --monitor localhost --collect=",
                            "priority": null,
                            "eventKey": "zport_dmd_Processes_Zenoss_osProcessClasses_zenmodeler_e30c534a85f0e417b34ca6a4a272de61",
                            "details": [
                               {
                                  "value": "cedc2cc0f45d",
                                  "key": "manager"
                               },
                               {
                                  "value": "/Server/SSH/Linux",
                                  "key": "zenoss.device.device_class"
                               },
                               {
                                  "value": "10.88.111.222",
                                  "key": "zenoss.device.ip_address"
                               },
                               {
                                  "value": "3",
                                  "key": "zenoss.device.priority"
                               },
                               {
                                  "value": "1000",
                                  "key": "zenoss.device.production_state"
                               }
                            ],
                            "lastTime": 1647651986,
                            "ipAddress": [
                               "10.88.111.222"
                            ],
                            "eventState": "Acknowledged"
                      }
                   ]
                }
          ],
          "success": true
       },
       "tid": 1,
       "type": "rpc",
       "method": "fetchEvents"
    }
    ```

<!-- -->

fetchThresholds:   Method Parameters: startTime, endTime, specs, metricIds (optional),
    allowMultiple, echoInput:   HTTP POST Body:
:

    ```sh
    {
       "action": "PortalRouter",
       "method": "fetchThresholds",
       "data": [{
          "startTime": "6h-ago",
          "specs": [{
                "idScheme": "uid",
                "id": {
                   "uid": "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev03"},
                "metricIds":[
                   "cpu_ssCpuIdlePerCpu"
                ]
          }]
       }],
       "tid": 1
    }
    ```

:   API Response:
:

    ```sh
    {
       "uuid": "1d83221a-7cb7-49d5-9996-9d7d4773fdbc",
       "action": "PortalRouter",
       "result": {
          "data": [
                {
                   "metrics": {
                      "cpu_ssCpuIdlePerCpu95%": 82.57357597351074,
                      "cpu_ssCpuIdlePerCpuMAX": 82.70233917236328,
                      "cpu_ssCpuIdlePerCpuAVG": 80.57150745391846
                   },
                   "input": {
                      "metricIds": [
                            "cpu_ssCpuIdlePerCpu"
                      ],
                      "id": {
                            "uid": "/zport/dmd/Devices/Server/SSH/Linux/devices/sma-dev03"
                      },
                      "idScheme": "uid"
                   },
                   "uuid": "d1fa058c-03d7-4c78-b1fa-088b2898c016",
                   "success": true,
                   "events": [
                      {
                            "prodState": "Production",
                            "firstTime": 1654266574,
                            "evid": "0242ac11-0021-81e0-11ec-e34997d55116",
                            "device_uuid": "d1fa058c-03d7-4c78-b1fa-088b2898c016",
                            "eventClassKey": null,
                            "component": null,
                            "DeviceClass": [
                               {
                                  "uid": "/zport/dmd/Devices/Server/SSH/Linux",
                                  "name": "/Server/SSH/Linux"
                               }
                            ],
                            "agent": "zencommand",
                            "clearid": null,
                            "dedupid": "sma-dev03||/Perf/CPU|cpu|cpu_ssCpuIdlePerCpu|cpuTooBusy|5",
                            "owner": null,
                            "Location": [],
                            "eventGroup": null,
                            "ntevid": null,
                            "component_url": null,
                            "device": "sma-dev03",
                            "stateChange": 1654266574,
                            "eventClass": "/Perf/CPU",
                            "Systems": [],
                            "component_title": "",
                            "monitor": "localhost",
                            "count": 1,
                            "device_title": "sma-dev03",
                            "DevicePriority": "Normal",
                            "severity": 5,
                            "message": "threshold of cpuTooBusy exceeded: current value 81.453333",
                            "facility": null,
                            "eventClass_url": "/zport/dmd/Events/Perf/CPU",
                            "DeviceGroups": [],
                            "summary": "threshold of cpuTooBusy exceeded: current value 81.453333",
                            "priority": null,
                            "eventKey": "cpu|cpu_ssCpuIdlePerCpu|cpuTooBusy",
                            "details": [
                               {
                                  "value": "81.4533333333",
                                  "key": "current"
                               },
                               {
                                  "value": "exceeded",
                                  "key": "how"
                               },
                               {
                                  "value": "d33cd33ae9ab",
                                  "key": "manager"
                               },
                               {
                                  "value": "5",
                                  "key": "max"
                               },
                               {
                                  "value": "/Server/SSH/Linux",
                                  "key": "zenoss.device.device_class"
                               },
                               {
                                  "value": "10.88.111.222",
                                  "key": "zenoss.device.ip_address"
                               },
                               {
                                  "value": "3",
                                  "key": "zenoss.device.priority"
                               },
                               {
                                  "value": "1000",
                                  "key": "zenoss.device.production_state"
                               }
                            ],
                            "lastTime": 1654266574,
                            "ipAddress": [
                               "10.88.111.222"
                            ],
                            "eventState": "New"
                      }
                   ]
                }
          ],
          "success": true
       },
       "tid": 1,
       "type": "rpc",
       "method": "fetchThresholds"
    }
    ```

## Attachments:

-   [zenpack-general.png](img/zenpack-zenpack-general.png)
-   [zenpack-general.png](img/zenpack-zenpack-general.png)


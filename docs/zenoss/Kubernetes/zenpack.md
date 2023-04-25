# Kubernetes

@lb[](img/zenpack-kubernetes-logo-zp.png)

## Commercial

This ZenPack is developed and supported by Zenoss Inc. Commercial
ZenPacks are available to Zenoss commercial customers only. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks. [Click here](https://zenoss.com/product/zenpacks?f%5B0%5D=im_field_zenpack_category:1046){.external-link} to
view all available Zenoss Commercial ZenPacks.

### Authors:

[Zenoss](https://www.zenoss.com){.external-link}

### Organization:

[Zenoss](https://www.zenoss.com){.external-link}

### License:

Commercial

### Name:

ZenPacks.zenoss.Kubernetes

### Applications Monitored:

Kubernetes

## Kubernetes ZenPack

This ZenPack provides system monitoring of Kubernetes (K8s) clusters.

@lb[](img/zenpack-header.png)

## Support

This ZenPack is included with commercial versions of Zenoss and
enterprise support for this ZenPack is provided to Zenoss customers with
an active subscription.

## Releases

Version 1.2.0-[Download](https://delivery.zenoss.com){.external-link}:   Released on December 6, 2021:   Requires [PythonCollector ZenPack](http://zenoss.com/product/zenpacks/pythoncollector){.external-link}, [ZenPackLib ZenPack](http://zenoss.com/product/zenpacks/zenpacklib){.external-link}:   Compatible with Zenoss Resource Manager 6.2 and Zenoss Cloud

Version 1.1.0-[Download](https://delivery.zenoss.com){.external-link}:   Released on January 13, 2020:   Requires [PythonCollector ZenPack](http://zenoss.com/product/zenpacks/pythoncollector){.external-link},
    [ZenPackLib ZenPack](http://zenoss.com/product/zenpacks/zenpacklib){.external-link}:   Compatible with Zenoss Resource Manager 6.2 and Zenoss Cloud

## Contents

-   [Background](#background)
    -   [Support Requirements](#support-requirements)
    -   [Gallery](#gallery)
-   [Features](#features)
    -   [Upgrade Notes](#upgrade-notes)
    -   [Kubernetes Structure and Discovery](#kubernetes-structure-and-discovery)
    -   [Dashboard Portlets](#dashboard-portlets)
-   [Usage](#usage)
    -   [RBAC Authentication](#rbac-authentication)
    -   [Kubernetes Batch Configuration](#kubernetes-batch-configuration)
    -   [Adding a Custom Datasource to Metrics](#adding-a-custom-datasource-to-metrics)
-   [Installed Items](#installed-items)
    -   [Configuration and zProperties](#configuration-and-zproperties)
    -   [Device Modeling Configuration](#device-modeling-configuration)
    -   [Common values for filter zProperties](#common-values-for-filter-zproperties)
    -   [Modeler Plugins](#modeler-plugins)
-   [Service Impact and Root Cause Analysis](#service-impact-and-root-cause-analysis)
    -   [Impact Relationships between Kubernetes Components](#impact-relationships-between-kubernetes-components)
-   [Appendix: Kubernetes RBAC Setup](#Kubernetes-Appendix%3AKubernetesRBACSetup)
-   [Appendix: Identifying Master Nodes](#Kubernetes-Appendix%3AIdentifyingMasterNodes)
-   [Appendix: AWS EKS nodes](#Kubernetes-Appendix%3AAWSEKSnodes)
-   [Appendix: AKS, Azure nodes](#Kubernetes-Appendix%3AAKS%2CAzurenodes)
-   [Changes](#changes)
    -   [1.2.0](#120)
    -   [1.1.0](#110)
    -   [1.0.1](#101)
    -   [1.0.0](#100)

## Background

This ZenPack monitors Kubernetes (K8s) clusters deployed on Google Cloud
Platform (GKE), Amazon Web Services (EKS), Microsoft Azure (AKS),as well
as on locally-hosted environments. It uses RBAC authentication to access
all data related to modeling and monitoring.

### Support Requirements

Zenoss:

-   Zenoss 6.2+
-   ZenPackLib ZenPack 2.1.0+

Kubernetes:

-   Kubernetes versions 1.9.X - 1.21.X
-   Kubernetes versions 1.17.X - 1.21.X deployed on Google Cloud
    Platform, GKE
-   Kubernetes versions 1.18.X - 1.21.X deployed on Amazon Web Services,
    EKS
-   Kubernetes versions 1.20.X - 1.22.X deployed on Microsoft Azure, AKS
-   Kubernetes versions 1.16.X - 1.21.X deployed on Local environment

### Gallery

@lb[](img/zenpack-k8soverview.png){.confluence-embedded-image width="1200"}

@lb[](img/zenpack-k8scontainers.png){.confluence-embedded-image width="1200"}

@lb[](img/zenpack-k8sdependencyview.png){.confluence-embedded-image width="1200"}

@lb[](img/zenpack-k8sdynamicview.png){.confluence-embedded-image width="1200"} @lb[](img/zenpack-k8smodel.png)
@lb[](img/zenpack-k8smodeldiagram.png) @lb[](img/zenpack-k8simpact.png){.confluence-embedded-image width="1200"} @lb[](img/zenpack-k8simpactdiagram.png) @lb[](img/zenpack-k8snamespaces.png){.confluence-embedded-image width="1200"} @lb[](img/zenpack-k8snodes.png){.confluence-embedded-image width="1200"} @lb[](img/zenpack-k8spersistentvolumes.png){.confluence-embedded-image width="1200"} @lb[](img/zenpack-k8sservices.png){.confluence-embedded-image width="1200"} @lb[](img/zenpack-k8sservices.png){.confluence-embedded-image width="1200"} @lb[](img/zenpack-k8sstatefulsets.png){.confluence-embedded-image width="1200"}

@lb[](img/zenpack-k8scomponentgraphs_containers.png){.confluence-embedded-image width="1200"} @lb[](img/zenpack-k8scomponentgraphs_deployments.png){.confluence-embedded-image width="1200"} @lb[](img/zenpack-k8scomponentgraphs_pods.png){.confluence-embedded-image width="1200"} @lb[](img/zenpack-k8scomponentgraphs_statefulsets.png){.confluence-embedded-image width="1200"}

@lb[](img/zenpack-k8sportlets.png)

## Features

ZenPack features include:

-   Overall Cluster Health Monitoring
-   Health Monitoring for Nodes, Services, Pods
-   Graphs for Kubernetes Cluster, Nodes, Deployments, StatefulSets,
    Pods, Containers
-   Dashboard Portlets for Pod CPU and Memory consumption
-   Service Impact and root cause analysis
-   Event Management

### Upgrade Notes

#### Version 1.2.0

When updating to version 1.2.0 monitoring of a new component StatefulSet
was added. Similar to Services, Deployments, Pods, and Containers,
StatefulSets can be selected for modeling using
zKubernetesNamespaceFilter. In addition, a new zProperty called
zKubernetesPodFilter was added to select Pods and Containers for
modeling.

Please note that the generation of identifiers for Pods and Containers
has been changed due to the improvements, therefore, after updating to
version 1.2.0, the old monitoring data for Pods and Containers,
collected before the update, will no longer be displayed on the
component graphs.

#### Version 1.1.0

When updating to version 1.1.0 or later (from versions prior to 1.1.0),
a new zProperty was added, zKubernetesNamespaceFilter, to filter
Deployments, Services, Pods, and Containers based upon the namespace to
which they belong. These four components link together, hence they all
rely on the same zProperty. Further, the default behavior for most
Kubernetes consoles hid components under the 'kube-system' namespace
while displaying everything else. This behavior has been adopted by the
1.1.0 Kubernetes ZenPack; the zProerties zKubernetesNamespaceFilter and
zKubernetesContainerNamesModeled may be updated during the upgrade
process to reflect the new default behavior.

If the zKubernetesContainerNamesModeled was changed from the default
value then the new value will not be updated, even if the value is
'kube-system/.\*/.\*'. In this situation, the property
zKubernetesNamespaceFilter will have to be updated to allow
'kube-system'.

Service Impact relations may become out of sync when upgrading to 1.1.0.
This issue should only affect instances where Service Impact is running.
Service Impact can be manually corrected (after installation is
complete) by running this command:

`zenimpactgraph run --update`

### Kubernetes Structure and Discovery

Objects are automatically discovered via the Kubernetes API. The ZenPack
class structure can be visualized in the diagram on the right:

@lb[](img/zenpack-k8smodel.png)

The Kubernetes model will be automatically updated as changes are
detected on the cluster. New and deleted Services, Deployments,
StatefulSets, Pods, and Clusters will be updated as part of the regular
monitoring cycle. Changes detected to Namespaces, Nodes, and
PersistentVolumes will also be automatically updated. Because
incremental modeling is conjoined with the Zenoss monitoring cycle,
(default 5 minutes cycles,) it may take several minutes before the
Zenoss Kubernetes model synchronizes with the Kubernetes Cluster.

Incremental modeling makes use of the Kubernetes Watch API to monitor
for changes to K8s clusters by tracking the resourceVersion for each API
endpoint. When a zenpython instance starts, the resourceVersion is set
to '0' and the first monitoring cycle will jump the resourceVersion to
the latest version. Occasionally, the resourceVersion may become 'Gone'
(indicating that the resourceVersion is too old and no longer in the K8s
history). In this situation, the resourceVersion is set back to '0' so
it can again jump forward to the latest version. Due to these factors,
it may take two cycles to fully synchronize the K8s model.

The following Kubernetes zProperties also affect incremental modeling:

-   zKubernetesContainerNamesModeled
-   zKubernetesContainerLabelsModeled
-   zKubernetesNamespaceFilter
-   ZKubernetesPodFilter

Changes to these properties may not be pick-up and applied until the
next modeling cycle.

@lb[](img/zenpack-k8smodeldiagram.png)

#### Device (Cluster)

-   Description: The device represents a single Kubernetes cluster.
-   Attributes:
    -   buildDate
    -   cluster_ip
    -   cpu_capacity
    -   cpu_usage
    -   gcp_cluster
    -   memory_capacity
    -   memory_usage
    -   platform
    -   version
-   Relationships:
    -   k8sNamespace
    -   k8sNode
    -   k8sPersistentVolume
-   Datasource/Datapoints:
    -   event
    -   metrics
        -   cpu
        -   memory
-   Graphs:
    -   CPU Utilization
    -   Memory Utilization
-   Capacity Thresholds:
    -   CPU Capacity
    -   Memory Capacity

#### Namespace

-   Description: Namespaces for Kubernetes.
-   Attributes:
    -   container_count
    -   namespace_uid
    -   status
-   Relationships:
    -   k8sService
    -   k8sPod
    -   k8sDeployments
    -   k8sStatefulSet

#### Node

-   Description: Compute nodes that Kubernetes is build from.
-   Attributes:
    -   architecture
    -   cpu_allocatable
    -   cpu_capacity
    -   cpu_usage
    -   ephemeral_storage_allocatable
    -   ephemeral_storage_capacity
    -   externalIP
    -   guest_device
    -   internalIP
    -   kubeletVersion
    -   manageIP
    -   memory_allocatable
    -   memory_capacity
    -   memory_usage
    -   modeled_cpu_allocatable
    -   modeled_cpu_capacity
    -   modeled_memory_allocatable
    -   modeled_memory_capacity
    -   node_hostname
    -   node_type
    -   node_uid
    -   operatingSystem
    -   pods_allocatable
    -   pods_capacity
    -   region
    -   status
-   Relationships:
    -   k8sCluster
    -   k8sPod
-   Datasource/Datapoints:
    -   status
        -   status
    -   metrics
        -   cpu
        -   memory
    -   allocatable
        -   cpu
        -   memory
    -   capacity
        -   cpu
        -   memory
-   Graphs:
    -   CPU Utilization
    -   Memory Utilization
-   Thresholds:
    -   High Memory (default: disabled)
    -   High CPU Load (default: disabled)

#### Persistent Volume

-   Description: Storage volume abstraction.
-   Attributes:
    -   capacity
    -   pvc_uid
    -   status
    -   storageClassName
-   Relationships:
    -   k8sNamespace
-   Datasource/Datapoints:
    -   status:
        -   status

#### Service

-   Description: Kubernetes Services represent virtual services that are
    realized by Pods and Containers.
-   Attributes:
    -   cluster_ip
    -   container_count
    -   port_list
    -   selector
    -   service_type
    -   service_uid
-   Relationships:
    -   k8sNamespace
    -   k8sPods

#### Deployments

-   Description: Kubernetes Deployments control automation for Pods and
    Containers.
-   Attributes:
    -   labels
    -   created
-   Relationships:
    -   k8sNamespace
    -   k8sPods
-   Datasource/Datapoints:
    -   replicas
    -   availableReplicas
    -   readyReplicas
    -   unavailableReplicas
    -   updatedReplicas
    -   collisionCount
-   Graphs:
    -   Replica Set
    -   Collision Count
-   Thresholds:
    -   Replica Count

#### StatefulSet

-   Description: StatefulSet controller for Kubernetes.
-   Attributes:
    -   labels
    -   created
-   Relationships:
    -   k8sPod
    -   k8sNamespace
-   Datasource/Datapoints:
    -   replicas
    -   currentReplicas
    -   readyReplicas
    -   updatedReplicas
    -   collisionCount
-   Graphs:
    -   Replica Set
    -   Collision Count
-   Thresholds:
    -   Replica Count

#### Pod

-   Description: A group of one or more containers with shared
    storage/network, and a specification for how to run the containers.
-   Attributes:
    -   labels
    -   pod_uid
    -   status
-   Relationships:
    -   k8sNamespace
    -   k8sNode
    -   k8sContainer
    -   k8sDeployments
    -   k8sStatefulSet
-   Datasource/Datapoints:
    -   metrics:
        -   cpu
        -   memory
    -   status:
        -   status
-   Graphs:
    -   CPU Usage
    -   Memory Usage

#### Container

-   Description: Lowest compute abstraction element for Pods.
-   Attributes:
    -   cpu_limits
    -   cpu_requests
    -   image
    -   labels
    -   memory_limits
    -   memory_requests
-   Relationships:
    -   k8sPod
-   Datasource/Datapoints:
    -   metrics:
        -   cpu
        -   memory
-   Graphs:
    -   CPU Usage
    -   Memory Usage
    -   **Note:** *It is common for some containers to have only partial
        data for cpu/memory so it is natural that some of those graphs
        will be missing data.*
-   Thresholds:
    -   High CPU Load
    -   High Memory

### Dashboard Portlets

This ZenPack adds portlets that provide at-a-glance views into Pod and
Cluster memory and CPU utilization. Portlets are viewed on the first
page upon login, and can be added or removed using the dashboard and
portlet controls.

@lb[](img/zenpack-k8sportlets.png)

#### Kubernetes Portlets

The following are portlets specific to Kubernetes:

-   Top K8s Pods by Memory
-   Top K8s Pods CPU

These two portlets can be filtered by:

-   Cluster
-   Namespace
-   Service

#### Platform Portlets

In addition to Memory and CPU, the following platform portlets support
Kubernetes events and issues:

-   Device Issues
-   Event View
-   Open Events
-   Open Events Chart

## Usage

### RBAC Authentication

You must expose the Kubernetes V2 and metrics.k8s.io APIs on your
system. We exclusively use Role-based access control (RBAC) for cluster
API access. For more information see [Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/){.external-link}.

You generally must do at least the following steps for both GCP and
locally installed Kubernetes systems:

1.  Set `MY_PREFIX` and capture `ACCOUNT_ID` and `API_SERVER`:

        MY_PREFIX=zenoss API_SERVER=$(kubectl cluster-info | head -1 | cut -d' ' -f6 | sed 's/\x1b\[[0-9;]*m//g')

    A. If using GKE deployed on the Google Cloud Platform, first ensure
    you are connected to the correct project associated with your
    cluster. Now find your `ACCOUNT_ID`:
    `ACCOUNT_ID=$(gcloud info --format='value(config.account)')`
    B. If using EKS deployed on the Amazon Web Services, first ensure
    you are connected to the correct project associated with your
    cluster. Now find your `ACCOUNT_ID`:

      `ACCOUNT_ID=$(aws sts get-caller-identity --output text --query 'Account')` C.
    If using AKS deployed on the Microsoft Azure, first ensure you are
    connected to the correct project associated with your cluster. Now
    find your `ACCOUNT_ID`:
            `ACCOUNT_ID=$(az account show --query id --output tsv)`
    D. If using locally-hosted Kubernetes, determine the `ACCOUNT_ID`
    and prepare the credentials as per [Kubernetes Getting started](https://kubernetes.io/docs/setup/){.external-link}.
    E. Alternative, setup [tutorials for Kubernetes Scratch](https://www.google.com/search?q=kubernetes+scratch+setup){.external-link} can
    be found via an internet search.

2.  Setup RBAC Authorization:

        kubectl create clusterrolebinding $MY_PREFIX-cluster-admin-binding --clusterrole=cluster-admin --user=$ACCOUNT_ID

3.  Grab the YAML from Appendix: Kubernetes RBAC Setup and save it to
    the file `zenoss_rbac.yaml` and use it to create the SA for the
    role:

        kubectl apply -f zenoss_rbac.yaml

4.  Get the secret Token and save it (adjusting `zenoss-secret` if
    required):

        TOKEN=$(kubectl describe secret zenoss-secret | sed -n '/^token/p' | cut -d' ' -f7) echo $TOKEN

5.  `$TOKEN` will be set to the zKubernetesClusterToken in the token
    section

6.  From the *Infrastructure Add* pull-down select **Add Kubernetes
    Cluster**

7.  Fill in the following fields:

    -   Device Name
    -   IP of K8s API ($API_SERVER from above)
    -   TCP Port of API
    -   Service Account
    -   Token for Service Account ($TOKEN from above)

8.  Select the correct Collector for your system

9.  Hit the **Add** button

### Kubernetes Batch Configuration

If you use Zenoss Service Dynamics, you can also add your devices in
batch for convenience and automation.

-   Attach to the Zope container:

         serviced service attach zope

-   Create a text file (filename: `/tmp/batch.txt`) and replace
    **`$TOKEN`** with your token from above:

         /Devices/Kubernetes kubernets101 zKubernetesClusterIP='10.20.30.40', \ zKubernetesPort="443", \ zKubernetesServiceAccount='zenoss', \ zKubernetesClusterToken='$TOKEN'

-   Now run the `zenbatchload` command:

         zenbatchload /tmp/batch.txt

-   The device should now load and model automatically

### Adding a Custom Datasource to Metrics

In order to add a metrics datasource, you must be familiar with the API
target you wish to call and the resulting JSON data response.

The metrics datasource provided requires three configuration parameters,
which we describe below:

1.  **api_target**: The API target that gets appended to the metrics
    base API URL
2.  **data_path**: The path through the returned JSON that identifies
    the metric
3.  **aggregator**: Method to aggregate values returned by apt_target
    and data_path.

Together, the `api_target` and `data_path` provide the complete
information for the datasource to acquire the requested data.
The `aggregator` provides the method to put that data together to form a
single data value.

#### api_target

The api_target must be a valid path for the API. It must be in a plain
REST GET format.

    <string1>/<string2>/<string3>

where each `<string*>` must be a valid string defined in the API.
Examples:

    api/v1/nodes api/v1/pods apis/metrics.k8s.io/v1beta1/nodes apis/metrics.k8s.io/v1beta1/pods

These examples supply the entire API path beyond the base URL, and are
required. More information can be found in [Resource metrics pipeline](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-metrics-pipeline/){.external-link}.

#### data_path

The *data_path* string represents a path through the returned JSON data
that loosely follows the
[jq](https://stedolan.github.io/jq/){.external-link} style format which
separates path elements (dictionary keys) by dots.
It can include the following items:

-   Plain *jq* strings. For example: `a.b`

-   Strings with square brackets with a *jq*-style identifier:

        items[metadata.name]

    This example will scan all list elements in *items* and select the
    *meta.name* element from those items.
    To clarify, this will match all `items` that have the JSON key
    `metadata` with sub-key `name`.
    Note that this element is not useful on its own unless
    `items[metadata.name]` filters `items` and selects out only those
    which have `metadata.name` structure.

-   Strings with square brackets with a value-qualified *jq*-styled
    identifier. This allows you to filter list items that match a
    dictionary key or value.
    Examples:

        items[metadata.name=server7] items[metadata.name=server7].usage items[metadata.name=${here/title}].usage items[metadata.name=${here/title}].status.capacity

    Note that the last two examples show that you can use dynamic TALES
    expressions instead of static strings to filter the `items` elements
    by value.
    Also note that the last three examples specify the path to the
    metric that matches the `item` list elements in square brackets.

#### aggregator

The required aggregator is selected from the drop-down. Choose from:

-   **AVERAGE**: Average all elements
-   **FIRST**: Choose the first element only
-   **MAX**: Select the maximum value
-   **MIN**: Select the minimum value
-   **PERCENT_AVERAGE**: Return average of the data multiplied by 100
-   **PERCENT_SUM**: Return sum of the data multiplied by 100
-   **SUM_OR_ZERO**: Sum the data, return zero if no data exists
-   **SUM**: Sum all the data

## Installed Items

Installing this ZenPack will add the following items to your Zenoss
system:

### Configuration and zProperties

The zProperties and default settings are as follows:

-   **zKubernetesClusterIP**: The IP address of the Kubernetes Cluster
    API.
-   **zKubernetesClusterName**: Name of cluster used for association
    with related resources.
-   **zKubernetesPort**: The TCP port of the API.
    -   Default value: **443**
-   **zKubernetesServiceAccount**: The Kubernetes *service account*
    associated with the API account. See
    **`kubectl get serviceaccounts`** for more information.
-   **zKubernetesClusterToken**: The token associated with
    `zKubernetesServiceAccount`. See **`kubectl describe secrets`** for
    more information.
-   **zKubernetesGuestUseExternalIP**: Boolean to set the `manageIp` to
    the external IP for host monitoring. This property should be set to
    False If guest device of EC2 account is modeled by an internal IP in
    order to have links to Kubernetes Guest devices.
    -   Default value: **True**
-   **zKubernetesEventInterval**: Polling interval for events.
    -   Default value: **60**
-   **zKubernetesMonitoringInterval**: Polling interval for metrics
    collection.
    -   Default value: **300**
-   **zKubernetesStatusInterval**: Polling interval for status updates.
    -   Default value: **300**
-   **zKubernetesContainerNamesModeled**: RegEx Pattern of Container
    names to model. Note that only Containers which are members of Pods
    that match the `zKubernetesNamespaceFilter` and
    `zKubernetesPodFilter` patterns may be captured. Containers that
    belong to Pods that are not modeled will also not be modeled. If
    kept blank, then no containers which satisfy
    `zKubernetesContainerNamesModeled` pattern will be modeled.
    -   Format: **regex**
    -   Default value: **`[".*"]`**
-   **zKubernetesContainerLabelsModeled**: Container labels to model. If
    both `zKubernetesContainerLabelsModeled` and
    `zKubernetesContainerNamesModeled` are set, then all containers that
    match at least one property will be listed, (i.e. Venn diagram
    union).
    -   Format: **key: value**
    -   Default value: `[""]`
-   **zKubernetesPodFilter:** Pattern for Pods to model and monitor.
    This affects the modeling and monitoring of Pods and Containers
    related to them. By default, all Pods and Containers are allowed to
    be modeled and monitored. If left blank, then no components will not
    be modeled.
    -   Format: **regex**
    -   Default value: `[".*"]`
-   **zKubernetesNamespaceFilter**: Pattern for namespaces to model and
    monitor. This affects the modeling and monitoring of Services,
    Deployments, StatefulSets, Pods and Containers. By default, only
    non-system (components not in namespace 'kube-system') will be
    watched. If left blank, then no components will not be modeled.
    -   Format: **regex**
    -   Default value: `["^((?!kube-system).)*$"]`

### Device Modeling Configuration

Some zProperties, noted above, can affect the application of other
properties during modeling of a device, i.e.:

-   **zKubernetesNamespaceFilter** can affect:
    -   zKubernetesPodFilter
    -   zKubernetesContainerNamesModeled
    -   zKubernetesContainerLabelsModeled
-   **zKubernetesPodFilter** can affect:
    -   zKubernetesContainerNamesModeled
    -   zKubernetesContainerLabelsModeled
-   **zKubernetesContainerNamesModeled** can affect:
    -   zKubernetesContainerLabelsModeled
-   **zKubernetesContainerLabelsModeled** can affect:
    -   zKubernetesContainerNamesModeled

To configure the modeling of Kubernetes Cluster components use the
following combination of zProperties:

1.  **zKubernetesNamespaceFilter**: All Deployments, StatefulSets, and
    Services, which belong to Namespaces, that are not specified by
    \`zKubernetesNamespaceFilter\` pattern will not be modeled. All Pods
    and Containers that belong to Namespaces, which are not specified by
    \`zKubernetesNamespaceFilter\` pattern will not be modeled even if
    they are specified by \`zKubernetesPodFilter\`,
    \`zKubernetesContainerNamesModeled\`, and
    \`zKubernetesContainerLabelsModeled\`.

2.  **zKubernetesPodFilter**: All Pods which belong to Namespaces
    specified by `zKubernetesNamespaceFilter` pattern and are not
    specified by `zKubernetesPodFilter` will not be modeled. Containers
    related to Pods allowed to model by `zKubernetesNamespaceFilter`
    will not be modeled if these Pods are not allowed to model by
    `zKubernetesPodFilter` even if the corresponding Containers are
    specified by `zKubernetesContainerNamesModeled` and
    `zKubernetesContainerLabelsModeled`.

3.  **zKubernetesContainerNamesModeled**: All Containers allowed for
    modeling by `zKubernetesNamespaceFilter` and `zKubernetesPodFilter`
    will not be modeled if they are not allowed by
    `zKubernetesContainerNamesModeled`, however, if they are allowed by
    `zKubernetesContainerLabelsModeled` they will be modeled.

4.  **zKubernetesContainerLabelsModeled**: All Containers allowed for
    modeling by `zKubernetesNamespaceFilter` and `zKubernetesPodFilter`
    will not be modeled if they are not allowed by
    `zKubernetesContainerLabelsModeled`, however, if they are allowed by
    `zKubernetesContainerNamesModeled` they will be modeled.

5.  **zKubernetesContainerNamesModeled +
    zKubernetesContainerLabelsModeled**: All Containers allowed for
    modeling by `zKubernetesNamespaceFilter` and `zKubernetesPodFilter`
    will be modeled if they are allowed by
    `zKubernetesContainerLabelsModeled` and
    `zKubernetesContainerNamesModeled`. This option provides an
    opportunity to mix approaches for the selection of Containers, which
    should be modeled, using their names and labels.

### Common values for filter zProperties

Common values for `zKubernetesNamespaceFilter`, `zKubernetesPodFilter`,
and `zKubernetesContainerNamesModeled`:

-   `[""]` - no components will be selected for the modeling.
-   `[".*"]` - all available components will be selected for the
    modeling.
-   `["default|test"]` - all components related to `default` and `test`
    will be selected for the modeling.
-   `["^((?!pod-1).)*$"]` - all containers which do not relate to
    `pod-1` will be selected for the modeling.

Common values for `zKubernetesContainerLabelsModeled`:

-   `[""]` - no components will be selected for the modeling.
-   `["app: mysql|app: redis"]` - containers which have a label `mysql`
    or `redis` will be selected for the modeling.

### Modeler Plugins

-   Kubernetes.Cluster

## Service Impact and Root Cause Analysis

@lb[](img/zenpack-k8simpactdiagram.png)

When combined with the Zenoss Service Dynamics product, this ZenPack
adds built-in service impact and root cause analysis capabilities. The
service impact relationships shown in the diagram (right) and described
below are automatically added and maintained. These will be included in
any services that contain one or more of the explicitly mentioned
components.

The following objects types would typically be added to Impact services.

-   Kubernetes Containers
-   Linux device associated with a Kubernetes Node

### Impact Relationships between Kubernetes Components

@lb[](img/zenpack-k8simpact.png)

-   GuestCluster (external): impacts Cluster
-   GuestDevice (external): impacts Node
-   Cluster: impacts Node, Persistent Volume
-   Node: impacts Container
-   Container: impacts Pod
-   PersistentVolume: impacts Pod
-   Pod: impacts Deployment, StatefulSet, Service
-   Deployment: impacts Service
-   StatefulSet: impacts Service

## Appendix: Kubernetes RBAC Setup

In order to properly enable the Core Metrics Service and provide RBAC
access permissions to other components, the following YAML must be
applied to the account in the following way:

    kubectl apply -f zenoss_rbac.yaml

as references in [Usage](#usage-1).

Save the following YAML as `zenoss_rbac.yaml` as references above. Make
sure to preserve the proper YAML formatting:

    apiVersion: v1 kind: ServiceAccount metadata: name: zenoss namespace: default secrets: - name: zenoss-secret --- apiVersion: v1 kind: Secret metadata: name: zenoss-secret annotations: kubernetes.io/service-account.name: zenoss type: kubernetes.io/service-account-token --- apiVersion: rbac.authorization.k8s.io/v1 kind: ClusterRole metadata: name: zenoss-role rules: - apiGroups: [""] resources: - clusterrolebindings - componentstatus - configmaps - controllerrevisions - cronjobs - daemonsets - deployments - endpoints - events - horizontalpodautoscalers - ingress - jobs - limitranges - namespaces - networkpolicys - nodes - persistentvolumeclaims - persistentvolumes - pods - poddisruptionbudgets - podsecuritypolicys - podtemplates - replicasets - replicationcontroller rolebindings - secrets - services - serviceaccounts - statefulsets - status - storageclasses - nodemetrics verbs: ["get", "watch", "list"] - apiGroups: ["metrics.k8s.io"] resources: - nodes - pods verbs: ["get", "watch", "list"]
    - apiGroups: ["apps"]
     resources:
     - deployments
     - statefulsets
     verbs: ["get", "watch", "list"] --- apiVersion: rbac.authorization.k8s.io/v1 kind: ClusterRoleBinding metadata: name: zenoss-role-binding roleRef: kind: ClusterRole name: zenoss-role apiGroup: rbac.authorization.k8s.io subjects: - kind: ServiceAccount name: zenoss namespace: default

To validate added permissions run

kubectl api-resources -o wide

## Appendix: Identifying Master Nodes

Master node primary is identified by having one of the three processes:
kube-apiserver, kube-controller-manager and kube-scheduler.

Identifying master nodes can sometimes fail. We provide several ways to
test for master using Kubernetes node labels:

1.  `"node-role.kubernetes.io/master": ["master" | "true" | True]`
2.  `"master": ["true" | True]`

Note that \#2 can be a custom set label as described below.

If you have issues with your nodes being identified as non-master, you
can set a label on your node metadata as:

`master: "true"`

In GCP, this is edited in the UI:

`Kubernetes Engine -> Cluster -> Node -> YAML -> Edit`

In `kubectl`, you can edit the node YAML directly:

`kubectl edit node ${NODE_NAME}`

You should see end up with something like this:

    apiVersion: v1 kind: Node metadata: annotations: node.alpha.kubernetes.io/ttl: "0" volumes.kubernetes.io/controller-managed-attach-detach: "true" creationTimestamp: 2018-06-25T20:55:33Z labels: beta.kubernetes.io/arch: amd64 beta.kubernetes.io/fluentd-ds-ready: "true" beta.kubernetes.io/instance-type: g1-small beta.kubernetes.io/os: linux cloud.google.com/gke-nodepool: default-pool failure-domain.beta.kubernetes.io/region: us-central1 failure-domain.beta.kubernetes.io/zone: us-central1-a kubernetes.io/hostname: gke-cluster-1-default-pool-fc3e27a3-2mmx master: "true" spec: ... etc ...

## Appendix: AWS EKS nodes

An Amazon EKS cluster consists of two components:

-   The Amazon EKS control plane
-   Amazon EKS worker nodes

The Amazon EKS control plane includes master nodes that run the
Kubernetes software, such as the Kubernetes API server and etcd. The
control plane runs in a separate account managed by AWS. Amazon EKS
worker nodes run in customer's AWS account and connect to cluster's
control plane. So, on AWS EKS we should see only worker nodes.

## Appendix: AKS, Azure nodes

An Azure AKS cluster consists of two components:

-   The Azure frontend is managed by Ingress
-   The Azure production cluster hosts kubernetes nodes
-   Read more about [Microservices architecture on Azure Kubernetes Service](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/microservices/aks){.external-link}.

## Changes

### 1.2.0

-   Added monitoring of StatefulSet component (ZPS-6984)
-   Added zKubernetesPodFilter for filtering Pods and Containers
    (ZPS-7294)
-   Fixed Cluster, Container, and Node templates (ZPS-7409)
-   Fixed modeling of Pods with the same names (ZPS-7887)
-   Fixed namespace setting during modeling of Containers (ZPS-7888)
-   Tested with Zenoss Cloud, Zenoss 6.6.0 and Service Impact 5.5.5

### 1.1.0

-   Added support for incremental modeling

-   Added support for EKS (AWS) and AKS (Azure)

-   Add Deployment component and updated Impact relations (ZPS-4625)

-   Improved explanation in auth related errors (ZPS-5955)

-   Added Operating System Relationships (ZPS-5878)

-   Tested with Zenoss 6.4.1,
    Zenoss Cloud and Impact 5.5.1

### 1.0.1

-   Fix install issue with Zenoss 6.2.0 (ZPS-4674)
-   Tested with Zenoss 6.2.1, Zenoss Cloud and Impact 5.3.1

### 1.0.0

-   Initial Release
-   Tested with Zenoss 6.2.1, Zenoss Cloud and Impact 5.3.1

## Attachments:

-   [header.png](img/zenpack-header.png)
-   [K8sContainers.png](img/zenpack-k8scontainers.png)
-   [K8sDependencyView.png](img/zenpack-k8sdependencyview.png)
-   [K8sDynamicView.png](img/zenpack-k8sdynamicview.png)
-   [K8sImpact.png](img/zenpack-k8simpact.png)
-   [K8sImpactDiagram.png](img/zenpack-k8simpactdiagram.png)
-   [K8sModel.png](img/zenpack-k8smodel.png)
-   [K8sNamespaces.png](img/zenpack-k8snamespaces.png)
-   [K8sNodes.png](img/zenpack-k8snodes.png)
-   [K8sOverview.png](img/zenpack-k8soverview.png)
-   [K8sPersistentVolumes.png](img/zenpack-k8spersistentvolumes.png)
-   [K8sPods.png](img/zenpack-k8spods.png)
-   [K8sPortlets.png](img/zenpack-k8sportlets.png)
-   [K8sServices.png](img/zenpack-k8sservices.png)
-   [kubernetes-logo-zp.png](img/zenpack-kubernetes-logo-zp.png)
-   [K8sContainers.png](img/zenpack-k8scontainers.png)
-   [K8sDependencyView.png](img/zenpack-k8sdependencyview.png)
-   [K8sDynamicView.png](img/zenpack-k8sdynamicview.png)
-   [K8sImpactDiagram.png](img/zenpack-k8simpactdiagram.png)
-   [K8sImpact.png](img/zenpack-k8simpact.png)
-   [K8sModel.png](img/zenpack-k8smodel.png)
-   [K8sNamespaces.png](img/zenpack-k8snamespaces.png)
-   [K8sNodes.png](img/zenpack-k8snodes.png)
-   [K8sOverview.png](img/zenpack-k8soverview.png)
-   [K8sPods.png](img/zenpack-k8spods.png)
-   [K8sPersistentVolumes.png](img/zenpack-k8spersistentvolumes.png)
-   [kubernetes-logo-zp.png](img/zenpack-kubernetes-logo-zp.png)
-   [K8sServices.png](img/zenpack-k8sservices.png)
-   [K8sPortlets.png](img/zenpack-k8sportlets.png)
-   [header.png](img/zenpack-header.png)
-   [K8sNamespaces.png](img/zenpack-k8snamespaces.png)
-   [K8sContainers.png](img/zenpack-k8scontainers.png)
-   [K8sImpactDiagram.png](img/zenpack-k8simpactdiagram.png)
-   [K8sDependencyView.png](img/zenpack-k8sdependencyview.png)
-   [K8sServices.png](img/zenpack-k8sservices.png)
-   [K8sImpact.png](img/zenpack-k8simpact.png)
-   [K8sPersistentVolumes.png](img/zenpack-k8spersistentvolumes.png)
-   [K8sPods.png](img/zenpack-k8spods.png)
-   [header.png](img/zenpack-header.png)
-   [K8sNodes.png](img/zenpack-k8snodes.png)
-   [K8sDynamicView.png](img/zenpack-k8sdynamicview.png)
-   [K8sOverview.png](img/zenpack-k8soverview.png)
-   [K8sImpact.png](img/zenpack-k8simpact.png)
-   [K8sImpactDiagram.png](img/zenpack-k8simpactdiagram.png)
-   [K8sDependencyView.png](img/zenpack-k8sdependencyview.png)
-   [K8sDeployments.png](img/zenpack-k8sdeployments.png)
-   [K8sModelDiagram.png](img/zenpack-k8smodeldiagram.png)
-   [K8sImpactDiagram.png](img/zenpack-k8simpactdiagram.png)
-   [K8sImpact.png](img/zenpack-k8simpact.png)
-   [K8sModelDiagram.png](img/zenpack-k8smodeldiagram.png)
-   [K8sDependencyView.png](img/zenpack-k8sdependencyview.png)
-   [K8sDeployments.png](img/zenpack-k8sdeployments.png)
-   [K8sPods.png](img/zenpack-k8spods.png)


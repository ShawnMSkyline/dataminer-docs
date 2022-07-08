---
uid: 10_2_9_General_RNs
---

# DataMiner 10.2.9 release notes

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!NOTE]
> For release notes related to DataMiner Cube, see [DataMiner Cube 10.2.9 release notes](xref:10_2_9_Cube_RNs).

## Highlights

## Other new features

### Core functionality

#### SLPort: Order of parameters in an HTTP session request will be identical to that in the protocol [ID_33796]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

In an HTTP session request, the order of the parameters will now always be identical to that in the protocol.

#### DVE function protocol version of active functions will now be deleted when the main DVE protocol version is deleted [ID_33834]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When a version of a DVE protocol with function DVE protocols is deleted from the system while functions are active, from now on, the function DVE protocol versions associated with those active functions will also be removed from the system.

### DMS web apps

#### Web apps now also support parameter comments configured in Param.Message elements [ID_33784]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When configuring a parameter in a protocol, you can add a `<Message>` element containing a comment to be displayed in a confirmation box when users change that parameter on the user interface. Up to now, this `<Message>` element was only supported by DataMiner Cube. It is now also supported by web applications like Monitoring and Dashboards.

#### DataMiner web apps updated to Angular 13 [ID_33869]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

The DataMiner mobile apps that use Angular (e.g. low code apps, Dashboards, Monitoring, Ticketing, Jobs and Automation) now use Angular 13 instead of Angular 12.

#### GQI: Table columns of type 'decimal' can now also be used when filtering or aggregating data [ID_33927]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

Table columns of type "decimal" can now also be used when filtering or aggregating data.

#### GQI: When all data is requested, the page size will now be calculated based on the amount of columns that are retrieved [ID_33935]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

Up to now, when all GQI data was requested, the page size would always be set to 50. From now on, the page size will be set to a number between 50 and 1000, based on the amount of columns that are retrieved (max. 3000 cells).

### DMS Service & Resource Management

##### BREAKING CHANGE: Removing a Resource or ResourcePool object will now always require a valid ID [ID_33836]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

Up to now, it was possible to delete Resource and ResourcePool objects in a filtered way by passing an "incomplete" object to the associated remove method of the ResourceManagerHelper. Moreover, passing an empty list or NULL would remove all resources on the system. This will no longer be possible.

From now on, it will only be possible to remove Resource objects by ID or name (case sensitive) and ResourcePool objects by ID.

When DataMiner detects a remove request that contains an object with an empty ID (and an empty name in case of a request to remove a Resource object, one of the following messages will be added to the *ResourceManager.txt* log file (type: info):

- In case of a request to remove a Resource object:

    ```txt
    Detected a resource delete request that contained at least one object without an ID. Deleting resources with resource object filters is not supported anymore.
    ```

- In case of a request to remove a ResourcePool object:

    ```txt
    Detected a resource pool delete request that contained at least one object without an ID. Deleting resource pools with object filters is not supported anymore.
    ```

> [!NOTE]
> From now on, the log entries added when creating or deleting resources or resource pools will no longer contain the IDs of all objects that were created or deleted. Instead, they will only contain the IDs of the first 10 objects that were created or deleted.

### DMS tools

## Changes

### Enhancements

#### Cassandra Cluster Migrator: Enhanced resilience of the migration process [ID_33467] [ID_33621] [ID_33727]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

The migration process will now be executed partition by partition. This greatly enhances the overall resilience of that process.

When the source database is a Cassandra database, at the end of a migration process, the Migrator tool will now automatically retry to migrate the partitions that could not be migrated the first time. Moreover, when you manually restart a migration with failed partitions, only those failed partitions will be included in the new migration attempt. The migration will no longer have to be redone from scratch.

Also, additional fail-safes have been built in to cope with situations where the target Cassandra database cannot be reached.

#### SLLogCollector: Enhanced processing of SLProtocol memory dumps [ID_33932]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

Because of a number of enhancements, SLLogCollector is now better able to collect SLProtocol memory dumps, especially in cases where there is no reference to an element.

### Fixes

#### SLLogCollector would become unresponsive when the name of the process or the path where the files had to be stored contained spaces [ID_33493]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

While collecting log information, SLLogCollector would become unresponsive when the name of the process or the path where the collected files had to be stored contained spaces.

#### Run-time errors due to MessageBrokerReconnectThread problems in SLCloudBridge [ID_33716]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

In some cases, run-time errors could occur due to MessageBrokerReconnectThread problems in the SLCloudBridge process.

#### SLProtocol would leak memory leak each time a parameter of a replicated element was updated [ID_33745]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

SLProtocol would leak memory each time a parameter of a replicated element was updated.

#### Web services API would incorrectly no longer clear a number of its caches when the connection was lost [ID_33764]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

When the connection was lost, the web services API would incorrectly no longer clear a number of its caches.

#### Service & Resource Management: Child DVE element would not get activated when the main DVE element was in an error state [ID_33787]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When you tried to create a booking with a child DVE element linked to a main DVE element in an error state, the child DVE element would not automatically be activated, causing the booking to fail. Moreover, SLNet would not try to activate this child DVE element, causing subsequent bookings needing that same child DVE element to also fail, even if the main element had already recovered from the error state in the meantime.

#### Problem with SLAnalytics when an element or a parameter was deleted [ID_33788]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

When an element or a parameter was deleted, in some rare cases, an error could occur in the SLAnalytics process. 

#### GQI: Columns of type 'decimal' would incorrectly not be treated as columns of type 'numeric' [ID_33792]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

Columns of type "decimal" would incorrectly be treated as columns of type "string" instead of columns of type "numeric".

### Dynamic virtual elements: Problem when processing table columns containing foreign keys [ID_33810]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When a table contained multiple foreign keys, invalid foreign key values referring to non-existing rows could prevent those rows from being exported to DVE child elements. This would cause alarms, trend information, subscriptions, etc. to not get updated for specific DVE elements and/or virtual functions.

#### SLAnalytics: Error messages could get added to the log file due to a problem with the automatic incident tracking algorithm [ID_33820]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

Due to a problem with the automatic incident tracking algorithm, error messages similar to the following one could incorrectly get added to the SLAnalytics log file:

```txt
2022/06/08 23:54:36.684|SLAnalytics|Counter.h(61): containers::Counter<ServiceInfo>::decrease)|ERR|0|Decreasing counter for key that is not in the map
```

#### Problem with SLElement when resolving foreign keys took a long time and the the element debug log level was equal to or higher than 1 [ID_33826]

<!-- Main Release Version 10.0.0 [CU22]/10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When the element debug log level was equal to or higher than 1, an error could occur in SLElement when resolving foreign keys took a long time. 

#### Dashboards app - Service definition component: Function nodes would incorrectly not display the number of Process Automation tokens in queue or in progress [ID_33848]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->
<!-- Not added to 10.3.0 -->

When a Process Automation definition was added to a Service definition component, the function nodes would incorrectly not display the number of tokens currently in queue or in progress.

#### Web apps: No group row would appear when you selected a single item in a list view [ID_33858]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->
<!-- Not added to 10.3.0 -->

When you selected a single item in a list view, in some cases, no group row would appear.

#### SNMPv3 credentials would incorrectly be checked when replicating an element with SNMPv3 connections [ID_33859]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When you replicated an element with SNMPv3 connections, the SNMPv3 credentials of that element would incorrectly be checked. As a result, alarms like the following one would appear in the Alarm Console:

```txt
Load Element Failed: Error parsing SNMPv3 password for element: <element name>
```

#### DataMiner upgrade: VerifyNatsRunning prerequisite could fail due to SLCloudBridge.dll having been renamed [ID_33875]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

During a DataMiner upgrade, the *VerifyNatsRunning* prerequisite could fail due to the *SLCloudBridge.dll* file having been renamed to *SLMessageBroker.dll* in DataMiner versions 10.2.0/10.1.5.

#### Certain types of alarms could affect and degrade an SLA [ID_33899]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When an alarm of one the following types was generated, in some cases, that alarm could affect and degrade an SLA or be added to the list of active alarms for that SLA (i.e. enhanced service):

- Information Event
- Suggestion Event
- Error Alarm
- Notice Alarm

#### SLDataMiner would incorrectly no longer accept 'protocol' as a valid scriptingProcesses option [ID_33970]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->
<!-- Not added to 10.3.0 -->

In *DataMiner.xml*, the `scriptingProcesses` option can be set to an integer value, to "[service]" or to "protocol". However, SLDataMiner would incorrectly no longer accept the latter as a valid option.

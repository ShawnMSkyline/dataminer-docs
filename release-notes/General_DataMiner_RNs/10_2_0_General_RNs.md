---
uid: 10_2_0_General_RNs
---

# DataMiner 10.2.0 release notes

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

## Changes in DataMiner 10.2.0 CU6

### Enhancements

#### Security enhancements 

A number of security enhancements have been made.

#### Cassandra Cluster Migrator: Enhanced resilience of the migration process [ID_33467] [ID_33621] [ID_33727]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

The migration process will now be executed partition by partition. This greatly enhances the overall resilience of that process.

When the source database is a Cassandra database, at the end of a migration process, the Migrator tool will now automatically retry to migrate the partitions that could not be migrated the first time. Moreover, when you manually restart a migration with failed partitions, only those failed partitions will be included in the new migration attempt. The migration will no longer have to be redone from scratch.

Also, additional fail-safes have been built in to cope with situations where the target Cassandra database cannot be reached.

#### NATS: Enhancements to the NATS configuration [ID_33558] [ID_33931]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.8 -->

A number of enhancements have been made to the NATS configuration:

- STAN clustering has been removed.

- New NATSForceManualConfig option to disable the automatic reset timer in NATSCustodian.

    Disabling the timer can be done in one of the following ways:

    - Set the SLNet option **NATSForceManualConfig** to true in the SLNetClientTest tool (default = false).
    - Set the **SLNet.NATSForceManualConfig** tag to true in *MaintenanceSettings.xml*.

    > [!NOTE]
    > - Changing this option in the SLNetClientTest tool can be done at run-time. The change will be applied immediately.
    > - Forcing manual configuration will disable the automatic NATS configuration on the DataMiner System. It will then be up to the user to either manually configure a NATS cluster or manually call NatsCustodianResetNatsMessage when changes are made to the DMS.

- On DataMiner startup, NAS and NATS will now automatically be started if they are not running.

Also, the nats-streaming-server binary has been updated to v0.24.6. However, note that it will not be updated automatically via upgrade actions. It will only be installed during fresh NATS installations or when reinstalling NATS via SLEndpointTool_Console. The previous version (v0.22.0) and the new version (v0.24.6) version are compatible and are able to communicate with each other.

#### Dashboards app: Enhanced 'loading' indication when state component linked to a GQI query receives an update [ID_33640]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.8 -->

Up to now, each time a state component linked to a GQI query received an update, a *loading* indication would be displayed over the entire component. From now on, when such a component receives an update, a more subtle loader bar will be displayed instead.

Also, when a query error occur, from now on, the actual error will be displayed instead of "No data".

#### GQI: Enhanced performance when running a GQI query with a filter applied to it [ID_33664]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.8 -->

Because of a number of enhancements, overall performance has improved when running a GQI query with a filter applied to it.

#### Serial connections: Hostname resolution enhancements [ID_33702]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When a serial connection was configured with a hostname instead of an IP address, up to now, the hostname would be resolved when the port was initialized. When the hostname suddenly pointed to a different IP address, an element restart or a dynamic IP address change was needed for the serial connection to be aware of that change.

This has now been changed:

- In case of a TCP-oriented serial connection (serial SSL/TLS, SSH and serial TCP), the hostname will be resolved upon every connect.

- In case of a UDP-oriented serial connection (serial UDP), the hostname will be resolved prior to every send.

#### Web apps now also support parameter comments configured in Param.Message elements [ID_33784]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When configuring a parameter in a protocol, you can add a `<Message>` element containing a comment to be displayed in a confirmation box when users change that parameter on the user interface. Up to now, this `<Message>` element was only supported by DataMiner Cube. It is now also supported by web applications like Monitoring and Dashboards.

#### SLPort: Order of parameters in an HTTP session request will be identical to that in the protocol [ID_33796]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

In an HTTP session request, the order of the parameters will now always be identical to that in the protocol.

#### DVE function protocol version of active functions will now be deleted when the main DVE protocol version is deleted [ID_33834]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When a version of a DVE protocol with function DVE protocols is deleted from the system while functions are active, from now on, the function DVE protocol versions associated with those active functions will also be removed from the system.

#### GQI: Table columns of type 'decimal' can now also be used when filtering or aggregating data [ID_33927]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

Table columns of type "decimal" can now also be used when filtering or aggregating data.

#### SLLogCollector: Enhanced processing of SLProtocol memory dumps [ID_33932]

<!-- Main Release Version 10.0.0 [CU22]/10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

Because of a number of enhancements, SLLogCollector is now better able to collect SLProtocol memory dumps, especially in cases where there is no reference to an element.

#### SLSNMPManager: Enhanced performance [ID_33940]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

Because of a number of enhancements, overall performance of the SLSNMPManager process has improved.

#### New BPA test 'Verify Cloud DxM Version' [ID_33956]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.8 [CU0] -->

This new BPA test checks if the minimum required version is installed for all DxMs in the system.

It is available from DataMiner 10.2.8 and 10.2.0 [CU6] onwards. You can run it in System Center (on the *Agents > BPA* tab), and it also runs automatically when you upgrade to 10.2.0 [CU6]/10.2.8 or higher.

For more information, see [DataMiner Dojo](https://community.dataminer.services/documentation/verify-cloud-dxm-version/).

#### Enhanced error handling in case QActions fail due to a problem with SLScripting [ID_34010]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When an error occurs in SLScripting, from now on, a new SLScripting instance will be started and all QActions will be reloaded.

#### Parameter changes will now only be pushed from SLProtocol to SLElement when needed [ID_34047]

<!-- Main Release Version 10.0.0 [CU22]/10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

Up to now, parameter changes would always be pushed from SLProtocol to SLElement. From now, those changes will only be pushed from SLProtocol to SLElement when needed.

#### Size of the WebSocket messages sent from SLPort to SLProtocol will now be limited to 1024 packets [ID_34049]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

In order to prevent SLPort from running out of memory, from now on, the size of the WebSocket messages sent from SLPort to SLProtocol will be limited to 1024 packets.

### Fixes

#### SLLogCollector would become unresponsive when the name of the process or the path where the files had to be stored contained spaces [ID_33493]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

While collecting log information, SLLogCollector would become unresponsive when the name of the process or the path where the collected files had to be stored contained spaces.

#### GQI: Datetime values in retrieved booking information would incorrectly not be converted to UTC time [ID_33607]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.8 -->

When a GQI query retrieved booking information, the datetime values would incorrectly not be converted to UTC time.

#### Monitoring app: Trend graph of table column parameter not displayed when table row index contained forward slash [ID_33661]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.8 -->

In the Monitoring app, the trend graph of a table column parameter would not be displayed when the table row index contained a forward slash.

#### SLProtocol would leak memory leak each time a parameter of a replicated element was updated [ID_33745]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

SLProtocol would leak memory each time a parameter of a replicated element was updated.

#### Web services API would incorrectly no longer clear a number of its caches when the connection was lost [ID_33764]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When the connection was lost, the web services API would incorrectly no longer clear a number of its caches.

#### Service & Resource Management: Child DVE element would not get activated when the main DVE element was in an error state [ID_33787]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When you tried to create a booking with a child DVE element linked to a main DVE element in an error state, the child DVE element would not automatically be activated, causing the booking to fail. Moreover, SLNet would not try to activate this child DVE element, causing subsequent bookings needing that same child DVE element to also fail, even if the main element had already recovered from the error state in the meantime.

#### GQI: Columns of type 'decimal' would incorrectly not be treated as columns of type 'numeric' [ID_33792]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

Columns of type "decimal" would incorrectly be treated as columns of type "string" instead of columns of type "numeric".

#### Dashboards app: Options displayed in component headers would not be readable when a dark theme was applied [ID_33805]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.8 -->

When a dark theme was applied, options displayed in the header of certain dashboard components (e.g. “Export to CSV”) would not be readable.

#### Dynamic virtual elements: Problem when processing table columns containing foreign keys [ID_33810]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When a table contained multiple foreign keys, invalid foreign key values referring to non-existing rows could prevent those rows from being exported to DVE child elements. This would cause alarms, trend information, subscriptions, etc. to not get updated for specific DVE elements and/or virtual functions.

#### Web apps: Visio files would not get rendered correctly [ID_33812]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

In some rare cases, Visio files would not get rendered correctly in web apps (e.g. Dashboards).

#### Cassandra Cluster Migrator tool: Problem when migrating a large amount of data [ID_33821]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.8 -->

When the Cassandra Cluster Migrator tool was migrating a large amount of data, in some cases, an out of memory exception could be thrown.

#### Problem with SLElement when resolving foreign keys took a long time and the the element debug log level was equal to or higher than 1 [ID_33826]

<!-- Main Release Version 10.0.0 [CU22]/10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When the element debug log level was equal to or higher than 1, an error could occur in SLElement when resolving foreign keys took a long time.

#### Dashboards app - Visual Overview component: Loading bar at the top of the component instead of large loading message on top of the component [ID_33829]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.8 -->

When a Visual Overview component was loading, up to now, a large loading message was displayed on top of the component. From now on, when a Visual Overview component is loading, a loading bar will appear at the top of the component instead.

#### Dashboards app - Service definition component: Function nodes not displaying number of Process Automation tokens in queue or in progress [ID_33848]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When a Process Automation definition was added to a *Service definition* component, the function nodes would not display the number of tokens currently in queue or in progress.

#### SNMPv3 credentials would incorrectly be checked when replicating an element with SNMPv3 connections [ID_33859]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When you replicated an element with SNMPv3 connections, the SNMPv3 credentials of that element would incorrectly be checked. As a result, alarms like the following one would appear in the Alarm Console:

```txt
Load Element Failed: Error parsing SNMPv3 password for element: <element name>
```

#### SLProtocol could leak memory when the NT_UPDATE_PORTS_XML command was sent [ID_33891]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

In some cases, the SLProtocol process could leak memory when the NT_UPDATE_PORTS_XML command was sent.

#### Certain types of alarms could affect and degrade an SLA [ID_33899]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When an alarm of one the following types was generated, in some cases, that alarm could affect and degrade an SLA or be added to the list of active alarms for that SLA (i.e. enhanced service):

- Information Event
- Suggestion Event
- Error Alarm
- Notice Alarm

#### SLSNMPManager: StackOverflow exception while trying to resolve the next Request ID [ID_33901]

<!-- Main Release Version 10.0.0 [CU22]/10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

In some cases, SLSNMPManager could throw a StackOverflow exception while trying to resolve the next Request ID.

#### DataMiner upgrade: Upgrade action 'DeletePreRN28047CustomDataTemplates' would fail when Elasticsearch required authentication [ID_34029]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

During a DataMiner upgrade, the upgrade action *DeletePreRN28047CustomDataTemplates* would fail when Elasticsearch required authentication.

#### Problem with SLSNMPManager when an SNMP Get or Set was put on the queue while the element in question was being stopped [ID_34038]

<!-- Main Release Version 10.0.0 [CU22]/10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

In some rare cases, an error could occur in the SLSNMPManager process due to an SNMP Get or Set having been put on the queue while the element in question was being stopped.

#### GQI: No longer possible to select another row after collapsing a group containing a selected row [ID_34042]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When, in a GQI table, you collapsed a group that contained a selected row, it was no longer possible to select another row.

#### GQI: Problem when filtering or aggregating data by custom properties [ID_34058]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

In some cases, it would no longer be possible to build a GQI query that filtered or aggregated data by custom properties.

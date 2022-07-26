---
uid: 10_3_0_General_RNs
---

# DataMiner 10.3.0 release notes

- 33665 moved from 10.3.0 to 10.2.0 CU6

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!NOTE]
> For release notes related to DataMiner Cube, see [DataMiner Cube 10.3.0 release notes](xref:10_3_0_Cube_RNs).

## Highlights

## Other new features

### DMS Web apps

## Changes

### Enhancements

#### Service & Resource Management: Enhancements made to ResourceManagerHelper [ID_33993]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

A number of enhancements have been made to the ResourceManagerHelper class.

For example, from now on, an ArgumentNullException will be thrown when a NULL argument is provided. Also, when a collection with one or more NULL objects is provided, those objects will be ignored.

### Fixes

#### Jobs app: Corrected start time would be saved incorrectly [ID_34043]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

When, after receiving a message that it was not possible to save a job because of an invalid start time, you had corrected the start time and tried to save the job again, that start time would get saved incorrectly.


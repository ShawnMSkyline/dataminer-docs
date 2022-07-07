---
uid: 10_2_9_Cube_RNs
---

# DataMiner Cube 10.2.9 release notes

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

## Highlights

## Other new features

#### Trending: Prediction type selection has now moved to the context menu [ID_33861]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

In a trend graph, up to now, a drop-down list in the top-right corner allowed you to select one of the available trend prediction types or "Auto". This drop-down list has now been removed. Instead, you can now right-click the graph and select one of the available trend prediction types or "Auto" from the context menu.

#### Tab layout: Closing a card tab by clicking it with the middle mouse button [ID_33883]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

When the card layout is set to "tab layout", you can now close a card tab by clicking it with the middle mouse button.

## Changes

### Enhancements

#### Alarm Console: Time of history sets will now always be converted to the local time zone [ID_33849]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

From now on, the time of history sets will always be converted to the local time zone.

#### Data Display: More separator replacement options when specifying a SystemName containing colons in an EPM object link [ID_33857]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

Since DataMiner version 10.2.3, there is a new way of adding links to EPM objects in a Data Display table. When, in a protocol, you configure a cell button as shown below, the table cell will display the SystemType and SystemName defined in the EPM object. Clicking the link will open a new card for that object.

Example:

```xml
<Measurement>
    <Type>button</Type>
    <Discreets>
        <Discreet>
            <Display>{linkedItemName}</Display>
            <Value type="open">{pid:530}</Value>
        </Discreet>
    </Discreets>
</Measurement>
```

The discreet value can contain the SystemType and SystemName of the object, or a reference like "{pid:530}".

If you know the type of the EPM object, you can add a type prefix (epm or view), followed by an equal sign and (a reference to) the identifier, and if you want to specify the page to be selected by default, you can add a suffix to the identifier in the `<Value>` tag containing the root page name and the page name, separated by a colon.

If the SystemName contains colons (e.g. a MAC address), you can replace the default separator (i.e. colon) by another one (e.g. a pipe character) by placing a `[sep:XY]` prefix in front of the system name. See the following example:

```xml
<Value type="open">{EPM=[sep::|]CPE/00:01:08:01:08:01|DATA|CPE Frequencies}</Value>
```

From now on, you can specify a second custom separator to also replace the existing separator inside the SystemType and/or SystemName. Since the default separator between the SystemType and the SystemName is "/", this would mean that neither the systemType nor the SystemName would be allowed to contain that character ("/").

In the following example, a second `[sep:XY]` is used to replace the "/" inside the SystemType ("CPE/CPE") with another character ("$").

```xml
<Value type="open">{EPM=[sep::|][sep:/$]CPE/CPE$00:01:08:01:08:01|DATA|CPE Frequencies}</Value>
```

In short,

- the first `[sep:XY]` will replace the separator between the arguments, and
- the second `[sep:XY]` will replace the separator inside the SystemType and/or SystemName.

> [!NOTE]
> If you want to replace the separator inside the name, you must specify both the first `[sep:XY]` and the second `[sep:XY]`, even if there are no arguments.

#### Alarm Console - Proactive cap detection: Reduction of false positive matches [ID_33871]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When trend data is often getting close to the low or high value of a data range, this data range value will no longer be considered as a critical data boundary. This will reduce the number of false positive matches.

### Fixes

#### DataMiner Cube - Profiles app: Selected list items not visible on the UI would incorrectly not be validated after being edited [ID_33753]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

When, in the *Profiles* app, you edited a profile definition, a profile instance, a profile parameter or a service definition, the change would incorrectly not be validated if the item in question was not visible in the list.

#### DataMiner Cube - Profiles app: No validation errors were displayed when no discrete values had been added yet for a profile parameter of type discrete [ID_33756]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

When an error occurred while configuring a profile parameter of type "discrete", up to now, that error would not be displayed on the UI when no discrete values had been added yet.

#### Resources app: Warning messages were incorrectly shown in the footer when resource manager configuration requests returned error trace data [ID_33780]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

When you open the *Resources* app, a warning will be shown in the footer when error trace data was found when fetching resource manager data from the server. Up to now, such a warning would incorrectly also be shown when resource manager configuration requests returned error trace data.

#### Resources app: Updating a session variable in a Resource Manager component would incorrectly cause that same session variable to be updated in the Occupancy tab of the Resources app [ID_33800]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

When a session variable (e.g. YAxisResources) was updated in an embedded Resource Manager component, in some cases, that same session variable would also incorrectly be updated in the *Occupancy* tab of the Resources app.

#### Alarm Console would incorrectly keep loading while the tickets linked to the alarms were being loaded [ID_33847]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When you open DataMiner Cube, it will load the alarms and try to link the existing tickets to them so it can show the ticket information in the Alarm Console.

While this process was ongoing, in some rare cases, the Alarm Console would incorrectly keep on loading.

#### Alarm Console: Problem when loading [ID_33860]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

In some cases, an exception could be thrown while the Alarm Console was loading.

#### Alarm Console: Cube could become unresponsive when a large number of alarms were being added and removed in an alarm tab of type 'sliding window' [ID_33870]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When, in an alarm tab of type "sliding window", a large number of alarms were being added and removed, in some cases, DataMiner Cube could become unresponsive.

#### System Center: Element counter on Agents > Status tab would not be set to 0 when removing all elements from a DMA [ID_33885]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When you go to *System Center > Agents > Status*, the *Elements* column shows you how many elements are being hosted by each agent in the DMS.

When, on a particular agent, you removed all elements, the number of elements of that agent would incorrectly not be set to 0. Instead, it would be set to the last-known number of elements on that agent before the element were removed.

#### Spectrum analysis: Recording icon would no longer be displayed while making a spectrum recording [ID_33904]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

While making a spectrum recording, in some cases, the recording icon would no longer be displayed.

#### Visual Overview: Wait cursor would still be displayed after the scripts had already finished [ID_33911]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When, in Visual Overview, you clicked a shape that executed two Automation scripts, the cursor would incorrectly still be displayed as a wait cursor after the two scripts had already finished.

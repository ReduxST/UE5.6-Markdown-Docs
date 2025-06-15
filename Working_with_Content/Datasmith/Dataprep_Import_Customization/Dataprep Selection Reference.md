# Dataprep Selection Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-selection-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-selection-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:46

---

This page describes each of the **Select By** blocks that you can use in the Visual Dataprep system to identify scene elements that you want to carry out operations on.

Each type of **Select By** block offers a different set of criteria that you can fill in. When the Visual Dataprep system carries out each action in your Dataprep graph, it at first assumes that all operations defined in that action should apply to all Actors and all Assets in the imported scene. However, if your action contains any of the **Select By** blocks described on this page, the Visual Dataprep system checks each of those scene elements to see if it matches the criteria you've set up in the **Select By** block. If the scene element doesn't satisfy your criteria, the Visual Dataprep system removes that element from the list of scene elements it applies operations to for the current action. For more background information, see [Dataprep Import Customization](/documentation/en-us/unreal-engine/dataprep-import-customization-in-unreal-engine).

For information about the operations you can carry out on the scene elements identified by your **Select By** criteria, see [Dataprep Operation Reference](/documentation/en-us/unreal-engine/dataprep-operation-reference-in-unreal-engine).

## Select By Condition

**Select By Condition** blocks select a scene element only if a given condition is true for that element.

### Is Class Of

Use the **Is Class Of** block to select a scene element only if its Class after import into Unreal Engine matches the Class name that you specify in the **Class** setting.

This filter can select Assets, Actors, and Components.

Click image for full size.

| Setting | Description |
| --- | --- |
| **Class** | The Class that all scene elements must match to be selected by this block. |
| **Should Include Child Class** | 
Determines whether this block should consider a scene element to match successfully if its Unreal Engine Class is derived from the Class you set in the **Class** setting.

-   Enabled by default, the block will accept any scene elements whose Class derives from the Class you specify in the **Class** setting.
-   If you disable this setting, the block will only accept scene elements whose Class matches the **Class** setting exactly.

For example, suppose that you set the **Class** setting to **Actor**, and a scene element being considered has the Class **StaticMeshActor**. In this case, **StaticMeshActor** inherits from the base **Actor** Class, so the **Is Class Of** block will select that scene element only if the **Should Include Child Class** setting is enabled.



 |

### Jacketing / Select Hidden

This filter requires you to enable the **Dataprep Geometry Operations** plugin.

Use the **Jacketing / Select Hidden** filter to select elements that are inside of one or several Actors that you previously selected.

Click image for full size.

| Setting | Description |
| --- | --- |
| **Accuracy** | Defines the accuracy of the voxel grid that Datasmith uses to determine which elements are inside or outside an Actor's boundaries. |
| **Merge Distance** | Sets the maximum size of the gaps in the occluding volumes that the occlusion tests will consider to be filled. |

## Select By Float

**Select By Float** blocks select scene elements only if some numeric property of those scene elements is **Less Than**, **Greater Than**, or **Is Nearly Equal** to a given threshold value.

**Select By Float** blocks consider two numbers to be **Is Nearly Equal** if the difference between them is less than `0.0001`.

### Bounding Volume

Use the **Bounding Volume** block to select a scene element only if it has extents in 3D space (and therefore a bounding box), and only if the total volume of that bounding box satisfies the comparison you specify in the settings.

This filter can select Assets, Actors, and Components.

Click image for full size.

| Setting | Description |
| --- | --- |
| **Dropdown Menu** | The type of mathematical comparison you want to carry out between the bounding volume of the object and the volume you specify: **Less Than**, **Greater Than**, or **Is Nearly Equal**. |
| **Float Value** | The volume that you want to compare your object's bounding volume against, in cubic centimeters. |

For example, suppose a Static Mesh has a bounding volume that is 100 centimeters by 100 centimeters. The volume of its bounding box is 100x100, or 10000 cubic centimeters. Therefore, this block would select that Static Mesh if you set it to **Less Than** any number larger than 10000, or **Greater Than** any number below 10000.

## Select By Integer

**Select By Integer** blocks select scene elements only if some numeric property of those scene elements is **Less Than**, **Greater Than**, or **Is Nearly Equal** to a given threshold value.

### Triangle Count

Use the **Triangle Count** block to select only the Static Mesh Actors and Static Mesh Assets whose number of triangles satisfies the comparison you specify in the settings.

This filter can select Assets, Actors, and Components.

Click image for full size.

| Setting | Description |
| --- | --- |
| **Dropdown Menu** | The type of mathematical comparison you want to carry out between the number of triangles in the mesh and the number you specify: **Less Than**, **Greater Than**, or **Is Nearly Equal**. |
| **Integer Value** | The number that you want to compare your object's triangle count against. |

For example, if a Static Mesh Actor or Asset has 2000 triangles, this block would select that object if you set the block to **Less Than** any number larger than 2000, or **Greater Than** any number below 2000.

### Vertex Count

Use the **Vertex Count** block to select only the Static Mesh Actors and Static Mesh Assets whose number of vertices satisfies the comparison you specify in the settings.

This filter can select Assets, Actors, and Components.

Click image for full size.

| Setting | Description |
| --- | --- |
| **Dropdown Menu** | The type of mathematical comparison you want to carry out between the number of vertices in the mesh and the number you specify: **Less Than**, **Greater Than**, or **Is Nearly Equal**. |
| **Integer Value** | The number that you want to compare your object's vertex count against. |

For example, if a Static Mesh Actor or Asset has 5000 vertices, this block would select that object if you set the block to **Less Than** any number larger than 5000, or **Greater Than** any number below 5000.

## Select By String

**Select By String** blocks select scene elements only if a given string property of those scene elements match a string pattern that you specify.

All string conditions can use either a single string or an array of strings. To toggle between these two options, click the **Switch to Single / Switch to Array** button. For string arrays, the filter will return any objects (Actors, Assets, and / or Components, depending on filter limitations) that match **at least** one of the array elements.

Click image for full size.

These blocks offer three string comparisons:

| Setting | Description |
| --- | --- |
| **Contains** | The comparison is successful if the string you provide is contained in its entirety anywhere within the value of the string property of the scene element being considered. You can't use any wildcards in this type of comparison; `*` and `?` characters are treated literally. |
| **Matches Wildcard** | 
The comparison is successful if the entire length of the string you provide matches the entire length of the string property of the scene element being considered, using the following wildcard characters:

-   An asterisk (`*`) in the pattern can stand in for any number of characters in the string property.
-   A question mark (`?`) in the pattern can stand in for zero or one characters in the string property.

The pattern must match the whole length of the string. If you want to provide a partial string that might occur anywhere within the value of the string property you are comparing against, start and end your string pattern with an asterisk (`*`). For example, if the string property value is `MyActorName`, then the pattern `A*tor` will not match, but `*A*tor*` will.



 |
| **Exact Match** | The comparison is only successful if the string you provide is an exact match for the value of the string property of the scene element being considered. It must be the same length, and it must contain the same set of characters all in the same order. |

### Actor Label

Use the **Actor Label** block to select Actors in the Dataprep preview scene — that is, any items shown in the **Outliner Preview** panel — only if the string that you specify matches the names that you see assigned to those Actors in the **Outliner Preview**.

This filter can only select Actors and Assets.

Click image for full size.

| Setting | Description |
| --- | --- |
| **Dropdown Menu** | The type of string comparison you want to carry out between the Actor's label and the string you provide. See [Select By String](/documentation/en-us/unreal-engine/dataprep-selection-reference-in-unreal-engine#selectbystring) above for details. |
| **Actor Label (String) Box** | The string pattern you want to test against the Actor's label. |

### Metadata Value

Use the **Metadata Value** block to select Actors in the Dataprep preview scene — that is, any items shown in the **Outliner Preview** panel — only if the Actor has Datasmith Metadata with the **Key** you specify in the settings, and the value of that Datasmith Metadata key matches the string value you provide in the settings.

This filter can select Assets, Actors, and Components.

Click image for full size.

| Setting | Description |
| --- | --- |
| **Dropdown Menu** | The type of string comparison you want to carry out between the Actor's Datasmith Metadata value and the string you provide. See [Select By String](/documentation/en-us/unreal-engine/dataprep-selection-reference-in-unreal-engine#selectbystring) above for details. |
| Metadata (String) Box | The string pattern you want to test against the Actor's Datasmith Metadata value. |
| **Key Box** | The name of the key that you want to look for in the Actor's Datasmith Metadata. |

For example, suppose that you have an Actor that is assigned the following set of Datasmith Metadata after import:

Click image for full size.

If you set the **Key** value to **Category**, you could select this Actor by choosing the **Contains** operation and setting the string pattern in the third column to `Floor` or `Floors`.

For more about Datasmith Metadata, see [Using Datasmith Metadata](/documentation/en-us/unreal-engine/using-datasmith-metadata-in-unreal-engine).

### Object Name

Use the **Object Name** block to select Assets — that is, Static Meshes, Textures, Materials, and Animations listed in the **Content Browser Preview** panel — only if the string you specify matches the names that you see assigned to those Assets in the **Content Browser Preview**.

This filter can select Assets, Actors, and Components.

Click image for full size.

| Setting | Description |
| --- | --- |
| **Dropdown Menu** | The type of string comparison you want to carry out between the scene element's name and the string you provide. See [Select By String](/documentation/en-us/unreal-engine/dataprep-selection-reference-in-unreal-engine#selectbystring) above for details. |
| **Object Name (String) Box** | The string pattern you want to test against the object's name. |

### Actor Layer

Use the **Actor Layer** block to select Actors in the Dataprep preview scene—that is, any items shown in the **Outliner Preview** panel—only if that Actor is in the Layer that you specify.

This filter can only select Actors.

Click image for full size.

| Setting | Description |
| --- | --- |
| **Dropdown Menu** | The type of string comparison you want to carry out between the Actor's Layer and the string you provide. See [Select By String](/documentation/en-us/unreal-engine/dataprep-selection-reference-in-unreal-engine#selectbystring) above for details. |
| **Actor Label (String) Box** | The string pattern you want to test against the Actor's Layer. |

### Tag Value

Use the **Tag Value** block to select a scene element only if it possesses the Actor tag you specify in the **Tag** setting.

This filter can select Assets, Actors, and Components.

Click image for full size.

| Setting | Description |
| --- | --- |
| **Dropdown Menu** | The type of string comparison you want to carry out between the Actor's label and the string you provide. See [Select By String](/documentation/en-us/unreal-engine/dataprep-selection-reference-in-unreal-engine#selectbystring) above for details. |
| **Tag (String) Box** | 
The name of the tag that you want to look for.

Only Actors that have a tag that exactly matches this value will be selected.



 |

For example, if your Actor is imported with the following set of tags:

Click image for full size.

You could select this Actor in your **Actor Tag** block by setting the value of the **Key** setting to `Max.superclassof: GeometryClass`, `Max.classof: EditablePolyMesh`, `Max.handle: 407`, or any other value shown in the list above.

For more information on the Actor tags imported by Datasmith, see [About the Datasmith Import Process](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine#metadata).
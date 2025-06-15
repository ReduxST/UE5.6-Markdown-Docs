# The Datasmith 3ds Max UI

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/the-datasmith-3ds-max-ui-for-exporting-to-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/the-datasmith-3ds-max-ui-for-exporting-to-unreal-engine)  
**Processed:** 2025-06-14 16:54:22

---

## The 3ds Max Ribbon

When you install the Datasmith 3ds Max Exporter plugin, it adds a Datasmith tab to the 3ds Max ribbon (see [Using the Ribbon](https://knowledge.autodesk.com/support/3ds-max/getting-started/caas/CloudHelp/cloudhelp/2021/ENU/3DSMax-Basics/files/GUID-F2C0C6D6-968E-40F1-9474-5A7FC44FBC06-htm.html) in the 3ds Max documentation). You can access all of the Datasmith tools and settings for 3ds Max from the ribbon.

![Datasmith tab of the 3ds Max ribbon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/474eb114-9300-4507-bd4a-b58305ed0a58/datasmith-ribbon.png "Datasmith tab of the 3ds Max ribbon")

The Datasmith tab of the 3ds Max ribbon

1.  [Direct Link Panel](/documentation/en-us/unreal-engine/the-datasmith-3ds-max-ui-for-exporting-to-unreal-engine#directlinkpanel)
2.  [File Export Panel](/documentation/en-us/unreal-engine/the-datasmith-3ds-max-ui-for-exporting-to-unreal-engine#fileexportpanel)
3.  [Settings Panel](/documentation/en-us/unreal-engine/the-datasmith-3ds-max-ui-for-exporting-to-unreal-engine#settingspanel)
4.  [Tools Panel](/documentation/en-us/unreal-engine/the-datasmith-3ds-max-ui-for-exporting-to-unreal-engine#toolspanel)

### Direct Link Panel

| Option | Description |
| --- | --- |
| Synchronize | 
Pushes the 3ds Max scene or selection to the local Direct Link cache directory.

Unreal Engine, and any other destination applications, monitors the cache, and updates the imported scene when it detects a change.

You can change the location of the Direct Link cache directory. For details, see [Change the Direct Link Cache Directory](/documentation/en-us/unreal-engine/using-direct-link-to-synchronize-3ds-max-and-unreal-engine#changethedirectlinkcachedirectory).



 |
| Toggle Auto Sync | 

When enabled, Datasmith automatically pushes the 3ds Max scene to the Direct Link cache whenever you make a change.

Unreal Engine re-imports the scene whenever it detects a change to the cache.



 |
| Connections | Opens the [Datasmith Direct Link Connection Status window](/documentation/en-us/unreal-engine/the-datasmith-3ds-max-ui-for-exporting-to-unreal-engine#thedatasmithdirectlinkconnectionstatuswindow). |

### File Export Panel

| Option | Description |
| --- | --- |
| Export | Exports the 3ds Max Scene to a `.udatasmith` file that you can import into Unreal Engine, or an Unreal Engine-based application such as Twinmotion, or an Unreal Engine runtime application. Datasmith only exports visible objects. |
| Export Selected | Exports currently selected objects in the 3ds Max scene to a `.udatasmith` file that you can import into Unreal Engine, or an Unreal Engine-based application such as Twinmotion, or an Unreal Engine runtime application. Datasmith only exports visible objects. |
| Animated Transforms | 
Specifies how the Datasmith exporter handles objects with animated 3D transforms.

-   **Current Frame Only**: Datasmith exports objects in the scene as they appear in the current frame, without any animation data.
-   **Active Time Segment**: Datasmith exports animation data for any objects whose 3D transforms are animated in the active time segment in the 3ds Max timeline.

The Datasmith importer converts animation data into a [Level Sequence](/documentation/en-us/unreal-engine/creating-level-sequences-with-dynamic-transforms-in-unreal-engine), which you can use to play back the animations in Unreal Engine.



 |

### Settings Panel

| Option | Description |
| --- | --- |
| Limit Texture Resolution | 
When Datasmith bakes procedural textures into images for import in Unreal Engine, this setting specifies the maximum number of pixels in the baked images. Possible values range from 4K (4096 pixels) to 16M (16 megapixels).

For example, if you set this value to 4K, Datasmith limits textures to resolutions that contain 4096 pixels (64x64, 128x32px, and so on).

This setting does not affect the size of raster textures, for example TIFF or JPEG files assigned as bump maps, diffuse maps, and so on.



 |
| Export XRef Scenes | 

Specifies whether to include XRef scenes in the exported `.udatasmith` file.

XRef scenes are externally-referenced scenes that appear in your current file, but are loaded temporarily from other MAX files.

For more information, see [XRef Scene](https://knowledge.autodesk.com/support/3ds-max/getting-started/caas/CloudHelp/cloudhelp/2023/ENU/3DSMax-Manage-Scenes/files/GUID-5DB41A62-D7A5-4D54-AC83-5D03C9F7DB11-htm.html?us_oa=akn-us&us_si=9d8783af-02e1-4f82-be05-9f5d61f67e42&us_st=xref%20scene) in the 3ds Max documentation.



 |

### Tools Panel

| Option | Description |
| --- | --- |
| Messages | Opens the [Datasmith Messages window](/documentation/en-us/unreal-engine/the-datasmith-3ds-max-ui-for-exporting-to-unreal-engine#thedatasmithmessageswindow). |
| Add Datasmith Attributes Modifier | 
Applies a Datasmith Attributes Modifier to currently selected objects.

Datasmith Attributes Modifiers provide options to customize the way Datasmith exports specific objects.For details, see [Per-Object Conversion Settings](/documentation/en-us/unreal-engine/datasmith-per-object-conversion-settings-for-exporting-to-unreal-engine).



 |

## The Datasmith Direct Link Connection Status Window

The Datasmith Direct Link Connection Status window lists connections between the current instance of 3ds Max and instances of Unreal Engine or another Unreal Engine-based application such as Twinmotion.

Hover over any item in the list to display a tooltip with additional information about the connection.

The Connection Status window also has options for setting the Direct Link cache directory. For details, see [Change the Direct Link Cache Directory](/documentation/en-us/unreal-engine/using-direct-link-to-synchronize-3ds-max-and-unreal-engine#changethedirectlinkcachedirectory).

![The Datasmith Direct Link Connection Status window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac47138b-b234-416a-b0c3-ab91d0047501/datasmith-direct-link-connection-status.png "The Datasmith Direct Link Connection Status window")

The Datasmith Direct Link Connection Status window in 3ds Max

## The Datasmith Messages Window

The Datasmith Messages window provides information about exports from 3ds Max to Unreal Engine. When you export a scene or a selection, the messages window displays some export statistics, and reports of any issues with the content. Typically, notifications alert you to things that the exporter couldn't translate perfectly, or that may not show up in the Unreal Engine in exactly the way they do in 3ds Max.

![The Datasmith Messages window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/348f9a64-dcc0-40b4-bb61-66abeaac1e23/datasmith-messages.png "The Datasmith Messages window")

The Datasmith Messages window in 3ds Max

### Enable Statistics for Direct Link

By default, the Datasmith Messages window only shows export statistics when you export a `.udatasmith` file. To enable export statistics for Direct Link Sync and AutoSync, enter the following command in the MaxScript console window :

`Datasmith_SetExportOption_StatSync true`
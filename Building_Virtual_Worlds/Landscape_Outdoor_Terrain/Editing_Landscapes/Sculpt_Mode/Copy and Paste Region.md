# Copy and Paste Region

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/copy-and-paste-region-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/copy-and-paste-region-in-unreal-engine)  
**Processed:** 2025-06-14 16:16:24

---

The **Copy/Paste** tool will copy the height data from one area of a Landscape to another area through the use of the gizmos. You can also import existing heightmap data that can be pasted into the Landscape or export selected regions of your height data as it's own heightmap .raw file for use in an external program.

## Using the Copy/Paste Tool

In this demonstration, the gizmo is manually scaled to copy a region and then paste it in another location, and then the Region Selection is used to paint an area the gizmo can automatically scaled to fit so that it can be copy and pasted to another location.

### Copy/Paste Gizmo

The Gizmo is used to capture the Landscape's height data that can then be copied to other parts of the Landscape. This enables you to easily move parts of your Landscape, import height data from an existing heightmap, or to export your height data to a heightmap file that can be used with an external program, like World Machine.

|   |   |   |
| --- | --- | --- |
| ![Selecting height data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/641052c9-57b5-4993-babe-c8cae714395d/01-selecting-height-data.png) | ![Copying height data to the Gizmo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b751e368-47af-4eb3-947b-9d19cb4944f8/02-copying-height-data-to-the-gizmo.png) | ![Copying gizmo data to the heightmap](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf7dcdb2-46a2-4068-a4f2-9728e706b453/03-copying-gizmo-data-to-the-heightmap.png) |

In these examples, the gizmo bounds have been scaled around a painted region that is to be captured, then the gizmo is positioned to another part of the Landscape, and, lastly, it's pasted onto the existing Landscape.

To learn how to use the gizmo, you can read about the [gizmo tool](/documentation/en-us/unreal-engine/landscape-copy-tool-in-unreal-engine) here.

## Tool Settings

|   |   |
| --- | --- |
| ![Copy/Paste Tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3a5f5ca-1770-4bea-8d74-f150160e51b6/04-copy-paste-tool.png) | ![Copy and Paste tool properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acd6c32e-bec4-4f36-a02a-aaeb9c950f35/05-copy-and-paste-tool-properties.png) |

| **Property** | **Description** |
| --- | --- |
| **Copy Data to Gizmo** | Copies the data within the gizmo bounds to the gizmo taking into account any masking from the selected regions. |
| **Fit Gizmo to Selected Regions** | Positions and resizes the gizmo so that it completely encompasses all region selections. |
| **Fit Height Values to Gizmo** | Scales the data in the gizmo to fit the gizmo's Z-size. |
| **Clear Gizmo Data** | Clears the gizmo of any copied data. |
| **Tool Strength** | Strength of the tool. If you're using a pen/tablet with pressure-sensing, the pressure used affects the strength of the tool. |
| **Paste Mode** | 
Whether the past will only raise, only lower, or both raise and lower:

-   **Both**: The paste will raise and lower values where the data would be.
-   **Raise**: The paste may only raise values and pastes where the data would be. Any areas below the heightmap are left unchanged. This is good for copying and pasting mountains.
-   **Lower**: The paste may only lower values and pastes where the data would be. Any areas above the heightmap are left unchanged. This is good for copying and pasting valleys or pits.



 |
| **Gizmo Copy/Paste All Layers** | Copies and pastes all layers. Otherwise, it will only copy and paste the layer selected in the targets panel. |
| **Snap Gizmo to Landscape Grid** | Makes sure the gizmo is snapped perfectly to the Landscape so that the sample points line up, which makes copy and pastes less blurry. Irrelevant if gizmo is scaled. |
| **Use Smooth Gizmo Brush** | Smooth the edges of the gizmo data into the Landscape. Without this, the edges of the pasted data will be sharp. |
| Advanced |   |
| **Gizmo Import/Export** | 

The available options that can be used when importing or exporting the selected region's heightmap:

-   **Heightmap**: Set the import file path for the heightmap file you want to import.
-   **Heightmap Size**: The size of the heightmap data that is being imported. This property should not have to be adjusted.
-   **Layer Filename**: Set the import file path for the heightmap data used for painted layers.
-   **Layer Name**: Set the name of the imported heightmap layer.



 |
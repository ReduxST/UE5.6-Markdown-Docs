# Landscape Copy Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-copy-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-copy-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:06

---

**Landscape Gizmos** are editor-only Actors that are similar to volumes in that they define a specified area. Their purpose is to hold height and layer data for an area of a Landscape so that it can be copied to another location on the Landscape or exported for use in a different Landscape or heightmap generator (World Machine, Terresculptor,...).

## Accessing the Gizmo Tool

**To access the Gizmo tool:**

1.  In **Landscape** mode, click the **Sculpt** tab to open the **Sculpt Tools** toolbar.
    
    ![Sculpt Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7d0dfdb-86fc-4f74-b4b5-c228e7cf197f/landscape_sculptmenu.png)
2.  Choose **Copy** option from the toolbar. The Gizmo brush appears on your selected Landscape as a red-outlined box.
    
    ![Gizmo Outline](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bffb2a9-14c7-4516-a09f-2b5e53720394/landscape_gizmooutline.png)

Selecting the Gizmo brush creates a temporary Gizmo Actor. You can use the transformation tools to manipulate this Actor as you would any other, to define the area of the Landscape you want to copy.

For more information about the transformation tools, see [Transforming Actors](/documentation/en-us/unreal-engine/transforming-actors-in-unreal-engine).

You can also modify the Gizmo Actor's properties in the **Details** panel.

![Gizmo Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/108e6482-4a20-4f8a-8c08-10206a52b9aa/landscape_gizmoproperties.png)

| Property | Description |
| --- | --- |
| **Width** | The base width for Gizmo Actor in Unreal Units; X axis shown as red line. |
| **Height** | The base height for the Gizmo Actor in Unreal Units; Y axis shown as green line. |
| **LengthZ** | The base Z length for the Gizmo Actor in Unreal Units. |
| **MarginZ** | The Z value for space when you fit the Gizmo to the selection, with Max height and Min height. When you fit Gizmo to selected region, LengthZ = (Max height - Min height) + 2 \* MarginZ. |
| **MinRelativeZ** | The minimum height value of data in the Gizmo. Height values in the Gizmo are normalized from 0.f to 1.f and displayed as (Value - MinRelativeZ) \* RelativeScaleZ. |
| **RelativeScaleZ** | The height scale of the data in the Gizmo. |
| **TargetLandscape** | The currently selected Landscape, which the Gizmo tool will be used on. |

## Copying to the Gizmo

In order to copy a portion of a Landscape, the data for that area must be copied to a Gizmo. Then, that data can later be pasted to another location.

**To copy a selected region:**

1.  In **Sculpt** mode, select the **Region Selection** sculpting tool.
    
    ![Region Select](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1565f132-7954-4550-9895-d3b14e7450bd/landscape_regionselect.png)
2.  Use the brush strokes to select a region of the Landscape, similar to the normal painting process.
    
    ![Gizmo Copy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/861ced88-835a-4b99-adb2-df3eb233fcf8/landscape_gizmocopy1.png)
3.  Select the **Copy/Paste** sculpting tool.
    
    ![Copy button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96d428ef-710f-4ae3-8f85-4b6b12555259/landscape_copy.png)
    
    The Gizmo will become visible in the viewport.
    
    ![Gizmo Tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6fec5507-7c6e-4a24-87e9-687c5fb92371/landscape_gizmocopy2.png)

1.  Click the **Fit Gizmo to Selected Regions** button to position and size the Gizmo so that it encompasses all selected regions.
    
    ![Copy Gizmo Data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e833e22c-5c2d-47b4-a888-d74ca85b3f9c/landscape_gizmocopy3.png)
2.  Click the **Copy Data to Gizmo** button to transfer the data for the selected region of the Landscape within the Gizmo's bounds. Pressing **Ctrl + C** performs the same function.
    
    ![Copied Gizmo Data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52f5ae59-9eb2-4746-85e7-e352fb5e4b56/landscape_gizmocopy4.png)

**To copy an area within a Gizmo:**

1.  Select the **Region Copy/Paste** sculpting tool. The Gizmo will become visible in the viewport.
2.  Select the Gizmo by clicking on it. The transform widget should appear.
    
    ![Transform Gizmo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12195450-0c01-43f6-a151-54dca38056de/landscape_gizmocopy5.png)
3.  Move, rotate, and scale the Gizmo so that it encompasses the portion of the Landscape you wish to copy.
    
    ![Transformed Gizmo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97e27529-5879-4101-8b9b-d92e8c239369/landscape_gizmocopy6.png)
4.  Press the **Copy Data to Gizmo** button to transfer the data for the portion of the Landscape within the Gizmo's bounds. Pressing **Ctrl + C** performs the same function.
    
    ![Copied Data to Gizmo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbecccbe-8c86-468a-96a9-3601f2925fe5/landscape_gizmocopy7.png) ![Copiy Data to Gizmo button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0c5fab8-49fb-4a69-8b3f-caf713271520/landscape_gizmocopy7-2.png)

## Pasting from the Gizmo

Pasting data from a Gizmo makes it possible to transfer parts of a Landscape from one location to another. The data can either be [pasted](/documentation/en-us/unreal-engine/landscape-copy-tool-in-unreal-engine#pastingdata) completely to create an identical feature, or it can be painted to the new location using brush strokes and strength settings to partially transfer the feature.

Before data can be pasted from a Gizmo, it must first be [copied](/documentation/en-us/unreal-engine/landscape-copy-tool-in-unreal-engine#copyingdata) to a Gizmo.

**To paste Gizmo data:**

1.  Move, rotate, and scale a Gizmo that contains data so that it covers the area you wish to paste the data to.
    
    ![Translating Gizmo to Paste](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48065246-8882-49e0-98c9-bd4dd03fb2dd/landscape_gizmopaste1.png) ![Gizmo Paste](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91b50d69-c954-4170-8fad-29b8e2efd709/landscape_gizmopaste2.png)
2.  Paste the data using one of the available brushes (Circle, Pattern, Alpha, Gizmo) to "paint" the data from the Gizmo.
    
    -   The Gizmo brush is used to fully paste the data from the Gizmo. Pressing **Ctrl + V** also fully pastes the data from the Gizmo.
    -   Other brushes can be used to paint the data from the Gizmo using the current brush size and strength.
    
    ![Painting Gizmo Data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0263798-573d-4020-935a-c405d94be218/landscape_gizmopaste4.png) ![Painted Gizmo Data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e6b5767-68d0-414e-8ca2-9400cbf0841e/landscape_gizmopaste5.png)

## Gizmo Data Import/Export

Heightmap data can be imported from and exported to the Gizmo through the **Gizmo Import/Export** section in the **Landscape Editor**.

![Gizmo Import/Export options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c48134a7-509d-4bb1-ac77-7f3ac1a7f980/gizmo_importexport.png)

**To import data to the Gizmo:**

1.  Click the browse for file button ( ![import_filebrowse.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/837260e2-8335-4b7b-b5f9-98ea6627d478/import_filebrowse.png)) and select the heightmap file (16-bit raw file) you want to import to the Gizmo.  
    ![Importing external Gizmo data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/965f844b-ad55-43e9-969f-6d0bf41ec1db/gizmo_import_file.png)
    
    Since the import process uses the .raw file format, there is no way to correctly determine which dimension is which. UE4 will populate a dropdown menu with several different sizes that can be accessed by clicking the down arrow shown above. You may need to try a few different sizes before you find the one that works for your Landscape.
    
2.  If you want to import layer weight information as well, press the Add Layer button ( ![import_layeradd.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/260e6171-ff84-4b08-a6dc-f785c7a80c9e/import_layeradd.png)) to add as many layers as desired.  
    ![Importing Layer weight data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29f77267-fab8-4055-961b-a745be267c6c/gizmo_import_layerfields.png)
3.  Select the layer weightmap file (8-bit raw file) to import for each layer. The file and layer name will be filled in. The layer name uses the name of the file by default. Change the layer name if needed. Enabling the **No Import** checkbox will prevent any individual layer information from being imported.
    
    The Layer Name must match the name of a layer that exists on the Landscape or the import will fail.
    
    ![Layer name must match exactly what is in the file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/243f6a0f-aef9-442f-8fb8-08bfa5630644/gizmo_import_layerfile.png)
4.  Once the heightmap and any layers are selected, press the **Import to Gizmo** button to import the data to the Gizmo.  
    If the dimensions are not correct, you may see something similar to this:
    
    ![Import Wrong Dimensions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d710afc7-694f-4c08-b255-34ef4b1ec52e/landscape_importwrongdimensions.png)
    
    Reverse the dimensions and re-import to get the correct result. If the dimensions were correct, the Gizmo should show the correct data.
    

**To Export Gizmo Data:**

1.  With the Gizmo populated with data (see [Copying to the Gizmo](/documentation/en-us/unreal-engine/landscape-copy-tool-in-unreal-engine#copyingdata)), press the **Export Gizmo Data** button to export the Gizmo data to a file. Enabling the **Gizmo copy/paste all layers** checkbox at the top of the Gizmo options will export the heightmap and all layers' weight data to files.
2.  Choose a location and name for the heightmap file.  
    ![Exporting Heightmap file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7859277-2ed0-44d6-9b07-9610fce20dbb/export_file.png)
3.  If exporting layers, choose locations and filenames for each exported layer.  
    ![Exporting Layer file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d792b133-5f45-4edc-9546-2257d1466dff/export_layerfile.png)
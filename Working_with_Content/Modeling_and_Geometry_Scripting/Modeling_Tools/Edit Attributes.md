# Edit Attributes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/edit-attributes-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/edit-attributes-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:30

---

The **Edit Attributes** tool creates, edits, and inspects various attributes of your mesh. Attributes are information defined on a mesh surface, often at a mesh element level (for example, per-vertex or per-triangle). You can edit the following attributes:

-   Normals
-   Tangents
-   UV channels
-   Lightmap UVs
-   Weight map layers
-   PolyGroup layers

You can use the Edit Attributes tool for optimization, organization, and adding details to a mesh.

![Edit Atributes' UI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69244028-ae97-47e6-902b-cb344513d8b9/edit-attributes-ui.png)

## Accessing the Tool

You can access the Edit Attributes tool from the following:

-   The **Attributes** category in **Modeling Mode**. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).
-   The **Editing Tools** tab in the **Skeleton Editor**. To learn more, see [Skeleton Editing](/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine).

## Using Edit Attributes

Depending on your workflow, you can use the Edit Attributes tool both before and after editing the topology of a mesh.

For example:

-   Reset normals after using the **Dynamic Sculpt** tool.
-   Create a weight map layer before using the **Paint Maps** tool.

### Normals

The Normals section consists of action buttons for removing normals and tangents.

Adjusting a mesh with various operations over time can cause undesirable normals and tangents. For example, if you sculpt a box mesh into a round shape, the direction of the original faces changes. This change can cause improper lighting or parts of your mesh to not render. To correct this effect, you can reset the normals to compute the new direction of the faces.

| **Buttons** | **Description** |
| --- | --- |
| **Reset Hard Normals** | Removes hard edges and split normals, setting all normals to a single average vertex normal. |
| **Discard Tangents** | Clears tangents from the mesh. |

### UVs

The **UVs** section contains options for creating and removing UV channels. You can use UV channels to create different UV maps for one mesh. To learn more about UVs and related terminology, see [UVs Category](/documentation/en-us/unreal-engine/uvs-category-in-unreal-engine).

To view and select UV channels, use the **UVLayer** dropdown. This dropdown is also known as UV channel. To create and adjust your UV channels, use the action buttons in the table below.

| **Buttons** | **Description** |
| --- | --- |
| **Clear All** | Removes all UV channels. UV values are set to (0,0) in a new UV0 channel. |
| **Add New** | Adds a new UV channel. |
| **Delete Selected** | Removes the selected UV channel. If you remove a channel in the center, the next channel takes its place. |
| **Duplicate Selected** | Copies the selected UV channel. A new channel is created and added to the end of the list. You can confirm and visualize your channels in the [UV Editor](/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine). |

### Lightmap UVs

A lightmap (used in baked lighting for rendering) associates lighting information with the UV coordinates on meshes. Lightmap UVs have stricter requirements on UV islands than regular textures. When you generate lightmap UVs, the (source) UV islands are repacked to meet the lightmap requirements. To learn more about lightmap UVs, see [Understanding Lightmapping](/documentation/en-us/unreal-engine/understanding-lightmapping-in-unreal-engine).

The **Lightmap UVs** section consists of action buttons to enable or disable the generation of lightmap UVs for a static mesh. In addition, you can view which UV channel is set as the source and which stores the repacked UVs (destination).

Only static meshes support lightmaps. The section doesn't show up as an option for dynamic meshes.

| **Buttons** | **Description** |
| --- | --- |
| **Enable** | Sets **Generate Lightmap UVs** to true. UVs are repacked based on the **Source** and **Dest Channel** to create a lightmap. |
| **Disable** | Sets **Generate Lightmap UVs** to false. |
| **Reset** | Resets **Source Channel** to 0 and **Dest Channel** to the max UV channel plus one. For example, if the last UV channel in the **UVLayer** dropdown is UV2, then the **Dest Channel** is set to UV3. |

| **Lightmap UV Properties** | **Description** |
| --- | --- |
| **Generate Lightmap UVs** | 
Shows whether lightmap UVs are enabled in the **Build Settings** of the **Static Mesh Editor**. To change the value, use the action buttons above or the **Static Mesh Editor**.

If the **Static Mesh Editor** is open when you click **Enable** and complete the tool changes, you won't see the editor update. You must close and reopen the editor.



 |
| **Source Channel** | Shows the source UV channel used to compute lightmap UVs. To change this value, use the **Static Mesh Editor**. |
| **Dest (Destination) Channel** | Shows which channel lightmap UVs are stored in. By default, the value is set to the current number of channels plus one. You can use the UVs section to add channels to increase this value and the **Static Mesh Editor** to set a specific channel. |

### New Attribute

The **New Attribute** section contains settings for creating new attribute layers for the selected mesh. You can use attribute layers to mark specific surface areas for mesh editing or store arbitrary data.

Before making a new layer, you must set the name in the **New Attribute Name** field and click one of the layer options below.

| **Attribute Layer** | **Description** |
| --- | --- |
| **Add Weight Map Layer** | 
Adds a new per-vertex weight map layer with the given name. The new layer is created in the **Vertex Attributes** field of the **Attributes Inspector** section.

You can use the layer in various tools, such as:

-   [Smooth](/documentation/en-us/unreal-engine/smooth-tool-in-unreal-engine)
    
-   [Displace](/documentation/en-us/unreal-engine/displace-tool-in-unreal-engine)
    
-   [Offset](/documentation/en-us/unreal-engine/offset-tool-in-unreal-engine)
    
-   [Paint Vertex Colors](/documentation/404)
    
-   [Paint Maps](/documentation/en-us/unreal-engine/paint-maps-tool-in-unreal-engine)
    



 |
| **Add PolyGroup Layer** | 

Adds a new PolyGroup layer with the given name. The new layer is created in the **Triangle Attributes** field of the **Attributes Inspector** section.

You can use the layer in various tools, such as:

-   [Paint PolyGroups](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#attribs)
    
-   [Edit Materials](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#attribs)
    
-   [UV Unwrap](/documentation/en-us/unreal-engine/uvs-category-in-unreal-engine#unwrap)
    
-   [Edit Normals](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#attribs)
    

For more information on PolyGroups, see [Understanding PolyGroups](/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine).



 |

### Modify Attribute

The **Modify Attribute** section contains the option to remove attribute layers.

To remove a layer, select the respective name in the **Attribute** dropdown, then click **Delete Selected**.

### Attributes Inspector

The **Attributes Inspector** acts as a visualizer for attributes currently attached to the mesh. You can use the inspector to confirm that the attribute layers you created or deleted appear appropriately or as a debugger. For example, if you're using [Geometry Scripting](/documentation/en-us/unreal-engine/introduction-to-geometry-scripting-in-unreal-engine) to store temporary data in a mesh but the data does not appear as expected, you can use the inspector to confirm the layer is created and its name. You can check the attributes of the following:

-   Vertex
-   Instance
-   Triangle
-   Polygon
-   Edge
-   Group

To exit the tool, click **Complete** in the [Tool Confirmation](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine) panel.

Changes made in the Edit Attributes tool are automatically applied to the mesh. If you use **ESC** to exit the tool, any updates made during the tool are still applied. To remove changes, click **Edit > Undo History** in the menu bar or **Ctrl + Z**.

### Hotkeys

| **Hotkey** | **Description** |
| --- | --- |
| **F** | Zooms into the location of the mesh. |
| **Enter or ESC** | Exits the tool. |
# Primitive Debugger

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/primitive-debugger-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/primitive-debugger-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:16

---

The **Primitive Debugger** is a runtime-only tool used to view information about primitives being rendered in the game client such as draw calls and LOD information.

## Using the Primitive Debugger

To launch the Primitive Debugger:

1.  Run a **Development** or **Test** client.
2.  Open the console with backtick key and enter the command `PrimitiveDebugger.Open`.
3.  The **Primitive Debugger** window will appear and be populated by a list of primitives that were being rendered at the time the window was open.
4.  To refresh the list of displayed primitives, press the **Refresh** button.
    
    Primitives that are destroyed during gameplay will be automatically removed from the list.
    

## Features of the Primitive Debugger

### List and Detail Views

Within the Primitive Debugger, you can filter the primitive list shown to you by using the search bar at the top. The search bar supports filtering the following properties by name:

-   Primitive name
-   Actor name
-   Component name
-   Actor class
-   Component class
-   Material name
-   Texture name

You can toggle visibility of each listed primitive as well as pin them to the top of the list for quick access. Scrolling the list shows the name of the actor for each primitive. When you select a table row opens up a Details panel with additional properties for the selected primitive.

This includes the following:

-   Triangle count (non-nanite meshes)
-   Location in world space
-   Current LOD (non-nanite meshes)
-   Total available LODs (non-nanite meshes)
-   Nanite support and usage
-   Materials
-   Textures used
-   Draw calls
-   Component and Actor type
-   Component and Actor name
-   Skeletal mesh bone count

![Details Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b310754e-53a3-49cb-a154-c45fc6a7476e/rpd-1.png)

Details Panel

### Debugging Controls and Visualizations

The Details panel provides some basic debugging tools depending on the configuration of the current build. A slider is available for all non-Nanite meshes to force a specific level of detail (LOD) for the primitive, updating the model shown in game.

Nanite meshes have an option to force disable Nanite rendering for them, causing the game to instead render a normal static mesh in its place. This option is useful for checking differences between Nanite and non-Nanite material variations, or checking for other visual inconsistencies and performance impacts.

In Development builds, skeletal meshes can display a debug visualization of the bones in its skeleton, updated in real time similar to what can be seen in the editor. This can be helpful to spot animation or rigging errors. Development builds also support displaying a debug bounding box around any primitive in the level, which will also be updated in real time. These bounds are different from the collider, and will represent the maximum extents of the primitive in 3D space.

|   |   |
| --- | --- |
| 
 | 

 |
| Debug visualization of skeleton. | Debug bounds visualization. |

Click images for full size.

Once you’re finished using the debug visualizations and using the tool, you can close the window to automatically undo any of the changes that have been made.

### Saving a Snapshot

The contents of the primitive list, including the details of each primitive, can be saved to the disk for later reference by using the **Save to CSV** option located in the top right of the window. This will dump all primitives recorded in the current snapshot, including those hidden by the search filter, to a csv file which can be found in the project’s **Saved/Profiling/Primitives/** folder in a timestamped **PrimitivesDetailed.csv** file. Alternatively, this action can be performed from the command line by using the command **DumpDetailedPrimitives** from the in-game command line.

## Limitations and Future Changes

These are some known limitations of the Primitive Debugger:

-   Debug visualizations are only available in Development configurations.
-   This tool is not supported in the editor and is designed to be used only in a built client binary.
-   Non-mesh primitives such as Niagara emitters currently have limited support.
-   The displayed draw call information may not provide the complete picture for instanced meshes. Currently the draw calls are computed as if the mesh exists by itself without batching.
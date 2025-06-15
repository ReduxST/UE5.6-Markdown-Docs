# How Datasmith Translates 3ds Max Content

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:31

---

When **Datasmith** translates scenes from **Autodesk 3ds Max** into **Unreal Editor**, it follows the process outlined in [Datasmith Overview](/documentation/en-us/unreal-engine/datasmith-plugins-overview) and [Datasmith Import Process](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine), but adds some special translation behavior that is specific to 3ds Max.

Read this page to better understand how the Datasmith exporter translates your scene, and how to work with the results in Unreal Editor.

## Geometry

This section describes how Datasmith converts geometric objects in a 3ds Max scene into **Static Mesh Assets** and **Actors** in an Unreal Engine Project.

### Meshes and Tessellation

In most cases, Datasmith uses each 3ds Max object's render mesh to create the geometry for the corresponding Static Mesh Asset in Unreal Engine. Assets in Unreal Engine usually have exactly the same triangles that you see in 3ds Max renderings.

For 3ds Max Body Objects (see [Body Objects Category](https://knowledge.autodesk.com/support/3ds-max/learn-explore/caas/CloudHelp/cloudhelp/2023/ENU/3DSMax-Data-Exchange/files/GUID-ABED9F9A-1CBD-4FBE-9893-4E12F03617F5-htm.html) in the 3ds Max documentation), Datasmith bases the geometry of the Static Mesh Asset on the 3ds Max viewport mesh instead of the render mesh.

You can control the granularity of the tessellation that 3ds Max uses to render in a viewport:

-   In the **Viewport Display Settings** rollout, set **Mesh Quality Presets** to **Coarse**, **Medium**, or **Fine**.

Datasmith respects the level of tessellation you set for each Body Object in the scene.

For more information about the Mesh Quality Presets setting, see [Viewport Display Settings Rollout](https://knowledge.autodesk.com/support/3ds-max/learn-explore/caas/CloudHelp/cloudhelp/2023/ENU/3DSMax-Data-Exchange/files/GUID-045AD5C8-8F2F-48E3-8060-8371DA83DCAC-htm.html) in the 3ds Max documentation

### Instances

When Datasmith detects multiple instances of the same master object in your 3ds Max scene, it creates one Static Mesh Asset for that object, and places multiple instances of that Static Mesh into the **Level** in Unreal Engine.

We recommend using instances in 3ds Max for repeating elements in your scene, such as windows, doors, or chairs. Instances are usually better for an Unreal Engine project's runtime memory requirements and performance. It also helps you manage content by reducing the number of Static Meshes.

For more information about instances, see [Creating Copies, Instances, and References](https://knowledge.autodesk.com/support/3ds-max/getting-started/caas/CloudHelp/cloudhelp/2022/ENU/3DSMax-Basics/files/GUID-9F0E9AC3-FAE6-46A6-83F3-591084220B12-htm.html) in the 3ds Max documentation.

### Pivot Points

In 3ds Max, you can set a custom pivot point for each object in your scene, even when those objects are instances of the same master object. In Unreal Engine, all instances of the same geometry need to use the same pivot point.

If object instances in your 3ds Max scene have custom pivot points, Datasmith tries to replicate the custom pivot points. How Datasmith translates pivot points depends on whether or not all of the instances in 3ds Max use the same pivot point.

Datasmith does not support importing instances that have both different pivot points and a non-uniform scale in 3ds Max. If you have instances like this, use the [Reset XForm Utility](http://help.autodesk.com/view/3DSMAX/2018/ENU/?guid=GUID-B98414B9-4F28-45F4-A1F4-9DA994548ED9) on them before you export.

#### Translating a Single Shared Pivot Point

If all instances in 3ds Max have the same custom pivot point, Datasmith sets it as the pivot location for the Static Mesh Asset it creates. When you rotate any Static Mesh Actor that Datasmith creates for this object in the Unreal Engine Level, it rotates around the location of that custom pivot as expected.

#### Translating Multiple Custom Pivot Points

If one or more instances use a different pivot location from the others, Datasmith does the following.

-   Sets the Static Mesh Asset it creates in Unreal to use the default pivot location of the 3ds Max object.
-   When it places the Asset in the Unreal Engine Level, Datasmith creates a new, empty parent Actor at the location of the custom pivot for that instance instead of creating a Static Mesh Actor.
-   Finally, Datasmith gives the parent Actor a **Static Mesh Component** that:
    -   References the Static Mesh Asset.
    -   Has a translation offset from the parent Actor that places it where it needs to be in the 3D scene.
    -   Has a `_pivot` suffix appended to its name.

When you move, rotate and scale the parent Actor in the Unreal Engine Level, the model behaves as you expect. All you need to note is that the model is a Component of the parent Actor, rather than being a Static Mesh Actor itself.

#### Custom Pivot Point Example

For example, in the following image, the teapot on the right uses the default pivot point, while the teapot on the left has a custom pivot at the top of its lid.

Click image to expand.

When Datasmith brings the scene into Unreal, it creates a Static Mesh Actor for the teapot on the right. For the teapot on the left, it does the following:

-   Creates a new Actor called `Teapot002`, at the location of that pivot point in the 3D world.
-   Gives the `Teapot002` Actor a Static Mesh Component named `Teapot002_2`, which refers to the Static Mesh asset for the teapot.
-   Offsets `Teapot002_2` from its parent Actor, `Teapot002`, by exactly the right amount to position it correctly, relative to the other geometry in the scene.

Click image to expand.

### UV Channels

Datasmith ensures that every Static Mesh it brings into Unreal Engine has a set of UVs that **Lightmass** can use to build static lighting into lightmap textures (see [Global Illumination](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine)). When you synchronize a 3ds Max scene or import a Datasmith file, Unreal Engine creates that UV channel automatically. Every Static Mesh Asset uses the new channel for baking lightmaps.

You can also create custom lightmap UVs in 3ds Max, and use those instead. In that case, it's important to understand how Datasmith brings UVs into Unreal from 3ds Max, and how you can override that behavior.

-   The next section describes how Datasmith imports UVs from 3ds Max.
-   The following section, [Use Custom Lightmap UVs](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine#usecustomlightmapuvs), explains how to override Datasmith's default import behavior.

#### How Datasmith Imports UV Channels

Unreal Engine supports up to eight UV channels per Static Mesh. Datasmith uses two of them to generate lightmap UVs. That means Datasmith can preserve up to six pre-existing UV channels for each object that it imports from 3ds Max. In 3ds Max, an object can have up to 99 UV channels, and you don't have to set channel indexes sequentially. Datasmith exports the six channels with the lowest indexes.

When Datasmith imports UV channels, it does the following:

-   Resets the UV channel indexes to begin at 0
-   Maps the lowest index in 3ds Max to the lowest index in Unreal, second lowest to second lowest, and so on.
-   Creates two additional channels for auto-generated lightmaps

For example, the table below shows how Datasmith reindexes UV channels when it imports a 3ds Max object with five channels whose indexes are not fully sequential. Notice that:

-   In addition to channels 0-4, Datasmith adds channels 5 and 6 for lightmaps.
-   While there are large gaps between some of the 3ds Max UV indexes, Datasmith remaps each index to the lowest available slot in Unreal Engine.

| 3DS Max UV Channel | Unreal UV Channel | Notes |
| --- | --- | --- |
| 1 | 0 |   |
| 2 | 1 |   |
| 3 | 2 |   |
| 10 | 3 |   |
| 99 | 4 |   |
|   | 5 | Generated during import to create an automatic unwrap of the geometry contained in the Datasmith scene. It is the basis for the lightmap UV generation used by UV channel 6. |
|   | 6 | Generated based on UV channel 5 to correctly pad and pack the UV charts based on the Datasmith Import Options used for the Static Mesh Lightmap Resolution values. |

#### Use Custom Lightmap UVs

If you want imported Static Meshes to use pre-existing UV channels that you created in 3ds Max, you have two options.

-   **Option 1**: Before you export your scene from 3ds Max, apply a Datasmith Attributes Modifier to specify the index of the UV channel you want Unreal Engine to use for lightmaps. For details, see [Per-Object Conversion Settings](/documentation/en-us/unreal-engine/datasmith-per-object-conversion-settings-for-exporting-to-unreal-engine).
    
-   **Option 2**: After you import your scene into Unreal Editor, you can change the index of the UV channel you want Unreal Engine to use for lightmaps.
    
    1.  In the Content Browser, double-click the Static Mesh Asset whose lightmap UV index you want to change.The Static Mesh Editor opens.
    2.  In the Details panel, navigate to **General Settings > Advanced**, and set **Light Map Coordinate Index** to the UV channel you want to use.

Alternatively, you can change the lightmap UV index in Python. Call the following function:

`static_mesh.set_editor_property("light_map_coordinate_index", index)`

### Custom Collision Shapes

To improve the behavior and performance of the physics simulation in Unreal Engine, you can model custom geometry for an object in 3ds Max, and use it as the collision mesh for the corresponding Static Mesh in Unreal Engine. The idea is to make the custom geometry match the volume of the original scene object as closely as possible, but minimize the number of triangles it contains.

-   The next section, [Considerations for Using Custom Collision Shapes](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine#considerationsforusingcustomcollisionshapes) explains what you need to consider when you use custom collision shapes.
-   The following section, [Set up Custom Collision Shapes](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine#setupcustomcollisionshapes), describes how to set up custom collision shapes.

#### Considerations for Using Custom Collision Shapes

##### Shape Type

When you use custom collision shapes, the object that you set as a collision mesh can be any completely closed, convex 3D shape. For example, a box. The following diagram illustrates what kinds of shapes are and aren't acceptable.

![Convex and non-convex examples](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bfba923f-dcab-4dae-a878-c49e808a4257/convex-resize334x269.gif "Convex and non-convex examples")

##### Pivot Point Location

Also make sure that the pivot point of your custom geometry is at the same location relative to its volume as the pivot point of the original object. For example, in the following image, both the chairs on the right, and the simplified representation on the left have pivot points in the bottom center of their volumes.

![Pivot points on custom collision volumes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da1339df-3816-4f89-bb4a-07e65ef3e9dc/collision-pivots.png "Pivot points on custom collision volumes")

If you don't keep the pivot point of your collision geometry at the same place relative to the overall volume, the representation of your object in the physics world won't align with the visible extents of the object. This can cause collisions to happen where you are not expecting them.

#### Set up Custom Collision Shapes

To set up custom collision shapes in 3ds Max so that Datasmith imports them into Unreal engine, use a Datasmith Attributes Modifier. In 3ds Max, assign the Modifier to one or more objects in your scene, then use it to specify the object you want Unreal Engine to use as a collision mesh. For details, see *Set a Custom Collision Volume* in [Per-Object Conversion Settings](/documentation/en-us/unreal-engine/datasmith-per-object-conversion-settings-for-exporting-to-unreal-engine).

#### Verify Custom Collision Shapes in Unreal Engine

To verify that Datasmith imported custom collision shapes correctly, turn on collision rendering in the **Level Viewport**.

-   From the Viewport overlay menu, select **Show > Collision**.

Unreal Engine renders the custom collision volumes on top of your scene objects. The following image shows a sphere that uses a box object as its custom collision volume.

Click for full image.

### Vertex Colors

When you associate vertex colors with your 3ds Max objects, Datasmith preserves them when it creates corresponding Static Mesh Assets in the Unreal Engine.

Datasmith does not translate data from other 3ds Max mesh channels, such as **Vertex Alpha**, **Map Channel Color**, or **Soft Selection Color**.

You can use these vertex colors when you create a custom **Material** in Unreal Editor by including the **Constants > Vertex Color** node in your Material Graph.

For example, the following images show an object in 3ds Max that is set to display its vertex colors, and a simple custom Material in Unreal Engine that retrieves the vertex colors and passes them directly into the **Base Color** output.

Vertex colors displayed in 3ds Max. Click image to expand.

Vertex colors displayed in Unreal Engine. Click image to expand.

#### Verifying Imported Vertex Colors

You can visualize your vertex colors in Unreal Engine to make sure that Datasmith translated them correctly.

-   In the **Content Browser**, double-click a **Static Mesh Asset** to open it in the **Static Mesh Editor**.
-   From the **Viewport** toolbar, select **Show > Vert Colors**.

#### Other Uses for Imported Vertex Colors

Vertex colors in a custom **Material Graph** can do more than just provide the visible color for a surface. You can also combine and blend them with other surface properties.

Alternatively, you can use vertex colors to associate custom data values with the geometry of your source objects, and pass those values to custom Materials in Unreal Editor to drive visual effects.

For example, you could use vertex colors to assign weights to the branches and leaves of a tree, and use those weights to modulate the effect of a wind animation effect that you apply in a vertex shader.

### Levels of Detail

Datasmith does not import custom **Levels of Detail** that you set up in 3ds Max. You can generate new Levels of Detail automatically in Unreal Editor. For details, see [Automatic LOD Generation](/documentation/en-us/unreal-engine/static-mesh-automatic-lod-generation-in-unreal-engine), or [Creating Levels of Detail in Blueprints or Python](/documentation/en-us/unreal-engine/creating-levels-of-detail-in-blueprints-and-python-in-unreal-engine).

### Forest Pack and RailClone Objects

[iToo Software](https://www.itoosoft.com/)'s [Forest Pack](https://www.itoosoft.com/forestpack) and [RailClone](https://www.itoosoft.com/railclone) are plugins for 3ds Max that scatter, or place large numbers of geometric objects procedurally to help you populate scenes.

#### How Datasmith Translates ForestPack and Railclone Objects

When you use Datasmith to import or sync a 3ds Max scene that contains a Forest Pack or RailClone object in Unreal Engine, Datasmith creates a single Actor in the Unreal Engine Level, and names it according to the name of the object in 3ds Max.

Within the Actor, Datasmith creates the following for each type of geometry that the object handles:

-   A Hierarchical Instanced Static Mesh (HISM) Component.
-   A Static Mesh Asset in your Project content.

Datasmith then sets each geometry type's HISM Component to refer to its Static Mesh Asset.

Within each HISM Component, Datasmith adds one instance of the Static Mesh asset for each instance that's visible in the 3ds Max scene, and matches the position and rotation of each instance in 3ds Max.

This import process produces an Unreal Engine Level that closely matches the original 3ds Max scene visually and structurally, meaning that in the scene hierarchy, one Forest Pack or RailClone object internally manages all its instances.

![Forest Pack in 3ds Max](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c0ee76d-479e-4b8e-878b-542441cacae3/datasmith-max-forestpack-before.png)

![Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91e6b30f-6a9e-4fd5-a232-ae6604f5cbdf/datasmith-max-forestpack-after.png)

The HISM Component is the same technology used in Unreal Engine's **Foliage** system. It's a very efficient way to render many instances of the same Static Mesh. The Unreal Engine renderer batches all instances managed by the same HISM Component, and makes a single draw call per Material assigned to the Static Mesh Asset. By using the HISM, the renderer can handle more instances without affecting GPU performance or frame rate.

#### Replace Forest Pack and RailClone Objects with Simplified Geometry

You might want to use Forest Pack or RailClone to manage objects with complex geometry, such as trees, that you intend to replace in Unreal Engine with simpler geometry that performs more efficiently in real time.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cae618ff-e14a-4711-8dcd-92a7e300e41d/datasmith-max-forestpack-bbox.png "datasmith-max-forestpack-bbox.png")

To replace a Forest Pack or RailClone object with simplified geometry:

1.  Apply a **Datasmith Attributes Modifier** to the Forest Pack or RailClone object in 3ds Max, and set it to export only the bounding box of the geometry. For instructions, see the Export the *Bounding Box Only* section of [Per-Object Conversion Settings](/documentation/en-us/unreal-engine/datasmith-per-object-conversion-settings-for-exporting-to-unreal-engine).
2.  Sync or import the 3ds Max scene.
3.  To update all instances in the Unreal Engine Level to use a new Static Mesh, edit the HISM Component, and, in the **Details** panel, change the **Static Mesh** setting.

### XRef Scenes

XRef scenes are externally-referenced scenes that appear in your current file, but are loaded temporarily from other MAX files. For more information, see [XRef Scene](https://knowledge.autodesk.com/support/3ds-max/getting-started/caas/CloudHelp/cloudhelp/2023/ENU/3DSMax-Manage-Scenes/files/GUID-5DB41A62-D7A5-4D54-AC83-5D03C9F7DB11-htm.html?us_oa=akn-us&us_si=9d8783af-02e1-4f82-be05-9f5d61f67e42&us_st=xref%20scene) in the 3ds Max documentation. If your scene references one or more XRef Scenes, Datasmith exports them by default.

To prevent Datasmith from exporting XRef Scenes:

From the **Datasmith** tab of the 3ds Max ribbon, go to the **Settings** panel, and disable **Export XRef Scenes**.

## Lighting and Rendering Environment

3ds Max offers much more detailed and sophisticated lighting and rendering features than many of the other third-party applications that Datasmith supports. This section describes how Datasmith tries to bring 3ds Max lighting and rendering data into Unreal Engine.

### Lights

Datasmith translates a variety of 3ds Max light types, including Standard, Photometric, V-Ray, and Corona lights. For each light, Datasmith brings the following light information into Unreal:

-   Position, orientation, shape and size in 3D space.
-   Light type (for example, point light or spot light).
-   Intensity, units, lamp color, temperature, and filter color.
-   Render shape visibility.
-   IES light profiles.

![3ds Max](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/920d47a0-3299-41b7-a80a-c0f04555d2a9/3ds_lightcharacteristics.png)

![Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/964449a5-aff1-4191-af38-95245ae3f864/ue4_lightcharacteristics.png)

Point lights with IES profiles and scaled Kelvin temperatures. Middle: Point lights with IES profiles and scaled light intensity. Bottom: Spot lights with filter color.

Datasmith tries to approximate the lighting you set up in 3ds Max as closely as possible, but you'll probably have to adjust your Level's lighting after you import a scene into Unreal Engine to make the results look the way you expect, and to optimize lighting performance at runtime. Usually you tweak the Level's lighting by adjusting the post-processing exposure value.

A few notable differences between 3ds Max and Unreal Engine when you use Datasmith:

-   Unreal Engine currently does not support instances for lights. For each instanced light in your 3ds Max scene, Datasmith creates a separate **Light Actor** in your Unreal Engine Level.
    
    Although lights are not instanced in Unreal Engine, you can still edit all of them at once by selecting them and changing their properties in the Detail Panel.
    
-   Standard lights in 3ds Max are unitless, and they allow custom attenuation parameters that Unreal Engine does not support.
-   Some V-Ray shapes are not supported, such as Vertical Cylinder, Spheroid, and Custom Mesh lights.
-   Area lights are handled using a special Blueprint class. For details, see [Datasmith Import Process](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine).

### Exposure

Datasmith preserves the intensity of 3ds Max lights, but intensity is not enough to ensure that the scene renders well. The Unreal Engine renderer needs a context to interpret light intensity in, so it can determine the luminance of the scene: how bright or dark the scene should appear in the final rendering.

Part of the context comes from the exposure of the camera or view — a set of physical characteristics that govern how sensitive the final image should be to the intensity of light in the scene.

Datasmith also translates several exposure values from 3ds Max.

See the following sections for details:

-   [Physical Camera Exposure Settings](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine#physicalcameraexposuresettings)
-   [Global Exposure Settings](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine#globalexposuresettings)
-   [Auto-Exposure](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine#auto-exposure)

#### Physical Camera Exposure Settings

If your 3ds Max scene contains a Physical Camera, Datasmith preserves its exposure and white balance settings and carries them over to the corresponding Cine Camera Actor the Unreal Engine Level.

For each camera, Datasmith sets the following settings in Unreal Engine to match their equivalents in 3ds Max.

-   **WhiteBalance > Temp**
-   **Shutter Speed**
-   **ISO**
-   **Aperture (f-stop)**

It also sets the **Exposure > Metering Mode** to **Manual**, which disables auto-exposure.

When you view your Level through the camera, you'll see light levels that closely match the rendered results in 3ds Max.

![3ds Max Physical Camera](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3ead120-d46e-4f77-ae3b-99d797cb0362/datasmith-max-exposure-camera.png)

![Unreal Engine CineCameraActor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/677d76e7-fa20-4fab-bbe7-924be54b856d/datasmith-ue4-exposure-camera.png)

For more information about Cine Camera Actor settings see [Cine Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine).

#### Global Exposure Settings

If your **Exposure Control** setting in 3ds Max uses either the **Physical Camera Exposure Control** or **VRay Exposure Control**, Datasmith creates a **Post Process Volume** in the Datasmith Scene that applies those global exposure settings to the whole Unreal Engine Level.

In 3ds Max, the exposure settings are in the Environment and Effects dialog. From the main menu, select **Rendering > Exposure Control...**

Datasmith sets the following settings for the Post Process Volume in Unreal Engine to match their equivalents in 3ds Max.

-   **WhiteBalance > Temp**
-   **Shutter Speed**
-   **ISO**
-   **Aperture (f-stop)**

It also sets the **Exposure > Metering Mode** to **Manual**, which disables auto-exposure.

When you view your Level using the default perspective camera in the Unreal Editor Viewport, you'll see light intensities that closely match the rendered result from 3ds Max.

![Global exposure in|3ds Max perspective camera](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48d340d6-4d02-4479-80ec-e9c74ec63186/datasmith-max-exposure-global.png)

![Post Process Volume|exposure in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4dcdf204-e3b8-4ad0-8b21-d2a098618843/datasmith-ue4-exposure-global.png)

##### Global Exposure Setting vs. Physical Camera Settings

In 3ds Max, the global white balance and exposure settings do not have to match the settings assigned to Physical Cameras. If this is the case, and you render the scene from the point of view of a perspective camera, the renderer uses your global exposure settings rather than the settings assigned to any specific Physical Camera.

The same thing happens in Unreal Engine. When you view the scene through the default camera in the Level Viewport, Unreal Engine uses exposure settings that are either global to the Project or come from the active post processing volume. When you view the scene through any Cine Camera Actor, Unreal Engine uses that camera's exposure settings.

#### Auto-Exposure

Unreal Engine has a built-in auto-exposure system. It monitors the amount of light that reaches the camera, and automatically adjusts the exposure so the final image appears at a reasonable level of luminance.

The auto-exposure system is active by default. For more information about auto-exposure in Unreal Engine see [Auto Exposure](/documentation/en-us/unreal-engine/auto-exposure-in-unreal-engine).

### Cameras

For every camera in your 3ds Max scene, Datasmith creates a Cine Camera Actor in Unreal Engine, at the same position and rotation in 3D space, and tries to preserve the camera's focal properties as much as possible. Ideally, viewing the Level through a camera in Unreal Engine is as similar as possible to viewing the scene rendered from the corresponding camera in 3ds Max.

If a camera in 3ds Max has a target, Datasmith sets the Cine Camera Actor to track the corresponding Actor in Unreal Engine. When you move the target Actor around in the Unreal Engine Level, the Cine Camera Actor automatically rotates to track the target Actor.

For more information about how Datasmith translates exposure settings for physical cameras, see [Physical Camera Exposure Settings](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine#physicalcameraexposuresettings).

### Materials

When Datasmith imports a 3ds Max scene into Unreal Engine, it creates one or more parent Material Assets in the project's **Materials / Master** folder. For each parent Material, it tries to create a Material Graph that uses Unreal Engine's physically-based renderer to produce results that are equivalent to what you see when you render the scene in 3ds Max.

Datasmith imports each material in your 3ds Max scene as a new instance of a parent Material. Not every Material Instance has its own parent. If two different Material Instances can share the same Material Graph, Datasmith attempts to use the same parent Material for both instances.

Datasmith can usually translate 3ds Max Materials with a single shading model and a relatively simple graph well. For example, the material in the following image.

![Simple material in 3ds Max](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e662eb38-2656-4275-99cc-0683e2d22662/3ds_simplematerial-resize526x484.png "Simple material in 3ds Max")

Even for simple materials, a parent Material Asset's graph often looks different from the corresponding material in 3ds Max. When Datasmith converts between shading models, it attempts to preserve the visual result as closely as possible, even if that means adding connections or constants to the graph.

#### Shading Model Conversion Limitations

3ds Max supports several other shading models for materials, such as V-Ray, Corona, Mental Ray, and more. Each shading model is a separate piece of software, with unique features that are not always consistent with one another. Datasmith can convert some features into similar features in Unreal Engine, but might not be able to handle some of the more complex or special-purpose ones.

For example, materials with complex graphs that mix multiple output shaders together might be difficult or impossible for Datasmith to reproduce in Unreal Engine. You need to do some extra work after importing the scene to adjust or replace them. The graph in the following image is a good example.

### Procedural Textures

If your 3ds Max scene uses procedural textures, Datasmith exports them as baked textures that it uses in the Unreal Engine Materials it creates. Datasmith saves these baked textures as .tga files. For more information about hoe Datasmith creates materials, see [Materials](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine#materials).

Both the number and the size of the textures in the scene affect how long it takes to export from 3ds Max and import into Unreal Engine. You can limit the resolution of baked and procedural textures to improve import export performance. This is especially useful for large scenes with complex materials.

This setting does not affect the size of raster textures, for example TIFF or JPEG files.

To specify the export resolution for baking procedural textures:

-   From the **Datasmith** tab of the 3ds Max ribbon, go to the **Settings** tab, and set **Limit Texture Resolution** to the desired value.

Values specify the number of pixels in the target resolution, and range from 4K (4096 pixels) to 16M (16 megapixels).

For example, if you set the resolution limit to 4K, Datasmith limits textures to resolutions that contain 4096 pixels, whether that's 64x64, 128x32px, or another set of width/height values.

## Metadata

Add your metadata to your 3ds Max objects on the **User Defined** tab of the **Object Properties** window.

![Metadata in 3ds Max User Defined Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53a82896-50aa-4e77-93d7-9411783a7375/3ds_max_user_defined_properties.png "Metadata in 3ds Max User Defined Properties")

To get to this panel for a mesh in 3ds Max:

1.  Select the mesh in the outliner or the viewport.
2.  Right-click and choose either **Properties** or **Object Properties** from the context menu, or select **Edit > Properties** from the main menu.
3.  Enter your metadata into this panel as `key = value` pairs, as shown above.
    
    **Be certain to leave a space on both sides of the equal (=) sign**. If you don't, Datasmith won't recognize your metadata, and won't import it as expected.
    

You can also set up user-defined properties [using MAXScript](https://help.autodesk.com/view/3DSMAX/2018/ENU/?guid=__files_GUID_AF1F51D4_449B_4C4D_9F58_85DB145BC0B9_htm).

If your model was originally created in Revit and then imported into 3ds Max, the user-defined properties should already be preset by the 3ds Max importer with the model's BIM information.

## Conversion Notes and Warnings

You can get information about the Datasmith conversion process:

-   In 3ds Max, after you export or synchronize a scene.
-   In Unreal Engine, after you synchronize or import a scene.

### Notes and Warnings in 3ds Max

After Datasmith exports your 3ds Max scene, it lists statistics, notes, problems, warnings or errors that it encountered during the process in the Messages Window (see [The Datasmith Messages Window](/documentation/en-us/unreal-engine/the-datasmith-3ds-max-ui-for-exporting-to-unreal-engine#thedatasmithmessageswindow)).

If you use Direct Link to synchronize 3ds Max and Unreal Engine, Datasmith does not output statistics by default. To enable export statistics for Direct Link Sync and AutoSync, enter the following command in the MaxScript console window:

`Datasmith_SetExportOption_StatSync true`

Messages notify you about elements in your scene that might not translate to Unreal Engine exactly as you expect. For example:

-   Problems with your source scene, such as missing images. You might want to fix these problems in 3ds Max before you export again.
-   Things in your 3ds Max scene that either Datasmith or the Unreal Engine doesn't support.
-   Things that Datasmith converted in a way you might not be expecting.

### Notes and Warnings in Unreal Engine

After you import your Datasmith scene into the Unreal Editor, you can find information about conversion issues you might need to clean up in the **Output Log** (from the main menu, select **Window > Output Log**).

As a starting point, try filtering the Output Log to show only warnings. From the Output Log toolbar, disable **Filters > Messages**, and **Filters > Errors**.
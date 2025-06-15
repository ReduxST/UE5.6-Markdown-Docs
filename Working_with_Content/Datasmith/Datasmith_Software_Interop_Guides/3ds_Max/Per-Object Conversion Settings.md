# Per-Object Conversion Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-per-object-conversion-settings-for-exporting-to-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-per-object-conversion-settings-for-exporting-to-unreal-engine)  
**Processed:** 2025-06-14 16:18:55

---

Apply a **Datasmith Attributes** modifier to objects in a **3ds Max** scene to customize the way **Datasmith** translates individual scene objects from 3ds Max to **Unreal Engine**.

You can:

-   Specify the index for the UV channel that you want to use for lightmaps you create in Unreal Engine. See Specify a Lightmap UV Index.
-   Assign custom collision geometry for objects in your scene. See Set a Custom Collision Volume.
-   Export objects as simplified bounding boxes, instead of their full geometry. See Export the Bounding Box Only.

## Apply a Datasmith Attributes Modifier

In 3ds Max, you apply a Datasmith Attributes modifier from the ribbon, or the **Modify** panel.

By default, the modifier does not change the export behavior described in [How Datasmith Translates 3ds Max Content](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine). To customize that default behavior, you need to change the modifier's settings.

### From the 3ds Max Ribbon

The easiest way to apply a Datasmith Attributes modifier to objects in your 3ds Max scene is from the 3ds Max ribbon.

1.  Select the object or objects whose export settings you want to customize.
2.  On the **Datasmith** Tab, of the 3ds Max Ribbon, select **Add Datasmith Attributes Modifier** from the **Tools** panel.

### From the Modify Panel

You can also apply a Datasmith Attributes modifier exactly the same way as you apply any other kind of modifier in 3ds Max. For more information, see [Modifiers](http://help.autodesk.com/view/3DSMAX/2019/ENU/?guid=GUID-79998C44-22AA-4485-9608-51630079E5A7) in the 3ds Max documentation.

1.  Select the object or objects whose export settings you want to customize.
2.  Open the **Modify** panel.
3.  From the Modifier List drop-down menu, find and select **OBJECT-SPACE MODIFIERS > Datasmith Attributes**.

## Specify a Lightmap UV Index

By default, Datasmith creates two new UV channels for each geometric object in your scene (see *UV Channels* in [How Datasmith Translates 3ds Max Content](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine)). One channel is a lightmap UV, which stores precomputed lighting, and ensures every object is compatible with **Static** and **Stationary** lighting in Unreal Engine.

If you've already created lightmap UVs for your objects in 3ds Max, you might want to use those instead. You can use the Datasmith Attributes modifier to make your objects use the lightmap UVs that you created in 3ds Max. In that case, Datasmith doesn't generate additional UVs when you import your scene into Unreal Engine.

To specify a lightmap UV index:

-   In 3ds Max, select the objects that you created lightmap UVs for.
-   Apply a Datasmith Attributes modifier (see [Apply a Datasmith Attributes Modifier](/documentation/en-us/unreal-engine/datasmith-per-object-conversion-settings-for-exporting-to-unreal-engine#applyadatasmithattributesmodifier)).
-   In the Datasmith Attributes modifier settings, do the following:
    -   Set **Lightmap UVs** to **Specify Lightmap Channel**.
    -   Set **Map Channel** to the index of the UV channel that you want the selected objects to use for precomputed lighting.

When you sync the scene with Unreal, or export it and import it into Unreal Engine, the objects with the Datasmith Attributes modifier applied use the Map Channel you specified. Datasmith does not create any new UV channels.

For more information about UVs in Unreal Engine, see [Using UV Channels With Static Meshes](/documentation/en-us/unreal-engine/using-uv-channels-with-static-meshes-in-unreal-engine).

### Verify the UV Index in Unreal Engine

To verify that Unreal Engine is using the correct lightmap UV index settings, do the following:

1.  In the **Content Browser**, find a **Static Mesh Asset** that corresponds to one of the objects you created lightmap UVs for in 3ds Max.
2.  Double click the Asset to open it in the **Static Mesh Editor**.
3.  In the **Details** panel, look for the **General Settings > Light Map Coordinate Index** setting. This value should correspond to the UV channel that you identified in 3ds Max.

Depending on how Datasmith re-indexes the UV channels when it imports the object into Unreal Engine, the index number shown in the **Light Map Coordinate Index** setting might not match the number you set in the Datasmith Attributes modifier.

To verify that the index refers to the UV layout that you are expecting, you can display your lightmap in the Static Mesh Editor.

-   From the Static Mesh Editor Toolbar, select **UV > \[UV INDEX NUMBER\]** where UV INDEX NUMBER is the number in the **Light Map Coordinate Index** setting.

The Static Mesh Editor displays the lightmap in the bottom left of the viewport.

## Set a Custom Collision Volume

You can use the Datasmith Attributes modifier to specify an object for Unreal Engine to use as the collision mesh for other scene objects. The collision mesh object must be fully convex, and it must have its pivot located at the same location relative to its volume as the original object. For more information, see Custom Collision Shapes in [How Datasmith Translates 3ds Max Content](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine).

To set a custom collision volume:

1.  In 3ds Max, select the objects that you want to set a custom collision mesh for.
2.  Apply a Datasmith Attributes modifier (see [Apply a Datasmith Attributes Modifier](/documentation/en-us/unreal-engine/datasmith-per-object-conversion-settings-for-exporting-to-unreal-engine#applyadatasmithattributesmodifier)).
3.  In the Datasmith Attributes modifier settings, do the following:
    -   Enable **Use Custom Collision Mesh**.
    -   Click **Pick Geometric Object**.
    -   In the 3ds Max **viewport** or **Outliner panel**, select the object that you want to act as the collision mesh.

When you sync, or re-import the scene into Unreal Editor, the object you assigned the Datasmith Attributes modifier to has a new collision volume in the shape of the collision mesh object.

## Export the Bounding Box Only

Sometimes, you might want Unreal Engine and 3ds Max to use different geometry for the same scene objects. For example, if your 3ds Max scene contains complex or very dense geometry that you use in offline rendering, you might want to use less complex versions in Unreal Engine because they perform more efficiently in real time.

You can use the Datasmith Attributes modifier to identify objects whose geometry you want to replace with simplified representations when you export the scene. Instead of exporting the full geometry, Datasmith creates lightweight geometric representations of the object based on each object's 3D bounding box.

When you sync, or import the scene into Unreal Engine, the scene objects you marked with the Datasmith Attributes modifier have their original geometry replaced by simple gray bounding volumes. They have the same names and locations as the original objects.

To export bounding box representation of selected objects.

-   In 3ds Max, select the objects for which you want to set export a bounding box representation..
-   Apply a Datasmith Attributes modifier (see [Apply a Datasmith Attributes Modifier](/documentation/en-us/unreal-engine/datasmith-per-object-conversion-settings-for-exporting-to-unreal-engine#applyadatasmithattributesmodifier).
-   In the Datasmith Attributes modifier settings, set Export Geometry As to **Bounding Geometry**.

### Bounding Box Export Example

In the images below, the windows of the 3ds Max scene have a Datasmith Attribute Modifier applied, and are set to export as bounding boxes only. When you import them into an Unreal Engine Level, they appear as simplified volumes with default Materials.

The windows in this 3ds Max scene are set to export as bounding boxes only. Click image to expand.

In Unreal Engine, the windows appear as simplified volumes with default Materials. Click image to expand.

You can use these simplified scene elements in many different ways. For example, you might want to replace the simplified objects with instances of your own custom Static Mesh Assets. Alternatively, you can hide the simplified Actors from view, but use the information they contain (for example, their placement in 3D space or the extents of their bounding boxes) for other purposes.
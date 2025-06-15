# Groom Components and Assets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/groom-components-and-assets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/groom-components-and-assets-in-unreal-engine)  
**Processed:** 2025-06-14 16:26:28

---

Traditionally, creating hair for use in real-time games and projects is done using card-based techniques, or other similar approximations. Card-based workflows use many flag sheets (or cards) to give the approximate shape and motion of a much larger number of individual hairs. Unreal Engine's groom system and tools provide a workflow for you to render hair using strand-based techniques, which significantly improves visual fidelity of simulated hair for real-time use cases.

While no standard file format currently exists for hair grooms, Unreal Engine's groom system provides a naming convention-based scheme using Alembic file types to ingest data exported from your modeling application to Unreal Engine. This convention-based naming supports multiple hair groupings within a single file, such as hair for the head, vellus hair, beard, eyelashes, and eyebrows. This groom system also uses its own hair shader and rendering system, along with dynamic physics integration driven by [Niagara](/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine).

Setting up a groom for a character in Unreal Engine requires several parts:

-   A **Groom** asset that stores the imported groom data from an Alembic file.
-   A **Groom Binding** asset that links a groom to a skeletal mesh.
-   A **Groom Component** that represents instances of groom assets.

Unreal Engine's groom system provides a minimal viable implementation of strand-based groom importing, editing, rendering, and simulation. The system does not provide a hair grooming solution, like being able to shape hair. This should be done in applications like Maya with [XGen](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2015/ENU/Maya/files/GUID-47644337-40F0-4766-BD3B-4104F9F9B7E2-htm.html), [Ornatrix](https://ephere.com/plugins/autodesk/max/ornatrix/), [Yeti](https://peregrinelabs.com/yeti/), [Shave and a Haircut](https://www.unrealengine.com/en-US/programs/shave-and-a-haircut?sessionInvalidated=true), or [Houdini](https://www.sidefx.com/docs/houdini/fur/workflow.html).

## Groom Asset

A **Groom** asset is created when you import an Alembic (\*.abc) file. These assets are saved in your Content Browser and can be opened in the **Groom Asset Editor**.

![Groom Asset Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f84517c8-46b3-49d0-a74f-07f9a03d96ca/groom-asset-editor.png)

When you open a groom asset, you can do the following in the Groom Asset Editor:

-   [Assign Materials](/documentation/en-us/unreal-engine/groom-materials-in-unreal-engine)
-   [Define levels of detail settings that represent strands, cards, or a mesh](/documentation/en-us/unreal-engine/setting-up-level-of-detail-for-grooms-in-unreal-engine)
-   [Enable and configure physics settings](/documentation/en-us/unreal-engine/enabling-physics-simulation-on-grooms-in-unreal-engine)
-   [Debug your groom with different view modes](/documentation/en-us/unreal-engine/debugging-grooms-in-unreal-engine)

For more information about using this asset editor, see [Groom Asset Editor](/documentation/en-us/unreal-engine/groom-asset-editor-user-guide-in-unreal-engine).

## Groom Binding

**Groom Binding** assets are used to link a Groom asset with a skeletal mesh. This binding asset enables skin motion and deformation to be applied to the hair. Opening a Groom Binding asset displays the groom asset and its link to a skeletal mesh. Groom bindings can be previewed with the Groom Asset Editor.

![Groom Binding Asset Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae7c948b-b338-4ea0-8508-89f360f9dd3c/groom-binding-asset.png)

For more information about this type of asset, see [Groom Bindings](/documentation/en-us/unreal-engine/setting-up-bindings-for-grooms-in-unreal-engine).

## Groom Component

**Groom Components** represent instances of groom assets in a level. A groom component can override some properties of a groom asset, such as its hair radius and LOD biasing.

![Groom Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee223e8d-2ec6-44c8-ae2a-8c1a4daf5a30/groom-component.png)

| Property | Description |
| --- | --- |
| Groom Group Desc |   |
| **Hair Width** | Overrides the hair width (in centimeters). |
| **Hair Root Scale** | The scale of the hair width at the root. |
| **Hair Tip Scale** | The scale of the hair width at the tip. |
| **Hair Shadow Density** | Controls the hair density to reduce or increase hair count during shadow rendering. It enables you to inrease/decrease the shadowing on hair when the number of strands is not realistic. |
| **Hair Raytracing Radius Scale** | Scales the hair geometry radius for ray-tracing effects, such as shadows. |
| **Use Hair Raytracing Geometry** | Enables hair geometry to be used with ray tracing features. |
| **LOD Bias** | Sets the bias for the selected level of detail (LOD). A value greater than 0 will progressively select lower detailed LODs. This property is used when 'r.HairStrands.Cluster.Culling' is enabled. |
| **Use Stable Rasterization** | When enabled, this ensures the hair does not alias. When enabled, groups of hairs might appear thicker. Isolated hair should remain thin. |
| **Scatter Scene Lighting** | When enabled, hair is lit with the scene color. It is used for vellus/short hair, like peach fuzz, to bring light from the surrounding surface, like skin. |
| **Hair Length Scale** | When enabled, this allows scaling the length of the hair. |
| Materials |   |
| **Element \[N\]** | Assign your Hair Material to this Asset slot. |
| Groom |   |
| **Groom Asset** | The Groom Asset to be used for rendering this Actor. |
| **Binding Asset** | An optional Binding Asset for binding a groom onto a Skeletal Mesh. If the Binding Asset is not specified, the projection is done at runtime, which implies a large GPU cost at statup time. |
| **Use Cards** | When enabled, this option forces the groom to use cards/meshes geometry instead of strands. |
| **Attachment Name** | An optional name, where the Groom component should be attached at, when parented to a Skeletal Mesh. |
| Groom Cache |   |
| **Groom Cache** | The groom animation to playback on this component. It must be compatible with the Groom Asset. |
| **Running** | Enable to play back the animation. |
| **Looping** | Enable to loop the animation when the elapsed time is past the animation range. |
| **Manual Tick** | Enable to play back only through Sequencer. |
| **Elapsed Time** | This is a read-only value that shows the time that has elapsed since the start of the animation. |
| Simulation |   |
| **Physics Asset** | The Physics Asset to be used for this groom when physics simulation is enabled. |
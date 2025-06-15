# Precomputed Visibility Volumes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/precomputed-visibility-volumes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/precomputed-visibility-volumes-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:07

---

Like other culling methods, **Precomputed Visibility Volumes** are used for performance optimization for small to medium-sized worlds and typically for Mobile where dynamic occlusion culling is limited depending on hardware. Precomputed Visibility Volumes store the visibility state of Actor's locations in the world based on where the player or camera is. For this reason, precomputed visibility is most useful for projects with mostly statically lit environments, restricted player movement, and somewhat 2D play areas.

Visibility cells are generated during a lighting build above shadow casting geometry. Actor visibility is stored from each cells position. Because precomputed visibility is generated offline, you're trading rendering thread time, normally taken up by hardware occlusion queries, at the cost of increasing runtime memory and lighting build time. With that in mind, it is recommended to only place the volumes in player or camera accessible areas to maintain visibility culling. 

![Example Scene View](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3606ee5-7f94-46cf-a787-5533b13d3843/pvis_visualizationdisabled.png)

![Precomputed Visibility Visualization Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3390ee58-ef4f-48e5-80a9-9e074463d95e/pvis_visualizationenabled.png)

## Setup and Usage

To get started, you'll first need to enable Precomputed Visibility for your Level. Do this by opening the **World Settings** and locate the **Precomputed Visibility** section. Once there, enable the checkbox next to **Precompute Visibility**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5379454d-72c2-4e52-b553-8f7aaffbff45/ws_enablepvis.png "WS_EnablePVIS.png")

From the **Modes** panel, drag a **Precomputed Visibility Volume** into the Level and scale it to fit the playable area.

See [Placement](/documentation/en-us/unreal-engine/precomputed-visibility-volumes-in-unreal-engine#placement) below for tips and suggestions to get the best result.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99f12458-15ab-480f-b54a-2668f0a45f5d/pvis_addvolume.png "PVIS_AddVolume.png")

Before precomputed visibility will work, you will first need to **Build Lighting** and use the Level viewport to enable precomputed visibility cells (blue boxes) by going to **Show > Advanced > Precomputed Visibility**.

When you are placing volumes, do so in player-accessible areas and not with a single all encompassing volume. This way you're not storing and loading visibility data at run time that can never be used.

![Precomputed Visibility visualization before light build](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83c18e5c-2d07-4c8e-91ca-059ed2fe13ae/pvis_visualizationbeforelightbuild.png)

![Precomputed Visibility visualization After light build](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e08912e3-20cc-43e5-a116-a65ab56cb1f8/pvis_visualizationafterlightbuild.png)

If you've already built lighting, you can use the **Build** dropdown from the main toolbar, then select **Precompute Static Visibility** to generate visibility cells without re-building lighting each time.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4c15143-8bc4-4ce4-8ecb-7f38ceb55788/tip_buildjustpvis.png "Tip_buildJustPVIS.png")

### Visibility Cells

After building lighting information at least once for your Level, you can place any number of Precomputed Visibility Volumes and generate the visibility cells that populate the surface of any static shadow casting Actor. You can generate the static visibility by selecting the **Precompute Static Visibility** option from the Build dropdown menu off the main toolbar.

![Precomputed Visibility Cells Visualization: Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e20a2d4e-b126-439a-9570-2d3af5b06693/visibilitycellsviewenabled.png)

![Precomputed Visibility Cells Visualization: Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62253cea-de05-432f-91e4-361fb1cd1f93/visibilitycellsviewdisabled.png)

Use **r.ShowRelevantPrecomputedVisibilityCells** to only show visibility cells near the camera when the show flag for **Show Precomputed Visibility Cells** is enabled. This can be helpful to reduce a lot of cells being on screen at once.

In the case of this scene, the precomputed visibility volumes has been placed (green), lighting built, and there are some Actors occluded by the walls and doorway.

Below, to give you a sense of how precomputed visibility works by storing Actor locations in cells, some of the walls and doorway have been hidden. Drag the slider to move the camera position and see the visibility state change based on where the camera is and the cell it's located in.

The precomputed visibility cells are not visible in the example image, to better display the visibility state of the Actors being occluded.

     ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aec88873-11f6-4b94-9057-e37aaa5d0fa3/pvis_1.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d2a602c-d779-4841-96a7-77bef3fdc3bc/pvis_2.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/281a34b8-2af2-498a-a8e6-ae0318f4d031/pvis_3.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0aabea41-e2ed-423f-88e7-1255c599e42e/pvis_4.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3a83862-3a28-4ae7-a48b-69ef199ad594/pvis_5.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bdd3a18d-a212-4b65-8cb4-1a8dc44a4d9f/pvis_6.png)

Once precomputed visibility has been generated, the cells store what Actors should be visible from that cell's location. In this example, because the cell knows what should be visible or not, occluding Actors (like the walls and doors) can be hidden and Actors occluded will not be visible as long as the camera is within the precomputed visibility cell, making this culling method well-suited as a trade-off for some game types and platforms.

### Setting Cell Play Area Height for Gameplay

One thing to keep in mind when using precomputed visibility is that scale is game-dependent and because of this, parameters for visibility will need to be set accordingly for each game.

To do this, you'll change settings in the `BaseLightmass.ini` file in `[Unreal Engine Root Directory]/Engine/Config` folder. Locate the `DevOptions.PrecomputedVisibility` section.

```
`[DevOptions.PrecomputedVisibility] bVisualizePrecomputedVisibility=False bCompressVisibilityData=True bPlaceCellsOnOpaqueOnly=True NumCellDistributionBuckets=800 CellRenderingBucketSize=5 NumCellRenderingBuckets=5 PlayAreaHeight=220 MeshBoundsScale=1.2 VisibilitySpreadingIterations=1 MinMeshSamples=14 MaxMeshSamples=40 NumCellSamples=24 NumImportanceSamples=40`
Copy full snippet
```
\[DevOptions.PrecomputedVisibility\] bVisualizePrecomputedVisibility=False bCompressVisibilityData=True bPlaceCellsOnOpaqueOnly=True NumCellDistributionBuckets=800 CellRenderingBucketSize=5 NumCellRenderingBuckets=5 PlayAreaHeight=220 MeshBoundsScale=1.2 VisibilitySpreadingIterations=1 MinMeshSamples=14 MaxMeshSamples=40 NumCellSamples=24 NumImportanceSamples=40

Of these settings, you'll want to focus on setting `PlayAreaHeight`. This value is the height (in Unreal Units) above a surface that the visibility cell will be. For your game, this should be the highest the camera can ever be above a surface and is usually the tallest players' eye height plus their jump height.

Setting the `PlayAreaHeight` or any other settings in the configuration file does not require a restart of the engine. You can make the edit and save the .ini file, then use **Precompute Static Visibility** in the **Build** menu dropdown of the main toolbar.

![Play Area Height: 220 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a13ff73d-cf20-4ef5-b254-339ba7a86dbd/pvis_playareaheightdefault.png)

![Play Area Height: 650](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5e4a913-c69f-442f-babd-c2f77344ec5b/pvis_playareaheightadjusted.png)

Using the **ThirdPerson** template, there are a couple of things we need to consider to determine what the PlayAreaHeight should be for this game type:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71f07700-2545-41a4-8009-3e7e92ec5934/pvis_findingcameraheight.png "pvis_findingcameraheight.png")

1.  **Finding the Camera's highest rotational point.**
    -   The camera can be rotated 360 degrees around the character in the ThirdPerson template. At its highest point, it's approximately **395** units above the ground surface.
2.  **Jump height of the player.**
    -   The player can jump approximately **210** units high.
3.  **Maximum height the camera can ever be.**
    -   Adding the highest camera position (365 units) to the player's jump height (210 units), the maximum height the camera can be without going outside of the cell is **615** units. 

Knowing the PlayAreaHeight must atleast be 615 units to keep the camera (at any vertical rotation), a little bit of a buffer is added to keep the camera within the visibility cells. The height with the buffer will be **650** units. For this game type and camera movement, it makes sense to have such a large height for the cells. However, keep in mind that larger PlayAreaHeight values require more runtime memory because more Actor visibility states must be stored.

## Using Precomputed Visibility Override Volumes

**Precomputed Visibility Override Volumes** let you manually override the visibility of Actors for their location in the world if the auto generated result of a Precomputed Visibility Volume is undesired. These are also used for performance optimization and should only be placed in areas where the Player can access.

### Placement

To use this volume, use the **Modes** panel to drag a **Precomputed Visibility Override Volume** into the Level and scale it to fit the playable area.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9a0a5a9-c57b-49d1-8d99-3587936034c5/pvis_overridevolume_addtoscene.png "pvis_overridevolume_addtoscene.png")

Use the **plus** (**+**) button to add any number of elements to the array list. 

![pvis_override settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6296e2d4-9312-4d2b-9937-877677783be3/pvis_overridesettings.png)

For each element added, use the eyedropper or dropdown selection to add an Actor or Level.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0098c50-ed1e-439d-9b6c-b218ed97aa4c/pvis_overridesettings_selectactor.png "pvis_overridesettings_selectActor.png")

For additional information, see [Visibility and Occlusion Culling Settings](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-reference-in-unreal-engine).

## Relevant Statistics

When checking performance of precomputed visibility, you'll want to start by looking at some of the stats for **Initviews** and ones for **Memory**. These two stat panels inform you how well precomputed visibility is performing and how much memory it's using at runtime in the process.

### Stat Initviews

Use the command **stat initviews** to see how effective precomputed visibility is in your Levels.

Click image for full size.

| Stat | Description |
| --- | --- |
| **Statically Occluded Primitives** | Displays how many primitives were determined invisible by precomputed visibility after frustum culling took place. This will only be visible when the camera view is inside a visibility cell. |
| **Occluded Primitives** | Displays how many primitives were determined invisible by both precomputed visibility and the dynamic occlusion system. |
| **Decompress Occlusion** | Displays how much time was spent decompressing precomputed visibility. Large volumes or smaller cell sizes can increase the memory used which will affect the time it takes to decompress. |

If you don't see any values, it's likely the camera is outside of the visibility cell or precomputed visibility has not been generated.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/273dd4a0-0f3d-4fe8-864e-e7a8f9276753/statinitviews2.png "StatInitviews2.png")

If the Statically occluded primitives is lower than expected, check **World Settings > Precomputed Visibility** and look at the **Visibility Aggressiveness**. More aggressive settings cull more Actors but cause more visibility errors to occur, like Actors popping in around corners.

### Stat Memory

Use the command **stat memory** to get an idea of the memory usage being allocated for your game, and more specifically, precomputed visibility.

Click image for full size.

The stat **Precomputed Visibility Memory** displays the actual runtime memory usage currently being used for precomputed visibility.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35b4e655-cd5a-41f9-aea3-aad277fa86b9/statmemory2.png "StatMemory2.png")

This stat is **not** reliable in Play-in-Editor (PIE) mode since memory usage is being counted for both the Editor and PIE simultaneously. Instead, only use the Editor in Game View mode or Standalone Game to get the most accurate result.

## Limitations

The following limitations apply to precomputed visibility:

-   Does not handle movable Actors.
-   Does not handle non-opaque Materials, such as translucent or masked materials.
-   Cells are only placed above surfaces. Projects with flying modes won't get much benefit.
-   Does not handle streaming levels efficiently. All data is stored in the persistent Level.
-   Only static shadow casting triangles will occlude.
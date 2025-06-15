# Hierarchical Level of Detail Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hierarchical-level-of-detail-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/hierarchical-level-of-detail-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:27:27

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdfb3352-dd83-4f4e-8c86-ffd83676c50b/hlod_howto_header.png)

**Hierarchical Level of Detail** (or HLOD), in its simplest form, is a way to combine pre-existing [Static Mesh Actors](/documentation/en-us/unreal-engine/static-mesh-actors-in-unreal-engine) into a single HLOD Proxy Mesh and Material (with atlased Textures). Using HLOD may lead to increased performance as they reduce draw calls down to one call per Proxy Mesh as opposed to a draw call for each individual Static Mesh Actor. When generating HLOD Proxy Meshes, there several parameters you can adjust which help define how Static Mesh Actors are grouped together as clusters that will ultimately be built into Proxy Meshes. 

To use HLOD, you will need to enable the HLOD system in each of the Levels you wish to take advantage of the system.

## Proxy Meshes

Proxy Meshes can be opened independently and their settings can be adjusted as desired. 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a2b3144-5eb1-4c52-ba1b-afe8344c058a/image_16.png)

The Proxy Mesh above contains several elements that had their own Textures which were combined into a single texture (below).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9320b825-5b04-48d6-8cce-88ead89c229e/image_17.png)

For anything using **Mask** or **Opacity**, alpha channels are not passed to the merged Texture. If opacity or masked items are needed, disable the option for **Merge Textures**. When doing this the Proxy Mesh will assign the original material as a **Material Element ID** instead of combining them.

## Hierarchical LOD Volume

The **Hierarchical LOD Volume** (HLOD Volume) is used to manually define/create an HLOD cluster. The **Hierarchical LODVolume** can be an be dragged into your Level from the **Place Actors** panel in the **Volumes** tab.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd07c391-ca2a-4531-96d2-c491d72a7608/hlodoverview_hlodvolume.png "HLODOverview_HLODvolume.png")

You can place this volume around Actors you want to be grouped in the same cluster. It can be helpful to make this slightly larger than the Actors you wish to include and should not be tightly bounding them. Once you have placed the volume around the Actors you can use the option **Generate Clusters** from the **HLOD Outliner** to create a new cluster with these grouped Actors.

Below, we have several cubes and spheres within an HLOD Volume and one cube and the floor outside the volume. 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24d7cc8f-0c2b-474c-a4c3-5efe98a00fee/hlodoverview_volume01.png "HLODOverview_Volume01.png")

When we **Generate Clusters** inside the **HLOD Outliner**, we have two separate clusters: one containing the Static Mesh Actors inside the HLOD Volume, the other containing the Static Mesh Actors that are not inside the HLOD Volume. 

Click image for full view.

Optionally, you can enable **Only Generate Clusters for Volumes** (below) to generate clusters for only Static Mesh Actors that exist within an HLOD Volume. 

Click image for full view.

### Example

Below is an example of Generated Clusters before and after adding HLOD Volume.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb6d74be-459b-4bd6-a42a-b93f8781b043/image_19.png)

HLOD Level Desired Bound Radius: 500

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7653013d-b200-4aef-910c-5ec3540faffc/image_20.png)

Drag in the Volume and scale accordingly to cover your **Actors**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/282af8a8-1002-4c91-9862-3bb13d1531d3/image_21.png)

Selecting the generated **LODActor** from the HLOD Outliner shows the cluster created and the Cluster bounds.

Right-click on the **LODActor** in the HLOD Outliner and click on **Select Contained Actors** to see the **Actors** used for this particular **LODActor** in your scene.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6300b9b-fdee-43bd-b8d7-069205ec04a9/image_22.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0023f145-7a0f-4344-99c4-e7993db1c0d2/image_23.png)

## HLOD Overrides

When you select an LOD Actor in the Level, inside the **Details** panel, you can override the **Hierarchical LODSettings** being used. 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59d56b39-b9c0-46b1-89c9-005f42ee5873/hlodoverview_overides.png "HLODOverview_Overides.png")

Please see [Mesh Generation Settings](/documentation/en-us/unreal-engine/hierarchical-level-of-detail-outliner-in-unreal-engine#meshgenerationsettings) and properties for more information.

## HLOD Visualization

There are visualization modes you can use to view Mesh LODs and HLODs in the viewport. To access these, click the **View Mode** button in the upper-left corner of the viewport and select your perfered method of LOD Coloration.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3b0b01a-2f5f-4ee6-9fb2-81a5c51054f6/levelofdetailcoloration.png)

During a play session you can enter console command `viewmode hlodcoloration` to achieve the same result.
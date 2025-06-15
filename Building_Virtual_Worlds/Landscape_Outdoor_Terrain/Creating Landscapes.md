# Creating Landscapes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-landscapes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-landscapes-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:34

---

Unreal Engine 5 (UE5) is capable of creating massive terrain-based worlds using its suite of powerful terrain editing tools. Use the **Landscape** tool to create immersive outdoor terrain pieces that are optimized to maintain playable frame rates across a multitude of different devices.

You can create your Landscape using any of the following methods:

-   Create a new Landscape heightmap from scratch using the in-engine Landscape tools.
    
-   Import a Landscape heightmap created previously in Unreal Editor or created through external tools. Check out [Importing and Exporting Landscape Heightmaps](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-and-exporting-landscape-heightmaps-in-unreal-engine).
    
-   Create your own format for importing Landscapes. Check out [Creating Custom Landscape Importers](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-custom-landscape-importers-in-unreal-engine).
    

For examples of the Landscape tool in action, see [Landscapes Content Examples](https://dev.epicgames.com/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine).

## Opening the Landscape Tool

Before you can create a Landscape, you must first open the Landscape tools. From the Main Toolbar, click **Select Mode**, then select **Landscape**.

[![Opening the Landscape tool](https://dev.epicgames.com/community/api/documentation/image/9d2f4203-4d1c-40bd-8398-fa6c8f61a4df?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9d2f4203-4d1c-40bd-8398-fa6c8f61a4df?resizing_type=fit)

Click image for full size.

You can also press **Shift + 2** on your keyboard to change to the Landscape tool at any time.

The first time you open the Landscape tool, you will automatically be taken to the [Manage Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-manage-mode-in-unreal-engine) tab. If you do not have any other Landscape Actors currently in your level, you will be prompted to create one. In Landscape Manage Mode, you can create new Landscapes and modify existing Landscapes and their components.

[![Manage Mode in the Landscape tool](https://dev.epicgames.com/community/api/documentation/image/e5632a7d-91ae-4d5f-b253-0a07564625f4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e5632a7d-91ae-4d5f-b253-0a07564625f4?resizing_type=fit)

Click image for full size.

If your Level already contains one or more Landscapes, the **Landscape** tab will look different. The **Landscape Editor** section will display a dropdown menu with the **Selection** tool visible. From this dropdown menu, you can select a Landscape to work with.

[![Selecting an existing Landscape](https://dev.epicgames.com/community/api/documentation/image/ebd9c3e6-a781-4b14-87a4-f119e98a7a24?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ebd9c3e6-a781-4b14-87a4-f119e98a7a24?resizing_type=fit)

Click image for full size.

## Creating a new Landscape using the Landscape Tool

You create a new Landscape from scratch from the **New Landscape** section of the **Landscape** tool panel.

[![Creating a new Landscape](https://dev.epicgames.com/community/api/documentation/image/4db0838a-2baa-4fc2-a3b6-c60d52c8ed3c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4db0838a-2baa-4fc2-a3b6-c60d52c8ed3c?resizing_type=fit)

Click image for full size.

| Number | Option | Description |
| --- | --- | --- |
| 
**1**

 | 

**Create New**

 | 

Creates a new Landscape Actor in your Level.

 |
| 

**2**

 | 

**Import from File**

 | 

Imports a Landscape heightmap made in an external program.

 |
| 

**3**

 | 

**Enable Edit Layers**

 | 

Enables the use of Non-Destructive Landscape Layers and Splines.

 |
| 

**4**

 | 

**Material**

 | 

Assigns a Material to your Landscape.

 |
| 

**5**

 | 

**Layers**

 | 

Displays any layers that are a part of your Landscape Material.

 |
| 

**6**

 | 

**Location**

 | 

Sets the location in the world where the Landscape is created.

 |
| 

**7**

 | 

**Rotation**

 | 

Sets the rotation of the Landscape in the world.

 |
| 

**8**

 | 

**Scale**

 | 

Sets the scale of the Landscape in the world.

 |
| 

**9**

 | 

**Section Size**

 | 

Landscapes use Section Size for LOD and Culling. Landscapes with smaller sections can have more optimized LODs but at a higher CPU cost. Larger sections have fewer components and are less costly on the CPU.

If you want to have a large Landscape, you will need to use a larger section size, since using a smaller section size and then scaling the Landscape will increase the cost on the CPU.

 |
| 

**10**

 | 

**Sections Per Component**

 | 

Sets the number of sections in a single landscape component. The number of sections and the section size determine the size of each landscape component. A component is the base unit of rendering and culling.

With a larger section size, you get the added benefit of reduced CPU calculation time. However, you might run into issues with the Landscape rendering too many vertices at once. This could be especially prevalent when using very large areas of Landscape. These issues could be even worse on mobile devices because of the limited amount of draw calls you can have due to hardware limitations.

 |
| 

**11**

 | 

**Number of Components**

 | 

Sets the size of your landscape along with Section Size. This value is capped at 32 x 32 since each component has a CPU cost associated with it. Going over this cap could result in performance issues with the Landscape.

 |
| 

**12**

 | 

**Overall Resolution**

 | 

The number of vertices your Landscape is using.

 |
| 

**13**

 | 

**Total Components**

 | 

The total number of components that will be created for your Landscape.

 |
| 

**14**

 | 

**Fill World**

 | 

Makes your Landscape as big as possible.

 |
| 

**15**

 | 

**Create**

 | 

Creates your Landscape in the world using the settings you specified.

 |

For the example below, we are going to leave all of the Landscape settings at their default values that are listed below.

| Property Name | Value |
| --- | --- |
| 
**Section Size**

 | 

63 x 63 Quads

 |
| 

**Section Per Component**

 | 

1 x 1 Section

 |
| 

**Number of Components**

 | 

8 x 8

 |
| 

**Overall Resolution**

 | 

505 x 505

 |

Be careful when choosing **Section Size** because as the number of components increase, build times and performance can be dramatically affected. 63x63 quads per section is generally recommended as it gives good performance and size.

When completed, you should have something that looks like this in your **New Landscape** properties box.

[![New Landscape settings](https://dev.epicgames.com/community/api/documentation/image/9fc53ed0-65f2-4863-b28e-950eb7075aab?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9fc53ed0-65f2-4863-b28e-950eb7075aab?resizing_type=fit)

Click image for full size.

In the main viewport, there should be a preview of the new Landscape you are setting up which should look like the following:

[![Landscape Actor preview](https://dev.epicgames.com/community/api/documentation/image/31562733-691a-4a7e-8d66-4545b0a2575c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/31562733-691a-4a7e-8d66-4545b0a2575c?resizing_type=fit)

Click the image for full size.

Landscape Actors can Move, Rotate, and Scale like any other Actor.

You can assign a Material to your Landscape when you create it. To do so, select an appropriate Material in the **Content Browser**, and then assign it in the **New Landscape** section, next to **Material**, by clicking the Assign arrow icon. For more information about Landscape Materials, see [Landscape Material Layer Blending](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine).

[![Assigning a Material to a Landscape](https://dev.epicgames.com/community/api/documentation/image/1c1788c9-a404-4a6a-b196-4d8905460dd9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1c1788c9-a404-4a6a-b196-4d8905460dd9?resizing_type=fit)

Click image for full size.

When you are ready to create your new Landscape, click the **Create** button in the lower-right corner of the Landscape tool panel. The Landscape will appear in the viewport as a flat plane. If you assigned a Material to it, it will appear with the Material applied. If not, it will use the Level Editor's default Material.

[![Create Landscape button](https://dev.epicgames.com/community/api/documentation/image/5cb371bf-5429-4cf8-a2bb-555266c850d7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5cb371bf-5429-4cf8-a2bb-555266c850d7?resizing_type=fit)

Click image for full size.

If the Landscape is large or complex, it may take a few seconds for it to appear.

Once you have pressed the **Create** Button, you should have something that looks similar to the following.

[![The final Landscape Actor](https://dev.epicgames.com/community/api/documentation/image/e77c3e3d-0376-4049-951e-69ef6318c43a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e77c3e3d-0376-4049-951e-69ef6318c43a?resizing_type=fit)

With your new Landscape now created, you can now start to [Sculpt](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-sculpt-mode-in-unreal-engine) or [Paint](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-paint-mode-in-unreal-engine) the Landscape to your liking.
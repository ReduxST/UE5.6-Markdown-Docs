# Foliage Mode

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine)  
**Processed:** 2025-06-14 16:24:05

---

**Foliage Mode** is a set of tools that enables you to quickly paint or erase sets of **Static Meshes** or **Actor Foliage** on filter-enabled Actors and geometry. Using this mode, it is possible to populate a large outdoor environment with foliage in a short amount of time.

[![Foliage Cottage](https://dev.epicgames.com/community/api/documentation/image/d972d48e-cfff-499e-825a-49062d12597c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d972d48e-cfff-499e-825a-49062d12597c?resizing_type=fit)

Foliage can quickly add detail to any outdoor environment.

For examples of the **Foliage** tool in action, see the **Foliage** section of the **Landscapes Content Examples** project.

## Foliage Edit Mode

To use the **Foliage** tool, click the **Foliage** option (**Shift+3**) in the **Modes** dropdown menu.

[![Foliage Mode Drop Down](https://dev.epicgames.com/community/api/documentation/image/2bb89564-c2ec-43d0-951f-a0eca5f5f5cc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2bb89564-c2ec-43d0-951f-a0eca5f5f5cc?resizing_type=fit)

Click image for full size.

This will open the **Foliage** panel.

### Foliage Mode Panel

[![Foliage Tools](https://dev.epicgames.com/community/api/documentation/image/8d64db41-e3b4-42a1-b87e-866a4e5f24a9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8d64db41-e3b4-42a1-b87e-866a4e5f24a9?resizing_type=fit)

Click image for full size.

| Numbers | Description |
| --- | --- |
| 
**1**

 | 

Tools Palette

 |
| 

**2**

 | 

Brush Options

 |
| 

**3**

 | 

Filter Options

 |
| 

**4**

 | 

Foliage Palette

 |
| 

**5**

 | 

Foliage Details

 |

### Foliage Types

[![Foliage Type Drop Down](https://dev.epicgames.com/community/api/documentation/image/2781ed57-9ebe-4ba6-a8d2-0466761ed2dd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2781ed57-9ebe-4ba6-a8d2-0466761ed2dd?resizing_type=fit)

Click image for full size.

Open the **Add Foliage Type** dropdown menu to add the following:

| Foliage Type | Description |
| --- | --- |
| 
**Actor Foliage**

 | 

Foliage type that places Blueprint or Native Actor instances in the scene. High densities of foliage can cause performance issues.

 |
| 

**Static Mesh Foliage**

 | 

Foliage type that uses mesh instancing.This type is best for non-destructive foliage.

 |

Static Meshes placed with Foliage Edit Mode are automatically grouped together into batches that are rendered using hardware instancing, where many instances can be rendered with only a single draw call, while Actor Foliage comes at the same rendering cost as placing normal Actors into a scene.

## Using Foliage Mode

Foliage Mode is a collection of tools that are used to paint foliage directly on to a Landscape or other filter-enabled Actor.

### Foliage Tools

[![Foliage Tools Palette](https://dev.epicgames.com/community/api/documentation/image/db4bf453-baeb-4e8f-b698-e6d9a5229ca9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/db4bf453-baeb-4e8f-b698-e6d9a5229ca9?resizing_type=fit)

Click image for full size.

| Tool | Description |
| --- | --- |
| 
**Select**

 | 

Selects individual Foliage Instances. You can select multiple Foliage meshes by holding down the **Ctrl** button.

 |
| 

**All**

 | 

Selects all Foliage Instances.

 |
| 

**Deselect**

 | 

Clears the current selection.

 |
| 

**Invalid**

 | 

Selects any invalid Foliage Instances.

 |
| 

**Lasso**

 | 

Selects any Foliage Instances of the selected Foliage type when painted over with the brush.

 |
| 

**Paint**

 | 

Paints instances of the selected Foliage type. Erase instances of the selected Foliage type by holding down the Shift key when painting.

 |
| 

**Reapply**

 | 

Selectively changes parameters for Foliage Instances already placed in the world. Use as follows:

1.  Select the Reapply tool and then select the Foliage type you want to apply changes to in the Mesh List.
    
2.  In the Foliage Details section, make your changes.
    
3.  Paint the changes on to the Foliage Instances in the level.
    

 |
| 

**Single**

 | 

Paints a single instance of the selected Foliage type.

 |
| 

**Fill**

 | 

Fills the selected target with Foliage Instances.

 |
| 

**Erase**

 | 

Erases the selected Foliage type when painted over with the brush.

 |
| 

**Remove**

 | 

Removes the selected Foliage Instances.

 |
| 

**Move**

 | 

Moves the selected Foliage Instances to the current Level.

 |

### Brush Options

The **Brush Options** section is context sensitive and contains one or more of the following:

[![Foliage Brush Options](https://dev.epicgames.com/community/api/documentation/image/3c2b2e19-dca8-46f6-90ab-7e560b53d9a1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3c2b2e19-dca8-46f6-90ab-7e560b53d9a1?resizing_type=fit)

Click image for full size.

| Option | Description |
| --- | --- |
| 
**Brush Size**

 | 

Adjusts the size of the foliage brush.

 |
| 

**Point Density**

 | 

Adjusts the density of the foliage affected by the selected tool. This is a multiplier of the **Density** property located in the selected foliage type's details.

 |
| 

**Erase Density**

 | 

Adjusts the density of the foliage that is left behind when erasing with the **Shift** key held.

 |
| 

**Single Instance Mode**

 | 

When enabled, paints a single foliage instance at the cursor location. Can be used in two modes:

-   **All Selected**: Places a single instance of all selected foliage types.
    
-   **Cycle Through Selected**: Cycles through placing a single instance of each selected foliage type, placing only one type with each mouse click.
    

 |
| 

**Place in Current Level**

 | 

When enabled, places instances of the selected foliage types in the current level. Otherwise places the instances of the selected foliage types in the level containing the mesh or Actor being painted on.

 |

### Filter Settings

Using the Filters section, you can control which surfaces the selected tool affects and which foliage types are currently active. This is also the section of the menu where new foliage types are added.

[![Foliage Filter Options](https://dev.epicgames.com/community/api/documentation/image/c3541b9c-033e-40d3-b34e-f0dcbe73e843?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c3541b9c-033e-40d3-b34e-f0dcbe73e843?resizing_type=fit)

Click image for full size.

| Option | Description |
| --- | --- |
| 
Landscape

 | 

Places the selected foliage types on to Landscapes.

 |
| 

Static Mesh

 | 

Places the selected foliage types on to Static Meshes.

 |
| 

BSP

 | 

Places the selected foliage types on to BSP geometry.

 |
| 

Foliage

 | 

Places the selected foliage types on to other blocking foliage geometry.

 |
| 

Translucent

 | 

Places the selected foliage types on translucent geometry.

 |
| 

Mesh List

 | 

Area in which Static Meshes and Actor Foliage used as foliage are placed.

Placing the mouse pointer over a foliage type displays a checkbox that enables or disables that foliage type when using a tool.

Clicking one or more foliage types displays their details in the Foliage Details located below the Mesh List area.

 |
| 

Foliage Details

 | 

Area displaying the details of the selected foliage types. Contains a variety of properties for customizing the behavior of the Static Mesh or Actor Foliage.

 |

For more information on adding foliage types to the Mesh List, see [Adding Foliage to a Landscape Actor](https://dev.epicgames.com/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine)

### Culling Settings

Foliage instances are rendered as clusters in a single draw call and each cluster is either rendered or not rendered based on occlusion. Setting a value in the **End Cull Distance** parameter in the foliage details causes the clusters to be culled beyond that distance. However, this will cause groups of meshes to disappear abruptly as the entire cluster goes out of range.

This can be reduced by adding a **Start Cull Distance** parameter and then setting up the Material appropriately. In the vertex shader, a per-instance fading factor is calculated, which goes from 1.0 at the start distance to 0.0 at the end distance. This is accessible in the Material using a **PerInstanceFadeAmount** node. When connecting that to an opacity or masking value, you can use it to fade instances over a distance before they reach the **Cull Distance End** and are removed from rendering. Lowering the value of the **FadeMultiplier** parameter will increase the speed of the fade. A value of zero will make your foliage invisible at any distance.

The example Material below multiplies the Material mask by the fading factor to thin out the foliage mesh's leaves until they completely disappear.

[![Foliage Culling](https://dev.epicgames.com/community/api/documentation/image/6a6302af-dfad-48ff-bb58-768a15bf8506?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6a6302af-dfad-48ff-bb58-768a15bf8506?resizing_type=fit)

Click image for full size.

Nanite-enabled meshes are not affected by culling distance and instance fading.

### LOD Settings

Static Mesh LOD is supported for foliage. There are a few caveats:

-   You should ensure your Static Mesh has only one entry in the Elements array (visible under **LOD0**).
    
-   Light and shadow maps are shared between all LOD levels, so all LODs need to use the same unwrapping.
    
-   Currently, the entire cluster of instances change LODs simultaneously. We may add support for distance-based fading per instance in the future.
    

### Lighting

Shadow and light maps are generated individually by Lightmass as needed for each instance, and these are tiled together for each precomputed batch. There are several settings on the Static Mesh that should be checked for precomputed lighting to operate well with instanced foliage. Lightmass is less forgiving when generating shadow maps for instanced meshes, and incorrect settings could lead to black meshes after rebuilding lighting.

-   **Light Map Coordinate Index**: This must be set to a valid UV channel that has a unique UV unwrapping. The Static Mesh Editor's **Generate Unique UVs** feature, which you can access from the Window menu, can quickly generate a unique unwrapping.
    
-   **Lightmap Resolution**: This must be a small enough number so that all the shadow maps for instances in a single cluster (by default 100) can be tiled together without exceeding the maximum texture resolution (4094x4096).
    

### Foliage Scalability

Foliage Static Meshes can use the Scalability System to increase or decrease the amount of Foliage Instances that are currently being rendered on screen.

To use this functionality within your project:

1.  Navigate to the **Foliage Mesh List** and select a **foliage type**.
    
    [![Select Foliage Type](https://dev.epicgames.com/community/api/documentation/image/a40b4a66-7221-4f65-ba44-ecc8b618db0c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a40b4a66-7221-4f65-ba44-ecc8b618db0c?resizing_type=fit)
    
    Click image for full size.
    
2.  In the **Foliage Details**, locate the **Scalability** section.
    
    [![Foliage Scalability Settings](https://dev.epicgames.com/community/api/documentation/image/ccb5e7c5-090f-4cae-a10e-63b119da7388?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ccb5e7c5-090f-4cae-a10e-63b119da7388?resizing_type=fit)
    
    Click image for full size.
    
3.  Select the checkbox for **Enable Density Scaling**.
    
    [![Enable Density Scaling](https://dev.epicgames.com/community/api/documentation/image/b1b50fab-f530-4ecb-a7d9-20a4f5ad750a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b1b50fab-f530-4ecb-a7d9-20a4f5ad750a?resizing_type=fit)
    
    Click image for full size.
    

You can now control the density of the foliage being rendered during runtime with the command `foliage.DensityScale`.

Below, you can see the density of the Foliage changes as the `foliage.DensityScale` setting is set to 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 1.0.

![Drag the slider to adjust the foliage.DensityScale setting from 0.1 to 1.0.](https://dev.epicgames.com/community/api/documentation/image/06466f5e-ccce-4a3c-9407-00d6009b4478?resizing_type=fit&width=1920&height=1080)![Drag the slider to adjust the foliage.DensityScale setting from 0.1 to 1.0.](https://dev.epicgames.com/community/api/documentation/image/d0713382-21e0-48b9-b7f1-7505dbd6419b?resizing_type=fit&width=1920&height=1080)![Drag the slider to adjust the foliage.DensityScale setting from 0.1 to 1.0.](https://dev.epicgames.com/community/api/documentation/image/4238d539-edc0-4f21-a439-c7fd9f660b87?resizing_type=fit&width=1920&height=1080)![Drag the slider to adjust the foliage.DensityScale setting from 0.1 to 1.0.](https://dev.epicgames.com/community/api/documentation/image/17a76ec6-3724-4da2-9548-45bc25e96b46?resizing_type=fit&width=1920&height=1080)![Drag the slider to adjust the foliage.DensityScale setting from 0.1 to 1.0.](https://dev.epicgames.com/community/api/documentation/image/41acf8b5-99c6-4675-9241-20408e1d1ced?resizing_type=fit&width=1920&height=1080)![Drag the slider to adjust the foliage.DensityScale setting from 0.1 to 1.0.](https://dev.epicgames.com/community/api/documentation/image/9c2fb2a4-1dcd-4185-ad4e-639d772f48e3?resizing_type=fit&width=1920&height=1080)![Drag the slider to adjust the foliage.DensityScale setting from 0.1 to 1.0.](https://dev.epicgames.com/community/api/documentation/image/dfea7114-746d-473d-8593-f87977fdd993?resizing_type=fit&width=1920&height=1080)![Drag the slider to adjust the foliage.DensityScale setting from 0.1 to 1.0.](https://dev.epicgames.com/community/api/documentation/image/d7d4282a-1cfb-4802-a86d-57a0e7c3b6e2?resizing_type=fit&width=1920&height=1080)![Drag the slider to adjust the foliage.DensityScale setting from 0.1 to 1.0.](https://dev.epicgames.com/community/api/documentation/image/edd81433-07f5-4484-a53b-1d51f77b75bf?resizing_type=fit&width=1920&height=1080)![Drag the slider to adjust the foliage.DensityScale setting from 0.1 to 1.0.](https://dev.epicgames.com/community/api/documentation/image/f229ff2f-acf1-4a7a-ba48-42dac49c4495?resizing_type=fit&width=1920&height=1080)

**Drag the slider to adjust the foliage.DensityScale setting from 0.1 to 1.0.**

### Using Foliage with World Partition

In a World Partition map, the default grid size for Foliage Instances is 256 meters. This is separate from the World Partition grid size.

To change the default size of the Instanced Foliage Grid for new maps:

[![Project Settings Foliage Instance Grid Size](https://dev.epicgames.com/community/api/documentation/image/4dc4b5c6-2888-4819-91f6-ad68d2063f3f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4dc4b5c6-2888-4819-91f6-ad68d2063f3f?resizing_type=fit)

Click image for full size.

1.  Open the Project Settings by opening the **Edit** menu and selecting the **Project Settings** option.
    
2.  In the search box, search for **Foliage**.
    
3.  Change the value of the **Instanced Foliage Grid Size** to your desired value in centimeters. In the above example, 25600 centimeters is equal to 256 meters.
    

The default grid size can be changed for existing maps using the **World Partition Builder Commandlet**:

[![Foliage Grid Size Commandlet](https://dev.epicgames.com/community/api/documentation/image/f04b39bf-b77b-40c9-ad99-4370e2ffb6da?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f04b39bf-b77b-40c9-ad99-4370e2ffb6da?resizing_type=fit)

Click image for full size.

To change the default grid size for Foliage Instances:

1.  In Windows, open a Command Prompt window.
    
    [![Windows Command Prompt](https://dev.epicgames.com/community/api/documentation/image/5c96a7ab-fa6b-4f74-bd4f-cf61238e827f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5c96a7ab-fa6b-4f74-bd4f-cf61238e827f?resizing_type=fit)
    
    Click image for full size.
    
2.  At the prompt, begin by navigating to the location of the `UnrealEditor.exe` executable file. In the above example: `c:\Builds\Home_UE5_Engine\Engine\Binaries\Win64`.
    
    [![Begin the command line with the executable](https://dev.epicgames.com/community/api/documentation/image/8d1efbce-e14b-4d5f-8a13-b0b903d5803e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8d1efbce-e14b-4d5f-8a13-b0b903d5803e?resizing_type=fit)
    
    Click image for full size.
    
3.  Next, begin the command with the name of the .exe file that will run the commandlet, `UnrealEditor.exe`.
    
4.  Add the name of the project. Here, `QAGame`.
    
    [![Add Project Name](https://dev.epicgames.com/community/api/documentation/image/42cffaa1-efa3-411f-81f1-3d77f6041be7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/42cffaa1-efa3-411f-81f1-3d77f6041be7?resizing_type=fit)
    
    Click image for full size.
    
5.  Add the name of the target map.
    
    [![Add Target Map](https://dev.epicgames.com/community/api/documentation/image/5b594786-a542-4bfc-8dfd-6c40f3b55e85?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5b594786-a542-4bfc-8dfd-6c40f3b55e85?resizing_type=fit)
    
    Click image for full size.
    
6.  Finish the command with the name of the commandlet and the following arguments:
    
    -   `-run=WorldPartitionBuilderCommandlet` is the name of the commandlet.
        
    -   `-Builder=WorldPartitionFoliageBuilder` is the name of the builder within the commandlet.
        
    -   `-NewGridSize` is the new value of the Instanced Foliage Grid in centimeters. In the example, a value 51200 is equal to 512 meters.
        
        [![Finish the Command Line](https://dev.epicgames.com/community/api/documentation/image/887cc409-ec72-466e-87e1-f30f9fcd53d2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/887cc409-ec72-466e-87e1-f30f9fcd53d2?resizing_type=fit)
        
        Click image for full size.
        
7.  Press **Enter** and the commandlet will change your Foliage Instance Grid setting for the designated map.
    

## Adding Foliage to a Landscape

Painting one or more types of foliage directly on to a Landscape Actor is an excellent way to quickly add detail to any outdoor environment.

[![Foliage Landscape Painting](https://dev.epicgames.com/community/api/documentation/image/f8e06206-627b-46f5-8a0e-1daf8a7efa72?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f8e06206-627b-46f5-8a0e-1daf8a7efa72?resizing_type=fit)

Click image for full size.

1.  Start by creating a new Landscape Actor if your level does not already have one. Sculpt some hills to create a bit of contrast. For more information on creating and working with Landscape Actors, see Landscape Quick Start Guide.
    
    [![Add Landscape Actor](https://dev.epicgames.com/community/api/documentation/image/b83efc44-7d26-4af2-aab1-0c9178aa2bd3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b83efc44-7d26-4af2-aab1-0c9178aa2bd3?resizing_type=fit)
    
    Click image for full size.
    
2.  Open the **Modes** drop down and select the **Foliage** mode. Alternatively, you can use the hotkey **Shift + 3**.
    
3.  In the **Content Drawer**, navigate to the location of a Static Mesh that you would like to use as a foliage type, such as this **Static Mesh Cube**. Click and drag the **Static Mesh** from the **Content Drawer** to the **Mesh List** in the **Foliage** panel.
    
    [![Drag Static Mesh from Content Drawer to Mesh List](https://dev.epicgames.com/community/api/documentation/image/b473cce2-30fa-4f1f-99e6-b73547d91353?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b473cce2-30fa-4f1f-99e6-b73547d91353?resizing_type=fit)
    
    Click image for full size.
    
4.  Select the **Paint** tool. Adjust the **Brush Size** in the **Brush Options** to **128**. Adjust the **Paint Density** to **0.3**.
    
    [![Adjusting Foliage Paint Setting](https://dev.epicgames.com/community/api/documentation/image/1b84fd49-de8c-4bdf-a0b4-16d0dc7d1705?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1b84fd49-de8c-4bdf-a0b4-16d0dc7d1705?resizing_type=fit)
    
    Click image for full size.
    
5.  Select the **Static Mesh** in the **Mesh List**. Under the **Painting** section of the **Foliage Details**, change the **Radius** value to **100**. In this example, this ensures that instances of the cube that will be painted on the Landscape do not overlap.
    
    [![Foliage Details Settings](https://dev.epicgames.com/community/api/documentation/image/600ea9c6-f909-4d42-98f8-6c4271366da0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/600ea9c6-f909-4d42-98f8-6c4271366da0?resizing_type=fit)
    
    Click image for full size.
    
6.  Next, adjust the **Min** value of the **Scale X** to **0.4** and the **Max** value to **0.8**. This will create some variety in sizes when the foliage is painted.
    
    [![Adjusting Foliage Details Scale](https://dev.epicgames.com/community/api/documentation/image/a8897a52-01f4-475e-9767-b89c61068de4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a8897a52-01f4-475e-9767-b89c61068de4?resizing_type=fit)
    
    Click image for full size.
    
7.  In the viewport, click and hold the **LMB** to paint foliage across the **Landscape**.
    
    [![Foliage Landscape Painting](https://dev.epicgames.com/community/api/documentation/image/ed3e54ea-e9fa-437a-8a69-852e71b9e1e0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ed3e54ea-e9fa-437a-8a69-852e71b9e1e0?resizing_type=fit)
    
    Click image for full size.
    

## Reattaching Foliage Instances

There may be times when Foliage Instances can become detached from their base component. For example, when the foliage placement is fine but the base Landscape needs to be changed.

To reattach the foliage to the underlying component, follow these steps:

1.  While in Foliage Mode, select the Foliage Instances you want to reattach.
    
2.  In the viewport, move the selected instances above the target component.
    
3.  Press the **End** key to snap the foliage to the ground. This will reparent the Foliage Instances to the target component. The foliage will also align to the component based on the component's normal if they were originally placed using the **Align to Normal** option. This setting is located in the **Placement** section of the Foliage type's Details.
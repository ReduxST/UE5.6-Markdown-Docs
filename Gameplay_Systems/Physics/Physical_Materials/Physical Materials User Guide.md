# Physical Materials User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/physical-materials-user-guide-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/physical-materials-user-guide-for-unreal-engine)  
**Processed:** 2025-06-14 16:42:30

---

This document will cover the creation and usage of **Physical Materials** as well as enabling or editing **Surface Types** for your project.

## Creation

1.  From the **Content Drawer**, click **Add > Physics > Physical Material** or right-click in the **Content Drawer > Physics > Physical Material**.
    
    ![ Click Add, Physics, Physical Material or right-click in the Content Drawer, Physics, Physical Material from the Content Drawer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/749304fe-7ef1-4660-8ac8-bb6118fba9af/new-physical-material.png)
2.  Double click the **NewPhysicalMaterial** to edit its properties.
    
    ![Double click the NewPhysicalMaterial](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a9b0d48-dbaf-48cd-9e82-de1a0f0a8b5f/physical-material-properties.png)
3.  Adjust properties.
    
    ![Adjust properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/387e0f43-6d1b-4a1b-8af6-9b8e692dbd59/adjust-properties.png)
4.  Click **Save**
    
    ![Click Save](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/542b825b-6f0b-48b9-8337-093831157cf9/icon-save-asset-40x.png)

See the [Physical Material Reference](/documentation/en-us/unreal-engine/physical-materials-reference-for-unreal-engine) for information on the properties of the Physical Material.

### Surface Type

By default, Unreal Engine 5 supports 62 Surface Types, which can be labeled as anything you desire, stored in your project's `DefaultEngine.ini`, which can be found in `YourProjectRoot\Config\DefaultEngine.ini`.

## Usage

### Material

1.  Open or create a new material.
    
    ![Open or create a new Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/738fc4a7-1745-46b6-a71c-62d7faceae44/physical-material-material-01.png)
2.  Select the main material node.
    
    ![Select the main material node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/369a22a2-c13a-4931-b287-12195860606b/physical-material-none.png)
3.  Change the **Physical Material**.
    
    ![Change the Physical Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b41c9fba-4863-4299-b03b-58cf680d1b75/physical-material-glass-2.png)

### Material Instance

1.  Open or create a new **Material Instance**.
    
    ![Open or create a new Material Instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a46c452-6acc-42c6-9164-4ef8401718c9/physical-material-material-instance-01.png)
2.  Change the Physical Material.
    
    ![Change the Physical Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d00be0c9-7762-4ba5-8116-28d054cc6646/basic-material.png)

### Physics Asset (Skeletal Mesh)

When adjusting the Physical Material for a **Physics Asset**, it is best to start by assigning the most commonly used Physical Material to all of the **Physics Bodies** in the Physics Asset.

1.  Double-click a **Physics Asset** in the **Content Drawer** to open it in the **Physics Asset Editor**.
    
    ![Double-click a Physics Asset in the Content Drawer to open it in the Physics Asset Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a8db4e8-270c-4027-b8aa-53cb1160d4c8/physics-asset.png)
2.  In the Physics Asset Editor, select a Physical Material from the **Physical Material** dropdown in the toolbar. ![Select a Physical Material from the Physical Material dropdown in the toolbar in the Physics Asset Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5f468ca-d3f8-4054-bdbc-e684349220bc/physical-material-dropdown.png) 

If specific Physics Bodies need differing Physical Materials, you can then adjust them individually.

1.  Double-click a **Physics Asset** in the **Content Drawer** to open it in the **Physics Asset Editor**.
2.  Select a **Physics Body**.
3.  In the Details pane, in the Physics Category, change the **Simple Collision Physical Material**.

![Physical Material Physics Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ccd68f6-ea73-4830-ae3b-e4909255ddf4/physical-material-physics-asset-04.png)

The default behavior for Physics interactions with Skeletal Meshes is to only interact with its associated Physics Asset, so the Skeletal Mesh's material's Physical Material will not be used.

With Physics Assets, though you are setting the Simple Collision Physical Material, when you trace against a Physics Asset, you will need to do a complex trace and the complex trace will return the Physical Material listed in the Simple Collision Physical Material property of the hit Physics Body.

### Static Mesh

**Static Meshes** have both **Simple Collision** (the Physics Bodies that you create in your 3D art package or the StaticMesh Editor) and **Complex Collision** (per poly collision) which can be composed of several different materials each with their differing Physical Materials.

| Collision | Physical Material Order |
| --- | --- |
| **Simple** | When any collision or trace uses Simple Collision, it will reference the Physical Material on the StaticMesh that is set in the StaticMesh Editor, or if the *Phys Material Override* on the StaticMesh Actor is set to something other than `None`, it will use what is listed in that property. |
| **Complex** | When any collision or trace uses Complex Collision, it will reference the Physical Material on the Material or Material Instances applied to the StaticMesh Actor, or if the Phys Material Override on the StaticMesh Actor is set to something other than `None`, it will use what is listed in that property. |

To set the Simple Collision Physical Material for a StaticMesh:

1.  Double Click a **Static Mesh** in the **Content Drawer** to bring up the **Static Mesh Editor**.
    
    ![Double Click a Static Mesh in the Content Drawer to bring up the Static Mesh Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7cfb69f-37ef-401e-84c3-611eb20e97c5/physical-material-static-mesh-editor-01.png)
2.  Change the **Simple Collision Physical Material** property in the **Static Mesh Settings** category to the desired Physical Material.
    
    ![Change the Simple Collision Physical Material property in the Static Mesh Settings category to the desired Physical Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51360c5a-a641-4524-8ec9-13e2585713fb/physical-material-static-mesh-editor-02.png)
3.  Click **Save**
    
    ![Click Save](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08e01969-169f-4742-bfa1-95353ba45bb7/icon-save-asset-40x.png)

### Misc

![The Phys Material Override property exists on everything with a Physics category](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e274376f-9ca0-4cb9-85d2-44a6cd077a28/physical-material-override.png)

The *Phys Material Override* property exists on everything with a **Collision** category. This can be used to completely override Simple Collision Physical Materials on an Actor or Component with the selected Physical Material.

-   Overriding a StaticMesh's simple collision Physical Material.
-   Since Skeletal Meshes Physics Assets always return Simple Collision, you can use this to override all Physical Materials on a placed Skeletal Mesh Actor.

This does not affect Complex Collision traces.
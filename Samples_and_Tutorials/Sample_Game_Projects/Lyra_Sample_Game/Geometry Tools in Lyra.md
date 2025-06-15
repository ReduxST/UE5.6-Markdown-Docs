# Geometry Tools in Lyra

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/lyra-geometry-tools-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/lyra-geometry-tools-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:31

---

**Geometry Scripting** is a new Experimental plugin introduced in Unreal Engine 5 which provides a base **Actor** class for **Procedural Mesh Actors** (**GeneratedDynamicMeshActor**) and a library of Blueprint functions that can be used to generate that Actor's mesh. For example, the simple Blueprint displayed below results in a **Parametric Box** object that can be resized using Width / Depth / Height Blueprint variables exposed in the Actor's **Details** panel.

![geometry-scripting-tool-being-used-in-the-editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d7a1ebe-d3b1-49c5-adc1-fb3eb5fafa9d/placebox.gif)

The **Geometry Script Library** includes a large set of over 160 functions that include various types of shape generators, extrudes and revolves, mesh booleans, and utility functions for configuring material assignments and copying to and from Static Mesh Assets.

## Tool Library

Lyra Tech Artists used procedural mesh generation in **Blueprint Actors** to build a library of parametric level design elements as Blueprint Actors. These Blueprints are called **Tools (Blueprint Actor Tools)** in the Lyra project, and are found in the **Content** **directory** of the **Tools subfolder**. To use one of the Tools, drag it into the Level, and then configure the part to your liking by using the settings in the Actor **Details panel**.

We settled on "Tool" to describe these parametric objects in this document. However, Generator and Generated Mesh have also been used in some places in the Blueprint user interfaces.

For example, in the image below-left is the default **B\_Tool\_AdvancedWindow**, and then two other variations built by changing the options / parameters / materials on the Actor.

Lyra was built using the **Blueprint Actor Tools** listed in the table below:

| Blueprint Actor Tool | Description | Image |
| --- | --- | --- |
| B\_ASimpleCubeTool B\_GeneratedTube B\_GeneratedTube\_Advanced B\_Tool\_AdvancedWindow | Useful for creating meshes that have square corners on the outside and rounded corners on openings. and where the opening can be dragged around with a 3D Gizmo. This includes a Mirror and custom boolean cutting plane options. | ![adavanced-window-example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae807cb8-72ea-449d-9976-c5916515cbe3/advancedwindow.png) |
| B\_Tool\_CornerExtrude B\_Tool\_CornerExtrude1 | Creates a corner mesh with a uniform Width and uniform corner Radius. | ![corner-extrude-example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bcabc8a4-9537-4dab-b6e3-f61b50a1aa19/cornerextrude.png) |
| B\_Tool\_Panel\_BGM | Creates a mesh with Corner Radius control. This is a boolean (add / subtract / intersection) inset mesh of uniform width and with a unique material ID. Mesh dimensions are controlled with a draggable 3D gizmo, and contains a Mirror and custom boolean cutting plane options. | ![tool-panel-example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6da74249-c56d-4683-b6e2-9658b928b87a/toolpanel.png) |
| B\_Tool\_RampMakerControl\_BGM | A user-defined tool that consists of a simple rectangular box with Width, Height, and Depth controls along a spline. You can edit and view the Spline points in Game View mode (G-key toggle). Using Alt+Left Mouse to drag will append a new spline point to the end spline point. This Tool bakes out a single mesh. | ![ramp-maker-control-example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a815699a-96b9-4d3f-b5cc-6104bb6b3b79/rampmakerbgm.png) |
| B\_Tool\_Repeater | Distributes an array of boxes with user defined dimensions along an editable spline, an example of this can be seen with **B\_Tool\_Stairs\_BGM** | ![stairs-example-tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4555ab86-6eff-4392-99df-84f15c838aa2/toolrepeater.png) |

## Baking To Static Mesh Assets

When using the **Parametric** **Tool Actors**, a Level Designer can efficiently prototype level layouts, and can use them in **PIE** (**Play-in Editor**) to do basic tests. The **Dynamic Mesh Actor** used as the basis for these Blueprints does not use the traditional UE StaticMesh Asset. Instead, It uses a **Dynamic Mesh Component**, a new type of component designed for efficient editing.

The Dynamic Mesh Component provides rapid parametric design, however it does not support UE Rendering features like [Lumen](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) or [Nanite](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine). Additionally, the Dynamic Mesh Component Actor does not support Instancing, meaning that a duplicate of a Tool is a completely separate mesh. Changing the parameters of the original Tool does not affect the duplicate.

This can be challenging when designing a level if the same element is used in multiple places, because the only option for the designer is to manually update the settings on each duplicate. Therefore, adhere to the standard UE rendering architecture and design workflows, as the Blueprint Tools Actors need to be baked to Static Mesh Assets.

To support this, the Tool Actors have a **Generation Management** section in their Details panel, which includes two action buttons, **Generate New Static Mesh** and **Bake to Static Mesh**.

To bake out a Static Mesh version of the Tool instance, click the **Generate New Static Mesh** button. This automatically creates a new StaticMesh Asset at the path defined by the other settings on the Actor.

As an example, in the image above, the Asset is created in the `ShooterMaps/Content/Meshes/` Generated folder directory, and given an auto-generated name prefixed with **Mesh\_.**

Instances of this Static Mesh Asset can now be placed in the level. When the **Generate** button is clicked, the Tool Actor keeps track of which Assets were created and stored in the **Target Static Mesh** field. The user can then click **Bake to Static Mesh** to update that Static Mesh Asset at any time. This makes it easier to edit the Instances in the level by editing the Tool.

When referring to the word "Instance" in this context, we are referring to an Actor in the level that references a Static Mesh Asset, for example an "Instance of the Asset", and *not* an **Instanced Static Mesh Component** instance.

In the gif below, you can observe a demonstration of this process. We begin by initially creating a new Asset from the **Generate New Static Mesh** button, then we place three separate instances, and update the Asset by editing and re-baking the Tool.

![generating-static-mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07921806-a621-4360-bc2b-e74c96e61d65/workflow.gif)

The Generate New Static Mesh and Bake To Static Mesh functionality is implemented in Blueprints using Geometry Scripting. The functions are located inside the Blueprint Subclass of a **Generated Dynamic Mesh Actor** called **BakedGeneratedDynamicMeshActor**.

You can navigate to this Dynamic Mesh Actor in the `/Content/Tools/BakedGeneratedMeshSystem` directory folder. All the Tool Blueprint Actors are subclasses of this base class.

## Non-Destructive Level Design

The **Bake to Static Mesh** functionality described in the section above provides an efficient way to do **non-destructive Level Design** using the parametric mesh Tools. The Level Designer configures a level element using a Tool, then bakes it to an Asset to place instances in the level. The baked asset supports Nanite and Lumen, efficient Instanced rendering, and all other Static Mesh features in UE.

The one drawback of this system is that the Tool Actor must exist in the level, as a sort of "template" for the Static Mesh Asset / Instances. If the Tool is deleted, the settings would be lost. One option to do this is to set the Tool to be hidden, however this means you have to explicitly show it to do any editing, then hide it again afterwards. Another option is to place the Tools somewhere in the level that is "out of the way". In Lyra, this is done by placing the Tools below the actual level.

This is why when you open the **L\_Expanse** map, for example, you may discover that there are many apparently-random objects placed below the main level. These are the Tools that were used to generate and edit the level Assets. Why they appear to have no coherent organization is explained in the following section.

## Swapping Between Tools and Assets

The Asset Baking system described above provides for non-destructive level design parametric Tool Actors, but still comes with some challenges. Specifically, finding the Tool used to author a particular Asset placed in the level is difficult. Additionally, it is not efficient to make tweaks to a placed Asset by iteratively editing and re-baking a Tool that is in some other location.

To support better workflows, a system for swapping between the placed Static Mesh Asset (Static Mesh Actor) and the Tool Actor was built entirely in Blueprints. This system uses the **Actor Action Utility** Blueprints, which provide the capability for creating Blueprint operations that appear in a right-click context menu in the Editor.

For additional information, refer to [Scripted Actions](/documentation/en-us/unreal-engine/scripted-actions-in-unreal-engine).

There are two Action Utilities located in the `/Content/Tools/BakedGeneratedMeshSystem/EditorActions/` folder.

The first, **SwapGeneratedActor\_ToSM** is used to replace a Tool Actor with an instance of its Baked Static Mesh Asset. This Editor action adds an item **Swap to Static Mesh** to the context menu for the **BakedGeneratedDynamicMeshActor** subclasses. When it is run, the following process occurs:

1.  Checks if a baked Asset is already configured in the Actor. If no baked Asset already exists, then automatically run the Generate New Static Mesh and Bake to Static Mesh operations on the Tool Actor.
    
2.  Create a new **Baked Static Mesh Actor** and assign the baked Asset.
    
3.  Set the **Transform** on the new Actor to be the same as the current Transform on the Tool.
    
4.  Copy the **Name**, **Data Layer**, and **Outliner** position from the Tool Actor to the new Static Mesh Actor.
    
5.  Reposition the Tool Actor to be below the Level.
    
6.  Append a prefix to the Tool Actor's name in the Outliner
    

This name is configured to be **ZZSTORED\_** in Lyra.

The second Editor Action, **SwapGeneratedActor\_FromSM**, is used to swap from the placed Static Mesh instance (**Baked Static Mesh Actor**) to the source Tool Actor. This adds a **Swap to Generated Mesh** action to the context menu for Baked Static Mesh Actors. When you run this Action, the StaticMesh Actor is deleted, then the transform on the Tool Actor is updated to take the position of the deleted StaticMesh Actor.

You can make parametric edits, update the baked Asset, and then run the **Swap to Static Mesh** Action to switch back to a Static Mesh.

![generate-mesh-animated-process](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42e9398a-ab19-4ef4-bb0a-922cec39c217/generatemeshworkflow.gif)

## Source Keys and Generated Mesh Cold Storage

Level Designers use the Tools, Baking functionality, and Swapping actions described above to create and edit the level. Now, you can explore the technical details about how the swapping is implemented entirely in Blueprints.

As mentioned before, the **Baked Generated Dynamic Mesh Actor** keeps track of its current baked Asset in the **Target Static Mesh** field. When the Asset is generated, a new **Source Generator Key** string is randomly generated too. This string is displayed in the Actor **Details panel**.

  

These fields can be manually initialized in addition to using the Generate New Static Mesh button.

The Static Mesh Actors created by the Swap to Static Mesh Action are a Blueprint subclass of the base StaticMeshActor called **Baked Static Mesh Actor**. This subclass has an additional field for the **Source Generator Key**. When a new Baked Static Mesh Actor is created by the Action, its Source Generator Key is set to the same string as the Tool it is based on.

This Source Generator Key string is the basis for the Swapping system. When given a Baked Static Mesh Actor, you can use the Key to determine which Tool it is derived from. Additionally, you can find all the Baked Static Mesh Actor instances when given a Key from the Tool.

One method to search is to iterate through all Actors. We added another Blueprint object to the system to centralize this information and provide a place for various utility functions (like those searches). This is the **GeneratedMeshColdStorage** Blueprint, which is an Editor Utility Actor.

One of these Actors must be placed in the level for the swapping system to function. It has no geometry and no effect on the game. It manages an array of known Tool Actors, in the **Stored Actors** list, as shown below.

The Generated Mesh Cold Storage object has two public Blueprint functions, **Store Actor** and **Extract Actor**. These are used by the Swap to and from Actions to store or restore the Tool Actors.

## New Level Setup for the Tool / Asset Swapping System

Below are step-by-step instructions for setting up a new level with the baking / swapping system described above.

1.  Drag an instance of the **Tools/BakedGeneratedMeshSystem/GeneratedMeshColdStorage** Asset from the Content Browser into the level.
    
2.  Drag an instance of **Tools/B\_Tool\_AdvancedWindow** Asset into the level.
    
3.  Select this new Actor (**B\_Tool\_AdvancedWindow**).
    
4.  Scroll down to the **Generation Management** section of the **Actor Details** panel, and click **Generate New Static Mesh**.
    
5.  Right-click on the Actor in the level and select **Swap to Static Mesh** from the **Scripted Actor Actions** submenu in the Actor context menu. This will replace the Tool Actor with a Static Mesh Actor.
    
6.  Hold the Alt key and drag on the 3D gizmo in the level to make a duplicate of the selected Static Mesh Actor.
    
7.  Select one of the two Static Mesh Actors, right-click, and select **Swap to Generated Mesh** from the **Scripted Actor Actions** submenu in the Actor context menu. This will replace the StaticMesh Actor with the Tool Actor.
    
8.  Scroll up to the **Wall** section in the Actor Details Panel and increase the **Wall Width**. This will only affect the Tool Actor.
    
9.  Scroll down to the **Generation Management** section of the **Actor Details** panel, and click **Bake to Static Mesh**. The Static Mesh Actor will update to look the same as the Tool Actor.
    
10.  Right-click on the Actor in the level and select **Swap to Static Mesh** from the **Scripted Actor Actions** submenu in the Actor context menu. This replaces the Tool Actor with a Static Mesh Actor again.
    

## Swapping System Common Issues

The Asset / Tool swapping system described above is included in the **Lyra L\_Expanse** level. Most level elements are based on Tools which exist in the level, and you can experiment with non-destructive level design by swapping between the Tool and the placed Assets.

During the course of Lyra development, we observed several frequent errors in usage which are useful for you to be aware of.

-   If the generated Static Mesh Assets are placed manually, instead of the swapping Actors, the resulting Actors will become Static Mesh Actors, not Baked Static Mesh Actors. In this situation, the Actor does not have the Source Key field, therefore there is no link to the source Tool, and the Swap to Static Mesh context menu Action will not be available.
    
-   The Swap to Static Mesh Action does not automatically bake the Tool to the Asset, except on the first invocation. You must explicitly click the Bake button, otherwise the Tool and baked Asset can become out-of-sync. You can fix this by swapping back and baking.
    
-   Once a Tool has been baked to an Asset, and that Asset is used in the level, do not use the Generate New Static Mesh button on that Tool again. Doing so generates a new Source Key, and any existing Asset instances then have a Source Key that doesn't refer to any existing Tool (it will not be possible to swap back).
    
-   If a Tool is duplicated in the level to make a variation, then both copies have the same Source Key and the same target Static Mesh Asset. In this case, Generate New Static Mesh **must** be run to resolve this collision.
    
-   The generated Static Mesh Asset does not have scope of the Source Key, only the Static Mesh Actors do. Therefore, if all Actors using an Asset in the Level are deleted, the link to the source Tool is lost (the Tool will still exist in the level, but it will be difficult to find). To fully delete an Asset, the Tool must be deleted first, and then the placed Actors, and then the Asset.
    
-   If a Tool is deleted, its settings are irrevocably lost. This does not affect any placed instances, however there is no way to recover the deleted Tool to further update the instances.
    
-   The Source Key fields are strings, and can be manually edited in the details panel. If this is done, the link between Asset instances and the Tool will be lost. However, this means that broken links can be repaired by manually updating the strings to be the same in the Tool and Instances.
    

We plan to improve on these limitations in future iterations of the Lyra sample.

## Additional Notes

**Assigned Materials**: When swapping between Tools and Asset Instances, in addition to copying the world Transform, the assigned Materials are also copied. This provides for different Instances of the Asset in the level to have different Material assignments while still providing for swap to / from the Tool, and the Tool (when "swapped in") will reflect the correct Materials. However, any Material assignments made directly on the Tool will be lost.

**Actor Settings:** Asset / Instance Swapping also preserves Data Layers, position in the Outliner, and Actor names where possible. it does try to hide / show the Tool Actors, in addition to moving them below the level. However, Unreal Editor does not save this hide / show state, so it is reset when the level is reloaded (this is why the Actors are visible below the level).

This copying is done from the low-level engine APIs that copy Actor properties, therefore many other Actor settings will be copied back and forth. However, it is not possible to copy Actor properties that do not exist on both objects. To handle such a case, the setting must be explicitly handled in the Copy To / From Actions.

**Cooking/Game Builds**: In UE 5.0, the Generated Dynamic Mesh Actor base class used for the Tools is Editor-Only. This means that placed Tool Actors will be visible in PIE, but they will not be included in the built cooked game.
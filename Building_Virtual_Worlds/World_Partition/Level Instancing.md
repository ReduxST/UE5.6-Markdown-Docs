# Level Instancing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/level-instancing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/level-instancing-in-unreal-engine)  
**Processed:** 2025-06-14 16:33:06

---

Level Instancing is a level-based workflow designed to improve and streamline the level editing experience. Use the Level Instancing workflow with one or more Actors to create Level Instances that can be placed down and repeated across your world.

This workflow provides the following benefits:

-   Level Instances are edited in-context, letting you immediately see how your changes will affect your world. Changes made to one instance are repeated across all instances when saved.
    
-   Quickly create copies of any static mesh arrangement as a template - anything from points of interest, buildings, and gameplay setups.
    
-   Production-ready process used in the creation of the [City Sample](https://www.fab.com/listings/4898e707-7855-404b-af0e-a505ee690e68) and [Valley of the Ancient](https://www.fab.com/listings/0c19880e-21bd-42ba-8287-1caccc3951b1) demos created by Epic Games.
    

The City Sample skyline.

Though it is possible to use **Level Streaming** without using **World Partition**, Level instances do not automatically have streaming management or streaming strategies outside of a World Partition main world.

## Creating Level Instances

There are two types of Level Instances:

-   **Level Instances**: Collections of Actors that are combined to create a sublevel. Multiple instances of a sublevel can be repeated across your project, something not possible in previous versions of Unreal Engine. Use this type for points of interest and standalone gameplay setups.
-   **Packed Level Blueprints**: **Static Mesh** assets that are combined to create a single **Blueprint Actor** that is optimized for rendering. The Static Meshes are replaced with an instance of the **Packed Level Blueprint** that is linked to a **Packed Level Actor**. This type is recommended for static buildings and dense visual setups like the mega assemblies used in Valley of the Ancient.

### Creating a Level Instance

New Level instances are generated from selected Actors and can be created in either the **Viewport** or the **Outliner**.

After selecting the Actors, right-click one of them to pull up the context-sensitive menu. In the menu, navigate to the **Level** option and select **Create Level Instance**.

Creating a Level Instance with the context menu.

You will see a dialog box with the following settings:

The new Level Instance dialog box.

| Setting | Description |
| --- | --- |
| External Actors | Enable external Actors to use the One File per Actor system. For more information, see the [One File Per Actor](/documentation/en-us/unreal-engine/one-file-per-actor-in-unreal-engine) documentation. |
| Pivot Type | 
The type of **Pivot** the Level instance will have:

-   **Center Min Z**: Pivot will be located at the center of the Level Instance at the lowest Z value.
-   **Center:** : Pivot will be located at the center of the Level Instance.
-   **Pivot Actor**: If an Actor is selected as the Pivot, use this dropdown to select which Actor will be the pivot point for the Level Instance.



 |
| Pivot Actor | If Actor is selected as the Pivot, use this dropdown to select which Actor will be the pivot point for the Level Instance. |

Once you have selected your settings and click **Ok**, you are asked to save the new Level Instance.

This process creates a new **Level Instance** Actor in the level, which replaces the previously selected Actors. This Actor represents the Level that was just created and all transforms applied to this Actor are applied to the Level Instance.

The new Level Instance Actor replaces the assets in the level.

The Actors that make up the Level Instance are still visible in the Outliner but are now a child of the Level Instance Actor and are not selectable.

The assets are now children of the Level Instance Actor.

### Creating a Packed Level Blueprint

Like Level Instances, Packed Level Blueprints are generated using selected Actors and can be created by right clicking in the **Viewport** or the **Outliner**.

After selecting the Actors, right-click one of them to pull up the context-sensitive menu. In the menu, navigate to the **Level** option and select **Create Packed Level Actor**.

Creating a Packed Level Blueprint with the context menu.

You will see the same dialog box as above. Select your settings and click **Ok**. You are then asked to save the new Level and the new Packed Level Blueprint.

This process creates a new **Packed Level Actor** in the level associated with your Packed Level Blueprint.

## Editing Level Instances

Once created, Level Instances and Packed Level Blueprints can be copied and placed across your world.

### Editing a Level Instance

To edit your Level Instance, select one of them in the Viewport and right click to open the menu, navigate to the **Level** option and select **Edit**. You can also click the **Edit** button in the **Details** panel.

This grays out all other Actors in your World, making it easier to edit your Level Instance in context.

All other Actors are grayed our while editing a Level Instance in the Viewport.

When you finish, select the Level Instance Actor in the **Outliner** and click **Commit Changes** in the **Details** panel.

Clicking Commit Changes in the Details Panel saves your Level Instance changes.

To leave editing without committing your changes, press **Esc** twice.

Any changes made to a Level Instance propagate to all copies of the Level Instance in your world.

### Editing a Packed Level Blueprint

To edit your Packed Level Blueprint, locate an instance of it in the **Outliner** and click **Edit**. You can also locate the Blueprint in the **Content Browser** and double click. This will open the Blueprint Editor window.

The Blueprint Editor window showing the selected Packed Level Blueprint.

Like Level Instances, any changes made to the Packed Level Blueprint propagate to all other copies of it in your world.

### Breaking Level Instances

Breaking a Level Instance removes the Level Instance Actor or Packed Level Actor from the world and replaces it with the original assets used to create them. It does not delete the Level Instance or Packed Level Blueprint from the Content Browser.

This operation cannot be undone.

## Level Instances at Runtime

### Data Layers

Level Instances and Packed Level Blueprints support [World Partition: Data Layers](/documentation/en-us/unreal-engine/world-partition---data-layers-in-unreal-engine).

The Actors contained within the Level Instance inherit the Data Layer assigned to its **Level Instance** Actor by default. Actors within the Level Instance also support additional Data Layers.

For example, a Level Instance that contains the assets to create a house point of interest can be assigned to a Neighborhood data layer. The Level Instance can also contain holiday themed items that are assigned to different holiday data layers that are only visible when that data layer is enabled.

### Level Streaming Modes

Level Instances and Packed Level Actors use the World Partition settings to define their streaming behavior, either Embedded Mode or Level Streaming Mode.

These settings are not editable and are included here for reference.

#### Embedded Mode

When using **Embedded Mode**, Level instances that use the [One File Per Actor (OFPA)](/documentation/en-us/unreal-engine/one-file-per-actor-in-unreal-engine) system are discarded and their Actors are added to the World Partition grid at runtime. This is the default runtime mode and the suggested method of streaming Level content. This also makes Level instances exist within the editor only.

Some Actors that do not use OFPA are lost at runtime when using Embedded Mode. For example, the AWorldSettings object of an embedded Level Instance does not exist at runtime as this is a non-OFPA Actor. It is your responsibility to avoid relying on these Actors or to use Level Streaming mode when needed.

#### Level Streaming Mode

Level instances that do not use OFPA cannot be embedded in the World Partition grid and instead use standard Level streaming at runtime. This means that when the **Level Instance** Actor is loaded through its owning World Partition runtime cell, it loads the associated Level.

This method of Level streaming has an added runtime cost as it adds more Levels to the stream. It is not recommended to use a high density of Levels that use this streaming mode due to the performance impact.

Embedded mode with [World Partition: Data Layers](/documentation/en-us/unreal-engine/world-partition---data-layers-in-unreal-engine) is a great way to approximate what could previously be done with dynamically loaded Levels.
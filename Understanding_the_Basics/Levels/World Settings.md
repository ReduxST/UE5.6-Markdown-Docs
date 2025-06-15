# World Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/world-settings-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/world-settings-in-unreal-engine)  
**Processed:** 2025-06-14 17:05:10

---

Each Level can have unique settings applied to it from the **World Settings** panel. You can use this panel to do everything from making sure the right **Game Mode** is activated when you play the Level to adjusting how global illumination works for that Level.

To open the World Settings panel, from the main menu, go to **Window**, then select **World Settings**.

Default location of the World Settings panel. Click the image for full size.

The **World Settings** panel docks next to the **Details** panel in the editor UI by default. From here, you can now specify the settings for the current Level.

Use the **Search** box to quickly find a setting.

![Searching for a property in World Settings by name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82de9ad7-aa25-4e39-9fef-164ab79afe03/world-settings-search.gif)

World settings are split into groups based on which aspects of your Level they influence. Some of these settings are general, such as those affecting the Game Mode and navigation. Other, more specialized groups of settings are used to configure your game's lighting, audio, physics, and so on.

You can adjust the following groups of settings:

## Precomputed Visibility

Precomputed visibility volumes reduce rendering thread time at the cost of runtime memory. This helps optimize your game's performance when you work with smaller levels or target a platform where dynamic occlusion culling may be limited depending on hardware, such as mobile. It doesn't scale well for larger, more complex environments.

For more information, see [Precomputed Visibility Volumes](/documentation/en-us/unreal-engine/precomputed-visibility-volumes-in-unreal-engine).

## Game Mode

This is where you select and configure a Game Mode for your current Level. Game Modes define the rules of your game, such as players number, score, or win conditions. You can choose from existing Game Modes that come with the project template you used, or create custom ones.

After you select a game mode from the **GameMode Override** drop-down, you can configure settings specific to it.

For more information, see [Setting Up a Game Mode](/documentation/en-us/unreal-engine/setting-up-a-game-mode-in-unreal-engine).

## Lightmass

In this section, you specify Lightmass settings, such as the detail and quality of indirect lighting and whether to use ambient occlusion (that is, simulating soft shadows from indirect lighting, which can add depth to your scene).

To learn more about Lightmass, as well as the different settings you can configure, see [Global Illumination](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine).

## World

These settings affect core aspects of your game world, like level bounds, navigation systems, and the depth an Actor can fall to before it is destroyed.

For more information on different areas inside this section, see:

-   [World Composition](/documentation/en-us/unreal-engine/world-composition-in-unreal-engine)
    
-   [Level Streaming Volumes Reference](/documentation/en-us/unreal-engine/level-streaming-volumes-reference-in-unreal-engine)
    

## Physics

Use this section to override the World Gravity, which affects certain Z-axis actions, such as how high up a character can jump or the fall speed of objects.

You can also specify more advanced settings here, such as a default physics volume class and a physics collision handler class.

To learn more about physics in Unreal Engine 5, see [Physics](/documentation/en-us/unreal-engine/physics-in-unreal-engine).

## Broadphase

This section contains settings for Broadphase collision, which is a feature of NVIDIA's PhysX system. You can specify whether to use Broadphase client- or server-side.

Unreal Engine implements Multi-Box Pruning, which splits up the Broadphase into a grid of boxes whose settings you can control. The **MBPBounds** and **MBPOuter Bounds** sections control the bounds for the multibox.

The space inside **MBPBounds** is divided by the **MBPNumSubDivs** value to create the grid. For example:

-   If MBPNumSubDivs = 2, this creates a grid of 4 cells (2 x 2).
    
-   If MBPNumSubDivs = 3, this creates a grid of 9 cells (3 x 3).
    

If a physically active object falls outside the bounds specified by the **MBPOuterBounds**, it is no longer considered for collision. Enabling the **Use MBPOuter Bounds** option creates four specialized cells at the edges of the multibox grid.

To learn more about this system, see NVIDIA's documentation on [Rigid Body Collision](https://docs.nvidia.com/gameworks/content/gameworkslibrary/physx/guide/Manual/RigidBodyCollision.html).

## HLOD System

In this section, you can enable Hierarchical Levels of Detail (HLODs).

HLODs can replace multiple Static Mesh Actors with single, combined Static Mesh Actor at long view distances. This helps reduce the number of Actors that need to be rendered for the scene, increasing performance by lowering the number of draw calls per frame.

To learn more about working with HLODs, see [Hierarchical Level of Detail](/documentation/en-us/unreal-engine/hierarchical-level-of-detail-in-unreal-engine).

## World Partition Setup and World Partition

**World Partition** is a new data management and distance-based level streaming system that provides a complete solution for large world management. The system removes the previous need to divide large levels into sublevels by storing your world in a single persistent level separated into grid cells, and provides you with an automatic streaming system to load and unload those cells based on distance from a streaming source.

To learn more about World Partition and how to configure its settings, refer to the [World Partition](https://docs.unrealengine.com/5.0/en-US/building-virtual-worlds/world-partition/) section of the Unreal Engine 5 Early Access documentation.

## Navigation

Configure the navigation grid used in your Level.

## VR

Use the **World to Meters** variable to adjust the scale of your virtual world. Increasing or decreasing this number will make the user feel larger or smaller in relation to the world around them. This setting is expressed in Unreal Units (UU). Inside of UE4, 1 Unreal Unit (UU) is equal to 1 Centimeter (cm).

Assuming your content was built with 1 Unreal Unit = 1 cm, setting **World To Meters** to **10** will make the world appear to be very large, while setting World To Meters to **1000** will make the world appear very small.

To learn more about scaling your VR experience, see [VR World Scale](/documentation/en-us/unreal-engine/xr-best-practices-in-unreal-engine#vrwordscale).

For a general introduction to XR development in UE5, see [XR Development](/documentation/en-us/unreal-engine/developing-for-xr-experiences-in-unreal-engine).

## Rendering

In this section, you can configure several settings related to distance field ambient occlusion, as well as dynamic indirect shadows.

For more information, see [Distance Field Ambient Occlusion](/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine).

## Audio

Use the settings in this section to configure default sound behaviors in your Project, such as volume, reverb, and fade time.

To learn more about audio and sound in Unreal Engine 5, see [Working with Audio](/documentation/en-us/unreal-engine/working-with-audio-in-unreal-engine).

## Tick

**Ticking** refers to running a piece of code or Blueprint script on an Actor or Component at regular intervals, usually once per frame. Ticking is generally enabled separately for each Actor or Component.

Unless your game is running legacy code that specifically requires the per-frame `Tick()` update function to run before the one-time initialization `BeginPlay()` function, you should disable this option to make sure that objects tick correctly.

To learn more about Ticking and Actor behaviors, see [Actor Ticking](/documentation/en-us/unreal-engine/actor-ticking-in-unreal-engine).

## AI

In this section, you can enable Unreal Engine 4's Artificial Intelligence (AI) system.

To learn more about this system, see [Artificial Intelligence](/documentation/en-us/unreal-engine/artificial-intelligence-in-unreal-engine).

## Cooking

**Cooking** is part of the process of building your game and deploying it to a platform, such as PC or mobile These settings affect how the content in your Scene will be included in your built game.

To learn more about this process, see [Packaging and Cooking Games](/documentation/en-us/unreal-engine/packaging-and-cooking-games-in-unreal-engine).
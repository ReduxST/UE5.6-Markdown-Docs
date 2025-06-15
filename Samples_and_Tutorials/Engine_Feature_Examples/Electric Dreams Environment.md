# Electric Dreams Environment

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/electric-dreams-environment-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/electric-dreams-environment-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:53

---

In the **Electric Dreams Environment** sample project, you can explore the environment demonstrated during the State of Unreal keynote at the 2023 Game Developers Conference. This demo offered a first look at several new, experimental features available in Unreal Engine 5.2, including:

-   [Procedural Content Generation framework](/documentation/en-us/unreal-engine/procedural-content-generation--framework-in-unreal-engine) (PCG)
-   [Substrate material authoring system](https://dev.epicgames.com/community/learning/courses/92D/unreal-engine-substrate-materials)
-   Unreal Engine's latest physics developments

![Electric Dreams Environment](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e0a8610-082f-46ce-898a-7934e52db443/river-bed.png "Electric Dreams Enviroment")

This demo also showcases several existing Unreal Engine 5 features, such as:

-   [Lumen](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine)
-   [Nanite](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine)
-   [Soundscape](/documentation/en-us/unreal-engine/soundscape-in-unreal-engine)

This environment sample is a learning resource to help you understand how the Electric Dreams world was built by incorporating both traditional and procedural workflows directly within Unreal Engine using the Procedural Content Generation framework. You can also explore other Unreal Engine features such as Substrate through the Opal Material example, Audio, Fluid Simulation Content, and more.

## Setup

To install the Electric Dreams Environment sample project, follow these steps:

1.  Access the [Electric Dreams Environment sample](https://fab.com/s/7ee8c5704aaa) from **Fab** and click **Add to My Library** for the project file to show in the **Epic Games Launcher**.
    1.  Alternatively, you can search for the sample project from the Fab plugin for UE.
2.  From the **Epic Games Launcher**, go to **Unreal Engine > Library > Fab Library** to access the project.
    
    Sample projects only appear in **Fab Library** when you install the compatible engine version.
    
3.  Click **Create Project** and follow the on-screen instructions to download the sample and start a new project.

To learn more about accessing sample content and the Fab plugin for Unreal Engine, see [Samples and Tutorials](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine).

## Recommended System Specs

The Electric Dreams Environment sample is a graphically intensive project that requires a powerful video card to run at a stable framerate. We recommend that you install this project on a solid-state drive (SSD). [Nanite](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) and [Virtual Textures](/documentation/en-us/unreal-engine/virtual-texturing-in-unreal-engine) depend on fast read speeds for the best possible performance.

The recommended hardware specifications are as follows:

| **Recommended System Specs** | **Minimum System Specs** |
| --- | --- |
| 
-   12-core CPU at 3.4 GHz
-   64 GB of system RAM
-   GeForce RTX 3080 (equivalent or higher)
-   At least 10 GB VRAM



 | 

-   8-core CPU at 3.6 GHz
-   32 GB of system RAM
-   GeForce RTX 2080 (equivalent or higher)
-   At least 8 GB VRAM



 |

The Electric Dreams Environment sample requires DirectX 12 support and up-to-date graphics drivers.

On lower spec systems, you can adjust the resolution and the viewport screen percentage setting to get better performance. On the minimum spec, we recommend a resolution of 1080p with 50% screen percentage for the larger environments. You can set this in the **Viewport Options Menu** located in the upper-left corner of your editor viewport using the **Screen Percentage** slider.

![Change screen percentage in viewport options menu.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5caa5b70-bcb5-4516-a010-c080a8a40258/viewport.png "Viewport Options Menu")

Alternatively, you can use the console command `r.ScreenPercentage` to set this value at runtime. For example, `r.ScreenPercentage 50` sets the screen percentage to 50%.

## Navigating the Sample

When you open the Electric Dreams Environment sample, you are placed in the Startup level. The Startup level provides on-screen information for how to use this sample project as well as the sample's recommended system requirements.

The Electric Dreams Environment sample includes several levels. To open one of these levels, find the **Content Browser** and navigate to **Content > Levels**.

### Levels

The levels available in the Electric Dreams Environment sample are listed below in the following table:

| **Level Name** | **Description** |
| --- | --- |
| **ElectricDreams\_Env** | 
This level is the full Electric Dreams environment. This level includes both hand-crafted and procedural areas created with the PCG Framework. It also includes:

-   Soundscape procedural ambient sounds
-   Fluid simulation puddle
-   Substrate shader ball
-   Demo Sequences

**Resource Needs**: This level is a resource intensive, 4 kilometer by 4 kilometer World Partition level with steaming disabled.

**Content File Path**: `/Game/Levels/ElectricDreams_Env`



 |
| **ElectricDreams\_PCG** | 

This level is a procedural-only version of the Electric Dreams environment.

**Resource Needs**: This level is a resource intensive, 4 kilometer by 4 kilometer World Partition level with streaming disabled.

**Content File Path**: `/Game/Levels/PCG/ElectricDreams_PCG`



 |
| **ElectricDreams\_PCGCloseRange** | 

This level is a smaller extract from the ElectricDreams\_PCG level. This level only contains the procedural river bed and creek area, as well as the large cliff structure.

**Resource Needs**: This level is resource friendly.

**Content File Path**: `/Game/Levels/PCG/ElectricDreams_PCGCloseRange`



 |
| **ElectricDreams\_PCGLargeAssembly** | 

This breakdown level contains the large cliff structure dropped into the world during the GDC demo with all Assemblies used to build it.

**Content File Path**: `/Game/Levels/PCG/Breakdown_Levels/ElectricDreams_PCGLargeAssembly`



 |
| **ElectricDreams\_PCGDitchAssembly** | 

This breakdown level contains the ditch embankment wall rule applied to an open spline with all Assemblies used to build it.

**Content File Path**: `/Game/Levels/PCG/Breakdown_Levels/ElectricDreams_PCGDitchAssembly`



 |
| **ElectricDreams\_PCGForest** | 

This breakdown level contains the parametrized PCG forest over a small landscape patch.

**Content File Path**: `/Game/Levels/PCG/Breakdown_Levels/ElectricDreams_PCGForest`



 |
| **ElectricDreams\_PCGSplineExample** | 

This example shows how to leverage a single Assembly onto a procedurally generated path by augmenting the original Assembly through PCG Graph logic.

**Content File Path**: `/Game/Levels/PCG/Breakdown_Levels/ElectricDreams_PCGSplineExample`



 |

You can interact with all of the PCG tools present in every level listed above in the following ways:

-   Live in the **Unreal Editor**.
-   During **Play-in-Editor** (PIE).
-   Individually through the **Content Browser** in **Content > PCG > Graphs**.

Additional Text description actors are scattered throughout the main areas within the world as quick reference guides for things to look for.

![Text description actor in the world.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d0e6447-1ffc-4cca-be9e-bed989faad88/text-actor.png "Text Description Actor")

## Electric Dreams In-Game Controls

### Drone Controls

Drone controls are available in PIE and cooked builds for every level within this sample. The following table provides an overview of the drone controls:

| **Drone Action** | **Controller** | **Keyboard and Mouse** |
| --- | --- | --- |
| **Move Forward** | Left Joystick | W |
| **Move Backward** | Left Joystick | S |
| **Move Left** | Left Joystick | A |
| **Move Right** | Left Joystick | D |
| **Look** | Right Joystick | Mouse Move |
| **Altitude Up (Ascend)** | Right Trigger | E |
| **Altitude Down (Descend)** | Left Trigger | Q |
| **Speed Up** | Right Bumper | F |
| **Slow Down** | Left Bumper | R |

### Sequence Shortcuts

The Electric Dreams GDC demo sequences are available when exploring the ElectricDreams\_Env level. These sequences can be triggered using the following keyboard shortcuts:

| **Sequence Action** | **Keyboard** |
| --- | --- |
| **Fly-Through** | Shift + C |
| **PCG Mid Range** | Shift + V |
| **PCG Long Range** | Shift + B |
| **Stop Playing Sequence** | Spacebar |

## Procedural Content Generation in Electric Dreams

Learn more about how the Electric Dreams Environment sample project incorporates traditional and procedural workflows together in Unreal Engine.
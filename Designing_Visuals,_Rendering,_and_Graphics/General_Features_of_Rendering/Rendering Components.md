# Rendering Components

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-components-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-components-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:49

---

## Atmospheric Fog Component

**AtmosphericFogComponents** are used to create fogging effects such as clouds or ambient fog in a level. There are several settings that can be adjusted for this Component that can affect how the effect is generated in your level when placed.

Examples of this type of Component in use with varying values for its **Decay Height** setting (which controls fog density decay height, ie. lower values cause the fog to be denser, while higher values thin the fog, causing less scatter) are portrayed below. For more information, see the **[Atmospheric Fog User Guide](/documentation/en-us/unreal-engine/environmental-light-with-fog-clouds-sky-and-atmosphere-in-unreal-engine)** page.

|   |   |
| --- | --- |
| ![Atmo0.5_4.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1462436-6054-49f5-bae9-de3511d07072/atmo0-5_4-resize298x233.png) | ![Atmo0.35_4.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/464d6fd5-3637-4fab-b06b-d9a0c70abdf7/atmo0-35_4-resize321x235.png) |
| Density Decay Height of 0.5 (8 km) | Density Decay Height of 0.35 (2.744 km) |
| ![Atmo1.0_4.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57e249f0-60b2-4cbf-a47c-54bc41483f38/atmo1-0_4-resize370x241.png) | ![Atmo1.0_1.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34bb2872-6c6e-4639-95c7-3da02266a470/atmo1-0_1-resize357x243.png) |
| Density Decay Height of 1.0 (64 km) and Max Scattering of 4 | Density Decay Height of 1.0 (64 km) and Max Scattering of 1 |

## Exponential Height Fog Component

The **ExponentialHeightFogComponent** is used to create fog effects but with a density that is related to the height of the fog.

Exponential Height Fog creates more density in low places of a map and less density in high places. The transition is smooth so you never get a hard cutoff as you increase altitude. Exponential Height Fog also provides two fog colors, one for the hemisphere facing the dominant directional light (or straight up if none exists), and another color for the opposite hemisphere.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e9bdb82-2ef6-46af-905f-05b31210e310/exponheightfog.png)

See **[Exponential Height Fog User Guide](/documentation/en-us/unreal-engine/exponential-height-fog-in-unreal-engine)** for more information and settings that can be adjusted.

## Billboard Component

The **BillboardComponent** is a 2D Texture that will be rendered always facing the camera and functions similarly to an **ArrowComponent** in that it can be used for a method of placement and easy selection. For example in the fog sheet that was created below, the only Component added is a **BillboardComponent** (the actual fog effect is a material that is dynamically created through script).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad684316-61b8-4f5a-9fee-878242792ba2/billboard1.png)

Inside the level, you can manipulate the fog sheet by selecting the **BillboardComponent** icon (which is a texture that you can specify).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d06a6694-89fa-47f3-a6e8-6411fedf3809/billboard2.png)

For an example of how this Fog Sheet was created, see the [Fog Sheet and Light Beams](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine) documentation.

## Material Billboard Component

The **MaterialBillboardComponent** is a 2D Material that will be rendered always facing the camera. One example of where this type of Component could be used is in the form of 2D grass or foliage. Rather than using Static Meshes to represent pockets of growing grass or even individual grass blades, using a **MaterialBillboardComponent** with a Material used to convey growing grass, there is no need to have a 3D representation of grass as the billboard will automatically turn and face the player giving the illusion of three dimensional grass.

## Custom Mesh Component

The **CustomMeshComponent** allows you to specify custom triangle mesh geometry.

## Poseable Mesh Component

The **PoseableMeshComponent** allows bone transforms to be driven by a **Blueprint**.

## Decal Component

A **DecalComponent** is a material that is rendered onto the surface of a mesh (a kind of "bumper sticker" for a model). Decals can be used for any number of purposes, such as bullet impact decals on a wall when shot, a skid mark decal for a car that breaks along a road, blood that splatters on the ground when being shot, etc. (an example decal is provided below).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a20da25-3bed-4875-9c39-ac904e53c00b/decal_1.png)

There are several pages you can refer to for more information on working with Decals.

-   See [Decal Actor User Guide](/documentation/en-us/unreal-engine/decal-actors-in-unreal-engine).
-   See [1.1 - Basic Decal](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine).
-   See [Decals Content Examples](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine#decalsmap).

## Instanced Static Mesh Component

An **InstancedStaticMeshComponent** is a Component that efficiently renders multiple instances of the same Static Mesh. This type of Component is particularly useful for procedural level or room creation, as instead of placing hundreds (or even thousands) of **Static Mesh Actors** in your level, you can place one **Instanced Static Mesh** and add multiple instances of the Static Mesh (floors or walls for example) at a much lower performance cost.

See the [**Procedural Room Generation**](https://wiki.unrealengine.com/Videos/Player?series=PLZlv_N0_O1ga0aV9jVqJgog0VWz1cLL5f&video=mI7eYXMJ5eI) training stream on our Wiki for an example of working with **InstancedStaticMesh** Components and procedurally generating a random room.

## Particle System Component

A **ParticleSystemComponent** allows you to add a particle emitter as a sub-object to another object. Adding a **ParticleSystemComponent** could be used for several reasons, from adding an explosion effect to something that gets destroyed to adding a fire effect to something you can set on fire. By adding this type of Component to another Object, through script you can access and set any of the parameters of the Particle Effect during gameplay (ie. turning the effect on or off).

For example, below we have a security camera and have added a **ParticleSystemComponent** for a spark effect.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e0d2cae-6eb2-43a1-9c9d-c0303dc776bd/particle1.png)

Through script we could state that the spark effect is off by default, but activated when the camera is shot.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39987321-75a4-4faa-b6ca-871b948e9359/particle2.png)

See [**Cascade Particle Systems**](/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine) for more information.

## Post Process Component

**PostProcessComponets** enable Post Process controls for **Blueprints**. It will use a parent `UShapeComponent` to provide volume data if available. This type of Component could be used to shift the tone of your level, when Post Process Settings are applied to it. For example suppose you defined a default Post Process Setting to use for your game, when the player is damaged (or potentially killed), you could through script change the settings to a black/white tone for the **Scene Color Tint**.

For more information see the [**Post Processing Content Examples**](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine) or [**Post Process Effects**](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine) documentation.

## Scene Capture 2D Component

The **SceneCapture2DComponent** is used to capture a "snapshot" of the scene from a single plane and feed it to a Render Target. There are settings for controlling the **Field of View** when capturing as well as specifying the **Render Target** texture (among other settings). An example of using this would be in the case of creating a mirror (shown below) or security camera view on a monitor (see [**Security Camera Switcher Button**](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine).)

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70363fb8-1f16-4417-a937-a8a0ca813024/2drender.png)

Above we have created a **Blueprint** with a **SceneCapture2DComponent** and assigned a **Render Target** texture which was then used as a **Material** that we applied to the piece of geometry in the level. For more information, see [**Scene Capture 2D Content Example**](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine).

## Scene Capture Cube Component

A **SceneCaptureCubeComponent** is used to capture a "snapshot" of the scene from 6 planes and feed it to a Render Target.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d60f0774-2620-4afb-9684-806a70312fbf/scene-capture-cube.png)

In most instances the **SceneCapture2DComponent** should accomplish most of your scene capturing needs, however in the event that you need a 3D capture of an environment you could use this type of Component. Be aware of your usage however as these are very expensive performance wise and should only be used when absolutely necessary. See the [**Reflections**](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine) for more information on the different the methods that can be used to create reflections in your levels.

## Spline Mesh Component

**SplineMeshComponents** can be used to stretch and bend a Static Mesh asset. With **SplineMeshesComponents**, you must provide vectors for the position and tangent for the start and end of the spline. Below, a **SplineMeshComponent** has been added to a **Blueprint** and a pipe **Static Mesh** has been assigned as the asset to affect.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd1080b2-34bb-4788-b7c9-3ec67dc78395/splinemesh.png)

While you specify the vectors for the position and tangent on the Component itself, you can use script to set these as variables and make them public so that they can be edited inside the Editor Viewport as seen below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79c594b1-9705-4ae0-8fdf-05f929de67bd/splinemesh2.png)

Above we can move the **Start Transform** and **End Transform** independently of moving the entire Actor, allowing us to stretch or rotate it as we desire. This example and setup can be found inside the [**Blueprint Splines Content Examples**](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine) Content Examples map.

## Text Render Component

A **TextRenderComponent** renders text in the world with the given font. Contains usual font related attributes such as Scale, Alignment, Color, etc. You might use this Component to indicate to a player that an object is intractable in your levels.

For example, suppose you had a chair in your level that players can sit down in when they approach it if they press a button. You could add a **TextRenderComponent** containing the instructions needed to execute the command of sitting (visibility set to off) along with a **BoxComponent** used as a trigger which will set visibility of the text to true when the player enters it (shown below).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/adfa8732-a9ff-4c24-907d-fef7b8bbd68d/text1.png)

In game when the player enters the trigger, the **TextRenderComponent** text is displayed informing the player how to sit.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/721b1f05-ca6c-43dc-a428-0038a800d4fd/text2.png)
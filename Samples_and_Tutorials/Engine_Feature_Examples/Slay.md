# Slay

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/slay-sample-project-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/slay-sample-project-for-unreal-engine)  
**Processed:** 2025-06-14 16:51:11

---

Virtual production is supported in Unreal Engine through the use of various cinematic tools, rendering features, and workflows. The Slay sample, built by **[Mold3D Studio](https://www.mold3dstudio.com/)**, was created to demonstrate techniques, rendering features, and workflows that can be achieved when considering virtual production in Unreal Engine.

This document provides an overview of how to view the Slay sample, as well as the workflows and production techniques that were used to create it.

#### Prerequisites

-   The Slay sample content is a graphically intensive scene. It requires at least an **Intel Core i9 Series** processor and **GeForce RTX 2080 Ti,** or similar.
    
-   When opening the project or Level for the first time, there may be a long initial load time as numerous assets are loaded and compiled for the first time.
    

## Setup

To set up a project with the Slay sample, follow these steps:

1.  Access the [Slay sample](https://fab.com/s/6066e5de148a) from **Fab** and click **Add to My Library** for the project file to show in the **Epic Games Launcher**.
    1.  Alternatively, you can search for the sample project from the Fab plugin for UE.
2.  From the **Epic Games Launcher**, go to **Unreal Engine > Library > Fab Library** to access the project.
    
    Sample projects only appear in **Fab Library** when you install the compatible engine version.
    
3.  Click **Create Project** and follow the on-screen instructions to download the sample and start a new project.
    
4.  Open your new project in the Unreal Editor.

To learn more about accessing sample content and the Fab plugin for Unreal Engine, see [Samples and Tutorials](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine).

## Viewing the Slay Sequence

To view the Slay sequence, click the **Cinematics** button in the main toolbar and select **TF\_Edit**.

![open slay cinematic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46ce3232-5e16-41b7-872b-58b97e792798/openscene.png)

This will open the **[Master Sequence](/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine)** for the Slay cinematic. You can see the multiple shots used to assemble the full sequence in this view.

![slay master sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2aa694e3-571d-4e88-ba4a-bcd0ea3774d5/seqeunce.png)

Select the **Camera** button on the Shot Track to look through the **[Cameras](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine)** for each shot, and click the **Play** button to play the sequence.

![play slay sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26a4a844-6333-4a57-ae69-be04d93cd532/playseqeunce.png)

## Quixel Megascan Assets

The Temple Level was built using a combination of unique assets and **[Quixel Megascan](https://quixel.com/megascans/home)** assets. These assets were used in Slay to provide background details, props, and foliage. Using Quixel Megascan assets in your project can save time and resources when creating large environments.

![slay quixel megascan](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2aeb78a5-4c87-49d7-b997-9c37ce8f4796/megascans.png)

You can view some of the Quixel Megascan assets used in the Slay sample by navigating to the **[Quixel Megascan](https://quixel.com/megascans/home)** website. Some notable examples include:

-   **[Gravestones](https://quixel.com/megascans/home?category=3D%20asset&category=historical&category=feudal%20japan&category=gravestone&search=gravestone)** in the Temple courtyard.
    
    ![quixel megascan grave](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/797e936b-4620-4178-aa71-9ecc95cd6fc8/graves.png)
    
-   **[Location or era-specific props](https://quixel.com/megascans/home?category=3D%20asset&search=japan)** placed around the Level.
    
    ![quixel megascan japan props](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da7f84bf-7906-4c41-b7c6-a80d80a036ed/props.png)
    
-   **[Grass](https://quixel.com/megascans/home?category=3D%20plant&category=grass)** and other foliage placed in the gardens and other areas.
    
    ![quixel megascan grass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1af2f6dc-47fd-4633-aca2-5f798ee03ae8/grass.png)
    

## Shot-Based Workflow

The Slay sequence was created using **[Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine)** and its **[Shot-Based](/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine#shots)** workflow. This was done so that each shot contains all necessary content for that shot only, rather than a larger single sequence. This setup allows for quick modifications to the sequence as a whole, as shots can be **[edited, trimmed, and re-arranged](/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine#shotsections)**, just like in any non-linear editing software.

In the Master Sequence **TF\_Edit**, you can see all the shots arranged in the **Shot Track**. Additionally there are **[Audio Tracks](/documentation/en-us/unreal-engine/cinematic-audio-track-in-unreal-engine)** for playing audio that has been timed to the sequence edit, and a **[Fade Track](/documentation/en-us/unreal-engine/cinematic-color-fade-track-in-unreal-engine)** for controlling the fade to and from black.

![slay master sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e9560e0-230f-40c8-a1f8-610d8bff4dfc/masterseqoverview.png)

Double-click any shot to open and view its contents.

### Level Visibility

The first shot of Slay is an exterior view of the Temple. Because of this unique angle, it was necessary to create a custom **[Landscape](/documentation/en-us/unreal-engine/landscape-outdoor-terrain-in-unreal-engine)** and assets for a Level that only is visible for the duration of **Shot TF0010\_02**. The Level's visibility is controlled by the **[Level Visibility Track](/documentation/en-us/unreal-engine/cinematic-level-visibility-track-in-unreal-engine)**, and can be seen in shot **TF0010\_02** (Shot 1)

With the Level Visibility Track placed inside the shot, it will evaluate only for the duration of the shot. In this case, the Level containing the lower-resolution Landscape for use when inside the Temple is hidden, and the Level containing higher-resolution Landscape and other assets is displayed instead.

![slay level visibility terrain](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1105b4a1-3655-4873-a8a0-50ea7d40e7ce/levelvisibility.png)

You can manually preview the higher-resolution Landscape Level by navigating to the **[Levels](/documentation/en-us/unreal-engine/working-with-levels-in-unreal-engine)** panel, enabling **Terrain\_TF0010,** and disabling **Terrain**.

### Using Spawnables

**[Spawnables](/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics)** are Actors that are spawned and typically exist only for the duration of a single sequence. These are used extensively in several shots throughout the Slay sequence in order to address problems unique to each shot. Since each shot is its own sequence, spawnables will only exist for the duration of a shot, making it easier to manage these Actors.

An example of a spawnable Actor can be seen in **Shot TF0020\_01** (Shot 2). In this example, the original static mesh door is hidden and replaced with a spawnable **Skeletal Mesh** door, containing animation to match the character's movement as she opens it. When the shot ends, the door is unspawned automatically.

![slay spawnable door actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/185dc185-9ce0-49a0-ab13-39f210aa092c/spawnabledoor.png)

### Artist Collaboration

In the Slay sample, each shot is its own sequence, and therefore its own asset. Shots also contain **[Subscene Tracks](/documentation/en-us/unreal-engine/cinematic-subscequences-track-in-unreal-engine)** which are their own sequence assets as well. Because of this division of assets, it is much simpler to enable multiple artists to work on a single sequence or shot at the same time, without file conflicts occurring. Subscenes can also be duplicated, enabling the same contents to be reused and shared across multiple instances.

In several shots, you can see Subscene Tracks for both **Lighting** and **FX**, which enable artists from these disciplines to work within these sequences instead of the main shot sequence. In this way, subscenes are not only useful for limiting file conflicts, but also for Sequencer organization.

![slay multi user subscene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf4ec21d-e41f-473c-8bb2-ac7ce279bc6b/subscenes.png)

You can double-click a Subscene section to open it and view its contents.

![subscene contents](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d50d3db-9f35-49db-b3a2-45092800e8f6/opensubscene.png)

When a shot or subscene is opened from a parent sequence, it will be displayed within the context of the Master Sequence. This means that even though you are viewing only a single subscene, all tracks from the Master Sequence and current shot also remain visible. You can edit lights, add visual effects, and perform other actions with full visual context of the scene.

![subscene editing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7dc3260-3466-45db-94e6-4f34c7fa075c/subscenecontext.gif)

This context view can be enabled or disabled by toggling **Evaluate Sub Sequences In Isolation** from Sequencer's [**Playback Menu**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#playbackoptions).

### Camera Animation

The Camera animation for Slay was **[created](/documentation/en-us/unreal-engine/how-to-animate-cinematic-cameras-in-unreal-engine)** entirely in Sequencer. In some cases, additive camera animation is also used to enhance the camera movement. This is done using **[Camera Animation Sequences](/documentation/en-us/unreal-engine/template-sequences-in-unreal-engine)**, which are a form of **[Template Sequence](/documentation/en-us/unreal-engine/template-sequences-in-unreal-engine)**.

![additive camera animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7999b6b-e364-4d43-bbbd-dc29805706ce/templateanim1.png)

Double-clicking one of these **Template Animations** will open the corresponding template sequence, where you can view the animation that is being used.

![camera animation sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/409257c3-60f8-47b4-81b5-681b0d90443b/templateanim2.png)

## Lighting and Materials

Lighting, Materials, and Effect usage plays a critical role in the Slay sample. Proper utilization of the Master Sequence and Shot ecosystem enables artists to more effectively light and apply material adjustments for each shot.

### Lighting Workflows

As mentioned [**previously**](/documentation/en-us/unreal-engine/slay-sample-project-for-unreal-engine#multi-userworkflows), lighting and other workflows can occur within Subscenes. Here, a typical lighting workflow would be to add your necessary **Light Actors** to the sequence as **[Spawnables](/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics)**. This is done so that the lights will only remain visible for the duration of the shot, and do not need to be manually turned on or off.

![spawnable light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/350f3095-91fc-4c70-be4b-390512279e0c/lighting1.png)

Other lighting techniques can be used to enhance your shots, such as using **Light Blockers** to block out certain areas of a scene from the main Level's light. Afterward you can more directly control the lighting of a shot using your spawnable lights.

For example, in **Shot TF0020\_01** (Shot 2), if you disable the **Camera** button to stop piloting it, then navigate in the viewport to view the Temple entrance area, you should see a large **Light Blocker** being used. This is used so that a more controlled lighting environment can be created for the shot.

![light blocker](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6e75be5-bd12-4af1-9598-a1d1d37ee4a0/lighting2.png)

With the light blocker in place, other lights can be spawned to better enhance the lighting in this shot, such as the spotlight shining through the nearby lattice, which casts soft shadows on the door.

![slay lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cb3c550-beb6-4788-a8c4-eb92e81f7ec5/lighting3.png)

In some other cases, it may be necessary to hide certain meshes to let light pass through and shine on your Actors. In **Shot TF0080\_01**, part of the Temple structure is hidden in order to let the sunlight cast on the Oni character.

![hide level for lights](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e212b3c7-2859-48e8-9e4a-069f90120c48/lighting4.png)

**[Lighting Channels](/documentation/en-us/unreal-engine/using-lighting-channels-in-unreal-engine)** are also used in Slay to control how lights affect the environment and characters. In this case, spawnable lights are only affecting **Channel 2**. This same channel is then enabled on all Characters, causing them to be lit by these lights. The environment is not lit by these lights because those meshes only have **Channel 0** enabled.

![lighting channels](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c39991b3-fd16-4914-882a-4301622bdb3f/lighting5.png)

### Material Workflows

If a **[Material](/documentation/en-us/unreal-engine/unreal-engine-materials)** is set up with **parameters**, you can reference these parameters in Sequencer to make overriding material parameter adjustments. In Slay, this was done to make minor adjustments to materials for specific shots. Similar to the previous lighting and shot-based workflows, these edits can be made on a per-shot basis without persisting to the next shot.

In Shot's **TF00110\_01 Lighting Subsequence**, you can see the **Roughness** and other parameters on Oni's armor material are adjusted using **Material Element Tracks**. The Material Element number corresponds to the same Material Element ID on the mesh.

![material parameter track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce17d634-fb20-48a2-b3e0-c0c1bee1cdaa/materials1.png)

Clicking **Add Parameter (+)** will reveal a list of the available material parameters for that element. Select a parameter to add it as a track.

![add material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/892c13e9-0b76-4ae2-8c0e-2a1707a0c78f/materials2.png)

## Render Settings

The Slay sample was created to be rendered as **Final Pixel** out, showcasing the high quality images that can be rendered with Unreal Engine. Because of this, there are several important parameters that are being set that increase the fidelity of the scene in both the viewport and when rendered using **[](/documentation/404)**.

### Post Process Volume

**[Post Processing](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine)** is used in the scene to control **Ray Tracing** effects such as **Global Illumination, Reflections,** and **Shadows**. Color correction is also applied using **[Color Grading and the Filmic Tonemapper](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine)** properties.

To view the post process properties being used in Slay, select the **Post Process Volume** in the Level. It can be found by searching for it in the **[Outliner](/documentation/en-us/unreal-engine/outliner-in-unreal-engine)**.

![post process volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bf93e85-3fe3-43c2-98da-8cbe2de91cf4/post1.png)

You can preview the effects of the Post Process Volume by enabling or disabling the **Enabled** property in its details. Using post processing can help you in making your scenes appear more vibrant.

![Post Processing Off](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5388e436-2be4-41d6-bf1d-d8dbf97f3a06/postoff.png)

![Post Processing On](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b08cb0b-5359-4691-857b-69ca67eb20da/poston.png)

### Viewport Optimization

As Slay is a graphically intense project, it became necessary to optimize the editor viewport experience to ensure smooth, reliable performance when working in Unreal Engine. This was done by setting certain [**Console Variables**](/documentation/en-us/unreal-engine/cinematic-rendering-image-quality-settings-in-unreal-engine#consolevariables) within the **DefaultEngine.ini** **[Configuration File](/documentation/en-us/unreal-engine/setting-up-your-development-environment-for-cplusplus-in-unreal-engine)**.

Some examples of the variables being set are:

```
	`r.HairStrands.Enable 1.0 	r.HairStrands.DeepShadow.Resolution 512.0 	r.RayTracing.Shadows.AcceptFirstHit 1.0 	r.RayTracing.SkyLight.ScreenPercentage 55.0`

Copy full snippet
```
r.HairStrands.Enable 1.0 r.HairStrands.DeepShadow.Resolution 512.0 r.RayTracing.Shadows.AcceptFirstHit 1.0 r.RayTracing.SkyLight.ScreenPercentage 55.0

To view the other console variables in use, you can navigate to the **Config** folder located in the install location of the Slay project and open **DefaultEngine.ini** in a text editor.

### Movie Render Queue Settings

The final picture for Slay is rendered using Unreal Engine's **[Movie Render Queue tool](/documentation/404)**. Movie Render Queue supports several features for producing high-quality renders, such as its temporal subsampling feature which is used to apply a high-quality radial motion blur effect. Additionally, Console Variables are used in Slay to increase graphical fidelity during the rendering process.

To open the Movie Render Queue window, click the **Render** button in Sequencer's Toolbar.

![open movie render queue](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c8f24cc-0c6e-4724-9126-62cdfbceafb5/mrq1.png)

The specific render settings used for Slay are saved as a **Movie Pipeline Master Config Asset**. To apply this preset to the render, click the **Settings** dropdown menu and select **Slay\_MovieRenderQueue\_Preset**.

![render settings preset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac3f9bcc-04d9-4f36-a42c-59cdb4390fbe/mrq2.png)

To see the settings being used, click the **Slay\_MovieRenderQueue\_Preset** settings text. This will open the **[Render Settings](/documentation/en-us/unreal-engine/cinematic-render-settings-and-formats-in-unreal-engine)** window which contains the various output, quality, and other settings applied during the rendering process.

![render settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d0d8249-c52d-4c8d-afe0-1b1f3aae570f/mrq3.png)

#### Anti-Aliasing

In order to reduce image noise, as well as to produce smoother edges and motion blur, [**Anti-Aliasing**](/documentation/en-us/unreal-engine/cinematic-rendering-image-quality-settings-in-unreal-engine#anti-aliasing) is used with **Temporal Sample Count** set to **19**.

![slay anti aliasing render settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c561a77-745a-4593-89b6-8158fb8135b2/mrq4.png)

#### Console Variables

To increase graphical fidelity in several areas including **Motion Blur**, **Subsurface Scattering**, and **Raytracing**, the following [**Console Variables**](/documentation/en-us/unreal-engine/cinematic-rendering-image-quality-settings-in-unreal-engine#consolevariables) are used:

![slay console variable render settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89a1c1ea-d7a0-48b1-86b2-dc8fb5b40854/mrq5.png)
```
	`r.MotionBlurQuality 4.0 	r.MotionBlurSeparable 1.0 	r.DepthOfFieldQuality 4.0 	r.ScreenPercentage 125.0 	r.ViewDistanceScale 50.0 	r.SSS.Quality 1.0 	r.SSR.Quality 4.0 	r.Shadow.DistanceScale 10.0 	r.ShadowQuality 5.0 	r.Shadow.RadiusThreshold 0.001 	r.SkeletalMeshLODBias -4.0 	r.RayTracing.GlobalIllumination.FireflySuppression 1.0 	r.RayTracing.SkyLight.ScreenPercentage 100.0 	r.RayTracing.AmbientOcclusion 1.0 	r.DiffuseIndirect.Denoiser 1.0 	r.RayTracing.Shadows.AcceptFirstHit 0.0 	r.HairStrands.Enable 1.0 	r.PathTracing.MaxBounces 2.0 	r.TemporalAACurrentFrameWeight 0.3 	r.RayTracing.GlobalIllumination.SamplesPerPixel 4.0 	r.RayTracing.Reflections.MaxRoughness 1.0 	r.RayTracing.GlobalIllumination.MaxBounces 2.0`
Copy full snippet
```
r.MotionBlurQuality 4.0 r.MotionBlurSeparable 1.0 r.DepthOfFieldQuality 4.0 r.ScreenPercentage 125.0 r.ViewDistanceScale 50.0 r.SSS.Quality 1.0 r.SSR.Quality 4.0 r.Shadow.DistanceScale 10.0 r.ShadowQuality 5.0 r.Shadow.RadiusThreshold 0.001 r.SkeletalMeshLODBias -4.0 r.RayTracing.GlobalIllumination.FireflySuppression 1.0 r.RayTracing.SkyLight.ScreenPercentage 100.0 r.RayTracing.AmbientOcclusion 1.0 r.DiffuseIndirect.Denoiser 1.0 r.RayTracing.Shadows.AcceptFirstHit 0.0 r.HairStrands.Enable 1.0 r.PathTracing.MaxBounces 2.0 r.TemporalAACurrentFrameWeight 0.3 r.RayTracing.GlobalIllumination.SamplesPerPixel 4.0 r.RayTracing.Reflections.MaxRoughness 1.0 r.RayTracing.GlobalIllumination.MaxBounces 2.0
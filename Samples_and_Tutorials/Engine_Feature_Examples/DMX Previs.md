# DMX Previs

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-previs-sample-project-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-previs-sample-project-for-unreal-engine)  
**Processed:** 2025-06-14 16:21:08

---

The DMX Previs sample is a fully-animated digital light show using the [DMX](/documentation/en-us/unreal-engine/dmx-overview) plugin in Unreal Engine. This sample was created in collaboration with [Moment Factory](https://momentfactory.com/home) to show an example of live event previsualization that is as close as possible to the real-life technical counterpart. To leverage Unreal Engine's rendering capabilities and to showcase the newly developed proxy fixture system, the sample features a complex lighting rig that fills the entire open space.

This video shows repeated, flashing lights at certain points that may cause discomfort or potentially trigger seizures for people with photosensitive epilepsy. Viewer discretion is advised.

Exploring and modifying this sample will help you learn how you can:

-   Use the DMX plugin Sequencer integration to record and play back an entire live event show programmed on an external lighting desk.
-   Use the extensible fixture system to create your own DMX-enabled virtual twins to real hardware devices.
-   Customize and tweak your fixture's rendering functions for both real-time previs and high-quality media export.

This project is both CPU-intensive for DMX Track playback in Sequencer and GPU-intensive for high-quality volumetric beam rendering. See the Fixtures and Hardware section for details on the hardware specifications used for this project.

## Getting Started

To create a project with the DMX Previs sample, follow these steps:

1.  Access the [DMX Previs sample](https://fab.com/s/14fbd7034e1b) from **Fab** and click **Add to My Library** for the project file to show in the **Epic Games Launcher**.
    1.  Alternatively, you can search for the sample project from the Fab plugin for UE.
2.  From the **Epic Games Launcher**, go to **Unreal Engine > Library > Fab Library** to access the project.
    
    Sample projects only appear in **Fab Library** when you install the compatible engine version.
    
3.  Click **Create Project** and follow the on-screen instructions to download the sample and start a new project.

To learn more about accessing sample content and the Fab plugin for Unreal Engine, see [Samples and Tutorials](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine).

1.  Press **Play** to view the previs sequence.
    
    ![Play the previs sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b10b587-a65b-4cc0-bb98-753a219552a5/image_3.png)

To view the show with optimal performance, build the project with the **Shipping** configuration.

Follow these steps to set the project's build configuration to **Shipping**:

1.  In the Editor's main menu, choose **File > Package Project > Build Configuration**, and select **Shipping**.
    
2.  Choose **File > Package Project > Windows** to package the project with the **Shipping** configuration.
    

![Shipping build configuration option in the Unreal Editor menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55eff37e-6d97-4f02-929f-9b1fe142713d/image_4.png)

## Viewing the Show from Multiple Perspectives

After opening the project and pressing **Play in the Editor**, the sequence begins with the cinematic camera view.

To view the show from other perspectives in the virtual auditorium, you can switch camera views with the playback controls defined in the project's [Level Blueprint](/documentation/en-us/unreal-engine/level-blueprint-in-unreal-engine) or disable the cinematic camera in **Sequencer**. Both methods are described below.

![Viewing the show](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aeb5c9d2-6d53-4a32-899c-2d3e099c44cc/image_5.png)

Image courtesy of Moment Factory.

### Show Playback Controls

Once the Unreal session has started, you can use the following playback controls:

| Key | Description |
| --- | --- |
| **F9** | Show the FPS counter, in both Standalone and Shipping builds. |
| **Space Bar** | Pause or resume the sequence and the DMX playback. |
| **T** | Toggle between cinematics and freecam. In freecam mode, you can move the camera to get a closer look at the light fixtures and view the show from other angles. |
| **V** | Cycle between predefined cinecamera views. |
| **R** | Restart the sequence and DMX playback. |
| **Escape** | Exit the session. |

### Disable Cinematic Camera

You can cycle through freecam and cinematics using the **T** toggle key. Press **V** to cycle between predefined camera locations. Follow the steps below to completely turn off the cinematic camera during the show.

1.  In the **Content Browser**, open **DMXPrevis\_Animations** in **Content > Sequences**.
    
    ![DMX previs animations in the content browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0287d5e1-5df5-4fd8-939f-629ac0a4c27a/image_6.png)
2.  In the **Sequencer** window, right-click on the **Camera Cuts** track and select **Mute** from the options.
    
    ![Sequencer window camera cuts track mute option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aadb4f2a-550b-4037-8709-5013cf438072/image_7.png)
3.  Press **Play**. You will be able to move the camera freely and view the show from different angles.
    

## Modifying the Show in Real-Time

During DMX track playback in Sequencer, it's useful to be able to modify the show as you are viewing it. This section describes how to change the look and feel of some of the light fixtures.

The project contains more assets than the ones described in this section. Explore all the light fixtures in the project; each type has its own Blueprint and functionality.

### Changing Spotlight Distance

Follow these steps to modify the light distance value of some of the lights. Decreasing this value can help to improve performance during playback; increasing the value creates more volumetric beam effects.

1.  In the **World Outliner**, type **Spot** in the search bar and select all the filtered assets.
    
    ![Filtering assets by the word spot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d91c36f-88dd-49b2-aa12-c18474a324d2/image_8.png)
2.  In the **Details** panel, change the **Light Distance Max** property value from **5000.0** to a smaller value for better performance or a higher value for increased volumetric effect.
    
    ![Light distance max 5000](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f77e3722-5257-46a8-a2a4-76060972b1a4/image_9.png)
    
    ![Light distance max 1000](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/baa7c607-e596-41d0-8c6a-833d23108d0d/image_10.png)
    

### Adjusting Beam Quality

All the fixtures used are specifically customised for the project and have adaptive quality logic for balancing speed and quality in real-time. The logic for adaptive quality is defined in the **M\_Beam\_Inhibitive\_Master** Material, located in **Content > DMX > FixtureMaterials**.

![fixture materials in the content browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29d4064e-c30f-4028-b800-2405cf82dca6/image_11.png)

This Material dynamically adjusts the volumetric beam shader sample counts as a function of the live DMX Zoom angle.

-   The wider the beam is, the lower the sample count to retain high performance with minimal visual impact.
-   The narrower the beam is, the higher the sample count for increased beam sharpness.

You can adjust the quality settings in the **Material Editor** for the **M\_Beam\_inhibitive\_Master** Material. The settings are located in the **Parameter Defaults** panel.

![Material parameter defaults panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28fd2cb1-d7c3-4e92-8398-ebfbc9a28204/image_12.png)

-   **Low Quality Level:** Defines the lowest possible multiple for the predefined sample count.
-   **Max Quality Level:** Defines the highest possible multiple for the predefined sample count.
-   **Use MRQ Override:** Forces a specific multiplier for all fixture material and material instances regardless of the low and max values set. This property is useful to set when exporting high quality videos or image sequences of the project.
-   **Zoom Based Intensity:** When enabled, the light function can lower in intensity when the zoom is wider but be closer to the intended brightness when the zoom is narrower. This mimics the behaviour of real lights where the brightness on any given surface is lower when the beam is wider.

![Low Quality Level 0.3 Max Quality Level 1.0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16cdabe7-7b04-4752-b051-7b536a1662b5/image_13.png)

![Low Quality Level 0.3 Max Quality Level 5.0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/494e4643-424f-4535-967c-a0f41564d50d/image_14.png)

In the left image, the Max Quality Level is set to 1 creating grainier beams. In the right image, the Max Quality Level is set to 5 so the beams appear sharper.

**Quality Levels** set to values greater than **1** are meant for offline renderings using [Movie Render Queue](/documentation/404). For this project, the **Quality Level** was typically set to **2** for both **Low and Max Quality Levels** to generate footage.

### Changing Catwalk Cell Count

Follow these steps to change the cell count for the DMX Fixture Matrix used in the Catwalk.

1.  In the project's **Content Browser**, double-click the **DMXLib\_v4** asset to open the **DMX Library Editor**.
    
    ![DMX library asset in the content browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d05fe21-962b-43bc-b89d-28887df20ab6/image_15.png)
2.  In the **Fixture Types** tab, select **CatwalkStrip** under **Matrix/Pixel Bar**. This example is going to modify its **Mode Properties**.
    
    ![catwalk strip mode properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/019b3cd6-2ca4-4b84-9acd-b253b2b76bbd/image_16.png)
3.  In the **Mode Properties** panel, change the **Y Cells** property value from **5** to **20**.
    
    ![changing the value of the y cells property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40b4f34a-386b-4b93-af3a-692f376cae5b/image_17.png)
4.  In the **World Outliner**, select all the **CatwalkStrips** assets.
    
5.  In the **Details** panel under the **DMX Matrix Fixture** section, click **Generate Preview Mesh** to update the mesh in the viewport with the changes you made in the DMX Library.
    
    ![Details panel DMX Matrix Fixture section Generate preview mesh button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa0ac3f3-4b3c-4b02-9559-24732879d8da/image_18.png)
6.  In the viewport, all the **CatwalkStrips** now have more cells.
    
    ![catwalk 5 Y cells](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe5fb683-dadd-4491-8f50-815ee3ab866a/image_19.png)
    
    ![catwalk 20 Y cells](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/904b7c42-486f-4cc0-8058-f7da9fcc1a56/image_20.png)
    

## Exporting Media with Movie Render Queue

In a typical live event previs workflow, designers and artists will work at lower quality levels for quicker iterations. For review purposes, it's useful to render high-quality image sequences or Apple ProRes files.

This sample includes two presets for [Movie Render Queue](/documentation/404) to generate high-resolution media. The presets are located in **Content > Cinematics > MoviePipeline > Presets**. The two presets have different resolutions:

-   **UHD**: Preset for Ultra High Definition (3840x2160) export to Apple ProRes 422 HQ.
-   **FHD**: Preset for Full High Definition (1920x1080) export to Apple ProRes 422 HQ.

![movie render queue presets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c3426fb-5647-48df-bf2d-a8a1990bbf67/image_21.png)

Follow these steps to export high quality media using Movie Render Queue.

1.  In the project's **World Outliner**, select all the spotlights and set their **Light Distance Max** property to **12,000**.
    
    ![spotlight light distance max 12000](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b357052-ba0c-4f88-a4f3-827c3371665c/image_22.png)
2.  In the project's **Content Browser**, navigate to **DMX > FixtureMaterials**.
    
3.  Open the **M\_Beam\_Inhibitive\_Master** Material in the Material Editor.
    
4.  In the **Parameter Defaults** panel of the **Material Editor**:
    
    1.  Set **Low Quality Level** to **2.0**.
        
    2.  Set **Max Quality Level** to **2.0**.
        
    
    ![quality levels set to 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/549fd3ec-8f9e-43c1-994d-3ce5aff99be6/image_23.png)
5.  Close the Material Editor.
    
6.  In the main Editor, choose **Window > Cinematics > Movie Render Queue** to open the **Movie Render Queue** window.
    
    ![open the movie render queue window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3bd8418-b969-4162-991d-f9fae8e00b9f/image_24.png)
7.  Press the **Add Render** button and select the **DMXPrevis\_Animations** Level Sequence.
    
    ![select the DMX previs animations level sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1759bc3-9b70-48ea-b2d0-e5f3ab264033/image_25.png)
8.  Under the **Settings** column, click the dropdown arrow and select the desired preset, UHD or FHD.
    
    ![select the preset in the settings column](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddaa5635-358c-4834-ae25-929819a57fba/image_26.png)
9.  Click **Render (Local)** to export the rendered frames locally.
    
    ![Click render local](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac099e08-0e81-48db-a8e5-190722144457/image_27.png)

You can set the **MRQ Override** parameter in **M\_B\_Inhibitive\_Master** to **1.0** in order to override the **Low** and **Max Quality Levels**.

## Live Event Previs Project File Structure

This sample project includes a variety of assets to recreate an auditorium and full light show with DMX. To help you explore everything in the project, see the descriptions of all the folders below.

### Content Browser

![DMX subfolders in the content browser hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11c04009-8e3a-482c-b686-273b10c4b0b4/image_28.png)

The **Content** folder contains the following sub-folders:

-   **Assets:** General project and level assets for the stage and auditorium.
    
-   **Audio:** The show soundtrack.
    
-   **Blueprints:** [GameMode](/documentation/en-us/unreal-engine/game-mode-and-game-state-in-unreal-engine) override using Spectator Pawn.
    
-   **Cinematics:** [Movie Render Queue](/documentation/404) settings for Ultra High Definition (UHD) and Full High Definition (FHD) offline renders.
    
-   **DMX:** All DMX-related content.
    
    -   **Disks:** Project-specific DMX fixture gobos, which control the shape and pattern of a light. A given light can have multiple gobos throughout the show and can be animated.
        
    -   **EffectTables:** Defines the effects for the DMX-enabled light types used in the project.
        
    -   **FixtureMaterials:** Project-specific and optimized DMX Fixture materials. This is an extension of what was shipped with the DMX plugin.
        
    -   **FixturesBP:** Project-specific Lighting Fixture blueprints. This is an extension of what was shipped with the DMX plugin.
        
    -   **GoboWheel:** Same as the contents of the **Disks** folder but as separate textures.
        
    -   **Plugins:** Useful DMX tools and widgets.
        
    -   **SpecialFXBP:** Project-specific pyro, laser, and fireworks fixture assets. It also contains the DMX-controlled sphere that is in the middle of the stage.
        
    -   **DMXLib\_v4:** The project core [DMX library](/documentation/en-us/unreal-engine/create-a-dmx-library-and-add-fixture-patches-in-unreal-engine), which contains all the Fixture definitions, Universes, and patching.
        
-   **Effects:**
    
    -   **Bloom:** Project-specific, high-quality, convoluted bloom **Texture** without streaks.
        
    -   **Fireworks:** Project-specific fireworks **Blueprints** and [Niagara](/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine) particle system.
        
    -   **Flash:** Audience cell phone lights and **Niagara** particle system.
        
    -   **RockLevitation:** Levitating rock **Niagara** particle system.
        
    -   **WaterMaterials:** High-quality water materials for the project.
        
-   **Maps:** Different parts of the level are contained in their own separate maps:
    
    -   **Main**: The persistent level that contains the sequencer track, post-process volume, and soundtrack.
        
    -   **DMXControlled**: This level contains all DMX-controlled elements, lighting fixtures, and effects.
        
    -   **Terrain:** This level contains the terrain and rock formation.
        
    -   **Venue:** This level contains the venue and structural-related actors, such as the arena, audience, and trusses.
        
-   **MegaScans: Quixel MegaScan** assets used for terrain and environment.
    
-   **Movies:** Contains [Media Framework](/documentation/en-us/unreal-engine/media-framework-in-unreal-engine) assets for movie playback.
    
    -   **Clock\_LED**: Contains the image sequence for animating the Clock LED that surrounds the catwalk.
        
    -   **Drapes**: Contains the image sequence for the drapes' video projection.
        
-   **MSPresets**: MegaScan preset assets.
    
-   **Sequences**: Contains the [Level Sequence](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview).
    
-   **Showfile**: The showfile (`.zip`) from the [grandMA2](https://www.malighting.com/downloads/products/grandma2/) lighting console. You can uncompress the file and use it on your console.
    
-   **Splash**: The project's splash image when it loads in the Unreal Editor.
    
-   **Tropical\_Jungle\_Pack**: The asset pack used for the environment.
    

### World Outliner

Explore all the assets in the **World Outliner**, especially the following items and folders:

-   **Cams:** The list of cameras used by Sequencer cinematics and predefined camera locations.
    
-   **DMX\_FX** and **DMX\_LX**: DMX-controlled fixtures and effects.
    
-   **DMXPrevis\_Animations:** The Level Sequence that drives the show, soundtrack, and DMX track.
    

## Fixtures and Hardware

This sample was designed to use the following fixtures and hardware.

### Fixtures

| Fixture Name | Fixture Type | Quantity |
| --- | --- | --- |
| Lighting Fixtures |   |   |
| **Audience Strip - No pixels** | Custom LED | 50 |
| **Audience Wash LED Par** | Elation SixPar 300 | 12 |
| **Catwalk Strip - 5 pixels** | Custom LED | 20 |
| **Matrix Strip - 5 pixels** | Custom LED | 32 |
| **Scenic Wash LED Par** | Elation SixPar 300 | 14 |
| **SpotMH1** | Elation Proteus Maximus | 64 |
| **SpotMH2** | Robe Megapointe | 94 |
| **Strobe RGB** | Elation Protron 3K LED Strobe | 122 |
| **Stage Strip - 5 pixels** | Custom LED | 24 |
| **Sun Strip - 5 pixels** | Custom LED | 90 |
| **Truss Toner** | Elation SixPar 300 | 220 |
| **WashMH1** | Ireos Space Canon | 8 |
| **WashMH2** | GLP X4 | 16 |
| **Vomitory LED Par** | Elation SixPar 300 | 2 |
| **Total Lighting Fixture Count** |   | 768 |
| SFX Fixtures |   |   |
| **Fireworks** | N/A | 8 |
| **Laser RGB** | N/A | 6 |
| **Pyrotechnic Launcher** | N/A | 33 |
| **Total SFX Fixture Count** |   | 47 |

### Lighting Console

| Hardware | Quantity |
| --- | --- |
| **grandMA2 light** | 1 |
| **MA Lighting NPU** | 1 |

### DMX

| Specs | Description |
| --- | --- |
| **Channels** | 7368 |
| **DMX Universes** | 15 |
| **Protocol** | Art-Net |
| **Unique Cues** | 144 |
| **Timecode Sync** | MIDI |

## Plugins

The following plugins provide the core functionality shown in this sample:

-   DMX Engine
-   DMX Fixtures
-   DMX Pixel Mapping
-   DMX Protocol
-   Level Sequence Editor
-   Movie Render Queue
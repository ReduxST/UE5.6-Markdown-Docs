# General Engine Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/general-engine-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/general-engine-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:25:18

---

## General Settings

### Fonts

| **Section** | **Description** |
| --- | --- |
| **Tiny Font** | Sets the font used for the smallest engine text. |
| **Small Font** | Sets the font used for small engine text, used for most debug displays. |
| **Medium Font** | Sets the font used for medium engine text. |
| **Large Font** | Sets the font used for large engine text. |
| **Subtitle Font** | Sets the font used by the default Subtitle Manager. |
| **Additional Font Names** | Sets additional fonts that will be loaded at startup and available using the `GetAdditionalFont()` function. |

### Default Classes

| **Section** | **Description** |
| --- | --- |
| **Console Class** | Sets the class to use for the game console, summoned with **~**. |
| **Game Viewport Client Class Name** | Sets the class to use for the game viewport client, which can be overridden to change game-specific input and display behavior. |
| **Local Player Class** | Sets the class to use for local players, which can be overridden to store game-specific information for a local player. |
| **World Settings Class** | Sets the class to use for `WorldSettings`, which can be overridden to store game-specific information on map / world. |
| **Level Script Actor Class** | 
Sets the Level Script Actor class, which can be overridden to allow game-specific behavior in per-map Blueprint scripting.

You can choose from the following options:

-   **FunctionalTestLevelScript**
-   **LevelScriptActor**
-   **ThirdPersonMap\_C**



 |
| **Physics Collision Handler Class** | Sets the `PhysicsCollisionHandler` class to use by default, which can be overridden to change game-specific behavior when objects collide using physics. |
| **Game User Settings Class** | Sets the `GameUserSettings` class, which can be overridden to support game-specific options for graphics, sound, and gameplay. |
| **Default Blueprint Base Class** | Sets the base class to use for new Blueprints created in the editor, configurable on a per-game basis. |
| **Game Singleton Class** | 

Sets the class for a global object spawned at startup to handle game-specific data.

If empty, it will not spawn one.



 |
| **Asset Manager Class** | 

Sets the class to spawn as the global `AssetManager`, configurable per game.

If empty, it will not spawn one.



 |

### Default Materials

| **Section** | **Description** |
| --- | --- |
| **Preview Shadows Indicator Material** | Path of the material that renders a message about preview shadows being used. |
| **Destructible Physics Material** | Path of the PhysicalMaterial to use if none is defined for a particular object. |

### Settings

| **Section** | **Description** |
| --- | --- |
| **Near Clip Plane** | The distance of the camera's near clipping plane. |

### Subtitles

| **Section** | **Description** |
| --- | --- |
| **Subtitles Enabled** | Toggles subtitle display for localized sounds. |
| **Subtitles Forced Off** | 
Flag for forcibly disabling subtitles. If this option is enabled, you will not be able to turn subtitles on using any other method.



 |

### Blueprints

| **Section** | **Description** |
| --- | --- |
| **Maximum Loop Iteration Count** | Script maximum loop iteration count used as a threshold to warn users about script execution runaway. |
| **Can Blueprints Tick by Default** | 
Controls whether Blueprint subclasses of Actors or Components can tick by default.

Blueprints that derive from native C++ classes that have `bCanEverTick=true` will always be able to tick.

Blueprints that derive from exactly `AActor` or `UActorComponent` will always be able to tick.

Otherwise, they can tick as long as the parent doesn't have `meta=(ChildCannotTick)` and either `bCanBlueprintsTickByDefault` is true or the parent has `meta=(ChildCanTick)`.



 |

### Anim Blueprints

| **Section** | **Description** |
| --- | --- |
| **Optimize Anim Blueprint Member Variable Access** | 
Controls whether anim blueprints nodes that access member variables of their class directly should use the optimized path that avoids a thunk to the Blueprint VM (Blueprint Virtual Machine).

This will force all anim blueprints to be recompiled.



 |
| **Allow Multi Threaded Animation Update** | 

Controls whether anim blueprint graph updates can be performed on non-game threads by default. This enables some extra checks in the anim blueprint compiler that will warn when unsafe operations are being attempted.

This will force all anim blueprints to be recompiled.



 |

### Framerate

| **Section** | **Description** |
| --- | --- |
| **Smooth Frame Rate** | Specifies whether to enable framerate smoothing. |
| **Use Fixed Frame Rate** | Specifies whether to use a fixed framerate. |
| **Fixed Frame Rate** | The fixed framerate to use. |
| **Smoothed Frame Rate Range** | Range of framerates in which smoothing will kick in. |
| **Min Desired Frame Rate** | Minimum desired frame rate setting. Below this frame rate, visual detail may be lowered. |
| **Custom TimeStep** | 
Overrides how the Engine processes the Framerate / Timestep.

This class will be responsible for updating the application Time and DeltaTime. Can be used to synchronize the engine with another process (gen-lock).



 |

### Timecode

| **Section** | **Description** |
| --- | --- |
| **Timecode Provider** | Sets `TimecodeProvider` when the engine starts. |
| **Generate Default Timecode** | 
Generate a default timecode from the computer clock when there is no timecode provider.

On desktop platforms, the system time will be used and will behave as if a `USystemTimecodeProvider` was set.

On console platforms, the high performance clock will be used. This may introduce drift over time.

If you want to use the system time on console platforms, set the timecode provider to `USystemTimecodeProvider`.



 |
| **Generate Default Timecode Frame Rate** | 

When generating a default timecode (`bGenerateDefaultTimecode` is true and no timecode provider is set), sets the frame rate at which it should be generated (number of frames).

You can choose from the following options:

-   **12 fps (animation)**
-   **15 fps**
-   **24 fps (film)**
-   **25 fps (PAL/25)**
-   **30 fps**
-   **48 fps**
-   **50 fps (PAL/50)**
-   **60 fps**
-   **100 fps**
-   **120 fps**
-   **23.976 fps (NTSC/24)**
-   **29.97 fps (NTSC/30)**
-   **59.94 fps (NTSC/60)**
-   **Custom**



 |
| **Generate Default Timecode Frame Delay** | Number of frames to subtract from generated default timecode. |

### Screenshots

| **Section** | **Description** |
| --- | --- |
| **Game Screenshot Save Directory** | The save directory for newly created screenshots. |

### Level Streaming

| **Section** | **Description** |
| --- | --- |
| **Streaming Distance Factor** | Fudge factor for tweaking the distance-based mip level determination. |

### Per Quality Level Property

| **Section** | **Description** |
| --- | --- |
| **Use Static Mesh Min LOD Per Quality Levels** | Use Static Mesh minimum LOD per quality levels. |
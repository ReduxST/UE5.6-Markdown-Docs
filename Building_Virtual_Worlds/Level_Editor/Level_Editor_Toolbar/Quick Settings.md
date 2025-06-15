# Quick Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-settings-in-the-unreal-engine-level-toolbar](https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-settings-in-the-unreal-engine-level-toolbar)  
**Processed:** 2025-06-14 16:45:24

---

The **Settings** menu in the **Level Editor Toolbar** contains a set of properties that control selecting, editing, and previewing in the Level Viewport. Open the Settings menu from the Main Toolbar (also known as the [Level Editor Toolbar](/documentation/en-us/unreal-engine/level-editor-toolbar-in-unreal-engine)).

![Settings button in the Main Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1ee1e38-a58c-4396-96cb-a57257cbcf5d/ue5_1-main-toolbar-settings-button.png)

The Settings menu contains the following groups of settings:

-   Selection
    
-   Scalability
    
-   Real Time Audio
    
-   Snapping
    
-   Viewport
    
-   Previewing
    

## Selection

| **Option** | **Description** |
| --- | --- |
| **Allow Translucent Selection** | 
If enabled, clicking geometry with translucent Materials applied selects the Actor.

Enabling this option makes it possible to select transparent meshes, such as glass objects. Disabling it can be useful in other cases. For example, if you have a room filled with translucent particles, selecting other objects in the room would be difficult with this option enabled because clicking the particles would select the Emitter Actor.



 |
| **Allow Group Selection** | If enabled, selecting an Actor in a group selects the whole group instead of the individual Actor. |
| **Strict Box Selection** | If enabled, an Actor must be completely within the marquee selection box in order to be selected. |
| **Box Select Occluded Objects** | If enabled, marquee box select operations also select objects that are occluded by other objects. |
| **Show Transform Widget** | Toggles the visibility of the Transform widget in Viewports. |

## Scalability

| **Option** | **Description** |
| --- | --- |
| **Engine Scalability Settings** | 
Provides quick access to [Scalability](/documentation/en-us/unreal-engine/scalability-in-unreal-engine) settings that control the fidelity of various rendering features.

Enable the **Monitor Engine Performance?** option to see how changing this settings affects your project's performance in real time.



 |
| **Material Quality Level** | 

Sets the Material quality level used for previewing in the Viewports.

See [Material Quality Switch Expression](/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine#qualityswitch) for more information on setting up Materials to work with this setting.



 |
| **Preview Rendering Level** | 

Sets the rendering level used by the editor. You can restrict rendering quality to device-specific capabilities, including different version of:

-   Android
-   iOS
-   D3D



 |

## Real Time Audio

| **Option** | **Description** |
| --- | --- |
| **Volume** | Controls the volume of Level audio that plays when the Viewport is set to realtime. |

## Snapping

| **Option** | **Description** |
| --- | --- |
| **Enable Actor Snapping** | If enabled, Actors snap to the location of other Actors if they are within a specified distance. |
| **Distance** | Sets the distance Actors must be within in order to snap to one another if **Enable Actor Snapping** is enabled. |
| **Enable Socket Snapping** | If enabled, Actors can snap to sockets. |
| **Enable Vertex Snapping** | If enabled, Actors snap to the nearest vertex on another Actor in the direction of movement. |
| **Enable Planar Snapping** | If enabled, Actors snap to the nearest location on the constraint plane. This only works correctly in Perspective views. |

## Viewport

| **Option** | **Description** |
| --- | --- |
| **Hide Viewport UI** | Hides the Viewport toolbar and all Viewport UI widgets. |

## Previewing

| **Option** | **Description** |
| --- | --- |
| **Draw Brush Polys** | If enabled, semi-translucent polygons are rendered for the faces of a CSG (constructive Solid Geometry) brush when selected. |
| **Only Load Visible Levels in Game Preview** | If enabled, only visible levels will be loaded when game preview starts. |
| **Enable Particle System LOD Switching** | If enabled, particle systems will use distance LOD switching in perspective Viewports. |
| **Toggle Particle System Helpers** | If enabled, shows particle system helpers in Viewports. |
| **Freeze Particle Simulation** | If enabled, particle systems freeze their simulation state. |
| **Enable LOD View Locking** | If enabled, Viewports of the same type use the same LOD. |
| **Enable Automatic Level Streaming** | If enabled, the Viewport will stream in levels automatically when the camera moves. |
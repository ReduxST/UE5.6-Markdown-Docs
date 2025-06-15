# Editor Preferences

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-preferences](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-preferences)  
**Processed:** 2025-06-14 16:56:07

---

![Editor Preferences Dialog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b07feba-2287-414c-ade0-30ed6a392436/editorpreferences.png)

The **Editor Preferences** window is used to modify settings that control the behavior of Unreal Editor with respect to controls, viewports, source control, auto-saving, and more.

To open the **Editor Preferences** window, click **Edit > Editor Preferences**.

## Level Editor Preferences - Viewports

### Controls

| Option | Description |
| --- | --- |
| **Flight Camera Control type** | 
This setting determines whether the flight camera is used and how it is accessed. The flight camera uses the W, A, S, and D keys to dolly and pan the camera, similar to how standard FPS controls work. W and S dolly the camera in and out, while A and D pan, or strafe, the camera side to side. When active, this overrides any hotkeys using these controls, including toggling show flags.

-   **Use WASD for Camera Controls**: The flight camera and WASD controls are always active.
-   **Use WASD Only When Right Mouse Button is Held**: The flight camera and WASD controls are only active when the RMB is pressed.
-   **Never Use WASD for Camera Controls**: The flight camera and WASD controls are never active.



 |
| **Grab and Drag to Move Orthographic Cameras** | If enabled, clicking the Left or Right Mouse Buttons and dragging the mouse in an orthographic viewport will scroll the camera. Essentially what this means in practice is when you click and drag, the scene will move with the mouse. With this disabled, the scene moves opposite of the mouse. |
| **Orthographic Zoom to Cursor Position** | If enabled, zooming in the orthographic viewports will be centered around the mouse cursor. When disabled, zooming is centered on the center of the viewport. |
| **Link Orthographic Viewport Movement** | If enabled, all orthographic viewports will be linked to focus on the same position. So moving the camera in one orthographic viewport will cause the other orthographic viewports to follow. When disabled, all viewports can be navigated independently. |
| **Aspect Ratio Axis Constraint** | 

Determines which axis of the perspective viewport is used to control the field of view (FOV) to maintain the aspect ratio when resizing.

-   **Maintain Y-Axis FOV**: The Y-Axis (vertical) is used to determine the FOV.
-   **Maintain X-Axis FOV**: The X-Axis (horizontal) is used to determine the FOV.
-   **Maintain Major Axis FOV**: The larger of the two axes is used to determine the FOV.



 |
| **Mouse Scroll Camera Speed** | Determines the speed at which the perspective camera moves when navigating with the mouse. |

### Viewport Look and Feel

| Option | Description |
| --- | --- |
| **Highlight Objects Under Mouse Cursor** | If enabled, objects will be highlighted using a transparent overlay in viewports while hovering over them with the mouse cursor. |

### Editor Look and Feel

| Option | Description |
| --- | --- |
| **Use Small Tool Bar Icons** | If enabled, toolbar icons across the whole editor will be smaller and without labels. [See below for details.](/documentation/en-us/unreal-engine/unreal-editor-preferences#smalltoolbaricons) |

#### Small Tool Bar Icons

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0750d4ce-4ead-4b3c-a5c4-01af2613f9b2/look_and_feel_normal.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f878d80-bc3e-4639-9747-52cc37510f0a/look_and_feel_small.png) |
| **Normal** | **Small** |

### Level Editing

| Option | Description |
| --- | --- |
| **Enable Combined Translate/Rotate Widget** | 
If enabled, the combined Translation and Rotate-Z tool is made available.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ffec3ed-58c7-4d6f-9e30-cdfcd55e293b/transrotation_widget.png)

 |
| **Clicking BSP Enables Brush** | If enabled, clicking on a Brush surface selects the brush and **Ctrl + Shift + Click** selects the surface. When disabled, the opposite is true; clicking selects the surface and **Ctrl + Shift + Click** selects the brush. |
| **Update BSP Automatically** | If enabled, Brush geometry rebuilds automatically when brushes are moved or modified in the viewport. When disabled, geometry must be rebuilt to see the changes. |
| **Preserve Actor Scale on Replace** | If enabled, replacing Actors will respect the scale of the original Actor. Otherwise, the replaced Actors will have a scale of 1.0. |

### Source Control

| Option | Description |
| --- | --- |
| **Prompt for Checkout on Package Modification** | If enabled, the editor will automatically prompt for SCC checkout on package modification. |
| **Allow Source Control** | If enabled, the editor source control integration for packages and maps is used. |
| **Add New Files when Modified** | If enabled, new files are automatically added to source control. |
| **Host** | The host and port for your source control server. Example: `hostname:1234` |
| **Username** | The user name to sue when connecting to source control. |
| **Workspace** | The clientspec for source control. |

### Particles

| Option | Description |
| --- | --- |
| **Use Curves for Distributions** | If enabled, Distributions will use the curves in place of the baked lookup tables when being rendered in the editor. |

### Content Browser

| Option | Description |
| --- | --- |
| **Auto Reimport Textures** | If enabled, source files for textures are monitored and textures are automatically re-imported when the source file is modified. |
| **Assets to Load at Once before Warning** | The number of objects to load at once in the **Content Browser** before displaying a warning about loading many assets. |

### Privacy

The Editor in Unreal Engine 4 (UE4) collects usage data to help Epic continually improve UE4. There are three types of data that the Editor can collect:

-   Crash reports - generated when an error causes the Engine to crash.
-   Bug reports (also known as ensures) - generated when an issue causes the project to reach a certain unforeseen state, but does not cause a crash.
-   Usage data (also known as analytics) - a collection of data about the user.

When the Engine crashes, a crash report is generated. Crash reports automatically offer you a choice of whether or not to send crash data to Epic.

#### Disable Bug Reports

For bug reports, you can disable data collection in the **Privacy** category of Editor Preferences. Follow these steps to disable bug reports.

1.  In the menu bar, click **Edit > Editor Preferences**.
    
2.  In the Editor Preferences dialog, scroll down to the **Privacy** category.
    
3.  Click **Bug Reports**. In the right pane, under **Options**, the default setting is **Send unattended bug reports**.
    
4.  If you do not want bug reports sent to Epic, click **Don't Send**.
    

#### Disable Usage Data

Usage data primarily consists of aggregated or anonymized information that does not directly identify you as an individual user. However, this usage data may also include the following:

-   User's IP address
-   User's Internet Service Provider (ISP)
-   User's Continent, Country and City
-   User's Epic Account ID
-   User's project name

If you are concerned about privacy and want to opt out of usage data collection, you can change the setting in the **Privacy** category of Editor Preferences. Follow these steps to disable usage data collection.

1.  In the **Editor Preferences** dialog, scroll down to the **Privacy** category.
    
2.  Click **Usage Data**. In the right pane, under **Options**, the default setting is **Send Usage Data**.
    
3.  If you do not want usage data sent to Epic, click **Don't Send**.
    

To learn more about Epic's general privacy practices, see Epic's [Privacy Policy](https://www.epicgames.com/site/en-US/privacypolicy).

### Auto Save

| Option | Description |
| --- | --- |
| **Enable AutoSave** | If enabled, the editor will automatically perform a save operation at specified intervals. |
| **Save Maps** | If enabled, the auto-save procedure will attempt to save modified, loaded maps. |
| **Save Packages** | If enabled, the auto-save procedure will attempt to save modified content packages. |
| **Frequency in Minutes** | The time interval in minutes to wait between auto-saves. |
| **Warning in Seconds** | 
The number of seconds the warning is displayed before an auto-save is performed.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3622c41-004f-439b-9e36-52f8d09b90fe/autosave_warning.png)

 |
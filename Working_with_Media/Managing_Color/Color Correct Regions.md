# Color Correct Regions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/color-correct-regions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/color-correct-regions-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:06

---

With **Color Correction Regions**, you can adjust and correct the colors of the environment and objects in your scene. For example, in an in-camera VFX scenario, you can match the lighting and shadows between the real-world set and the environment displayed on the LED walls.

![A scene with a Color Correction Region applying a fuchsia color in a sphere volume to the environment.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6866a76-74c0-4ae0-8746-42b2a5f8d6db/ccr-example.png)

At the end of this page, you will be familiar with adding Color Correction Regions to your level and modifying their settings.

There are two types of Color Correction Actors in Unreal Engine:

**Color Correction Regions (CCR):** Use CCR to apply color correction to any Actors inside a shaped volume (Sphere, Box, Cylinder, or Cone).

**Color Correction Windows (CCW):** Use CCW to apply color correction to any Actors behind a flat plane, relative to the position of your camera.

## Add Color Correction Regions to your scene

To add a **Color Correction Region** (Either CCR or CCW) to your scene, follow these steps:

1.  In the Editor's main menu, choose **Edit** > **Plugins** to open the **Plugins** window.
    
    ![The Edit menu in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb862881-19b5-45d6-a456-3112cb26e482/ccr-plugin-menu.png)
2.  In the **Plugins** window, find **Color Correction Regions** in the **Other** section. Check the **Enabled** checkbox to enable the plugin.
    
    ![The Plugins window with the Color Corection Regions plugin highlightd](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55bb5192-3433-4c0e-ba0e-753f38167cb7/ccr-select-plugin.png)
3.  Restart the engine.
    
4.  In the Editor's main menu, choose **Edit** > **Project Settings** to open the Project Settings window.
    
5.  In the **Project Settings** window, go to **Engine** > **Rendering**, and change the **Custom Depth Stencil Path** to **Enabled With Stencil**.
    
    ![The Project Settings window with the Custom Depth Stencil Path option highlighted](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/297e27a2-ddd1-4bd0-b9ae-f78e98b844f3/ccr-customdepth-setting.png)
    
    **Custom Depth Stencil Path** must be set to **Enabled With Stencil** to use Color Correct Regions.
    
6.  In the **Place Actors** panel, select the **Volumes** category.
    
    ![The Place Actors window with the CCR and CCW volumes highlighted](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f506365-a97b-4266-ac67-eb9a1f08bb37/ccr-select-volume.png)
7.  Drag the **Color Correction Region** Asset or **Color Correction Window** Asset into the level.
    
    ![The Unreal Editor showing the Place Actors window and two mannequins in the Viewport with the CCR and CCW volumes highlighted](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0cb33e6-a621-4e9e-a41c-ff6fc1188018/ccr-place-actors.png)
8.  After you place your CCR or CCW volume in your level, you can modify the following settings in the **Details** panel to apply color grading to your level.
    

## Adjust Color Correction Region settings

CCR and CCW mostly use the same settings, however the **Type** and **Priority** settings are different for each type of Color Correction Region.

| **Property** | **Description** |
| --- | --- |
| Type | 
Determines the shape of the region.

**CCR options:**

-   Sphere
-   Box
-   Cylinder
-   Cone

**CCW options:**

-   Square
-   Circle



 |
| Priority | 

**CCR:** When multiple Color Correction Regions overlap, the priority of the regions determines what order the color grading of the regions are applied to the level. **CCW:** The **Priority** property does not appear in the Details panel for CCW. The priority of CCWs is based on the distance of the CCW from the camera. Regions closer to the camera have a higher priority and are applied first.



 |
| Intensity | Use this setting to control the strength of other Color Grading settings. |
| Inner and Outer | Use this setting to control the Region's falloff area. |
| Falloff | Use this setting with **Inner and Outer** to control the strength and area of falloff. |
| Invert | If checked, color grading is applied to everything in the level except for the area of this Color Correction Region. |
| Temperature Type | 

Select the type of color temperature control for this region.

-   **White Balance:** White Balance is the conventional color temperature control method.
-   **Color Temperature:** Color Temperature is the reverse of white balance
-   **Temperature (Legacy):** Temperature (Legacy) uses an older algorithm to modify color temperature. This algorithm can be faster than **White Balance** or **Color Temperature**, but the end results may not be comparable to conventional color correction algorithms.



 |
| Temperature | Use this setting to adjust the applied color temperature in kelvins. |
| Tint | Use this setting to adjust the tint of the color correction. Lower values adjust the color towards pink, higher values adjust the color towards green |
| Color Grading Settings | Color grading settings such as Gamma, Highlights, Midtones, and Shadow. |
| Enabled | If unchecked, this region will not be visible in your scene and it will not apply any color corrections. |

## Per Actor Color Correction

![The Viewport showing two mannequins and a Color Correct Region. One actor is not affected by the Color Correct Region](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cf91ea1-d54c-4177-8f2a-c25e3b1cf173/ccr-peractor-example.png)

You can use Per Actor Color Correction to selectively apply color correction to Actors in your scene.

There are two Per Actor CC modes:

-   **Exclude Selected Actors:** Use this setting to exclude selected Actors from this Color Correction Region. The region does not apply color correction to the selected Actors.
    
-   **Affect Only Selected Actors:** Use this setting to \_only \_include the selected Actors. This region only applies color correction to the selected Actors.
    

To enable Per Actor Color Correction, select your Color Correction Volume, go to the **Details** panel, and check the **Enable Per Actor CC** checkbox.

![The Per Actor Color Correction section of the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6581a28b-d012-47f7-a334-9f2ff0748838/ccr-enable-peractorcc.png)

After enabling Per Actor CC, you can select Actors to include or exclude from this Color Correction Region by adding them to the Actor Selection.

1.  Click the **+** icon to add an element to the Actor Selection.
    
2.  Select your Actor from the dropdown menu, or use the eyedropper tool to select an Actor from your viewport.
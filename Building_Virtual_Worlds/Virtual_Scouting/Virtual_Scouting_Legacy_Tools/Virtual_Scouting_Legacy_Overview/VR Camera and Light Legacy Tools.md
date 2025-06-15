# VR Camera and Light Legacy Tools

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/vr-camera-and-light-legacy-tools](https://dev.epicgames.com/documentation/en-us/unreal-engine/vr-camera-and-light-legacy-tools)  
**Processed:** 2025-06-14 17:03:46

---

The [Virtual Scouting Legacy tools](/documentation/en-us/unreal-engine/virtual-scouting-legacy-tools) described on this page will be sunset and deprecated in a future engine release. We encourage users to move to the [new Virtual Scouting tools](/documentation/en-us/unreal-engine/virtual-scouting-in-unreal-engine). Unused VREditor code and modules will be fully deprecated in a future engine release.

## Viewfinder

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27ca8a82-de4f-4e1e-82fb-ea136f5e3cfe/viewfinder1.png)

With the **Viewfinder** tool you can view the environment through a virtual lens and then spawn a virtual camera in the scene with the same viewport. The initial viewfinder display is only visible to you. For others to see your composition, you can create a camera in the scene easily with this tool. To activate this tool, open the Virtual Scouting menu and select the **Viewfinder** option.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4cfe97a-568b-4e7e-9f73-232c12c96e65/viewfinder2.png)

The initial viewport monitor has a few features available from the trackpad or thumbstick on your motion controller.

-   The upper-left and upper-right sections of the Vive motion controller's trackpad can be clicked to change the lens: left switches to a shorter lens and right switches to a longer lens.
-   Moving the Rift thumbstick left or down switches to a shorter lens and right or up switches to a longer lens. The lens selections are determined by the [Lens Kit](/documentation/en-us/unreal-engine/vr-camera-and-light-legacy-tools#howtochangelenskitinformation).
-   The bottom area of the Vive Trackpad or the Rift's B or Y buttons takes a snapshot of the current viewfinder display. This is helpful when wanting to show other users in a Multi-User scouting session with you a particular composition.
-   Snapshots are also saved to the Content/Snapshots/\[Level Name\] folder on your computer. These snapshots can be useful for storyboards or shot planning.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/242caf4e-9b67-4d61-bcaf-f46625ae1e9f/08.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/840fdcc0-1ad3-470e-9d26-84512ed37a6f/oculusvf.png) |
| Vive | Oculus Touch |

An example of a snapshot (the image frame on the left) taken from the Viewfinder tool.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5367ef5f-a795-4b34-921b-bc1e8769edb9/badger3_ucusnapshotsexample.png)

## Virtual Camera

To spawn a virtual camera in the scene, press the trigger on your motion controller while the Viewfinder tool is active.

-   You can change the lens of the new camera using the same controls as the viewfinder display.
-   You can also select and operate the camera with your controller using this tool.
-   While you can also operate the camera with the Interaction tool, you won't be able to adjust the lenses unless you use the camera's context menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f887644e-4d80-4dd5-a00e-ab160d48dfa5/virtualcamera1.png)

### Camera Context Menu

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a3ea9ab-0cb7-400a-a641-374bb6875003/badger3_cameracontextmenu.png)

You can make changes to the camera's settings directly in VR with the Camera Context Menu. Click the menu button on your motion controller while the camera is highlighted to bring up the Context Menu. The settings you can modify on the virtual camera are listed below.

-   **Delete**: Removes the camera from the level.
-   **Mark**: Spawns a camera location flag at the camera's current position. See the Camera Marks section for more.
-   **Focal Length**: Opens an additional HUD with lens options for the camera.
-   **F-Stop**: Opens an additional HUD with aperture options that can be used to adjust the focus range on the camera.
    
    F-Stop adjustments do not affect exposure.
    
-   **Snapshot**: Takes a snapshot image from the camera's current position.

If using the Focal Length or F-Stop context menu options, click the left or right sections on the Vive motion controller's trackpad or move the Oculus Touch controller's thumbstick to the left or right. This adjusts the camera's settings using what is in the [Lens Kit](/documentation/en-us/unreal-engine/vr-camera-and-light-legacy-tools#howtochangelenskitinformation) settings.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a684543-7c99-45d9-8933-12b7defb78fb/fstop1.png)

### Camera Monitor

Floating above the virtual camera object when the camera is selected is a camera monitor to show what the camera sees. You can interact with this camera monitor to pin or move it. The following are ways you can interact with the camera monitor:

-   On the bottom left of the camera monitor is the Pin button. Selecting this keeps the camera monitor visible even when you deselect the camera or select other objects in the scene.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e8cec39-394f-4358-9f9b-2c5a8f293351/badger3_ucuviewfindermonitorpinned.png)
-   On the bottom right of the camera monitor is a toggle button. This option toggles between the camera monitor being locked to the camera or to you. If attached to you, the camera view stays in front of you as you navigate around the scene.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2be47dd-f653-49df-a7bf-bf54e27813e4/vcammon1.png)
-   While the camera monitor is attached to you, you can select the bar underneath the monitor to reposition it. Moving your motion controller moves the camera monitor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b86b3a6-ca00-4033-a753-55f312483afe/vcammon2.png)
-   You can anchor the monitor in its current location and detach from you. To anchor the monitor in the level, select the arrow button to the left of the monitor bar.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ee53381-74af-4620-8b2b-2ec3a6ec0893/vcammon3.png)

### Camera Marks

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c3225ae-bd88-40e5-b792-59f3487f37f6/image_35.png)

Use **Camera Marks** to save the position of the camera as well as its lens settings. You can return the camera to this position and these settings at any time to recreate the same shot composition. This feature is also helpful for communicating the start and end position of the camera for a moving shot, such as with a dolly.

You can teleport to the position of a camera mark by opening the **Virtual Scouting** menu and selecting the **Camera Marks** tab on the right panel. Press the trigger on your motion controller when the camera mark to which you want to teleport is highlighted.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa51b569-de0e-46b1-883c-8cb7ed70a8fb/image_36.png)

### Tripod

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf57b0be-c511-4312-bd9b-50fbbf75abbb/image_50.png)

With the **Tripod** tool active, you can connect the virtual camera to your motion controller to operate the camera's pan and tilt rotation. The instructions below explain how to activate and use the tool:.

-   Open the **Virtual Scouting** menu and select the **Tripod** option to activate this tool. A virtual tripod appears and is connected to your motion controller.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cceadd8d-93a5-4c14-9393-8459a19cccb3/image_51.png)
-   Press the trigger on your motion controller to have your virtual camera attach to the tripod rig. Your motion controller drives the motion of the tripod, so you cannot detach your controller from the tripod while in this mode.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b16f66f-092c-452a-8039-383b127daed5/image_52.png)
-   Press the trigger on your motion controller again to detach the camera from the tripod.
    
    |   |   |
    | --- | --- |
    | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73eb2c8d-69a6-4982-a35e-cc234d5e7524/tripod1.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/caf74b45-dd96-43e2-a715-c353d60aa5e8/tripod2.png) |
    

### Handheld

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d63bea4c-1d7a-47d3-a37d-18b32925abf5/image_53.png)

With the **Handheld** tool you can connect your virtual camera to your motion controller to operate the camera. This movement tracking includes translations, along with pan, tilt, and roll.

Follow these instructions to activate and use the tool:.

-   Open the Virtual Scouting menu and select the Handheld option to activate the Handheld tool. A handheld camera rig appears and is connected to your controller.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd2d6ea7-de64-4887-8c90-f67172944415/image_54.png)
-   Press the trigger on your motion controller to have a virtual camera attach to the handheld camera rig. Your motion controller drives the motion of the rig, so you cannot detach your controller from the rig while in this mode.
    
    |   |   |
    | --- | --- |
    | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0fd47ca-6bad-4ef2-b862-b06b7e1e1518/handheld1.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f5edecc-0b66-435b-bf03-c67aa14e83bb/handheld2.png) |
    
-   Press the trigger on your motion controller again to detach the camera from the tripod.
    

### Dolly

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c81dda37-a71b-4ebf-9e85-f7e41e3346e0/image_55.png)

With the **Dolly** tool active, you can create a dolly track in VR and have the virtual camera move along the track. Open the **Virtual Scouting** menu and select the **Dolly** option to activate the tool.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72af45c3-059d-4058-9ce2-30bcd264776d/image_56.png)

-   When using the Vive motion controller to add dolly points to the level, click the top section on the trackpad. After two or more points have been created, click the bottom section of the trackpad to spawn the rails into the level.
-   When using the Oculus Touch controller to add dolly points to the level, press the B or Y button. After two or more points have been created, press down on the thumbstick to spawn the rails into the level.
    
    |   |   |
    | --- | --- |
    | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa536098-bab5-4947-9bce-f64e91d77bea/09.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8df8417d-b9e0-4329-ae76-15bf5a59774b/rightrift_dolly.png) |
    | Vive | Oculus Touch |
    
-   After the rails have been spawned, the dolly points can be edited to adjust the shape and path of the track. To edit the dolly points, select a dolly point and press the trigger on the motion controller.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/721b9b97-af77-43a5-90ec-f5b0d99f9296/image_57.png)

In order to connect cameras to the dolly track, you must parent the camera to the rails in the Editor. This cannot be done in VR.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f35bf85-6434-429b-ba62-1072a90205d9/image_58_cropped.png)

You can drive the position of the camera along the track with a custom Blueprint setup. With this custom setup, you can move the virtual camera using a physical dolly tracked in three-dimensional space.

## Using the VR Camera

### Mounting the Motion Controller to a Real Camera Rig

You can mount your motion controller onto a real tripod or handheld rig when using the Tripod and Handheld tools. This way, if desired, when you move your real tripod or handheld rig you can have more realistic camera motions using professional equipment.

To account for the variance of mounting positions of your motion controller to your physical rig, you can adjust the pivot point between your motion controller and the virtual camera.

1.  With the virtual camera attached to the rig, use the Interaction tool with your other motion controller to select the camera with the interaction pointer.
2.  Hold down the trigger on your motion controller to reposition the pivot point on the rig.
3.  Release the camera with the Interaction tool to save the new pivot point for the virtual camera on the rig.

### Camera Viewfinder and UI Panel Brightness

You can adjust the brightness on your viewfinder or camera monitor if it is too bright or dark by following these steps.

1.  Navigate to **Edit > Editor Preferences**.
2.  Select **VR Mode**.
3.  On the VR Mode settings page, modify the **UI Panel Brightness** setting.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be327daa-da60-4d28-b52f-ad172ce06b97/image_12.png)

### Camera Operating and Gizmos

Manipulating the camera in a single axis is easier with the Transform Gizmo enabled. You may find it preferable to disable the Transform Gizmo if you plan to operate the camera directly with your motion controller.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca16e6ce-23f3-423e-9f20-053b477c9903/turnoffgizmo1.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3712e74-a06d-493b-94d8-b8be8f2f305e/turnoffgizmo2.png) |
| With Transform Gizmo enabled | With Transform Gizmo disabled |

### How to Change the Camera Filmback

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f86252c-f39f-4147-98aa-960ccd1fb3ce/image_66_cropped.png)

Any virtual camera added to the level with the Viewfinder tool is going to have a set of film backs that can be used on that camera. You can edit the list of film back options and aspect ratio for each.

1.  Open your project's Engine > Config > DefaultEngine.ini file in a text editor.
2.  Edit the options in the FimbackPresets array.
3.  Edit the DefaulFilmbackPresetName to change the default film back for the Viewfinder tool.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/baef043a-f808-4d58-b6c8-9a49500d2829/image_67.png)

If the preset values are edited, it is recommended to distribute that DefaultEngine.ini to any other machines that are going to be used together for a Multi-User Virtual Scouting session.

### How to Change Lens Kit Information

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bec6ca57-b5fc-4771-a0e7-b4966febc46e/image_69_cropped.png)

Any virtual camera added to the level with the Viewfinder tool is going to have a set of lenses that can be used on that virtual camera. You can add to or edit this list of lenses that the virtual camera can use while Virtual Scouting.

1.  Open your project's **Engine > Config > DefaultEngine.ini** file in a text editor.
2.  Edit the options in the **LensPresets** array.
3.  Edit the **DefaultLensPresetName** within the lens kit array to change the default lens for the Viewfinder tool.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/683bb5ae-c198-4ab9-8bc9-e96829da8981/image_68.png)

Prime and Zoom lenses can be defined but the Viewfinder tool will only switch between the possible Prime lens options.

## Gaffer

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb984b8f-bd45-4e91-8ded-eefbefc41ee5/image_59.png)

With the **Gaffer** tool, you can spawn a light in your scene. You can move and adjust this light as if it were a real light on set.

1.  Open the Virtual Scouting menu and select the Gaffer option to activate the Gaffer Tool.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c759a42-24e0-4e31-a0dd-085f19c90da0/image_60.png)
2.  Press the trigger on your motion controller to make a light appear in your level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/edf49a6d-ff9d-4ab0-ba8f-fdcc277f75e4/image_61.png)
3.  Move your motion controller inside the light's collision layer to make moving and rotating the light more natural.
4.  You can adjust the spread and brightness of the light using the trackpad on your Vive motion controller or the thumbstick on your Oculus Touch controller.
    
    -   The top section of the trackpad or thumbstick makes the light brighter and the bottom section of the trackpad or thumbstick makes the light dimmer.
    -   The left section of the trackpad or thumbstick widens the spread and the right section of the trackpad or thumbstick narrows the spread.
    
    |   |   |
    | --- | --- |
    | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b8c8348-c53a-4f50-b996-46b122d70450/10.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bba00d88-5f2e-4ea1-8998-7eeca5501b8b/rightrift_gaffer.png) |
    | Vive | Oculus Touch |
    

### Light Context Menu

Using the **Light Context Menu** you can edit the light's intensity and spread as well as settings for the light's temperature. To view the Light Context Menu, select the light and press the **Menu** button on your motion controller.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e5ac6f1-4a7e-4efc-abe5-dadf7fc2b811/lightcontext1.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08236007-a03b-4023-a7aa-89f4d37a03b4/lightcontext2.png) |

Click down on the trackpad or thumbstick to select the options in the menu. This opens a HUD with the following settings. Choose an option in the HUD using the trackpad or thumbstick.

-   **Delete**: Removes the selected light from the scene.
-   **Intensity**: Brings up an additional HUD with Brightness options for the light.
-   **Spread**: Brings up an additional HUD with throw angle options for the light. These are visible from the angle of the panels attached to the light.
-   **Temperature**: Brings up an additional HUD with color temperature options in Kelvin for the light.
-   **Duplicate**: Spawns a copy of the light in the scene.
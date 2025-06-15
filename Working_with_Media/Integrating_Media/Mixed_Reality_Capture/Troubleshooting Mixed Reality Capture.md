# Troubleshooting Mixed Reality Capture

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/troubleshooting-mixed-reality-capture-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/troubleshooting-mixed-reality-capture-in-unreal-engine)  
**Processed:** 2025-06-14 16:55:06

---

This page provides troubleshooting information for Mixed Reality Capture (MRC).

## Flickering During Captures

Depending on the resolution of the MR capture target (the default is 1080p), your app may be constrained by its render target pool size. By default, render targets are set to reallocate as needed, which can lead to ping-ponging and flickering as the MR capture targets fight with the stereo render targets. (shown in the video below)

If you see this kind of behavior, you can change the render target resize rule to 'Grow' (in your engine.ini file, set *r.SceneRenderTargetResizeMethod=2*). Making this change should resolve the issue.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08dd5788-bbb6-4f99-96ef-74c753d0cc06/mr_captureflicker.gif)

## Capture Not Displaying on Spectator Screen

The MRC framework uses the [Virtual Reality Spectator Screen](/documentation/en-us/unreal-engine/virtual-reality-spectator-screen-in-unreal-engine) to display the composited scene. This means the Mixed Reality capture will only be displayed when running in Virtual Reality. If your project also uses the spectator screen, then you need to conditionally guard where you use them. There are MRC methods to help with this:

**Get Mixed Reality Capture Texture**  
Returns the Capture Texture, or a nullptr if there isn't one.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25e0d3ac-a8d0-43a5-ab6f-bc8f0de5613e/01-get-mixed-reality_ue5.png "01-get-mixed-reality_ue5.png")

**Is Mixed Reality Capture Broadcasting**  
Returns true, if the system is sending the capture texture to the spectator screen.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/269eb38f-f02d-4955-a4db-6d7f57bea11e/02-is-mixed-reality_ue5.png "02-is-mixed-reality_ue5.png")

**Set Mixed Reality Capture Broadcasting**  
Toggles whether the capture system is sending the capture texture to the spectator screen or not.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8494d0fc-f944-4c7a-9db6-594668447424/03-set-mixed-reality_ue5.png "03-set-mixed-reality_ue5.png")

**An Example of Using the MRC Methods**

Click image to expand.

## Controller/Trigger Not Responding During Calibration

If your controller input does not appear to respond during calibration, below are several possible causes.

-   **The headset sensor in not covered.** If theheadset's sensor is not covered, the controllers may not be active.
-   **The application window needs to have focus.** If theMRCalibration window is not the current active window, the controller actions may not be captured by the calibration program. 
-   **The Oculus system may not be configured to run from Unknown Sources.** As a part of Beta access, the calibration program is still in active development and has not been reviewed by Oculus. 
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98c459c9-2d32-4071-a38b-47fb5003bb80/mr_oculusunknownsourcessetting.png "MR_OculusUnknownSourcesSetting.png")
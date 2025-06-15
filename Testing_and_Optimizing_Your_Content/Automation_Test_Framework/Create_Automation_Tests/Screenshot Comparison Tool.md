# Screenshot Comparison Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/screenshot-comparison-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/screenshot-comparison-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:01

---

The **Screenshot Comparison** browser enables you or your quality assurance (QA) teams to quickly compare screenshots that are captured in the **Unreal Engine Editor**. The screenshots generated via an automation test can be viewed using the **Unreal Session Frontend** tool where a history of screenshots is maintained enabling obvious rendering errors to be identified between builds.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eebaf057-88c8-4697-ac55-fad9f9ffddbe/screenshotcomparisonbrowser.png)

Populated screenshot tests from Epic's own automation testing project.

## Screenshot Capture Methods

There are a couple of ways you can construct a screenshot test; the easiest way is to start using the Screenshot Functional Actor or to take a screenshot during an existing Functional Test.

#### Functional Test Actor Settings

The **Functional Screenshot Test** Actor uses a camera to capture the screenshot and because of this shares a lot of settings with the existing Post Process and Camera settings that are available. The settings listed below, are specific to the Functional Screenshot Test that are used to capture the screenshots you want.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11abd2d7-ae64-4d12-b664-1db36da9e280/ft_screenshotoptions.png)

| Setting | Description |
| --- | --- |
| **Resolution** | The desired resolution of the screenshot. If none is provided, the default resolution of the platform setup in the Automation Settings will be used. |
| **Delay** | The delay before the screenshot will be taken. |
| **Disable Noisy Rendering Features** | Disables Anti-aliasing, Motion Blur, Screen Space Reflections, Eye Adaptation (Auto-Exposure), and Contact Shadows because these features contribute a lot of noise in the final rendered image if you're explicitly looking for changes. |
| **Visualize Buffer** | Allows you to screenshot a buffer other than the default final lit scene image. This is useful if you're trying to build a test for a specific GBuffer that may be harder to tell if errors are introduced. |
| **Tolerance** | 
These are quick defaults for tolerance. By default, Low is used because there's some constant variability in every pixel's color introduced by Temporal Anti-Aliasing.

-   Zero
-   Low
-   Medium
-   High
-   Custom



 |
| **Tolerance Amount** | 

For each channel and brightness levels, you can control a region where the colors are found to be essentially the same. Generally, this is necessary as modern rendering techniques tend to introduce noise constantly to hide aliasing.

-   **RGBA Channels**: Set values for any of the RGBA channels separately.
-   **Min Brightness**: The minimum tolerance brightness value to accept.
-   **Max Brightness**: The maximum tolerance brightness value to accept.



 |
| **Maximum Local Error** | After you've accounted for color tolerance changes, you now need to control for local acceptable error. Depending on how pixels were colored on triangle edges, there may be a few percent of the pixels that fall outside of the tolerance levels. Unlike the Maximum Global Error, the Maximum Local Error works by focusing on a smaller subset of the image. These chunks will be compared to the local error in an attempt to local to locate hot spots of change that are important that otherwise would be ignored by the global error. |
| **Maximum Global Error** | After you've accounted for color tolerance changes, you now need to control for the total acceptable error. Depending on how pixels were colored on triangle edges, there may be a few percent of the pixels that fall outside of the tolerance levels. |
| **Ignore Anti-Aliasing** | If this is enabled, neighboring pixels will be searched for the expected pixel as what to what may have happened, such as the pixel shifting a little bit. |
| **Ignore Colors** | If this is enabled, the luminance of the scene is all that will be compared for the screenshot test. |

#### Editor Preferences

In the **Editor Preferences**, the default resolution of all captured screenshots for comparison can be set for all placed Functional Screenshot Test Actors. This can be set by going to **Edit** > **Editor Preferences** > **Automation** > **Screenshots**.

Click image for full size.

The screenshot resolution set on individual Functional Screenshot Test Actors will override this value.

### Functional Screenshot Test Actor

The **Functional Screenshot Test** Actor is a component that can be placed in your level and used to capture a screenshot as part of the automation tests that are run from Unreal Frontend. There are two varieties of screenshot tests that you can run; a normal screenshot that captures the scene view or one that is used to capture your games user interface (UI).

To access these Functional Screenshot Actors, use the **Place Actors** panel to drag one in your scene. You can find the Functional Screenshot Test and Functional UIScreenshot Test located in the **All Classes** tab.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b38fbf8b-6edd-43ba-86a7-7a5acc839815/modespanel.png)

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c527fae-122d-41b0-9f7a-8669e7fb3c79/screenshottest.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34c52626-1aef-4a4a-b29d-74796a847e3b/screenshotui.png) |
| Functional Screenshot Test | Functional UI Screenshot Test |

### Taking a Screenshot as part of another Functional Test

In addition to taking a standalone screenshot, you can also take a screenshot during a [Functional Test](/documentation/en-us/unreal-engine/functional-testing-in-unreal-engine) enabling you to utilize screenshot comparisons during other scripted actions.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bd67e63-2761-40dd-a66a-7315f1e68ab5/screenshotwfuncttest.png)

Blueprint example used to capture a screenshot during another Functional Test.

One thing to keep in mind is that you can customize the [screenshot settings](/documentation/en-us/unreal-engine/screenshot-comparison-tool-in-unreal-engine#functionaltestactorsettings) that are applied when capturing the screenshot. There are two useful Blueprint nodes you can should consider setting to default tolerances when capturing gameplay or rendering functionality for comparison.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8cf8bfa-bcad-4937-b474-3a94cf8e1185/getscreenshotdefauloptions.png)

The **Default Screenshot Options** node for gameplay and rendering are useful to set the default **Tolerance** level for the Screenshot Test Actor. When capturing gameplay differences, the **Gameplay** node can be useful to disable noise in the shot and buffers that aren't necessarily needed. If you're explicitly testing rendering functionality, the **Rendering** node should be used instead, otherwise, the default settings of the Functional Screenshot Test Actor will be used for each instance placed in the level.

## Screenshot Browser

The Screenshot Comparison browser is where all your screenshot comparisons will populate, and as you introduce new ones or if a screenshot comparison fails, this view is where you will take care of it. From this browser, you can review the failures and make the correct decision, which might be to update the screenshot if a feature change has necessitated the updated screenshot or enter a bug report for your game if you suspect there is an issue.

To access the Screenshot Comparison browser, you'll first need to open Unreal (Session) Frontend. You can do this from inside the Editor by selecting **Window** > **Developer Tools** > **Session Frontend**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49f9f463-85aa-4351-a293-851432c295f7/screenshotbrowsertab.png)

The Screenshot Comparison Browser from Epic's internal test project for Automation Testing.

When screenshots are captured they will be saved to the project's folder in the **Saved** > **Automation** > **Comparisons** folder. You can use the text box to enter your save location if necessary.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7a4665d-ec40-4d10-83f5-3e27ba15a991/comparisonsaveloc.png)

When several tests have been run, you'll have your own populated images for comparison. This will give you access to several options for what to do with these images when connected to Source Control. If you're not connected to any form of source control, these dialog options will be disabled.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a15ab25-49e6-4ae4-97ea-4c5da28fae3d/addnew.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82d0fd51-7e19-4004-a3cd-64c77cbf8c32/replacealternative.png) |
| Add New | Replace/Add As Alternative |

| Action | Description |
| --- | --- |
| **Add** | Adds the screenshot to the ground truth folder and adds it to a pending change list in your Source Control. |
| **Replace** | Deletes all examples of ground truth data and replaces them with the newest screenshot as the new ground truth data. |
| **Add As Alternative** | Occasionally, two images can both be correct. Perhaps due to small differences in hardware or driver or maybe even extensions the hardware supports. Because we only bucket screenshots based on Platform\_RHI\_ShaderModel, it's possible further refinement is needed. That's where **Add As Alternative** comes into play. It adds another ground truth version of the image, and when comparing images, the system will always pick the ground truth screenshot matching closest based on the metadata. This option will be grayed out if the screenshot is from an identical device. |

Always use **Delete All Reports** before running a fresh set of tests. Because the tool accumulates individual reports over time, there's no good place for the tool to automatically clean up reports from a previous run in the applications. This ensures that you start with a clean slate before running the next tests.

### Ground Truth Screenshot

The **Ground Truth** version of your screenshot is the version that you know is correct. For screenshot comparison, the ground truth screenshot will be used as the comparison for any later screenshots that are taken. Should the latest screenshot not match it will cause a testing failure.

The first time you run a screenshot automation test, a warning in the Message Log and the Screenshot Browser will indicate that you need to add the newly taken screenshot as your Ground Truth image.

|   |   |
| --- | --- |
| 
Click image for full size.

 | 

Click image for full size.

 |
| Message Log Warning | Screenshot Browser Warning |

In the Screenshot Browser tab, click the **Add New** button to create a change list to submit your Ground Truth image.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6917e15-6e95-49c1-a6fe-7dc4e4e685ea/screenshotaddnew.png)

If your **Add New** button is grayed out, make sure you're connected to your source control to enable it.

## Screenshot Comparison View

From the Screenshot Comparison browser, if you click on any of the images, a window will open that enables you to blend between the ground truth and the incoming image. This makes it easier to see all the differences in context with one another.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a40b2741-bfbf-4b92-ab58-e6c20e430388/comparisonimages.png)

The three images here (from left to right) are as follows:

-   **Ground Truth** is the image that you know to be correct.
-   **Difference** is the difference between the two images used for the comparison slider.
-   **Incoming** is the latest captured screenshot after an automation test has been run.

Click image for full size.

Click on any of the three images to open the comparison slider window. This screen enables you to drag the slider between the Ground Truth and the Incoming captured screenshot for comparison.

![Ground Truth](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2b13022-3d1e-4e58-aaf3-5eec639fc975/groundtruth.png)

![New Screenshot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f29c5d5-8af3-4c1a-8ca0-c169d369f4e9/comparison.png)

In this example, there is a noticeable difference between the set Ground Truth image that is known to be correct and the latest run automation test that capturing the Incoming screenshot.

## Screenshot Workflow

1.  You will start by picking a method that you would like to use to take the screenshot:
    
    -   [Screenshot Functional Test Actor](/documentation/en-us/unreal-engine/screenshot-comparison-tool-in-unreal-engine#functionalscreenshottestactor)
    -   [Taking a screenshot as part of another Functional Test](/documentation/en-us/unreal-engine/screenshot-comparison-tool-in-unreal-engine#takingascreenshotaspartofanotherfunctionaltest)
2.  When you run the test locally, or on a build farm, you will receive a warning letting you know that you need to approve the first screenshot.
    
    Click image for full size.
    
    In the **Screenshot Browser**, you add it as the Ground Truth image by clicking **Add New**.
    
    Click image for full size.
    
    For other platforms, the build farm can take care of the initial screenshot and you can remotely approve the screenshots taken on those platforms by providing the network path in the Screenshot Browser, which appears at the top of the automation report.
    
3.  The next time you run a **Screenshot Comparison** test, the screenshots should pass or fail. Use the **Screenshot Browser** to select a screenshot test and compare the differences.
    

Click image for full size.

For ones that fail, they will automatically show up in the Screenshot Browser tab for comparison so that you can choose to **Replace** or **Add as alternative** to the Ground Truth image.

Click image for full size.

If you are using [Source Control](/documentation/en-us/unreal-engine/source-control-in-unreal-engine), the Screenshot Browser will add them to a pending change list so that you the images can be checked in after the tests complete.
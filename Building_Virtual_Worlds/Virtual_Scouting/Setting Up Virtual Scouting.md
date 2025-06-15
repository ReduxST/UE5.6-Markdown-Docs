# Setting Up Virtual Scouting

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-virtual-scouting-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-virtual-scouting-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:58

---

This guide covers how to set up your headset to use the Virtual Scouting tools. For an overview of Virtual Scouting, refer to [Virtual Scouting](/documentation/en-us/unreal-engine/virtual-scouting-in-unreal-engine).

To use Virtual Scouting, you must set up a compatible VR headset, as well as the OpenXR runtime provider. Then, you can create an Unreal Engine project and enable the Virtual Scouting plugin.

## Set Up Your VR Headset

Virtual Scouting supports the following VR headsets:

-   Oculus Rift S
-   Meta Quest 2
-   Meta Quest Pro
-   Meta Quest 3
-   Valve Index

### Oculus and Meta Headsets

To set up your Oculus or Meta headset, you must install and start the Oculus Desktop. For install instructions, see Meta's [Install the Oculus PC app for Meta Quest Link](https://www.meta.com/en-gb/help/quest/articles/headsets-and-accessories/oculus-rift-s/install-app-for-link/) documentation.

When you start the Oculus Desktop and put on the headset, you should see a generic controller model.

![A generic controller model.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30767dad-1cc1-4c35-a923-9ffe3d8645f9/generic-controllers.png)

All of the button maps for Oculus and Meta devices are identical between the different headsets and their respective controllers. Button maps are the inputs that connect a controller button to an action.

#### Meta Quest Link - Cable

If you are using a USB-C cable, you must use the Meta Quest Link to connect to your Meta headset. For more information, see Meta's [Set up Meta Quest Link](https://www.meta.com/en-gb/help/quest/articles/headsets-and-accessories/oculus-link/set-up-link/) documentation.

#### Meta Quest Link - Wireless

To wirelessly connect your Meta headset to your PC, you must use the Meta Quest AirLink. For more information, see Meta's [Connect Meta Quest to your PC over Wi-Fi with Air Link](https://www.meta.com/en-gb/help/quest/articles/headsets-and-accessories/oculus-link/connect-with-air-link/) documentation.

#### SteamLink with Quest

You can connect your Meta headset to the SteamVR PC desktop software using the SteamLink app. For more information about the app and how to access it, see [Steam Link on Meta Quest](https://www.meta.com/en-gb/experiences/5841245619310585/) in the Meta store.

For best results, set up a dedicated wireless router connected by ethernet to your PC, and ensure that both the headset and router are in the same room. The quality and effectiveness of the wireless stream in VR is affected by the quality of the wireless network connectivity.

### Valve Index

Virtual Scouting supports the Valve Index headset and Index Knuckle Controllers.

![The Valve Index Knuckle Controllers.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5bd2384-cf92-465d-b682-9829f4d6f8e5/knuckle-controllers.png)

To set up your Valve Index headset, open the Steam client on your PC and start the SteamVR app.

Check the SteamVR window to confirm your headset and controllers are connected in the UI. You should see an icon for each of the following components:

-   the headset
-   the left controller
-   the right controller
-   any tracking cameras in your system

![The SteamVR window showing a connected headset, left and right controllers, and two cameras.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aaaa2ebf-ce60-40fb-be5f-a41aa87d0f43/steamvr-window.png)

### Set Up OpenXR Runtime Provider

If you are using a Meta or Oculus headset, ensure the Meta Quest Link desktop software is set to be your OpenXR provider.

To set the Meta Quest Link desktop software as your OpenXR provider, follow these steps:

1.  Open the Meta Quest Link desktop software.
2.  Click **Settings** > **General** > **OpenXR Runtime** > **Set Meta Quest Link as act…**

![The Meta Quest desktop settings dialog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93633d5a-1863-49ba-b4f1-e404271fc9dc/meta-quest-link.png)

If you are using a Valve Index headset or a Meta Headset with the SteamLink app, ensure SteamVR is set to be your OpenXR provider.

To set SteamVR as your OpenXR the provider, follow these steps:

1.  Open SteamVR.
2.  In the system tray, click **Settings**.
3.  In the settings dialog that opens, click **OpenXR** > **Set SteamVR as OpenXR Runtime**.

![The SteamVR OpenXR settings dialog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d87a8ac8-34f4-4cd6-87da-6c446573e9a9/steamvr-runtime.png)

### Confirm VR Rendering & Streaming

To confirm the Unreal Editor will render and stream to your headset, check that you can see one of the following scenes in your VR headset.

![The Meta Link PC desktop view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6acdd629-5cb0-486b-b70a-9977757c0cc7/meta-link-view.png)

The Meta Link PC desktop view

![The SteamVR PC desktop view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01b7a1c2-91b7-4880-a962-67a4614e2ce4/steamvr-view.png)

The SteamVR desktop view

## Set Up Virtual Scouting in an Unreal Engine Project

### Enable the Virtual Scouting Plugin

To enable the Virtual Scouting Plugin, follow these steps:

1.  Create a blank project in Unreal Engine.
2.  In the top toolbar, click **Edit** > **Plugins**.
3.  In the **Plugins** menu window, search for "Virtual Scouting" and enable the plugin.
    
    ![The Virtual Scouting plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cabe776e-7508-4960-8dcd-eaf858e80b45/vscout-plugin.png)
4.  Click **Yes** in the dialog popup and restart the engine.

#### VR Considerations

##### Remove VR Game Input Mappings

If you are using a project that already has VR Enhanced Input Actions pre-set, such as the VR Game template, you must remove all of these for Virtual Scouting to work correctly.

To remove VR Game Input Mappings, follow these steps:

1.  Click **Edit** > **Project Settings** > **Engine**.
2.  Expand the **Enhanced Input** category.
3.  Next to the **Default Map Contexts** header, click the delete icon.

![The Enhanced Input project settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8a36260-80f6-463f-b32d-0b053831beea/enhanced-input.png)

##### Rendering Considerations

Instance culling is not supported in VR. If your project has instance culling enabled (as it is in the [City Sample](https://www.fab.com/listings/4898e707-7855-404b-af0e-a505ee690e68) project), then you must disable it with the console variable `r.InstanceCulling.OcclusionCull=0`. To learn more about culling, see [Visibility and Occlusion Culling Reference](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-reference-in-unreal-engine).

**Lumen** and **Nanite** work in VR but, as of Unreal Engine 5.4, there is a significant performance demand when using Lumen. You may need to lower your project’s scalability settings to improve performance. You can lower screen percentage to improve performance but this will be at the expense of rendering artifacts, especially on text elements such as the VR Palette Menu.

##### Post Process Alpha Channel Support

To launch Virtual Scouting, you must disable alpha channel support for post-processing. Go to **Project Settings** > **Engine** > **Rendering** > **Default Settings**, then set **Alpha Output** to **False**.

##### Outline Stencil Support

The Virtual Scouting tools use stencil materials to draw outlines on objects (see [Content Placement Tool](/documentation/en-us/unreal-engine/using-the-virtual-scouting-tools-in-unreal-engine#contentplacementtool)). To enable outline stencils, go to **Project Settings** > **Engine** > **Rendering** and set **Custom Depth-Stencil Pass** to **Enabled with Stencil**.

### Project and User Settings

The Virtual Scouting Plugin has its own project and user settings, as well as plugin settings. You can also change the handedness of your VR controllers in the XRCreative Editor settings.

#### Project Settings

You can access the plugin settings from **Project Settings** > **Plugins** > **Virtual Scouting Settings**. These settings affect the project for all users if checked into a version control system.

![Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b046613-8c7b-4994-b280-b35578f06ff2/project-settings.png)

These settings include parameters that control the Virtual Scouting toolset, such as the unit system to use for measurements and the viewfinder exposure parameters.

If you modify the unit system, existing measurements retain their values stored in the previous measurement system until they are updated. New measurements automatically reflect the current state of the project settings.

#### User Settings

You can access the user settings from **Project Settings** > **Plugins** > **Virtual Production Editor** > **Legacy Virtual Scouting**. These settings are saved per user with your project’s data. They control the user’s preference for movement speed and tooltip visibility. You can modify these settings both in the editor and while you are in VR.

![User Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1beadce5-c7cc-451d-8c3f-67d8e7b9f5b7/user-settings.png)

#### XRCreative Editor Settings

You can access the XRCreative Editor settings from **Edit** > **Editor Preferences** > **XRCreative Editor Settings**.

![XRCreative Editor Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eabc4d36-fdec-4f4c-8742-b182ecddc4e8/xrcreative-settings.png)

The XRCreative Editor setting **Handedness** defines which hand your tools spawn into. You cannot change this setting while in VR.

By default, **Handedness** is set to **Right**. Left-handed mode is an exact mirrored control set, swapping functionality between hands.

### Setting the VR mode

To set the VR mode for Virtual Scouting, on the main toolbar, next to the VREditor button, click the **ellipses (...)** dropdown.

![VREditor Button and Mode selection drop down](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3257eb26-1dfe-4ae0-89ec-f0efe9682c66/vreditor-mode.png)

Ensure the Scouting Default mode is selected. To learn more about the customization of VREditor modes, see [Create a New XR Creative Mode and Toolset](/documentation/en-us/unreal-engine/customizing-virtual-scouting-in-unreal-engine).

### Launch Into VR

To start the Virtual Scouting toolset and view your level in VR, click the VREditor button.

![VREditor Button on Main Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0cbfb72e-19f8-4e8b-af36-3298094f0c12/vreditor-launch.png)

To learn more about using the Virtual Scouting toolset, see [Using the VR Tools](/documentation/en-us/unreal-engine/using-the-virtual-scouting-tools-in-unreal-engine).
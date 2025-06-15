# Virtual Reality Spectator Screen

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-reality-spectator-screen-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-reality-spectator-screen-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:13

---

Please refer to our PlayStation VR (PS VR) Spectator Screen documentation if you're developing for PlayStation.

If you've ever wanted to be a Virtual Reality (VR) Spectator (from a third-person perspective) while others are interacting with a VR environment (from a first-person perspective), then Unreal Engine 4's (UE4) **VR Spectator Screen** is the ideal feature for you. While running the VR Spectator Screen, you'll be able to observe other players with your computer monitor (or television), which is valuable when you're gathering feedback on an immersive VR experience.

*Images Courtesy of [GhostPaint.com](http://ghostpaint.com/)*

|   |   |
| --- | --- |
| ![VRSpecScreen.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/514cee1b-a642-4ea0-af13-86f232cf1b7d/vrspecscreen.png) | ![VRPlayerPerspectiveScreen.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed4407eb-7ca2-4bc8-a1e6-a03267b04d41/vrplayerperspectivescreen.png) |
| VR Spectator Screen Perspective | VR Player's HMD Perspective |

*On the left side, you (the spectator) are watching this artist paint a brick wall in VR, while on the right side, the artist is focusing on the painting in VR.*

Depending on the Head Mounted Display (HMD) manufacturer, a VR Spectator Screen could be synonymous with a VR Social Screen; or VR Spectator Mode could be synonymous with VR Mirror Mode. Within the context of this documentation, the **Spectator Screen** is a standard output device (such as a computer monitor or television) that is connected to a VR device. Additionally, enabling **Spectator Mode** means that you can observe (or, in certain scenarios, interact) with the VR experience while a player uses a HMD in a VR environment.

## Supported Platforms

The following platforms currently support Spectator Screen Mode in UE4:

-   [HTC Vive](https://www.vive.com/us/)
-   [Oculus Rift](https://www.oculus.com/rift/)
-   [Steam VR](http://store.steampowered.com/steamvr)
-   [PlayStation VR (PS VR)](https://www.playstation.com/en-us/explore/playstation-vr/?emcid=pa-pe-97928)

Although we expect this feature to be supported by other personal computing devices and consoles, we don't anticipate Mobile VR devices (platforms) to support this feature.

## Getting Started with Spectator Screen Mode

With the exception of PS VR, Spectator Screen Mode is enabled by default in UE4.

When working with textures in Spectator Screen Mode, the upper left coordinate represents minimum coordinate values, while the lower right coordinate represents maximum coordinate values.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80b76a17-ede8-4af7-801c-fd9d7ca277e7/vrspec_bptexturecoordinate.png)

## Spectator Screen Blueprint Nodes

For the Example Usage, we're using the following Blueprint interface:

| Node | Description |
| --- | --- |
| **[Set Spectator Screen Texture](/documentation/en-us/unreal-engine/set-spectator-screen-texture-in-unreal-engine)** | This node changes the texture being displayed on the Social (Spectator) Screen. |
| **[Set Spectator Screen Mode Texture Plus Eye Layout](/documentation/en-us/unreal-engine/set-spectator-screen-mode-texture-plus-eye-layout-in-unreal-engine)** | This node sets up the layout for the TexturePlusEye function in ESpectatorScreenMode. |
| **[Set Spectator Screen Mode](/documentation/en-us/unreal-engine/set-spectator-screen-mode-in-unreal-engine)** | This node sets the Social (Spectator) Screen mode. |

### Example Usage

1.  Go ahead and set up a VR project for one of the platforms that support a Spectator Screen.

1.  Now, you'll want to create a new Blueprint script, specifying the image that you want to render to the Spectator Screen. For illustrative purposes, the following Blueprint nodes respond to three Keyboard inputs:
    
    1.  For example, when the **1** key is pressed, this first Blueprint node specifies a static texture, which will be drawn in the Texture area.
        
        ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/248175ae-80e6-4c7a-8856-2d55346ab292/vrspec_bp_1.png)
    2.  When the **2** key is pressed, this second Blueprint node specifies a layout where the HMD eye view is being drawn to the entire screen (with the Texture being drawn in the upper left quadrant of the screen). Additionally, this node specifies the Texture layout while making sure to draw the Eye layout first.
        
        ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc7bac1d-23d4-48ce-ba00-7629726fb94a/vrspec_bp_2.png)
        
        The Eye and Texture rectangle minimum and maximum values are normalized between `[0.0, 1.0]`.
        
    3.  Finally, when the **3** key is pressed, this third Blueprint node enables (thereby switching to) **TexturePlusEye** mode.
        
        ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9339e78f-39b5-4345-9bff-8e9b6ec4597d/vrspec_bp_3.png)

### End Result

In summary, your new Blueprint sets the Spectator Screen's Texture (along with its Eye and Texture layout) along with the Spectator Screen Mode that you'd like to use.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38cfbdac-698c-4004-bf63-b596a7a78f3c/vrspec_bp.png)

Although the Texture can serve as a render target (which you can write to from a **SceneCaptureComponent2D**), or a container for User Interface elements, it's important to note that **SceneCapture** can be computationally expensive.

If you want to test different Textures or layouts at runtime, you can switch the Texture (or even the layout) while Spectator Screen Mode is active.

## Switching Modes

If you'd like to switch to a new Spectator Screen Mode, you can open the Console and input `vr.SpectatorScreenMode` **Value**. For example, entering `vr.SpectatorScreenMode 2` enables **Distorted** mode, which is currently supported by Oculus Rift.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20447f64-7025-469e-911a-eee394cb7cff/vrspec_cvarexample.png)

### Supported Modes

Depending on your platform, certain Screen Spectator Modes are supported, including the following:

| Value | Mode | Oculus Rift | SteamVR | PS VR | Notes |
| --- | --- | --- | --- | --- | --- |
| **0** | Disabled | ✓ | ✓ |   | For the best performance on HMDs, this mode disables Spectator Screen output. |
| **1** | SingleEyeLetterboxed | ✓ | ✓ | ✓ | This mode is primarily intended for debugging purposes, showing only one letterboxed eye on the screen. |
| **2** | Undistorted | ✓ | ✓ | ✓ | This is a debug mode, showing the entire rendered area for both eyes. |
| **3** | Distorted | ✓ |   |   | This mode is only supported by Oculus. Specifically, this is an Oculus specific debug mode, showing chromatic abberations, etc. |
| **4** | SingleEye | ✓ | ✓ | ✓ | Much like the **Undistorted** mode, this a debug mode for only one eye. Because this mode stretches the scene, it may be useful for identifying small artifacts in the scene. |
| **5** | SingleEyeCroppedToFill | ✓ | ✓ | ✓ | This mode crops the eye to fill the entire screen. |
| **6** | Texture | ✓ | ✓ | ✓ | This mode shows a full screen view of a specified **UTexture**. |
| **7** | TexturePlusMirror | ✓ | ✓ | ✓ | This mode shows a Texture in one render rectangle, whereas, the eye is shown in another render rectangle. |

## Optimizing Spectator Screen Mode

Currently, there is no standard optimization setting for Spectator Screen mode. If you'd like to implement your own optimization solution for Spectator Screen mode, it's recommended to perform scene captures at 30 fps (assuming your VR application is running at 60, 90, or 120 fps). Additionally, it's recommended to limit the Spectator Screen output to 30 fps. Please be aware that if you attempt to limit Spectator Screen output on certain hardware, you might run into rendering issues if the VR framerate is running at 90 fps (basically, every third frame will be dropped).

## Currently Known Issues for Version 4.17

-   RenderTargets created at runtime are not assigned as the Spectator Texture until one frame has passed, thereby silently failing until the application's first frame has already been rendered.
-   Currently, if a RenderTarget is destroyed (released) while being assigned as the Spectator Texture, the application might crash.
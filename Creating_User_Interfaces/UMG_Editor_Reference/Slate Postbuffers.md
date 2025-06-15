# Slate Postbuffers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-slate-postbuffers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-slate-postbuffers-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:56

---

![Example of a Slate postbuffer creating a VHS blur](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6689b698-d373-4b58-910b-52a9739cd2dc/heroimage.gif)

**Slate postbuffers** sample the game scene for use in UI materials, similar to how SceneColor is used in postprocess materials. This makes it possible for you to create visual effects that apply to both your game world and your user interface. Slate postbuffers can also potentially apply a **Slate postprocess** class to handle a broad postprocess such as a blur effect.

Some example use-cases for Slate postbuffers include:

-   Blurring the scene behind a transparent popup message.
-   A vignetting effect to show damage or darkness.
-   A screen-wide blur that selectively obscures widgets as well as the game world.
-   A distortion filter that looks similar to a worn VHS tape.

Each of the above examples is available in the **UI\_SlatePostBuffer** level in the [Content Examples](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine) project.

This page provides:

-   An overview of the workflow for using Slate postbuffers.
-   Technical information about how Slate postbuffers function and their limitations.
-   Instructions for how to:
    -   Enable Slate postbuffers.
    -   Configure your Slate postbuffers.
    -   Create a new Slate Post Processor class.
    -   Integrate a Slate postbuffer into a material and apply it to a UI element.

## Overview

Slate postbuffers and postprocessor classes are global resources, so you should communicate with your entire team about how your project uses them.

UE supports up to 5 Slate postbuffers, which each sample the game scene for use in UI materials. You can set a Slate postprocessor class for each postbuffer to apply a broad postprocess to that buffer before you use it in a UI material. If there is no postprocessor, it will just sample a copy of the game scene.

![The Slate RHI Settings in Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddd09e95-103b-4ced-8742-07271a4c49c3/slaterhisettings.png)

A UI material can sample a postbuffer using the **GetSlatePost** functions. For example, `GetSlatePost0` samples Slate Postbuffer 0, while `GetSlatePost4` samples Slate Postbuffer 4. UI materials can use Slate postbuffers similarly to how post-process materials sample a scene with SceneColor.

![Example of the GetSlatePost node in use](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15407ab3-61ed-4ac6-98e9-5c19f05a048b/getslatepost.png)

When you apply your UI material to a widget, it will use the widget to apply the material’s postprocess to the portion of the screen behind it. The following example uses inverted Y axis UV coordinates to flip the portion of the viewport within a square widget upside-down.

![Example of a picture-in-picture with inverted UV coordinates from the Content Samples project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2cb12c2-3bf8-4f5c-8175-defaf4b696b9/contentsample3.png)

As a more complex example, the following screenshot shows a widget distorting the screen to look like a worn VHS tape. The widget applying the VHS distortion material takes up the entire screen and is layered on top of other widgets within the UI. This makes it possible for UE to process the UI and game scene together, so you can control elements like the date and timecode with text widgets in the UMG Blueprint.

![Example of a Slate postbuffer creating a VHS blur](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e063df33-68d2-423a-9431-2cad4ae12588/heroimage.png)

By default, the GetPostBuffer nodes sample directly behind your UI widgets. To learn how to override them, see the section below on Tips for Using Postbuffers in UI Materials.

## Enable Slate Postbuffers

To enable Slate postbuffers, add the following CVar to your project’s \*Engine.ini file:

DefaultEngine.ini

```
	`[ConsoleVariables] 	Slate.CopyBackbufferToSlatePostRenderTargets=1`
Copy full snippet
```
\[ConsoleVariables\] Slate.CopyBackbufferToSlatePostRenderTargets=1

Alternatively, you can use the following console command to enable this CVar:

Console

```
	`-dpcvars=Slate.CopyBackbufferToSlatePostRenderTargets=1`
Copy full snippet
```
\-dpcvars=Slate.CopyBackbufferToSlatePostRenderTargets=1

## Configure Slate Postbuffers in Your Project Settings

To configure your postbuffers:

1.  Open your **Project Settings**.
    
2.  Navigate to **Game** \> **Slate RHIRenderer Settings** > **Post Processing**.
    
3.  Unfold the drop-down for buffers that you want to configure. You can enable or disable each buffer as needed.
    
    ![Enable the postbuffer in your project settings.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6f3bc7b-abe6-4dfb-8c41-779cbedef3b3/enablepostbuffer.png)
4.  If you want to add a specific postprocess to a Slate postbuffer, select a **Post Processor Class** for it.
    
    ![Set the post processor class alongside your postbuffer settings.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9aa39285-6ad7-4687-838e-46d63cc858af/setpostbufferclass.png)

## Create and Use a Slate Post Processor Class

To create a new Slate postprocessor class:

1.  Create a **new Blueprint Class** derived from **USlateRHIPostBufferProcessor** or one of its child classes. This tutorial uses USlatePostBufferBlur as an example.
    
    ![Use the Slate postbuffer blur class as the base for a new Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13967141-d88f-433b-af11-08db13419d7a/inheritslatepostbufferblur.png)
2.  Open the Blueprint for your new postprocessor, then edit the class defaults. Change the default setting for **Gaussian Blur Strength** to something other than the default value inherited from the parent class. In this example, the Gaussian Blur Strength is set to 10.0.
    
    ![Set the blur strength for the derived postbuffer blur class.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8063701-9398-4012-bdbe-f84016b36954/setblurstrength.png)
3.  Open **Project Settings** > **Slate Renderer Settings** > **Post Processing**, unfold the dropdown for one of your postbuffers, and set the **Post Processor Class** to your new postprocessor.
    
    ![Set the blur postprocessor on one of the postbuffers.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed0d9b6d-b613-42a4-9cc2-4c11fe557aaa/setblurprocessor.png)

UE now uses your postprocessor to process the backbuffer before widgets copy it. In this case, it adds a gaussian blur.

You also can implement your own postprocessor by deriving a new C++ class from `USlateRHIPostBufferProcessor`.

### Modify a Slate Post Processor at Runtime

You can modify your Slate postprocessors’ values at runtime using the **Slate FX Subsystem**.

1.  Create a **Slate FX Subsystem** node.
    
2.  Call **Get Slate Post Processor** to get a postprocessor from one of your postbuffers.
    
3.  Cast the postprocessor to the appropriate class.
    
4.  Access the postprocessor’s parameters from the casted postprocessor object.
    
    ![Modifying a blur postprocessor at runtime in Blueprint.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2738a747-9cb3-4546-ac59-18e8684a02bd/modifyblurexample.png)
    
    The above image is only an example of how modifying a postprocessor at runtime looks. We do not recommend performing this operation on tick as depicted.
    

Because Slate postbuffers and postprocessors are global resources, if you modify a Slate Post Processor’s value as in the example above, it will change the value globally. Every instance of a Slate widget or UI material that uses this postprocess will therefore reflect that change. Use caution and communicate with your entire team before modifying Slate postprocess values at runtime.

## Use the Postbuffer in a UI Material

To create a UI material that samples the postbuffer:

1.  Create a new **Material**.
    
2.  Set the Material’s **Material Domain** to **User Interface**.
    
    ![Set the material's domain to User Interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d4f9f1a-ace7-4de7-94df-9d16ddb03c5f/uimaterialdomain.png)
3.  To sample a buffer, call the **GetSlatePost** function corresponding to the postbuffer you want to use. For example, `GetSlatePost0` gets Slate Postbuffer 0.
    
    ![Use a GetSlatePost node to get a postbuffer.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43b8a393-11f3-4d33-add8-24df83c5545d/getslatepost.png)

### Tips for Using Postbuffers in UI Materials

The following are some tips for using postbuffers in UI materials:

-   By default, GetSlatePost nodes only sample pixels behind the current widget, but you can modify this using the **UVs** input.
-   Use **LinearRGB** to get a gamma-correct sampling of the backbuffer.
-   **RGB** is useful for effects such as correct color inversion.

The following graph is an example of a material that uses a postbuffer to create a rotating UE logo that inverts the colors of the world behind it. The UE logo texture feeds into the Opacity output, while the Final Color inverts the RGB output of GetSlatePost0.

![A material that inverts and blurs portions of the buffer.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aee5b63a-74f5-40fd-96b8-1c5566c0279f/invertblurexample.png)

This material is used in the image below. Note that the material samples the scene directly behind the widget despite having no UV input to `GetSlatePost0`.

![The previous material in use on UE logos in frame.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ced988a2-196f-4195-a28c-847d9708cd29/invertexample.png)

### Capture UI Widgets in Your Postbuffer

By default only the scene will be captured by GetSlatePost nodes. However, you can capture both the scene and other UI widgets using a **Post Buffer Update Widget** to tell Slate when to capture the UI. To capture UI in your postbuffer:

1.  Find the **Post Buffer Update Widget** in the Palette in UMG Designer.
    
    ![The Post buffer update widget in the palette.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62132b8d-e726-4a49-a274-c5275a68a889/postbufferupdatewidget.png)
2.  Add the Widget wherever you want a current UI update. The Slate postbuffer will update wherever this widget is placed.
    
    ![An example of the update widget placed in the hierarchy.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37c46edf-c300-4c0d-baf9-e6eba90bcf65/addwidgetupdate.png)
    
    We recommend putting the update widget as the last element within your hierarchy to ensure it draws after (or on top of) whatever widgets you would like to sample.
    
3.  Configure the Post Buffer Update Widget in the Details panel.
    
    ![Configuring the details of the post buffer update widget.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f1bf171-9630-4533-b637-cd2ba5511abd/configuredetails.png)

The Post Buffer Update Widget has the following parameters:

| **Parameter** | **Description** |
| --- | --- |
| **Perform Default Post Buffer Update** | If true the default scene-only copy / slate postprocess will occur. Else the default copy / process will not occur. If no postbuffer updates have been "drawn" and this setting is off, when a widget attempts to sample the slate postbuffers the behavior is undefined. (The result may be the last frame or black / white - avoid this scenario.) |
| **Buffers to Update** | Array of Buffers this widget should trigger a sampling of the UI + Scene for. Should correspond to the expected usage of GetSlatePost nodes from this point in the UI. |

Once you configure your Post Buffer Update Widget, future widgets can freely sample both the Scene and UI with any applied post FX for the buffers you select to update.

### Postbuffer and Draw Order

For postbuffer updates to function correctly, Slate must draw all the UI elements the postbuffer will sample *before* the postbuffer can sample them. Putting the postbuffer in an overlay within a vertical / horizontal / grid box might not guarantee this due to drawing out-of-order. As a guideline:

-   The bottom layer of your hierarchy should be widgets you want to show postbuffer-affected visuals.
-   The middle layer should contain the postbuffer widget.
-   The top layer should be a material that samples the postbuffer and applies the effect to the bottom layer.

The following image demonstrates an effective draw order:

![An example hierarchy.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0fa9ab1-5fae-470e-a1ac-9e824a9fec92/examplehierarchy.png)

The following images demonstrate the material applied to the images in the horizontal box:

![An example material that blurs the inside of a horizontal box.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0bc1885f-d6cc-4fdf-b592-02e0098485bf/materialexample.png)

## Technical Information and Limitations

The following are some technical insights and limitations on how Slate postbuffers behave.

### Sampling

GetSlatePost nodes sample a once-per frame processed copy of the scene backbuffer for widgets to sample. These buffers are global, thus you need team planning to use them. Since materials sample a copy of the backbuffer, widgets drawn on top will not sample lower widgets unless you use the Post Buffer Update Widget.

### Performance and Blur Postprocesses

Expect blur postprocesses to have a higher performance cost in proportion to the amount of blur you are using. In other words, a 32 pixel blur has a higher performance cost than a 16 pixel blur. The following table shows performance measurements taken from rendering a frame of a game scene. These measurements were taken on an RTX 3080 using Renderdoc on UE 5.4.

| **Blur Strength (Pixels)** | **Kernel Size** | **Blur time in Micro-seconds (us)** | **Total GPU Frame Time** | **GPU Percentage Use****d by Blur** |
| --- | --- | --- | --- | --- |
| 72 | 28x28 | 93 us | 8272 | 1.1% |
| 256 | 97x97 | 212 us | 8254 | 2.5% |

The figures above are mainly intended to give you an idea of the relative performance difference between blur sizes. They do not necessarily reflect the current performance of either Unreal Engine or the current generation of hardware.

#### Multiple Post Processors

When you use multiple postbuffers with postprocesses on them, you only pay the performance cost for the postprocesses actually visible onscreen. For example, if you have two postbuffers that each use a blur postprocess with a different value:

-   If only one of them is visible, you only pay for that one.
    
-   If both are visible, then you pay for both of them.
    

### Minimizing Buffer Usage

Each buffer is only copied/populated if a widget is drawn that uses the buffer. When a buffer is not used for two frames, it is resized on the GPU to 1x1.

### HDR Support

Slate postbuffers support **HDR**. However, when using HDR, materials should **sample from RGB** instead of LinearRGB. Additionally, HDR support only works immediately with HDR Composite off. If you want to use HDR composite you may need to correct gamma values during use.

### Cached Buffer Usage

Widget materials cache postbuffer usage on material/texture creation and on resource update, but does not update this cached value per draw.

Because of this caching, if you run with the global CVar Slate.CopyBackbufferToSlatePostRenderTargets turned off, you may get stuck with materials showing no usage. In this scenario, materials attempting to use the postbuffers may only sample black / white. If this happens, you may need to restart if you want to clear the usage cache and get correct results. We encourage enabling Slate.CopyBackbufferToSlatePostRenderTargets in your \*Engine.ini or early on when testing.

When resizing in PIE with Post Buffer Update Widgets, sampling results may be black/white temporarily during the resize. This issue occurs because we are more conservative on postbuffer update widgets when it comes to size checking. This only occurs in PIE since PIE is more active about drawing during resizes due to drawing the editor. This does not occur in Standalone or Shipping builds.
# Blend Spaces

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:12

---

Blend Spaces are assets that allow multiple animations or poses to be blended by plotting them onto either a one or two-dimensional graph. This graph can then be referenced within [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) where the blending can be controlled by gameplay input or other variables. By using Blend Spaces, virtually any type of blending arrangement can be used for your animations.

This document provides an overview of Blend Spaces, their different types, and their setup.

#### Prerequisites

-   Your project has a **Skeletal Mesh** with various directional or similar **Animation Sequences** imported.

## Blend Space Overview

Blend Spaces are assets where you specify animations along a graph at various points, called **samples**. The overall animation is calculated by blending between the points on the graph based on input values for each axis. For example, a locomotion system that blends between directional movement and idle animations can be created.

![blend space overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f95c004-277a-44ab-9e13-e6c3758f7dcd/overview.gif)

## Blend Space Creation and Types

There are different types of Blend Spaces, which provide different functionality in either the asset editor, or how they are used within [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine).

The following Blend Space types can be created by clicking on the **Add (+)** button in the Content Browser, then selecting from the **Animation** menu:

-   **Aim Offset**
-   **Aim Offset 1D**
-   **Blend Space**
-   **Blend Space 1D**

![create blend space](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f767f131-dea6-4214-9778-2ad6b8433625/creation.png)

### Blend Space

Regular Blend Spaces are the base variety of Blend Space, which provides all the main functionality of blending animations along the graph. They are intended to be referenced within Animation Blueprints as a base layer, with secondary animations proceeding from it.

![blend space type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54df0415-b872-4f54-a096-1863d039a2fd/typeblend.png)

### Aim Offset

Aim Offsets are Blend Spaces meant to contain mesh-space additive animations as their samples. Typically, these are used to create weapon or other look-at aiming blend spaces. Aim Offset Animation Blueprint nodes are intended to receive an input pose along with the normal axis inputs

![aim offset type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d179e665-a5d9-459b-8233-a97212ca7334/typeaim.png)

Refer to the [Aim Offsets](/documentation/en-us/unreal-engine/aim-offset-in-unreal-engine) page for more information on how to use them.

### 1D

Both Blend Spaces and Aim Offsets also support single-axis (1D) variants. Typically these Blend Spaces are used when you only need a single axis of blending. In the case of Blend Space 1D or Aim Offset 1D, the graph only provides a horizontal axis.

![blend space 1d](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8eb29b2b-5764-4dd6-bb9f-152c26d1fa15/1danim.png)

Although 1D Blend Spaces are available, normal 2D graphs can also be used in a one-dimensional way by only using a single axis for your sample placement. This way, you can expand the Blend Space from 1D to 2D if needed.

## Blend Space Setup

After creating and opening your Blend Space type, proceed with the following setup.

### Defining Axis Names and Ranges

In most cases, you will want to define the names and value ranges of the axes used in your Blend Space. To do this, navigate to the **Asset Details** panel and change the following properties located in the **Axis Settings** category:

-   **Name**
-   **Minimum Axis Value**
-   **Maximum Axis Value**

![blend space axis value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c5e6dbc-0e06-4245-9acc-e7a5e2fad6c1/axis.png)

Depending on the type of Blend Space, you may want to use different value scales, such as **\-90** to **90**, or **\-180** to **180** if you are creating an Aim Offset and want your grid to match rotation values.

### Adding Animations to the Graph

You can populate the graph with animations by dragging them from the **Asset Browser** or **Content Browser** onto the graph. Holding **Shift** will cause the animations to snap to the grid points which can be useful for alignment. Depending on what kind of Blend Space you want to create, these can either be looping animations or static poses.

![blend space add animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d95b78c6-d26f-4104-9f9a-75487f66e195/addanims.gif)

Because 1D Blend Spaces only have a single axis for input, you can only apply animations along that single axis.

![blend space 1d graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ad55cec-4645-40d3-a573-db083f7b9158/1danim.png)

In this example, the vertical and horizontal axes are mapped to the direction and speed, respectively. Several cycle-based animations are then set up to blend appropriately based on the values of these inputs resulting in the final pose you see in-game.

![blend space graph axis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d84650f4-2361-4d12-a886-31713471eb1b/axis2.png)

### Referencing in Animation Blueprints

Once you have a completed graph, you can reference and manipulate the [Blend Space in Animation Blueprints](/documentation/en-us/unreal-engine/blend-spaces-in-animation-blueprints-in-unreal-engine). To add your Blend Space, right-click in the **AnimGraph** and locate your Blend Space. You can also drag it from the **Content Browser** into the graph. Doing this creates a **Blend Space player**, which references the asset

![blend space animation blueprints](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fcb0385-8329-479f-bf0a-82d8a954a532/animbp1.png)

Refer to the [Blend Spaces in Animation Blueprints](/documentation/en-us/unreal-engine/blend-spaces-in-animation-blueprints-in-unreal-engine) page to learn more about using Blend Spaces in [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine).

## Editor Overview

Regardless of the Blend Space type being used, the following editor is displayed when opening one of these assets:

![blend space editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e130f4a0-3d70-43f0-a992-dc6311b4d1b4/editoroverview.png)

1.  [**Asset Details**](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine#assetdetails), where you can set properties and other settings for this Blend Space.
2.  **Viewport**, which displays the Skeletal Mesh and current playing animation according to the graph.
3.  **Asset Browser**, which can be used as a convenient location to drag animations into the graph.
4.  [**Blend Graph**](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine#blendgraph), where you plot your animations along either a one or two-dimensional graph and preview the blending functionality.

### Asset Details

The Asset Details panel contains properties and other settings for this Blend Space asset.

![asset details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1eaadafe-f9b4-4a2a-9fd2-8f68b106517f/assetdetails.png)

| Name | Description |
| --- | --- |
| **Use Grid** | Enabling this will use the legacy grid mode for blending, as opposed to the default triangulation method. Typically, you would only use the grid if you are performing specific blending arrangements, such as using Wrap Input. Otherwise, in most cases you should leave this disabled and instead use triangulation for more accurate blend results. |
| **Preferred Triangulation Direction** | 
Controls the triangular blend angle between samples. This will only affect samples that are placed in a uniform manner and only if **Use Grid** is disabled.

-   **None** will cause the triangles to have the same angle along the entire graph. Typically, you should not pick this option if you are creating a symmetrical Blend Space as the blending result will be different on each side.
    
    ![triangulation direction none](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9abadebe-4b72-43c8-adaa-57324455f19e/trianglenone.png)
    
-   **Tangential** will cause the triangles to face outward from the graph origin.
    
    ![triangulation direction tangential](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8857f8bc-f6e5-48fb-8ecc-934f981c6d2a/triangletangential.png)
    
-   **Radial** will cause the triangles to face inward to the graph origin.
    
    ![triangulation direction radial](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34d549f4-a847-41eb-b2d8-4b824b43a9c7/triangleradial.png)
    



 |
| **Axis to Scale Animation** | If **Smoothing Time** is being used, then this specifies the axis on which to scale the animation playback speed. In most cases this would be used for locomotion animations where you would specify the axis for speed. |
| **Name** | The name of the axis to display in the Blend Graph and on the Blend Space Animation Blueprint node. |
| **Minimum Axis Value** | The minimum displayed value for this axis. |
| **Maximum Axis Value** | The maximum displayed value for this axis. |
| **Grid Divisions** | The number of divisions on this axis. Higher values here will result in more precise blending results. Odd numbers will also provide different blending results from even numbers. If **Use Grid** is disabled, then this will only cause cosmetic changes for the grid. |
| **Snap to Grid** | Enables snapping to the **Grid Divisions** when moving animation points along this axis. Holding **Shift** will also temporarily enable snapping for all axes. |
| **Wrap Input** | When enabled, the input value for this axis can exceed the **Minimum** and **Maximum Axis Values**. When this occurs, the Blend Space will treat the axis as circular and convert the input to the inverse value on the other side. If you enable this property, ensure the animations on either end of the axis are similar to prevent popping. |
| **Smoothing Time** | 

The time in seconds for this axis to blend between different inputs. A value of **0** will cause no time blending to occur. You can preview the blend within the graph by observing the secondary crosshair moving independently of your preview point.

![smoothing time](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4059874-885e-4b7a-9de8-34d46b9c05f8/smoothingtime.gif)

 |
| **Smoothing Type** | 

Determines which easing function is used if Smoothing Time is used. You can select from the following:

-   Averaged
-   Linear
-   Cubic
-   Ease In/Out
-   Exponential
-   Spring Damper



 |
| **Damping Ratio** | 

When using **Spring Damper** for the **Smoothing Type**, this determines how much damping there is. Values less than **1** will result in overshoot, which can make some motions look more natural.

![blend space damping ratio](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f8d2765-cb2f-4d23-b05d-216b34295431/damping.gif)

 |
| **Max Speed** | The maximum rate of change of this axis value when smoothing. Only used when the **Smoothing Type** is set to **Spring Damper** or **Exponential**. If set to **0**, then blending speeds can be limitless. |
| **Analysis** | 

You can specify a function to be used per axis to analyze and automatically place the samples in the Blend Space. Refer to the [Blend Space Analysis](/documentation/en-us/unreal-engine/automatic-blend-space-creation-in-unreal-engine) page for more information.



 |
| **Blend Samples** | This section lists all the samples involved in the Blend Space, allowing their details to be modified or deleted. You can also preview these same properties by right-clicking on the sample in the Blend Graph. |
| **Weight Speed** | This controls the speed at which the individual sample weights can change. A value of **2.0** means that a sample can have its weight change from zero to one in half a second. A value of **0.0** disables this feature, unless you are using **Per Bone Overrides**. In general, do not use this in conjunction with **Smoothing Time** or **Smoothing Type**. |
| **Smoothing** | Enables easing in and out of the Weight Speed. In general, do not use this in conjunction with **Smoothing Time** or **Smoothing Type**. |
| **Per Bone Overrides** | An array where you can specify different Weight Speeds for Bones to blend at a different rate. Bones specified here will also include all descendants. |
| **Preview Base Pose** | If you are using additive animations in a Blend Space or Aim Offset, then you can specify a base animation here to preview the additive animations from. |
| **Notify Trigger Mode** | 

The current mode used by this Blend Space to control how [Animation Notifies](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine) trigger when blending between multiple samples. You can select from the following:

-   **All Animations**, which will trigger all notifies.
-   **Highest Weighted Animation**, which will only trigger the notifies from the sample with the highest weight.
-   **None**, which will cause no notifies to trigger.



 |

### Blend Graph

The Blend Graph is the primary interaction panel within a Blend Space. Here you will place and manipulate animation samples, preview the blending behavior, and debug blending problems.

![blend space graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a788a222-808b-4eb6-afc5-ac02ee6d5c0f/blendgraph.png)

#### Toolbar

Clicking **Show Triangulation** enables or disables the triangulation view. This button only appears if **Use Grid** is disabled from the **Asset Details** panel, which enables triangulation as the blend method.

![blend space triangulation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11c0d5fa-5034-41e1-adf5-98f2567f4a8d/showtriangulation.gif)

Clicking **Show Samples** enables each sample to display its name.

![blend space sample name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9762fe97-57c2-4b35-a765-c1b5e0bdf1dd/showsamples.png)

You can stretch the graph to fit the panel by clicking **Stretch Grid to Fit**. Disabling this will cause the graph to maintain relative scale based on each axis range.

![blend space graph stretch](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a159401-1e4c-42e8-80ba-88e998338abd/stretch.gif)

If a sample is selected, it will display its axis coordinates in the toolbar, which can be manipulated.

![blend space sample values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9dd1f23d-e3e2-408c-a6bd-a74736ec7ad4/sampletoolbar.png)

These toolbar settings are also accessible in the context menu when right-clicking in the graph.

![blend space graph context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/020229cf-fa2d-492d-8b43-e77fe8139523/toolbarcontext.png)

#### Interaction

Samples can be moved by dragging them within the graph. Holding **Shift** will snap them to the grid increments defined in the **Grid Divisions** property for that axis.

![blend space move sample](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49fd8e29-d5f8-4afb-800d-299563a21c9a/interaction1.gif)

Right-clicking a sample will show a context menu where you can edit its **Blend Sample** properties.

![blend space sample context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a74eedca-1798-4d06-8a60-5aeb94e92f79/toolbarcontext2.png)

#### Previewing

Holding **CTRL** and moving your cursor within the graph will preview the blend at that position, which is marked by a green crosshair. If you are using **Smoothing Time** properties, then a secondary green crosshair will also appear, allowing for the preview of both the target position and smoothing.

![preview blend space](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3965caeb-18d0-4cc8-a701-502e1869754e/previewing1.gif)

Holding **CTRL + ALT** will also enable an influence display, where you can see the different sample weights update relative to the preview point.

![blend space preview influences](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7cbefe2-c481-4ff8-97b7-2e0fa5258651/previewing2.gif)

#### Debugging

If samples are placed in such a way that it will cause very thin triangulation between points, then that triangle will display in red to denote that it should be adjusted. Typically this can happen when performing a [Blend Space Analysis](/documentation/en-us/unreal-engine/automatic-blend-space-creation-in-unreal-engine).

![blend space debugging](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c974825-7d61-436a-bd1c-fb1f2fc2e3e0/error1.png)

If **Use Grid** is enabled, then samples that are awkwardly placed will indicate this error with a red highlight around the sample point. This also indicates that the highlighted sample will not contribute to the Blend Space properly.

![blend space debugging](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14c2da2d-8d35-4293-b5a1-ce5a97b5906c/error2.png)
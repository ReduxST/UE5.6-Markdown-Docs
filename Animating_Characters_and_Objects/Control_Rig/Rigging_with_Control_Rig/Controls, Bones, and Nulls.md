# Controls, Bones, and Nulls

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine)  
**Processed:** 2025-06-14 16:16:00

---

The primary rig elements used when creating robust rigs in Control Rig are **Controls**, **Bones**, and **Nulls**. Each of these elements have wide-ranging applications and can be used together to create complete rigs.

This document provides an overview of Controls, Bones, and Nulls, and provides simple workflow examples for using them.

#### Prerequisites

-   You have created and opened a [Control Rig](/documentation/en-us/unreal-engine/rigging-with-control-rig-in-unreal-engine#createcontrolrigasset) for a skeletal mesh.

## Elements Overview

Controls, Bones, and Nulls are created by right-clicking in the **Rig Hierarchy** panel and selecting one of the options from the **New** menu.

![new bone new control new null](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efaf1664-96bd-4215-b2ba-0ce498a08718/creation1.png)

By default, creating one of these elements will locate it at the origin (0,0,0) of the viewport. If you have an element selected in the Rig Hierarchy panel, it will instead create it at the location of, and parented to, that selected element. This makes it easy to align your elements with each other, using this selection context.

![create control](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d870ffd-b418-4123-a3a3-3ebf91cfbf95/creation2.gif)

### Organization

Elements can be renamed by right-clicking them in the **Rig Hierarchy** and selecting **Rename** or by pressing **F2**.

![rename control](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/618cd69a-4965-4c0c-8fef-0a8475f3420f/rename.png)

Elements can be re-organized by dragging them in the **Rig Hierarchy**.

-   Dragging an element onto another element parents it to that element.
-   Dragging an element to an empty region unparents it.
-   Pressing **Shift+P** also unparents selected elements.

![control drag drop reparent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0197a825-8f7a-49b9-a96c-cf0a81a61997/reparenting.gif)

## Controls

**Controls** are the main elements used for your Control Rig interaction. They are used to drive your Bone chains, animate in **Sequencer**, and provide additional custom attributes. You can also customize your Controls to have different [shapes and colors](/documentation/en-us/unreal-engine/control-shapes-and-control-shape-library-in-unreal-engine), property types, and transform limits.

### Creation Context

When creating Controls relative to a Bone, the Control will automatically inherit the same name as that Bone and apply `_ctrl` as a suffix.

![create control](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91cb3791-c2e4-45df-9a18-2f8ada44e625/controlcreation1.gif)

#### Creating Multiple Controls

In addition to the normal creation method, you can also create Controls when multiple Bones are selected using a provided [Python script](/documentation/en-us/unreal-engine/control-rig-python-scripting-in-unreal-engine#editorstartup). In the [Rig Hierarchy](/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine#righierarchy), select multiple Bones, then right-click on them and select **New > Add Controls For Selected**. This will create Controls for all selected Bones, matching their names with the suffix `_ctrl`, and matching the hierarchy structure.

![add controls for selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da17696a-edeb-4014-bcb3-f988f3ca3281/addcontrolsselected.gif)

You can customize this creation method by holding **Alt** and clicking **New > Add Controls For Selected**. This will open a dialog window where you can customize the following settings:

![add controls for selected options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f96c1b8-0c53-4406-aa32-0c234e2e0db4/addcontrols2.png)

| Name | Description |
| --- | --- |
| **Output Format** | 
How to organize the controls once created. You can select the following options:

-   **Hierarchy**: Copies the same hierarchy as the selected Bones, with the top-most control unparented from the Bone hierarchy.
-   **List**: Unparents all created Controls so they appear at the root of the Rig Hierarchy as a flat list.
-   **Child**: Parents all created Controls underneath the associated Bone.



 |
| **Suffix** | The text to apply after the Control name, which is copied from the Bone name. |
| **Prefix** | The text to apply before the Control name, which is copied from the Bone name. |

### Control and Value Types

There are a variety of Control types that you can specify for Controls which provide alternative or more limited properties for it. This can be useful if you are wanting to create attribute-based Controls, Proxy Controls, or feedback Controls.

You can specify the type of the Control by clicking the **Animation Type** drop-down menu for a selected Control in the Details panel. The following Control types can be chosen:

![control type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/206eb505-05a3-423d-8f7f-6762ce961ccf/controltype1.png)

| Control Type | Description |
| --- | --- |
| **Animation Control** | 
The default Control type, which provides a normal visible animatable Control.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8600bb35-5a75-4192-8da8-af197960f0b8/controltype2.png)

 |
| **Animation Channel** | 

A type of Control that is used to provide an animation channel or custom attribute. If **Group Channels** is enabled, this attribute will be accessible on the parent Control, where it can be animated together with other attributes.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e16f015-10db-481e-a077-4bc5b140ddf9/controltype3.png)

 |
| **Proxy Control** | 

Proxy Controls are a type of Control which can be linked to other Controls in a **Driver / Driven** relationship. This is done by adding the Controls you want to drive in the **Driven Controls** array. Proxy Controls cannot be animated directly, however you can use them to drive other Controls in a consolidated manner using **Get Driven** and **Set Driven** nodes.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/557d6065-dae0-44da-b642-c78bbe577b27/controltype4.png)

 |
| **Visual Cue** |   |

In addition to the Animation Type, you can also adjust the **Value Type**, which sets the output data of a Control. From the **Value Type** dropdown menu, you can set the following types:

| Name | Description |
| --- | --- |
| **Bool** | 
Makes the Control become a **bool-type**, where you can set **True / False** states in animation. Bool-type Controls are not visible in the **Viewport**.

![control type bool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed89b5ad-5137-4099-8d9a-ee73f9d8698f/typebool.png)

 |
| **Float** | 

Makes the Control become a **float-type**, where you can animate the Control along a single position axis. If **Animation Type** is set to **Animation Control**, then you can specify which axis by selecting an axis from the **Primary Axis** property. The range you can move the Control when using this type is [limited by default](/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine#transformlimits) between **0 - 100**. Floats can be useful if you are wanting to create a slider Control.

![control type float](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd1f9af4-7770-4d37-9951-21b8b8327ea4/typefloat.png)

 |
| **Integer** | 

Makes the Control become an **integer-type**, where you can animate the Control along a single position axis, incrementing by one. If **Animation Type** is set to **Animation Control**, then you can specify which axis by selecting an axis from the **Primary Axis** property. The range you can move the Control when using this type is [limited by default](/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine#transformlimits) between **0 - 100**. You can also convert this Control Type to an Enum by referencing an **Enumeration** in the **Control Enum** property.

![control type integer enum](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bf45cc4-4a86-4325-badb-ca4c1ab678f4/typeint.png)

 |
| **Vector 2D** | 

Makes the Control become a **vector 2d-type**, where you can animate the Control along two position axes. If **Animation Type** is set to **Animation Control**, then the axis specified in **Primary Axis** will not be used, with the remaining axes being the ones providing the 2D plane. The range you can move the Control on both axes when using this type are [limited by default](/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine#transformlimits) to between **0 - 100**.

![control type vector 2d](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1afddd42-dce5-4b4c-9260-259209069b69/type2d.png)

 |
| **Position** | 

Makes the Control become a **position-type**, where you can only animate the Control's location.

![control type position](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c869c582-8133-4dee-a1b1-55e5eb03675f/typeposition.png)

 |
| **Scale** | 

Makes the Control become a **scale-type**, where you can only animate the Control's scale.

![control type scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54c2b0fd-7bc3-4918-ac4a-8c94248f897a/typescale.png)

 |
| **Rotator** | 

Makes the Control become a **rotator-type**, where you can only animate the Control's rotation.

![control type rotator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f6911b1-b581-4090-b7b7-b111807a727a/typerotator.png)

 |
| **Euler Transform** | 

Makes the Control become a **transform-type**, where you can freely manipulate the Control on all translation, rotation, and scale axes. This is the default type.

![control type euler transform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2567c02-b316-4f3a-a6bf-62d3e0273e8f/typetransform.png)

 |

For spatial Controls, such as **Euler Transform**, **Rotator**, **Scale**, and **Position**, there are additional transform-related features available to you in the details panel when viewing the **Transform** properties:

![control transform buttons](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53f26e36-4a2b-45a8-8eb7-1c33634fa5e5/spatialbuttons.png)

1.  The **Rotation** drop-down menu is where you can select different rotation interpolation modes, such as **Euler**, **Quaternion**, or **Axis and Angle**.
2.  **Local /World Space** buttons will swap the axis information displayed between local and world space. Shift-clicking will change all three axes.
3.  Locks **Scale**, which will cause scaling to occur uniformly in each direction when changing scale.

### Transform Limits

Spatial Controls can have limits placed on them so that they only can animate within a certain range. This can be useful if you are wanting to create slider or 2D-based controls and limit their movement range.

Limits are set on Controls by defining their minimum and maximum property ranges. You can locate these properties for a selected Control by clicking **Min** or **Max** under the **Transform** category in the **Details** panel.

![control limits min max](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d695bc29-3cfc-471a-9081-0aca0253c291/limits1.png)

Enable any axis channel to enable limits for that value, and define the number within the region next to it. In this example a Minimum limit of -**50** and Maximum limit of **50** is set. Manipulating your Control will now keep its movement restricted to those limits.

![control limits min max](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05e3a509-5b11-4951-884e-c6e981fed04c/limits2.gif)

Enable **Draw Limits** to visualize the limits of all Controls in the Viewport.

![draw limits](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47e42054-2835-4fe5-95de-c17cbc01d9b8/limits3.png)

## Bones

Separate from normal Bones that are included in your skeleton, new Bones can also be created in Control Rig. These Bones can be used in an auxiliary manner to provide extra Bones for specific rigging behavior, such as making ending effectors in an IK-chain, or making "dummy" Bones in order to control "real" Bones in a consolidated manner.

Bones created in the Control Rig editor have their hierarchy icons displayed hollow to differentiate them from normal Skeletal Mesh Bones.

After creating a new Bone, you can move it in the viewport by entering into the **Setup Event** mode, which enables the ability to edit the **Initial Pose** of an element in the viewport. In the toolbar, click the [Solve Direction](/documentation/en-us/unreal-engine/control-rig-forwards-solve-and-backwards-solve-in-unreal-engine) drop-down menu and select **Setup Event**.

![setup event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b547859-a51c-429b-a4d5-c22b8fc768a3/setupevent.png)

Once **Setup Event** is enabled, you can move your Bone in the viewport.

![setup event bone manipulation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf86cde1-83f8-4bb5-bb08-206cf12c9f27/setuptoe.gif)

By default, only selected Bones are displayed in the viewport. You can change this view mode by clicking **Character > Bones** in the viewport toolbar, then select your desired Bone drawing setting.

![bone display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05f7fa33-f6a5-41fe-ad9f-91bbf4d717c8/bonedisplay.png)

### Workflow Example

In this example, a Bone created in Control Rig is being used as an end effector for a finger IK chain.

![bone control example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37f8aef2-3c8e-4b5f-a3d1-3bb7755a319d/fingerik.gif)

## Nulls

**Nulls** are container elements used to collect, group, and transform other rig elements together in arbitrary ways. In a typical humanoid control rig setup, they can be used as a way to group your symmetrical controls, such as legs and arms, in order to mirror these controls. In this way, Nulls are a similar concept to **Groups** from Autodesk Maya, and are meant to be used for rigging organization.

![new null](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d230c96d-00e9-4753-90c8-dd4f5e45b109/null.png)

By default, Nulls are not visible in the viewport. To view nulls, you can enable **Display Nulls** from the Viewport toolbar.

![display nulls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4dd6cbe7-d05e-472a-ad24-c907bc949041/nulldisplay1.png)

Similar to Bones, Nulls can be edited by enabling **Setup Event** from the [Solve Direction](/documentation/en-us/unreal-engine/control-rig-forwards-solve-and-backwards-solve-in-unreal-engine) dropdown menu. Once **Setup Event** is enabled, you can move your Null in the viewport.

![setup event null move](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03cb60ec-2476-408f-9f64-813ec227007f/null2.gif)

Enabling **Setup Event** will also enable visibility on all Nulls in the Viewport.

### Workflow Example

In this example, Nulls are being used to group several controls together along symmetrical and limb lines. This grouping can now facilitate easier organization, mirroring, and other rigging operations.

![null group symmetrical controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b40fd25f-d2da-49a2-962d-a1f52d81122e/null3.gif)

## Transform Types

The position, rotation, and scale of rig elements are determined from multiple transform sources, which are named **Initial**, **Current**, and **Offset**. These transform types each perform transformations on rig elements at different phases of the Control Rig execution. You can view these different types from any selected rig element's details.

![initial current offset transform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c976f9c-f39a-4c0d-81b7-f2ebaadd95bd/valuetypes1.png)

When a different [Control type](/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine#controltypes) is specified for a Control, you can only specify **Initial** and **Current Values**.

![initial current value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/557f7e68-9cbd-43c3-8f9c-d95a16058094/valuetypes2.png)

Holding **Shift** and clicking the different types will display them alongside each other in the Details panel.

![multiple type display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/175b5310-b60f-4c6c-83f4-e323f91c25bc/shifttypes.png)

### Initial

**Initial** is the starting value of the element before control rig logic from the rig graph executes. It also specifies the default value of a rig element within its range of operation, and will affect the default value of **Current**.

You can edit the Initial value by either editing it from the Details panel, or by enabling [Setup Event](/documentation/en-us/unreal-engine/control-rig-forwards-solve-and-backwards-solve-in-unreal-engine#setupevent) and manipulating the element in the Viewport, if it has a Transform.

![initial transform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fafcda8e-6a64-4777-8b39-02c1f049ccb0/initial.png)

### Current

**Current** is the value of the element when operating in the **Forwards Solve** mode. It is meant to be the real-time actual transform of your Control, and manipulating Controls in the viewport will edit the Current pose. Within the Control rig editor, the Current pose is temporary and can be reset by recompiling or reopening the asset.

![current transform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2df27d40-07cc-4993-99ba-2db5a3a80d2d/current.png)

When animating a Control Rig within Sequencer, you are animating the Current value.

### Offset Transform

**Offset** only appears for Controls with **Control Type** set to **Euler Transform**. It is used to spatially offset controls without changing the Initial or Current values, and provides the ability to change a Control's "zero position". In other rigging tools such as Autodesk Maya, Offset is analogous to **Freeze Transformations**, or **Transform Offset Parent Matrix**.

![offset transform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c2f6a22-ef75-44f0-8c33-0a81b8b0e0ce/offset.png)

If you are outputting Transform values from a Control with an offset specified, the resulting transform will combine both **Offset** and **Current** for its final calculated transform. You can change this by setting the **Space** property to **Local Space**, which will then only output **Current**.

![transform pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f65887a6-4385-4046-9144-8eeaf363dcc4/offset2.png)
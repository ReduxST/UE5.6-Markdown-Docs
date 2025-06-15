# Animation Curves

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:03

---

As you play [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) on your **Skeletal Mesh**, you may find it necessary to animate additional properties and values synchronized to that animation. You can accomplish this using **Animation Curves** (also called **anim curves**, or **curves**), which are float-type values you can add and keyframe within an Animation Sequence. Curves can be useful for augmenting your animations with additional animatable properties, such as animating [Material Parameters](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine), [Morph Targets](/documentation/en-us/unreal-engine/fbx-morph-target-pipeline-in-unreal-engine), and other attributes.

This document provides an overview of Animation Curves, and the various ways you can use them.

#### Prerequisites

-   Your project contains a [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) and [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine).
-   If you are using anim curves to affect **Material Parameters**, you need a basic understanding of [Material Instancing](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine).
-   If you are using anim curves to affect **Morph Targets**, you need a basic understanding of setting up [Morph Targets](/documentation/en-us/unreal-engine/fbx-morph-target-pipeline-in-unreal-engine) on your Skeletal Mesh.

## Creating Animation Curves

Animation Curves can be created in the following ways:

1.  When viewing an **Animation Sequence** in the [Animation Sequence Editor](/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine), click the **Curves** track dropdown menu and select **Add Curve… > Create Curve**. Type in the name of the new curve and press **Enter** to create it.
    
    ![create curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/22145f2c-9468-4f2d-af0b-5fa8607f5227/create1.png)
    
2.  In the [Anim Curves panel](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine#animcurvespanel), right-click in the **curve list area** and select **Add Curve**. Type in the name of the new curve and press **Enter** to create it.
    
    ![anim curve panel add curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c3d4a90-4fe0-4448-8a9a-246a4ded0454/create2.png)
    
3.  If your skeleton already has curves, you can select them from the **Curves > Add Curve…** dropdown menu.
    
    ![add existing curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cf09eaa-e65c-4af0-9b32-e39b0da2b148/create3.png)
    

Animation Curves are stored on the **Skeleton Asset**. Therefore, when you are creating curves, you are also editing the [Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine), which will require you to save it.

### Importing Animation Curves

Custom attributes can also be created externally in animation software like Autodesk Maya, and then imported as curves along with your Animation Sequence.

To do this, first [create a custom attribute](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2019/ENU/Maya-Basics/files/GUID-C7385EC4-74E1-4F6E-8C9D-60F5CCDA7994-htm.html) on any bone in your skeleton and keyframe it. You must ensure that it is a float-type attribute, as that is the only compatible data type with curves. Once finished, export your animation.

![create bone attribute](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0970406-86ac-4c49-9d74-8f530a2983dd/attribute1.png)

Your custom attribute must be keyframed in order for curve data to correctly import.

Next, [import your Animation Sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) containing the custom attributes. When importing the FBX, ensure that **Import Custom Attribute** is enabled.

![import animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc343f3b-5bc1-4807-9f8d-a1cfc0007dad/attribute2.png)

Once imported, your curves should appear in your Animation Sequence. In this example, two attributes were created on different bones and then imported.

![attribute to curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62850f65-e2b9-40df-a79d-47e674f29e58/attribute3.png)

## Creating Curve Animation

Once you have created an Animation Curve and added it to your Animation Sequence, you can animate its value. Select the **Curve** dropdown menu on the Animation Curve track and click **Edit Curve**. This will open the [Curve Editor](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine).

![edit curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73e70d84-dd6e-4304-980f-234264a45878/animate1.png)

You can also open the Curve Editor by double-clicking the **timeline region** for the specific curve track.

![double click to edit curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09c8a4f4-c292-4806-b2a8-dcd0b42693ba/animate2.gif)

Once the Curve Editor is open, you can create keyframes by pressing **Enter**. This creates a keyframe at the **Playhead** location, which can be moved by dragging it to set keyframes at different times along the sequence. You can click and drag keyframes to change their time and value.

![edit curve in curve editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c5eb492-e1e8-4ecc-a98c-f0c3e32ee59e/animate3.gif)

Refer to the [Curve Editor](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine) page for more information on navigation, keyframes, and tangent editing using the Curve Editor.

## Anim Curves Panel

Your created and stored curves can be viewed and managed from the **Anim Curves** panel. To view this panel, navigate to the main editor menu and enable **Window > Anim Curves**. The Anim Curve panel can only be viewed from the [Skeleton Editor](/documentation/en-us/unreal-engine/skeleton-editor-in-unreal-engine), [Animation Sequence Editor](/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine), or [Animation Blueprints Editor](/documentation/en-us/unreal-engine/animation-blueprint-editor-in-unreal-engine).

![anim curves panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2a654ed-6b8c-4603-9a4a-4574c4f9b6b0/panel1.png)

### Curve Management

Several settings and features can be adjusted on your curve entries within the Anim Curve panel.

![curve settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f6b9462-f908-4658-9d44-629a172975c5/panel2.png)

| Name | Description |
| --- | --- |
| **Curve Name** | 
The name of the curve. You can rename curves by right-clicking one in the Anim Curve panel and selecting **Rename Curve**.

![rename curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/778837ee-0fa4-4355-91d2-911d1507dc1b/panel3.png)

 |
| **Type** | Enables this curve to either be used for [Morph Targets](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine#morphtargets) or [Materials](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine#materials). |
| **Weight** | The current value of the curve. |
| **Auto** | 

Enabling this causes the **Weight** value to change automatically according to its keyframed values if the curve is being animated in this sequence. If disabled, it ignores its animated values. Disabling this can be useful for testing how the curve value affects the character without keyframing it.

![auto setting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6875d132-626c-4047-bdef-81fa05c2c153/panel4.gif)

 |
| **Bones** | The number of bones [connected](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine#curvedetails) to this curve. |

### Curve Filtering

You can filter the list of curves in the Anim Curves panel to display only the actively-used curves, or only certain types of curves.

-   Disabling **All Curves** causes only the currently-used curves for this Animation Sequence to be displayed.
-   Disabling **Morph Target**, **Attribute**, and **Material** curves disables those curve types from being displayed.

![curve filtering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eeca51ff-819c-451a-855d-df7cac0a3c19/panel5.gif)

### Curve Details

Selecting a curve reveals the following properties in the **Details** panel.

![curve details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c1a2f05-9579-44c5-880b-19cc6142df81/panel6.png)

| Name | Description |
| --- | --- |
| **Curve Name** | The name of the curve. |
| **Connected Bones** | An array of bones that you can connect to this curve. This is useful if you want certain curves to be active depending on if a bone is being used or not. Bones can be active or inactive depending on if [different skeletons are merged](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine#mergingduringimport), or bones are being [reduced](/documentation/en-us/unreal-engine/skeletal-mesh-lods-in-unreal-engine#reducingbones) for different LODs. |
| **Max LOD** | The maximum [LOD](/documentation/en-us/unreal-engine/skeletal-mesh-lods-in-unreal-engine) to use before this curve no longer evaluates. For example, setting this value to **1** will cause this curve to evaluate for LODs 0 and 1, but not for 2 and beyond. |

## Using Animation Curves

Once you have created and animated your curve, there are a variety of ways you can use it to affect your character.

### Materials

You can use Animation Curves to automatically affect [Scalar Material Parameters](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine#scalarparameters). This requires you to do the following:

1.  Match the curve name to the name of the Material Parameter in the Material.
    
    ![curve name matching material parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4e87dfa-9739-42b7-b3df-f4ff908b760f/material1.png)
    
2.  Enable the Material curve type in the **Anim Curves** panel.
    
    ![enable material type on anim curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5665dbd-ff59-4862-864a-46c1a94bf57e/material2.png)
    

Once this is done, the curve value starts to affect the Material Parameter.

![curve affecting material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9cb8f71-680e-4371-adb8-6706530c1d31/material3.gif)

Material Animation Curves affect all Materials (and their parameters) assigned to a Skeletal Mesh. Therefore, you may need to adjust your content appropriately if you want your anim curve to only affect a parameter from a single Material. This can happen if your Skeletal Mesh has multiple assigned Materials deriving from a single parent, which will cause parameter names to share between all assigned Materials.

![multiple materials](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aca1a9d8-7466-45d7-b16a-10536c56e33e/multiplemats.png)

### Morph Targets

Similarly to Materials, you can use Animation Curves to automatically affect [Morph Targets](/documentation/en-us/unreal-engine/fbx-morph-target-pipeline-in-unreal-engine) on your Skeletal Mesh. This requires you to do the following:

1.  Match the curve name to the name of the Morph Target found in the [Morph Target Previewer](/documentation/en-us/unreal-engine/morph-target-previewer)
    
    ![match anim curve name to morph target](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90d296c7-0e26-487e-9d2e-c3cee0465deb/morph1.png)
    
2.  Enable the Morph Target curve type in the **Anim Curves** panel.
    
    ![enable morph target type on anim curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b8d02c8-b4cb-430c-8755-552de688a00d/morph2.png)
    

Once this is done, the curve value starts to affect the Morph Target.

![curve affecting morph target](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6868a6dd-c388-4b4c-af08-53a332a6fd30/morph3.gif)

### Animation Blueprints

You can use Animation Curves to affect arbitrary values in [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine). In most cases, you can use them to affect the alpha values of certain Anim Graph nodes, such as IK, in order to change IK states during animation playback.

![curve values in animation blueprints](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8d34808-210c-4530-8b9a-543d82592b89/animbp1.png)

The following curve-related functions are available in both the Animation Blueprint Anim Graph, and Event Graph:

| Name | Image | Description |
| --- | --- | --- |
| **Get Active Curve Names** | ![get active curve names](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24d04b3a-5f04-443c-b66a-4bb7b0efdd2a/animbp2.png) | This targets an Anim Instance and returns the last up-to-date list of active curve names for the specified curve type. |
| **Get All Curve Names** | ![get all curve names](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23f14e17-d1ab-4aa7-8232-fcabfe7eb006/animbp3.png) | This targets an Anim Instance and returns all Curve Names into a string array. |
| **Get Curve Value** | ![get curve value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39052cb6-1473-4dc8-be89-d5b0cd5bcaa5/animbp4.png) | This targets an Anim Instance and returns the value of a specified Curve Name. |

## Metadata Curves

Metadata Curves are Animation Curves that output a static curve value of **1.0** when added to an Animation Sequence. They can work conversely with normal Animation Curves, which by default (with no keyframes) output a static curve value of **0.0**. If no curve is added to a sequence, the anim curve value also falls back to a value of **0.0**.

This behavior can be useful in larger projects that contain many Animation Sequences. In these projects, many of those animations may require constant **1.0** curve values throughout them. Therefore, you can use **Metadata Curves** to expedite this process, rather than manually adding normal curves and keyframing them to **1.0**. In other words, large projects that are using anim curves can structure their usage in Animation Sequences in the following way:

-   A small number of Animation Sequences may require explicit curve animation on them. Therefore, add **Animation Curves** to those animations and **keyframe** them accordingly.
-   A larger number of Animation Sequences may require curve values set constantly to **1.0**, in order to maintain a property value. Therefore, add **Metadata Curves** to those animations.
-   The remainder of all Animation Sequences may not require curve value considerations, or require curve values set constantly to **0.0**. No action is required.

To create a Metadata Curve, click the **Curves** track dropdown menu and select **Add Curve… > Create Curve**. You can either select a currently-existing curve, or click **Create New** to create a new curve.

![create metadata curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/22ab29a0-07f8-4494-b061-76baad88b16a/meta1.png)

Alternatively, a currently-existing anim curve can be converted to a Metadata Curve by clicking the **Curve** drop down menu on a curve track and selecting **Convert To Metadata**.

![convert to metadata curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d2aab6b-09bd-46a5-9ce8-08bf09e4ca99/meta2.png)

Once created, Metadata Curves are read-only and output a constant curve value of **1.0**.

![metadata curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4516ff7-4bf7-42d4-8edf-909edc21ccfc/meta3.png)
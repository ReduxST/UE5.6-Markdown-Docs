# Control Rig Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-control-rigs-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-control-rigs-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:01

---

This page provides an overview of Control Rig, and shows how to create and animate rigs in Unreal Engine.

## What is a Control Rig?

Control Rig is Unreal Engine's solution to animating characters directly in the engine.

The **Control Rig Editor** is where you can create custom controls, channels, and other manipulators for your characters. After a rig is created, you can animate these controls within other areas of Unreal Engine, such as **[Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine)**.

![control rig editor overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd8affa6-e197-4884-8e2b-ad5af4327ccd/controlrigoverview.png)

Control Rigs require the creation of **Control Rig Assets**, which are created and stored in the **Content Browser**.

![control rig asset content browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7239a1a-c246-4b2a-91e7-0a3b621b6bdb/contentbrowser.png)

## How do I Create and Open a Control Rig?

The main way to create a new Control Rig asset is to right-click on a **[Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine)** in the Content Browser and select **Create > Control Rig**. This creates a Control Rig asset in the same directory with the postfix "\_CtrlRig".

![create control rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41f45274-89e8-42e5-addf-31e0f3c4795e/createcontrolrig.png)

Next, double-click on the Control Rig asset to open the **Control Rig Editor**.

![open control rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ef957ea-f287-4c61-933f-1c1f9011def7/opencr.png)

## How do I Rig and Animate with Control Rig?

One of the simplest control types you can create is an **FK Control**. This guide gives an overview of how to create this control and animate it in **Sequencer**.

### Create Control

In the Control Rig Editor, select the **Rig Hierarchy** tab to view the skeleton hierarchy for your character. Navigate to the bone you want to animate, right-click it, and select **New > New Control**.

![create new control](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ef31a89-ec3d-4bb5-b24a-e07f4697ea1e/newcontrol.png)

This creates a control at the same location and orientation of the bone. The control is also named the same as the bone with the postfix "\_ctrl".

![create new control](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f1e885c-50ac-42a5-9745-de248e1b3ca6/newcontrol2.png)

Although you can keep the control nested within the skeleton hierarchy, it is best practice to remove it from the hierarchy and build your own control rig hierarchy adjacent to the skeleton. Select the control and press **Shift+P** to unparent the control from the skeleton.

![unparent control](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e85c7c00-bb1e-4826-af21-384de0167d36/shiftp.gif)

### Edit Control Shape

In order to better see and select the control in the viewport, you can change the **Control Shape**. To do this, navigate to the **Details** panel and locate the **Control Shape** property category. Here you can set a new shape using the **Shape** property, as well as customize the scale and offset of it using the **Transform** properties.

For this example, the shape is set to **Circle\_Thick**, Rotation Y is set to **90**, and all Scale axes are set to **3.0**.

![change control shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6a77cb7-e942-4d10-8db6-ff434e5aeb95/controlshape.png)

### Drive Bone with Control

Next, reference your control and bone in the **Rig Graph**. Do this by dragging the control from the **Rig Hierarchy** panel into the graph, then select **Get Control**.

![get control graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e87de7d3-b5e1-4180-8c43-54ba1c211d3d/getcontrol.gif)

Do the same for the bone you want this control to affect. Drag the bone from the **Rig Hierarchy** panel into the graph, then select **Set Bone**.

![set bone graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97279d8e-67e1-463e-b086-956e6c941a68/setbone.gif)

Connect the **Transform** output data pin from the **Get Transform - Control** node to the **Transform** input data pin of the **Set Transform - Bone** node, then connect the **Execute** output pin from the **Forwards Solve** node to the input execution pin of the **Set Transform - Bone** node.

![set bone transform control](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da3f1053-8d2d-4847-af79-4cfb9346df27/connectpins.png)

You can now manipulate the control in the viewport and see the control driving the bone.

![test control](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a347caf-d2f7-4389-a5c5-896cd41837c6/viewporttest.gif)

Clicking **Compile** resets the control position back to default.

### Animate Control in Sequencer

Now that your control is appropriately manipulating a character's bone, you can start to animate it in **[Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine)**.

Drag the **Control Rig Asset** from the **Content Browser** into the Level viewport. Once this is done, Sequencer opens with the character added to it as a **[Track](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine)**.

![add control rig to level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b196828a-b670-462d-9a4d-a8bd8d7c73a4/animate1.gif)

Expand the **Control Rig** track to locate the controls you created. You can either select them here, or in the viewport.

![control rig in sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ff02073-b164-4c83-b526-1ffe99f95481/animate2.png)

With the control selected in the Viewport, press the **S** key to create a transform **Keyframe** for the selected control at the [**Playhead**](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#playhead). Afterward, drag the **Playhead** to a different location in the sequence, manipulate your control, then press **S** again to set a second **Keyframe**.

![keyframe control rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4a21069-7ba2-4f3c-818c-949415cf20ff/animate3.gif)

Now when playing or scrubbing the sequence, you should see your control and character animate between the two keyframes.

![keyframe control rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5213f189-0737-4dc4-978d-17efd79273ca/animate4.gif)
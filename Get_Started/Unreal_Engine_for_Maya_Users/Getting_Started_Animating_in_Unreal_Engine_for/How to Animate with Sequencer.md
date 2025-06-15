# How to Animate with Sequencer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-animate-with-sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-animate-with-sequencer)  
**Processed:** 2025-06-14 16:28:40

---

Now that you've got Unreal Engine installed and a new project setup, you'll learn walk through the process of creating a new level, a Level Sequence where you'll animate actors in your scene, and how using a control rigged object can make animating inside of Unreal Editor that much simpler. 

## Recommended Reading

If you're new to Unreal Engine, or using a real-time engine, we recommend starting with our guided tour of the [Unreal Editor and Features Overview for Maya Users](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-and-features-overview-for-maya-users). This guide can help provide needed context and workflows for some of the features and tools you'll use in this guide to animating in Unreal Engine. 

## Create a New Level

1.  In the editor, go to the main menu and choose **File > New Level**.
    
2.  In the New Level dialog, select **Open World**.
    
    [![Select type of level you want to create.](https://dev.epicgames.com/community/api/documentation/image/7852c29b-1662-4d07-9bd9-13adb21a102c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7852c29b-1662-4d07-9bd9-13adb21a102c?resizing_type=fit)
    
    Select type of level you want to create.
    
3.  Click **Create**.
    

The new Open World level will be created and automatically open. You should see this when it loads and is done compiling and preparing shaders.

[![A newly created Open World Level.](https://dev.epicgames.com/community/api/documentation/image/b0247535-4949-4c3c-8a44-f1a36bb140f1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b0247535-4949-4c3c-8a44-f1a36bb140f1?resizing_type=fit)

A newly created Open World Level.

## Preparing the Scene

1.  In the main toolbar, click the **Cinematics** icon and select **Add Level Sequence** from the dropdown menu.
    
    [![Add a level sequence to the world.](https://dev.epicgames.com/community/api/documentation/image/b52882cf-8791-4d70-ba51-797f86824ef4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b52882cf-8791-4d70-ba51-797f86824ef4?resizing_type=fit)
    
    Add a level sequence to the world.
    
2.  In the **Save Asset As** window, give the Level Sequence asset a name (1), and click **Save** (2). For the purposes of this guide, the level sequence is named “MyLevelSequence”.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/35b0dc35-4473-4e58-8f3b-69ad4eac9fce?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/35b0dc35-4473-4e58-8f3b-69ad4eac9fce?resizing_type=fit)
    
    The level sequence will automatically open and add the Sequencer panel at the bottom of the level editor viewport.
    
    [![Sequencer panel with an open Level Sequence.](https://dev.epicgames.com/community/api/documentation/image/0b093214-a52e-418d-8f5d-869e6a783e8b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0b093214-a52e-418d-8f5d-869e6a783e8b?resizing_type=fit)
    
    Sequencer panel with an open Level Sequence.
    
3.  In the **Content Browser**, navigate to the **ControlRig > Props > CardBox** folder, and drag the asset named **CR\_Cardbox** into the scene.
    

Once the Control Rig for Cardboard Box prop is dragged into the scene, a couple of things happen: the [Level Editor Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/level-editor-modes-in-unreal-engine) automatically switches to **Animation** mode to better work with and animate the Control Rig, and the cardboard box control rig is automatically added to the level sequence you created earlier.

Before the next section, you can choose to move the cardboard box prop over to be out of the way of any other actors in the scene. Pressing the F keyboard shortcut will quickly focus the camera view on the actor you have selected.

## Using Sequencer to Animate with Control Rig

Before you start animating in Unreal Editor, let's take a moment and review some of the tools and editor modes you'll be using to animate in Unreal Engine. 

### Level Editor Animation Mode

The Level Editor includes a **Modes** selection menu where you can put the editor into these modes for different types of workflows. With each workflow, you may get additional panels with tools and viewport toolbar options to work with. **Animation** mode includes tools and settings that help you animate directly in the level viewport.

[![The Level Editor's Animation Mode with Sequencer open.](https://dev.epicgames.com/community/api/documentation/image/48742045-51b2-4c66-a7e3-a16eb2087a82?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/48742045-51b2-4c66-a7e3-a16eb2087a82?resizing_type=fit)

The Level Editor's Animation Mode with Sequencer open.

In Animation mode, you’ll notice that the layout has changed and opened several additional panels, these are:

-   **Animation Panel:** A list of animation tools you can use to animate objects in the level.
    
-   **Anim Outliner:** A list of controls found in any control rig placed in the level.
    
-   **Anim Details:** A list of properties and transform settings with information relevant to the controls in a selected Control Rig. Its function is similar to the Details panel but for Control Rigs.
    

### Control Rig Control Points

Control Rigs enable you to animate characters and objects in Unreal Editor directly. You can create and rig custom controls on a character, animate it in Sequencer, and use a variety of other animation tools to aid your animating process.

For more information on setting up and using control rigs, see [Control Rig](https://dev.epicgames.com/documentation/en-us/unreal-engine/BlueprintAPI/EditorScripting/SequencerTools/ControlRig).

For the purposes of this guide, let’s take a look at the control points set up on the prop named **CR\_Cardbox**.

[![The CR_Cordbox proper from the Control Rig Sample Pack.](https://dev.epicgames.com/community/api/documentation/image/4d990fe1-b804-407f-bd14-7a28d10e2906?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4d990fe1-b804-407f-bd14-7a28d10e2906?resizing_type=fit)

The CR\_Cordbox proper from the Control Rig Sample Pack.

The Control Rigs setup in the [Control Rigs Sample Pack](https://www.fab.com/listings/2ce3fe44-9ee6-4fa7-99fc-b9424a402386) you’ve downloaded for this guide include the following elements you’ll use to animate the cardboard box prop:

-   The **Global** controller is the yellow square at the base of the box that aligns with the ground plane. You’ll use this to move the entire control rig within the scene for placement.
    
-   The **Body** (or Center of Mass) controller is the yellow ring around the center of the box prop. This is used to move the prop’s rig without moving the global controller. You can move the rig freely.
    
-   The **Squash and Stretch** controllers are the red squares located at the base, middle, and top sections of the prop. Moving or scaling any of these will deform the mesh in those areas.
    

**Control Points** are red spheres and small squares along the lid flaps of the mesh used to move and animate these elements of the rig.

The **Proxy** controller is a green diamond shape. These are similar to proxy meshes you’d set up in Maya to control a set of points.

## Setting the Control Rig Pose

Before we start to animate the box, we’ll want to first close the flaps on the box. We’ll use the **Control Points** on the inner edges of the box to select these and rotate the flaps inward. You can select control points individually or multiple ones and rotate them inward at the same time. 

To do this:

1.  Select the control points along the inner edge of two sides opposite one another.
    
2.  So that these rotate simultaneously in the same inward direction, you’ll want to switch from World Space to **Local Space** when rotating the flaps. You can do this by clicking the mouse on the Space toggle in the viewport toolbar, or you can use the keyboard shortcut **Ctrl + \`** to swap between the two coordinate spaces.
    
    [![Toggle between local and world space for the transform tools.](https://dev.epicgames.com/community/api/documentation/image/5fbe362e-a617-40ff-aec7-af2e9e0fa07c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5fbe362e-a617-40ff-aec7-af2e9e0fa07c?resizing_type=fit)
    
    Toggle between local and world space for the transform tools.
    
3.  Set the transform tool to the **Rotate** gizmo. You can use the viewport toolbar to select the rotate tool, you can use the **Spacebar** to toggle between the move, rotate, and scale tools, or you can press **E** to switch to the rotate tool.
    
    ![Toggle between the transform gizmos using the Spacebar.](https://dev.epicgames.com/community/api/documentation/image/b72cb39a-46cb-45c2-b10d-13346eac339a?resizing_type=fit)
    
    Toggle between the transform gizmos using the Spacebar.
    
4.  Select an axis in the direction you want to rotate and **Left Mouse Click** and **Drag** to rotate the flaps until the box is closed.
    
    ![Select multiple control points and rotate them simultaneously.](https://dev.epicgames.com/community/api/documentation/image/595a29cd-403d-416e-a788-c0c81c060353?resizing_type=fit)
    
    Select multiple control points and rotate them simultaneously.
    
5.  Select the remaining two control points and repeat the previous step to close these flaps.
    

This is the result of the steps above: 

## Animating and Setting Keyframes in Sequencer

In this animation example, we’ll look at how we can take this Cardboard Box prop to have it rock back and forth a bit, squash, stretch, and jump to land in another spot. Before we look at how we’d do it for this guide, let’s look at a few different ways you can go about animating in Unreal Editor in general. 

First, you could just animate it. This requires rotating and translating the object, setting key frames, and repeating this process over and over again until you’re done. For something like the cardboard box prop, you’d have to move and rotate the object, faking the feel of the pivot along the edge of the box. This can be a lot of manual work every time. 

The second option is to use the **Temporary Pivot Tool** found in the Viewport Toolbar. This provides an on-screen toggle between **Edit** and **Pose** to move and place the pivot point temporarily where you make adjustments. In the case of animating the cardboard box prop, this option is less involved than the first option, but it’s still a very manual process to move the pivot, rotate the box, set the key frame, and repeat the process.  

The third option — the one this guide will use in later steps — uses **Proxy Controls** that are built into the Control Rig to handle this for us. These controls are not things that you keyframe, instead, they are things that drive values in other controls. This cardboard box prop’s control rig has pivots laid out along each edge specifically for edges, and corners. This proxy controller looks for these and dynamically changes pivots for you without all the manual work of doing it yourself.

If you don’t see the green proxy controller, you can use the **Anim Outliner** panel to select it from the list of controls.

With these different ways of animating your objects using a Control Rig with Sequencer, we’re going to look at this third option that uses these controllers and proxy controls to do a short animation with a handful of keyframes. We’ll use the proxy and controllers setup in the Control Rig to perform some actions like rocking the box back and forth, then having it jump to a new location, and finally using the squash and stretch controllers for more refined action in between. 

We’ll break these steps down in the following ways to build off each other: 

-   Set some general keyframes that incorporate rotating the box along its edges back and forth and jumping from one point to another.
    
-   Use the Squash and Stretch controllers to add a little bit of personality to the animation.
    
-   Use some tools in Sequencer and Animation editor mode that can improve the smoothness and look of the animation.
    

The goal of this guide is not to replicate this exactly as shown. Instead, using this simplistic animation, we want to show key features of animation tools and Sequencer in Unreal Engine that will make your animation process simpler. 

For the best results in following this guide, see the Optional and Recommend Settings section of this page to better match your editor with what is being demonstrated in the sections below.

### Setting the Initial Key Frames for the Animation

We’ll start by setting some initial keyframes that capture the basics of the jump. These do not need to match exactly what is shown in this guide, but you should have something similar by following the steps below. 

1.  In the **Sequencer** panel, click **Add Keyframe** to create the initial keyframe used for the animation.
    
    [![Manually add a keyframe.](https://dev.epicgames.com/community/api/documentation/image/44bf495a-5825-4e6d-9d64-92eccef2b993?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/44bf495a-5825-4e6d-9d64-92eccef2b993?resizing_type=fit)
    
    Manually add a keyframe.
    
2.  Move the **Playhead** forward on the timeline to create a new key. Where you’ll create the first of three keys: one for the rock back, one for the fall back to sitting flat, and one for the rock forward before the jump:
    
3.  In the **Anim Outliner**, select the **Proxy** control in the hierarchy.
    
    [![Select the Proxy controller in the Anim Outliner panel.](https://dev.epicgames.com/community/api/documentation/image/f55dc500-a814-42d9-a2d6-bbda3eff6b52?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f55dc500-a814-42d9-a2d6-bbda3eff6b52?resizing_type=fit)
    
    Select the Proxy controller in the Anim Outliner panel.
    
4.  Use the **Rotate** tool to rock the box to the left.
    
5.  Move the **Playhead** forward on the timeline a few frames.
    
6.  Use the **Rotate** tool to move the box back to its original sitting flat position and add a key. This ensures that since the pivot of the proxy control is switching, the box isn’t blending through the ground.
    
7.  Move the **Playhead** forward again on the timeline a few frames.
    
8.  Use the Rotate tool to rock the box to the right.  
    

At this time, your keys and animation in Sequencer should look similar to this:

Next, we’ll add the Jump to the animation to move the box from one location to another. 

1.  From the last position where the box was tilting right, move the **Playhead** forward on the timeline some.
    
2.  Press the **Spacebar** to toggle through the transform tools or press **W** to select the **Move** gizmo.
    
3.  Select the **Global** controller (yellow box) in the scene or use the **Anim Outliner** panel to select it. You’ll use this to move the control rig with the box prop in the scene.
    
    [![Select the Global controller in the Anim Outliner panel to move the control rigged prop.](https://dev.epicgames.com/community/api/documentation/image/fd5211e5-03e9-42e0-a6d0-7875bdc0503d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fd5211e5-03e9-42e0-a6d0-7875bdc0503d?resizing_type=fit)
    
    Select the Global controller in the Anim Outliner panel to move the control rigged prop.
    
4.  With the Global controller selected, grab the **Move** gizmo and move the box to somewhere above the ground and to the right of where it was located. This should create a key with the box in the air above the ground.
    
5.  Move the **Playhead** forward on the timeline some.
    
6.  With the Global controller still selected, grab the **Move** gizmo and move the box to the ground and a little more to the right of where it was in the air.
    
7.  Switch to the **Rotate** tool using the **Spacebar** or press **E** on the keyboard.
    
8.  Select the **Proxy** control in the **Anim Outliner**.
    
9.  Rotate the box to the left to have it sit flat on the ground again.
    

At this time, your keys and animation in Sequencer should look similar to this for the addition of the jump:

With everything combined, for the initial rocking of the box back and forth and the jump from one point to another, you should see something like this: 

### Animating Squash and Stretch

The Control Rig has built in controls for this prop that make it easier to squash and stretch the mesh when animating it in sequencer.

For this section of the guide, we’ll apply some deformation using the controllers on the control rig and register those changes on the keys you’ve already set in the previous step. Follow the steps below to see how to do this with the first few keys in Sequencer and you can do the rest on your own to create something uniquely yours.

1.  In Sequencer, select the second key for the initial rock back pose.
    
    [![Select a keyframe you want to add animation to.](https://dev.epicgames.com/community/api/documentation/image/00788d22-b846-4bee-86e2-29c7145dd4de?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/00788d22-b846-4bee-86e2-29c7145dd4de?resizing_type=fit)
    
    Select a keyframe you want to add animation to.
    
2.  With this pose selected, we’ll select the top red square at the top of the box. Using the Move gizmo, drag the Z axis (blue) direction up, stretching the mesh.
    
3.  Click the **Key** button next to the **CR\_Cardbox** to add keys for this action to the Sequencer timeline.
    
    [![Use the Add a Keyframe button to capture all movements on the timeline.](https://dev.epicgames.com/community/api/documentation/image/b86aca7e-7e05-4819-b130-0f9729a62b3e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b86aca7e-7e05-4819-b130-0f9729a62b3e?resizing_type=fit)
    
    Use the Add a Keyframe button to capture all movements on the timeline.
    
4.  You can **repeat these steps and actions for each of the remaining keys** to make it uniquely your own using these stretch and squish controls on the control rig.
    

If you do this for the remaining keys — adding keyed changes to the control points — you can get something as simple as this or take it as far as you want to create more nuance to the animation of the cardboard box.

![The result of applying some squash and stretch to the prop.](https://dev.epicgames.com/community/api/documentation/image/9e2b224c-6e5e-4118-a83a-9ce0c2e6d756?resizing_type=fit)

The result of applying some squash and stretch to the prop.

### Making Fine Adjustments to Keyframes

Two built-in tools you can use to refine edits to your animation keys in Sequencer are the **Curve Editor** and the **Tween Tools**. 

The **Curve Editor** is a standalone window that provides control over the way your objects are animated. It can be used to modify and fine-tune your keyframes with specificity that you cannot in the Sequencer panel.

You can access the Curve Editor from the Sequencer panel by clicking on its icon in the toolbar.

[![Click the Curve Editor icon to open it in a separate dockable window.](https://dev.epicgames.com/community/api/documentation/image/e8136c71-164e-4d43-a255-9d52b0309717?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e8136c71-164e-4d43-a255-9d52b0309717?resizing_type=fit)

Click the Curve Editor icon to open it in a separate dockable window.

In the Curve Editor, you can create new keyframes, edit tangents, and use its built-in tools to adjust animation curves. The Tween Tools are also built into the main toolbar of the Curve Editor. This editor is not exclusive to Sequencer and is also used with other tools like the Niagara VFX editor.

[![The Curve Editor.](https://dev.epicgames.com/community/api/documentation/image/ec90796e-4b24-4d91-8dcb-d71390682719?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ec90796e-4b24-4d91-8dcb-d71390682719?resizing_type=fit)

The Curve Editor.

Use the selection panel on the left-hand side to select specific controls to edit only those keyframes for finer control.  
  

[![Use Ctrl + LMB to select multiple tracks at once.](https://dev.epicgames.com/community/api/documentation/image/2c258905-9d0a-42a8-a6c9-48d3b7c1d3f7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2c258905-9d0a-42a8-a6c9-48d3b7c1d3f7?resizing_type=fit)

Use Ctrl + LMB to select multiple tracks at once.

For more information on using this editor and familiarizing yourself with its tool, see [Curve Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine) documentation.

The **Tween Tools** are an integral part of any animator’s toolbox as it can be used to adjust the interpolation between selected keyframes and their neighboring keyframes in a variety of ways. 

You can access the Tween Tools in one of two ways: 

-   Through its integration the level editor’s Animation mode and use with the Sequencer panel.
    
    [![Click the Tweens button in the Animation panel to open the Tweens  Tools while in Animation Mode.](https://dev.epicgames.com/community/api/documentation/image/c7788057-a89d-4e50-bb8e-b3d63d2456f1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c7788057-a89d-4e50-bb8e-b3d63d2456f1?resizing_type=fit)
    
    Click the Tweens button in the Animation panel to open the Tweens Tools while in Animation Mode.
    
-   Built into the Curve Editor’s main toolbar.
    
    [![The Tweens Tool is built into the main toolbar of the Curve Editor.](https://dev.epicgames.com/community/api/documentation/image/81da9418-cdc4-401f-aad0-daa8d7d14c84?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/81da9418-cdc4-401f-aad0-daa8d7d14c84?resizing_type=fit)
    
    The Tweens Tool is built into the main toolbar of the Curve Editor.
    

The Tween Tool includes the following modes for adjusting the in-between keyframes using the dropdown selection:

[![Tween Tools Modes](https://dev.epicgames.com/community/api/documentation/image/557c0d70-dd22-46f5-a5b8-7d3c7dff4861?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/557c0d70-dd22-46f5-a5b8-7d3c7dff4861?resizing_type=fit)

Tween Tools Modes

| Tween Method | Description |
| --- | --- |
| 
**Blend Neighbor**

 | 

Blend to the next or previous values for the selected keys. 

 |
| 

**Push / Pull**

 | 

Push or pull the values to the interpolation between the previous and next keys.

 |
| 

**Blend Ease**

 | 

Blend with an ease falloff to the next or previous value for the selected keys.

 |
| 

**Move Relative**

 | 

Move relative to the next or previous value for the selected keys. 

 |
| 

**Time Offset**

 | 

Shifts the curve to the left or right by changing the key’s Y values and maintaining frame position.

 |
| 

**Smooth / Rough**

 | 

Push adjacent blended keys further together or apart. Smooth is useful for softening noise, like in mocap animations.

 |
| 

**Tween**

 | 

Interpolates between the previous and next keys. 

 |

Additionally, you can select several keyframes at once to adjust.

![Selecting multiple keyframes and using the Tweens Tool.](https://dev.epicgames.com/community/api/documentation/image/4c95c83d-b417-4cba-a469-a76fd173f0aa?resizing_type=fit)

Selecting multiple keyframes and using the Tweens Tool.

For more information about these tools, see the “Tween Tools” section of the [Animation Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-editor-mode-in-unreal-engine) documentation.

Now that you have a general overview of these tools you can use, you can give them a try with your own animation to make edits yourself. 

In the example below, the Curve Editor was used to change a bit of the rotation at the height of the jump and landing with added key frames. The tween tools were used to blend these slightly. Give this a try with your animation to explore using the Curve Editor with your animation and try out the different tween tool modes to make something unique to your animation.

## Next Step

Now that you have a simple animation to work from, the next step is to add some lighting and other environment elements to the scene to make it look interesting. You’ll add some lights, props, and fog elements to the scene and learn how you can make edit them to create interesting and different looks for your scene in real-time.

[

![How to Add Lighting and Actors to a Scene](https://dev.epicgames.com/community/api/documentation/image/76dd6b45-1611-42af-a915-c4704354d61c?resizing_type=fit&width=640&height=640)

How to Add Lighting and Actors to a Scene

How to add lights and other actors to a scene while working in real-time.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-add-lighting-and-effects-to-a-scene)
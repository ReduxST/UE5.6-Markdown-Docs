# Skeletal Mesh Sockets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-sockets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-sockets-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:47

---

When attaching objects to Bones on your Skeletal Mesh, it may be necessary to offset this attachment. Instead of using math operations to estimate the offset transform, you can create **Sockets**. Sockets are dedicated attach points within the hierarchy of your Skeleton, which can be transformed relative to the Bone it is parented to. Once set up, you can attach your objects, weapons, and other actors to the Socket.

This document provides an overview of how to create and use Sockets.

#### Prerequisites

-   Your project has a [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine).

## Creating Sockets

Sockets are created from the **Skeleton Tree**, which can be accessed from any of the main [Animation Editors](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine). Right-click on a Bone in the **Skeleton Tree** and select **Add Socket.**

![add socket](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a39642c-cbfb-4202-91c3-e498446c6257/create1.png)

Your new Socket will now be displayed in the Skeleton Tree, parented to the Bone that you selected previously.

![new socket](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7602e3a1-6541-483f-9e15-cb3268647f7e/create2.png)

Sockets can be deleted by right-clicking on them and selecting **Delete** or by pressing **Delete** on your keyboard.

![delete socket](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9bcfbcd-0fec-47b9-a064-6c3ea85b8731/create3.png)

By default, when creating and manipulating Sockets, this will edit the [Skeleton Asset](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) of your Skeletal Mesh. Therefore, you must save it when making Socket changes.

## Managing and Editing Sockets

Once you have created a Socket, you can interact with them in the following ways.

### Socket Visibility

By default, Sockets are not visible in the [Animation Editor Viewport](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine#viewport), you can make them visible by navigating in the Viewport menu to **Character > Bones**, and enabling **Sockets**.

![show sockets in viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a617ad6f-a69a-462b-a99c-fd276546ae16/visibility.png)

### Selection and Movement

Sockets can be selected by either clicking them in the Skeleton Tree, or if made visible in the viewport, by clicking them in the Viewport. You can then move them by dragging on the transform manipulator in the Viewport. Sockets can be translated, rotated, and scaled.

![select and move socket](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/749b505d-c36a-4601-8b44-1a8f860b6753/selectionmove.gif)

### Copy and Paste

Sockets can be copied and pasted in different ways depending on your requirements.

To copy a Socket, right-click on it in the Skeleton Tree and select **Copy Selected Sockets**, or press **Ctrl+C**.

![copy selected sockets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bd39ae4-7729-4b3b-bacf-d9a62fd1b64b/copypaste1.png)

Next, you can choose to either:

1.  Paste the Socket to the same bone, which is done by right-clicking on any Bone in the Skeleton Tree and selecting **Paste Sockets**. This will essentially duplicate the Socket.
    
    ![paste sockets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb1f219e-a2fd-4366-8a74-eefb2869ed8a/copypaste2.png)
    
2.  Paste the Socket to a different Bone, which is done by right-clicking a different Bone in the Skeleton Tree and selecting **Paste Sockets To Selected Bone**. This will paste a copy of that Socket with the same offset information, but parented to the new Bone.
    
    ![paste sockets to selected bone](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c4c2317-3362-4ad3-8040-1589d4170fb9/copypaste3.png)
    

### Mesh Sockets

When [sharing Skeletons](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine#sharingskeletons) between different Skeletal Meshes, it may be necessary to create Sockets that are exclusive for one of the Skeletal Meshes. This can be done by using **Mesh Sockets**, which will make a Socket exist on the **Skeletal Mesh**, instead of the **Skeleton**.

![mesh socket compare](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d14dca9-9701-4dbf-900e-ba132caf68d7/meshsocket1.png)

To make a Mesh Socket, right-click an existing Socket and select **Create Mesh Socket**. This will convert the Socket into a Mesh Socket. Ensure that you are currently using the [Skeletal Mesh Editor](/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine) for the Skeletal Mesh you want to create this for.

![create mesh socket](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a99f8a4-bc92-4e80-af54-53e701e8c7f0/meshsocket2.png)

As with Sockets existing on the Skeleton Asset, Mesh Sockets will instead exist on the Skeletal Mesh, requiring you to save that asset if you create or modify Mesh Sockets.

### Socket Details

Sockets contain the following properties in the **Details** panel when selected.

![socket details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a292f2d7-43b8-4df9-9fe8-32276092b622/details1.png)

| Name | Description |
| --- | --- |
| **Relative Location / Rotation / Scale** | The current transform coordinates of the Socket in relative coordinates to its parent Bone in either location, rotation, or scale. |
| **Force Always Animated** | Enabling this will cause all parent bones of this Socket to always evaluate, regardless of if they are being removed due to the current LOD setting. |
| **Socket Name** | The name of this Socket. |
| **Bone Name** | The name of the Bone this Socket is attached to. Changing this value to a different Bone will re-parent the Socket. |

## Attaching with Sockets

Once you have created and positioned your Socket, you can attach objects, effects, and other actors to it. The following kinds of attachments can be performed.

### Basic Level Attachment

You can set up a basic attachment within a Level, where an object will be attached to a Socket by default. There are a few ways you can do this.

![basic socket attachment in level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70fdf2b4-d65a-4272-9933-0e44421c303c/basic1.png)

#### Drag and Drop

In the Level Outliner, drag the object onto your Skeletal Mesh Actor. A window will appear after where you can select any Bone or Socket to attach to. Select your Socket and the attachment process will complete.

![drag and drop socket attach](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1680a36a-c874-4936-b05f-a200bb6f9253/basic2.gif)

When attaching in the Level, the object will retain its world transform from before, which can be useful if you are creating unique offsets for different objects. If you want the object to match the Socket's transform, then set the transform values of the object to default.

![zero transform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a03856ea-47d3-4d5c-9623-89f7eca480de/basic3.png)

#### Context Menu

Right-click your object and select **Attach To**, then click on your Skeletal Mesh Actor. A window will appear after where you can select any Bone or Socket to attach to. Select your Socket and the attachment process will complete.

![context menu socket attach](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3438d7d5-b35d-4227-a274-bc232d1755ae/basic4.png)

#### Socket Snapping

Click the **Settings** dropdown menu in the Level editor and select **Enable Socket Snapping**. This will make all **Sockets** visible in the viewport.

![enable socket snapping](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5957c61a-8e22-4baa-85df-1dc8011f6209/basic5.png)

Next, you can quickly attach an object to any visible Socket by selecting the object first, then selecting a Socket.

![socket snap attach](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc417dba-c585-41a6-95bc-71997e8cfb8b/basic6.gif)

### Basic Blueprint Attachment

You can also set up a basic default attachment to a **Skeletal Mesh Component** in [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine).

First, parent the object to the Skeletal Mesh Component by dragging the object on the Skeletal Mesh in the **Components** panel.

![blueprint socket attachment](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d9f1e69-432b-445f-b12d-94f570661f7c/blueprints1.png)

Next, select the child object, and in the **Details** panel locate the **Parent Socket** property. Click the **search button** and select the Socket to attach to.

![blueprint parent socket attachment](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee684b9a-3813-4559-966e-7d70fe931a2d/blueprints2.gif)

### Dynamic Attachment

In cases where you want to control when your object attaches and detaches to Sockets, you can use various **Attach** and **Detach** Blueprint functions.

For attaching, you can use the following functions:

-   **Attach Actor To Actor**.
-   **Attach Actor To Component**.
-   **Attach Component To Component**.

![attach blueprint functions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf2230c1-7100-4ff8-9ea8-d2cd7c9a2af7/dynamic1.png)

Attaching functions contain the following properties:

| Name | Description |
| --- | --- |
| **Target** | The child actor or component that is being attached. |
| **Parent** | The parent actor or component that the **Target** is being attached to. |
| **Socket** | The Socket to use when attaching |
| **Location / Rotation / Scale Rule** | 
Transform rules that control where the **Target** should end up after being attached. You can select from the following options:

-   **Keep Relative**, which maintains the current transform numerical values. This will likely cause the Target to pop into a new position and is useful to maintain the same offset coordinates when attaching.
-   **Keep World**, which will maintain the current visual transform of the Target. This will not cause a pop when attaching as a calculation will occur to maintain the same visual transform before and after the attachment.
-   **Snap to Target**, which will teleport the Target to the coordinates of the Parent or Socket.



 |
| **Weld Simulated Bodies** | Whether or not to [weld](/documentation/en-us/unreal-engine/welding-physics-bodies-in-unreal-engine-by-using-the-physics-asset-editor) the Target to the Parent. |

For detaching, you can use the following functions:

-   **Detach From Actor**
-   **Detach From Component**

![detach blueprint functions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2cda117-1ae9-46ee-96e8-885714b737f1/dynamic2.png)
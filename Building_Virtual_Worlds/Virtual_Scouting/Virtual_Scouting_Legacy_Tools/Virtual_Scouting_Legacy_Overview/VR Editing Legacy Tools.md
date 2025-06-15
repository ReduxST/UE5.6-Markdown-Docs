# VR Editing Legacy Tools

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/vr-editing-legacy-tools](https://dev.epicgames.com/documentation/en-us/unreal-engine/vr-editing-legacy-tools)  
**Processed:** 2025-06-14 17:03:48

---

The [Virtual Scouting Legacy tools](/documentation/en-us/unreal-engine/virtual-scouting-legacy-tools) described on this page will be sunset and deprecated in a future engine release. We encourage users to move to the [new Virtual Scouting tools](/documentation/en-us/unreal-engine/virtual-scouting-in-unreal-engine). Unused VREditor code and modules will be fully deprecated in a future engine release.

## Interaction

The **Interaction** tool allows you to transform and manipulate objects in your scene. When in Interact mode, a ray always appears from your virtual controller indicating where you are pointing in the scene. Direct this pointer at an object in the scene in order to interact with it by translating, scaling, or rotating the object in the scene. There are two ways to switch to the Interact tool:

-   Select the **Interact** option in the Virtual Scouting menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7472b0c-b0a2-443c-a7f4-8d37abed0d43/image_19.png)
-   Double tap the menu button on one of your motion controllers.
    
    |   |   |
    | --- | --- |
    | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2c9ca86-5746-430f-9269-99931c207cab/03.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfe5a21d-286a-4fc4-99eb-67a32c620276/rightrifts_fastinteract.png) |
    | Vive | Oculus Touch |
    

Select an object by directing the pointer at the object and then pressing and releasing the trigger on your motion controller.

-   When an object is selected, it is highlighted in the scene.
-   After an object is selected, press and hold the trigger to move it around at the end of the pointer.
-   Scroll up or down on the Vive motion controller's trackpad to move the object away from or toward you, respectively, along the pointer ray.
-   You can also select an object by holding your virtual controller inside the object's collision layer. With your virtual controller still inside the object's collision layer, press and hold the trigger to grab the object and move it around the scene.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63cf5ba9-d29d-4a67-8052-82472cec1034/badger_interact_selectiongold.png)

### Transformation Gizmos

The Interaction tool includes the ability to transform objects by scaling, rotating, and translating them.

#### Transformation Gizmos with the Vive Controllers

The Vive motion controller's trackpad is divided into four sections:.

-   Press the top section of the trackpad to fly through the scene while holding an object.
-   As with the Navigation tool, use the bottom section of the Vive motion controller's trackpad to teleport.
-   The right side of the trackpad cycles through the standard transformation gizmos—translation, rotation, and scaling. These transformations can occur along all three axes with ways to constrain movement to a combination of two axes.
-   The left side of the trackpad toggles between the selected gizmo and the Universal Gizmo.
    -   Translation, rotation, and scaling are separate gizmos and occur along all three axes with ways to constrain movement to a combination of two axes.
    -   The Universal Gizmo combines translation, rotation, and scaling into one gizmo.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad299ce5-ad55-40be-b180-38f62b911c98/04.png)

#### Transformation Gizmos with the Oculus Touch Controllers

The Oculus Touch controllers are organized as follows:

-   Move the thumbstick on the Oculus Touch controller in the direction you want to fly.
-   As with the Navigation tool, you can teleport by pressing the B or Y buttons on the Oculus Touch controller.
-   Clicking down on the Oculus Touch controller's thumbstick cycles through the standard transformation gizmos as well as the Universal Gizmo.
    -   Translation, rotation, and scaling are separate gizmos and occur along all three axes with ways to constrain movement to a combination of two axes.
    -   The Universal Gizmo combines translation, rotation, and scaling into one gizmo.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32e91adc-a6bc-4205-a5b8-a6f98f7db633/rightrift_interact.png)

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8ce24a4-f9de-463a-b731-a2ae893eab7e/badger_interact_universalgizmo.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3c75094-f057-4e87-ae65-0c0406a78920/badger_interact_standardgizmo.png) |
| Universal Transform Gizmo | Standard Translation Gizmo |

### Object Context Menu

When an object is selected, you can open a context menu to quickly perform a series of actions. To open the context menu, press the **Menu** button on the motion controller. For most objects the context menu buttons default to the two options below. Cameras and lights have other options. Refer to the **Camera Context Menu** in the **Viewfinder** tool section and the **Light Context Menu** in the **Gaffer** tool section of the [VR Camera and Light Tools](/documentation/en-us/unreal-engine/vr-camera-and-light-legacy-tools) for more.

-   **Delete**: Removes the selected object from the scene.
-   **Duplicate**: Makes a copy of the selected object in the scene.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98e67bc1-2f67-4c41-8de8-2979404ab31c/image_22.png)

To use the gizmos, you must enable the Transform Gizmo option in the Virtual Scouting menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c87774e-eec5-49c7-b1e4-a35eb88c768f/image_21.png)

## Marker

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a13ea6e-b374-42dc-b4d6-b60b72e3308d/image_41.png)

With the **Marker** tool, you can spawn a colored ribbon in your scene for making notations in the scene. These marks are also visible to other users in a Multi-User Virtual Scouting session. To switch to the Marker tool, open the Virtual Scouting menu and select the Marker option.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86ae879d-a578-43cd-8f95-7e41abfce29a/image_42.png)

-   With the Marker tool equipped, press the trigger on your motion controller to draw a three-dimensional ribbon in the scene with the tip of the virtual controller.
-   To change the color of the marker, rest your thumb on the Vive motion controller's trackpad or move the Oculus Touch controller's thumbstick to select a color in the color wheel.
-   Clicking down on the Vive motion controller's trackpad or the Oculus Touch controller's thumbstick selects the color to which the white circle is pointing.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9878cb70-121e-4838-9bb8-39f53f5add70/image_43.png)

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e997ee1a-235f-4871-99ca-05c03ba10bce/05.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5bd08696-8c34-439f-ae94-8cb6278913c2/rightriftsmarker.png) |
| Vive | Oculus Touch |

You can erase the marks you make with the Marker tool.

-   Select the eraser icon in the middle of the color wheel to switch the marker into an eraser.
-   To delete a mark, move the tip of the virtual controller to the mark and press the trigger on the motion controller.
-   Marks can also be deleted with the **Undo** option in the Virtual Scouting menu or with the Undo gesture.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ee1f93e-6b6c-42d8-b2f8-543b0e32a1f5/image_44.png)

## Measure

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d952981e-7343-43a7-9534-4ca673d85fb8/measure_metric.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8992ad6f-dcd0-4ae1-be1e-bfe3804b815a/measure_imperial.png) |
| Measure tool example with metric units | Measure tool example with imperial units |

With the **Measure** tool, you can measure the distance between objects or specific locations in your scene, in either metric or imperial units. To switch to the Measure tool, open the Virtual Scouting menu and select the Measure option.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1b14ee8-0ec0-4324-a2b5-753242ca5503/image_46.png)

With the Measure tool equipped, a pointer ray projects from your virtual controller.

-   A small gold cube appears at the end of the ray when there is an object from which that you can measure the distance from. Press the trigger on your motion controller to trace a light blue line to another object.
-   Release the trigger to measure the length of the light blue line. A heads-up display (HUD) appears with the measurement between the two points.
-   To switch the measurement units in the HUD, open the Settings panel in the Virtual Scouting menu and toggle between metric and imperial unit scale.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecebe646-2202-4424-b8e9-3794af899525/image_47.png)

In addition to measuring the distance between objects, you can place custom flags to measure between different locations in your scene. Placing multiple flags shows the distance between neighboring flags as well as the total distance from end to end.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/041c33f9-8bc3-42a4-bced-c0f4f55b84c2/image_49.png)

-   To place these flags in your scene, use the top section of the Vive motion controller's trackpad or the B or Y buttons on the Oculus Touch controller with the Measure tool active.
-   To remove an existing flag, move the virtual controller towards the flag until it interacts with it. Then, click the bottom half of the Vive motion controller's trackpad or pull the Oculus Touch controller's thumbstick down.
-   Flags also disappear when you switch away from the Measure tool.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4a025c8-ec69-41dc-bcfb-8a66614e050f/06.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fdd1471-1932-4143-80bf-1c7e26b688f7/rightrift_flag.png) |
| Vive | Oculus Touch |

## Multi-User Editing

Virtual Scouting as a workflow concept makes heavy use of the **Multi-User Editor** so all of the key members of a production can explore a scene together. All tools, unless otherwise noted, will have their changes reflected to all users in the multi-user session.

When multiple users are in a session, their names will appear in the left section of the menu. You can teleport to another user's location by selecting that user in this list.

Not all users have to be in virtual reality to participate. Sessions often work best when one of the artists is working from the desktop, performing complex actions that are hard to do in VR but straightforward when sitting in front of a computer.

For more information on multi-user editing, see [Multi-User Editing](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1db798bc-7305-45e8-9d02-0d476ad5b3f4/multiuser.jpg)

**Pointer**

You can create a pointer ray from your virtual controller that is visible to other users in your Multi-User scouting session in order to direct their attention to a particular part of the scene. To use the pointer function, activate the Navigation tool and either press on the top section of the Vive motion controller's trackpad or press the trigger on the Oculus Touch controller.

### Flare

To show where you are in the level to other users who are in a Multi-User scouting session with you, hold both controllers up over your head until they are close together. A red flare appears from the tip of your virtual controller.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83a85fd8-afea-48be-b709-f5cd3457ea5b/_mg_0292_cropped.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9a9ba73-cfd1-47e9-8c5f-6badeecb68a3/badger_beacon_example.png) |

## Sequencer

Using the **Sequencer** tool, you can play back a sequence within your scene. To activate the tool, open the Virtual Scouting Menu and select the Sequence panel at the bottom of the menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/706d1f70-16d1-45d7-992d-dc0c20c915ac/image_62.png)

You must have a sequence already added to your level and the Sequencer window / tab must be open in UE4 for this tool to function properly. See the [Sequencer Overview](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview) for more information on adding a sequence to your level.

-   To scrub the sequence timeline, press and hold the trigger on your motion controller and move the motion controller to your right or left.
-   To play or pause the sequence, press the B or Y buttons on your Oculus Touch controller or press down on the center of your Vive controller's trackpad.
-   You can slowly track the playhead forward or back.
    -   Using the Vive motion controller, slide your thumb over the trackpad in a clockwise or counter-clockwise direction.
    -   Using the Oculus Touch controller, move the thumbstick on to the left or right.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bc10360-0d11-4b32-a3d7-780a524be857/07.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0871578-f974-4ce0-ac91-dceeaa61549e/rightrift_sequencer.png) |
| Vive | Oculus Touch |

### Live Editing with Sequencer

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2313eab2-5e72-4b29-a32c-e4a5e027bcf1/image_65.png)

**Live Editing** provides the ability to animate objects and keyframe objects in real time while in VR. This requires that your level have a sequence associated with it so the additional keys can be saved within that sequence.

Live Editing must be enabled in the Virtual Scouting Settings to use this feature.

To set keys and manipulate objects in your scene over time, you need to make changes to the position, rotation, or scale of your object on different frames in your sequence. Move the sequence to the frame number you wish to modify and edit the objects using the Interaction tool. When you scrub the sequence, you can see the edit you made to the object in the playback.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/026c84f7-48b8-496c-9a7c-00dbf006609b/image_64.png)

The Sequencer tool is important for this workflow.

**Editing: Turn Off Snapping**

When interacting directly with objects in VR, disabling snapping features can provide a better experience because movements will be smoother. You can disable these settings by following these steps.

1.  Navigate to Edit > Editor Preferences.
2.  Select the Viewports section.
3.  Disable Grid Snapping, Rotation Snapping, and Scale Snapping.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bbe6527e-bd57-49a8-a732-5dc54af37bf1/image_10.png)
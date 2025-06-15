# Unreal VCam Tools and Configuration

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-vcam-tools-and-configuration-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-vcam-tools-and-configuration-in-unreal-engine)  
**Processed:** 2025-06-14 16:57:38

---

The **Tools** menu includes configurable settings and toggles that let you adjust how you interact with the Live Link-enabled device and the virtual camera in the Unreal Engine scene.

To open the Tools menu, tap the **Wrench** icon on the right side of the screen.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86d768ab-b23c-4a93-9cc3-cb68a923794b/vcamtoolsicon.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c62e4000-a189-4bcb-9f7f-125fd715420a/vcamtoolsmenu.png)

The **Tools** menu includes the following settings:

| **Icon** | **Dial Name / Action** | **Description** |
| --- | --- | --- |
| **Section 1** |   |   |
| ![Takes Browser icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d720262d-e98b-49db-832d-f1f6a07b34d2/takesbrowser.png) | [**Takes Browser**](/documentation/en-us/unreal-engine/unreal-vcam-tools-and-configuration-in-unreal-engine#browsingforsequencesandreviewingtakes) | Opens the Virtual Camera’s Takes Browser, where you can search for and open level sequences for review or recording. |
| ![Scale and Gain icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/659aff79-c6cd-4c9a-89d5-dac8ba0c1d74/scaleandgain.png) | [**Scale and Gain Settings**](/documentation/en-us/unreal-engine/unreal-vcam-tools-and-configuration-in-unreal-engine#virtualcameramovementwithscaleandgainsettings) | Contains settings to configure how movement of the Live Link-enabled device works with the Unreal Engine scene. This includes how sensitive the movement of the device is in a physical space and the sensitivity of the joystick movement. |
| ![Hold icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b28df59a-7b75-4098-bfef-bc4887e5d4b9/hold.png) | **Hold** | Toggle this to freeze the virtual camera's location and rotation until it is toggled again. This is useful for repositioning your physical live link-enabled devices without losing your virtual camera's position in the scene. |
| ![Zero to Stage icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e62cf9d8-dac8-4ab9-b4ab-d2bf6fc46cc6/zerotostage.png) | **Zero To Stage** | Tap this to remove any offsets to the virtual camera’s tracked location. This puts the camera back into tracking space. |
| ![Zero to Parent icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d099ce20-c3bf-43b7-8cae-d9b89c41bc2b/zerotoparent.png) | **Zero to Parent** | Tap this to snap the virtual camera onto its parent with an effective relative location of (0,0,0). If the virtual camera has no parent, this snaps to the world origin. |
| ![Local Space Flight Mode icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/622daec9-5f88-4ece-99f4-cf6800c1c027/localspaceflightmode.png) | **Local Space Flight Mode** | Enable this to make the forward joystick movement follow the forward direction of the camera instead of the world. When in Local Space Flight Mode, looking up or down moves the camera in that direction when you push a joystick forward. When disabled, the camera can freely look around the scene but move forward without moving in the direction the camera is pointed. |
| ![Kill Roll icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffc01b50-35b3-4ba6-8113-565a12d55f89/killroll.png) | **Kill Roll** | Toggle this to disable virtual camera rotation along the X-axis, keeping the camera level when moving around while the Live Link-connected device is moving in a physical space. |
| ![Spline Mode icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fd7b9a4-827c-459b-8586-4046bec3eae8/splinemode.png) | [**Spline Mode**](/documentation/en-us/unreal-engine/unreal-vcam-tools-and-configuration-in-unreal-engine#creatingandoperatingcustomrigrails) | This mode lets you create and edit your own Rig Rails from the Unreal VCam app. |
| ![Tile Offset icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/153f2ff5-ca41-4924-8d6a-7f512a665503/tiltoffseticon.png) | **Tile Offset** | 
Enable this to apply an arbitrary offset to the Tilt of the virtual camera. This makes holding shot angles more comfortable. When enabled, the Tilt HUD value will display a + symbol.

![Tile offset enabled HUD display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a489c67a-7932-4bd1-8764-19fd9c752da4/tiltoffsetenabled.png)

 |
| ![Bookmark Browser icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9e83cdd-538b-4270-849f-1ceaed63fb24/bookmarkbrowsericon.png) | **Bookmark Browser** | Opens the Virtual Camera Bookmark Browser |
| ![Multi User Replication](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34924683-85c8-43ff-a636-c1794eba92c1/multiuserreplication.png) | **Multi User Replication** | Tapping this sets the current client as the author of the Virtual Camera in Multi User, changes made from this client propagate to others, while changes from others are overridden from this client. |

### Virtual Camera Movement with Scale and Gain Settings

Movement in the Live Link-enabled device is registered by tracking positional data from the device and through the use of touch-screen joysticks, including tilt, pan, and roll movement. The touch-screen joysticks layer directional and rotational movement on top of the ARKit motion.

Virtual camera movement from a Live-Link-enabled device is controlled by:

-   ARKit tracked axial and locomotor movement.
    
-   Touch-screen Joysticks
    
-   The **Left** joystick controls directional forward, backward, diagonal, and side-to-side movement.
    
-   The **Right** joystick includes two separate movement controls:
    
-   **Rotational** movement by dragging left and right on the screen.
    
-   **Vertical** movement by dragging up and down on the screen.
    

You can adjust the sensitivity of each type of movement so that small movements can have a bigger effect, or the opposite where bigger movements have smaller impact. You can find these controls under the **Scale and Gain** settings menu on the right side of the screen.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cb1acec-95fe-4aa3-96bb-2b3eff153b58/scaleandgainsettings.png)

The menu includes the following settings:

| **Dial Name / Action** | **Description** |
| --- | --- |
| **Left Dials** |   |
| **Axis** | 
Sets the axis constraint for movement:

-   **All** allows movement along all axes.
-   **Planar** allows only movement along the X-axis and Y-axis to be scaled. Vertical movement is unaffected.
-   **Vertical** allows movement along the Z-axis to be scaled. Planar movement along the X-axis and Y-axis is unaffected.



 |
| **Scale** | Scales the ARKit tracked movement of the device in physical space. The scale adjusts how movements are translated from real-world physical space to the virtual camera digital space through Live ink. Small scale values translate as larger physical space movement to smaller digital space movement. Larger scale values translate as smaller physical space movement to larger digital space movement. |
| **Right Dials** |   |
| **Joystick Movement Gain** | Controls the speed of both the left directional joystick and the right vertical-only joystick movement. |
| **Joystick Rotation Gain** | Controls the speed of rotation when engaging the right joystick in left or right rotational movement. |

Setting any dial to **Locked** or **0** restricts movement being tracked through Live Link or any engagements of the joystick. For example, setting the Axis to Vertical with a Scale set to Locked means that vertical movement cannot happen. Another example is setting the Joystick Rotation Gain to 0 restricts any rotation applied through the joystick.

## Browsing for Sequences and Reviewing Takes

### Takes Browser

Tapping the **Takes Browser** button in the tools menu opens the Takes Browser. The Takes Browser displays a sorted list of level sequences that can be opened for review or recording.

![The Takes Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fe1fe9c-1394-408e-b348-3041a020cfc1/browsingtakes.png)

Tapping on a level sequence brings up two options

| **Button** | **Description** |
| --- | --- |
| ![Takes Reload icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5aacacd1-cd1c-4822-acb5-ba201945767e/takesreload.png) | Tap this to load the selected sequence into the Take Recorder, making it the base for the next recording. Use this option to select the animation that you want to record cameras onto. |
| ![Takes Review icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f533c19a-bec1-4bd2-a756-18c8d3c2c839/takesreview.png) | Tap this to open a sequence into review. This pilots the camera cuts track of the sequence and provides simplified controls for reviewing the sequence. |

Holding on a level sequence shows the asset path. It also shows the dirty state when the level sequence is modified

![Take overlay showing asset path](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48373e1a-bd93-483c-bc25-14f07f1f1b24/vcam_takeoverlay.png)

#### Tagging Takes

Swiping left or right on a sequence in the Takes Browser tags that sequence with the selected metadata, which can be used to filter the sequences in the Takes Browser.

| **Option** | **Description** |
| --- | --- |
| ![Star tag](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f674f382-f6b8-4cba-9b40-15a46d31dffa/startag.png) | Swiping to the right illuminates one, two, or three stars, depending on how far you swipe. Stopping at a number of illuminated stars tags the take with that number of stars. |
| ![Flag take](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95919f9e-9f40-494d-9f54-f2575579335e/flagtakes.png) | Swiping to the left reveals a yellow flag. Tapping this tags the take as flagged. Use this flag to denote any information relevant to your workflow. |
| ![Take no good](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73c52986-f2bb-48a5-abbd-8e8651fba914/takenogood.png) | 
Swiping to the left reveals a red thumbs down. Tapping this marks the take as "no good" and filters it out of the Takes Browser. After tapping, you are presented with a short undo prompt. Tapping this before the time has elapsed removes the No Good tag and returns the take to the browser.

This does not delete the level sequence, only hides it from the Takes Browser list by default.



 |

#### Filtering and Ordering the Takes Browser

The top of the Takes Browser contains a search bar and filters dropdown. Typing into this search bar filters the list by takes containing the matching string.

![Filter takes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/173c2e44-dcaa-4099-95c1-4a41658076ad/filtertakes.png)

Tapping the filters dropdown reveals or hides the Takes Browser filters and sorting options.

![Take Sorting options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9ebf679-c5d1-46b1-92ac-2daa8951d8a0/takesort.png)

The available filters are:

| **Filter/Sorting Option** | **Description** |
| --- | --- |
| ![Show Only Take icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/070f55be-cab2-48a0-acfc-6cdafc9b1ebc/showonlytake.png) | Tap this to toggle showing only sequences recorded from Take Recorder and hide Non-recorded sequences. |
| ![Show Flagged icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47fa1e74-8549-4407-80b9-5446eb7068f6/showflagged.png) | Tap this to toggle showing only sequences marked with the flag tag. |
| ![Show No Good icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ac1c5ab-8a28-4f5a-803c-24f22dffe943/shownogood.png) | Tap this to toggle only sequences marked as "no good". Use this if a sequence needs to be recovered or was marked no good in error. |
| ![Show Starred icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25308909-62e1-4783-9d30-50ce06bfa540/showstarred.png) | Tap this to cycle between showing only sequences tagged with a number of stars greater than the number shown. For example, tapping until the star displays the number 2 shows only sequences with 2 or 3 stars. |
| ![Sort Takes by Time icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29fe3ef6-e3a2-4cf7-83c5-a8c6bfa6fc30/sorttakestime.png) | Tap this to cycle between sorting the Takes Browser newest to oldest or oldest to newest. There is no sub sorting, so the list can only be sorted by creation date or alphabetically. |
| ![Sort Takes Alphabetical icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/311808fc-132c-4acf-8cab-2dab05d4c998/sorttakesalpha.png) | Tap this to cycle between sorting the Takes Browser in alphabetical or reverse alphabetical order. There is no sub sorting, so the list can only be sorted by creation date or alphabetically. |

### Take Viewer

You can use the Take Viewer to navigate between individual takes, so you can tag and smooth them.

The Take Viewer window opens when you load a take from the Takes Browser. Alternatively, you can tap the Take thumbnail in the lower left corner in the HUD to open the latest Take.

![Take Viewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/562857bd-323b-4962-840e-9c2316824b8a/takeviewer.jpg)

#### Tagging Takes

On the current Take, you can add stars, a flag tag, or mark the take as "no good.

![Take tagging options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f11db29-0074-4786-9a13-a0fe0e5ad81f/takeviewer_tagging.png)

#### Smoothing Takes

When viewing a take, you can tap the button in the top right corner to show a slider to smooth the camera keyframes in the level sequence

![Slider for Take smoothing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6960ab8d-8f8d-4e0f-917b-5668882188d6/vcam_smoothtake.png)

#### Navigating Takes With Carousel View

To open the carousel view, tap the Take thumbnail in the lower left corner. The carousel view lists all takes in chronological order.

![Take Viewer carousel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/764519e6-1473-4397-afde-92cbe4f4d51f/takeviewer_carousel.png)

In the carousel view, you can do the following:

-   Swipe the thumbnails to navigate the takes. The thumbnail in the center becomes the current item, which is indicated by the white highlight on top and the thumbnail being bigger in the preview window.
    
-   Tap the preview window to open the level sequence for review. The blue highlight on the top indicates the current level sequence in review.
    
-   Tap the down arrow in the lower button to close the carousel view.
    
-   Tap the **<** and **\>** buttons next to the carousel to navigate the takes one by one.
    

#### Open Takes Browser

You can tap the magnifier icon on the lower right corner to open Takes Browser for more search and filtering options. For more information about the Takes Browser, see the Takes Browser section under Browsing for Sequences and Reviewing Tasks further up on this page.

![Open Takes Browser icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c2ed06a-5572-40e0-b322-e44f244c962c/takeviewer_takesbrowser.png)

## Teleporting

Pressing down on the screen with 2 fingers and dragging enables teleportation of the VCam for faster movement around the scene. While 2 fingers are held down, a blue landing zone indicator is displayed where you are touching. Moving your fingers causes the landing zone to follow your fingers. Upon releasing your fingers, the Virtual Camera teleports to the location indicated by the landing zone.

Teleportation can only detect surfaces with collision.

### Sequencer and Bookmarks Settings

The bottom-most section of the Virtual Camera actor includes quick reference to camera settings, and Sequencer playback. The top-most section contains camera bookmarks and recording.

![Virtual Camera actor top](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9db8bfc-3d2e-4a3a-b856-4593cdf0b9ad/vcamtop.png) ![Virtual Camera actor bottom](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a265748-e072-4187-be7f-de9969525596/vcambottom.png)

| **Icon** | **Dial Name / Action** | **Description** |
| --- | --- | --- |
| **Section 1** |   |   |
| ![Create Bookmark icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b7558ee-897d-4e5f-9a75-77fe7be600a4/createbookmark.png) | **Create Bookmark** | Tap this to create a bookmark of the current position and rotation and camera settings used by the virtual camera. If you have Photo Save Mode enabled, an icon image of a DSLR Camera appears instead. |
| ![Re-inherit Camera Settings icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21ed1047-d4fa-4029-9df3-1287e495dce9/reinheritcamera.png) | **Re-inherit Camera Settings** | Bookmarks store camera parameters (including aperture and focal length). This controls whether those stored camera parameters are loaded when jumping to a bookmark. |
| ![Bookmark Navigation icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48377a1b-e6cf-4bc9-b415-5b512e631506/bookmarknavigation.png) | **Bookmark Navigation** | Navigational controls to cycle forward and backwards through any virtual camera bookmarks in the scene. |
| ![Remove Bookmark icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b48b94aa-e17e-4379-9840-b2a8e7ac1a31/removebookmark.png) | **Remove Bookmark** | Tap this to remove the currently selected bookmark from the Unreal VCam app. This button removes the bookmark scene actor from your Unreal Engine project. |
| ![Current/Select Bookmark icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d895cae9-1438-4259-aaa0-3372ce674d46/currentselectbookmark.png) | **Current/Select Bookmark** | Displays the most recently loaded bookmark. Tapping this brings up a list of available bookmarks which can be selected from. |
| **Section 2** |   |   |
| ![Scale icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba18695e-63d1-4e3b-90e6-123391ea7f2b/scale.png) | **Scale** | Displays the current scales applied to device movement. For more information, see [Virtual Camera Movement with Scale and Gain Settings](/documentation/en-us/unreal-engine/controlling-a-virtual-camera-actor-using-live-link-in-unreal-engine#virtualcameramovementwithscaleandgainsettings). |
| ![Stabilization icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b13fc7ea-95fb-4557-939f-5943d3ddf570/stabilization.png) | **Stabilization** | Displays the amount of stabilization applied to the virtual camera's rotation and location movement. Higher values give more stabilization to movement at the cost of responsiveness creating smoother camera movement. Lower values give less stabilization and are more responsive, which creates rougher camera movement. For more information, see [Virtual Camera Stabilization](/documentation/en-us/unreal-engine/controlling-a-virtual-camera-actor-using-live-link-in-unreal-engine#virtualcamerastabilization). |
| ![Orientation icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68f12f42-535c-4545-8938-d9c4a64e72fb/orientation.png) | **Tilt, Pan, Roll Orientation** | Displays the virtual camera's rotational position. For more information, see [Virtual Camera Movement with Scale and Gain Settings](/documentation/en-us/unreal-engine/controlling-a-virtual-camera-actor-using-live-link-in-unreal-engine#virtualcameramovementwithscaleandgainsettings). |
| **Section 3** |   |   |
| ![Timeline icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/404c86d6-89c4-4073-9ba0-140e4ed3fa53/timeline.png) | **Timeline** | Displays the timeline for the currently loaded Sequence in the Unreal Editor. To move the slider to a different frame within the Sequence, drag your finger along the timeline. |
| ![Sequencer Playback Controls icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd8ea8ec-4e8b-4572-9174-0a1d775706e3/playbackcontrol.png) | **Sequencer Playback Controls** | The playback controls function similarly to standard media playback applications with play, skip frame, skip to beginning and end frames, and so on. For more information, see [Sequencer Cinematic Editor](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine). |
| ![Playback TimeScale icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1599c116-6cbc-464b-a321-bbdde9c4cc5b/timescale.png) | **Playback TimeScale** | Use this to the time scale of the sequencer. For example, setting a value of 0.5x causes the sequence to playback at half speed. |
| ![Slate icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ac8e86d-7a0f-473e-98fa-fe8ec08ace3c/slate.png) | **Slate** | Displays the slate name to be used for the next recording. This can be tapped to bring up the on screen keyboard, allowing the slate name to be edited |
| ![Take number icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5dedf64b-c748-498f-841a-2b021fbe6158/takenumber.png) | **Take** | Displays the take number of the next recording. This can be tapped to bring up the on screen keyboard, allowing the take number to be edited. |
| ![Sequencer Frame Counter icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27c060e1-80a3-42e0-b61b-36f62be2c227/sequencerframecounter.png) | **Sequencer Frame Counter** | Displays the current frame number the timeline is reading. |
| ![Take Recorder icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4663ccd5-2ecf-4278-8736-76cf490c8b4d/takerecorder.png) | **Take Recorder** | Tap this to open Take Recorder and start recording of gameplay, live performance, and other sources directly into Unreal Engine. For more details, see [Take Recorder](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine) and [Using Take Recorder](/documentation/en-us/unreal-engine/record-gameplay-in-unreal-engine). |
| ![Recording Time Scale icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6d15c01-5a00-4281-b6de-385e0dd712f6/recordingtimescale.png) | **Recording Time Scale** | Use this to set the current time scale for the recording. For example, recording at 0.5x plays the pending take back at half speed. When reviewed, your camera move is sped up 2x to match the original speed of the sequence. |
| ![Open Last Take icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb48e021-e74f-48e5-b971-a58756b18e6e/takedefaulticon.png) | **Open Last Take** | Tap the thumbnail to open the last recorded take in Take Viewer. |

### Virtual Camera Stabilization

Tap on the **Stabilization** text to open the virtual camera stabilization dials. These dials affect how much the camera prevents or compensates for unwanted camera movement. Camera movement appears smoother and less responsive when using higher stabilization values. Lower values tend to be more responsive, causing a lot of shake and instability in camera movement.

The **Left** dial controls **Rotation Stabilization**, and the **Right** dial controls **Location Stabilization**. In the video below, you can see the difference between using a value of 0x, 50x (default), and 100x.

## Parenting and Platforming

When not in Spline Mode, the top right of the virtual camera displays the parenting and platforming control.

![Parenting and Platforming controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/887fda00-d081-4f6e-9439-43dbbc1cd799/parentingplatforming.png)

### Creating an Attach Mount

Though the virtual camera can be attached to anything from the desktop, the available options to the handheld operator are limited to Cine Camera RigRails, Cine Camera Actors, and Cine Camera Attach Mounts. Using the Cine Camera Attach Mount gives you more control over how the virtual camera attaches to its parent, including enabling and disabling certain axes as well as introducing lag in following the parent for a more natural follow behavior.

To create an Attach Mount click the place actors menu and search for "attach." Drag and drop the **Cine Camera Attach Mount** into the world.

![Create an Attach Mount](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4b9b3d7-3f99-42f5-91eb-51f5de3ab2c4/createattachmount.png)

To configure the parent for the attach mount, select it in the world outliner and in the **Details** panel**,** set the **Target Actor** to the desired actor. If the Target Actor is skeletal, specify the **Target Socket** to enable attachment to a specific bone or socket.

![Configure an Attach Mount](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f1e6a9a-870f-4c43-8e87-4d81d5a2a6e0/configureattachmount.png)

Name the Attach Mount to something indicative of its parent for later.

### Selecting and Attaching to a Parent

Tapping the central dropdown brings up a list of available parents. Though the virtual camera can be attached to anything in your scene, the available options to the handheld operator are limited to Cine Camera Rig Rails, Cine Camera Actors, and Cine Camera Attach Mounts. Selecting an option from this drop-down automatically snaps the virtual camera to its new parent and enables attachment. Attachment can be toggled on and off using the **paperclip** button.

![Select and attach a camera to a parent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23c812e5-1fd2-41f5-8ead-73d2567eaeb2/selectandattach.png)

### Inheriting Specific Axes and Camera Parameters

By default, the virtual camera inherits all axes from its parent, though it can still move on top of this platform. Selecting the right most axis button, however, expands a list of axis and camera parameters that can optionally be disabled, inherited (the virtual camera inherits its parent’s axis value but can still offset on top), or locked (the virtual camera inherits its parent’s axis value but can’t offset on top). These options are only available if the parent is CineCamera Rig Rail, Cine Camera Actor, or Cine Camera Attach Mount.

The available options are:

| Icon | Dial Name / Action | Description |
| --- | --- | --- |
| Section 1 |   |   |
| ![Dolly icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3fa3558-b05f-402d-beb9-3c632acfcf3f/dolly.png) | **Dolly** | Tap this to cycle between inheriting, locking, or ignoring the forward and backward movement of its parent. |
| ![Truck icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe5e13cb-b33b-4b9e-ab12-89795ad7bd5a/truck.png) | **Truck** | Tap this to cycle between inheriting, locking, or ignoring the side to side movement of its parent. |
| ![Crane icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0a4f61d-4320-4084-874c-f0b329183b9f/crane.png) | **Crane** | Tap this to cycle between inheriting, locking, or ignoring the up and down movement of its parent. |
| ![Roll icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/281f5dcd-6105-450e-b550-52a9f834c491/roll.png) | **Roll** | Tap this to cycle between inheriting, locking, or ignoring the roll rotation of its parent. |
| ![Tilt icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5db38b8f-129c-4ee7-8223-aa9daca2d4a3/tilt.png) | **Tilt** | Tap this to cycle between inheriting, locking, or ignoring the tilt rotation of its parent. |
| ![Pan icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd7c1b14-6184-4a8f-9ac4-5a60986908b8/pan.png) | **Pan** | Tap this to cycle between inheriting, locking, or ignoring the pan rotation of its parent. |
| ![Iris icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/939bc441-6c19-4f7a-899b-fc782ce4ba27/iris.png) | **Iris** | Tap this to cycle between inheriting, locking, or ignoring the iris camera parameter of its parent. Camera parameters can only be inherited from Cine Camera Rig Rails and Cine Camera Actor parents. |
| ![Focal Length icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1551e7c4-0bc3-4903-ba4a-153fbf99c06a/focallength.png) | **Focal Length** | Tap this to cycle between inheriting, locking, or ignoring the focal length camera parameter of its parent. Camera parameters can only be inherited from Cine Camera Rig Rails and Cine Camera Actor parents. |
| ![Focus Distance icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1bcdc89-8116-4580-a236-9ecb456a25b8/focusdistance.png) | **Focus Distance** | Tap this to cycle between inheriting, locking, or ignoring the focus distance camera parameter of its parent. Camera parameters can only be inherited from Cine Camera Rig Rails and Cine Camera Actor parents. |

### Introducing Lag to the Attachment

If attached to a CineCameraAttachMount, the virtual camera has the additional ability to enable and disable lag into the follow. This allows for more natural feeling movement when following things like cars, where a physical camera would not immediately follow a movement. To toggle lag on and off, tap the lag button in the attach menu.

![Toggle Lag](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a34dec8-6e3d-4efb-961a-08e1f8dfcb53/eagleattach.png)

The speed of this lag can be controlled from the Details panel of the CineCameraAttachMount. Lower Values for Location/Rotation Lag Speed lead to a larger delay in response, while higher values lead to a faster response.

![Set lag in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba9c235f-8a85-4cb9-8c3c-a12ce730b2be/lag.png)

## Creating and Operating Custom Rig Rails

Press the Spline icon in the tools menu to enter Spline Mode. In this mode, the attachment controls in the upper-right change to spline controls. The bottom-left now also includes keyframing controls.

Dolly splines for Virtual Camera are represented by CineCameraRigRail actors. The CineCameraRigRail allows for the creation of spline points which store both transform and camera parameters (Focus, Iris, and Zoom), which can be inherited back to and operated upon by the virtual camera.

![Creating a Spline point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c08bf4e-cd52-4556-a0b4-57290b9a977d/camerarigrail.png)

### Creating a New CineCameraRigRail

To create a new CineCameraRigRail, ensure the controls are set to the spline selection controls, represented by a spline icon.

![Select the Spline controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84c04811-99aa-4ba1-83c1-e184703a5a0a/newrigrail.png)

This mode offers the following controls:

| Icon | Dial Name / Action | Description |
| --- | --- | --- |
| Section 1 |   |   |
| ![Spline Mode Select icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3a16dab-9f84-417e-b73c-85d302623aff/splinemodeselect.png) | Mode | 
Tapping an option in this segmented control switches the current operating mode between **RigRail** selection mode, **Edit** mode, and **Drive** mode.

In **RigRail** selection mode, the blue spline icon is highlighted.



 |
| ![Active RigRail icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1d15392-1368-4741-b9e6-22fd60fd186b/activerigrail.png) | Active RigRail | This dropdown indicates the currently selected RigRail. This is the RigRail that is acted upon by all other editing, attachments, and driving tools. To change the current selection, expand the drop-down and select a new RigRail. |
| ![New RigRail icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/007f9c01-744b-4868-801f-822a95e62b94/newrigrailicon.png) | New RigRail | Tapping this creates a new RigRail, and sets it to the current selection. |
| ![Delete RigRail icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91103986-a85b-4b82-ae18-da84ebae2082/deleterigrail.png) | Delete RigRail | 

Pressing this deletes the currently selected RigRail. To confirm deletion, hold the button until the red time indicator has completed a full circle. Releasing anytime before this cancels the action.

This is a destructive action that fully deletes the CineCameraRigRail from the scene.



 |
| ![Attach icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5169cfcc-43e1-4783-8022-ea518c47c05e/attach.png) | Attach | Toggling this attaches/detaches the virtual camera from the currently selected RigRail. |
| ![Attach Axes icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/adffbbb7-a519-481c-82c2-3f72c2a14ba2/attachaxes.png) | Attach Axes | This dropdown offers controls for axis inheritance from the RigRail to the Virtual Camera. |

Tapping the New Rig Rail button creates a new CineCameraRigRail with its first point set with the current transform and camera parameters of the virtual camera. The Controls immediately switch to Editing Mode.

### Editing a CineCameraRigRail

Switching the mode segmented control to the pencil icon switches the controls to Edit Mode. This mode is used to add, remove, and modify points on the currently selected RigRail.

![Select Edit mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe1e68c3-0f5b-439e-b3a2-de5a22d617ef/editmodeselected.png)

This mode offers the following controls:

| Icon | Dial Name / Action | Description |
| --- | --- | --- |
| Section 1 |   |   |
| ![Edit Mode Select icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef3ff555-99fc-4fc4-9b48-fb095cffbf87/editmode.png) | Mode | 
Tapping an option in this segmented control switches the current operating mode between **RigRail** selection mode, **Edit** mode, and **Drive** mode.

In **Edit** mode, the blue pencil icon is highlighted.



 |
| ![Current Point icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d179812a-4bf0-4834-b20f-57b2e5f2e33f/currentpoint.png) | Current Point | This stepper displays the current position of the mount along the spline and the current point of editing. Tapping the forward and backward arrow jumps to the next or previous point, respectively. Interacting with the stepper in any way brings up a slider, which can be used to scrub along the RigRail. |
| ![Delete Current Point icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6c538ef-7109-40e6-8e29-e083d11e1393/deletecurrentpoint.png) | Delete Current Point | 

Pressing this deletes the currently selected Point. To confirm deletion, hold the button until the red time indicator has completed a full circle. Releasing anytime before this cancels the action. If the icon is grayed out, the current value of the stepper is between points.

This is a destructive action that fully deletes the point.



 |
| ![Add Point icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e67a24ee-8223-4aa4-98a9-942568914957/addpoint.png) | Add Point | 

Pressing this adds a new point to the RigRail with the current transform and camera parameters of the virtual camera. The position along spline value ascribed to this point is contextual to your current position value:

-   If the current value *n* of the stepper is at the end of the RigRail, the value is *n+1.*
-   If the current value *n* is at a point and not at the end, the value is between the current value and the next point. For example, if you press this on point 1 when there is a point 2, this creates a point with position 1.5.
-   If the current value *n* is not at a point, the position value is *n.*



 |
| ![Attach icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffead0d5-0c65-4085-9ef1-8b8202238e13/attach.png) | Attach | Toggling this attaches/detaches the virtual camera from the currently selected RigRail. |
| ![Attach Axes icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/384901ce-c284-4df3-9475-e6e4eb34e5c5/attachaxes.png) | Attach Axes | This dropdown offers controls for axis inheritance from the RigRail to the Virtual Camera. |

To create a RigRail, move the virtual camera to a position and add a point to the RigRail at that transform and with those camera parameters. Repeat this process for every point along the rail.

After completing the RigRail, tap the car icon to enter Drive mode.

### Riding and Driving a CineCamera RigRail

Switching the mode segmented control to the pencil icon switches the controls to Edit Mode. This mode is used to drive the RigRail mount movement and differs from the other two modes in that it uses the dials in addition to the spline controls.

![Creating a Custom RigRail](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7035c15-eb3b-4946-8361-ff9d8a424a3c/customrigrail.png)

Drive Mode offers 3 drive modes for controlling the RigRail, selected by the right dial:

-   **Manual:** Manual mode is used to drive RigRail by hand. When in this mode, drag the left dial to scrub the position along the rail. Manual mode should also be used if the position is being driven by hardware input or by sequencer.
    
-   **Duration:** Duration mode drives the RigRail automatically to complete the full path within the set amount of time. When in this mode, a second right dial appears. Use this dial to set the desired amount of time for the completion of one full path.
    
-   **Speed:** Speed mode drives the RigRail automatically to move at a set speed. When in this mode, a second right dial appears. Use this dial to set the desired speed (measured in cm/s). To speed up or slow down the RigRail, turn this dial while in motion.
    

Regardless of the mode selected, you can use the RigRail controls in the top-right to manage the attachment and to offer transport controls for the two automatic drive modes.

The available options are:

| Icon | Dial Name / Action | Description |
| --- | --- | --- |
| Section 1 |   |   |
| ![Drive Mode Select icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06a0bb75-5be5-419a-ac88-e7e70777eef4/drivemode.png) | Mode | 
Tapping an option in this segmented control switches the current operating mode between **RigRail** selection mode, **Edit** mode, and **Drive** mode.

In **Drive** mode, the blue car icon is highlighted.



 |
| ![Back to Start icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cde4ad3f-bc8f-48a1-8c45-5f001726d152/backtostart.png) | Back to Start | Tap this to reset the current position along the RigRail back to the first point. |
| ![Play and Reverse Play icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2f8ba46-03a7-4493-8cb2-1dfa928df046/playreverseplay.png) | 

Play and Reverse Play | These controls are only available in speed and duration modes. To make the mount move forward along the RigRail, tap the forward arrow. To make the mount move backward along the RigRail, tap the back arrow. The speed of the movement is determined by your current drive mode and settings.

While moving in either direction, the respective arrow changes to a pause icon. Tap this to pause the mount at its current position.



 |   |
| ![Loop icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be79d56d-b85b-4d84-8561-5e196da92b1b/loop.png) | Loop | Tap this to cycle between looping and not looping the spline. When looping, the spine returns to its start upon completion and continues moving according to your drive mode. |
| ![Attach icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29a8a88a-a84b-4c47-9af9-da317a7f313a/attach.png) | Attach | Toggling this attaches/detaches the virtual camera from the currently selected RigRail. |
| ![Attach Axes icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7c78bae-5fab-4a97-aa52-4e0c84568619/attachaxes.png) | Attach Axes | This dropdown offers controls for axis inheritance from the RigRail to the Virtual Camera. |

### Using Cine Camera Rig Rails with Sequencer

When in Spline Mode, an additional set of controls in the bottom-left appears, which you can use for keyframing in Sequencer. You can add and remove keyframes for the Rig Rail mount manually or through autokey. Keyframing the Rig Rail mount position allows for specific positions along the Rig Rail to be tied to frames of the current sequence. Playing a level sequence with keyframes for a Rig Rail causes the mount to move according to the keyed positions. To prevent conflicting attempts to drive the rail, the Rig Rail should be either in Manual mode or should have speed/duration modes paused.

![Using RigRail with Sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37668ba1-89eb-4533-b6db-909575b60bae/rigrailwithsequencer.png)

The color of the timeline indicates the relative speed that the mount moves during that portion of the sequence. Red indicates the fastest segments, gradienting to green for the slowest segments. A blue color indicates that the mount is stationary

The available keyframing commands are:

| Icon | Dial Name / Action | Description |
| --- | --- | --- |
| Section 1 |   |   |
| ![Autokey icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fdb716e-58fa-4426-a11f-69df94199827/autokey.png) | Autokey | 
Tap this to toggle autokey on and off.

When autokey is enabled, any new points added to the Rig Rail keys the respective position of the mount into sequencer at the current frame. Removing a point along the rail removes its respective keyframe.



 |
| ![Remove Keyframe icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/850567ba-59a9-42e3-9c8d-2c7c54577354/removekeyframe.png) | Remove Keyframe | Tap this to remove the keyframe at the current playhead position. To confirm removal, hold the button until the red time indicator has completed a full circle. Releasing anytime before this cancels the action. If the icon is grayed out, the sequencer playhead is not on a Rig Rail keyframe. |
| ![Add Keyframe icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb90141e-f000-4dfe-8a03-45d63819ba4b/addkeyframe.png) | Add Keyframe | Tap this to add a new keyframe to the open level sequence. This keyframe is placed at the playhead position and uses the current mount position as indicated on the drive mode dial or the Rig Rail controls. |

## Virtual Camera Bookmarks

To create a new **VPBookmark** actor in the scene, press the green **Bookmark** icon in the top-left of the screen on your Live Link-enabled device. This actor stores information about the virtual camera, including its position and rotation. The bookmark also stores any settings that have been adjusted for the camera, for example, the exposure and lens settings.

You can reload any placed bookmark by using the Bookmark navigation controls in the bottom-left of the screen using the forward and backwards arrows, or by tapping the bookmark drop down and choosing a bookmark from the list. Toggle the **Camera** icon to load the camera parameters stored with this bookmark, such as the aperture, filmback, and focus settings.

Use the **Minus** (-) icon to remove a currently referenced bookmark from the Live Link-enabled device. Because bookmarks exist as an actor in your Unreal Engine scene, you can also add and remove them manually from the Editor using the **Outliner** panel.

### Bookmark Browser

You can also use the Bookmark Browser to list and manage VPBookmark actors in the scene. You can launch Bookmark Browser from the bookmark icon in the right ear menu.

![Bookmark ear menu icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ce07898-051a-4b82-847b-20b57912c1f9/bookmark_earmenuicon.png)

The VPBookmark Actors are listed in the tile view:

![The Bookmark Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/000f51fa-d097-4671-b10a-fd1c932e3016/bookmarkbrowser.png)

#### Loading a bookmark

To open a bookmark, tap the thumbnail for an entry to jump to the bookmark. Once you have opened a bookmark, you have several options.

#### Tagging bookmarks

<table class="table" style="--columns-count: 2;"><tbody><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e4c874e-413d-475e-a370-5a6b3e47dc30/bookmark_swiperight.png" alt="Bookmark swipe right options" loading="lazy"></td><td>Swipe to the right to add stars.</td></tr><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11ab0cfd-d69e-4f31-8bfe-5b4fdeb84f6d/bookmark_swipeleft.png" alt="Bookmark swipe left options" loading="lazy"></td><td>Swipe to the left to either add a flag tag, or delete the bookmark.</td></tr></tbody></table>

#### Renaming bookmarks

<table class="table" style="--columns-count: 2;"><tbody><tr><td><img src="Bookmark_Rename.png" alt="Rename a bookmark" loading="lazy"></td><td>Tap and hold an entry to bring a text input in the LiveLinkVCam app where you can rename the bookmark.</td></tr></tbody></table>

#### Filtering and sorting bookmarks

The filtering and sorting options are displayed in the top part of the bookmark browser. Once you’ve expanded the Filter button, further options appear.

![Bookmark Browser filtering and sorting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/933a8e65-66a7-4177-ab71-04c961233ca3/bookmarkbrowser_sortfilter.png)

<table class="table" style="--columns-count: 2;"><tbody><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04c38cc5-4758-4efc-9d0d-d792150443ba/bookmark_filter_search.png" alt="Bookmark search filter" loading="lazy"></td><td>Type in the search field to filter bookmarks with matching words or strings.</td></tr><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51b676a6-768b-43f4-932e-1408b6afa92f/bookmark_filter_flag.png" alt="Bookmark flag filter" loading="lazy"></td><td>Tap the flag icon to list only bookmarks that are flagged.</td></tr><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32598171-2e35-4936-b177-d7f506263dca/bookmark_filter_star.png" alt="Bookmark star filter" loading="lazy"></td><td>Tap the star icon to cycle between showing only bookmarks tagged with a number of stars greater than the number shown. For example, tapping until the star displays the number 2 shows only bookmarks with 2 or 3 stars.</td></tr><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6fe124bc-cb43-4319-8c34-58342c1274bd/bookmark_sort_datetime.png" alt="Bookmark time filter" loading="lazy"></td><td>Tap this to cycle between sorting the bookmarks newest to oldest or oldest to newest. The list can only be sorted by creation date or alphabetically.</td></tr><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a53d042-4556-4cae-a245-6d0b5568a79d/bookmark_sort_name.png" alt="Bookmark alphabetical filter" loading="lazy"></td><td>Tap this to cycle between sorting the bookmarks in alphabetical or reverse alphabetical order. The list can only be sorted by creation date or alphabetically.</td></tr></tbody></table>

#### Other Options

Tap the gear icon to open the settings menu for the bookmark, which opens the following options:

![Bookmark Browser settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/737a2e84-3b06-4c21-9636-49ffe3d5bb32/bookmarkbrowser_config.png)

<table class="table" style="--columns-count: 2;"><tbody><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed8e8414-7a1c-432c-bc88-e8fe7b3c4443/bookmark_cameraparam.png" alt="Bookmark store camera parameters" loading="lazy"></td><td>Bookmarks store camera parameters, including aperture and focal length. You can use this setting to determine if those stored camera parameters should be restored when jumping to a bookmark.</td></tr><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c17483e2-3fe8-4439-83e4-7f0f637ad37c/bookmark_refreshthumbnail.png" alt="Bookmark refresh thumbnails" loading="lazy"></td><td>Tap to refresh all thumbnails.</td></tr></tbody></table>

### Controlling a Sequence

When a **Sequence** is open in the Unreal Editor, you can control the timeline and playback of it using the **Transport** buttons on your Live Link-connected device. You can use the playback controls for **Play**, **Pause**, and the **Scrub** marker on the timeline to observe the current Sequence's data.

### Using Take Recorder with Unreal VCam App

You can use **Take Recorder** to record your own Sequences (or shots) of the scene and characters in your Unreal Engine project. These can be played back within Unreal Editor using the Take Recorder and Sequencer for review.

To start recording a shot, tap the **Record** button in the top-right of the Unreal VCam app.

When you use Take Recorder with the Unreal VCam app, be aware of these things:

-   The **Take Recorder** window automatically opens in Unreal Engine (if not already open) when a recording is started.
    
-   When you start a recording, the current Level Sequence plays automatically.
    
-   After recording a take, you can click **Review the last recording** button in the Take Recorder window to see the shot. This plays back the shot and hides the virtual camera HUD. Exiting review mode unhides the virtual camera HUD.
    
-   All recorded takes are saved as **Sequencer Clips**. Saving the clip replaces the Virtual Camera actor with a [Cine Camera actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine), since virtual cameras are used to animate the camera and record its settings and movements.
    

When the Virtual Camera is active, it displays the current **Timecode**, **Slate**, and **Sequence Frame** in the HUD. This data is derived from the Take Recorder window, and displays the same information across the Unreal Editor and the Live Link-connected device.

For more information about using Take Recorder in a project, see:

-   [Take Recorder](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine)
    
-   [Using Take Recorder](/documentation/en-us/unreal-engine/record-gameplay-in-unreal-engine)
    
-   [Multi-User Take Recorder](/documentation/en-us/unreal-engine/multi-user-take-recorder-in-unreal-engine)
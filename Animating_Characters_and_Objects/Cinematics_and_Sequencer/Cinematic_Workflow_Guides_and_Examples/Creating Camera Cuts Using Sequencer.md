# Creating Camera Cuts Using Sequencer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-camera-cuts-using-sequencer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-camera-cuts-using-sequencer-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:18

---

## What is Sequencer?

![Sequence of camera cuts](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2fe1d1b-0a54-466d-b141-ea4756005a48/sequence_complete.png "Sequence of camera cuts")

[**Sequencer**](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine) is a robust cinematic tool that you can use to create animation and cinematic sequences without leaving Unreal Engine (UE). Sequencer is a non-linear editing suite. Non-linear editing is a form of offline editing for a wide variety of UE assets. In offline editing, the original content is not modified.

### Common User Cases for Sequencer

Sequencer can create level fly-throughs, animate assets such as lights, materials, objects, and characters, and render out sequences. These are some of the more common uses for Sequencer.

![Finished camera cuts](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf4365e7-5e36-47a5-8cc5-8116bf5066cb/finished_camera_cuts.gif "Complete sequence")

Sequencer provides you with the tools and intuitive UI to create cinematics using level sequences, [tracks](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine), and [keyframed assets](/documentation/en-us/unreal-engine/how-to-animate-cinematic-cameras-in-unreal-engine#creatingtransformkeyframes) all in one platform.

### What You'll Learn

This tutorial is designed to show new users to UE how to gain experience, provide a light introduction to animating assets, setting static and animated up cameras, gain exposure to Sequencer's UI, and learn how to create camera cuts in Sequencer.

## Set Up the Project

1.  Create a new Unreal Engine project using the [**Third Person template**](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine). You don't need to modify any of the default project settings.
2.  In the [**Content Browser**](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine), create a folder by right-clicking in an empty space in the Content Browser, and name it **Sequences**. Make sure you create this folder under the **Content** folder.
3.  Inside the Sequences folder, right-click and add a [**Level Sequence**](/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine#levelsequences) from the **Cinematics** menu.
4.  Double-click this sequence to open it in Sequencer. At this point, you have an empty level sequence.

## Animate a Cube

With your level sequence set up, you need to consider what your camera cuts will focus on. For this tutorial, you'll animate a cube moving across the scene and create three camera cuts to follow it as it moves.

1.  From the [**Outliner**](/documentation/en-us/unreal-engine/outliner-in-unreal-engine) or the [**Viewport**](/documentation/en-us/unreal-engine/editor-viewports-in-unreal-engine), select **SM\_ChamferCube2**. This cube is the one furthest away from the three cubes that come with the template.
    
    ![Select the cube](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/367d9d9a-0d60-417d-90b0-6e8973e6d336/select_cube.png "Select the cube")
2.  In Sequencer, click the **\+ Add** button and select **Actor to Sequencer > Add 'SM\_ChamferCube2'**. This creates a track that has a transform property that you can animate in Sequencer.
    
    ![Add selected cube as a track in Sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecf6c18f-a737-4020-9be1-a0fdfb8c4384/track_actor_to_sequencer_cube.png "Add cube to Sequencer")
3.  Expand the [**Transform property**](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine) and click the **Add keyframe button** at frame 0000 for the **Location** property of Transform. This adds a keyframe to the X, Y, and Z attributes of Location. If you haven't moved this cube, the Location keyframe should be set to 1050 on X, 320 on Y, and 50 on Z.
    
    ![Set intitial keyframe on cube](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ab02527-186a-413c-8310-3194b091a310/set_start_keyframe_cube.png "Set intitial keyframe")
4.  Move the playback head to the end of the shot by clicking the **To End** button.
    
    ![Move playback head to end](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de78a570-6bc3-403a-a291-d70d8af52d5c/move_playback_head_to_end.png "Move playback head to end")
5.  Toggle the automatic keyframe creation feature by enabling the [**Auto-Key**](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine) button in the Toolbar.
    
    ![Enable Auto-Key](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3dfb206-02a4-4b92-9d35-f74a6ae817bd/enable_auto-key.png "Enable Auto-Key")
    
    The magnet icon turns blue when enabled.
    
6.  Move the cube to the other side of the scene to these Location coordinates: X: 1050, Y: 3200, and Z: 280. At this point, you can scrub the playback head back and forth and see the cube move from the start to end point in your shot.
    
    ![Finished cube animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c83a984-d086-46ee-8eb6-eecc40c6db0d/finished_cube_animation.gif "Finished cube animation")
7.  If you need to adjust the animation, move the selected cube around on the end frame with the **Auto-Key** enabled. This updates the cube's Location keyframes automatically. Or, you can click the [**Curve Editor**](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine) and adjust the keyframe values as necessary by selecting the appropriate key and drag it up ordown to adjust its value or left-right to change what frame it starts or ends on.
    
    ![Curve Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0493d937-aca1-4926-8ea1-9f9bd2783cbf/curve_editor.png "Curve Editor")

## Add Cameras

Now you need to create some cameras to focus on the action of the cube.

1.  In Sequencer, click the **Create Camera button** (1) to create a camera. This action creates a camera called [**Cine Camera Actor**](/documentation/en-us/unreal-engine/actors-and-geometry-in-unreal-engine), creates and assigns this asset to its own Sequencer track, creates a [**Camera Cuts**](/documentation/en-us/unreal-engine/cinematic-camera-cut-track-in-unreal-engine) (2) track (more on this later), and changes your viewport to look through this newly created camera.
    
    ![Add first camera](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/732cfd97-5304-45c4-a384-5543eca376c8/add_first_camera.png "Add first camera")
    
    If you want to change back to the scene view in the Viewport, you can enable the **Cine Camera Actor** icon in its Sequencer track.
    
    ![Toggle camera cut views](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72b108df-c6b0-4219-9cf6-625ec9ba663e/toggle_camera_cut_views.png "Toggle camera cut view")
2.  While the camera is locked to the Viewport, you can [**pilot**](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#piloting) the camera. Ensure that your frame is set to 0000, then expand the tracks for **Location** and **Rotation** (found under Transform for the Cine Camera Actor track) and position the camera to these Transform values:
    -   **Location**:
        -   X: -520
        -   Y: 740
        -   Z: 890
    -   **Rotation**:
        -   Roll: 0
        -   Pitch: -25
        -   Yaw: 355
3.  Move the playback head to just before the cube leaves the camera's view (frame 0050). Now you are ready to make your first camera cut. [**Trim**](/documentation/en-us/unreal-engine/cinematic-animation-track-in-unreal-engine#trim,loop,andplayrate) the duration of the camera shot by grabbing and pulling the right end of the track until it reaches frame 0050. Hover your mouse over the end of the track until you see the edge turn blue and the cursor turn into a right-left arrow.
    
    ![Trim camera cut](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/552a4d64-00c6-4e85-851b-01e5f5eac14a/trim_camera_cut.gif "Trim camera cut")
4.  For a little more practice, create a second camera called Cine Camera Actor (2) by clicking the **Create Camera** button in **Sequencer**. From the Viewport, nothing changes, but a new camera asset and track have been added to Sequencer. The new camera has the same position as the first camera. Remembering that the creation of a new camera automatically puts you into camera pilot mode, move the new camera to look at the cube in an oncoming shot. Position your camera to these values:
    
    -   **Location**:
        -   X: 685
        -   Y: 2600
        -   Z: 640
    -   **Rotation**:
        -   Roll: 0
        -   Pitch: -25
        -   Yaw: -70
    
    ![Cine Camera Actor (2) position](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37d9ff31-4886-4ceb-b14e-aca0666a6a87/cine_camera_actor_2_position.png "Position second camera")
5.  In the **Camera Cuts** track, click the plus sign and select **New Binding > Cine Camera Actor (2)**. This adds the second camera track to the Camera Cuts track.
    
    ![Bind Cine Camera Actor (2)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d733f38-f071-4a37-80a8-0f8a45e0e046/new_camera_binding_camera.png "Bind second camera")
6.  If you slide the playback head around, you see the cube moving but the cuts between the cameras don't change. Keep in mind which camera is active. At this point, the second camera is active. To see the camera cuts, you need to disable the **Lock Viewport**.
    
    ![Disable camera view back to camera cut](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96b4892d-b2ed-4c6f-beb7-d324014591eb/disable_camera_view_back_to_camera_cut.png "Disable camera view")
7.  For the third and final camera, create a camera that follows the cube to its final position. Move the playback head to frame 0079 (the cube should be nearly touching the bottom-right edge of the Viewport). Crop the camera cut of Cine Camera Actor (2) to end on this frame. Once you complete this step, the camera seems to jump out of its position. This is expected as the camera cut ends at this frame and the playback head is at this same position. If you double-click this camera, the camera cut fills Sequencer's track view (zooms in and focuses on the camera cut). If you hover the camera cut for a second, UE tells you the name of the camera (Cine Camera Actor (2)), start and end frames (50-79), and frame duration (29 frames).
    
    ![Cut camera duration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/588aa0fe-f1eb-4e9c-bcf1-f5429aa7714b/cut_camera_duration.png "Cut camera duration")
8.  Double-click the Sequencer Slider to zoom out to see all the camera cuts you have created so far and the remaining frames.
    
    ![Sequencer slider](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b11a89c-03a7-4cf7-a990-d24534aa5e71/sequencer_slider.png "Sequencer slider")
9.  Click **Create Camera** to add a third camera. This camera's purpose is to follow the cube until it reaches its final resting position.
10.  Position the camera to focus on the end point of the cube animation. Use these **Transform** values and set a keyframe for them on frame 0079:
    
    -   **Location**:
        -   X: -920
        -   Y: 1835
        -   Z: 1410
    -   **Rotation**:
        -   Roll: 0
        -   Pitch: -30
        -   Yaw: 21
    
    ![Cine Camera Actor (3) first position](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bf16284-9083-44ca-a346-aff374d7b2c1/cine_camera_actor_3_first_position.png "Position third camera")
11.  Move the playback head to frame 0149 and set the **Transform** values for Cine Camera Actor (3) to the following values:
    -   **Location**:
        -   X: 157
        -   Y: 2733
        -   Z: 585
    -   **Rotation**:
        -   Roll: 0
        -   Pitch:-22
        -   Yaw: 25 If Auto-Key is still enabled, these keyframes are set automatically once you change the position of the camera.
12.  Move the playback head to frame 0079 and enable the Camera Cuts Lock Viewport. Select the **Camera Cuts** track in Sequencer, and add the third camera to this track: click the **Plus** icon, then select **New Binding > Cine Camera (3)**. This automatically adds the final camera cut at frame 0079 and ends at 0149.
13.  Move the playback head back to frame 0000 and click **Play**. Your animation and camera cuts are now complete.
    
    ![Finished camera cuts](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44f97fe3-6486-414b-96e1-71d1c51ec035/finished_camera_cuts.gif "Finished camera cuts")
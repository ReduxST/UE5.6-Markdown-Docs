# Face AR Sample

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/face-ar-sample-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/face-ar-sample-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:11

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f20dccc3-1215-4de1-9f7f-175820968323/facearsample.png "FaceARSample.png")

The **Face AR Sample** project showcases Apple's ARKit facial tracking capabilities within Unreal Engine. You can download the **Face AR Sample** project from the **Epic Games Launcher** under the **Learn** tab.

Unreal Engine supports Apple's ARKit face tracking system. Using a front-facing TrueDepth camera, this API enables the user to track the movements of their face and to use that movement in Unreal Engine. The tracking data can be used to drive digital characters, or can be repurposed in any way the user sees fit. Optionally, the Unreal Engine ARKit implementation enables you to send facial tracking data directly into the Engine via the [Live Link plugin](/documentation/en-us/unreal-engine/live-link-in-unreal-engine), including current facial expression and head rotation. In this way, users can utilize their phones as motion capture devices to puppeteer an on-screen character.

The **Face AR Sample** project is a fully functional sample; however, some setup and configuration information is provided to assist you in exploring the project. You should keep in mind that as Apple's ARKit and Epic's OpenXR support evolves, specific project implementation details may change.

For more information about face tracking with Apple's ARKit, please see Apple's official documentation: [Creating Face-Based AR Experiences](https://developer.apple.com/documentation/arkit/creating_face_based_ar_experiences)

Mobile facial animation capture system is only available on iOS devices with a front-facing TrueDepth camera, such as the iPhone X, iPhone XS, iPhone XS Max, iPhone XR, iPad Pro (11-inch), and the iPad Pro (12.9-inch, 3rd generation).

## Face AR Capture Overview

At a high level, the facial capture system with ARKit uses the Apple TrueDepth camera to track the motion of a user's face. In the process, it compares the pose of the face against 51 individual face poses. These poses are native to the Apple ARKit SDK, and each pose targets a specific portion of the face, such as the left eye, right eye, sides of the mouth, etc. As a given part of the user's face approaches the shape of a pose, the value of that pose blends between 0.0 and 1.0. For example, if the user closes their left eye, the LeftEyeBlink pose would blend from 0.0 to 1.0. As a user's face moves, all 51 poses are being evaluated by the SDK and assigned a value. The Unreal Engine ARKit integration captures the incoming values from the 51 blended face poses, feeding those into the Engine via the [Live Link plugin](/documentation/en-us/unreal-engine/live-link-in-unreal-engine). Those 51 pose values can then drive the motion of a real-time character's face. So, all that you really need to utilize face capture to animate a character's head is to ensure the character content is set up to use data from those 51 shapes. Because those shapes each feed back individual 0.0.to 1.0 values, they are perfect for driving the motion of a list of blend shapes on a character.

If the blend shapes created on the Unreal character are named precisely the same as those in the official list of shapes from Apple, then the connection is automatic. However, if the shape names differ between the Apple mesh and the Unreal character, then a remapping Asset must be used. For more details on remapping blend shape names, see the [Remapping Curve Names in a LiveLinkRemap Asset](/documentation/en-us/unreal-engine/face-ar-sample-in-unreal-engine#remappingcurvenamesinalivelinkremapasset) section. 

For a complete list of the blend shapes brought in by Apple's ARKit, please refer to Apple's official documentation: [ARFaceAnchor.BlendShapeLocation](https://developer.apple.com/documentation/arkit/arfaceanchor/blendshapelocation)

## Face AR Capture Setup

Setting up a face capture system for animating a character's face with ARKit requires a few steps:

1.  Set Up Character Blend Shapes and Import the Character into Unreal Engine.
    1.  Create a character with blend shape based facial animation, accounting for the 51 blend shapes defined in [Apple's ARKit guidelines](https://developer.apple.com/documentation/arkit/arfaceanchor.blendshapelocation). Ideally, the geometry for these blend shapes should be named the same as the functions listed by Apple (*eyeBlinkLeft, eyeLookDownLeft*, etc.). However, there is a little leeway here as the names can be remapped if necessary.
        
    2.  Import this character into the Engine, making sure to import Blend Shapes in the import options.
        
2.  Enable face tracking in the *DefaultEngine.ini* file for your Project by adding the following lines to your *DefaultEngine.ini* file (the *DefaultEngine.ini* can be found in your Project's Config folder.)
    
    ```
        `[/Script/AppleARKit.AppleARKitSettings]     bEnableLiveLinkForFaceTracking=true`
    Copy full snippet
    ```
    \[/Script/AppleARKit.AppleARKitSettings\] bEnableLiveLinkForFaceTracking=true
3.  Create and apply a Data Asset in your Project to enable face tracking.
    1.  Right-click in the Content Browser and choose *Miscellaneous > Data Asset*.
        
    2.  From the **Pick Data Asset Class** window that appears, choose *ARSessionConfig* and click *Select*.
        
    3.  Double-click this new Asset to open it and set the set the following options:
        -   **World Alignment**: Camera
            
        -   **Session Type**: Face
            
        -   **Horizontal Plane Detection**: Off
            
        -   **Vertical Plane Detection**: Off
            
        -   **Enable Auto Focus**: Off
            
        -   **Light Estimation Mode**: Off
            
        -   **Enable Automatic Camera Overlay**: Off
            
        -   **Enable Automatic Camera Tracking**: Off
            
        -   **Candidate Images**: Ignore
            
        -   **Max Num Simultaneous Images Tracked**: 1
            
        -   **Environment Capture Probe Type**: None
            
        -   **World Map Data**: Ignore
            
        -   **Candidate Objects**: Ignore
            
    4.  In the Level Blueprint for your face tracking level, from Begin Play, call the *Start AR Session* function, and set the Session Config property to the ARSessionConfig data Asset you just created.
4.  Create an Animation Blueprint that uses a LiveLinkPose node, with Subject Name set to *iPhoneXFaceAR*. This will feed the ARKit face values into the Unreal Engine animation system, which will in turn drive the blend shapes on your character.

## The AR Face Component

The ARKit face tracking system uses an internal face mesh that it wraps to the user's face and uses as a basis to mimic expressions. In Unreal Engine, this mesh is exposed by the *AppleARKitFaceMesh* component. This can be added to an existing Blueprint and set up to visualize what the ARKit SDK is seeing, and help you correlate that to how your character's face moves.

*AppleARKitFaceMesh* component properties:

| Name | Description |
| --- | --- |
| **Wants Collision** | If enabled, this adds collision geometry to the face mesh. This is very expensive in terms of performance, and should only be used in instances where your app needs to trace against the mesh. For example, if you need to stick something to the face, or get a location on the face. |
| **Auto Bind to Local Face Mesh** | If enabled, this will automatically bind this component to the local ARKit face geometry on the device. ARKit will then update this component on every tick and handle the loss of tracking. |
| **Transform Setting** | 
**Component Only:** Only uses the transforms of the component. Use this only if you are not planning on tracking the face.

**Component Location Tracked Rotation:** Uses the components location, but tracks rotation from the user's head rotation while using the app.

**Component with Tracked:** Concatenates the transforms of both the component and tracked data together.

**Tracking Only:** Ignores the transforms of the component, and only uses the tracked data.



 |
| **Flip Tracked Rotation** | If enabled, reverses the tracked rotation. Useful if you want a mirror image type of effect on your character. |
| **Face Material** | Applies a material to the face mesh of the AppleARKitFaceMesh component. By default, the AppleARKitFaceMesh component is not visible. We generally recommend you add an unlit wireframe material to this property to make the mesh easily visible, as was done in the **Face AR Sample** project, |
| **Live Link Subject Name** | Used as a unique identifier as part of the Live Link animation pipeline. |

## Driving Joints with Face Capture

Most character faces for games or real-time projects are not animated with blend shapes alone. Generally, there is also some sort of facial skeleton helping to control movement of facial parts. Although the Live Link implementation for face capture in ARKit can automatically drive facial blend shapes, with the help of a Pose Asset you can also drive facial joints.

It is important to note that bone setups are not required when using ARKit for facial animation. It is documented here in the event you either already have joints in your facial setup, or know that you will need them.

## Corrective Blend Shapes with Joints

In certain cases, such as when using joints animate a face, you may find that you will also need a blend shape that is triggered at the same time in order to make the motion look appropriate. Such blend shapes are often referred to as *corrective blend shapes*.

For example, look at this image where the Kite Boy's jaw is opening only with joint rotation, and how it is improved by layering a corrective blend shape on top of it.

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0436dd59-5693-4a40-820b-0257bb8d6479/kiteboy1.png "kiteboy1.png") | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d259f36-b59d-4b09-a07e-a6892daeb4c0/kiteboy2.png "kiteboy2.png") | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2fdf3ab6-8773-4be1-9e9b-b8dc2e6a57d3/kiteboy3.png "kiteboy3.png") |

On the left is the boy's mouth opening with joint rotation only. Notice that the lower part of the jaw looks too wide. The middle shows the jaw opening with joint rotation, but now with a corrective blend shape layered on it. The jaw is stretching properly and looks more natural. On the right is the corrective blend shape by itself, it contracts the mouth and chin to aid in the stretching process. The idea is that these two systems, joint rotation and corrective blend shapes, will always work together; never one without the other.

## More Corrective Blend Shapes

In the **Face AR Sample's** Animation Blueprint, you'll notice in the Animation Graph a section that is just adding on corrective blend shapes. This is for special correctives such as when the eye is looking in diagonal directions, such as both left and down. Such poses are generally handled by way of additional blend shapes not included in the original list provided with ARKit, and blending them on based on the value of standard shapes.

For example, if you have a special corrective blend shape for when the right eye is looking diagonally down and left, then you could use your Animation Blueprint to read the values of *eyeLookDownRight* and *eyeLookInRight*, and use that data to activate a completely separate blend shape. This can bee seen in the **Face AR Sample** AnimBP.

## Creating a Pose Asset for Facial Animation

To create the necessary Pose Asset to drive facial animation from ARKit data:

1.  Create an animation in your DCC app in which:
    1.  The first frame is the rest pose, keyframed with no changes.
        
    2.  For frames 2 and on, each frame should be a different keyframed skeletal pose that achieves the pose from Apple's ARKit list. For example, Frame 2 could be *eyeBlinkLeft*, Frame 3 could be *eyeLookDownLeft*, and so on.
        
    3.  You do not need to create every single pose requested by the ARKit list, only those that would require joints to move for your rig. For instance, in the case of our **Face AR Sample** file, *jawOpen* is handled by way of joint rotation. However, there is also a blend shape that squishes the face in a bit for a more natural look while the jaw is opening.
        
        You can see an example of what this animation will look like in the **Face AR Sample** project, with the animation Asset named *KiteBoyHead\_JointsAnim*.
        
2.  You must keep a list of what poses are in the animation, and the order in which they appear. We recommend that you do this in a spreadsheet, so you can easily paste the names into Unreal Engine later.
    
3.  Import your animation into the Unreal Engine, making sure it is associated with your character's skeleton.
    
4.  Right-click on the animation in the Unreal Engine and choose *Create > Create Pose Asset.*
    
5.  The Asset will have a list of poses for each frame of the animation. You can copy and paste a list of names straight from a spreadsheet to rename them.

Special thanks goes to the team at [3Lateral](http://www.3lateral.com/), who were a great help in setting up the rig for the Kite Boy's face.

## Remapping Curve Names in a LiveLinkRemap Asset

1.  In the My Blueprint panel's Function group, choose Override and select Get Remapped Curve Names.
    
2.  This opens up a function graph with inputs and outputs. The goal is to use this graph to change the incoming name from the expected list of names from Apple's SDK, to a name that corresponds to blend shape names on your character. For instance, if you had a character whose blend shapes were named appropriately, but had "Character\_" appended to them, you would use a graph like this:
    
    Click for full image.
    
    Notice that it takes the incoming name from the Apple SDK, appends "Character\_" to the front, and outputs the result.
    

## Handling Head Rotation

For some projects you may need access to rotation of the tracked face. In the Unreal Engine implementation of ARKit, we pass in the rotation data alongside the face shape values. Within the *KiteBlyHead\_JointsAndBlends\_Anim* Animation Blueprint, you will see a section where this data is broken out and applied to the joints of the neck and head via Modify Bone nodes, as shown here:

Click for full image.

The data is sent out by way of 3 curves: HeadYaw, HeadPitch, and HeadRoll.

## Deploying to iPhone X

The **Face AR Sample** project should be deployed to an iPhone X to fully explore its feature set. While there are deployment docs in place already, see [iOS Game Development](/documentation/en-us/unreal-engine/ios-ipados-and-tvos-support-for-unreal-engine), you may find it easier to use the Project Launcher to deploy the **Face AR Sample** project to your device.

1.  Open **Project Launcher** (use the small arrow to the right of the **Launch** button on the main toolbar).
    
2.  At the bottom of the window click the + button across from **Custom Launch Profiles** to create a new profile.
    
3.  Set the following settings:
    -   **Build Configuration:** Development
        
    -   **How would you like to Cook Content:** By the Book (also check iOS in the build list)
        
    -   **Cooked Maps**: FaceTrackingMap\_Simplified (we do not recommend deploying FaceTrackingMap2, as it is not optimized for mobile rendering)
        
    -   **How would you like to package the build:** Do not package
        
    -   **How would you like to deploy the build: Copy to Device:** All\_iOS\_On\_ (on Mac, you may see your specific device - choose it if you do)
        
4.  Click **Back** when finished.
    
5.  Plug in your device, making sure iTunes can see it.
    
6.  Click the **Launch This Profile** button for your new profile.

## Project Features

The **Face AR Sample** project should be deployed to an iPhone X in order to be explored properly. Once on devices, users can test out all of the features of the system, which include:

-   Calibration
    
-   Live Link Broadcasting
    
-   Show/Hide Debug and Stats Data
    
-   Mirroring Control
    

### Calibration

By default, the character's face may not seem to mimic your own. In many cases, there are slight discrepancies between expectations and the final pose, generally due to data interpretation from the SDK to the character. This is most easily seen as a slight parting of the Kite Boy's lips when the user is in a neutral pose with the mouth closed while using the app.

To counteract this problem the app has a calibration system. In the app, the calibration system can be opened by way of the settings button in the lower left corner, then entering Calibration Mode. The app will guide you through the process from there.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c05e2c9-04a5-4242-a48c-7af0c6068cb6/calibration.png "calibration.png")

In the Editor, the **Face AR Sample** project also has a calibration process.

1.  While Simulating in Editor, select the KiteBoy in the scene.
    
2.  You will see the *In Editor Calibration* event button in the **Details Panel**. Click the button to calibrate in the same manner as the app.
    

In both cases, the project is recording the current facial capture values received by the SDK, and scaling those to the new zero. The function to gather those values is in different locations depending on whether you are on device or within the editor (in the pawn within app, within the Kite Boy Blueprint in editor). Once gathered, the values are processed in the Animation Blueprint  using a Modify Curve node with its Apply Mode setting set to Remap Curve.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b4465d5-01e3-4382-809b-aef4091031f4/applycalibration.png "applycalibration.png")

### Live Link Broadcasting

Aside from just being used for amusement, the **Face AR Sample** showcases how the iPhone X and ARKit can be used as a powerful digital puppeteering and motion capture device. This is done somewhat outside of the standard Live Link workflow, but has been simplified on the app.

It is important that the device and the computer are on the same physical network—check the WiFi settings on your iPhone to make sure.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0495bb7-0bab-4d2a-8a43-7c7f33d47a00/livelinkconnection.png "livelinkconnection.png")

1.  Within the app, tap the **Settings** button.
    
2.  Tap the **Live LInk Connection** button,
    
3.  Enter your IP address into the provided line.
    
4.  Relax your face as shown in the image.
    
5.  Tap **Connect**.
    

You are given the option of saving your IP address. This will save your IP address between sessions. However, we intentionally do not save the state of the **Save IP Address** checkbox, so you must confirm the setting each time you relaunch the app.

### Show Flag Checkboxes

The **Face AR Sample** app includes a few checkboxes for features that can be turned on and off to display specific features.

-   Show Debug Mesh
    
-   Show Debug Values
    
-   Show Unit Stats
    

#### Show Debug Mesh

This checkbox shows and hides Apple's ARKit debug mesh. This is the mesh the SDK is using to track the motion of the user's face. Within the app, this is rendered with a very simple unlit wireframe material.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/918ebccc-29d7-4205-9d86-58270252c766/showdebugmesh.png)

If using the **Face AR Sample** app as a facial motion capture puppeteering device, it is recommended that you only show the Debug Mesh. This is faster, more performant, and has less of an impact on device thermals. This is important, as performance of the device diminishes if it overheats.

#### Show Debug Values

Show Debug Values give you direct visualization of the numeric float data being passed from ARKit into the Unreal Engine. These values are separate from any calibration offsets that are in place. Use the debug values to help diagnose discrepancies between the incoming ARKit data, and the expected result in your apps.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4184b8ba-6adf-4b6b-b4ba-6f2766152adb/showdebugvalues.png "showdebugvalues.png")

#### Show Unit Stats

Show Unit Stats is the same as typing `STAT UNIT` into the console within the app. This just opens up the standard unit stats in the Engine, so you can see performance numbers on the device.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51779456-6d9d-4f45-b5ae-3eeaf2af4c75/showunitstats.png "showunitstats.png")

### Help & About

The **Help & About** screen is an in-app overview of the **Face AR Sample**, similar to what you see on this page.

### Connecting the App to Your Computer

One of the more exciting features of the **Face AR Sample** project is that it can be used as a motion capture device on your computer. The app has been streamlined to make this process as painless as possible, but before you begin, verify that the device and your computer are on the same physical network.

It is important that the device and the computer are on the same physical network—check the WiFi settings on your iPhone to make sure.

1.  Launch the **Face AR Sample** project on your computer.
    
2.  Open the **FaceTrackingMap2** map in the editor and navigate to a viewing position directly in front of the character.
    
3.  Press **Simulate** in the Editor (located under the arrow next to the **Play in Editor** button).
    
4.  On your device, launch the **Face AR Sample** app.
    
5.  After a few seconds, the settings button appears in the lower left corner. Tap it.
    
6.  Choose **LiveLink Connection** from the **Settings** panel.
    
7.  Enter your computer's IP address into the provided line. 
    
8.  Tap **Connect**.
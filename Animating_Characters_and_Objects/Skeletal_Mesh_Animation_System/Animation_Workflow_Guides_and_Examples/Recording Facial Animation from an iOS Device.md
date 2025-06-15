# Recording Facial Animation from an iOS Device

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/recording-face-animation-on-ios-device-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/recording-face-animation-on-ios-device-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:02

---

Recent models of the Apple iPhone and iPad offer sophisticated facial recognition and motion tracking capabilities that distinguish the position, topology, and movements of over 50 specific muscles in a user's face. If your iOS device contains a depth camera and ARKit capabilities, you can use the free **Live Link Face** app from Epic Games to drive complex facial animations on 3D characters inside Unreal Engine, recording them live on your phone and in the engine.

This page explains how to use the Live Link Face app to apply live performances on to the face of a 3D character, and how to make the resulting facial capture system work in the context of a full-scale production shoot.

Live Link Face relies on the same ARKit features used by the **Face AR Sample** that you'll find on the **Learn** tab of the Epic Games Launcher. However, the Face AR Sample needs to be compiled for iOS, which requires a Mac and an Apple developer account. With the Live Link Face app, you can immediately get started applying facial animation to any properly set up character in any Unreal Engine Project.

**Prerequisites:**

-   The material on this page refers to several different tools and functional areas of Unreal Engine. You'll have best results if you're already familiar with the following material:
    -   [Live Link Plugin](/documentation/en-us/unreal-engine/live-link-in-unreal-engine)
    -   [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine)
    -   [Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine) and [Take Recorder](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine)
-   You'll need to have an iOS device that supports ARKit and depth API.

## Getting Started

Follow the instructions in this section to set up your Unreal Engine Project, connect the Live Link Face app, and apply the data being recorded by the app to a 3D character.

1.  Enable the following Plugins for your Project:
    
    -   **Live Link**
    -   **ARKit**
    -   **ARKit Face Support**
2.  You need to have a character set up with a set of blend shapes that match the facial blend shapes produced by ARKit's facial recognition. You'll typically need to do this in a third-party rigging and animation tool, such as Autodesk Maya, then import the character into Unreal Engine.
    
    For a list of the blend shapes your character will need to support, see [the Apple ARKit documentation](https://developer.apple.com/documentation/arkit/arfaceanchor/blendshapelocation).
    
    If you don't have a character of your own ready, you can use the boy that you'll find in the **Face AR Sample** on the **Learn** tab of the Epic Games Launcher.
    
    Your character's blend shapes don't have to use exactly the same names as the ARKit blend shapes. You can create a custom Blueprint function in a **LiveLinkRemap** Asset to translate the ARKit blend shape names into the ones used by your character. For instructions, see the [Face AR Sample documentation](/documentation/en-us/unreal-engine/face-ar-sample-in-unreal-engine). However, for best results, you should make sure that your character's facial blend shapes cover the same facial areas as the ARKit blend shapes.
    
3.  Set up your character in Unreal Engine with an animation Blueprint that includes a **Live Link Pose** node. For example, in the animation Blueprint for the boy in the Face AR Sample:
    
    ![Live Link Pose node in an Animation Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5bdb0c12-f737-423a-83fb-20ac2d879b0b/livelinkpose.png "Live Link Pose node in an Animation Blueprint")
    
    Later, you'll use this node to apply the animation data being sent from the phone to your character.
    
4.  Get the IP address of your computer. You'll need this to connect your Live Link Face app.
    
    You can typically find the IP address in your computer's control panel or settings. Alternatively, on most Windows platforms you can use the **ipconfig** command-line utility.
    
    -   If your computer is connected to the Internet, you may have both a local IP address that is visible only within your network and a public IP address that identifies you on the open Internet. If so, choose the local IP address. Local IP addresses typically start with either `10.` or `192.168.`.
    -   Your computer may also have multiple IP addresses configured for different adapters. For example, you may have a wired Ethernet adapter and a wireless adapter, each with its own address. Make sure you choose the IP address of whichever adapter your computer is using to connect to the same network as your device.
    
5.  Find the free **Live Link Face** app from Epic Games on the Apple App Store, and install it on your phone.
    
    ![Live Link Face icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cab7c1bf-0394-4784-8b9c-ead58fe7d080/faceapp-store-icon.png "Live Link Face icon")
6.  Connect your phone to the same wireless network as your computer, or use an Ethernet cable to connect the phone directly to the computer using a Lightning Ethernet adapter.
    
    Live Link requires a network data source, so it's not enough to connect the phone to your computer by USB.
    
7.  Run the Live Link Face app on the device. You'll start on the home screen, where you can initiate new recordings.
    
    Click for full image.
    
    When you first get started, you'll see the camera picture overlaid by the triangular mesh generated by the ARKit facial recognition system. You can disable the overlay to see just your face, as shown in the image above, by turning off the **Preview Mesh** setting. See the [Live Link Face App Controls](/documentation/en-us/unreal-engine/recording-face-animation-on-ios-device-in-unreal-engine#livelinkfaceappcontrols) section below.
    
8.  Tap the icon at the top left to open the app settings. At a minimum, you'll need to go into the **LiveLink** settings to be able to connect to your computer.
    
    Click for full image.
    
    On the LiveLink settings page, tap **Add Target** and enter your computer's IP address.
    
    If you need to broadcast your animations to multiple Unreal Editor instances, you can enter multiple IP addresses here. See also the [Working with Multiple Users](/documentation/en-us/unreal-engine/recording-face-animation-on-ios-device-in-unreal-engine#workingwithmultipleusers) section below.
    
    For details on all the other settings available for the Live Link Face app, see the sections below.
    
9.  In the Unreal Editor, open the **Live Link** panel by selecting **Window > Live Link** from the main menu. You should now see your device listed as a subject.
    
    ![Live Link subject](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f514ec8-4fb6-40ef-8692-816613a16713/livelinksubject.png "Live Link subject")
10.  In your character's animation graph, find the **Live Link Pose** node and set its subject to the one that represents your device.
    
    ![Live Link Pose node with subject](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67b65383-7be9-4abc-b3d2-154c9219b0b5/livelinkposewithsubject.png "Live Link Pose node with subject")
11.  **Compile** and **Save** the animation Blueprint.
    
12.  Select your character. In the **Details** panel, ensure that the **Update Animation in Editor** setting in the **Skeletal Mesh** category is enabled.
    
    ![Update Animation in Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ff2cb26-0f3e-40ca-93c1-fb0a10e57a91/updateineditor.png "Update Animation in Editor")
13.  Back in Live Link Face, point your phone's camera at your face until the app recognizes your face and begins tracking your facial movements.
    
    At this point, you should see the character in the Unreal Editor begin to move its face to match yours in real time.
    
14.  When you're ready to record a performance, tap the red **Record** button in the Live Link Face app. This begins recording the performance on the device, and also launches Take Recorder in the Unreal Editor to begin recording the animation data on the character in the engine.
    
    Tap the **Record** button again to stop the take.
    

## Setting Up Head Rotation

To apply head rotation to the Actor using data from the Live Link Face App, you first need to set up Blueprints in the Event Graph and Anim Graph to drive the joints in the head.

### Head Rotation Blueprint - Event Graph

This Blueprint is placed in the Event Graph of your character's Anim Blueprint. It takes in yaw, roll, and pitch data from your Live Link performance and applies it to the appropriate bones in your character's rig.

Click for full image.

1.  Right click in the Blueprint and add an **Event Blueprint Update Animation** node. This ensures the head position updates each frame there is movement.
2.  Next, in the My Blueprint panel create 3 float variables named **HeadRoll**, **HeadYaw**, and **HeadPitch**. Drag each into the Blueprint and choose the **Set** option from the menu.
3.  Drag off from the Event Blueprint Update Animation node and create an **Evaluate Live Link Frame** node. This will provide the data from the Live Link source that will be stored in your float variables.
4.  Using the **Subject** dropdown menu, choose the subject that represents your device.
5.  Open the **Role** dropdown menu and choose the **LiveLinkBasicRole**.
6.  Right click near Evaluate Live Link Frame and create three **Get Property Value** nodes. These will be used to get the yaw, roll, and pitch from the Live Link app. Using the **Property Name** box on each node, set one to **headYaw**, another to **headRoll**, and the last to **headPitch**.
7.  Connect the **Valid Frame** output of Evaluate Live Link Frame to the **Set** variables as seen in the image above.
8.  Finally, connect the **Value** outputs of each of the Get Property Value nodes to the float input on its corresponding Set variable node.

### Head Rotation Blueprint - Anim Graph

With the head and neck rotation data coming in from the app, it can now be applied to the character's rig in the Anim Graph:

Click for full image.

The section shown above is added to the end of the Anim Graph, right before the Output Pose node.

1.  Starting from **Output Pose**, drag off from the **Result** and create a **Component To Local** node.
2.  Next, you will need a **Transform (Modify) Bone** node for each head and neck bone in your character's skeleton that will be influenced by the rotation data. If you are using the Kite Boy from the Face AR Sample project, you will need two.
3.  For each node, click on it in the Blueprint and set the Bone to Modify setting in the Details panel to the correct bone name. For the Kite Boy, this is the **neckRoot** and **head**.
4.  Connect the output of the first node to the **Component Pose** input of the next, similar to what you see in the image above.
5.  In each of the Transform (Modify) Bone nodes, click on the dropdown for the **Translation Space** option and change it to **Bone Space**.
6.  In the Details panel for the Transform (Modify) Bone nodes, find the **Rotation** section and change the **Rotation Mode** to **Add to Existing**, and change the **Rotation Space** option to **Bone Space**.
7.  Now take the yaw, pitch, and roll data that you are gathering in the Event Graph and create a Rotator to update the rotation of the head and neck bones. Drag in a copy of each of your float variables created earlier and choose **Get** from the menu.
8.  For each variable, drag from the output and create a **Float x Float node**. Multiply the Pitch by 15 and the Yaw and the Roll by -15. The yaw, pitch, and roll multiplier may need to be adjusted to achieve the desired result. You may need to try positive and negative values to get the correct rotation.
9.  With the multipliers set up, it is time to create the rotator. Right click in the Blueprint panel and create a **Make Rotator** node.
10.  Connect the output from the yaw multiplier into the **X (Roll)** input on the Make Rotator.
11.  Connect the pitch multiplier to the **Z (Yaw)**.
12.  Finally, connect the roll multiplier to the Y (Pitch).
13.  Connect the output of Make Rotator to the Rotation input on each of the Transform (Modify) Bone nodes.
14.  Finish the sequence by creating a **Live Link Pose** node and setting **Live Link Subject Name** to your device. Drag off from the output and create a **Local to Component** node.
15.  Connect its output to the Component Pose input on the first of the Transform (Modify) Bone nodes.

The yaw, pitch, and roll connections may need to be adjusted to achieve the correct rotation. The best way to check your rotations is with a live test once the sequence is complete. Your character should move with you. If you tilt your head to the left, your character should do the same to their left.

Press Play in Editor and test your head rotation setup. Your character's head should now rotate to match what is being recorded by the Live Link app.

## Live Link Face App Controls

The home screen of the Live Link Face app offers the following controls.

Click for full image.

<table class="table" style="--columns-count: 2;"><tbody><tr><td>1</td><td>Opens the Settings dialog.</td></tr><tr><td>2</td><td><div><p>Toggles sending facial animation data to all LiveLink targets. When highlighted in green, the app is sending the animation data.</p><p>When live, also lists the current timecode value being read from the timecode source configured in the app settings.</p></div></td></tr><tr><td>3</td><td>Toggles video display and facial tracking on and off.</td></tr><tr><td>4</td><td>Starts and stops recording a new take.</td></tr><tr><td>5</td><td>Opens the list of takes previously recorded by the app.</td></tr><tr><td>6</td><td>Shows the current slate and take, and the LiveLink subject name. Tap to rename the current slate or change the take number.</td></tr><tr><td>7</td><td>When highlighted in green, indicates that the ARKit facial capture system is able to successfully detect a face in the current camera view.</td></tr></tbody></table>

## Live Link Face App Settings

Tap the icon at the top left of the home screen to enter the Settings page, where you can configure the behavior of the app.

| Setting | Description |
| --- | --- |
| LiveLink | Configures the app to connect to computers running Unreal Engine, so that it can send animation data and control recordings through Live Link. |
| Timecode | Configures the timecode source for the Live Link Face app. For details, see [Timecode Sources](/documentation/en-us/unreal-engine/recording-face-animation-on-ios-device-in-unreal-engine#timecodesources) below. |
| OSC | Configures connections between the Live Link Face app and external OSC controllers and devices. For details, see [Controlling Live Link Face through OSC](/documentation/en-us/unreal-engine/recording-face-animation-on-ios-device-in-unreal-engine#controllinglivelinkfacethroughosc) below. |
| Calibration | Opens the [Calibration](/documentation/en-us/unreal-engine/recording-face-animation-on-ios-device-in-unreal-engine#calibration) menu. |
| Stream Head Rotation | 
Determines whether the app sends head rotation (yaw/pitch/roll) data from ARKit through the Live Link connection.

This option can be useful if you set up your phone on a static tripod stand, and you want to use the Live Link Face app to drive the movements of a virtual head as you move your head up and down and side to side relative to the phone.

If you use the Live Link Face app in conjunction with a body motion capture setup, you probably will not need this setting. Instead, you would typically mount your device to your head using a custom helmet so that it is always directly in front of your face, and let the body motion capture system record the up and down and side-to-side movements of your head.



 |
| Preview mesh | Determines whether the home screen overlays the camera picture with the triangular mesh generated by the ARKit facial recognition system. |
| Record button | 

Determines whether the red Record button is visible on the home screen.

You may want to disable this option if you are toggling recordings from an external OSC device, to avoid the possibility of actors accidentally hitting the button on the phone.



 |
| Blendshape data | Determines whether the home screen shows the data values being produced by the ARKit facial recognition system for all facial blend shapes. This information is typically useful only for debugging purposes. |
| Take Recorder | Determines whether the home screen should show the current slate name and take number, or the filename that will be used for the current recording. |
| Overlay | 

Determines whether the main screen of the Live Link Face app remains visible at all times, or whether it fades out until you interact with the touchscreen.

Fading out the overlay may prevent actors being distracted by seeing the captured video during their performances.



 |
| Video Quality | Determines the quality of the JPEG compression used to encode the reference video. Higher quality produces sharper images, but takes correspondingly more storage space on your device. |
| Storage | Shows the amount of free space on your device, and the amount of space being used by Live Link Face. You can also use this screen to delete takes that you've recorded previously. |
| Reset | Allows you to reset the Live Link Face app to its factory settings, undoing any changes you made to the settings above since you installed the app. |
| About | Displays legal information about the app. |

## Raw Facial Recordings

Whenever you initiate a new recording from the Live Link Face app, the capture is recorded to the device in two files:

-   A `.mov` file that contains a reference video recorded by the camera.
    
    The video frames are compressed using the JPEG codec, but it is frame-accurate with no temporal compression. The file contains audio and timecode, and is intended to act as a reference for animators who may need to work with the animation performance after the recording.
    
-   A `.csv` file that contains the raw animation data captured by ARKit during the recording.
    
    You can export this .csv file from the iOS device and import it into Unreal Engine as if you had recorded it in Take Recorder. Read the sections below about how to extract a .csv recording from Live Link and use it to drive facial animation in Unreal Engine. The raw data in this file may also be useful for developers who want to build additional tools around the facial capture.
    

### Extracting .CSV Facial Recordings from an iOS Device

There are two methods for extracting raw Live Link facial recordings from an iOS device in the `.csv` format. The easiest method is to share the Takes from within the Live Link App itself, but you can also browse to the `.csv` files in the iOS Files App and transfer or share them manually.

#### Within the Live Link App

1.  Tap the **Take Browser** icon in the bottom-left corner of the main screen.
    
    ![Open Take Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b921fe5c-44c5-47ae-b041-167e66eb7a17/open-take-browser.png)
2.  Tap **Select** and then choose the **Takes** you want to extract from the device.
    
    ![Select Takes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45e64eac-b86f-4a03-98ab-a0cad367f7f8/select-takes.png)
3.  Hit the **Share** icon and use one of the built-in iOS share functions such as AirDrop or Mail.
    
    ![Share options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c34755da-e692-4236-890e-b4b2a93afc92/share-takes.png)

AirDrop is the most reliable option to share Live Link takes from the device. Extracting a large number of takes, or long takes, may cause issues with third party services like Google Drive. The iOS share functionality is frequently buggy with integrated non-Apple services.

#### iOS Files App

The iOS Files App provides several alternative ways to extract files from an iOS device. Read [Apple's documentation](https://support.apple.com/guide/iphone/transfer-files-iphone-computer-iphf2d851b9/ios) on transferring files between an iOS device and computer.

The Live Link App stores raw facial recordings in a folder called **Live Link Face** in the **Files** > **Browse** folder on your iOS device.

![Live Link App location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42c86dcc-874b-413a-83ee-b9e184c1e286/live-link-face.png)

Open **Live Link Face** > **takes**, then tap the folder of the take you want to share. The raw `.csv` file is found inside that folder.

Click for full image.

You can share the `.csv` file by tapping it and selecting one of the Share options in the context menu.

### Using .CSV Facial Recordings in Unreal Engine

This process requires all three Plugins listed in the [Getting Started](/documentation/en-us/unreal-engine/recording-face-animation-on-ios-device-in-unreal-engine#gettingstarted) section at the top of this document, plus the **LiveLinkFaceImporter** Beta Plugin.

1.  Go to **Edit** > **Plugins** to open the Plugins Browser. Search for **LiveLinkFaceImporter** and enable the plugin. Restart the Editor before you proceed.
    
    ![Enable Live Link Face Importer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6717e80e-9c7a-4803-85c0-5acb99005707/enable-live-link-face-import.png)
2.  Click **Import** in the **Content Browser** and import the Live Link `.csv` file you want to use.
    
    ![Import Live LInk CSV Take](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df0a671d-5637-47ac-b483-345bcf9a5675/import-csv-take.png)
3.  A new **Level Sequence** Asset is created in the Content Browser with the same name as the `.csv` file.
    
    ![Live Link Level Sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0db5b425-1871-4d70-bb41-81460f95553d/level-sequence.png)
4.  Double-click this asset to open the Level Sequence in **Sequencer**. If you click the dropdown caret next to the name of the Track you will see keyframe data from all the different facial blendshapes.
    
    Click for full image.
    

#### Applying the .CSV to a MetaHuman Character

To use the Level Sequence with a character, open it in Sequencer and then set it as a Subject wherever your Live Link source is configured. The Level Sequence should appear as an option. To play the animation on a MetaHuman, you can select the MetaHuman Blueprint and then configure the following settings in the **Live Link** section of the **Details Panel**.

![MetaHuman Blueprint Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/286be234-8af3-4d25-a2fb-8953f147cc11/metahuman-enable-arkit.png)

1.  Check the box to enable **Use ARKit Face**.
2.  In the **ARKit Face Subj** dropdown menu, select the subject that matches the `.csv` you imported.

These settings are also accessible from the Event Graph of the MetaHuman Blueprint.

Click for full image.

Now when you play the Level Sequence in Sequencer, the facial animation is bound to your MetaHuman character.

## Calibration

In order to improve facial tracking quality, you can calibrate the Live Link Face app to better respond to changes in your face by capturing an image of your neutral "rest" face pose.

To enable calibration, open the **Settings** icon in the top left when Live Link Face app is open, then tap on **Calibration**. You should now see the calibration menu where you can enable the feature by tapping the **Enable** button.

![face app calibrate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e03dee1-c0ca-4f6e-a72f-1c7a815ae169/enablecalibration.png)

You can optionally enable the **Countdown** property too, which enables a three-second timer when initiating the calibration image.

Now when you return to the main Live Link Face screen, a new **Calibrate (+)** button will appear at the bottom right of the screen. Tapping this will enable a special "calibration mode", which converts the **Record** button function into the calibration capture.

![face app calibration button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/595af2df-fc9c-4508-8d4b-8fb300b5c381/calibrationbutton.png)

To calibrate your face, tap the **Calibrate** button. Next, face towards your device camera, ensure your face is neutral and expressionless, and press the **Record** button. The calibration image will either be taken immediately, or a three-second countdown will occur before the image is captured, if **Countdown** was enabled from the calibration settings.

After the calibration image is captured, you can choose to either **Save** or **Discard** it to try again. If you save it, then tapping on the **Calibration** button again will display options to **Recalibrate** and capture a new image, or **Remove** the calibration.

## Recording Modes and Results

Anytime you initiate recording from the Live Link Face app on your device, or through the OSC interface of the Live Link Face app, your performance will be recorded to the phone as described in the previous section. You don't have to be connected to any instances of Unreal Engine to record in this way.

If you are connected through Live Link to any instances of Unreal Engine at the time you start recording from the Live Link Face app or through the OSC interface, you will *also* launch the Take Recorder on all connected instances of Unreal Engine. Your animation performances will be recorded both on your device and in the Take Recorder on your computer.

If you are connected through Live Link to one or more instances of Unreal Engine, and you initiate recording from the Take Recorder in the Unreal Editor interface *instead* of initiating the recording from your device or the OSC interface, your performance will *not* be saved to the device. It will only be recorded in the Take Recorder on your computer.

## Working with Multiple Users

In the context of more complex, real-world productions, you may have multiple operators working in Unreal Engine at the same time, using [Multi-User Editing](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine) to collaborate live in the same virtual world. In this case, we recommend that you configure the Live Link Face app to connect to *all* Unreal Engine instances run by all operators. The app will multicast the performance capture to all engine instances. This ensures that all operators see the incoming animation data in context with a minimum of latency.

## Timecode Sources

It's likely that in a real production Live Link Face will only be part of a much larger performance capture setup. You will likely need to record other things at the same time: audio, live video, other body capture data, camera tracking data, and so on. In order to be able to synchronize these separate recordings with perfect accuracy, you need to ensure that all recordings embed consistent timecode values.

Live Link Face offers three options for timecode sources, which you can configure in the Settings panel.

-   **System Timer**
    
    By default, Live Link Face bases its timecode values on the device's System Timer. This timer is based on the elapsed time since the last system reboot. This provides a base option that is accurate in itself, but it can be hard to link this timecode up with recordings made on other devices.
    
-   **NTP Server**
    
    One way to get consistent timecode based on the time of day is to rely on a server that provides time values through Network Time Protocol (NTP). If you choose this option, the default server is **time.apple.com**, which is the same server that Apple uses to synchronize the device's time of day. However, if you use a custom NTP server, as many productions do to synchronize timecode for devices on stage, you can enter the server name and IP address.
    
-   **Tentacle Sync**
    
    The Tentacle Sync is a third-party hardware device that allows devices to synchronize via Bluetooth to a master clock on stage. This is likely the most professional timecode option; high-end productions typically rely on a master clock for timecode synchronization during a shoot. For details, see [Tentacle Sync](https://tentaclesync.com/).
    

## Controlling Live Link Face through OSC

The Live Link Face app supports two-way communication through the [Open Sound Control (OSC)](https://en.wikipedia.org/wiki/Open_Sound_Control) protocol.

-   You can use OSC devices to control Live Link Face remotely. For example, you could use an external device to start the app recording remotely.
    
-   You can also configure Live Link Face to send notifications of its activity to other OSC devices. For example, you could trigger actions on other devices whenever the app begins a new recording.
    

To set up OSC, open the app settings:

-   In the **Listener** section, you'll see the current IP address of your device, and the port that the Live Link Face app is listening to for incoming OSC messages. You'll need to make your OSC remote control device send commands to this IP address and port.
    
-   If you want Live Link Face to send OSC commands to control another device, enter the IP address and port of that device in the **Target** section.
    

The Live Link Face app supports the following OSC commands:

| Command | Description |
| --- | --- |
| `/OSCSetSendTarget <IP:string> <port:int32>` | Sets the OSC send target to the given IP address and port. The app replies to the new OSC send target with the command `/OSCSetSendTargetConfirm`. |
| `/AddLiveLinkAddress <IP:string> <port:int32>` | Adds a new Live Link target for the app to broadcast blend shape data. |
| `/ClearAllLiveLinkAddresses` | Removes all Live Link targets. |
| `/LiveLinkSubject <name:string>` | Sets the Live Link subject name. |
| `/LiveLinkStreamStart` | Starts streaming data to all Live Link targets. |
| `/LiveLinkStreamStop` | Stops streaming data to Live Link targets. |
| `/BatteryQuery` | Requests the battery level of the device. The app replies to the OSC send target with `/Battery <level:float32>`. |
| `/ThermalsQuery` | Requests the thermal state of the device. The app replies to the OSC send target with `/Thermals <state:int32>`. |
| `/Slate <name:string>` | Sets the slate to the given name. |
| `/Take <number:int32>` | Sets the take number to the given value. |
| `/ARSessionStart` | Turns on video and AR tracking. The app replies to the OSC send target with `/ARSessionStartConfirm`. |
| `/ARSessionStop` | Turns off video and AR tracking. The app replies to the OSC send target with `/ARSessionStopConfirm`. |
| `/RecordStart <slate:string> <take:int32>` | Starts recording with the given slate and take number. The app replies to the OSC send target with `/RecordStartConfirm <timecode:string>`. Note that at this time the timecode is always `00:00:00.000`. |
| `/RecordStop` | Stops recording. The app replies to the OSC send target with `/RecordStopConfirm <timecode:string> <blendshapesCSV:string> <referenceMOV:string>`. You can use the two strings in the `/Transport` command below to copy data from the device. |
| `/Transport <IP:port:string> <path:string>` | Using a path returned by the `/RecordStopConfirm` command (above), requests the app to transport the contents of the file to the specified IP address and port. The app will open a TCP connection to that address and port. It first sends an `int32` that contains the total size of the file, in big-endian format. It then sends the contents of the file. |
| `/VideoDisplayOn` | Turns the display of the video on. |
| `/VideoDisplayOff` | Turns the display of the video off. Tracking and recording can and will still occur. |
| `/AppActivated` | The app sends this to the OSC send target when the it becomes active on the phone. That is, when it is first started, brought to foreground, and so on. |
| `/AppDeactivated` | The app sends this to the OSC send target when the it becomes inactive on the phone. That is, when it is killed, sent to background, and so on. |
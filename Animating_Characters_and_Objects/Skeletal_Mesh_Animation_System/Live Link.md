# Live Link

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/live-link-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/live-link-in-unreal-engine)  
**Processed:** 2025-06-14 16:33:57

---

The purpose of Live Link is to provide a common interface for streaming and consuming animation data from external sources (for example, DDC tools or Mocap Servers) into Unreal Engine. It is designed to be extensible through Unreal Plugins, allowing third parties to develop new features—hopefully with no need to make, then maintain Engine changes.

With DDC tools like Motionbuilder, Live Link provides a way for you to edit animations externally while seeing a preview of your work inside Unreal Engine in real-time. Motion Capture Systems can also use Live Link to stream data into the Engine that can be previewed in real-time.

## Live Link Client

The hub of Live Link is the **Live Link Client** that is created when the Live Link plugin is enabled inside a project. It has two main responsibilities:

1.  **Manage Sources**: These are the sources of data and mostly represent connections to other applications, either on the same machine or across the network, that provide data to Live Link.
2.  **Manage Subjects**: Subjects are individual streams of data within the client. One animating character would be a subject for instance.
    
    A subject is made up of the following data:
    
    1.  A name.
    2.  Static data that doesn't change (like the Skeleton for an animation role.).
    3.  One or more "frames" of data (like the bone transforms for the animation role).

The client is also responsible for building up the next frame of data to be used by the Engine. This can either be a straight copy of the latest received data or an interpolated frame created by buffering the incoming data and playing it back with a user-definable delay.

**Roles**

Live Link also uses a concept of **Roles** that define how incoming data should be used. This allows for the data to be more easily mapped to a target Actor within the Engine. Supported Roles include Cameras, Lights, Characters, Transforms, and a Basic role (for generic data).

**Sources**

Sources are how data gets into the Live Link client. Sources can be defined within plugins so that third parties can build their own without having to change Engine code. Sources are responsible for managing how they receive the animation data (over a network protocol for example, or reading from an API for a device connected to the machine itself). Each source is handed a reference to the client to allow it to pass data to it. Within the Live Link plugin, we have defined our own source (called the **Message Bus Source**) that reads data from an Unreal Message Bus connection. We have used this to build a Live Link plugin for Motionbuilder.

### UDP Messaging

When using the Live Link Message Bus Source, it uses UDP Messaging under the hood and (by default) will use the first Network Adapter it finds. If you have more than one Network Adapter in your machine, this may cause issues if you expect to receive data from a particular adapter. If you want to receive UDP data on a specific Network Adapter, you will need to modify your Project Settings by going to **Edit > Project Settings > UDP Messaging** and changing the **Unicast Endpoint**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e63feff0-024e-458f-8881-04faef37079c/udpmessaging.png)

For example, if you have two adapters:

-   Adapter A: XX.X.XXX.123
-   Adapter B: XXX.XXX.X.53

If you want to receive data from the Live Link Message Bus Source on Network Adapter B, you would need to set your Unicast Endpoint to: XXX.XXX.X.53:0

The ":0" specifies that all ports should be listed to.

UDP Messaging is not enabled by default in -game. You can enable it by adding `-messaging` in a packaged game (shipping target is not supported).

## Enabling Live Link

The Live Link plugin can be enabled by opening the Plugins window (**Edit > Plugins**), selecting the **Animation** category and selecting **Enabled** on the Live Link Plugin.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66503b0b-0ed0-425e-80fc-76566bebf6cc/step_02-1.png)

## Live Link Connection Window

Once enabled. the Live Link client can be accessed from the **Window** menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85f27b23-c4ea-4817-9150-e5ec0bb17a95/enablelink_1-1.png)

Upon selecting the Live Link option, the **Live Link Connection** window opens, where you can add Source Types and Subjects.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0670076b-ea66-41d0-8c84-7c9b003fdfbb/sourcesettings.png)

Above we can see the Live Link client with an open connection to an instance of Maya running our plugin (top left section). That instance is sending three subjects to the Editor: two Camera subjects (one named "EditorActiveCamera" and another named "camera1"), as well as a subject containing Transform data called "TestCube" (bottom left section).

**Adding a Source**

You can add sources through the **\+ Source** button and select the type of source you want to connect with Live Link.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77dcfb4c-a5b2-4bb7-b1d8-17dbd36f6f76/addsourcetype.png)

Your external application will need to be set up to push data to Unreal Engine through Live Link for it to be displayed as a source to connect to. See the [Live Link Plugin Development](/documentation/en-us/unreal-engine/live-link-plugin-development-in-unreal-engine) page for more information.

In addition to receiving data through a Message Bus Source, Live Link supports **Hand Tracking** sources for devices like Magic Leap, as well as the ability to create **Virtual Subjects** that allow you to combine multiple Subjects into one "Virtual Subject". For example, you could take the lower body from Character A and the upper body from Character B, then combine them into a new Subject. Or you could use the camera tracking data from one source and combine just the translation from another tracked object and drive it manually.

In the Sources panel, you can manage all your connected Sources. You can also delete a Source by clicking the **Trashcan** icon next to a Source.

You can also click the **Presets** button to save or load any previously saved presets.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e02677f3-f5b4-4770-a0f0-cb45c275eafd/saveaspreset.png)

Presets are saved as assets inside the **Content Browser** and enable you to quickly load up any previous configurations.

### Subject Panel

The **Subjects** panel of the Live Link Connection window indicates a connected source and the subjects that are being streamed in.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9dc1326-63f7-4f74-b1c0-379267193a5a/subjectsettings.png)

This panel indicates the name of each subject, their associated role, and a status indicator where a green light is displayed if you are receiving data. A yellow light is displayed if you are connected to the Source but you didn't recieve data in the specified amount of time (configurable in the Project Settings, the default is 0.5ms).

**Connection Settings**

Once you establish an active connection, the following settings can be used to define the parameters of the connection:

| Property | Description |
| --- | --- |
| Evaluation Mode | 
Determines how to create the frame snapshot.

-   **Engine Time**: The source will use the Engine's time to evaluate its subjects. This mode is most useful when smooth animation is desired.
-   **Latest**: The source will use the latest frame available to evaluate its subjects. This mode will not attempt any type of interpolation or time synchronization.
-   **Timecode**: The source will use the Engine's timecode to evaluate its subjects. This mode is most useful when sources need to be synchronized with multiple other external inputs (such as video or other time synchronizes sources).
    
    Do not use when the Engine is not set up with a Timecode provider.
    



 |
| Valid Engine Time | If the frame is older than ValidTIme, remove it from the buffer list (in seconds). |
| Engine Time Offset | When evaluating with time, how far back from current time should the buffer be read (in seconds). |
| Timecode Frame Rate | When evaluating with timecode, what is the expected frame rate of the timecode. |
| Valid Timecode Frame | If the frame timecode is older than ValidTimecodeFrame, remove it from the buffer list (in TimecodeFrameRate). |
| Timecode Frame Offset | When evaluating with timecode, how far back from the current timecode should the buffer be read (in TimecodeFramerRate). |
| Max Number of Frame to Buffered | Defines the maximum number of frames to keep in memory. |
| Source Debug Infos | A collection of debugging information passed through from the source. |

**Interpolation Settings**

After a Subject has been added, you can assign any **Pre Processors**, **Interpolation** methods, or **Translators** to the selected Subject.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f6167f7-c2e8-4363-b9e9-e5d7e057da65/livelinkconnected-1.png)

| Property | Description |
| --- | --- |
| Pre Processors | These are good for processing the incoming data before it is pushed to the Subjects for a given frame. One possible use case is the **Axis Switch**, that will switch any axis of an incoming transform with another axis. |
| Interpolation | Defines the type of interpolation method used for blending frames. |
| Translators | These enable you to transform data from one role to another. For example, if you wanted to translate data from a Skeleton to a Transform. This could be useful if you wanted to just get the location of the hips of a character. This will transform the data into the correct role. |

## Editor Integration

Currently, the Animation Editors have a built-in integration with Live Link. This is accessed in the **Preview Scene Settings** tab under the **Preview Controller** property.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1cc08a0a-d3ff-4c9f-bbe5-4ad3584d5db4/previewscenesettings-3.png)

When the Live Link plugin is enabled, the Preview Controller option can be changed to **Live Link Preview Controller**. Once selected, you can set the following options:

-   **Subject Name**: The name of the subject in Live Link you would like to apply to the Preview Mesh.
-   **Enable Camera Sync**: Enables syncing of the Unreal Editor camera with an external editor. Internally this looks at Live Link for a subject called **EditorActiveCamera**. Our internally developed Motionbuilder plugin supports this.
-   **Retarget Asset**: This specifies the Retarget Asset to apply to the Live Link data that will be applied to the Preview Mesh.

### Live Link Components

The **Live Link Controller** and **Live Link Skeletal Animation** components can be added to an Actor in order to drive its parameters with Live Link from a connected external source.

To use these components, click the **Add Component** button and use the Live Link Controller (or Live Link Skeletal Animation) component.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17073d9c-2410-4634-b229-c4a6b28d847c/addlivelinkcomponent.png)

For the Live Link Controller, in the **Details** panel, you can use the **Subject Representation** property and select from your connected Subjects. Based on the Subject, a role will automatically be assigned (you can change if needed). The **Component to Control** is what will actually be driven through Live Link. In the example below, we have a Cine Camera Actor with a Live Link Controller component that allows us to move the camera and change the Focal Length from MotionBuilder. We also use the Live Link Skeletal Animation component on a Skeletal Mesh and stream in animation data. To achieve this, the **Live Link Pose** node has been added to our Animation Blueprint and our Subject has been selected.

The Live Link Controller can control Animation, however, it is recommended that the Live Link Skeletal Animation component be used for Animation for best results.

### Live Link in Blueprint

You can also use Blueprint function calls to access Live Link data. Below, the **Evaluate Live Link Frame** function attempts to get a Live Link Frame from a specified subject using a given role (in the case below, the Subject "camera1" and the role of Camera is accessed).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff680975-8e7b-4705-aed3-4024d02b30f5/livelinkinblueprints.png)

We can then get frame data from the data result, and in this case, the transform information from our Subject. That information is then used to update the relative transform of a Cine Camera within our Blueprint.

## Animation Blueprints

Data from Live Link can be applied directly inside Animation Blueprints:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4192b813-5c9e-474c-a7d3-f09242ec81ee/animbplivelink.png)

This is achieved by creating a **Live Link Pose** node inside the AnimGraph of an Animation Blueprint. The node has 2 properties:

-   **Subject Name**: The name of the subject in live link to stream data from
-   **Retarget Asset**: The Retarget Asset to use to apply the data from Live Link to the Skeleton that the animation Blueprint uses.

The output of the Live Link Pose node is a normal pose like any other pose node in an Anim Blueprint, and therefore can be manipulated like other poses (fed into Modifier or Blend nodes for instance).

While you can drive animation without the Live Link Pose node in the Editor, if you want to drive animation at runtime, you will need the Live Link Pose node set up in your Animation Blueprint.

## Plugin Development

There are two paths for integrating with Live Link:

-   Building an Unreal Engine plugin that exposes a new Source to Live Link.

This is the recommended approach for anyone that already has their own streaming protocol.

-   Integrating a Message Bus endpoint in third-party software to allow it to act as a data transmitter for the built-in Message Bus Source.

This is the approach we have taken for our Motionbuilder plugin.

For more information, please see the [Live Link Plugin Development](/documentation/en-us/unreal-engine/live-link-plugin-development-in-unreal-engine) page.

## Motionbuilder Live Link Plugin

The Motionbuilder Plugin appears as a connection in Editor in a similar way to the standard Live Link connections. It also has a custom UI for managing streaming:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f62887ad-0216-4808-b812-86eba46e0d0e/motionbuilderlivelinkplugin.png)

Objects can be selected from the current scene and added to the streamed list (as shown above). From there, their names can be set in the **Subject Name** column and their **Stream Type** (Camera, Skeleton, for example) can be set. Streaming on the subject can also be enabled and disabled from here.

You can download the [Motionbuilder Live Link Plugin](https://github.com/ue4plugins/MobuLiveLink) binaries from the Unreal Engine 4 GitHub repository.

For a step-by-step guide on how to set up the Motionbuilder Live Link plugin, please see the [Connecting Unreal Engine to Motionbuilder with Live Link](/documentation/en-us/unreal-engine/live-link-stream-motionbuilder-to-unreal-engine) How-to guide.
# Camera Actors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/camera-actors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/camera-actors-in-unreal-engine)  
**Processed:** 2025-06-14 16:11:51

---

Any kind of experience you create in **Unreal Engine 5**, whether it is a game or something else, will need at least one Camera through which a user can view it. Unreal Engine contains different kinds of **Camera Actors** that you can use for this purpose.

The following types of Camera Actors are available in Unreal Engine:

-   **Camera Actor**, which is a generic type of camera that can be used as a stationary or mobile viewpoint.
    
-   **Cine Camera Actor**, which is a specialized type of camera used to create cinematics. Refer to the [Cine Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine) page to learn more.
    

In addition to Camera Actors, you can use the following types of Actors to work with cameras in Unreal Engine:

| Actor Type | Description | Further Reading |
| --- | --- | --- |
| Camera Blocking Volume | Prevents the camera from entering a specific volume. This is useful, for example, to prevent the camera from clipping through walls or other environments. |   |
| Camera Rig Crane | Emulates a boom arm or Camera Jib system, which is used to create Crane Shots. The crane can be pivoted along horizontal and vertical axes, and can be extended as needed. | [Camera Rigs](/documentation/en-us/unreal-engine/camera-jibs-and-dollies-in-unreal-engine) |
| Camera Rig Rail | Emulates a Camera Dolly system, which is used to create Tracking Shots. The rail's track length and curvature can be modified to suit the needs of your shot. | [Camera Rigs](/documentation/en-us/unreal-engine/camera-jibs-and-dollies-in-unreal-engine) |
| Level Sequence Actor | Acts as a container for the Level Sequence Asset. The Level Sequence Asset is located in the Content Browser and contains Sequencer's data. This includes tracks, cameras, keyframes, and animations. This is assigned to a Level Sequence Actor in order to bind its data to a Level. | [Sequencer Overview](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview) |

## Placing a Camera Actor

Camera Actors are placed from the [Place Actors panel](/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine). To add a Camera to your Level, find it in the **Place Actors** panel, then drag it and drop it into the Level Viewport.

## Previewing a Camera Actor

If you select a Camera Actor (or a Blueprint that contains a Camera component), a separate preview window will open within the Level viewport. This window shows what the currently selected Camera "sees".

The Preview window of a Camera Actor. Click the image for full size.
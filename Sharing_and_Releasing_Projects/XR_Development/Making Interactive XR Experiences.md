# Making Interactive XR Experiences

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/making-interactive-xr-experiences-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/making-interactive-xr-experiences-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:44

---

There are many different kinds of input for XR, such as hand tracking, motion controllers, and eye tracking. This page contains links to documentation about how to add input to your XR projects.

## Input in OpenXR for Head-Mounted Experiences

The OpenXR runtime uses interaction profiles to support various hardware controllers and provide action bindings for whichever controller is connected. This page explains the concepts of input and controller mapping emulation with OpenXR in Unreal Engine.

## Motion Controllers

Motion Controllers represent the controller or hands used for input with XR devices. Motion Controllers can be accessed through a Motion Controller Component, which is typically attached to your project's Pawn. The Motion Controller Component inherits from the Scene Component, which supports location-based behavior, and moves the Pawn it is attached to based on the tracking data from the hardware. This component provides the functionality to render the Motion Controller and to expose the controller for user interactions defined by the Pawn.

These pages show how to set up motion controllers in your project.

## Hand Tracking

The following sections explain how to get started with using hand tracking for input on each platform that supports it.

### Oculus Quest

Hand tracking on Oculus Quest is available through the **Oculus VR** plugin. Currently, you cannot use hand tracking with an OpenXR project. The APIs for hand tracking on Oculus Quest are provided through an Oculus-custom component. Refer to Oculus's [hand tracking documentation](https://developer.oculus.com/documentation/unreal/unreal-hand-tracking/) for more details on visualizing the user's hands and using them as input.

![Oculus Quest hand tracking](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0445b44-d61a-477d-a38f-25a6d31d933c/handtracking_smaller.gif)

## Training Streams

Watch these training streams to learn how to add input to your XR projects.

## Next Steps

After setting up input in your XR project, follow these guides to add more functionality to your project and to improve its performance.
# Camera Motion Blur with nDisplay

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/camera-motion-blur-with-ndisplay-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/camera-motion-blur-with-ndisplay-in-unreal-engine)  
**Processed:** 2025-06-14 16:12:02

---

Previously, motion blur was disabed because it interfered with the common case of filming a static environment. The exposed sensor of the physical camera naturally blurs the inner frustum as the camera moves. If motion blur were naively enabled in nDisplay, it would be incorrectly amplified in the final footage: the inner frustum would be rendered with blur due to the tracked camera motion, and the physical camera would capture a blurred exposure of the inner frustum.

However there are cases in which rendered motion blur on the LED wall is desired. For example:

-   When content displayed on the wall has animation, such as animated vehicles or characters in the virtual environment.
-   When shooting a *process shot*, where the virtual environment itself has motion relative to the actors and props on the set. A common example of a process shot is where actors are sitting in a car and the background appears to be moving. In this case, the blur must be rendered to the LED wall because the physical camera and prop vehicle do not have any gross translational movement.

nDisplay now provides a solution to render the inner frustum with motion blur by subtracting out any blur due to the tracked camera motion. For example, if there's a camera pan in a process shot, it should not create additional blur in the inner frustum even while the background appears to move quickly by.

![Virtual production stage showing camera motion blur](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30a75edc-6bbe-4244-89cc-a26b1e1c5d19/camera-blur-background.png) ![Close up showing camera blur effect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0143fe75-8122-4614-90da-c934915e4793/camera-blur-closeup.png)

A car process shot on the Unreal Engine 4.27 In-Camera VFX Test shoot.

## Process Shots: Move the Stage vs Move the World

There are two approaches you can take to prepare a scene for a process shot:

-   **Move the Stage**: Where the nDisplay Root Actor moves through the environment.
-   **Move the World**: Where the entire environment moves around the nDisplay Root Actor.

There are use cases for each approach. The best choice depends on your project's needs.

The nDisplay motion blur calculation was designed to handle both cases. Further testing of real-world scenes is needed to validate the accuracy of motion blur for the Move the Stage approach. We believe that the Move the World approach works reliably in all cases.

### Move the Stage

For this approach, the nDisplay Root Actor should be animated with a path representing the gross motion of the vehicle. This is easier to set up than the other approach since the environment can be used without any modifications to make it moveable.

There can be some drawbacks to this approach:

-   Each take must be carefully choreographed with the timing of the animation playback.
-   Unless it is possible for the motion path to be a closed loop animation, the playback will have a noticeable reset between the last and first frames.
-   The longer the take, the more environment content you'll need to create.
-   Due to the limits of the single-precision floating-point format, Unreal's rendering can become unstable if the gross translation of the camera is too far from the origin.

### Move the World

For this approach, you keep the virtual stage fixed in Unreal's world space and animate the environment to move around it. This might be the more flexible approach when you just need a generic visual motion outside of the vehicle.

Many tricks can be employed in this case, especially if the motion path of the vehicle is simple. For example, you can reuse blocks of the environment by moving them like a conveyor belt around the virtual stage, allowing for infinite playback and uninterrupted camera shoots.

If the vehicle path is more directed and the environment has been designed to be moveable, the animation of the vehicle could be created separately and then inverted onto a root transform that is the parent of the environment.

The drawbacks to this approach are that it requires custom scene setups and fully moveable dynamic content and lights.

## Limitations

There are fundamental limitations to capturing motion-blurred LED wall content in a physical camera.

For example, if the camera on a real moving vehicle was panning to track a fixed spot in the world, like a sign moving past the vehicle, in reality there would be no blur in the captured image. This is not possible to do on an LED stage since the exposure of a panning camera will blur the wall no matter what.
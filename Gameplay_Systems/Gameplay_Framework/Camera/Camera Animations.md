# Camera Animations

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/camera-animation-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/camera-animation-in-unreal-engine)  
**Processed:** 2025-06-14 16:11:53

---

Conceptually, a **CameraAnim** is simply an animation that can be layered onto the in-game camera. You can animate the camera position and rotation, FOV, and post process settings. A CameraAnim's position, rotation, and FOV changes are applied additively to the game camera. These keyframes are treated as "relative to initial", which means that only the delta from time 0.0 in the animation will be applied.

The CameraAnim's postprocess settings are applied in a blended/layered fashion, like other systems that can affect the scene's postprocessing. You can select which settings you would like to override in the temporary camera's properties and animate the settings via appropriate Matinee tracks. What you see in the preview window should closely match what you see when the animation is played. The temporary camera also has a PostProcessBlendWeight you can set or animate to control how strongly your settings affect the scene.

## Creating and Editing CameraAnims

There are a few ways to create a CameraAnim. The easiest is to create a blank one as you would any other asset via the **Content Browser**. You can also convert a camera track in another Matinee to a CameraAnim by choosing "Export to CameraAnim" in the **right-click** menu on the camera interp group. Since you can import camera keyframes into Matinee from tools like Maya, this provides a pipeline to import CameraAnims from external sources.

To edit a CameraAnim, simply **double-click** the asset in the **Content Browser** like you would any other asset. The CameraAnim editor is a slightly customized version of Matinee. When you edit a CameraAnim, a temporary camera is placed in the world that you can manipulate to create keys and use to preview your animation.

## Playing a CameraAnim

The **PlayerCameraManager** contains functions that allow you to control the application of CameraAnims to the game camera from either C++ code or Blueprint script. When you play a CameraAnim, a CameraAnimInst is created which contains the playback information for an active instance of the animation. You can use this object to stop the animation manually or modify its playback parameters.

Multiple CameraAnimInsts (up to 8 currently) can be active at once, all blending and contributing to the final camera settings.

## Play Spaces

A CameraAnim has the ability to play in any arbitrary space. The most common usage is for it to play in camera space. For example, if you make an animation that shakes left and right (Y axis) and play it in game, it will still appear to shake the camera left and right no matter which way the camera is pointing.

A less common but still useful case is playing a CameraAnim in world space. This can be useful for simulating something like a ship rocking side to side, where you want the motion of the camera to roll when looking forward, but pitch when looking off the side of the ship.

Finally, you have the ability to specify any arbitrary space. Using the boat example, you might do this if the boat you are walking on can move around and change the world-space axis of the rocking motion. Another use case is for directional camera "hits" based on shots or explosions. Imagine creating a single animation that pitches the camera quickly upward. If an explosion goes off near you, you could then define a transform using the direction vector to the center of the blast and play the CameraAnim in that space, resulting in your camera always rotating away from the blast.
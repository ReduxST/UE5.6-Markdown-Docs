# Panoramic Capture Tips and Tricks

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/panoramic-capture-tips-and-tricks-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/panoramic-capture-tips-and-tricks-for-unreal-engine)  
**Processed:** 2025-06-14 16:41:42

---

Epic Games no longer supports or maintains the Panoramic Capture Plugin, and it only exists as a reference if you want to create your own solution. The plugin may not work as-is.

In the following section, we will go over some of the most common errors and issues that you might run into when using the Panoramic Capture plugin, and how to go about solving or getting around them.

## Slow Capture Process

The default capture of a stereoscopic image is 6K, which takes a significant amount of resources. You can reduce the resource impact of the image capture by lowering the value specified for **SP.StepCaptureWidth**, thereby reducing the size of the image capture. In the **BP\_Capture** Blueprint, simply change the **SP.StepCaptureWidth** value from 6144 (6K) to 1024 (1K).

## Image Distortion

Due to the manner in which the stereo images are created, you will get some image distortion/pinching at the top and bottom of the image. You can see an example of what this distortion/pinching looks like in the following image.

Click for full image.

While you can not eliminate this distortion, there are a few things you can do to help minimize it. Below you will find a few tips on how to address this distortion/pinching issue.

-   You can add a small gradient that fades to black at the bottom and or top of the image to help hide this distortion/pinching issue like in the image below.
    
    Click for full image.
    
-   Be careful with objects that get too close to the camera, as this will cause divergence, which makes it hard for a user to focus on the 3D image. While in some cases image divergence will not be possible to avoid, thinking about your camera placement can help lessen the effect. The following video shows how you can have different levels divergence in your images.
    
    When the user looks up, they will have issues getting the top part of the image to be in focus due to how close the top of the hang glider was to the capture camera. However, when the user looks down, they will have no focus issues as the ground was far enough away from the camera to not cause divergence.
    

## Not all Effects Work

Effects that are created in screen space or effects that are camera facing will not work with the Panoramic Capture tool. This means that the following types of effects should be disabled so that your images do not have any errors in them.

-   Light Shafts
-   Screen-based Distortion effects
-   Camera Facing Meshes or Particles
-   Vignette

Please note that there could be other effects not listed here that also do not capture well. If you see any similar artifacts in your images, try disabling the effect and re-capturing the image to see if the artifact goes away.

In the following image, you can see what happens when you try to capture something that makes use of screen-based effects, or is camera facing. If you take a look at the highlighted areas of the image, you will notice what appears to be a hard line in the clouds that are off in the distance. This line is there because the capture tool works by capturing your scene in a series of zoomed-in images for both the horizontal and vertical axis. Because the effects that face the camera do not know that the camera has moved and do not update their orientation to reflect this, the result is artifacts like you see in the image.

Click for full image.
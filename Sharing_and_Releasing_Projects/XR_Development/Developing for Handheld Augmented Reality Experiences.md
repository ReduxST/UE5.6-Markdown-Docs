# Developing for Handheld Augmented Reality Experiences

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/developing-for-handheld-augmented-reality-experiences-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/developing-for-handheld-augmented-reality-experiences-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:19

---

Unreal Engine supports handheld AR development with a unified framework so your applications can target multiple mobile platforms with minimal platform checks. Handheld AR platforms provide a variety of features that you can use in your Unreal Engine projects, such as facial tracking, environment probes, and object occlusion.

Currently, you cannot use OpenXR to develop with handheld AR devices. To develop XR projects with OpenXR, refer to [Developing for Head-Mounted Experiences with OpenXR](/documentation/en-us/unreal-engine/developing-for-head-mounted-experiences-with-openxr-in-unreal-engine).

This page contains links to documentation on how to develop for handheld AR devices in Unreal Engine.

## Getting Started with Handheld AR

Unreal Engine includes a template project for handheld AR. This template provides a simple base for handheld augmented reality projects, which you can modify to suit your project's needs. These pages explain how to use the template and how to get started developing with handheld AR in Unreal Engine.

## Supported Platforms

These pages provide information on the platforms and mobile devices that support handheld augmented reality in Unreal Engine and how to deploy your applications to them.

## Handheld AR Features

The following is a list of handheld AR features you can add to your projects and whether they're supported on the platforms.

| Feature | Description | ARCore Support | ARKit Support |
| --- | --- | --- | --- |
| **Plane Detection** | You can detect vertical or horizontal planes in the real world. Once the planes are detected, you can then place virtual objects in that location so they can appear to be attached to the real-world object, such as on a table top. | Yes | Yes |
| **Object Occlusion** | Real-world objects can occlude your virtual objects, that is, your virtual objects appear to be rendered behind the real-world object. | Yes | Yes |
| **People Occlusion** | Similar to object occlusion, people can occlude virtual objects. | No | Yes |
| **Environment Probe** | You can estimate the intensity and direction of the real-world lighting. You can then apply this light estimation to your virtual objects to blend them with the real world. | Yes | Yes |
| **ARPins** | You can attach your virtual objects to real-world locations with ARPins. You can also save these ARPins to the cloud and share them with other devices so multiple users can view the same content in the same location. | Yes, locally and through the cloud with Cloud Anchors and Azure Spatial Anchors. | Yes, locally and through the cloud with Geo Anchors, Cloud Anchors, and Azure Spatial Anchors. |
| **Augmented Images** | You can provide reference images that your app can detect and augment. | Yes | Yes |
| **Facial Tracking** | You can detect feature points on the user's face for tracking and augmenting. | Yes | Yes, through either the ARKit API or the [Live Link Face app](/documentation/en-us/unreal-engine/recording-face-animation-on-ios-device-in-unreal-engine). |
| **Geotracking** | You can track specific geographic locations using the device's GPS and world tracking based on downloaded images. This feature is dependent on whether images have been collected for the area. | No | Yes, for more details, refer to [Apple's documentation](https://developer.apple.com/documentation/arkit/content_anchors/tracking_geographic_locations_in_ar). |
| **Camera Intrinsics** | You can retrieve information about the device's physical camera, such as focal length and image resolution. | Yes | Yes |
# Developing for ARKit

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/developing-for-arkit-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/developing-for-arkit-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:18

---

[ARKit](https://developer.apple.com/augmented-reality/) is a [handheld augmented reality](/documentation/en-us/unreal-engine/developing-for-handheld-augmented-reality-experiences-in-unreal-engine) platform from [Apple](https://www.apple.com) that is supported in Unreal Engine. This page describes how ARKit is supported in Unreal Engine, and how to set up your environment to develop with ARKit. Refer to [Supported XR Devices](/documentation/en-us/unreal-engine/supported-xr-devices-in-unreal-engine) for the full list of which devices and which SDK versions Unreal Engine supports.

## Developing with the ARKit APIs

To develop for ARKit in Unreal Engine you must set up the following:

-   Updated hardware and software. Refer to [iOS Development Requirements](/documentation/en-us/unreal-engine/ios-ipados-and-tvos-support-for-unreal-engine).
-   Xcode 12 or later installed.
-   iOS 14 or later installed
-   A supported, configured, and connected handheld iOS device with an A12 Bionic chip or greater.
-   **Apple ARKit** plugin enabled in your project.

Once you're set up for developing with ARKit, you can use the unique ARKit functionality to develop for your iOS devices. Refer to [Handheld AR Features](/documentation/en-us/unreal-engine/developing-for-handheld-augmented-reality-experiences-in-unreal-engine#handheldarfeatures) for what features are supported in Unreal Engine.

## Getting Started with Development

After setting up your project with the Apple ARKit plugin, follow these guides to get started developing for ARKit devices.

## Profiling

The following guides show how to profile your XR application and what to consider when you need to improve performance.

-   [XR Performance and Profiling in Unreal Engine](/documentation/en-us/unreal-engine/xr-performance-and-profiling-in-unreal-engine)
-   [Testing and Optimizing Your Content in Unreal Engine](/documentation/en-us/unreal-engine/testing-and-optimizing-your-content)
-   [Debugging iOS and tvOS Projects](/documentation/404)

## Known Limitations

The following are known limitations of features in ARKit:

-   Candidate images for image detection must have unique friendly names. If multiple candidate images share the same friendly name, only the image with the first instance of the friendly name will be recognized.
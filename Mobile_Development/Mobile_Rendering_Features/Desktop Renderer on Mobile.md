# Desktop Renderer on Mobile

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-desktop-renderer-on-mobile-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-desktop-renderer-on-mobile-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:24

---

Unreal Engine (UE) provides support for both the forward and deferred desktop renderers for iOS devices and Android devices using Vulkan. This uses the same rendering path as PC and console platforms.

The iOS implementation of the desktop renderer is considered Beta in terms of feature readiness. The Android Vulkan implementation is considered experimental.

## How to Enable the Desktop Renderer on Mobile

The sections below provide instructions on how to enable the desktop renderer on iOS and Android.

### iOS/tvOS/iPadOS

To enable the desktop renderer for iOS, follow these steps:

1.  Open your **Project Settings**.
    
2.  Navigate to **Platforms** \> **iOS** \> **Rendering**.
    
3.  Enable **Metal Desktop Renderer**.
    

### Android Vulkan

To enable the desktop renderer for Android Vulkan, follow these steps:

1.  Open your **Project Settings**.
    
2.  navigate to **Platforms** \> **Android** \> **Build**.
    
3.  Enable **Support Vulkan Desktop \[Experimental\]**.
    
4.  Set r.Android.DisableVulkanSupport\` to 0 to ensure that Android Vulkan is enabled.
    
5.  Set `r.Android.DisableVulkanSM5Support` to `0` to allow the use of Shader Model 5 (SM5).
    

### Finalize Settings and Configure Desktop Renderer

You must restart the Unreal Editor for your changes to take effect. You can then configure forward and deferred rendering features the same way you would in a desktop application.

## Device Compatibility

The desktop renderer is only available for mobile devices that can use shader model 5 (SM5).

## Benefits

The desktop renderer provides access to high-fidelity rendering consistent with desktops and game consoles.

## Drawbacks

The desktop renderer has a high resource cost compared with the mobile forward and mobile deferred shading paths, and most mobile hardware isn't set up in such a way to run it efficiently.

## When to Use the Desktop Renderer

The desktop renderer is considered beta on iOS and experimental on Android Vulkan. We do not recommend using it for shipped projects, but welcome any feedback if you decide to experiment with it.
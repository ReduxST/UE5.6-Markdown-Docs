# Developing for Oculus

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/developing-for-oculus-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/developing-for-oculus-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:22

---

The OculusVR plugin has been deprecated in Unreal Engine 5.1. You should use the OpenXR plugin instead.

[Oculus](https://www.oculus.com/) is a [head-mounted virtual reality](/documentation/en-us/unreal-engine/developing-for-head-mounted-experiences-with-openxr-in-unreal-engine) platform from [Meta](https://about.facebook.com/meta/) that is supported in Unreal Engine. This page describes how Oculus is supported in Unreal Engine, and how to set up your environment to develop with Oculus. Refer to [Supported XR Devices](/documentation/en-us/unreal-engine/supported-xr-devices-in-unreal-engine) for the full list of which Oculus devices Unreal Engine supports.

Currently, you can develop for Oculus devices with either the **OpenXR** plugin or the **Oculus VR** plugin:

-   When you develop with the OpenXR plugin, your application can run on any device that supports the OpenXR APIs.
    
-   When you develop with the Oculus VR plugin, your application can use Oculus-specific features that aren't currently included in the **Oculus OpenXR** extension plugin.
    

Refer to the [Developing with OpenXR APIs](/documentation/en-us/unreal-engine/developing-for-oculus-in-unreal-engine#developingwithopenxrapis) and [Developing with Oculus APIs](/documentation/en-us/unreal-engine/developing-for-oculus-in-unreal-engine#developingwithoculusapis) sections below for more details.

## Developing with OpenXR APIs

To develop for Oculus using OpenXR in Unreal Engine you must set up the following:

-   Updated hardware and software. Refer to [Oculus' System and Hardware Requirements](https://developer.oculus.com/documentation/mobilesdk/latest/concepts/mobile-reqs#mobile-reqs)
    
-   [Oculus app](https://www.oculus.com/setup/)
    
-   Oculus Runtime v33.0 or later
    
-   [OpenXR Runtime for Oculus](/documentation/en-us/unreal-engine/openxr-prerequisites-in-unreal-engine)
    
-   **OpenXR** plugin enabled in your project
    
-   (Oculus Quest only) **Oculus OpenXR** plugin enabled in your project
    

Once you're set up for developing with OpenXR, you can use the OpenXR APIs to develop for not only Oculus devices but any device that supports the OpenXR APIs. Refer to [Developing for Head-Mounted Experiences with OpenXR](/documentation/en-us/unreal-engine/developing-for-head-mounted-experiences-with-openxr-in-unreal-engine) for more details.

## Developing with Oculus APIs

To develop for Oculus using the Oculus-specific APIs in Unreal Engine you must set up the following:

-   Updated hardware and software. Refer to [Oculus' System and Hardware Requirements](https://developer.oculus.com/documentation/mobilesdk/latest/concepts/mobile-reqs#mobile-reqs)
    
-   [Oculus app](https://www.oculus.com/setup/)
    
-   Oculus Runtime v33.0 or later
    
-   **Oculus VR** plugin enabled in your project
    

Once you're set up for developing with the Oculus VR plugin, you can use Oculus-specific features that aren't available in the OpenXR APIs yet. The following features are currently available only in the Oculus VR plugin for Oculus devices:

-   [Hand tracking with Oculus Quest](/documentation/en-us/unreal-engine/making-interactive-xr-experiences-in-unreal-engine#oculusquest)
    
-   [Fixed Foveated Rendering](/documentation/en-us/unreal-engine/xr-performance-features-in-unreal-engine#variablerateshadingandfixedfoveatedrendering)
    

## Getting Started with Development

After setting up your project with the **OpenXR** or **Oculus VR** plugins, follow these guides to get started developing for Oculus devices.

## Auto Instancing on Oculus

A **draw call** is the RHI command to draw an object. **Auto-Instancing** is a feature that automatically combines multiple draw calls into one instanced draw call. An **instanced draw call** is a way for the graphics API to draw multiple instances of similar objects that have varying attributes. These can be any attributes that relate to the rendering of a mesh: position, orientation, color, and so on. This page contains more details about auto-instancing on Oculus Quest.

## Troubleshooting and Profiling

The following guides show how to profile your XR application and what to consider when you need to improve performance.

-   [XR Performance and Profiling in Unreal Engine](/documentation/en-us/unreal-engine/xr-performance-and-profiling-in-unreal-engine)
    
-   [Testing and Optimizing Your Content in Unreal Engine](/documentation/en-us/unreal-engine/testing-and-optimizing-your-content)
    
-   Oculus's page on [Optimization Tools](https://developer.oculus.com/documentation/unreal/ts-book-tools)
    

If you experience issues with your Oculus headset, visit the [Oculus Support Center](https://support.oculus.com/) for troubleshooting help.
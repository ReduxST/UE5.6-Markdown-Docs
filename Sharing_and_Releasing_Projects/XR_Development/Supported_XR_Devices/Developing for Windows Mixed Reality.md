# Developing for Windows Mixed Reality

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/develping-for-windows-mixed-reality-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/develping-for-windows-mixed-reality-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:39

---

[Windows Mixed Reality](https://www.microsoft.com/en-us/mixed-reality/windows-mixed-reality) is a [head-mounted virtual reality](/documentation/en-us/unreal-engine/developing-for-head-mounted-experiences-with-openxr-in-unreal-engine) platform from [Microsoft](https://www.microsoft.com) that is supported in Unreal Engine through the OpenXR APIs. This page describes how Windows Mixed Reality is supported in Unreal Engine, and how to set up your environment to develop with Windows Mixed Reality. Refer to [Supported XR Devices](/documentation/en-us/unreal-engine/supported-xr-devices-in-unreal-engine) for the full list of which devices Unreal Engine supports.

To develop Unreal Engine projects for Windows Mixed Reality VR devices you should use the **OpenXR** plugin and the **[Microsoft OpenXR](https://www.fab.com/listings/8c00dec5-60fa-4b23-b861-98ee885419ce)** plugin.

Refer to the [Developing with OpenXR APIs](/documentation/en-us/unreal-engine/develping-for-windows-mixed-reality-in-unreal-engine#developingwithopenxrapis) and [Developing with Windows Mixed Reality APIs](/documentation/en-us/unreal-engine/develping-for-windows-mixed-reality-in-unreal-engine#developingwithwindowsmixedrealityapis) sections below for more details.

## Developing with OpenXR APIs

To develop for Windows Mixed Reality VR devices using OpenXR in Unreal Engine you must set up the following:

-   Updated hardware and software. Refer to Microsoft's [Installation checklist](https://docs.microsoft.com/windows/mixed-reality/develop/install-the-tools).
-   [OpenXR Runtime for Windows Mixed Reality](/documentation/en-us/unreal-engine/openxr-prerequisites-in-unreal-engine).
-   **OpenXR** plugin enabled in your project.
-   [Microsoft OpenXR](https://www.fab.com/listings/8c00dec5-60fa-4b23-b861-98ee885419ce) plugin installed from [Fab](https://www.fab.com) and enabled.

Once you're set up for developing with OpenXR, you can use the OpenXR APIs to develop for not only Windows Mixed Reality VR devices but any device that supports the OpenXR APIs. Refer to [Developing for Head-Mounted Experiences with OpenXR](/documentation/en-us/unreal-engine/developing-for-head-mounted-experiences-with-openxr-in-unreal-engine) for more details.

## Developing with Windows Mixed Reality APIs

To develop for Windows Mixed Reality VR devices using Windows Mixed Reality APIs in Unreal Engine you must set up the following:

-   Updated hardware and software. Refer to Microsoft's [Installation checklist](https://docs.microsoft.com/windows/mixed-reality/develop/install-the-tools)
-   **Windows Mixed Reality** plugin enabled in your project.

Once you're set up for developing with the Windows Mixed Reality plugin, you can use the Windows Mixed Reality APIs to create experiences for your Windows Mixed Reality VR devices.

## Getting Started with Development

After setting up your project with the OpenXR or Windows Mixed Reality plugin, follow these guides to get started developing for XR.

## Profiling

The following guides show how to profile your XR application and what to consider when you need to improve performance.

-   [XR Performance and Profiling in Unreal Engine](/documentation/en-us/unreal-engine/xr-performance-and-profiling-in-unreal-engine)
-   [Testing and Optimizing Your Content in Unreal Engine](/documentation/en-us/unreal-engine/testing-and-optimizing-your-content)
-   Microsoft's documentation on [Profiling with Unreal Insights](https://docs.microsoft.com/windows/mixed-reality/develop/unreal/unreal-insights)
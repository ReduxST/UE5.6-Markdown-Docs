# Developing for SteamVR

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/developing-for-steamvr-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/developing-for-steamvr-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:24

---

The SteamVR plugin has been deprecated in Unreal Engine 5.1. You should use the OpenXR plugin instead.

[SteamVR](https://www.steamvr.com) is a [head-mounted virtual reality](/documentation/en-us/unreal-engine/developing-for-head-mounted-experiences-with-openxr-in-unreal-engine) platform from [Valve](https://www.valvesoftware.com) that is supported in Unreal Engine through the OpenXR APIs. This page describes how SteamVR is supported in Unreal Engine, and how to set up your environment to develop with SteamVR.

SteamVR supports Vive, Oculus, and Windows Mixed Reality headsets. Refer to [Supported XR Devices](/documentation/en-us/unreal-engine/supported-xr-devices-in-unreal-engine) for the full list of XR devices Unreal Engine supports.

Currently, you can develop for SteamVR with either the OpenXR plugin or the SteamVR plugin:

-   When you develop with the OpenXR plugin, your application can run on any device that supports the OpenXR APIs.
-   When you develop with the SteamVR plugin, your application can only run on devices that SteamVR supports. Some Unreal Engine features, such as [Live Link XR](/documentation/en-us/unreal-engine/livelinkxr-in-unreal-engine), require the SteamVR plugin to use.

Refer to the [Developing with OpenXR APIs](/documentation/en-us/unreal-engine/developing-for-steamvr-in-unreal-engine#developingwithopenxrapis) and [Developing with SteamVR APIs](/documentation/en-us/unreal-engine/developing-for-steamvr-in-unreal-engine#developingwithsteamvrapis) sections below for more details.

## Developing with OpenXR APIs

To develop with SteamVR using OpenXR in Unreal Engine you must set up the following:

-   Updated hardware and software. Refer to your device's system and hardware requirements.
-   SteamVR version 1.5.17 or later
-   [OpenXR Runtime for SteamVR](/documentation/en-us/unreal-engine/openxr-prerequisites-in-unreal-engine)
-   **OpenXR** plugin enabled in your project

Once you're set up for developing with OpenXR, you can use the OpenXR APIs to develop for not only devices that SteamVR supports but any device that supports the OpenXR APIs. Refer to [Developing for Head-Mounted Experiences with OpenXR](/documentation/en-us/unreal-engine/developing-for-head-mounted-experiences-with-openxr-in-unreal-engine) for more details.

## Developing with SteamVR APIs

To develop with the SteamVR plugin you must set up the following:

-   Updated hardware and software. Refer to your device's system and hardware requirements.
-   SteamVR version 1.5.17 or later
-   **SteamVR** plugin enabled in your project

Once you're set up for developing with the SteamVR plugin, you can use the SteamVR APIs to develop for SteamVR-supported devices.

## Getting Started with Development

After setting up your project with the OpenXR or SteamVR plugin, follow these guides to get started developing for XR.

## Troubleshooting and Profiling

The following guides show how to profile your XR application and what to consider when you need to improve performance.

-   [XR Performance and Profiling in Unreal Engine](/documentation/en-us/unreal-engine/xr-performance-and-profiling-in-unreal-engine)
-   [Testing and Optimizing Your Content in Unreal Engine](/documentation/en-us/unreal-engine/testing-and-optimizing-your-content)
-   [SteamVR Frame Timing](https://developer.valvesoftware.com/wiki/SteamVR/Frame_Timing)

If you experience issues with your headset, visit [SteamVR Support](https://support.steampowered.com/kb_article.php?ref=8566-SDZC-9326) or [HTC Vive Support](https://www.vive.com/us/support/) for troubleshooting help.
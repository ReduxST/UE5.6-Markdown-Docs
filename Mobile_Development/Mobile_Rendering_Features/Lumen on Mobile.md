# Lumen on Mobile

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-lumen-global-illumination-on-mobile-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-lumen-global-illumination-on-mobile-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:43

---

Experimental support for [Lumen](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) is available for Unreal Engine 5.4 and newer on high-end Android mobile devices. This page provides:

-   Compatibility information for Lumen on mobile devices and renderers.
    
-   Instructions for how to enable Lumen for mobile devices.
    
-   Limitations and known issues.
    

## Compatibility

Lumen is available for high-end devices compatible with Android Vulkan Shader Model 5 (SM5) running the desktop renderer. This includes support both with and without hardware ray tracing.

The desktop renderer for Android is not enabled by default when you create a new project. However, after you enable the desktop renderer, enabling Lumen for your project makes it available on devices using the following device profiles:

-   `Android_Vulkan_SM5`
    -   `Android_Adreno_Vulkan_SM5`
    -   `Android_Mali_Vulkan_SM5`
    -   `Android_Xclipse_Vulkan_SM5`

The following devices currently use the needed Vulkan SM5 device profiles:

-   Samsung Xclipse (9xx)
-   Adreno (7xx)
-   Mali (G7xx)

Lumen currently does not work on iOS/tvOS/iPadOS devices.

## How to Enable Lumen on Mobile Devices

To enable Lumen on mobile devices, follow these steps:

1.  Enable the desktop renderer and SM5 support for mobile. See the Desktop Renderer section in [Feature Levels and Rendering Modes](/documentation/en-us/unreal-engine/mobile-feature-levels-and-rendering-modes-in-unreal-engine) for detailed instructions.
    
2.  Enable Lumen as you would in a desktop application. See [Lumen Global Illumination](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) for detailed instructions.
    

This enables the `Android_Vulkan_SM5` device profiles, which automatically apply to the device types listed in the Compatibility section above. If your device falls under one of these profiles, you do not need to follow any additional steps after you enable Lumen. If you need to add support to a device or device family that doesn't normally have it enabled, see the sections below.

### Apply Existing Lumen-Compatible Profiles to a New Device

To use one of the existing profiles that supports the desktop renderer and Lumen, open your `DeviceProfiles.ini` file and add a `MatchProfile` line that specifies that devices meeting your criteria should use the SM5 profile of your choice. See the Compatibility section above for a list of the existing SM5 profiles.

The following example is the `MatchProfile` line that applies the `Android_Adreno_Vulkan_SM5` profile to Adreno 7xx devices.

Engine/Config/BaseDeviceProfiles.ini

```

`; Enable SM5 on Adreno 7xx when SM5 is enabled  +MatchProfile=(Profile="Android_Adreno_Vulkan_SM5",Match=((SourceType=SRC_GpuFamily,CompareType=CMP_Regex,MatchString="Adreno \\(TM\\) 7[0-9][0-9]"),(SourceType=SRC_AndroidVersion, CompareType=CMP_Regex,MatchString="([0-9]+).*"),(SourceType=SRC_PreviousRegexMatch,CompareType=CMP_GreaterEqual,MatchString="10"),(SourceType=SRC_SM5Available,CompareType=CMP_Equal,MatchString="true")))`

Copy full snippet
```
; Enable SM5 on Adreno 7xx when SM5 is enabled +MatchProfile=(Profile="Android\_Adreno\_Vulkan\_SM5",Match=((SourceType=SRC\_GpuFamily,CompareType=CMP\_Regex,MatchString="Adreno \\\\(TM\\\\) 7\[0-9\]\[0-9\]"),(SourceType=SRC\_AndroidVersion, CompareType=CMP\_Regex,MatchString="(\[0-9\]+).\*"),(SourceType=SRC\_PreviousRegexMatch,CompareType=CMP\_GreaterEqual,MatchString="10"),(SourceType=SRC\_SM5Available,CompareType=CMP\_Equal,MatchString="true")))

See [Customizing Android Device Profiles](/documentation/en-us/unreal-engine/customizing-device-profiles-and-scalability-in-unreal-engine-projects-for-android) for more information on matching device profiles.

### Create a New Lumen-Compatible Device Profile

You can create a new device profile that supports Lumen in your `DeviceProfiles.ini`.

In Android, this means you need to enable both Vulkan and SM5 support. While you can create a device profile from scratch, you can also extend the `Android_Vulkan_SM5` device profile by setting it as the `BaseProfileName` for a new profile.

The following is the `Android_Vulkan_SM5` device profile:

Engine/Config/BaseDeviceProfiles.ini

```
	`[Android_Vulkan_SM5 DeviceProfile] 	DeviceType=Android 	BaseProfileName=Android 	+CVars=sg.ViewDistanceQuality=2 	+CVars=sg.AntiAliasingQuality=1 	+CVars=sg.ShadowQuality=2 	+CVars=sg.GlobalIlluminationQuality=2 	+CVars=sg.ReflectionQuality=2 	+CVars=sg.PostProcessQuality=2 	+CVars=sg.TextureQuality=2 	+CVars=sg.EffectsQuality=2 	+CVars=sg.FoliageQuality=2 	+CVars=sg.ShadingQuality=2 	+CVars=sg.LandscapeQuality=2 	+CVars=r.BloomQuality=2 	+CVars=r.LightShaftQuality=1  	; Shadows 	+CVars=r.Shadow.MaxResolution=2048 	+CVars=r.Shadow.MaxCSMResolution=2048 	+CVars=r.Shadow.WholeSceneShadowCacheMb=40 	+CVars=r.Shadow.CachedShadowsCastFromMovablePrimitives=0 	+CVars=r.Shadow.MaxNumPointShadowCacheUpdatesPerFrame=1 	+CVars=r.Shadow.MaxNumSpotShadowCacheUpdatesPerFrame=1 	+CVars=r.Shadow.DistanceScale=1.0 	+CVars=r.Shadow.CSM.MaxCascades=2  	+CVars=r.ShadowQuality=2 	+CVars=r.Shadow.CSMShadowDistanceFadeoutMultiplier=2.5 	+CVars=r.SSS.Quality=0 	+CVars=r.SSS.Scale=0 	+CVars=r.SSR.Quality=0 	+CVars=r.Android.DisableVulkanSM5Support=0 	+CVars=r.Android.DisableVulkanSupport=0 	+CVars=r.DistanceFields=1 	+CVars=r.Vulkan.RayTracing.AllowCompaction=0 	+CVars=r.Vulkan.RayTracing.TLASPreferFastTraceTLAS=0 	+CVars=r.RayTracing.RequireSM6=0`
Copy full snippet
```
\[Android\_Vulkan\_SM5 DeviceProfile\] DeviceType=Android BaseProfileName=Android +CVars=sg.ViewDistanceQuality=2 +CVars=sg.AntiAliasingQuality=1 +CVars=sg.ShadowQuality=2 +CVars=sg.GlobalIlluminationQuality=2 +CVars=sg.ReflectionQuality=2 +CVars=sg.PostProcessQuality=2 +CVars=sg.TextureQuality=2 +CVars=sg.EffectsQuality=2 +CVars=sg.FoliageQuality=2 +CVars=sg.ShadingQuality=2 +CVars=sg.LandscapeQuality=2 +CVars=r.BloomQuality=2 +CVars=r.LightShaftQuality=1 ; Shadows +CVars=r.Shadow.MaxResolution=2048 +CVars=r.Shadow.MaxCSMResolution=2048 +CVars=r.Shadow.WholeSceneShadowCacheMb=40 +CVars=r.Shadow.CachedShadowsCastFromMovablePrimitives=0 +CVars=r.Shadow.MaxNumPointShadowCacheUpdatesPerFrame=1 +CVars=r.Shadow.MaxNumSpotShadowCacheUpdatesPerFrame=1 +CVars=r.Shadow.DistanceScale=1.0 +CVars=r.Shadow.CSM.MaxCascades=2 +CVars=r.ShadowQuality=2 +CVars=r.Shadow.CSMShadowDistanceFadeoutMultiplier=2.5 +CVars=r.SSS.Quality=0 +CVars=r.SSS.Scale=0 +CVars=r.SSR.Quality=0 +CVars=r.Android.DisableVulkanSM5Support=0 +CVars=r.Android.DisableVulkanSupport=0 +CVars=r.DistanceFields=1 +CVars=r.Vulkan.RayTracing.AllowCompaction=0 +CVars=r.Vulkan.RayTracing.TLASPreferFastTraceTLAS=0 +CVars=r.RayTracing.RequireSM6=0

The most important parameters from this profile are as follows:

-   `r.Android.DisableVulkanSupport`: Turning this setting off enables Vulkan support.
    
-   `r.Android.DisableVulkanSM5Support`: Turning this setting off enables Vulkan SM5 device profiles.
    
-   `r.DistanceFields`: Enables Distance Field Shadows, which are needed for software ray tracing in Lumen.
    
-   `r.RayTracing.RequireSM6`: Turning this setting off allows ray tracing on non-SM6 devices, which is needed for hardware ray tracing in Lumen.
    

For more information on how to configure device profiles, see [Customizing Android Device Profiles](/documentation/en-us/unreal-engine/customizing-device-profiles-and-scalability-in-unreal-engine-projects-for-android).

## Limitations and Known Issues

The desktop renderer on mobile devices incurs a significant performance cost compared to mobile forward or deferred rendering. Using Lumen as well compounds the performance cost further. Because this support is experimental, we do not recommend shipping projects with it yet, but if you want to test it and profile it in your project, we appreciate any feedback you provide!
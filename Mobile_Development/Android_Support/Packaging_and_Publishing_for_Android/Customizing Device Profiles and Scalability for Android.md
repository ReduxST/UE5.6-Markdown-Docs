# Customizing Device Profiles and Scalability for Android

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/customizing-device-profiles-and-scalability-in-unreal-engine-projects-for-android](https://dev.epicgames.com/documentation/en-us/unreal-engine/customizing-device-profiles-and-scalability-in-unreal-engine-projects-for-android)  
**Processed:** 2025-06-14 16:18:17

---

**Unreal Engine** uses **[device profiles](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-device-profiles-in-unreal-engine)** and **[scalability settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/scalability-in-unreal-engine)** to customize rendering settings on a per-hardware basis. Scalability settings define levels of quality for individual features like shadows, foliage, and mesh detail, condensing an array of different settings into one easily scaled value. Device profiles then map those settings to devices that are compatible with them.

**Android** has a large array of profiles matched to specific **GPU families**. This guide will explain the **device-matching rules**, how to edit them, and how you can work with scalability settings to create profiles that fit your game's specific needs.

## Configs and Order of Priority

**[Configs](https://dev.epicgames.com/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine)** in Unreal Engine are read from both your Engine's install directory and your project folder. The `Engine/Config` folder sets the base config settings for the Engine. After that, they override each other in the following order:

[![Order of Priority for Configs](https://dev.epicgames.com/community/api/documentation/image/d6479f53-2fa6-4771-b226-9b71bb48404c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d6479f53-2fa6-4771-b226-9b71bb48404c?resizing_type=fit)

1.  `Engine/Config/Base*.ini`
    
2.  `Project/Config/Base*.ini`
    
3.  `Engine/Config/Android/Android*.ini`
    
4.  `Project/Config/Android/Android*.ini`
    

As an example, the `AndroidDeviceProfiles.ini` file in `Engine/Config/Android` takes precedence over `BaseDeviceProfiles.ini` in both `Engine/Config` and `Project/Config`. The `AndroidDeviceProfiles.ini` in `Project/Config/Android` takes precedence over all of the above.

## Android Device Profiles

The standard Android device profiles are `Android_Low`, `Android_Mid`, and `Android_High`. The `Android_High` profile represents the full range of features that Unreal Engine supports on the highest-end Android devices, while `Android_Low` represents the minimum feature set for the lowest-end Android devices.

We also categorize more specific device profiles based on the GPU families supported by Unreal Engine, due to the fact that mobile devices with the same GPU typically have similar performance characteristics. These GPU-specific device profiles usually map one of the standard profiles (like `Android_High`) to specific devices, but occasionally they need to provide special case tweaks.

For example, the following device profiles are for **Adreno 5xx** devices in **Unreal Engine 4.24**:

C++

BaseDeviceProfiles.ini

`[Android_Adreno5xx DeviceProfile] 	DeviceType=Android 	BaseProfileName=Android_High 	+CVars=r.DisjointTimerQueries=1  	[Android_Adreno5xx_No_Vulkan DeviceProfile] 	DeviceType=Android 	BaseProfileName=Android_Adreno5xx; 	There are several issues (vulkan sub-passes, occlusion queries) on devices running Android 7 and earlier 	+CVars=r.Android.DisableVulkanSupport=1`

\[Android\_Adreno5xx DeviceProfile\] DeviceType=Android BaseProfileName=Android\_High +CVars=r.DisjointTimerQueries=1 \[Android\_Adreno5xx\_No\_Vulkan DeviceProfile\] DeviceType=Android BaseProfileName=Android\_Adreno5xx; There are several issues (vulkan sub-passes, occlusion queries) on devices running Android 7 and earlier +CVars=r.Android.DisableVulkanSupport=1

Copy full snippet(10 lines long)

The standard `Android_Adreno5xx` device profile inherits from `Android_High` for all of its base settings, with only one override for `rDisjointTimerQueries`. The `Android_Adreno5xx_No_Vulkan` profile then inherits from the standard `Android_Adreno5xx` profile, and provides another override disabling support for the **[Vulkan renderer](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-android-vulkan-mobile-renderer-in-unreal-engine)** due to issues on older Adreno5xx devices.

Depending on your game's content you may need to override existing profiles or provide new ones within your project's `AndroidDeviceProfiles.ini`. You can extend these GPU-specific profiles further to represent even more specific devices within these GPU families if need be, or you can re-write any previously defined profiles completely.

## Device Profile Matching Rules

When an Unreal Engine application launches, it loads information about the device that is running it. The application then iterates through a list of rules that identify devices based on these parameters. These can be found in `**BaseDeviceProfiles.ini**`, under the section `[/Script/AndroidDeviceProfileSelector.AndroidDeviceProfileMatchingRules]`. When the application finds a rule that matches the device information retrieved, it stops running through the list and uses that device profile.

The format for an entry in this list is as follows:

C++

`+MatchProfile=(Profile="Profile_Name", Match=( ( Rule 1 ), ( Rule 2 ), (...) )`

+MatchProfile=(Profile="Profile\_Name", Match=( ( Rule 1 ), ( Rule 2 ), (...) )

Copy full snippet(1 line long)

The rules themselves are string comparisons taking the following format:

C++

`SourceType=[source string], CompareType=[comparison type], MatchString=[string to compare the source string to]`

SourceType=\[source string\], CompareType=\[comparison type\], MatchString=\[string to compare the source string to\]

Copy full snippet(1 line long)

Depending on what value you supply to **SourceType**, it will output a **source string** that the system will then compare **MatchString** to.

The values that are valid for SourceType and their corresponding source string outputs are as follows:

| SourceType Value | Description | Example Output |
| --- | --- | --- |
| 
`SRC_DeviceModel`

 | 

The model number of the device.

 | 

"Nexus 6"

 |
| 

`SRC_DeviceMake`

 | 

The manufacturer of the device.

 | 

"NVidia"

 |
| 

`SRC_GPUFamily`

 | 

The GPU family of the GPU in this device.

 | 

"Adreno (TM) 320", "NVIDIA Tegra"

 |
| 

`SRC_GlVersion`

 | 

The OpenGL version this device is running.

 | 

OpenGL ES 3

 |
| 

`SRC_AndroidVersion`

 | 

The version of the Android operating system used by this device.

 | 

Any numeric value.

 |
| 

`SRC_VulkanAvailable`

 | 

Checks to see if the application was packaged with Vulkan enabled, and if the device supports the required version of Vulkan specified in your Project Settings.

 | 

`False` if Vulkan is not available, `true` if it is.

 |
| 

`SRC_VulkanVersion`

 | 

The version of Vulkan this device uses, if available.

 | 

Any numeric value.

 |
| 

`SRC_PreviousRegexMatch`

 | 

The value of a previous regex match within the same MatchProfile entry.

 | 

Any information previously output by a regex match.

 |

The comparison types available are as follows:

| Comparison Type | Description |
| --- | --- |
| 
`CMP_Regex`

 | 

Performs a comparison that uses regex operators in the MatchString.

 |
| 

`CMP_Equal`

 | 

Check that the values of the two strings are exactly the same.

 |
| 

`CMP_EqualIgnore`

 | 

As `CMP_Equal`, but ignores case-sensitivity.

 |
| 

`CMP_NotEqual`

 | 

Check that the values of the two strings are not the same.

 |
| 

`CMP_NotEqualIgnore`

 | 

As `CMP_NotEqual`, but ignores case-sensitivity.

 |
| 

`CMP_Less`

 | 

Checks to see if the numeric value of the source string is less than the MatchString.

 |
| 

`CMP_LessIgnore`

 | 

As `CMP_Less`, but ignores case-sensitivity.

 |
| 

`CMP_LessEqual`

 | 

As `CMP_Less`, but returns true if the source and MatchString are equal as well.

 |
| 

`CMP_LessEqualIgnore`

 | 

As `CMP_LessEqual`, but ignores case-sensitivity.

 |
| 

`CMP_Greater`

 | 

Checks to see if the numeric value of the source string is greater than the MatchString.

 |
| 

`CMP_GreaterIgnore`

 | 

As `CMP_Greater`, but ignores case-sensitivity.

 |
| 

`CMP_GreaterEqual`

 | 

As `CMP_Greater`, but returns true if the source and MatchString are equal as well.

 |
| 

`CMP_GreaterEqualIgnore`

 | 

As `CMP_GreaterEqual`, but ignores case-sensitivity.

 |

As an example, the following is an entry for Mali T8xx devices in 4.24:

C++

BaseDeviceProfiles.ini

`+MatchProfile=(Profile="Android_Mali_T8xx_No_Vulkan",Match=((SourceType=SRC_GpuFamily,CompareType=CMP_Regex,MatchString="^Mali\\-T8"),(SourceType=SRC_AndroidVersion, CompareType=CMP_Regex,MatchString="([0-9]+).*"),(SourceType=SRC_PreviousRegexMatch,CompareType=CMP_Less,MatchString="8")))`

+MatchProfile=(Profile="Android\_Mali\_T8xx\_No\_Vulkan",Match=((SourceType=SRC\_GpuFamily,CompareType=CMP\_Regex,MatchString="^Mali\\\\-T8"),(SourceType=SRC\_AndroidVersion, CompareType=CMP\_Regex,MatchString="(\[0-9\]+).\*"),(SourceType=SRC\_PreviousRegexMatch,CompareType=CMP\_Less,MatchString="8")))

Copy full snippet(1 line long)

This MatchProfile entry has three rules:

1.  There must be a regex match for the GPU family with the string "^Mali-T8".
    
2.  The Android version must have one or more digits, and the digits will be remembered until a non-digit is found.
    
3.  The Android version obtained from the second rule must be less than 8.
    

If all of these criteria are met, it will use the profile `Android_Mali_T8xx_No_Vulkan`.

The device profile rules are listed first by manufacturer, and then in ascending order from the lowest-end specifications to the highest. The standard Android profiles are listed as fallbacks in case none of the rules fit and the specific device cannot be identified.

If you add any rules to this list, make sure that you place them in the appropriate order relative to other devices within the same family.

## Enabling Vulkan

A special parameter called `VulkanAvailable` is used to discern whether or not a device can use the Android Vulkan renderer. It first checks to see if the game itself has Vulkan support enabled, then checks to see if the device has Vulkan drivers. If both of these conditions are met, then `VulkanAvailable` is considered `true`.

Devices that support Vulkan have profiles both with and without Vulkan enabled to account for projects that do not use Vulkan even though it is available on the target device. All profiles have a parameter called `r.Android.DisableVulkanSupport`, which by default is set to `1`. Vulkan-enabled device profiles override this parameter to `0`.

Enabling Vulkan is only recommended for devices running Android 9 or higher, as the earliest devices with Vulkan support had a number of bugs in their drivers.

## Scalability Settings

Unreal Engine's base Scalability Settings are defined in `Engine/Config/BaseScalability.ini`, which can be found in your engine install directory. The Scalability Settings for Android devices are defined in `Engine/Config/Android/AndroidScalability.ini`.

[![Unreal Engine's base Scalability location](https://dev.epicgames.com/community/api/documentation/image/744ca782-a59d-45d1-a3c4-596d6159aa55?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/744ca782-a59d-45d1-a3c4-596d6159aa55?resizing_type=fit)

### Understanding Scalability Values

Scalability settings take in broad sets of parameters and condense them under broad categories that can then be defined with simple values between 0 and 3. For example, this is the scalability mapping for ShadowQuality level 0 in `BaseScalability.ini`:

C++

BaseScalability.ini

```code
`[ShadowQuality@0] 	r.LightFunctionQuality=0 	r.ShadowQuality=0 	r.Shadow.CSM.MaxCascades=1 	r.Shadow.MaxResolution=512 	r.Shadow.MaxCSMResolution=512 	r.Shadow.RadiusThreshold=0.06 	r.Shadow.DistanceScale=0.6 	r.Shadow.CSM.TransitionScale=0 	r.Shadow.PreShadowResolutionFactor=0.5`

```

Expand codeCopy full snippet(15 lines long)

Each of the values listed represent highly specific features, and each of them has their own scale. For example, some work in terms of pixel resolution, some work in terms of a scale factor that multiplies a default value, and some are more arbitrary. These can be overwhelming to define on a per-feature basis, and they need to be tweaked in-between releases as hardware is frequently updated.

Therefore, we use ShadowQuality to condense a group of related settings under a single, human-readable value. The above entry defines how all of these values behave when `sg.ShadowQuality` is set to `0` in a config file. Similar entries exist for `ShadowQuality@1` through `3`.

The guidelines for these default scalability values are as follows:

| Scalability Value | Description |
| --- | --- |
| 
0

 | 

Low quality. The lowest settings that are compatible with the minimum range of hardware that Unreal Engine supports.

 |
| 

1

 | 

Medium quality. Settings that are comfortable on a broad range of hardware in-between the lowest-end and highest-end devices that Unreal Engine has been tested on.

 |
| 

2

 | 

High quality. Settings that are comfortable on most high-end hardware that Unreal Engine has been tested on.

 |
| 

3

 | 

Epic quality. The highest values possible for a given feature on the current version of Unreal Engine.

 |

### Overriding Scalability Settings

To override scalability settings, you can create an `AndroidScalability.ini` in your project's own Config directory. For example, if you have a project called AndroidQuickStart, you would place it in `AndroidQuickStart/Config/Android`.

[![Project's base Scalability location](https://dev.epicgames.com/community/api/documentation/image/9387dbd5-57cc-46b6-8ace-e16dfb888c9c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9387dbd5-57cc-46b6-8ace-e16dfb888c9c?resizing_type=fit)

Any scalability settings created in this file will take precedence over the settings defined in `Engine/Config/Android/AndroidScalability.ini`.

### Setting Scalability Values in Device Profiles

To refer to a scalability value in device profiles, use the prefix `sg.` followed by the name of the value you want to set. For example, if you wanted to set ShadowQuality to 1 in a device profile, you would use the following:

C++

`+CVars=sg.ShadowQuality = 1`

+CVars=sg.ShadowQuality = 1

Copy full snippet(1 line long)

Any settings that you list after this scalability value will take precedence over its original value. However, it is strongly recommended that you change scalability parameters inside your `*Scalability.ini` files and observe the scalability groups consistently instead changing small-scale parameters inside of device profiles. This ensures that **Preview Rendering Level** inside the Editor accurately applies mobile scalability values.

## Changing Scalability Settings at Runtime

The initial scalability settings selected by a device profile are simply the defaults, and scalability can easily be changed at runtime through a variety of methods.

### Using the Settings Menu in Unreal Editor

For testing purposes, you may change the scalability settings in your game inside **Unreal Editor** by clicking the **Settings** dropdown in the **toolbar** and navigating to **Engine Scalability Settings**.

[![Scalability Settings in Unreal Editor](https://dev.epicgames.com/community/api/documentation/image/66cff30f-9fec-4d4e-ab56-04e01980bbf8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/66cff30f-9fec-4d4e-ab56-04e01980bbf8?resizing_type=fit)

Click image for full size.

Any changes made in this menu are applied immediately.

### Changing Scalability Settings with Console Commands

You may also refer to any scalability setting as a **[console command](https://dev.epicgames.com/documentation/en-us/unreal-engine/console-variables-cplusplus-in-unreal-engine)**. For example, if you type `sg.FoliageQuality 2` inside the console and press Enter key, it will change the value of all the CVars under FoliageQuality accordingly.

[![Adjust Scalability Settings using Console Commands](https://dev.epicgames.com/community/api/documentation/image/66b6a792-53c1-476d-9214-e17bfafe8c69?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/66b6a792-53c1-476d-9214-e17bfafe8c69?resizing_type=fit)

The values in the Engine Scalability Settings menu will reflect this change.

[![Reflected Change in the Scalability Settings](https://dev.epicgames.com/community/api/documentation/image/316ef533-3ff3-402b-b667-68c8fb0c34d8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/316ef533-3ff3-402b-b667-68c8fb0c34d8?resizing_type=fit)

You may also output the current value of a scalability setting by typing in its name as a console command, with no numeric value. For example, if you type `sg.FoliageQuality` and press enter, the console will print both the current value of FoliageQuality and the last place where it was set.

[![Console Output of the current value of a Scalability Settings](https://dev.epicgames.com/community/api/documentation/image/c82ad027-d47e-4575-b45c-c8bce801dee0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c82ad027-d47e-4575-b45c-c8bce801dee0?resizing_type=fit)

### Changing Scalability Settings in Blueprint

While you can use console commands through Blueprint to change scalability settings, they are also accessible through dedicated functions as a part of **Game User Settings**, which you can get a reference to using the **Get Game User Settings** node.

[![Set Scalability using Blueprint Scripting](https://dev.epicgames.com/community/api/documentation/image/fb91abc9-f520-4f2c-8457-8efaa8881e5b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fb91abc9-f520-4f2c-8457-8efaa8881e5b?resizing_type=fit)

Click image for full size.

You can use this functionality together with **UMG** to build menus where your users can change these settings. This enables users to customize a game's graphics and performance as desired.

### Changing Scalability Settings in C++

In C++, Game User Settings can be accessed with the static function `UGameUserSettings::GetGameUserSettings`. You can then use its dedicated get and set functions to get and set the quality level on scalability settings.

C++

```code
`#include "MyActor.h" 	#include "GameUserSettings.h"  	void AMyActor::SampleScalabilityFunctions() 	{ 		//Getting a reference to the Game User Settings. 		UGameUserSettings* UserSettings = UGameUserSettings::GetGameUserSettings();  		//Getting the current Foliage Quality. 		Int32 FoliageQuality = UserSettings->GetFoliageQuality();`

```

Expand codeCopy full snippet(14 lines long)
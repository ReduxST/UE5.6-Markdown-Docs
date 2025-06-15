# Lyra Scalability and Device Profiles

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/scalability-and-device-profiles-in-lyra-sample-game-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/scalability-and-device-profiles-in-lyra-sample-game-for-unreal-engine)  
**Processed:** 2025-06-14 16:47:49

---

## Setting up Scalability and Device Profiles For A Project

Unreal Engine provides a wide variety of **Scalability** settings that can affect your project's performance and visual quality. Usually, the engine default settings will accommodate most of your needs, however, you may want to change these settings for better performance or higher quality. Projects can launch on multiple platforms, therefore the Scalability settings may require different values for different platforms. The behavior of Platforms such as the PC is open to encompass a wide range of different types of hardware, as a result, these settings may need to be adjusted by individual users to best match their particular system.

## Scalability and Device Settings Systems

To achieve your goals in Scalability, multiple engine systems can be used together to create project profile configurations that work across all platforms and users. Below, you will find an explanation of the different engine systems involved in this process.

## Console Variables

Most performance and quality settings are implemented in the engine as [Console Variables](/documentation/en-us/unreal-engine/console-variables-cplusplus-in-unreal-engine) (CVars). These are named variables that store numbers, strings, or enumeration values. Console variables have a default set in source code, which can then be overridden by game-specific config files or the other systems described below. Most variables can be set while the game is running or from the command line, which provides a preview of quality and performance settings before committing them to a value. You can add data-driven CVars to your project by clicking on the Toolbar and navigating to **Edit > Engine** **\>Data Driven Cvar > CVars Array** and clicking on the **Add**(**+**) button.

![project-settings-cvars](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/daaa3a61-a47d-4ea7-967e-d36122f3cbf2/projectsettings.png)

Pictured above are the Data Driven CVars Array located in the Project Settings.

## Device Profiles

The engine uses [Device Profiles](/documentation/en-us/unreal-engine/setting-up-device-profiles-in-unreal-engine) to define a hierarchy for different types of physical devices that may run your project. You can find these settings by navigating to the Toolbar and clicking on **Tools** >**Instrumentation >** **Platforms** > **Device Profiles**.

![platforms-device-profiles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/614ba3fd-d591-4633-86e7-8b275790cc5a/deviceprofiles.png)

As an example, in the default engine settings there is a base "Android" device profile that is used for every Android device.

![android-device-profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c37ac13b-edc9-4b9d-85d6-341f1c8ae359/androiddeviceprofile.png)

In the Device Profiles settings you can access Existing Device Profiles(1), additionally, you can edit your own Console Variables in the CVars column(2).

Below the base profile are multiple performance buckets such as "Android\_High", and specific CPU/GPU types below that profile. When the project is launched the engine uses a [customizable process](/documentation/en-us/unreal-engine/customizing-device-profiles-and-scalability-in-unreal-engine-projects-for-android) to determine which specific device profile to use, then applies the settings associated with that profile, starting from the top level such as "Android" and overriding it with any values set in the more specific profiles below it.

## Scalability Groups

The [scalability system](/documentation/en-us/unreal-engine/scalability-reference-for-unreal-engine) is used to define a related set of performance settings that can be selected at runtime. For example, the engine default **PostProcessQuality** group defines settings for **Motion Blur** and **Bloom** and is split into 4 levels ranging from Low to Epic as well as a Cinematic level for maximum quality. When the project or user chooses a specific scalability group quality level, it will apply all of the console variables in that quality level.

![engine-scalability-settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbe07717-d316-4d12-9daa-76b433af3328/enginescalabilitysettings.png)

Scalability groups apply their console variable settings before device profiles. Settings defined in specific device profiles will override those in scalability groups chosen by the user. This means that device profiles can specify a base scalability group console variable like `sg.PostProcessQuality` before overriding individual settings.

It is possible to create platform-specific scalability group settings by using the general platform config override system described below. However, it is not possible to set up different scalability groups for specific device profiles.

In general, scalability groups are useful on open platforms like PC because they allow users to take advantage of a varying range of PC hardware components.

## Game User Settings

The `UGameUserSettings` class stores all settings that an individual user can change from an options UI menu. The user's specified settings are stored in a GameUserSettings.ini file on the specific device that runs your project. On some platforms that restrict file access, platform-specific options need to be enabled to allow the game user settings to save and load properly. The default engine class stores the user's choice of quality for each scalability group in addition to specific settings such as window resolution. Many projects may want to use a game-specific subclass, which is done by creating a native subclass and then modifying the GameUserSettings Class Name. This can be done from the `DefaultEngine.ini` file, by navigating to the \[/Script/Engine.Engine\] section, or by navigating to **Edit** > **Project Settings** > **Engine** > **General Settings** > **Default Classes** > **Advanced** > **Game User Settings Class**.

![general-user-settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e152d87-e0d1-419d-894f-8d1e158a8b89/generalsettings.png)

In your game-specific settings class, you can add new settings or change how settings are applied at runtime. Default values for a specific game can be set in the game's `DefaultGameUserSettings.ini` file, which will be used for any new users. The Game User Settings are exposed to Blueprint and have useful functions that can be called from either a Blueprint-based settings UI or in source code.

For example, the `RunHardwareBenchmark` function runs an automated benchmark that detects the relative CPU and GPU speed of the local machine and uses the `Scalability.ini` settings starting with `PerfIndexThresholds` to estimate the best scalability group settings for a particular machine. `ApplyHardwareBenchmarkResults` can then be called to apply and save the settings.

## Texture Group Settings

When textures are created in the editor, they can be assigned to different groups such as "World" or "UI". These groups specify what [Texture Settings](/documentation/en-us/unreal-engine/texture-format-support-and-settings-in-unreal-engine) are applied at runtime. Each group has different settings for maximum size, mip levels, and texture group settings that can be customized for specific device profiles. Packaging takes these settings into account. You can set a lower maximum resolution for mobile builds and the install package will only include the mip levels that could be streamed on that device. Texture group settings do not use console variables directly because they cannot be modified at runtime.

## Setting Priority

Before settings are applied, they are loaded from config files. The core [Configuration File Hierarchy](/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine) is used to determine what settings will be applied. This priority matters for any settings loaded from config files that cannot be modified at runtime. For settings that use the Console Variable system and can be modified at runtime, they are applied in the following order with higher numbers overriding lower numbers. This order is defined in the `EConsoleVariableFlags` enum:

| **Priority Order** | **Flag** | **Description** |
| --- | --- | --- |
| 1 | SetByConstructor | The default value set in a console variable's constructor. |
| 2 | SetByScalability | Values set by scalability group quality levels. |
| 3 | SetByGameSetting | Low priority values set by the engine's GameUserSettings. |
| 4 | SetByProjectSetting | 
Sets the ProjectSettings from the `DefaultEngine.ini` file from sections such as \[/Script/Engine.RendererSettings\].

These settings are usually set by the Project Settings menu located in the editor.



 |
| 5 | SetBySystemSettingsIni | The \[ConsoleVariables\] and \[SystemSettings\] sections of `DefaultEngine.ini`. |
| 6 | SetByDeviceProfile | From device profiles, with the more specific profiles overriding generic ones. |
| 7 | SetByGameOverride | High priority values set by a game's GameUserSettings subclass, this should be used for settings that need to override device profiles. |
| 8 | SetByConsoleVariablesIni | The engine `ConsoleVariables.ini` file, mostly used for testing in development. |
| 9 | SetByCommandline | Used by some command line options. |
| 10 | SetByCode | Used by various debugging tools. |
| 11 | SetByConsole | The highest priority, set by typing "NameOfCVar Value" in the console of a running game |

![priority-call-order](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09582673-107e-4e4f-8e0a-2f48d2aaa24e/prioritysettings.png)

As an example the engine override process is demonstrated in this diagram that begins with the Scalability Group system. First, the engine checks the \[PostProcessing@2\] category (displayed as High in the UI) in the engine-provided `BaseScalability.ini` file which contains the Console Variables(CVar) for bloom.

Then, the engine will check to see if any of these settings have been overridden by the category \[PostProcessing@2\] in the game-specific `DefaultScalability.ini` file or platform-specific files like `WindowsScalability.ini`.

Next, the Engine checks CVars specified in the \[SystemSettings\] category beginning with the `BaseEngine.ini file`. Any overrides in `DefaultEngine.ini` or a platform-specific ini are applied as before.

The call order continues down into the Device Profiles system. First, the [Device Profile Matching Rules](/documentation/en-us/unreal-engine/customizing-device-profiles-and-scalability-in-unreal-engine-projects-for-android) are run to determine the lowest level device profile that should be applied (Android Galaxy in this case).

Next, it starts applying rules by first applying the highest level device profile (Android) that matches the device. It starts by checking the CVars in the engine-provided `BaseDeviceProfiles.ini`, then checks the game-specific `DefaultDeviceProfiles.ini` to see if any of the CVars have been overridden.

This process continues down the hierarchy and checks the AndroidMid and the Android Galaxy device profile settings in a similar process to the Android call described above. Once all device profiles have been applied, it would continue on to apply any overrides at higher priority levels described above.

# Setting Game-Specific Overrides

If you want to change a specific setting for your game, then you need to set up the configuration files. The settings are stored in several different locations, so this is a multi-step process that begins with finding the correct setting. In the examples below, we will demonstrate the process of starting with a general concept such as "bloom quality" to finding a specific setting like `r.BloomQuality`. You can find this setting from either an `.ini` file, the in-editor Console Variable list, or in the source code.

### Engine Configuration: BaseScalability.ini

Begin by navigating to your `Engine/Config` folder, and clicking on the `BaseScalability.ini` file. Once you have opened the file, you can look for the PostProcessQuality group section to find the variable `r.BloomQuality`.

```
	`[PostProcessQuality@0]  	r.MotionBlurQuality=0  	r.MotionBlur.HalfResGather=1  	r.AmbientOcclusionMipLevelFactor=1.0  	r.AmbientOcclusionMaxQuality=0  	r.AmbientOcclusionLevels=0  	r.AmbientOcclusionRadiusScale=1.2  	r.DepthOfFieldQuality=0  	r.RenderTargetPoolMin=300  	r.LensFlareQuality=0  	r.SceneColorFringeQuality=0  	r.EyeAdaptationQuality=2  	r.BloomQuality=4`
Copy full snippet
```
\[PostProcessQuality@0\] r.MotionBlurQuality=0 r.MotionBlur.HalfResGather=1 r.AmbientOcclusionMipLevelFactor=1.0 r.AmbientOcclusionMaxQuality=0 r.AmbientOcclusionLevels=0 r.AmbientOcclusionRadiusScale=1.2 r.DepthOfFieldQuality=0 r.RenderTargetPoolMin=300 r.LensFlareQuality=0 r.SceneColorFringeQuality=0 r.EyeAdaptationQuality=2 r.BloomQuality=4

### Device Profiles: Console Variables

Open the Device Profile editor by navigating to **Tools**\->**Platforms**\->**Device Profiles**. Once in the editor, locate the **Windows** profile, then in the **CVars** column, click the **Edit** icon next to Windows.

![device-profiles-edit-cvars](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7dd92d8a-d0d2-402e-bdb9-fe8b91b6cb81/deviceprofilescvaricon.png)

This opens a window with a categorized list of all Console Variables that can be set from Device Profiles:

![bloom-quality-variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf3f621e-d1a5-400f-9938-e3bc35c8d59c/bloomquality.png)

The Bloom Quality variable pictured in the image above is listed in the Rendering category.

### Editor Command Line

Open up a running game or editor window, hit the **tilde** key(**~**) to open the full console, then in the **Cmd** line text field, type in "Bloom". The autocomplete section will list all console variables that include "Bloom" and can be set at runtime, which includes `r.BloomQuality`.

![editor-command-line-bloom](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9db078a3-75ef-4a5e-ae21-15e41a6c828a/bloomquality2.png)

### Manually Searching

You can search all `.ini` files in the engine for a term like "bloom" using a code editor such as Visual Studio that supports a text search within the engine directories. Alternatively, you can search the Engine API code base for specific terms. Once you find your specified console variable or config setting, we recommend you search all engine `.ini` files for that setting so you know where it is set, then you can apply your game or platform-specific setting.

## Overriding Settings In Config Files

If you want a Console Variable setting to always be the same across all platforms and scalability groups, this can be done from the \[ConsoleVariables\] section of the `DefaultEngine.ini` file. As an example, we can override bloom quality in all cases by adding the following to the `DefaultEngine.ini` file.

```
	`[ConsoleVariables]  	r.BloomQuality=1`
Copy full snippet
```
\[ConsoleVariables\] r.BloomQuality=1

If the setting you are seeking is in the `BaseScalability.ini` or another config file, then you can override it by creating a new config file in your project. To do this, create or edit the file in your project's config directory that matches the same name as the engine, but instead use the Base to replace the Default. You can add or find a section with the same name as the variable in the Engine. For instance, to change the bloom quality for the Low quality post process scalability group, you can add this text to the `DefaultScalability.ini` file.

```
	`[PostProcessQuality@0]  	r.BloomQuality=1`
Copy full snippet
```
\[PostProcessQuality@0\] r.BloomQuality=1

If the engine sets a Console Variable in a platform-specific config file such as WindowsEngine.ini, then you can override this setting for a specific platform using the same platform-specific config files. Additionally, you can change any platform-specific settings that do not use the device profile or console variable system. To do this, make a new platform-specific config file that matches the same config in the engine. For example, to override the `Engine/Config/Windows/WindowsEngine.ini` file, You can make a new `ProjectName/Config/Windows/WindowsEngine.ini` file, and make the same type of changes described above.

For platforms such as consoles that use the top level Platforms directory in the engine, we recommend that you make a parallel directory in your project folder. You can create a `PlatformNameScalability.ini` file in the correct directory, and this will provide you with the ability to override scalability groups for specific platforms such as Android.

## Setting Up Device Profiles

To accomodate device-specific differences, you will need to set up your project-specific device profile hierarchies. The easiest way to do this is using the **Device Profile** editor found by navigating to **Tools** > **Platforms** > **Device Profiles**. Once you are in the editor, click the **Edit** icon next to the device profile you want to set values for:

![device-specific-profiles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec68992c-50ed-439d-b8db-c96b25e1ef23/setdeviceprofiles.png)

We recommend that you edit the highest-level profile that includes all devices you want to change. Then, edit the console variables list to add or remove settings for the profile you want to change:

![highest-profile-variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3d089ee-757a-4a19-bfb1-3bf63d98a8d6/cvarprofile.png)

This screen will not save your changes. Unlike other settings screens in the editor you will need to open the `DefaultDeviceProfiles.ini` file using the button at the top of the editor, then when you are finished editing, click **Save as Defaults** to write the changes out to your project's `DefaultDeviceProfiles.ini` file. If your editor is connected to source control you may need to click that same area to check out or add that file to source control. This editor save will only write the modified profiles, but you may want to manually fix the resulting .ini file to make it easier to read.

**Texture LODGroups** settings for specific platforms can be set from the Device Profiles window, by clicking the **Edit** icon in the TextureLODGroups column.

![texture-lod-groups](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/caf80669-7371-488a-9c0a-7a9369a503bc/texturelod.png)

If you have a lot of platforms that will run your project, then it may be easier to choose to override the engine defaults by adding a \[/Script/Engine.TextureLODSettings\] section to your `DefaultDeviceProfiles.ini`. You can also add additional device profiles by adding new `DeviceProfileNameAndTypes` entries to the \[DeviceProfiles\] section. Following these methods, your settings will now be working as you intend. However, because of the setting priority hierarchy described in the table above, the engine settings at a higher priority may conflict with Project-specific settings at a lower priority.

For example, if the engine sets a variable in the `DefaultDeviceProfiles.ini`, but you want to set it by scalability groups, then you will have to undo the engine's device profile setting.

## Undoing an Existing Engine Setting

In some cases, you need to undo the engine's default value for a setting because it causes a conflict with your desired setting. Usually, this behavior is because you want to move a setting to a different level in the setting priority list, or move things between scalability groups. As an example, we want to move Bloom Quality from the PostProcess Scalability bucket to the Effects bucket. This can be done by opening your `DefaultScalability.ini` file and adding lines similar to the examples below:

```
		`[PostProcessQuality@0]  		-r.BloomQuality=4  		[PostProcessQuality@1]  		-r.BloomQuality=4  		[PostProcessQuality@2]  		-r.BloomQuality=5  		[PostProcessQuality@3]  		-r.BloomQuality=5  		[PostProcessQuality@Cine]  		-r.BloomQuality=5  		[EffectsQuality@0]  		r.BloomQuality=2  		[EffectsQuality@1]  		r.BloomQuality=2  		[EffectsQuality@2]  		r.BloomQuality=2  		[EffectsQuality@3]  		r.BloomQuality=5  		[EffectsQuality@Cine]  		r.BloomQuality=5`
Copy full snippet
```
\[PostProcessQuality@0\] -r.BloomQuality=4 \[PostProcessQuality@1\] -r.BloomQuality=4 \[PostProcessQuality@2\] -r.BloomQuality=5 \[PostProcessQuality@3\] -r.BloomQuality=5 \[PostProcessQuality@Cine\] -r.BloomQuality=5 \[EffectsQuality@0\] r.BloomQuality=2 \[EffectsQuality@1\] r.BloomQuality=2 \[EffectsQuality@2\] r.BloomQuality=2 \[EffectsQuality@3\] r.BloomQuality=5 \[EffectsQuality@Cine\] r.BloomQuality=5

This uses an advanced configuration system syntax where you use a line starting with a '-' to cancel the engine change in one category (the line in the DefaultScalability needs to match the line in BaseScalability exactly other than the -), and then move it to a new category.

Overriding an Array such as the **CVars** array located in the `BaseDeviceProfiles.ini` file, can be accomplished using two different methods. If you use the **Device Profile** window in the editor and save your settings, then it will create a DefaultDeviceProfile with multiple `-CVars=` lines that will cancel each individual default element in the array.

If you want to wipe out an entire array set by the engine and replace it, you can use the line:

```
	`!Cvars=ClearArray`
Copy full snippet
```
!Cvars=ClearArray

then add new elements by using the line:

```
	`+CVars`
Copy full snippet
```
+CVars

Additionally, if the base array uses the `@Array=Key` syntax, then it is treated like a Map, and you can override lines using that key.

As an example, the lines below can be added to the `DefaultDeviceProfiles.ini` file to set the World Normal Map textures to automatically reduce to a dimension of 2048x2048 (if they are larger than that amount).

The line `@TextureLODGroups=Group` located in the `BaseDeviceProfiles.ini`, means you do not need to remove the old value with a `-` or a `!` preface :

```
	`[/Script/Engine.TextureLODSettings]  	+TextureLODGroups=(Group=TEXTUREGROUP_WorldNormalMap,MinLODSize=1,MaxLODSize=2048,LODBias=0,MinMagFilter=aniso,MipFilter=point,MipGenSettings=TMGS_SimpleAverage)`
Copy full snippet
```
\[/Script/Engine.TextureLODSettings\] +TextureLODGroups=(Group=TEXTUREGROUP\_WorldNormalMap,MinLODSize=1,MaxLODSize=2048,LODBias=0,MinMagFilter=aniso,MipFilter=point,MipGenSettings=TMGS\_SimpleAverage)

# Lyra Examples

The Lyra game sample serves as an example for how to combine these different features for your specific project. In the sections below you will observe how the different components come together.

## Scalability Groups

The `Lyra/Config/DefaultScalability.ini` file was created manually, by copying and renaming the `BaseScalability.ini` file located in the `Engine/Config` folder, then editing it to remove any redundant sections.

The file has two sets of changes that tweak how the scalability groups work:

-   The **Performance Thresholds** used by the automated benchmark tools have now been raised from the original engine defaults, as a result faster computers are required to reach High or Epic quality levels.
    
-   The `foliage.DensityScale` and `grass.DensityScale` **Console Variable** settings have been moved out of the FoliageQuality category and into the ViewDistanceQuality category.
    

This is done to make a simplified options menu UI because it is unnecessary to single out foliage quality for a specific game.

## Device Profiles

The `DefaultDeviceProfiles.ini` file was created using the Save To Defaults option in the **Device Profile** window located in the editor, then these values were manually edited to add additional profiles, and modified later using the Device Profile window to tweak individual settings.

It includes the following changes:

-   A default texture group override was added to define settings for a game-specific "UI With MIPs" category, which is named in the editor using the \[EnumRemap\] section in `DefaultEngine.ini`.
    
-   A new Mobile device profile was added to serve as a base profile for IOS and Android.
    
-   The new Mobile profile was defined with a new CVar setting and override texture groups to reduce the maximum Mip size on mobile devices to save on memory and download size. These sizes are applied at cooking time.
    
-   The IOS and Android device profiles were modified to set their base profile to the new Mobile profile.
    

## Platform Configuration Files

Platform configuration files provide an example to create files for your own project. Config files for public platforms are available in the `Default*.ini` file located in the Config folder. Supported platforms that require licensing from the platform holder, such as game consoles, are available in the `Lyra/Config/PlatformName/PlatformName*.ini` directory.

If you have a license for a non-public platform, you can contact your Epic partner. See [Epic Online Services](https://dev.epicgames.com/en-US/services) for additional information.

Lyra includes a custom configuration option that can be used to create distribution-specific variants of a game. For example, if your game is shipping on multiple Windows-based stores, you can create subfolders inside the Config/Custom folder that contains the .ini files that override the store-specific settings.

These `.ini` file overrides are enabled with the development command line option:

```
	`-CustomConfig=Directory`
Copy full snippet
```
\-CustomConfig=Directory

Alternatively, you can use the CustomConfig parameter located in a `Target.cs` file. Platform-specific custom config files can be added by creating files named using a file path similar to `Config/Custom/CustomConfigName/PlatformName/PlatformNameEngine.ini`.

## Game User Settings

For handling user specific device settings, Lyra uses the `ULyraSettingsLocal` class as a subclass of `UGameUserSettings`. Lyra uses the same settings UI to modify the local settings such as Volume and Graphics Quality which are only stored on the device, and the `ULyraSettingsShared` class to handle key bindings which can be written to cloud storage and used on multiple devices.

Refer to the [GameSettings plugin](/documentation/en-us/unreal-engine/lyra-sample-game-settings-in-unreal-engine) documentation for further information.
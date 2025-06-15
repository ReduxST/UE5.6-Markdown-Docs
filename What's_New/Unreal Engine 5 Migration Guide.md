# Unreal Engine 5 Migration Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-5-migration-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-5-migration-guide)  
**Processed:** 2025-06-14 16:56:15

---

This guide describes how to upgrade your Unreal Engine 4 projects to **Unreal Engine 5** (UE5).

**Unreal Engine 5** (UE5) introduces a series of changes, upgrades, and new features to the systems that made up Unreal Engine 4 (UE4). Although there have been significant changes to the engine, the built-in conversion process handles most of the work involved in migration without requiring any user action.

To begin, open UE5 from the Epic Games Launcher. If UE5 is already running, from the main menu, go to **File > Open Project** from the main menu. Then, select the project you want to upgrade and click **Open**.

Click the **Open a Copy** button to upgrade a separate copy of your project, leaving the original unchanged.

![Opening a project copy to upgrade it to UE5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/785f721d-3022-4f6d-9db8-db0c0cea6ae1/convert-project.png)

If you click **More Options** on this dialog, you can choose to either:

-   Skip the conversion, which attempts to open the project as-is.
-   Convert in-place, which attempts to convert the existing project rather than make a copy of it.

When you convert a project to UE5, we highly recommend using the **Open a Copy** workflow described above. The **Convert in-place** and **Skip conversion** options may not work as expected and may lead to data corruption and data loss.

Once you update a project to a newer version of Unreal Engine, you won't be able to open it in an older version. Attempting to do so will fail.

Once the conversion process is complete, most projects will be ready to build and run in UE5 without further action. However, certain new or upgraded features benefit from, or even require, some manual updates to operate properly in UE5 and take advantage of its full capabilities. Among the largest systemic changes are Nanite, Lumen, and Chaos. Nanite and Lumen will require some of work to get graphics-centric projects looking the same as they did in UE4, and heavily physics-based projects that have not already switched to Chaos will need some configuration and Asset modification.

This page covers mandatory updates and other noteworthy system changes, such as system deprecations and replacements. If you are using these features, you will need to perform the updates described in the **Mandatory Updates** section to bring your UE4 projects into UE5 successfully. Updates described in the **Other Changes** section may or may not impact your projects, but it is worth to keep them in mind.

## Version-Specific Conversion Notes

Refer to the table below to understand how your project will convert depending on the Unreal Engine version it was created with.

| **Project Created With Version** | **Conversion Notes** |
| --- | --- |
| Unreal Engine 4.0 to 4.26 | 
Your project will load in any version of Unreal Engine that is the same or newer than the version it was created with.

The Unreal Engine API has changed over time, which means some projects created with much older versions may not load correctly. For example, Blueprints saved all the way back in 4.0 might call functions that were deprecated in 4.10 and no longer exist in 5.0. However, the project should still load and let you fix up the references that were deprecated or removed.



 |
| Unreal Engine 4.27 | 

Your project will load in Unreal Engine 4.27, 5.0, and newer versions. Note that your project will **not** load in Unreal Engine 5.0 Early Access.

This was communicated as part of the Unreal Engine 5.0 Early Access [compatibility notes](https://docs.unrealengine.com/5.0/en-US/Welcome/#compatibility).



 |
| Unreal Engine 5.0 | Your project will load in Unreal Engine 5.0 and newer versions. |
| Unreal Engine 5.1 and newer versions | Your project will load in any version of Unreal Engine that is the same or newer than the version it was created with. |

### Asset Compatibility

Assets saved in an older version of Unreal Engine can be opened in a newer version. For example, if you save an Asset in Unreal Engine 4.26, you can open it with Unreal Engine 5.0.

Assets saved in a newer version of Unreal Engine **cannot** be opened in an older version. For example, if you saved an Asset in Unreal Engine 5.0, you will not be able to open it in Unreal Engine 4.26.

## Mandatory Updates

The following sections describe changes that you may need to make to your UE4 project in order to bring it into UE5. Some of these changes are mandatory, while others are optional but recommended and will become mandatory in future versions of UE5.

### Development Platform Changes

If you write C++ code in Visual Studio, you must switch to Visual Studio 2019 if you are not already using it. This is also the default Visual Studio IDE for the latest version of UE4. UE5 does not support Visual Studio 2017 or Visual Studio 2015.

UE5 does not support 32-bit platforms, and there are no plans to add 32-bit platform support in the future.

UE5 standardizes **Target Platform Names**. You will need to update build scripts and, in some cases, `DeviceProfiles.ini` files. This primarily affects you if you run these scripts directly; if you use **UAT**, you should not need to make changes.

The following table contains the list of changed Target Platform Names:

| UE4 Target Platform Name | UE5 Target Platform Name |
| --- | --- |
| Windows | WindowsEditor |
| WindowsNoEditor | Windows |
| MacNoEditor | Mac |
| Mac | MacEditor |
| LinuxNoEditor | Linux |
| Linux | LinuxEditor |
| LinuxAArch64NoEditor | LinuxAArch64 |

### PhysX and Chaos Physics Systems

UE5 uses the **Chaos Physics** engine for physical simulation, replacing **PhysX** as the default. Physics simulation under Chaos Physics behaves differently from PhysX, requiring developers to make adjustments in order to see consistent behavior.

The physics tick rate will change for any newly created projects by default. The tick rate change will be accessible from Tick Async Physics within Project Settings (menu: **Edit > Project Settings**). This new feature will simulate Physics on its own thread instead of on the Game Thread.

This change improves determinism by running physical simulation updates at a fixed rate. As a result of having a fixed update rate, networked physics simulation is easier to keep synchronized because client and server systems run at the same interval.

No longer running on the Game Thread means that there is a potential delay between input to the physics system from the Game Thread and the physics system's reaction to that input. You must account for this delay to avoid unpredictable behavior in projects where gameplay logic relies heavily on physics simulation. Running Physics-heavy gameplay code in C++ callbacks which execute on the Physics Thread can mitigate this, but will require modifying project code to use this approach.

### Console Variables for Shader Debugging

For the release of Unreal Engine 5, the console variables used for debugging shaders have changed. The table below offers a guide to these renames.

If your project use any of these variables in their configuration files, you will need to update them when migrating to UE5 to continue using the generated data for shader debugging.

| **Old Console Variable Name** | **New Console Variable Name** | **Description** |
| --- | --- | --- |
| `r.Shaders.KeepDebugInfo` | `r.Shaders.Symbols` | Enables debugging of shaders by generating symbols and writing them to disk for consoles. Desktop symbols are stored online. |
| N/A | `r.Shaders.ExtraData` | Generates shader names and any additional shader data. |
| `r.Shaders.PrepareExportedDebugInfo` | `r.Shaders.GenerateSymbols` | Generates symbols but does not write them to disk. Instead, symbols are stored in the Derived Data Cache (DDC). |
| `r.Shaders.ExportDebugInfo` | `r.Shaders.WriteSymbols` | Writes symbols to disk if they have been generated. |
| `r.Shaders.AllowUniqueDebugInfo` | `r.Shaders.AllowUniqueSymbols` | Generates symbol associations based on shader source. By default, this is off. |
| `r.Shaders.ExportDebugInfo.Zip` | `r.Shaders.WriteSymbols.Zip` | When writing symbols to disk, they are written out as a single ZIP file. |

The console variable `r.Shaders.KeepDebugInfo` has been split into two console variables (`r.Shaders.Symbols` and `r.Shaders.ExtraData`) to remove the changes to runtime shader data when only symbols are required. It is useful for platforms that support exported debug information because it allows symbols to be generated for shipping builds without changing the final shader data.

For more information about this process, refer to the [Shader Debugging](/documentation/en-us/unreal-engine/shader-development-in-unreal-engine) page.

## Other Changes

These updates are not required to get your **Unreal Engine 4** (UE4) project running in the **Unreal Engine 5** (UE5), but may be required in future versions, or may help you to take advantage of the engine's full capabilities.

Read through this page to learn how to prepare yourself for future versions of **Unreal Engine 5** (UE5), and to get the most out of the engine's new and upgraded features.

### C++ Object Pointer Properties

The following section only applies to projects using C++ code. Blueprints Visual Scripting users do not need to take any action. C++ Licensee projects can keep using raw object pointers or optionally begin to use `TObjectPtr`.

UE5 introduces `TObjectPtr`, a template-based, 64-bit pointer system, as an optional replacement for raw object pointers in editor builds. This system adds dynamic resolution and access tracking in editor builds, while performing identically to raw pointers in non-editor builds. `TObjectPtr` variables also convert automatically to raw pointers when passed to functions or stored in local variables. Many engine classes that once featured raw pointers in `UPROPERTY` variables now use `TObjectPtr`. While most interactions with `TObjectPtr` types will implicitly convert to raw pointers, there are some rare cases where direct interactions with engine class member variables need to change from raw pointer semantics to `TObjectPtr` semantics. For example, the `RootComponent` property in `AActor` was a `USceneComponent*` in UE4, but is a `TObjectPtr<USceneComponent>` in UE5; in some rare cases, you may need to update direct interactions with `RootComponent`, though calls to `GetRootComponent`, which still has `USceneComponent*` return type, can always remain as they are.

Although it is optional, we recommend using `TObjectPtr<T>` over `T*` for `UObject` pointer properties and container classes found in `UCLASS` and `USTRUCT` types. Since `TObjectPtr` converts to raw pointers for non-editor builds, this will not impact the behavior or performance of a shipped product, but may improve your experience when developing in editor builds. Use the following methods to adapt your programming style to this new pointer system:

-   When calling the "Find" family of container functions, use `TObjectPtr<T>*` instead of `T**` to capture the return value.
    
-   Range-based iteration through raw pointer containers might have used `auto*` as the iterator variable type. Change these to `auto&`. We also recommend using `auto&` or `const auto&` in new code, since `TObjectPtr` can cache resolved object addresses, saving time on future access attempts.
    
-   Call `ToRawPtr` or `Get` on your `TObjectPtr` when you need a raw pointer and implicit conversion is not available. Common cases include ternary operations and usage inside of `const_cast`. When passing parameters to function delegates, declare a parallel delegate function as a pass-through, replacing raw pointers with `TObjectPtr` parameters. The following example shows a passthrough delegate function:
    
    ```
                 `// Original function signature, using raw pointers, which we will use in most cases:              static bool MyFunction(UObject* FirstParameter); 		           // In rare cases where implicit conversion is not available, use this pass-through function.              // Pass-through function signature, using TObjectPtr:              static bool MyFunction(TObjectPtr<UObject> FirstParameter); 		              // Pass-through function body (in the source file):              bool UMyClass::MyFunction(TObjectPtr<UObject> FirstParameter)              {                  return ShouldShowResetToDefault(FirstParameter.Get());              }`
    Copy full snippet
    ```
    // Original function signature, using raw pointers, which we will use in most cases: static bool MyFunction(UObject\* FirstParameter); // In rare cases where implicit conversion is not available, use this pass-through function. // Pass-through function signature, using TObjectPtr: static bool MyFunction(TObjectPtr<UObject> FirstParameter); // Pass-through function body (in the source file): bool UMyClass::MyFunction(TObjectPtr<UObject> FirstParameter) { return ShouldShowResetToDefault(FirstParameter.Get()); }

In most cases, such as when passing parameters to functions or storing data in local variables, `TObjectPtr` automatically converts to raw pointer types. There are a few rare cases, such as those described above, where you will have to perform minor code modifications, but most projects will not need this.

#### Optional Conversion Tool

UE5 includes **UnrealObjectPtrTool**, a program that automatically converts engine-visible raw pointer properties to the `TObjectPtr` system. You can find it in the `UE5/Programs/UnrealObjectPtrTool/` section of the solution hierachy in your code IDE. The source code resides in `Engine/Source/Programs/UnrealObjectPtrTool/`. The executable exists in your `Engine/Binaries/Win64` folder. Depending on your Operating System or Development Enviroment, this executable may be located in your Engine/Binaries/OS folder, where OS represents your operating system.

This optional program's purpose is to expedite the process of converting your code from raw pointers to the `TObjectPtr` system. It will update `UPROPERTY` variables in class and struct definitions within your header files, but will not make all of the necessary changes to your source code as described above; you will still need to make those adjustments manually and ensure that your project compiles before using **UnrealObjectPtrTool**.

To use **UnrealObjectPtrTool**, follow these steps:

1.  Navigate to your `DefaultEngine.ini` UHT config file located in your `Engine\Programs\UnrealHeaderTool\Config` directory.
    
2.  Inside of your DefaultEngine.ini file, modify the following script:
    
    ```
            	`NonEngineNativePointerMemberBehavior=AllowAndLog`
    Copy full snippet
    ```
    NonEngineNativePointerMemberBehavior=AllowAndLog
3.  Rebuild your project to ensure all the code is parsed by UHT.
    
4.  Depending on how you compile your project, you may find your UHT log information in a file named Log.txt or UnrealHeaderTool.log. You can find those files in the following folder directories:
    
    ```
                `C:\Users\USERNAME\AppData\Local\UnrealBuildTool\Log.txt             C:\Users\USERNAME\AppData\Local\UnrealHeaderTool\Saved\Logs\UnrealHeaderTool.log             Engine\Programs\UnrealBuildTool\Log.txt`
    Copy full snippet
    ```
    C:\\Users\\USERNAME\\AppData\\Local\\UnrealBuildTool\\Log.txt C:\\Users\\USERNAME\\AppData\\Local\\UnrealHeaderTool\\Saved\\Logs\\UnrealHeaderTool.log Engine\\Programs\\UnrealBuildTool\\Log.txt
5.  Compile UnrealObjectPtrTool from the Visual Studio solution.
    
    This step is only required if running the Engine from source, otherwise the UnrealObjectPtrTool is precompiled when installing from the Epic Games Launcher.
    
6.  Run the UnrealObjectPtrTool executable:
    
    ```
                   `UnrealObjectPtrTool.exe <UHT_LOG_PATH> -SCCCommand="p4 edit -c UPGRADE_CL {filenames}"`
    Copy full snippet
    ```
    UnrealObjectPtrTool.exe <UHT\_LOG\_PATH> -SCCCommand="p4 edit -c UPGRADE\_CL {filenames}"
    
    You can add the Optional parameter: -PREVIEW or -n to get a preview of the potential changes.
    

### Rendering

The following default settings have changed, and could affect the look of your project:

-   **Screen Space Global Illumination:** The project setting for **Screen Space Global Illumination (Beta)** and the related console variable `r.SSGI.Enable` have been removed and the previous status lost. To re-enable Screen Space Global Illumination as the project's default global illumination method, go to **Project Settings > (Engine) Rendering > Global Illumination properties** and set **Dynamic Global Illumination Method** to **Screen Space (Beta)**. To re-enable Screen Space Global Illumination on a Post-Process Volume, go to the volume's properties and locate the **Global Illumination** category, then set the **Method** field to **Screen Space (Beta)**.
    
-   **Ray Tracing support with Lumen Hardware Ray Tracing:** Standalone Ray Tracing features are being deprecated in Unreal Engine 5 . However, the engine's ability to compute these lighting effects is not being removed, since Lumen covers these lighting features. What is being removed is the standalone Ray Tracing system that has been developed in Unreal Engine 4. Those features worked mostly in isolation of one another, meaning that they weren't guaranteed to support the same features of the engine equally or consistently. Lumen is adding entirely new implementations of ray tracing features for reflections and global illumination to its Hardware Ray Tracing path. As UE5 continues to develop, the ray tracing features of Lumen will continue to improve, offering wider support and feature parity with other parts of the engine.
    
    -   Ray Tracing Reflections, Global Illumination, and Shadows have been separated into their own features that can be enabled independently of each other. Each of these features can be found in **Project Settings > Rendering** and requires that **Support Hardware Ray Tracing** be enabled to use them.
    
    *Under the Global Illumination section, select the **Dynamic Global Illumination Method** preferred.* Under the Reflections section, select the **Reflection Method** preferred. \* Under the Hardware Ray Tracing section, check the box for **Ray Tracing Shadows** to be used.
    
    -   Reflections and Global Illumination can also be set using a Post Process Volume to select from the Global Illumination and Reflection methods.
-   **Generating Mesh Distance Fields:** Lumen's **Software Ray Tracing** features largely rely on **Signed Distance Fields** for mesh representation. The **Default Voxel Density** of all **Distance Fields** has increased from 0.1 to 0.2. This is neccessary to achieve good software tracing quality with Lumen, but it significantly increases Distance Field memory usage. To adjust this property, go to **Project Settings > (Engine) Rendering**, where you will find the **Generate Mesh Distance Fields** checkbox and the **Distance Field Voxel Density** property. You may need to restart the editor after changing this setting for it to take effect.
    

#### Removals

**Nanite** obsoletes most use cases for **Hardware Tessellation**. Hardware Tesselation has been removed from UE5. For use cases that Nanite does not support, users may want to increase the resolution of their assets if necessary.

**Lumen** replaces **Light Propagation Volumes** and **Distance-Field Global Illumination** (DFGI).

\* Compared to Light Propagation Volumes, Lumen provides additional features, much higher quality, and is under active development, although it has a higher baseline performance cost.

\* DFGI was an experimental feature; developers should use Lumen instead of DFGI for dynamic global illumination.

\* Over time, Lumen Global Illumination and Reflections will replace the majority of ray tracing features with similar or higher-quality results.

**Legacy Tonemapper**, which was deprecated in UE4, does not exist in UE5. No developer action is required.

#### Deprecations

-   **Cascade** will be deprecated in UE 5.0, and removed in a later release. UE5 developers should switch to **Niagara**. An automated converter to upgrade Cascade data to Niagara is in development.
-   Some **Ray Tracing** features are being deprecated and moved from a standalone system that requires support to having these features integrated into Lumen's Hardware Ray Tracing system. This means that Reflections and Global Illumination will be directly integrated into Lumen. These standalone features have been deprecated to provide a unified experience with broader support of engine features. (See the "Rendering" section above for more details.)

### World Building

#### Deprecations

**World Partition** is the system UE5 uses to handle large, streaming worlds. The **World Composition** system that UE4 used still exists, but is deprecated and will not receive upgrades, fixes, or support. World Composition will be removed in a future version of UE5.

To convert your maps to the World Partition system, use `WorldPartitionConvertCommandlet` on your project, and provide the name of each map to convert, one at a time. As an example, to convert the `TM_WorldComp_P` map, found at `/Game/Maps/Tools/Landscape/TM_WorldComp_P` in the packaged `QAGame` project, run the editor with the command-line options:

```
	`QAGame -run=WorldPartitionConvertCommandlet TM_WorldComp_P -ConversionSuffix -SCCProvider=None`
Copy full snippet
```
QAGame -run=WorldPartitionConvertCommandlet TM\_WorldComp\_P -ConversionSuffix -SCCProvider=None

This will convert the `TM_WorldComp_P` map to the World Partition system. The `-ConversionSuffix` causes the converted map to save as `TM_WorldComp_P_WP` instead of overwriting the original map. Because of the `-SCCProvider=None` option, the commandlet will run without interacting with your project's source control provider. This process will also generate a `TM_WorldComp_P.ini` file containing the settings used to convert the map, and for potential future conversions. The conversion process itself builds runtime grids (for the World Parition system) out of the existing World Composition data, and assigns the map's Actors to the appropriate grids.

Developers using C++ can see `UWorldPartitionRuntimeSpatialHash::ImportFromWorldComposition` and `UWorldPartitionRuntimeSpatialHash::GetActorRuntimeGrid` to examine or modify the logic involved in generating grids and assigning Actors to them.

### Tools

#### Removals

New geometry editing tools will replace the experimental **Legacy Editable Mesh Plugin**.

**Movie Render Queue** will replace **Movie Scene Capture**.

**VR Level Editing** will be stripped down to only support VR preview, but UE5 continues to support virtual production scouting.

**Take Recorder** will replace **Sequence Recorder**. Take Recorder includes all of the features that Sequence Recorder offered.

**Camera Animation Sequences** will replace **Camera Anims**.

UE5 also removes **Editor Feature Packs** associated with removed plugins. Users of those plugins will need to ensure that they do not reference the removed content in their projects.

#### Deprecations

**Sequencer** will fully replace **Matinee** after the full release of UE5. Matinee was deprecated, but still existed in UE4.

### Control Rig

#### Changes

**Spaces** are renamed to **Nulls**.

**Gizmos** are renamed to **Shapes**.

**Set Initial Transform from Current** now reads as **Set Offset Transform from Current**.

#### Deprecations

**Collections** are now replaced by **Arrays**.

**Transform Constraint** node is deprecated and replaced with individual **point**, **rotation**, and **parent contraint** nodes.

The new **Parent Constraint** node can be used in place of a **Project to New Parent** and **Set Transform** nodes.

**Space Switching** can now be used instead of **Parent Switch Constraint**.

**Bezier Data Type** is replaced with the **Splines plugin**.

**ControlRigHierarchyModifier** no longer is in use for Python, this is replaced with **RigHierarchy** for querying rig elements and **RigHierarchyController** to author rig elements.

**ControlRigBlueprint** no longer has a property named **controller**. To access the main **RigVMController**, use the function: **ControlRigBlueprint.get\_controller()**.

Mapping is not handled in Construction Script, but on **Pre-Initialize** of Control Rig Component.

### Audio

#### Removals

**Unreal Audio Mixer** will replace the deprecated **Legacy Audio Backends** by UE 5.0. Users do not need to take any action. UE5 will use Unreal Audio Mixer and leverage modern audio backends by default; these are compatible with all preexisting audio features.

#### Deprecations

**Audio Volumes**, **Sound Class Mix**, and **Sound Cues** will be deprecated by UE 5.0, with plans to remove them in a future release of UE5.

-   Sound Cues will be superseded by **MetaSounds**, which will be available in UE 5.0.
    
-   Sound Class Mix will be superseded by the **Modulation** and **Submix** systems, which are now available.
    
-   Audio Volumes will be superseded by a new system currently in development, which will be available in UE 5.0.
    

Users are encouraged to move to the new versions of these systems as soon as possible.

### Gameplay Framework

#### Removals

**Blueprint Nativization** will not exist in UE5. Projects that leveraged this feature should not see any changes or need to receive any modifications in order to function properly, though performance may be impacted. If this happens, developers will need to take other optimization approaches.

### Networking

#### Deprecations

**AES, RSA, and RSA Key AES Encryption Handlers** are deprecated and planned for removal.

### Core

#### Removals

**Zen Loader** will replace the **Event-Driven Loader**. Since most users do not interface directly with the Event-Driven Loader, this change use not require any actions during project migration.

#### Deprecations

**Unreal Insights** instrumentation will replace the **Stats System** after the full release of UE 5.0. The Stats System will continue to exist in UE 5.0, but will eventually be removed in favor of Unreal Insights.
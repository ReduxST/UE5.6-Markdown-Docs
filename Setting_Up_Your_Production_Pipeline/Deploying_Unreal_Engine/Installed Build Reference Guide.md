# Installed Build Reference Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/installed-build-reference-guide-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/installed-build-reference-guide-for-unreal-engine)  
**Processed:** 2025-06-14 16:31:09

---

Developers always look for ways to efficiently deliver build solutions for various hardware profiles and operating systems. An **Installed Build** is a fully featured Unreal Engine (UE) build that you can redistribute to get your team up and running with the engine quickly. From a technical standpoint, an Installed build contains precompiled binaries for UE and a static library for each target platform in development and shipping configurations.

The Installed Build process automates build packages and tools needed to make an Installed Build version of UE. In summary, making an Installed Build is the process of setting up default target platforms, compiling UE with its tools and editor, running tests, and deploying the Installed Build version of UE to targeted platforms.

In addition to making your build, you should download UE from Launcher; for more information see [](programming-and-scripting\development-environment-setup\downloading-unreal-engine-source-code).

## Making an Installed Build

You can create Installed Builds using the [BuildGraph](https://dev.epicgames.com/documentation/en-us/unreal-engine/buildgraph-for-unreal-engine) scripting system with the Installed Build script located in the folder with your downloaded source code at `[UERoot]/Engine/Build/InstalledBuild.xml`.

To create an Installed Build:

1.  Open **Command Prompt** on your system.
    
2.  Input command line to run the Installed Build Script by invoking the **AutomationTool**. This command line may look as follows (replace `[PLATFORM]` with either `Win64`, `Linux`, or `Mac`, depending on your system):
    
    C++
    
    `C:\EpicSource\UE_5.5\UnrealEngine-5.5\Engine\Build\BatchFiles\RunUAT.bat BuildGraph -target="Make Installed Build [PLATFORM]" -script="Engine/Build/InstalledEngineBuild.xml" -clean`
    
    C:\\EpicSource\\UE\_5.5\\UnrealEngine-5.5\\Engine\\Build\\BatchFiles\\RunUAT.bat BuildGraph -target=&quot;Make Installed Build \[PLATFORM\]&quot; -script=&quot;Engine/Build/InstalledEngineBuild.xml&quot; -clean
    
    Copy full snippet(1 line long)
    
    Let's get familiar with the parts of this command line:
    
    -   `C:\EpicSource\UE_5.5\UnrealEngine-5.5\` - location of downloaded source code (could be different on your PC).
        
    -   `Engine\Build\BatchFiles\RunUAT.bat` - location of Unreal Automation Tool command file, that you use for command of building.
        
    -   `-target="Make Installed Build [PLATFORM]"` - target platform, you want to build engine (replace `[PLATFORM]` with either `Win64`, `Linux`, or `Mac`).
        
    -   `-script=Engine/Build/InstalledEngineBuild.xml` - location of the file, that contain options for installation process.
        
    -   You can also adjust additional [Installed Build Script Options](https://dev.epicgames.com/documentation/en-us/unreal-engine/installed-build-reference-guide-for-unreal-engine).
        
    
    If you use additional [Installed Build Script Options](https://dev.epicgames.com/documentation/en-us/unreal-engine/installed-build-reference-guide-for-unreal-engine), your code will look as follows (depends on settings you adjust):
    
    C++
    
    `C:\EpicSource\UE_5.5\UnrealEngine-5.5\Engine\Build\BatchFiles\RunUAT.bat BuildGraph -target="Make Installed Build [PLATFORM]" -script="Engine/Build/InstalledEngineBuild.xml" -set:WithWin64=true -set:WithMac=true -set:WithTVOS=false -set:WithLinux=false -set:WithHTML5=true`
    
    C:\\EpicSource\\UE\_5.5\\UnrealEngine-5.5\\Engine\\Build\\BatchFiles\\RunUAT.bat BuildGraph -target=&quot;Make Installed Build \[PLATFORM\]&quot; -script=&quot;Engine/Build/InstalledEngineBuild.xml&quot; -set:WithWin64=true -set:WithMac=true -set:WithTVOS=false -set:WithLinux=false -set:WithHTML5=true
    
    Copy full snippet(1 line long)
    
3.  By default, your Installed Build should be located in the `LocalBuilds/Engine/` folder of your Unreal Engine directory. If you specified a different directory to publish to, navigate to that directory instead.
    

## Installed Build Script Options

The `InstalledEngineBuild.xml` script creates an Installed Build with all the default options and platforms enabled. However, you can configure it using a set of specified options. These options provide more control, such as targeting which platforms to include and where to publish the build.

You can view a list of available options for customizing the build process (along with a list of nodes built by default) by passing the `-listonly` option to the script.

The available options are listed in the table below.

| Option | Default | Description |
| --- | --- | --- |
| 
`-set:HostPlatformOnly=[true/false]`

 | 

false

 | 

A helper option to make an installed build for your host platform only, so that you don't have to disable each platform individually.

 |
| 

`-set:WithWin64=[true/false]`

 | 

true

 | 

Include the Win64 target platform.

 |
| 

`-set:WithWin32=[true/false]`

 | 

true

 | 

Include the Win32 target platform.

 |
| 

`-set:WithMac=[true/false]`

 | 

true

 | 

Include the Mac target platform.

 |
| 

`-set:WithAndroid=[true/false]`

 | 

true

 | 

Include the Android target platform.

 |
| 

`-set:WithIOS=[true/false]`

 | 

true

 | 

Include the iOS target platform.

Enabling this option requires a Mac set up for remote building.



 |
| 

`-set:WithTVOS=[true/false]`

 | 

true

 | 

Include the tvOS target platform.

Enabling this option requires a Mac set up for remote building.



 |
| 

`-set:WithLinux=[true/false]`

 | 

true

 | 

Include the Linux target platform.

 |
| 

`-set:WithLinuxArm64[true/false]`

 | 

true

 | 

Include the Linux Arm64 target platform.

 |
| 

`-set:WithPS4=[true/false]`

 | 

false

 | 

Include the PS4 target platform.

Enabling this option requires the PS4 SDK.



 |
| 

`-set:WithPS5=[true/false]`

 | 

false

 | 

Include the PS5 target platform.

Enabling this option requires the PS5 SDK.



 |
| 

`-set:WithSwitch=[true/false]`

 | 

false

 | 

Include the Switch target platform.

Enabling this option requires the SwitchSDK.



 |
| 

`-set:WithXboxOneGDK=[true/false]`

 | 

false

 | 

Include the legacy WithXboxOneGDK target.

Enabling this option requires the Xbox One SDK.



 |
| 

`-set:WithGDK=[true/false]`

 | 

false

 | 

Include the GDK target platform.

Enabling this option requires the GDK.



 |
| 

`-set:WithXB1=[true/false]`

 | 

false

 | 

Include the XB1 target platform.

Enabling this options requires the XB1 XDK.



 |
| 

`-set:WithWinGDK=[true/false]`

 | 

false

 | 

Include the WinGDK target platform.

Enabling this option requires the WinGDK.



 |
| 

`-set:WithXSX=[true/false]`

 | 

false

 | 

Include the XSX target platform.

 |
| 

`-set:WithDDC=[true/false]`

 | 

true

 | 

Build a stand-alone derived-data cache for the engine content and templates.

Building a stand-alone [Derived Data Cache (DDC)](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-derived-data-cache-in-unreal-engine) for the engine and template content can be one of the slowest aspects of the build. If you don't need a stand-alone DDC, you can skip this step by appending `-set:WithDDC=false` to the command line.



 |
| 

`-set:HostPlatformDDCOnly=[true/false]`

 | 

true

 | 

Whether to include DDC for the host platform only.

 |
| 

`-set:WithClient=[true/false]`

 | 

false

 | 

Include precompiled client targets.

 |
| 

`-set:WithServer=[true/false]`

 | 

false

 | 

Include precompiled server targets.

 |
| 

`-set:WithFullDebugInfo=[true/false]`

 | 

false

 | 

Generate full debug info for binary editor and packaged application builds.

 |
| 

`-set:SignExecutables=[true/false]`

 | 

false

 | 

Sign the executables produced if you have to set up your machine to sign executables as part of the build process.

 |
| 

`-set:AnalyticsTypeOverride=[ID]`

 | 

no default

 | 

Identifier for analytic events to send.

 |
| 

\` -set:EmbedSrcSrvInfotrue/false\`

 | 

false

 | 

Whether to add Source indexing to Windows game apps so they can be added to a symbol server.

 |
| 

`-set:AllowParallelExecutor=[true/false]`

 | 

false

 | 

Allow the use of UAT's ParallelExecutor when compiling.

 |
| 

`-set:GameConfigurations=[Configurations]`

 | 

Shipping;Development;DebugGame

 | 

Specifies the configurations for packaged applications.

 |
| 

`-set:SignWindowsExecutablesInParallel=[true/false]`

 | 

false

 | 

Sign the executables in parallel, Windows only.

 |
| 

`-set:ExtraCompileArgs`

 | 

no default

 | 

Extra arguments to pass to compiles run on non-Mac-based platform. Use to enable options like UBA.

 |
| 

`-set:Extra arguments to pass to compiles run on Mac platforms`

 | 

no default

 | 

Extra arguments to pass to compiles run on Mac-based platforms. Use to enable options like UBA.

 |
| 

`-set:ExtraDDCArgs`

 | 

no default

 | 

Extra arguments to pass to DDC Generation. Use to enable options like UBA.

 |

### Including Additional Files

RuntimeDependencies (set in `build.cs` files for each module) automatically collate and determine which files are included in an Installed Build. However, some required files cannot be included cannot be included this way, so they're defined in `[UERoot]/Engine/Build/InstalledEngineFilters.xml`. The `InstalledEngineFilters` XML file also lists patterns of files that should be excluded from the build, determining the types of files that need to be stripped or signed, and finally, deciding what projects to build the DDC for. If you need to include additional files with the Installed Build, the `InstalledEngineFilters` XML file is a great place to start.

## Registering an Installed Build

UE has the concept of "foreign" projects and "non-foreign" projects. Foreign projects are those stored in a separate directory tree to the engine, while non-foreign projects are stored in sub-directories of the engine root, referenced by the `UEGames.uprojectdirs` extension.

The "EngineAssociation" field in a `.uproject` file identifies which Editor version will open the project. For non-foreign projects, it is left blank, because being non-foreign implies the existence of an Editor in a (known) relative location, up from the directory hierarchy of the project. For foreign projects using Engine builds installed by the Launcher, the field will contain the official version number (such as "5.5"), and the Launcher can find the appropriate Editor binary (assuming it has been installed) based on its list of installed applications. For foreign projects using an Engine build distributed by means other than the Launcher, the Engine build's random unique identifier can be used to find the installed directory via a globally-accessible data repository, specifically, the registry on Windows, or a file in the library folder on Mac. If an association with an installed Editor build cannot be found, the user will be prompted to select a version, and the `.uproject` file will be updated with the selected version.

When distributing an Installed Build to a team, make sure that the build's identifier is common to everyone. This will prevent the Editor from prompting for version selection and then updating the `.uproject` file with a locally-generated unique identifier. Setting a custom identifier can be done as follows:

-   On **Windows**, add a registry key to `HKEY_CURRENT_USER\SOFTWARE\Epic Games\UnrealEngine\Builds` that uses your identifier as its key, and the path to the Engine as its value. For example, the key might be `MyCustom419` , and the value might be `D:\CustomUE`.
    
-   On **Mac**, open `/Users/MyName/Library/Application Support/Epic/UnrealEngine/Install.ini` and add an entry to the `[Installations]` section that uses your identifier as the key, and the path to the engine as the value. For example:
    
    C++
    
    `[Installations]         MyCustom419 = /Users/MyName/CustomUE`
    
    \[Installations\] MyCustom419 = /Users/MyName/CustomUE
    
    Copy full snippet(2 lines long)
    

## Choosing this Deployment Method

If you rarely need to change the engine, and if you're looking for a way to quickly (and efficiently) deliver build solutions for a variety of hardware profiles and operating systems, you can deploy an Installed Build of UE (or download the engine from our launcher).

Keep in mind, if you're not looking for a read-only distribution of UE (that can be installed into C:\\Program Files), then this method isn't for you, mainly because it's designed to create standalone, read-only engine content, source code, and third-party libraries. Although we provide Installed Engine Builds as a courtesy through the Epic Games Launcher, we don't consume this method for our internal games teams. Furthermore, we treat this as a standalone deployment product in its own right.
# Creating Bundled PSO Caches for Android

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-bundled-pso-caches-for-android-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-bundled-pso-caches-for-android-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:17

---

[PSO Caching](/documentation/en-us/unreal-engine/optimizing-rendering-with-pso-caches-in-unreal-engine) creates and stores the most commonly-used Pipeline State Object data for your app in advance to improve rendering performance, most especially to reduce hitches while running your application. This guide provides a walkthrough of implementing PSO Caching in an Android project in Unreal Engine (UE).

This page provides instructions for the Bundled PSO caching method, which is the legacy, manual PSO caching system used in UE versions 5.2 and earlier. We recommend using the PSO precaching system from 5.3 and newer if it is viable for your project. See the [documentation for PSO Precaching](/documentation/en-us/unreal-engine/pso-precaching-for-unreal-engine) for more details.

## Required Setup

To follow this guide, you need the following:

-   An Unreal Engine project that is set up for [Android as a target platform](/documentation/en-us/unreal-engine/setting-up-unreal-engine-projects-for-android-development).
    
-   The version of [Android SDK and NDK](/documentation/en-us/unreal-engine/advanced-setup-and-troubleshooting-guide-for-using-android-sdk) compatible with your current version of Unreal Engine.
    
-   A compatible Android testing device with [developer mode and USB debugging](/documentation/en-us/unreal-engine/setting-up-your-android-device-for-developing-applications-in-unreal-engine) enabled.
    

To learn more about which Android devices are compatible with your version of Unreal Engine, see [Android Development Requirements](/documentation/404)

## Set Up Project Settings for PSO Caching

To configure your project settings to support PSO caching, follow these steps:

1.  Open your project in Unreal Editor.
    
2.  Open **Edit** \> **Project Settings**.
    
3.  Navigate to **Project** \> **Packaging** and make sure **Share Material Shader Code** and **Shared Material Native Libraries** are both enabled.
    
4.  In the next step you need to edit config files manually. Close Unreal Editor to avoid conflicts between your manual edits and the Project Settings.
    
5.  Open your project's `Config/Android` folder, then open `AndroidEngine.ini`. Add the following settings:
    
    ```
    		
         `[DevOptions.Shaders]      NeedsShaderStableKeys=true`
    		
    Copy full snippet
    ```
    \[DevOptions.Shaders\] NeedsShaderStableKeys=true

## Run Your Game and Gather PSOs

Now that your project settings are PSO cache-compatible, run a build of your project with the `-logPSO` command line enabled.

1.  Make sure your testing device is connected to your computer.
    
2.  Open your project in Unreal Editor.
    
3.  Click **Platforms** \> **Project Launcher**.
    
4.  In the Project Launcher, click **\+ Add** \> **Create Custom Profile** to make a new launch profile.
    
    ![In the Project Launcher, the user selects the Add button and clicks Create Custom Profile.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/927b9eec-06b5-4de7-a25b-8adeaf40f0bb/createcustomprofile.png)
5.  Re-name your profile **PSO Caching - ETC2**.
    
6.  In the dropdown next to **How would you like to cook your content?**, click **Cook by the Book**.
    
7.  Choose **Android\_ETC2** as your target platform.
    
    ![In the Project Launcher, Cook by the Book is the cook setting, and Android_ETC2 is the target platform.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a4c6ae8-acd8-4431-b93b-b73b336bfcc8/androidetc2.png)
8.  Under **Deploy**, choose your mobile device as the target device and set the **Variant** to **Android\_ETC2**.
    
9.  Under the **Launch** category, add the `-logPSO` command to **Additional Command Line Parameters**.
    
    ![The -logPSO command is added to Additional Command Line Parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dcc1d9e2-53bf-4196-9a5c-cb0ce84ac195/logpso.png)
    
    You can use **Android File Server (AFS)** to add the `-logPSO` command to the \`UECommandLine.txt file to an existing build on your device. For more details, see the [documentation for AFS](/documentation/en-us/unreal-engine/android-file-server-for-unreal-engine).
    
10.  Launch your profile. UE builds and packages the project, then deploys it to your device.
    
11.  Play through your game. The Output Log displays a message anytime your game logs a new PSO.
    

When you do future PSO gathering sessions, you can re-use the profile you created from this section.

### Tips for Gathering PSOs

The more PSOs you gather, the longer your game's startup time will be when you package the final app, as all your PSOs have to be loaded before users can start playing. Therefore, we advise gathering PSOs specifically in locations you know are commonly used and have noticeable stuttering, as PSO caches for these locations provide the most benefit to users’ experience.

Anytime a location significantly changes, previously-gathered PSOs for that location will become outdated. Therefore, make sure to gather PSOs frequently throughout production.

## Retrieve Gathered PSO Data From Your Device

After logging your PSOs, you need to retrieve the data from your testing device and incorporate it into a new build. To retrieve your PSO data, follow these steps:

1.  Unplug your testing device from your computer and close your game.
    
    If you try to close your game from the Project Launcher, your device might not save the PSO data it logged.
    
2.  Close your project and re-connect your testing device to your computer.
    
3.  Pull the PSOs from the following directory:
    
    `Internal Storage/Android/Data/[package name of project]/files/UnrealGame/[project name]/Saved/CollectedPSOs`
    
    You can pull the CollectedPSOs directory's contents using any of the following methods:
    
    \* Run the following command using Android File Server (AFS): `UnrealAndroidFileTool -p [package name] -k [security token] pull ^saved/CollectedPSOs [destination path]`
    
    \* Connect your device to your computer and use your computer's file system to browse to the location of the PSOs.
    
4.  Copy the `.UPIPELINECACHE` file to your computer in a location that is easily accessible. This example uses a folder in in the project's directory called `Import/PSOFiles`.
    

## Build Final PSO Cache Data and Add It To Your Project

To incorporate your PSO cache into a build, follow these steps:

1.  Open your project folder and locate Saved/Cooked/Android\_ETC2/\[Project Name\]/Metadata/PipelineCaches. Copy the files in this folder into Import/PSOFiles.
    
2.  Open your command line tool and navigate to the install directory for the engine version you are using for your project, then locate the Engine/Binaries/Win64 folder. For example: C:/Program FIles/Epic Games/UE\_5.2/Engine/Binaries/Win64.
    
3.  Run the following command line:
    
    ```
         `UnrealEditor-Cmd.exe "YourProjectPath.uproject" -run=ShaderPipelineCacheTools expand C:\PSOfiles*.rec.upipelinecache C:\PSOfiles*.shk C:\PSOfiles\"Alias Name"_"Project Name"_"Used Graphics API".spc`
    Copy full snippet
    ```
    UnrealEditor-Cmd.exe "YourProjectPath.uproject" -run=ShaderPipelineCacheTools expand C:\\PSOfiles\*.rec.upipelinecache C:\\PSOfiles\*.shk C:\\PSOfiles\\"Alias Name"\_"Project Name"\_"Used Graphics API".spc
4.  After the command line runs successfully, the Import/PSOFiles directory should contain a new PKCS #7 certificate file. Copy it to your project's Build/Android/PipelineCaches folder.
    
5.  Rebuild and launch your game again. The new build includes the final PSO cache data.
    

## Result

On launch, you should also see a log stating how many PSOs were loaded. When you run your game, any rendering stutters from locations you gathered PSOs from should be addressed.
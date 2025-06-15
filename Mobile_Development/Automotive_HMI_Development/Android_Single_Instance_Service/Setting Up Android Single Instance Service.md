# Setting Up Android Single Instance Service

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-android-single-instance-service-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-android-single-instance-service-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:16

---

This guide explains how to set up Android Single Instance Service (ASIS) in Unreal Engine, then how to create, package, and run your Unreal Engine project as an Android application.

## Set up Android SDK and NDK

To set up ASIS, you must first set up the Android Software Development Kit (SDK) and Android Native Development Kit (NDK) in Unreal Engine. Unreal Engine uses Android Studio and the Android SDK Command-Line Tools to download and install the Android SDK components required to develop Android projects.

To set up the Android SDK and NDK, follow these steps:

1.  Follow the steps on the [Setting Up Android SDK and NDK](https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-android-sdk-ndk-and-android-studio-using-turnkey-for-unreal-engine) page.  
    
2.  If you are using Unreal Engine 5.5 or higher, enable the following SDK Platforms and Tools:
    
    1.  **SDK Tools** > **Android SDK Build-Tools 36** > **35.0.0** and **34.0.0**
        
        [![SDK Tools > Android SDK Build-Tools 36 > 35.0.0 and 34.0.0](https://dev.epicgames.com/community/api/documentation/image/4805fd3d-1c59-4b3e-89f9-19674f97a456?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4805fd3d-1c59-4b3e-89f9-19674f97a456?resizing_type=fit)
        
    2.  **SDK Tools** > **NDK (Side by side)** > **25.1.8937393**
        
        [![SDK Tools > NDK (Side by side) > 25.1.8937393](https://dev.epicgames.com/community/api/documentation/image/c3d5889d-407b-41c1-af75-750806f9026b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c3d5889d-407b-41c1-af75-750806f9026b?resizing_type=fit)
        
    3.  **SDK Platforms** > **Android 14.0 ("UpsideDownCake")**, API Level 34
        
        [![SDK Platforms > Android 14.0 ("UpsideDownCake"), API Level 34, Revision 3](https://dev.epicgames.com/community/api/documentation/image/1bec09c8-739a-40bb-a07f-0b1ede84e8fd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1bec09c8-739a-40bb-a07f-0b1ede84e8fd?resizing_type=fit)
        

## Create a New Project from the ASIS Template

After the Android SDK and NDK are installed, you can setup the ASIS template plugin. The plugin is delivered as a separate archive, so manual steps need to be done to prepare the Unreal Engine source code.

### Get Unreal Engine source code

Pull the latest source code from the UE5 Main in either Perforce or Github. For more information on using Perforce and Github with Unreal Engine, refer to the following resources:

-   [Using Perforce as Source Control](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-perforce-as-source-control-for-unreal-engine)
    
-   [How To Use Unreal Engine 5 - Perforce](https://www.perforce.com/blog/vcs/how-use-unreal-engine-5-perforce)
    
-   [Accessing Unreal Engine source code on Github](https://www.unrealengine.com/en-US/ue-on-github)
    
-   [Downloading Unreal Engine Source Code](https://dev.epicgames.com/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine)
    
-   [Building Unreal Engine from Source](https://dev.epicgames.com/documentation/en-us/unreal-engine/building-unreal-engine-from-source)
    

### Set Up the ASIS Plugin

1\. Navigate to the ASIS Templates folder.

1.  Navigate to the ASIS Templates folder.
    
    1.  If you're using Perforce, navigate to `UE5_Main\Engine\Restricted\NotForLicensees\Plugins\AndroidSingleInstanceService\Templates\`
        
    2.  If you're using GitHub, access the `ue5-main` branch and navigate to `ue5-main\Engine\Restricted\NotForLicensees\Plugins\AndroidSingleInstanceService`. 
        
2.  Copy the **TP\_HMI\_ASIS** folder to `UE5_Main\Templates\` (Perforce) or `ue5-main\Templates\` (GitHub).
    
3.  Copy the following code and paste it in `UE5_Main\Templates\TemplateCategories.ini` (Perforce) or `ue5-main\Templates\TemplateCategories.ini` (GitHub):
    
    C++
    
    `Categories=(Key="HMI", LocalizedDisplayNames=((Language="en",Text="Automotive\nHMI &\nVehicle Cockpit using Android Single Instance Service")), LocalizedDescriptions=((Language="en",Text="Find templates for automotive vehicle cockpit using Android Single Instance Service"), Icon="TP_HMI_ASIS/Media/AutomotiveHMI_2x.png", IsMajorCategory=true)`
    
    Categories=(Key=&quot;HMI&quot;, LocalizedDisplayNames=((Language=&quot;en&quot;,Text=&quot;Automotive\\nHMI &amp;\\nVehicle Cockpit using Android Single Instance Service&quot;)), LocalizedDescriptions=((Language=&quot;en&quot;,Text=&quot;Find templates for automotive vehicle cockpit using Android Single Instance Service&quot;), Icon=&quot;TP\_HMI\_ASIS/Media/AutomotiveHMI\_2x.png&quot;, IsMajorCategory=true)
    
    Copy full snippet(1 line long)
    
4.  Run **UnrealEditor**. The Unreal Project Browser should now include a new HMI template:
    
    [![The new HMI template in the Unreal Project Browser.](https://dev.epicgames.com/community/api/documentation/image/064bc529-a97b-4e9b-a555-90d1d4caec11?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/064bc529-a97b-4e9b-a555-90d1d4caec11?resizing_type=fit)
    
5.  Click **Create**. The project should look like the following screenshot:
    
    [![A screenshot of Unreal Engine, showing a blank HMI project created from the template.](https://dev.epicgames.com/community/api/documentation/image/316b10fa-ac4a-4156-ac36-f72862a03c7e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/316b10fa-ac4a-4156-ac36-f72862a03c7e?resizing_type=fit)
    

Add ASIS Plugin to an Existing Project

## Add ASIS Plugin to an Existing Project

If you have an existing project you want to add ASIS to, follow these steps:

1.   Go to **Edit** \> **Plugins** and enable **AndroidSingleInstanceService**.
    
    [![Screenshot of the enabled AndroidSingleInstanceService plugin](https://dev.epicgames.com/community/api/documentation/image/61a68dd3-fa01-4188-97bf-40934caee4bb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/61a68dd3-fa01-4188-97bf-40934caee4bb?resizing_type=fit)
    
2.  Copy the following code and paste it into the  `{Project_Name}/Config/DefaultGame.ini`  file:
    
    Config
    
    `[Staging] +RemapDirectories=(From="Engine/Restricted/NotForLicensees/Plugins/AndroidSingleInstanceService", To="Engine/Plugins/Runtime/AndroidSingleInstanceService") +RemapDirectories=(From="Engine/Restricted/NotForLicensees/Plugins/Experimental/MultiWindow", To="Engine/Plugins/Experimental/MultiWindow")`
    
    \[Staging\] +RemapDirectories=(From=&quot;Engine/Restricted/NotForLicensees/Plugins/AndroidSingleInstanceService&quot;, To=&quot;Engine/Plugins/Runtime/AndroidSingleInstanceService&quot;) +RemapDirectories=(From=&quot;Engine/Restricted/NotForLicensees/Plugins/Experimental/MultiWindow&quot;, To=&quot;Engine/Plugins/Experimental/MultiWindow&quot;)
    
    Copy full snippet(3 lines long)
    
3.  In Unreal Engine, go to **Edit** \> **Project Settings.**
    
4.  Under **Plugins** > **AndroidSingleInstanceService**, enable the following settings:
    
    [![The Android Single Instance Service settings](https://dev.epicgames.com/community/api/documentation/image/9a0995f5-67be-4c14-a577-e58ddb820adb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9a0995f5-67be-4c14-a577-e58ddb820adb?resizing_type=fit)
    
    1.  **Compile ASISProject**
        
    2.  **Enable asis libs generation**
        
    3.  **Use AndroidSingleInstanceService**
        

## Package and Run the ASIS Project

After setting up ASIS in your Unreal Engine project, you can package and run the project as an Android application.

To package the ASIS project as an Android application, follow these steps:

1.  In the Main Toolbar, click **Platforms** > **Android** > **Package Project**.
    
    [![The Package Project menu item](https://dev.epicgames.com/community/api/documentation/image/7932f70c-52a5-4add-8367-8a51bb4e2734?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7932f70c-52a5-4add-8367-8a51bb4e2734?resizing_type=fit)
    
2.  Check the **Output Log** to make sure the build was successful.
    
    [![The Output Log showing a successful build.](https://dev.epicgames.com/community/api/documentation/image/a5702abe-77d4-4fd9-a3cc-9e9e544c27a9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a5702abe-77d4-4fd9-a3cc-9e9e544c27a9?resizing_type=fit)
    

The package is saved by default to `/Documents/UnrealProjects/_packages/ASIS_Package`.

[![The ASIS package folder](https://dev.epicgames.com/community/api/documentation/image/8c4d1055-1c28-4715-b549-b315b4707d9c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8c4d1055-1c28-4715-b549-b315b4707d9c?resizing_type=fit)

### Communicating Between The Android Application and the Unreal Engine APK

After packaging the application, you can use an example client application to communicate with the Unreal Engine APK.

The Unreal Engine package includes 3 main parts:

-   An **APK** with Android Service. It is located in the folder that was chosen while project package dialog.
    
-   A set of ASIS helper libraries that are used in the client applications.
    
    C++
    
    `Binaries/Android/aars ├── asisclientlib-1.0.1-debug.aar ├── asisclientlib-1.0.1-debug.jar ├── asiscommon-1.0.1-debug.aar └── asiscommon-1.0.1-debug.jar`
    
    Binaries/Android/aars ├── asisclientlib-1.0.1-debug.aar ├── asisclientlib-1.0.1-debug.jar ├── asiscommon-1.0.1-debug.aar └── asiscommon-1.0.1-debug.jar
    
    Copy full snippet(5 lines long)
    
-   An example client application that communicates with the service. This is not located in the packaged Unreal Engine project, but the Binaries folder of your Unreal Engine Project (`\Unreal Projects\{Project_Name}\Binaries\Android`).
    
    [![The example application in the Binaries folder.](https://dev.epicgames.com/community/api/documentation/image/e7619fc2-1635-4b2d-8fd9-e26e8f13cc91?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e7619fc2-1635-4b2d-8fd9-e26e8f13cc91?resizing_type=fit)
    

You can use Android Studio to open the example Android project. It will automatically go through the Android build process when you open it. 

You can also build the project using the following command line prompt:

Command Line

```code
`cd {Project_Name}\Binaries\Android\ExampleUseCase_{Project_Name}\ gradlew assembleDebug`
```

cd {Project\_Name}\\Binaries\\Android\\ExampleUseCase\_{Project\_Name}\\ gradlew assembleDebug

Copy full snippet(2 lines long)

This command will generate an APK file at  `{Project_Name}\Binaries\Android\ExampleUseCase_{Project_Name}\app\build\outputs\apk\debug\app-debug.apk`.

In Android Studio, with an Android device selected, you can run the application by pressing **Shift** + **F10,** or by clicking the **Play** button in the top toolbar.

[![The Play button in Android Studio](https://dev.epicgames.com/community/api/documentation/image/69a185de-e7b8-4bc6-a238-2dac361443ca?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/69a185de-e7b8-4bc6-a238-2dac361443ca?resizing_type=fit)

To install the APK on your Android device, run the following `adb` command:

C++

`adb install {Project_Name}.apk`

adb install {Project\_Name}.apk

Copy full snippet(1 line long)

In the application on your device, tap **Activate View1**, **Activate View2**, and **Activate View3** to view the Android Service communicating with the Unreal Engine application.

[![The Android app, showing the three views.](https://dev.epicgames.com/community/api/documentation/image/00778065-0b86-4da8-b8fd-cc615db138f3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/00778065-0b86-4da8-b8fd-cc615db138f3?resizing_type=fit)
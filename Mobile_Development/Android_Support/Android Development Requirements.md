# Android Development Requirements

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/android-development-requirements-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/android-development-requirements-for-unreal-engine)  
**Processed:** 2025-06-14 16:05:41

---

This page contains the software development kit (SDK) requirements needed to develop Unreal Engine (UE) projects for Android devices, as well as compatible hardware for the current version of UE.

## Current SDK Information

Since August 31, 2024, Google Play Store requires apps to target Android 14, which requires API level 34. To publish new apps on the Google Play Store, you must update to UE 5.4.4 or newer for target SDK 34 support. Apps built with previous versions of UE will no longer submit successfully.   
  
For more information, see the [Android documentation on Google Play's target API level requirement](https://developer.android.com/google/play/requirements/target-sdk).

-   Current UE Version: 5.6
    
-   Android Studio Version: Koala 2024.1.2 August 29, 2024
    
-   Android SDK:
    
    -   Recommended: SDK 34
        
    -   Minimum for compilation: SDK 34
        
    -   Default target SDK for shipping on devices: 34
        
    -   Minimum install SDK level: 26
        
        Different stores have their own target SDK minimum requirements, which may differ from that mentioned above.
        
-   NDK Version:  r25b
    
-   Build-tools: 34.0.0
    
-   Java runtime: OpenJDK 21.0.3 2024-04-16
    
-   AGDE v23.2.91+ required for [AGDE debugging](https://dev.epicgames.com/documentation/en-us/unreal-engine/debugging-unreal-engine-projects-for-android-in-visual-studio-with-the-agde-plugin). 
    

## Current Compatible Devices

UE supports Android devices meeting the following specifications:

-   Android 8 or higher
    
-   64-bit Arm-based CPU
    
-     UE 5.6 supports both 4KB and 16KB page sizes
    
-   Compatible GPUs
    
    -   Mali T8xx, G68, G71, G72, G76, G77, G78, or G7xx series
        
    -   Adreno 5xx, 6xx or 7xx series
        
    -   PowerVR GM9xxx series
        
    -   Samsung Xclipse 9xx series
        
-   Compatible Graphics APIs
    
    -   OpenGL ES 3.2
        
    -   Vulkan 1.1 on Android 10 or later devices with compatible drivers
        

## Version History

| UE Version | Android Studio Version | Minimum Android SDK Version | Android NDK Version | Notes |
| --- | --- | --- | --- | --- |
| 
5.6

  


 | 

Koala 2024.1.2 August 29, 2024

 | 

Recommended: SDK 34

Minimum: SDK 34

 | 

NDK r25b

 | 

Supports 16kb memory page size.

 |
| 

5.5

 | 

Koala 2024.1.2 August 29, 2024

 | 

Recommended: SDK 34

Minimum: SDK 34

 | 

NDK r25b

 |  |
| 

5.3-5.4

 | 

Flamingo 2022.2.1 Patch 2 May 24, 2023

 | 

Recommended: SDK 33

Minimum: SDK 30

 | 

NDK r25b

 |  |
| 

5.1-5.2

 | 

Android Studio 4.0

 | 

Recommended: SDK 32

Minimum: SDK 30

 | 

NDK r25b

 | 

While SDK 30 is the minimum needed to compile on your system, SDK 26 is the minimum SDK you can target for shipping projects on devices.

 |
| 

5.0

 | 

Android Studio 4.0

 | 

SDK 23

 | 

NDK r21e

 | 

Minimum SDK version required to use Android File Server (AFS) is 26.

 |
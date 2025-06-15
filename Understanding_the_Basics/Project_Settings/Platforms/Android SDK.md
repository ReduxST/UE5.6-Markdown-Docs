# Android SDK

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/android-sdk-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/android-sdk-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:05:49

---

## Android SDK

### SDK Config

| **Setting** | **Description** |
| --- | --- |
| **Location of Android SDK** | 
The on-disk location of Android SDK (falls back to the `ANDROID_HOME` environment variable if this field is blank).

The directory usually contains `android-sdk-`.



 |
| **Location of Android NDK** | 

The on-disk location of Android NDK (falls back to the `NDKROOT` environment variable if this field is blank).

The directory usually contains `android-ndk-`.



 |
| **Location of JAVA** | 

The on-disk location of Java (falls back to the `JAVA_HOME` environment variable if this field is left blank).

The directory usually contains `jdk`.



 |
| **SDK API Level** | 

Define which SDK to package and compile Java with.

You can use:

-   A specific version.
-   `latest` for latest version on disk.
-   `matchndk` to match the NDK API Level.



 |
| **NDK API Level** | 

Define which NDK to compile with (a specific version or `latest` for latest version on disk).

Choosing `android-21` or any later version will result in the app not running on pre-5.0 devices.



 |
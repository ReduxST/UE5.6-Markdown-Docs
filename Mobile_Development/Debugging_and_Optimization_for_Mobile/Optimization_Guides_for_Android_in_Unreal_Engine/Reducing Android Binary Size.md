# Reducing Android Binary Size

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/reducing-android-binary-size-in-unreal-engine-projects](https://dev.epicgames.com/documentation/en-us/unreal-engine/reducing-android-binary-size-in-unreal-engine-projects)  
**Processed:** 2025-06-14 16:46:06

---

Mobile storefronts limit the amount of data that can be sent to a device, especially when delivering games over cellular data. Many stores impose mandatory limits on the size of APKs and OBBs. Because of this, it is a best practice to reduce the size of mobile applications as much as possible. Content delivery systems like [Google Play Asset Delivery](/documentation/en-us/unreal-engine/using-google-play-asset-delivery-in-unreal-engine) and [ChunkDownloader](/documentation/en-us/unreal-engine/using-chunkdownloader-for-patching-unreal-engine-games) can reduce the size of your core executable significantly by separating assets from binaries, but it is helpful to optimize your binary size as well.

This page provides a guide for the **Unreal Engine (UE)** tools that you can use to optimize your Android projects' binaries.

## Changes Since UE4

UE5 ships with updated compiler and linker flags that enable dead code elimination and identical code folding. Some UE4 code has been also rewritten for UE5 to reduce code bloat; this provides significant savings. These changes are enabled by default and do not require you to take any action.

## Advanced Optimizations

Other, more advanced binary optimizations are only available with specific Android SDK versions and must be manually activated. You can change your minimum SDK version in **Project Settings** > **Platforms** > **Android**, or you can change it in your `*Engine.ini` file:

```
	`[/Script/AndroidRuntimeSettings.AndroidRuntimeSettings]  	MinSDKVersion=23`
Copy full snippet
```
\[/Script/AndroidRuntimeSettings.AndroidRuntimeSettings\] MinSDKVersion=23

To enable advanced optimizations, add the following setting to your `*AndroidEngine.ini` file:

```
	`[/Script/AndroidRuntimeSettings.AndroidRuntimeSettings]  	bEnableAdvancedBinaryCompression = true`
Copy full snippet
```
\[/Script/AndroidRuntimeSettings.AndroidRuntimeSettings\] bEnableAdvancedBinaryCompression = true

After that, the optimizations available for your SDK version will be applied when packaging your project. These optimizations are summarized below.

### On Android SDK 23 or Higher

The following optimizations are available if your project's minimum Android SDK version is 23.

#### GNU Hash and Startup Time

Projects on SDK 23 and up use the new GNU hash ELF section instead of the previous format. This provides better performance and faster startup times.

#### APS Relocation Table Compression

Additionally, your project will take advantage of APS relocation table compression, an Android-specific compression format. In our tests, a relocation table with a size of 62 MB was reduced to roughly 8 MB using this format.

#### APK Compression and Direct Loading for .so Binaries

If you set your minimum SDK version to 23 or higher, Android OS can load `.so` binaries from your application's APK directly, eliminating the need to unpack and install them on the device separately from a compressed APK.

Unreal Engine enforces APK compression by default, but you can disable it with the following config variable in your `*Engine.ini` file:

```
	`[/Script/AndroidRuntimeSettings.AndroidRuntimeSettings]  	bExtractNativeLibs = false`
Copy full snippet
```
\[/Script/AndroidRuntimeSettings.AndroidRuntimeSettings\] bExtractNativeLibs = false

If you set `bExtractNativeLibs` to false, your application will load `.so` binaries directly and avoid compression. However, if your APK is under the Google Play Store's 150 MB cellular data limit, we recommend disabling this setting because Google Play Store's on-the-fly compression provides smaller file sizes than the zip compression in an APK and reduces cellular traffic caused by your application.

If you leave `bExtractNativeLibs` enabled, it will generate a smaller APK, but the OS will unpack it and install the `.so` binaries separately, effectively consuming more disk space. However, this is recommended for stores other than the Google Play Store.

### On Android SDK 28 or Higher

The following optimizations are available if your project's minimum Android SDK version is 28.

#### RELR Relocation Table Compression

Projects with a minimum SDK version of 28 or higher can take advantage of RELR relocation table compression, which is even more efficient than APS. For example, a 62 MB relocation table was reduced to roughly 600 KB when using RELR, which is a reduction of two orders of magnitude. RELR also provides higher performance than APS.
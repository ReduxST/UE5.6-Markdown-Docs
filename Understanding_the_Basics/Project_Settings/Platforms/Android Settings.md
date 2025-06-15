# Android Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/android-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/android-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:05:51

---

## Android

### APK Packaging

| **Setting** | **Description** |
| --- | --- |
| **Android Package Name ('com.Company.Project', \[PROJECT\] is replaced with project name)** | 
The official name of the product (same as the name you use on the Play Store website).

The name must have at least 2 sections separated by a period, and it must be unique.



 |
| **Store Version (1-2147483647)** | The version number used to indicate newer versions in the Store. |
| **Store Version Offset (ARMv7)** | Offset to add to store version for APKs generated for ARMv7. |
| **Store Version Offset (ARM64)** | Offset to add to store version for APKs generated for ARM64. |
| **Store Version Offset (x86\_64)** | Offset to add to store version for APKs generated for x86\_64. |
| **Application Display Name (app\_name), Project Name If Blank** | 

The application name displayed for end users (`app_name`).

If this field is left blank, the engine will use the project name.



 |
| **Version Display Name (usually x.y)** | The version displayed for end users. |
| **Minimum SDK Version (19=KitKat, 21=Lollipop)** | Sets what Android version the app is allowed to be installed on (do not set this lower than 19). |
| **Target SDK Version (19=KitKat, 21=Lollipop)** | Sets what OS version the app is expected to run on (do not set this lower than 19). |
| **Install Location** | 

Preferred install location for the application.

You can choose from the following options:

-   **Internal Only:** Install your app only on internal device storage.
-   **Prefer External:** Install your app on external storage when available.
-   **Auto:** Internal storage is preferred over external, unless the internal storage is low on space.



 |
| **Enable Lint Depreciation Checks** | Enable `-Xlint:unchecked` and `-Clint:depreciation` for Java compiling (Gradle only). |
| **Package Game Data Inside .apk** | 

Defines whether the data should be placed into the `.apk` file instead of a separate `.obb` file.

Amazon requires this to be enabled, but Google Play Store does not allow `.apk` files larger than 100 MB, so only small games will work with this setting enabled.



 |
| **Generate Install Files for All Platforms** | If enabled, both batch (`.bat`) files and shell script (`.command`) files will be generated, otherwise only done for the current system (default). |
| **Disable .obb Verification on First Start or Update** | Disable the verification of an `.obb` file when it is downloaded or on first start when in a distribution build. |
| **Force Small .obb Files** | If enabled, `.obb` file size is limited to 1 GB. |
| **Allow Large .obb Files** | If enabled, `.obb` file size is not limited to the 2 GB allowed by Google Play Store, but it is still limited to the 4 GB `.zip` limit. |
| **Allow Patch .obb File** | If enabled, a patch `.obb` is generated for files not fitting in the main `.obb`. This requires using multiple `.pak` files so split up content by chunk ID. |
| **Allow Overflow .obb Files** | If enabled, up to two additional overflow `.obb` files are generated for files not fitting in the patch `.obb`. This requires using multiple `.pak` files, so you should split up content by chunk ID. |
| **Use ExternalFilesDir for UnrealGame Files** | 

If enabled, UnrealGame files will be placed in `ExternalFilesDir` which is removed on uninstall.

You should also enable this if you need to save your game progress without requesting runtime `WRITE_EXTERNAL_STORAGE` permission in Android API 23+.



 |
| **Make Log Files Always Publicly Accessible** | 

If enabled, log files will always be placed in a publicly available directory (either `/sdcard/Android` or `/sdcard/UnrealGame`).

You may require `WRITE_EXTERNAL_STORAGE` permission if you do not use the `ExternalFilesDir` checkbox in Android API 23+.



 |
| **Orientation** | 

The permitted orientation of the application on the device.

You can choose from the following options:

-   **Portrait:** Portrait orientation (the display is taller than it is wide).
-   **Reverse Portrait:** Portrait orientation, rotated 180 degrees.
-   **Sensor Portrait:** Use either portrait or reverse portrait orientation, where supported by the device, based on the device orientation sensor.
-   **Landscape:** Landscape orientation (the display is wider than it is tall).
-   **Reverse Landscape:** Landscape orientation, rotated 180 degrees.
-   **Sensor Landscape:** Use either landscape or reverse landscape orientation, based on the device orientation sensor.
-   **Sensor:** Use any orientation the device normally supports, based on the device orientation sensor.
-   **Full Sensor:** Use any orientation (including ones the device wouldn't choose in Sensor mode), based on the device orientation sensor.



 |
| **Maximum Supported Aspect Ratio** | 

Maximum supported aspect ratio (width / height).

Android will automatically letterbox applications on devices with bigger aspect ratio.



 |
| **Use Display Cutout Region** | Enables use of the display cutout area on Android 9+. |
| **Restore Scheduled Notifications on Reboot** | 

Defines whether the scheduled local notification should be restored on reboot.

This will add a receiver for boot complete and a permission to the manifest.



 |
| **Enable Full Screen Immersive on KitKat and Above Devices** | Defines whether the software navigation buttons should be hidden or not. |
| **Enable Improved Virtual Keyboard** | 

If enabled, you can edit the text field directly.

If disabled, tapping the in-app text field will open the additional text field for editing.



 |
| **Preferred Depth Buffer Format** | 

The preferred depth buffer bitcount for Android.

You can choose from the following options:

-   **Default**
-   **16-bit**
-   **24-bit**
-   **32-bit**



 |
| **Validate Texture Formats** | Verifies that the device supports at least one of the cooked texture formats at runtime. |
| **Force Gradle to Compress Native Libs Regardless of MinSDKVersion Setting** | 

When building for MinSDKVersion >= 23, Gradle will leave native libs uncompressed in the `.apk`.

This option may be helpful for builds that are not intended to be distributed via Google Play.



 |
| **Enable Compression of Relocation Tables (Depends on MinSDKVersion Setting)** | Generates Android binary with RELR and APS2 relocation tables when building for MinSDKVersion >= 28 or just APS2 when building for MinSDKVersion >= 23. |
| **Status of Platform Setup File** | 

This shows whether the project is configured for the Android platform.

To users from 4.6 or earlier: The engine now generates an `AndroidManifest.xml` file when building, so if you have customized your `.xml` file, you will need to put all your changes into the below settings. Note that the engine doesn't make changes to your `AndroidManifest.xml` that is in your project directory.

The `.xml` file, generated by the engine, is placed in the `(YourProjectName)\Intermediate\Android\APK` folder.

Additionally, the engine no longer uses `SigningConfig.xml`, the settings are now set in the **Distribution Signing** section.

You must accept the SDK license agreement to use Gradle. You can do this from the Project Settings > Android window if the button isn't disabled.



 |
| **Accept SDK License** | The SDK license agreement must be accepted for Gradle usage. |
| **Build Folder** | The folder containing the build files in Explorer or Finder. We recommend checking these files in to the source control to share them with your team. |

### App Bundles

| **Setting** | **Description** |
| --- | --- |
| **Generate Bundle (AAB)** | Enables generating an AAB bundle. |
| **Generate Universal .apk from Bundle** | Enables generating a universal `.apk` from bundle. |
| **Enable ABI Split** | Separate ABIs into their own `.apk` files in bundle. |
| **Enable Language Split** | Separate resources by language into their own `.apk` in bundle. |
| **Enable Density Split** | Separate resources by density into their own `.apk` bundle. |

### Build

| **Setting** | **Description** |
| --- | --- |
| **Support OpenGL ES3.2** | Include shaders for devices supporting OpenGL ES 3.2 and above (default). |
| **Support Vulkan** | Support the Vulkan RHI and include Vulkan shaders. |
| **Support Vulkan Desktop / SM5 (Experimental)** | Enable Vulkan SM5 rendering support. |
| **Debug Vulkan Layer Directory** | Directory for Debug Vulkan Layers to package. |
| **Debug Vulkan Device Layers** | Debug Vulkan Device Layers to enable. |
| **Debug Vulkan Instance Layers** | Debug Vulkan Instance Layers to enable. |
| **Support Backbuffer Sampling on OpenGL** | 
Whether to render to an offscreen surface instead of rendering to backbuffer directly on Android OpenGL platform.

Enable this option if you want to support UMG background blur on Android OpenGL.



 |
| **Support ARM64 (also known as arm64-v8a)** | 

Defines whether to support ARM64 CPU architecture.

Use at least NDK r11c. This requires Lollipop (Android-21) minimum.



 |
| **Support x86\_64 (also known as x64)** | This requires GitHub source. |
| **Advanced** |   |
| **Detect Vulkan Device Support** | 

Defines whether to detect Vulkan device support by default if the project is packaged with Vulkan support.

If disabled, the `-detectvulkan` command line will enable Vulkan detection.



 |

### Advanced APK Packaging

| **Setting** | **Description** |
| --- | --- |
| **Extra Tags for Node** | Any extra tags for the node. |
| **Extra Tags for Node** | Any extra tags for the node. |
| **Extra Settings for Section (add newline character (\\n) to separate lines)** | 
Any extra settings for the section (an optional file, `<Project>/Build/Android/ManifestApplicationAdditions.txt`, will also be included).

Add a newline character (`\n`) to separate lines.



 |
| **Extra Tags for com.epicgames.unreal.GameActivity node** | Any extra tags for the com.epicgames.unreal.GameActivity node. |
| **Extra Settings for Section (add newline character (\\n) to separate lines)** | 

Any extra setting for the main section (an optional file, `<Project>/Build/Android/ManifestApplicationActivityAdditions.txt`, will also be included).

Add newline character (`\n`) to separate lines.



 |
| **Extra Permissions** | 

Any extra permissions your app needs (for example, 'android.permission.INTERNET').

An optional file, `<Project>/Build/Android/ManifestRequirementsAdditions.txt`, will also be included, or an optional file, `<Project>/Build/Android/ManifestRequirementsOverride.txt`, will replace the entire **Requirements** section.



 |
| **Add Permissions to Support Voice Chat** | Adds required permission to support voice chat (`RECORD_AUDIO`) |
| **Package for Oculus Mobile Device** | Package for an Oculus Mobile device. |
| **Remove Oculus Signature Files from Distribution .apk** | Removes Oculus Signature Files (`.osig`) from `.apk` file if Quest/Go `.apk` is signed for distribution, and enables entitlement checker. |

### Advanced Build

| **Setting** | **Description** |
| --- | --- |
| **Build with Hidden Symbol Visibility in Shipping Config (Experimental)** | 
Build the shipping config with hidden visibility by default.

This results in a smaller `.so` file, but will also remove symbols used to display call stack dumps.



 |
| **Always Save a Copy of the libUnreal.so With Symbols (Experimental)** | Always save `.so` file with symbols, allowing use of `addr2line` on raw call stack addresses. |
| **Force Linking to Use LD instead of LLD (Force LDLinker)** | Use legacy LD instead of new LLD linker. |

### Project SDK Override

Leave these fields blank to use global Android SDK project settings. Changing these settings will only affect this project.

| **Setting** | **Description** |
| --- | --- |
| **Build-Tools Version** | Which build-tools to package with (a specific version or `latest` for latest version on disk). |
| **SDK API Level** | Whick SDK to package and compile Java with (a specific version or `latest` for latest version on disk, or `matchndk` to match the NDK API Level). |
| **NDK API Level** | 
Whick NDK to compile with (a specific version or 'latest' for latest version on disk).

If you choose android-21 or later, your game won't run on pre-5.0 devices.



 |

### Distribution Signing

| **Setting** | **Description** |
| --- | --- |
| **Key Store** | This is the file that keytool outputs, specified with the `-keystore` parameter (file should be in `<Project>/Build/Android`). |
| **Key Alias** | This is the name of the key that you specified with the `-alias` parameter to keytool. |
| **Key Store Password** | 
This is the password that you specified for the keystore when running (either with `-storepass` or by typing it in).

This is Key Store password, not to be confused with Key password.



 |
| **Key Password** | 

This is the password for the key that you may have specified with keytool, if it's different from the keystore password.

Leave blank to use same password as Keystore.



 |
| **Android Developer Page on Signing for Distribution** | Opens a page that discusses the signing using keytool. |

### Google Play Services

| **Setting** | **Description** |
| --- | --- |
| **Request Access Token On Connect** | 
Enabling this adds `GET_ACCOUNTS` to the app manifest and requires user permission.

This is required to reset achievements.



 |
| **Achievement Map** | Mapping of game achievement names to IDs generated by Google Play. |
| **Leaderboard Map** | Mapping of game leaderboard names to IDs generated by Google Play. |
| **Enable Snapshots on Google Play Login (Experimental)** | Enabling this requests snapshots support for saved games during Google Play login. |
| **Google Cloud Messaging Sender ID** | 

The sender ID, obtained from Firebase Console. Associate this with your app in Google Player Developer Console.

Leave this field blank to disable it.



 |
| **Status of Platform Setup File** | This section shows whether the project is configured properly for the Google Play services platform. |
| **Android Developer Page on Google Play Services** | Opens a page that discusses Google Play Services. |
| **Enable Google Play Support** | Defines whether Google Play support should be enabled. |
| **Games App ID** | The app ID obtained from the Google Play Developer Console. |
| **Include AdMob Support for Ads** | 

Enabling this includes the AdMob SDK and will be detected by Google Play Console on APK upload.

Disable if you don't need ads to remove warnings.



 |
| **Ad Mob Ad Unit IDs** | Identifiers for ads obtained from AdMob. |
| **Google Play License Key** | The unique identifier for this application (needed for in-app purchases). |

### Icons

| **Setting** | **Description** |
| --- | --- |
| **Android Developer Page on Iconography** | Opens a page on Android Iconography. |
| **Icon** | Default app icon. |
| **LDPI Icon** | The app icon for low-density screens. |
| **MDPI Icon** | The app icon for medium-density screens. |
| **HDPI Icon** | The app icon for high-density screens. |
| **XHDPI Icon** | The app icon for extra-high-density screens. |

### Launch Images

The launch images will be scaled to fit the device in the active orientation. Additional optional launch images may be provided as overrides for LDPI, MDPI, HDPI, and XHDPI by placing them in the project's corresponding `Build/Android/res/drawable-*` directory.

| **Setting** | **Description** |
| --- | --- |
| **Show Launch Image** | Show the launch image as a startup splash screen. |
| **Download Background Vertical Image** | The Download Background image is used as the background when downloading OBB files. |
| **Download Background Horizontal Image** | The Download Background image is used as the background when downloading OBB files. |
| **Launch Portrait** | The Launch Portrait image is used as a splash screen for applications with Portrait, Reverse Portrait, Sensor Portrait, Sensor, or Full Sensor orientation. |
| **Launch Landscape** | The Launch Landscape image is used as a splash screen for applications with Landscape, Sensor Landscape, Reverse Landscape, Sensor, or Full Sensor orientation. |

### Graphics Debugger

| **Setting** | **Description** |
| --- | --- |
| **Enable Mali Perf Counters** | 
If enabled, this will disable the `security.perf_harden` flag on the Android device when launching or installing your app via the generated batch file.

Disabling `security.perf_harden` is necessary for HWCPipe to be able to report performance counters on Mali devices.



 |
| **Android Graphics Debugger** | 

Several Android graphics debuggers require configuration changes to be made to your application in order to operate.

Choosing an option from this menu will configure your project to work with that graphics debugger.

You can choose from the following options:

-   **None**
-   **Mali Graphics Debugger**
-   **Adreno Profiler**



 |

### Input

| **Setting** | **Description** |
| --- | --- |
| **Allow IMU Sampling** | 
Allows accelerometer, magnetometer, and gyroscope event handling.

Disabling this may improve performance.



 |
| **Allow Bluetooth Controllers** | If enabled, Bluetooth-connected controllers will send input. |
| **Block Android System Keys Being Sent from Controllers** | If enabled, controllers will not send `Android_Back` and `Android_Menu` events that might cause unnecessary or unwanted operations. |
| **Block Force Feedback on the Device When Controllers Are Attached** | Block force feedback on the device when controllers are attached. |

### Audio

| **Setting** | **Description** |
| --- | --- |
| **Encoding Format** | 
Android audio encoding options.

You can choose from the following options:

-   **Default:** Selects the default encoder.
-   **Ogg Vorbis:** Selects the OGG Vorbis encoding.
-   **ADCPM:** Selects ADCPM lossless encoding.



 |
| **Audio Mixer Sample Rate** | Sample rate to run the audio mixer with. |
| **Callback Buffer Size** | 

The amount of audio to compute each callback block.

Lower values decrease latency but may increase CPU cost.



 |
| **Number of Buffers To Enqueue** | 

The number of buffers to keep enqueued.

More buffers increase latency, but can compensate for variable compute availability in audio callbacks on some platforms.



 |
| **Max Channels** | 

The maximum number of channels (voices) to limit for this platform.

If you specify Max Channels both here and in your global audio quality settings, your application will use the smaller of the two values.

If this is set to 0, Unreal Engine will use all the channels available.



 |
| **Number of Source Workers** | 

The number of workers to use to compute source audio.

This only uses up to the maximum number of sources (Max Channels value) and evenly divides sources to each source worker.



 |
| **Compression Overrides** | See the [Compression Overrides](/documentation/en-us/unreal-engine/android-settings-in-the-unreal-engine-project-settings#compressionoverrides) table below. |
| **Cook Overrides** | See the [Cook Overrides](/documentation/en-us/unreal-engine/android-settings-in-the-unreal-engine-project-settings#cookoverrides) table below. |
| **Spatialization Plugin** | 

Defines which of the currently enabled spatialization plugins to use.

If you can't find a spatialization plugin you want to use in the dropdown menu, make sure its plugin is enabled (from the main menu, go to **Edit > Plugins**).

You can choose from the following options:

-   **Built-In Spatialization**
-   **Resonance Audio**
-   **Other**



 |
| **Reverb Plugin** | 

Defines which of the currently enabled reverb plugins to use.

If you can't find a reverb plugin you want to use in the dropdown menu, make sure its plugin is enabled (from the main menu, go to **Edit > Plugins**).

You can choose from the following options:

-   **Built-In Reverb**
-   **Resonance Audio**
-   **Other**



 |
| **Occlusion Plugin** | 

Defines which of the currently enabled occlusion plugins to use.

If you can't find an occlusion plugin you want to use in the dropdown menu, make sure its plugin is enabled (from the main menu, go to **Edit > Plugins**).

You can choose from the following options:

-   **Built-In Occlusion**
-   **Other**



 |
| **Sound Cue Cook Quality** | Quality level to cook SoundCues at (if set, all other levels will be stripped by the cooker). |

#### Compression Overrides

| **Setting** | **Description** |
| --- | --- |
| **Override Compression Times** | If enabled, overrides the Sound Group on each Sound Wave, and instead uses the Duration Threshold value to determine whether a sound should be fully decompressed during initial loading. |
| **Duration Threshold** | 
When **Override Compression Times** is enabled, any sound under this threshold (in seconds) will be fully decompressed on load.

Otherwise, the first chunk of this sound is cached at load and the rest is decompressed in real time.

If this is set to 0, will default to the Sound Group on the relevant Sound Wave.



 |
| **Maximum Branches on Random SoundCue Nodes** | 

On this platform, any random nodes on Sound Cues will automatically only preload this number of branches and dispose of any others on load.

This can drastically reduce memory usage.

If this is set to 0, no branches are culled.



 |
| **Quality Index for Sound Cues** | On this platform, use the specified quality at this index to override the quality used for SoundCues on this platform. |

Return to the [Audio](/documentation/en-us/unreal-engine/android-settings-in-the-unreal-engine-project-settings#audio) table.

#### Cook Overrides

| **Setting** | **Description** |
| --- | --- |
| **Resample for Device** | Enables audio resampling on this platform, using the given Resampling Quality Sample Rates. |
| **Compression Quality Modifier** | 
Scales all compression qualities when cooking to this platform.

For example, 0.5 will halve all compression qualities, and 1.0 will leave them unchanged.



 |
| **Stream Caching** | See the [Stream Caching](/documentation/en-us/unreal-engine/android-settings-in-the-unreal-engine-project-settings#streamcaching) table below. |
| **Resampling Quality** | See the [Resampling Quality](/documentation/en-us/unreal-engine/android-settings-in-the-unreal-engine-project-settings#resamplingquality) table below. |

Return to the [Audio](/documentation/en-us/unreal-engine/android-settings-in-the-unreal-engine-project-settings#audio) table.

##### Stream Caching

| **Setting** | **Description** |
| --- | --- |
| **Max Cache Size (KB)** | 
Determines the maximum amount of memory that should be used for the cache at any given time.

If set low (<= 8 MB), it lowers the size of individual chunks of audio during the cooking.



 |
| **Max Chunk Size Override (KB)** | This overrides the default maximum chunk size used when chunking audio for stream caching (ignored if < 0). |

Return to the [Cook Overrides](/documentation/en-us/unreal-engine/android-settings-in-the-unreal-engine-project-settings#cookoverrides) table.

##### Resampling Quality

| **Setting** | **Description** |
| --- | --- |
| **Max Sample Rate** | Resampling quality maximum sample rate. |
| **High Sample Rate** | Resampling quality high sample rate. |
| **Medium Sample Rate** | Resampling quality medium sample rate. |
| **Low Sample Rate** | Resampling quality low sample rate. |
| **Min Sample Rate** | Resampling quality minimum sample rate. |

Return to the [Cook Overrides](/documentation/en-us/unreal-engine/android-settings-in-the-unreal-engine-project-settings#cookoverrides) table.

### Multi-Texture Formats

| **Setting** | **Description** |
| --- | --- |
| **Include ETC2 Textures** | Include ETC2 textures when packaging with the Android (Multi) variant. |
| **Include DXT Textures** | Include DXT textures when packaging with the Android (Multi) variant. |
| **Include ASTC Textures** | Include ASTC textures when packaging with the Android (Multi) variant. |

### Texture Format Priorities

| **Setting** | **Description** |
| --- | --- |
| **ETC2 Texture Format Priority** | 
Priority for the ETC2 texture format when launching on device or packaging using Android\_Multi.

The highest priority format supported by the device will be used.

Default value is 0.2.



 |
| **DXT Texture Format Priority** | 

Priority for the DXT texture format when launching on device or packaging using Android\_Multi.

The highest priority format supported by the device will be used.

Default value is 0.6.



 |
| **ASTC Texture Format Priority** | 

Priority for the ASTC texture format when launching on device or packaging using Android\_Multi.

The highest priority format supported by the device will be used.

Default value is 0.9.



 |

### Misc

| **Setting** | **Description** |
| --- | --- |
| **Stream landscape visual mesh LODs** | 
Defines whether to enable LOD streaming for landscape visual meshes.

Only supported on feature level ES3.1 or above.



 |
| **Enable DOM storage for WebViews** | Enables WebViews to use the DOM storage API. |
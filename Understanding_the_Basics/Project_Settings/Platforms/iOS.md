# iOS

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ios-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/ios-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:31:51

---

## iOS

### Mobile Provision

By default, Unreal Engine scans all available mobile Provisioning Profiles and Certificates (supplied by Apple) on your computer and automatically chooses which ones to use.

You can override that behavior by selecting the Provisioning Profiles and Certificates in the following settings.

| **Setting** | **Description** |
| --- | --- |
| **Import Provision** | Select the Provisioning Profiles for your application here. |
| **Import Certificate** | Select the Certificate for your application here. |

### Bundle Information

Note to users from 4.6 or earlier: The engine now generates an `Info.plist` file when building, so if you have customized your `.plist` file, you will need to transfer all of your changes into the settings below. Note that the engine doesn't change the `.plist` file that is in your project directory, so you can use it as a reference.

| **Setting** | **Description** |
| --- | --- |
| **Bundle Display Name** | 
Specifies the display name for the application.

This displays under the icon on the device.



 |
| **Bundle Name** | 

Specifies the name of the application bundle.

This is the short name for the application bundle.



 |
| **Bundle Identifier** | Set a Bundle Identifier (Bundle ID) for unique identification of your app in the App Store. |
| **Version Info** | Specifies the version for the application. |

### Orientation

| **Setting** | **Description** |
| --- | --- |
| **Supports Portrait Orientation** | 
Support default portrait orientation.

Landscape will not be supported.



 |
| **Supports Upside Down Orientation** | 

Support upside-down orientation.

Landscape will not be supported.



 |
| **Supports Landscape Left Orientation** | 

Supports left landscape orientation.

If you select this, portrait orientation will not be supported.



 |
| **Supports Landscape Right Orientation** | 

Supports right landscape orientation.

If you select this, portrait orientation will not be supported.



 |
| **Preferred Landscape Orientation** | 

The Preferred Orientation will be used as the initial orientation at launch when both Landscape Left and Landscape Right orientations are supported.

You can choose from the following options:

-   **Landscape (left Home button)**
-   **Landscape (right Home button)**



 |

### Input

| **Setting** | **Description** |
| --- | --- |
| **Can the Game Have Multiple Gamepads Connected at a Single Time** | If enabled, the game will be able to handle multiple gamepads at the same time (the Siri Remote is a gamepad). |
| **Allow AppleTV Remote Landscape Mode** | If enabled, the Siri Remote can be rotated to landscape view. |
| **Use AppleTV Remote Absolute Trackpad Values** | 
If enabled, the center of the trackpad is `0,0` (center) for the virtual joystick.

If disabled, the location the user taps becomes `0,0`.



 |
| **Allow MFi (Bluetooth) Controllers** | If enabled, Bluetooth connected controllers will send input. |
| **Block Force Feedback on the Device When Controllers Are Attached** | Block force feedback on the device when controllers are attached. |
| **Disable Motion Controls** | 

Disables usage of device motion data.

If the application doesn't use motion data, disabling this option will improve battery life.



 |
| **Use Integrated Keyboard** | Defines whether or not the keyboard should be usable on its own without a `UITextField`. |

### File System

| **Setting** | **Description** |
| --- | --- |
| **Support iTunes File Sharing** | Defines whether files created by the app will be accessible from the iTunes File Sharing feature. |
| **Support Files App** | Defines whether files created by the app will be accessible from within the device's Files app (requires iTunes File Sharing). |

### Rendering

| **Setting** | **Description** |
| --- | --- |
| **Use Fast-Math Intrinsics** | 
Whether to use the Metal shading language's "fast" intrinsics.

Fast intrinsics assume that no `NaN` or `INF` value will be provided as input, so they are more efficient.

However, they will produce undefined results if `NaN` / `INF` is present in the arguments.



 |
| **Force 32-bit Floating Point Precision** | 

Defines whether to force Metal shaders to use 32-bit floating point precision even when the shader uses half-floats.

Half-floats are much more efficient (when they are available), but have less accuracy over large ranges. Some projects may need to use 32-bit floats to ensure correct rendering.



 |
| **Enable Fast-Math Optimizations** | 

Defines whether to use Metal shader-compiler's `-ffast-math` optimizations.

Fast-Math performs algebraic-equivalent and reassociative optimizations not permitted by the floating point arithmetic standard (IEEE-754).

These can improve shader performance at some cost to precision and can lead to NaN/INF propagation as they rely on shader inputs or variables not containing `NaN` / `INF` values.

By default, Fast-Math is enabled for performance.



 |
| **Tier of Indirect Argument Buffers to Use When Compiling Shaders** | Defines whether to compile shaders using a tier Indirect Argument Buffers. |
| **Support Apple A8** | Enables the support of Apple A8 devices and disables 3D texture compression. |
| **Metal Mobile Renderer** | Whether to compile iOS Metal shaders for the Mobile renderer (requires iOS 8+ and an A7 processor). |
| **Metal Desktop Renderer** | Whether to compile iOS Metal shaders for the desktop renderer (requires iOS 10+ and an A10 processor). |
| **Metal Shader Standard To Target** | 

The Metal shader language version to use when compiling the shaders.

You can choose from the following options:

-   **Minimum, Currently v2.3 (iOS 14.0 / tvOS 14.0)**
-   **Metal v2.3 (iOS 14.0 / tvOS 14.0)**
-   **Metal v2.4 (iOS 15.0 / tvOS 15.0)**



 |

### OS Info

| **Setting** | **Description** |
| --- | --- |
| **Minimum iOS Version** | 
Defines the minimum iOS version the app supports.

You can choose from the following options:

-   **14.0**
-   **15.0**



 |

### Power Usage

| **Setting** | **Description** |
| --- | --- |
| **Frame Rate Lock** | 
Sets the maximum frame rate to save on power consumption.

You can choose from the following options:

-   **None:** Frame rate is not limited.
-   **20 FPS:** Frame rate is limited to a maximum of 20 frames per second.
-   **30 FPS:** Frame rate is limited to a maximum of 30 frames per second.
-   **60 FPS:** Frame rate is limited to a maximum of 60 frames per second.

You can also edit the config values of this property.



 |
| **Enable Dynamic Max FPS** | 

When enabled, the engine will take the `MaxRefreshRate` from the device instead of a constant (20, 30 or 60 FPS) in the `IOSPlatform/framePacer` class.

You can also edit the config values of this property.



 |

### Devices

| **Setting** | **Description** |
| --- | --- |
| **Supports IPad** | Whether to add support for iPad devices. |
| **Supports IPhone** | Whether to add support for iPhone devices. |

### Build

| **Setting** | **Description** |
| --- | --- |
| **Build Project as a Framework (Experimental)** | Defines whether to build the iOS project as a framework. |
| **Override Location of Metal Toolchain** | When using Windows to compile Metal shaders, use this to override the default install location of the Apple's Metal developer tools for Windows. |
| **Generate dSYMs for Code Debugging and Profiling** | Enables generation of dSYM file. |
| **Generate dSYMs as a Bundle for Third Party Crash Tools** | Enables generation of dSYM bundle. |
| **Generate .udebugsymbols File** | 
Enable generation of a `.udebugsymbols` file, which allows offline, platform-independent symbolication for the Malloc Profiler or external crash reporting tools.

Requires a dSYM file or bundle.



 |
| **Generate Xcode Archive Package** | Enable generation of Xcode archive package. |
| **Support Bitcode in Shipping** | 

Defines whether to enable Bitcode compiling.

The support of this feature by Apple will soon be dropped.



 |
| **Enable Advertising Identifier (IDFA)** | Enable the Advertising Identifier (see more information in [Apple's developer documentation](https://developer.apple.com/documentation/adsupport/asidentifiermanager/1614151-advertisingidentifier)). |
| **Additional Non-Shipping Linker Flags** | 

Any additional linker flags to pass to the linker in non-shipping builds.

You can also edit the config values of this property.



 |
| **Additional Shipping Linker Flags** | 

Any additional linker flags to pass to the linker in shipping builds.

You can also edit the config values of this property.



 |
| **Override Existing SSH Permissions File** | 

The path of the SSH permissions key to be used when connecting to the remote server.

You can also edit the config values of this property.



 |
| **Support User Switching on tvOS** | 

Defines whether the app should be compatible with the Multi-User feature on tvOS.

If enabled, the game will shut down with the typical exit flow.



 |
| **Dev Center Username** | 

The username or email to use when logging in to DevCenter with Turnkey.

This can be overridden in Turnkey with `RunUAT Turnkey -command=ManageSettings`.

This value is stripped out when making builds.

You can also edit the config values of this property.



 |
| **Dev Center Password** | 

The password to use when logging in to DevCenter with Turnkey.

This password is saved in plaintext and is meant for shared accounts.

This value is stripped out when making builds.

You can also edit the config values of this property.



 |
| **Remote Build Options** |   |
| **Remote Server Name** | 

The name or IP address of the remote Mac which will be used to build iOS.

You can also edit the config values of this property.



 |
| **RSync User Name** | 

Username on the Remote Server for remote builds using RSync.

Should match the username used for SSH Private Key generation.

You can also edit the config values of this property.



 |
| **Remote Server Override Build Path** | 

Optional path on the remote Mac where the build files will be copied.

If blank, `~/UE5/Builds` will be used.

You can also edit the config values of this property.



 |
| **Found Existing SSH Permissions File** | The existing location of an SSH key found by Unreal Engine. |
| **Cw Rsync Install Path** | 

The install directory of cwRsync.

You can also edit the config values of this property.



 |
| **Generate SSH Key** | Select this to generate the SSH key. |

### Online

| **Setting** | **Description** |
| --- | --- |
| **Enable Game Center Support** | 
Defines whether to enable Game Center support (iOS Online Subsystem).

You can also edit the config values of this property.



 |
| **Enable Cloud Kit Support** | Defines whether to enable the Cloud Kit support (iOS Online Subsystem). |
| **iCloud Save Files Sync Strategy** | 

Strategy to use for reading from iCloud save files.

You can choose from the following options:

-   **Never (do not use iCloud for Load / Save Game):** Only at game start.
-   **At Game Start Only (iOS):** Only at game start.
-   **Always (whenever LoadGame is called).**



 |
| **Enable Background Fetch** | Defines whether to enable background fetch support. |
| **Enable Facebook Support** | Defines whether the app supports Facebook. |
| **Facebook App ID** | 

Facebook App ID obtained from [Facebook's Developer Center](https://developers.facebook.com/apps/).

You need a Facebook Developer account for this.



 |
| **Allow Web Connections to Non-HTTPS Websites** | Defines whether to allow web connections to websites that do not use HTTPS. |
| **Enable Remote Notifications Support** | 

Enable remote notifications support.

This requires GitHub source.



 |

### Extra PList Data

| **Setting** | **Description** |
| --- | --- |
| **Additional Plist Data** | 
Any additional plist key/value data.

Add a newline character `\n` to separate lines.



 |

### Required Icons

| **Setting** | **Description** |
| --- | --- |
| **Marketing Icon (1024x1024)** | 
The `.png` icon of the size of 1024x1024px, used in the AppStore.

Other icons sizes can be generated from the Marketing Icon.



 |
| **Default iPhone Icon (120x120)** | The `.png` icon used as a default for iPhone. |
| **Default iPad Icon (152x152)** | The `.png` icon used as a default for iPad. |
| **iPad Pro Retina App Icon (167x167)** | The higher-resolution version of the **Default iPad App Icon**. |

### Optional Icons

| **Setting** | **Description** |
| --- | --- |
| **3x iPhone App Icon (180x180)** | 3x iPhone App Icon (180x180) |
| **3x iPhone Spotlight Icon (120x120)** | 3x iPhone Spotlight Icon (120x120) |
| **Default Spotlight Icon (80x80)** | Default Spotlight Icon (80x80) |
| **3x iPhone Settings Icon (87x87)** | 3x iPhone Settings Icon (87x87) |
| **Default Settings Icon (58x58)** | Default Settings Icon (58x58) |
| **3x iPhone Notification Icon (60x60)** | 3x iPhone Notification Icon (60x60) |
| **Default Notification Icon (40x40)** | Default Notification Icon (40x40) |

### Launch Screen

| **Setting** | **Description** |
| --- | --- |
| **Custom Launchscreen Storyboard (Experimental)** | 
Choose whether to use a custom LaunchScreen.

To use this option, create a storyboard in Xcode and copy it in `Build/IOS/Resources/Interface` under your Project folder. Name it `Launchscreen.storyboard`.

This will be compiled and copied to the bundle app, and the Launch screen image above will not be included in the app.

When using assets in your custom `LaunchScreen.storyboard`, add them in `Build/IOS/Resources/Interface/Assets` and they will be included.



 |
| **Launch Screen Image** | 

This image is used for the Launch Screen when custom launch screen storyboards are not in use.

This image is used in both portrait and landscape modes and will be scaled to occupy the full width or height for all devices, so if your app supports both, a square image is recommended.

The `.png` file supplied must not have an alpha channel.



 |

### TvOS

| **Setting** | **Description** |
| --- | --- |
| **Icon Large Back (1280x768)** | Icon Large Back (1280x768) |
| **Icon Large Front (1280x768)** | Icon Large Front (1280x768) |
| **Icon Large Middle (1280x768)** | Icon Large Middle (1280x768) |
| **Icon Small Back (400x240)** | Icon Small Back (400x240) |
| **Icon Small Front (400x240)** | Icon Small Front (400x240) |
| **Icon Small Middle (400x240)** | Icon Small Middle (400x240) |
| **Top Shelf (1920x720)** | Top Shelf (1920x720) |
| **Top Shelf (6840x1440)** | Top Shelf (6840x1440) |
| **Top Shelf Wide (2320x720)** | Top Shelf Wide (2320x720) |
| **2x Top Shelf Wide (4640x1440)** | 2x Top Shelf Wide (4640x1440) |

### Audio

| **Setting** | **Description** |
| --- | --- |
| **Audio Mixer Sample Rate** | Sample rate to run the audio mixer with. |
| **Callback Buffer Size** | 
The amount of audio to compute each callback block.

Lower values decrease latency but may increase CPU cost.



 |
| **Number of Buffers To Enqueue** | 

The number of buffers to keep enqueued.

A larger number of buffers will increase latency but can compensate for variable compute availability in audio callbacks on some platforms.



 |
| **Max Channels** | 

The maximum number of channels (voices) to limit for this platform.

If you specify Max Channels both here and in your global audio quality settings, your application will use the smaller of the two values.

If this is set to 0, Unreal Engine will use all the channels available.



 |
| **Number of Source Workers** | 

The number of workers to use to compute source audio.

Will only use up to the maximum number of sources (**Max Channels** value).

Will evenly divide sources to each source worker.



 |
| **Compression Overrides** | See the [Compression Overrides](/documentation/en-us/unreal-engine/ios-settings-in-the-unreal-engine-project-settings#compressionoverrides) table below. |
| **Cook Overrides** | See the [Cook Overrides](/documentation/en-us/unreal-engine/ios-settings-in-the-unreal-engine-project-settings#cookoverrides) table below. |
| **Spatialization Plugin** | 

Defines which of the currently enabled spatialization plugins to use.

If your desired spatialization isn't found in the dropdown menu, make sure it's enabled in the Plugins window (main menu: **Edit > Plugins**).

You can choose from the following options:

-   **Built-In Spatialization**
-   **Resonance Audio**
-   **Other**



 |
| **Reverb Plugin** | 

Defines which of the currently enabled reverb plugins to use.

If your desired reverb plugin isn't found in the dropdown menu, make sure it's enabled in the Plugins window (main menu: **Edit > Plugins**).

You can choose from the following options:

-   **Built-In Reverb**
-   **Resonance Audio**
-   **Other**



 |
| **Occlusion Plugin** | 

Defines which of the currently enabled occlusion plugins to use.

If your desired occlusion plugin isn't found in the dropdown menu, make sure it's enabled in the Plugins window (main menu: **Edit > Plugins**).

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

If set to 0, will default to the Sound Group on the relevant Sound Wave.



 |
| **Maximum Branches on Random SoundCue Nodes** | 

On this platform, any random nodes on Sound Cues will automatically only preload this number of branches and dispose of any others on load.

This can drastically reduce memory usage.

If set to 0, no branches are culled.



 |
| **Quality Index for Sound Cues** | On this platform, use the specified quality at this index to override the quality used for SoundCues. |

Return to the [Audio](/documentation/en-us/unreal-engine/ios-settings-in-the-unreal-engine-project-settings#audio) table.

#### Cook Overrides

| **Setting** | **Description** |
| --- | --- |
| **Resample for Device** | Enables audio resampling on this platform using the given Resampling Quality Sample Rates. |
| **Compression Quality Modifier** | 
Scales all compression qualities when cooking to this platform.

For example, 0.5 will halve all compression qualities, and 1.0 will leave them unchanged.



 |
| **Stream Caching** | See the [Stream Caching](/documentation/en-us/unreal-engine/ios-settings-in-the-unreal-engine-project-settings#streamcaching) table below. |
| **Resampling Quality** | See the [Resampling Quality](/documentation/en-us/unreal-engine/ios-settings-in-the-unreal-engine-project-settings#resamplingquality) table below. |

Return to the [Audio](/documentation/en-us/unreal-engine/ios-settings-in-the-unreal-engine-project-settings#audio) table.

##### Stream Caching

| **Setting** | **Description** |
| --- | --- |
| **Max Cache Size (KB)** | 
This determines the maximum amount of memory that should be used for the cache at any given time.

If set low (<= 8 MB), it lowers the size of individual chunks of audio during cooking.



 |
| **Max Chunk Size Override (KB)** | This overrides the default maximum chunk size used when chunking audio for stream caching (ignored if < 0). |

Return to the [Cook Overrides](/documentation/en-us/unreal-engine/ios-settings-in-the-unreal-engine-project-settings#cookoverrides) table.

##### Resampling Quality

| **Setting** | **Description** |
| --- | --- |
| **Max Sample Rate** | Resampling quality maximum sample rate. |
| **High Sample Rate** | Resampling quality high sample rate. |
| **Medium Sample Rate** | Resampling quality medium sample rate. |
| **Low Sample Rate** | Resampling quality low sample rate. |
| **Min Sample Rate** | Resampling quality minimum sample rate. |

Return to the [Cook Overrides](/documentation/en-us/unreal-engine/ios-settings-in-the-unreal-engine-project-settings#cookoverrides) table.

### Misc

| **Setting** | **Description** |
| --- | --- |
| **Stream Landscape Visual Mesh LODs** | Defines whether to enable LOD streaming for landscape visual meshes. |
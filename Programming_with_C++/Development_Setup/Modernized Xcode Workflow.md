# Modernized Xcode Workflow

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-modern-xcode-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-modern-xcode-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:05

---

**Unreal Engine (UE)** from 5.3 onward updates the Xcode project workflow for Unreal Engine to be more consistent with standard Xcode app projects. The new project setup improves organization and quality of life for Xcode developers and provides access to several tools within Xcode to streamline codesigning and provisioning, including:

-   Automatic Code-Signing
    
-   Managing entitlements
    
-   Editing `.plist` files
    
-   Standard Xcode framework handling
    

This page overviews the changes for users transitioning to UE 5.3 and newer (5.3+) from earlier versions.

## Prerequisites

The updated Xcode workflow is available for UE 5.3 and newer, and is enabled by default for new projects. If you need to enable it manually, however, follow these steps:

1.  Open your engine's install directory, open `Engine/Config/BaseEngine.ini`, and make sure that you set the following config variable:
    
    Engine/Config/BaseEngine.ini
    
    C++
    
    `[/Script/MacTargetPlatform.XcodeProjectSettings]      bUseModernXcode=true`
    
    \[/Script/MacTargetPlatform.XcodeProjectSettings\] bUseModernXcode=true
    
    Copy full snippet(2 lines long)
    
2.  Regenerate your Xcode project files for both the engine and your project. If you are using a source build of UE, run the `GenerateProjectFiles.command` script in your engine install directory to regenerate the project files for UE's source code. You should see three Xcode workspace files in your project's directory:
    
    -   `UE5 (Mac).xcworkspace`
        
    -   `UE5 (TVOS).xcworkspace`
        
    -   `UE5 (IOS).xcworkspace`
        

The new Xcode setup is now ready to use. The following sections explain what's new compared to the old project setup.

## Projects, Schemes, and Build Configurations

Previously, UE Xcode projects combined **targets** and **build configurations** under **Schemes**. For example, under a single project (MyProject), users had a "Development Editor" scheme that built a Development build of an Editor target.

UE 5.3+ provides a separate Xcode project (within the same Xcode workspace) for each target type. For example, an Xcode workspace for a project titled "MyProject" would have a separate project for MyProjectEditor, MyProjectGame, MyProjectClient, and MyProjectServer.

[![Separate projects for Client, Editor, Game, and Server.](https://dev.epicgames.com/community/api/documentation/image/bc4aea7a-e1a7-4a5a-bfbb-6c6275706d61?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bc4aea7a-e1a7-4a5a-bfbb-6c6275706d61?resizing_type=fit)

Each target has only the build configurations it supports. For example, most editors do not support Test or Shipping configuration, so they are unavailable under Editor projects.

[![Build Configuration](https://dev.epicgames.com/community/api/documentation/image/5464288a-dcf7-41ed-9fa0-61ee8c67dae7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5464288a-dcf7-41ed-9fa0-61ee8c67dae7?resizing_type=fit)

Updated workspaces have a large number of schemes. When looking through them, use the Filter and the Recent section to narrow your list as needed.

[![Schemes list](https://dev.epicgames.com/community/api/documentation/image/339e6914-8137-4653-a828-a9db526d05d1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/339e6914-8137-4653-a828-a9db526d05d1?resizing_type=fit)

## Per-Platform Workspaces

Previously, when UE generated project files, it created one monolithic workspace that included targets for each of Apple's platforms.

In UE 5.3+, when UE generates project files, it creates a separate workspace for each Apple platform.

[![Xcode workspaces](https://dev.epicgames.com/community/api/documentation/image/9818c8f3-a160-4468-93bc-5bc15a278d48?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9818c8f3-a160-4468-93bc-5bc15a278d48?resizing_type=fit)

This simplifies workspaces and projects, and since Xcode can open multiple workspaces, you can toggle between platforms by pressing Command + \` (backtick).

Each workspace only contains the targets that support that platform, so iOS and tvOS have fewer schemes available. They do have an UnrealEditor target, but it can't successfully build. Instead, these targets are present to make the source code available for searching.

## Self-Contained Apps

Previously, UE bundled all the data needed to run iOS, iPadOS, and tvOS apps into their respective `.app` files, making them self-contained. However, macOS projects split the data between the `.app`, the `Saved/Cooked/Mac` directory, and other locations in the Engine and Project directories.

In UE 5.3+, all Mac platforms use the same workflow, which gathers the needed data into one location and bundles it into a .app that you can run manually or with Xcode. To do this, you need to use the Stage step in the cooking process.

Editor builds are still uncooked and contained in loose folders.

## Package and Distribute

The packaging processes for macOS and iOS/tvOS/iPadOS are now fully consistent with one another.

UE no longer generates an .ipa file for iOS automatically, as it is not necessary on macOS and only useful on Windows.

### Distribution

Distribution mode no longer codesigns using a Distribution certificate. Instead, it creates a standard Xcode archive (`.xcarchive`), which you can use to distribute the `.app` to various destinations, such as the App Store or your team. When making distribution builds, Xcode also generates a `.dSYM` file to put into the Xcode archive, which is useful for debugging crashes and can be sent to Apple for debugging live crashes. You submit your `.dysm` alongside your app when uploading your app to Apple for submission.

`.dSYM` generation will take several minutes.

To package normally, click **Platforms** > **Package Project** in Unreal Editor, or add `-package -clientconfig=Shipping` to your BuildCookRun command line.

To package for distribution, check the **Distribution** check box in your Project Settings, or add `-package -clientconfig=Shipping -distribution` to your BuildCookRun command line.

Alternatively, you can click **Product** \> **Archive** in Xcode.

[![The Product / Archive button highlighted in Xcode](https://dev.epicgames.com/community/api/documentation/image/3308158e-ad27-4416-9766-dd7979447f6e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3308158e-ad27-4416-9766-dd7979447f6e?resizing_type=fit)

Xcode uses the standard flow to generate a `.xcarchive`, including bringing in the Staged directory and codesign frameworks. This uses the Shipping configuration, even if you set the scheme to Development.

If you use Archive in Xcode, it automatically opens the Archives window and selects the new archive. If you use other UE methods to create it, you have to manually open the window by clicking **Window > Organizer**, then select your project and Archives in the upper left.

[![Xcode archives listed in Xcode](https://dev.epicgames.com/community/api/documentation/image/205c970a-650d-48fd-ade3-27d6a0ea7ddc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/205c970a-650d-48fd-ade3-27d6a0ea7ddc?resizing_type=fit)

Use the buttons on the right of the **Archives window** to **Validate** or **Distribute** your app. You can use this to create an iOS `.ipa` file for internal usage by following the prompts for each option. For App Store validation/distribution, you must make an App entry at [appstoreconnect.apple.com](https://appstoreconnect.apple.com/).

[![The Distribute and Vlaidate App buttons](https://dev.epicgames.com/community/api/documentation/image/f30f1300-97a6-4d27-8436-bed6c8e3948c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f30f1300-97a6-4d27-8436-bed6c8e3948c?resizing_type=fit)

The prompts for distributing or validating your app may require you to choose a Distribution certificate or follow other provisioning steps. Refer to [Apple's documentation](https://developer.apple.com/documentation/xcode/distribution) for more information.

Archiving in Xcode uses Shipping because it is the default configuration for the Archive action in the scheme UE generates. Additionally, `-package -distribution` will use the `archive` Xcode action in the background instead of the `build` action.

[![Archiving shipping projects](https://dev.epicgames.com/community/api/documentation/image/1ecc3a13-2ca2-417d-a1fb-1678a73d2393?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1ecc3a13-2ca2-417d-a1fb-1678a73d2393?resizing_type=fit)

You can change this in the Scheme if needed for testing, but we recommend only distributing Shipping builds.

### Configure Your App's Display Name on MacOS

Your app's **display name** is the name of the Mac `.app` when making an archived build. When you package for distribution (or using Archive menu in Xcode), the display name is the name of the `.app` that users see when using Finder. If this is not set, the `.app` will have the same name as the `.uproject` file. To change your display name in UE 5.3.2 and newer, open your `MacEngine.ini` file and set the `ApplicationDisplayName` config variable:

MacEngine.ini

C++

`[Xcode] 	ApplicationDisplayName="Friendly Application Name"`

\[Xcode\] ApplicationDisplayName="Friendly Application Name"

Copy full snippet(2 lines long)

The `ApplicationDisplayName` is not the same as the bundle display name used for iOS, and you need to configure these separately for apps running on both MacOS and iOS.

## Content/Blueprint-Only Projects

Because content-only (or Blueprint-only) projects do not have an Xcode project or build target source files, they re-use the generic UnrealGame targets from the engine combined with their project-specific data to create a build.

## Standard Xcode Practices

The updated Xcode workflow uses Xcode to handle as many components according to the standard Xcode workflow as possible, including:

-   Codesigning.
    
-   `.plist` files.
    
-   Entitlements files.
    
-   Frameworks.
    

### Codesigning

Previously, only iOS/iPadOS/tvOS required codesigning. As of 2023, Apple also requires codesigning for macOS. The updated workflow uses Xcode's **Automatic Codesigning** for all platforms by default.

To use Automatic Codesigning, follow these steps:

1.  Log into your Apple Developer Account in Xcode.
    
2.  Open your Project Settings, then locate Platforms > Xcode Projects and set the following properties:
    
    [![Project settings for Xcode Projects](https://dev.epicgames.com/community/api/documentation/image/c9192316-9540-4fb6-82de-1400faaeafdf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c9192316-9540-4fb6-82de-1400faaeafdf?resizing_type=fit)
    

| Setting Name | CVar | Description |
| --- | --- | --- |
| 
Use Modern Code Signing

 | 

`bUseModernCodeSigning`

 | 

Enables Automatic Codesigning for your UE project. Requires the following two settings to be set.

 |
| 

Modern Signing Prefix

 | 

`ModernSigningPrefix`

 | 

A reverse domain name for your company. For example: `com.epicgames`. UE combines this with the project's name to create the bundle ID for your game unless you override this in a plist. See Metadata below for details.

 |
| 

Modern Signing Team

 | 

\`ModernSigningTeam

 | 

The Team ID your application uses when signing. This is the same as the Team ID in Xcode's Signing and Capabilities section. See Find Your Team ID below for more details.

 |

### Find Your Team ID

To find your Team ID for the Modern Signing Team setting, open the [Apple Developer Page](https://developer.apple.com/account), log into your account, and click **Membership Details**. Your Team ID is displayed.

[![Team ID setting in Xcode](https://dev.epicgames.com/community/api/documentation/image/6b8c6061-5916-4d2f-a43b-5265d7b4dab9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6b8c6061-5916-4d2f-a43b-5265d7b4dab9?resizing_type=fit)

### .plist Files

Every app needs to include an embedded `.plist` file. The final `.plist` file is usually made from a partial (template) that Xcode will modify based on Xcode project settings. Due to UE generating Xcode projects, this can be a complicated process.

The updated Xcode workflow provides high-level control over `.plist` file handling. Additionally, editing of the `.plist` settings in Xcode is now supported

By default, you will lose iOS changes if you edit the `.plist` settings. See the MacOS vs iOS section below for more details.

#### Template vs Premade

It is preferred for Xcode to finalize the `.plist` in the app using settings from the UE-generated Xcode project. However, UE also supports premade `.plist` files that Xcode will not modify. Because this is an advanced feature, it is not exposed in the Xcode Project Settings and requires editing a config file. Refer to Use a Premade `.plist` below for instructions.

The `.plist` settings in your Project Settings (the `Mac Target Info.plist` and `IOS Target Info.plist` items) provide a way to specify either the default Template `.plist`, or your own custom Template `.plist`.

The default locations for the `Template.plist` files are in your project's `Build/IOS` directory. When UE generates Xcode project files for your project, it will look to see if you have a Template `.plist` file in your project, and if it is not present, it will copy a `.plist` from the engine into your project folder.

If you edit `.plist` settings in the Xcode, and it points to a `.plist` file in your UE install directory (as opposed to your project's directory), then Xcode will mark it writable and modify it, and all UE projects using that installation will be affected. This is why UE copies the engine's `.plist` file into your project. You may want to compare future engine versions' `.plist` file to see if we have updated the default settings.

If this happens, refer to the instructions on how to Restore a .plist to Default below.

The UnrealEditor target has a unique `.plist`, as the `.app` is shared across all projects. This is something most users will not have to deal with.

##### Use a Premade .plist

If you want to use a premade `.plist`, modify your `DefaultEngine.ini` file, and set one or both of the following settings with paths to the files you want to use:

DefaultEngine.ini

C++

`[/Script/MacTargetPlatform.XcodeProjectSettings] 	PremadeMacPlist=(FilePath="/Game/Build/Mac/Resources/MyGameMac.plist") 	PremadeIOSPlist=(FilePath="/Game/Build/IOS/Resources/MyGameIOS.plist")`

\[/Script/MacTargetPlatform.XcodeProjectSettings\] PremadeMacPlist=(FilePath="/Game/Build/Mac/Resources/MyGameMac.plist") PremadeIOSPlist=(FilePath="/Game/Build/IOS/Resources/MyGameIOS.plist")

Copy full snippet(3 lines long)

#### Restore a .plist to Default

You can also use the **Restore Info.plist to default** button to re-copy the Engine directory's Mac default Template `.plist` file to your project, and set the values appropriately. This can be useful if you want to use updated default `.plist` files in future UE versions.

You can take a `.plist` file out of a generated app and use that as the source for a premade `.plist`.

#### Privacy Manifests

Xcode uses **Privacy Manifests** to summarize what kind of data your app collects about its users and why it collects that data. This includes data collected by your own code as well as third-party SDKs you are using. When you distribute your app, Xcode combines the privacy manifests for your SDKs and your app into a single privacy report, making it easy to provide users with transparent information about your app's privacy practices.

UE provides default privacy manifests in the following locations:

-   **MacOS**: `Engine/Build/Mac/Resources/UEMetadata/PrivacyInfo.xcprivacy`
    
-   **iOS, tvOS, and iPadOS**: `Engine/Build/iOS/Resources/UEMetadata/PrivacyInfo.xcprivacy`
    

Projects using additional privacy functions need to provide an additional `PrivacyInfo.xcprivacy` file in the location specified by their UE project settings. By default, these are:

-   **MacOS**: `/Game/Build/Mac/Resources/PrivacyInfo.xcprivacy`
    
-   **iOS, tvOS, and iPadOS**: `/Game/Build/IOS/Resources/PrivacyInfo.xcprivacy`
    

For more information, refer to [Apple's documentation on Privacy Manifests](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests).

#### MacOS vs. iOS

Working with .plist files differs between macOS and iOS in the new Xcode workflow because UBT has deeply-embedded logic for generating iOS `.plist` files. Bringing that logic over to the project generator/Xcode was not feasible.

If you look at the default settings for UBT, you can see that it points to `/Game/Build/IOS/UBTGenerated/Info.Template.plst**`,\*\* which indicates that every time UBT runs, it can potentially change the contents for iOS `.plist`s.

However, you can change the project setting to use your template (or premade) `.plist` file, which will ignore what UBT generates. If you do that, you can use Xcode to edit the `.plist` file.

The following is an overview of the differences between Mac and iOS `.plist` files:

|   | Mac | IOS |
| --- | --- | --- |
| 
**Default .plist**

 | 

Template copied from the Engine directory.

 | 

UBT-Generated Template.

 |
| 

**Xcode .plist modification**

 | 

Yes

 | 

Not if using UBT Generated

 |

### Entitlements

Every app designates Entitlements as part of codesigning. Entitlements control some Apple-made features or restrictions, such as GameCenter support or running in the Mac security Sandbox.

UE's Xcode project generation treats entitlements similarly to the (Mac) `.plist` files above. UE generates an Xcode project, and if there is no Entitlements file in the default location in the project, the default is copied from the Engine directory. You can then use Xcode (or a text editor) to modify the entitlements, which are are located under `Build/Mac/Entitlements` or `Build/IOS/Entitlements` in your project.

If you have different Sandbox restrictions or other differences in what you ship to end users, you can set separate entitlements for Shipping and Development. You should point them at the same file if you don't need separate features.

Currently, only Mac entitlements are exposed in Project Settings.

The following are the default entitlement settings for macOS and iOS:

| Entitlement Setting | Mac | IOS |
| --- | --- | --- |
| 
Default Development

 | 

Sandboxed, allows client/server network connections.

 | 

No special entitlements set.

 |
| 

Default Shipping

 | 

Sandboxed, allows client network connections.

 | 

No special entitlements set.

 |

Crash Reporter is not compatible with packaged games that enable the sandbox entitlement (default since UE 5.3).

### Frameworks

Frameworks are an Xcode system for collecting headers, libraries, and content. The new Xcode workflow now handles Frameworks using standard Xcode methods instead of manually copying and codesigning as with the previous workflow. When UE generates an Xcode project, it uses the build system to find the referenced Frameworks set in various build source files. It then sets up the Xcode project to copy dynamic libraries and content into the app bundle, and codesign as needed.

### Access Logs

Log files can appear in different locations depending on your sandbox settings and how you are running your application:

-   If Sandbox is enabled:
    
    -   Running through xcode: ~/Library/Logs/\[project name\]
        
    -   Running by double-clicking or by using terminal: ~/Library/Containers/\[your app's bundle ID\]/Data/Library/Logs
        
-   With Sandbox disabled:
    
    -   ~/Library/Logs/\[project name\]
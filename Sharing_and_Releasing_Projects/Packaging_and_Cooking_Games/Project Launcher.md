# Project Launcher

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-project-launcher-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-project-launcher-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:43

---

The Project Launcher is used to cook and deploy builds of your projects to specified platforms for testing, debugging, and releasing your project. The following reference page breaks down the elements that make up the Project Launcher and the settings you can use when creating your own Custom Launch Profiles for deploying your content to different platforms.

![Project Launcher UI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f3bf514-db3b-4172-bd7c-3cef47ae4341/ue5_1-01-project-launcher-ui.png "Project Launcher UI")

## Project Launcher interface

To open the Project Launcher click **Platform** and select **Project Launcher**.

![Open the Project Launcher window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eec81b0f-85d2-41cc-95a0-a046a3c55e7d/ue5_1-02-open-project-launcher.png "Open the Project Launcher window")

The Project Launcher interface can be broken up into two main areas:

![Project Launcher UI description](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ba952ee-187d-40af-8d74-a843fa0995c9/ue5_1-03-project-launcher-ui-description.png "Project Launcher UI description")

1.  Default Launch Profiles
    
2.  Custom Launch Profiles
    

From the **Default Launch Profiles** window, you can see the available platforms and select from the devices that you want to deploy builds to. At the top of this window, you can specify a **Project** (if it's different than the current one you have opened) and a toggle for **Advanced** settings for these default launch profiles.

When you click the **Advanced** toggle button, you'll get additional options next to the default launch profiles that enables you to select a **Build Configuration** and a **Cook** method.

![Advance options in the Project Launcher](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d00a66a3-cd69-4ad6-b2b9-f9d81de1cc0a/ue5_1-04-project-launcher-advance.png "Advance options in the Project Launcher")

In the **Custom Launch Profiles** window, you can create your own profiles that enable you to specify many more options for how content is built and deployed, which is detailed more in the [Custom Launch Profiles](/documentation/en-us/unreal-engine/using-the-project-launcher-in-unreal-engine#customlaunchprofiles) section.

## Custom Launch Profiles

From the Project Launcher, you can create a **Custom Launch Profile** that can be used with all platforms or even specific ones, like the Nintendo Switch. These profiles enable you to build your content in specific ways by setting how it is cooked, packaged, and even deployed using the available build operations.

To add your own Custom Launch Profile, click the **+Add** button in the **Custom Launch Profiles** section.

![Add a Custom Launch Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f8084f2-073b-4b20-9f63-4842093a1d55/ue5_1-05-add-custom-profiles.png "Add a Custom Launch Profile")

After doing so, your Custom Launcher Profile will immediately open. Be sure to give it a name so that you can identify it later on.

![Custom Launch Profile editor window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d075662-fb4a-4b99-bed3-29af575d174c/ue5_1-06-custom-launch-profile-editor.png "Custom Launch Profile editor window")

### Name and Description

In the header bar, you'll find the **Name** and **Description** that you can apply to this custom profile. To edit these, double-click on either section's text to start editing them.

![Editing of the name and description of the Custom Launcher Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc7746a1-2231-494c-8bfe-a484d1f72776/ue5_1-07-editing-name-description.png "Editing of the name and description of the Custom Launcher Profile")

### Project

In the **Project** section, you can specify what project you want this profile to be associated with or if it can be used with any project. By default **Any Project** is set, but it can be set to a specific one. This can be useful when you are developing your project for multiple platforms, and those platforms require particular ways to deploy, test, debug, and even release them.

![Specify project for the Custom Launch Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76ba935b-5fae-4d8d-847c-47f6045ffd7f/ue5_1-08-specify-project.png "Specify project for the Custom Launch Profile")

### Build

The **Build** section enables you to specify the type of configuration you want to build and deploy against depending on your project's progression in development and how you need to test, debug, or release your project.

![Build section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5351c169-c493-4c6a-8e9b-ee1b1f7a8a74/ue5_1-09-build-section.png "Build section")

| Setting | Description |
| --- | --- |
| **Build Configuration** | 
Choose from the available configurations you want to build and test with your project.

![Settings of the Build Configuration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90566a10-7a28-4321-9931-69797010b2f6/ue5_1-10-build-configuration-settings.png "Settings of the Build Configuration")

-   **DebugGame**: This configuration builds the Engine as optimized but leaves the game code debuggable. It is ideal only for debugging game modules.
-   **Development**: This configuration is equivalent to a release build. Unreal Editor uses the Development configuration by default. When your project is compiled using this configuration, it enables you to see code changes made to your project reflected in the Editor.
-   **Shipping**: This is the configuration for optimal performance and shipping your game. This configuration strips out console commands, stats, and profiling tools. This configuration should be used when you are ready to release your game.



 |
| **Build UAT** | When enabled, the [Unreal Automation Tool](/documentation/en-us/unreal-engine/automation-test-framework-in-unreal-engine) will be built as part of the build. |
| **Additional Command Line Parameters** | Parameters specified here will be passed to the app on launch |

### Cook

In the **Cook** section, there are two ways you can cook content for your projects: **By the book** and **On the fly**.

#### By the Book

The Cook **By the book** option enables you to specify which content should be cooked and cooks everything in advance before launching the game.

![Cook By the Book option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c48f6ef0-99b6-4d0d-94b6-9410baf8de24/ue5_1-11-cook-by-the-book.png "Cook By the Book option")

| Setting | Description |
| --- | --- |
| **Cooked Platform** | Select from the available target platforms listed that you would like this custom launch profile to be able to cook content for. |
| **Cooked Cultures** | Select from the available localization cultures you would like this content to be cooked for. |
| **Cooked Maps** | Select from the available maps in your title that you would like to cook. |
| Release/DLC/Patching Settings |   |
| **Create a release version of the game for distribution** | Enables you to create a release version of your title that will be used for distribution. |
| **Name of the new release to create** | Give your release a new name that will be used during the cook. |
| **Release version this is based on** | This is the release version to base the next release / DLC / patch on. |
| **Generate Patch** | If enabled, content will be diffed against source content and only changed files will be included in the new pak file. |
| **Build DLC** | If enabled, DLC will be built without the content released with the original game. |
| **Name of the DLC to build** | Give a name to the DLC that is going to be built. |
| **Include Engine Content** | If enabled, DLC will include Engine content which was not included in the original release. If it is not checked, an error will be produced when accessing content from the **Engine** directory. |
| Advanced Settings |   |
| **Iterative Cooking: Only cook content modified from previous cook** | If enabled, only modified content will be cooked resulting in much faster cooking times. It is recommended to enable this option whenever possible. |
| **Stage base release pak files** | If enabled, unchanged pak files present in the base release version will be staged. |
| **Compress Content** | If enabled, content generated will be compressed. These will be smaller but potentially take longer to load as it decompresses. |
| **Add a new patch tier** | If enabled, a new numbered pak file will be generated with the patch content. |
| **Save Packages Without Versions** | If enabled, the version is assumed to be the current at load. This is potentially dangerous but results in smaller patch sizes. |
| **Store all content in a single file (UnrealPak)** | If enabled, the content will be deployed as a single UnrealPak file instead of many separate files. |
| **Encrypt INI files (only with Use Pak File enabled)** | If enabled, ini files stored inside the UnrealPak file will be encrypted. |
| **Generate Chunks** | If enabled, the content will be deployed as multiple UnrealPak files instead of many separate files. |
| **Don't include Editor content in the build** | If enabled, the cooker will skip Editor content and not include it in the build. |
| **HTTP Chunk Install Data Path** | 
-   **Create HTTP Chunk Install Data**: If enabled, the content will be split into multiple Pak files and stored as data that can be downloaded.
-   **HTTP Chunk Install Data Path**: Specify the file path for the Chunk Install Data.
-   **HTTP Chunk Install Release Name**: Name of this version of the HTTP Chunk Install Data.



 |
| **Cooker Build Configuration** | Sets the build configuration to use for the cooker commandlet. |
| **Additional Cooker Options** | Additional cooker command line parameters can be specified here. |

#### On the Fly

The Cook **On the fly** option enables content to be cooked at runtime as needed before it is being sent to the device.

![Cook On the Fly option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40507f54-e6a2-4f25-9b1c-91f1548c3f8d/ue5_1-12-cook-on-the-fly.png "Cook On the Fly option")

| Setting | Description |
| --- | --- |
| **Only Cook Modified Content** | If enabled, only modified content will be cooked, resulting in much faster cooking times. It is recommended to use this option whenever possible. |
| **Additional Cooker Options** | Additional cooker command line parameters can be specified here. |

### Package

In the **Package** section, you can choose how the build is packaged and whether it should be stored locally or in a shared repository that can be accessed.

![Package section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/974a970b-7724-486f-9997-c049c5eb1b2c/ue5_1-13-package-section.png "Package Section")

#### Package Method

| Setting | Description |
| --- | --- |
| Package & Store Locally |   |
| **Local Directory Path** |   |
| **Is this build for distribution to the public** | If checked the build will be marked as for release to the public (distribution) |
| **Include an installer for prerequisitea of packaged games** | If checked the build will include the prerequisites installer on platforms that support it. |
| **Use container files for optimized loading (I/O Store)** | If checked the build will use container files for optimized loading (I/O Store). |
| **Make a binary config file for faster runtime startup times** | Bakes the config (.ini, with plugins) data into a binary file, along with optional custom data. |
| **Optional I/O Store Reference Block Database:** | 
-   The path to a global UTOC in a derictory of previously released iostore containers.
-   The path to a crypto JSON to decrypt the reference block containers, if indeed.



 |
| Package & Store In Repository |   |
| **Repository Path** |   |

### Archive

In the **Archive** section, you can specify whether or not to archive the build and the directory path if it is going to be archived for later reference.

![Archive section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45cd1f44-47b7-44fc-8b46-80a855c2aff7/ue5_1-14-archive-section.png "Archive section")

### Deploy

In the **Deploy** section, you'll need to decide how you would like to deploy your current build to a device; using a **File server**, **Copy to device**, or **Copy repository**.

Use the following selections to determine which deployment method to use:

![Deploy method selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76e91d98-fd60-4e87-9bf8-dea53b10be25/ue5_1-15-deploy-method.png "Deploy method selection")

-   **File Server** will cook and deploy the content at runtime as it is needed to the device.
-   **Copy to Device** will copy the entire cooked build to the device.
-   **Do Not Deploy** will not deploy the build to any device once the cook and package complete.
-   **Copy Repository** will copy a build from a specified file location to deploy to any device.

#### File Server

The available settings you can use when selecting File Server.

![File server deploy method](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/710547c3-4f0b-4620-9611-ef5277b284ad/ue5_1-16-deploy-file-server.png "File server deploy method")

| Setting | Description |
| --- | --- |
| **Default Deploy Platform** | Set the default target platform(s) you want to deploy content. |
| Advanced Settings |   |
| **Hide the file server's console window** | If enabled, the file server's console window will be hidden from your desktop. |
| **Streaming server (experimental)** | If enabled, the file server will use an experimental implementation that can serve multiple files simultaneously. |

#### Copy to Device

The available settings you can use when selecting Copy to Device.

![Copy to device deploy method](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07b6e190-7141-4cf7-a0d9-fb82633b9829/ue5_1-17-deploy-copy-to-device.png "Copy to device deploy method")

| Setting | Description |
| --- | --- |
| **Default Deploy Platform** | Set the default target platform(s) you want to deploy content. |
| Advanced Settings |   |
| **Only deploy modified content** | If enabled, only modified content will be deployed, resulting in much faster deployment times. It is recommended to use this option whenever possible. |

#### Copy Repository

The available settings you can use when selecting Copy Repository.

![Copy repository deploy method](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ab6a811-98d8-47f4-9ae8-a8a4103a2ad8/ue5_1-18-deploy-copy-repository.png "Copy repository deploy method")

| Setting | Description |
| --- | --- |
| **Repository Path** | Set the file path to the repository that you want to copy to device. |
| **Default Deploy Platform** | Set the default target platform(s) you want to deploy content. |

### Launch

![Launch section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9502096b-0ad5-4e3e-bed2-5a14db1dfcdf/ue5_1-19-launch-section.png "Launch section")

| Setting | Description |
| --- | --- |
| **Launch As** | 
Select how you would like to launch this instance of your build.

![Launch As options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6333f683-2f5d-4f68-9c98-5c69971a3b73/ue5_1-20-launch-options.png "Launch As options")

-   **Standalone Client**: Launches this instance as a standalone game client.
-   **Listen Server**: Launches this instances a game client that can accept connections from other clients.
-   **Dedicated Server**: Launches this instance as a dedicated game server.
-   **Unreal Editor**: Launches this instance as an Unreal Editor.



 |
| **Initial Culture** | Select the culture that you're initially targeting to use when launching the build. |
| **Initial Map** | Select the initial map you want the project to use when launching the build. |
| **Additional Command Line Parameters** | Enter any necessary command line parameters you want to use when launching the build. |
| **Synchronize Screen Refresh Rate (VSync)** | Enable this for the build to attempt to run the project at the same refresh rate as the monitor it's being run on. |
# Packaging Unreal Engine Projects

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project)  
**Processed:** 2025-06-14 16:41:26

---

This page provides an overview of packaging key concepts, and tutorials for cooking and packaging. To skip to the tutorials, see [Let’s Cook Content](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#let-s-cook-content) and [Let’s Package a Project](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#let-s-package-a-project).

## What is Packaging?

**Packaging** is a process that converts an **Unreal Engine** project into a standalone executable (`.exe`) or application.

The packaging process compiles a project’s content into a format that can run on a [target platform](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#supported-target-platforms) such as Windows, iOS, or a console. For example, when you download a game to your machine, the executable and data files that you receive have been packaged to ensure their compatibility with your operating system.

Packaging can occur at multiple stages in the development pipeline:

[![The Development Pipeline](https://dev.epicgames.com/community/api/documentation/image/39be121d-9228-456f-becf-6177e45c0362?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/39be121d-9228-456f-becf-6177e45c0362?resizing_type=fit)

-   **Production and Testing**
    
    During production and testing, packaging can be used to verify a project’s functionality. For example, quality assurance (QA) or testing a packaged project on mobile platforms. 
    
-   **Distribution**
    
    During distribution, also called **shipping**, packaging is used to prepare a final build for release.
    
-   **Post-Production**
    
    During post-production, packaging can be used to distribute content updates, such as downloadable content (DLC) and patches.
    

A **final build** is a project that is ready for users or players.

## Supported Target Platforms

A **target platform** is an operating system or console that a project will run on. Unreal Engine supports packaging for the following target platforms:

-   Desktop platforms, such as Windows, macOS, and Linux.
    
-   Mobile platforms, such as iOS, iPadOS, tvOS, and Android.
    
-   All major consoles.
    
-   XR (extended reality) platforms such as OpenXR, PSVR2, ARKit, ARCore, and visionOS.
    

### Additional Software

Developing and packaging for Windows and macOS does not require any additional software.

Developing and packaging for consoles requires a source code build of the Unreal Engine and cannot use the pre-compiled version obtained through the Epic Games Launcher. You can download a source code build from [GitHub](https://www.unrealengine.com/en-US/ue-on-github).

Developing and packaging for some target platforms, such as Linux, mobile, and XR platforms, may require additional Software Development Kits (SDKs) and Unreal Engine components. For more information on SDKs for your target platform, see [Sharing and Releasing Projects](https://dev.epicgames.com/documentation/en-us/unreal-engine/sharing-and-releasing-projects-for-unreal-engine). For more information on Unreal Engine components, see [Install Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/install-unreal-engine).

## How Does Packaging Work?

Packaging a project is a [build operation](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#build-operations). **Build**, **cook**, and **stage** are build operations that contribute to the packaging process.

[![The Packaging Process](https://dev.epicgames.com/community/api/documentation/image/847e4530-1586-46a8-a346-44efcfb5e5c7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/847e4530-1586-46a8-a346-44efcfb5e5c7?resizing_type=fit)

-   **Build**
    
    During this phase, the project’s code, plugins, and binaries are compiled for the target platform. If the project uses C++, all code is compiled into binaries.
    
-   **Cook**
    
    During this phase, the project’s assets (geometry, materials, textures, **Blueprints**, audio, and more) are saved into a format that can run on the target platform. Assets are optimized to increase load efficiency.
    
-   **Stage**
    
    During this phase, compiled code and cooked content is copied to a **staging directory**. 
    
    A **staging directory** is a temporary folder on your drive, outside of the development directory, that you designate during the packaging process.
    
-   **Package**
    
    During this phase, compiled code and cooked content is bundled into a distributable set of files inside the staging directory. For example, on Windows, distributable files include an installer or executable and a folder containing [Pak](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#pak-files-and-pak-file-chunking) (`.pak`) files.
    
-   (Optional) **Deploy**
    
    The project is pushed to a target platform where it will run.
    
-   (Optional) **Run**
    
    This phase launches the project from the **Unreal Editor** on the target platform. This operation is ideal when quickly iterating and testing on a device that is not your local desktop.
    

### Build Operations

While each build operation contributes to the packaging process, they can also be performed independently.

When performed independently, each operation is uniquely useful in different stages of development. For example, the **cook** operation can optimize and save specific assets instead of every asset in your game level — making it ideal for distributing content updates, such as DLC or patches.

For a comparison of when each build operation is useful, see the table below:

| Build Operation | Example Use |
| --- | --- |
| 
**Build**

 | 

Compiling code during development.

 |
| 

**Cook**

 | 

Preparing a project for QA testing or distribution.

Preparing DLC and patches for testing or distribution.

 |
| 

**Stage**

 | 

Preparing a project for QA testing or distribution.

 |
| 

**Package**

 | 

Preparing a project for QA testing or distribution.

 |
| 

**Deploy**

 | 

Testing a project on a platform that is not your local desktop computer, such as console or mobile.

 |
| 

**Run**

 | 

Testing a project on a platform that is not your local desktop computer.

Users running a shipped project on a target platform.

 |

## Cooking Content

**Cooking** is a build operation that prepares game content so that it can be run outside of the Unreal Editor. It’s performed as part of the packaging process, but can also be performed independently.

Cooking is necessary because it: 

-   Ensures game content is optimized and compatible with the target platform.
    
-   Is required before packaging a final build for distribution or testing on a device, such as mobile or console.
    
-   Converts editor-only formats into runtime-ready formats.
    

**Runtime** refers to the period of time when a project is running on its target platform.

The following tasks are performed during the cooking process:

-   Assets (geometry, materials, textures, Blueprints, audio, and more) are converted into a platform-specific format.
    
-   Assets are compressed and optimized, when possible.
    
-   Unused data is not included, in order to reduce the size of the project on disk and improve performance.
    
-   Blueprints are compiled into their native code, if necessary.
    
-   Maps and Levels are processed and optimized.
    
-   Cooked content is stored in one or more [Pak](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#pak-files-and-pak-file-chunking)  (`.pak`) files.
    

During cooking, optimizing strips out any content that isn’t referenced by the project’s game levels or code. For example, assets that appear in the Unreal Editor’s **Content Browser**, but not in the game level, won’t be cooked.

When cooking independently, files are copied to the **development directory** instead of the staging directory.

For more information on the cooking process, see [Content Cooking](https://dev.epicgames.com/documentation/en-us/unreal-engine/cooking-content-in-unreal-engine) documentation.

### Pak Files and Pak File Chunking

A **Pak** (`.pak`) file is an archive file format that Unreal Engine uses to store cooked content. While Pak files are the default file type, you can explore the other archiving file types in the project’s [Packaging Settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#packaging-settings).

Pak files can be further separated into smaller Pak files, called **chunks**. When using chunks, you can assign specific assets from your project to a chunk. This is useful in the following situations:

-   Separating out DLC content or patches that you don’t want included in the fully packaged project.
    
-   Streaming installation. Chunks allow for customizing the priority of content that’s downloaded first.
    

**Streaming installation** is a way for users to interact with a shipped project before it’s finished installing. This is ideal for console games, allowing players to play the game sooner.

For more information on Pak files and Pak file chunking, see [Cooking and Chunking](https://dev.epicgames.com/documentation/en-us/unreal-engine/cooking-content-and-creating-chunks-in-unreal-engine) and [Preparing Assets for Chunking](https://dev.epicgames.com/documentation/en-us/unreal-engine/preparing-assets-for-chunking-in-unreal-engine).

### Let’s Cook Content

There are two methods to cook content for a project:

| Cooking Method | Description |
| --- | --- |
| 
**By the book** (default)

 | 

-   The project’s assets are cooked *before packaging* the project for its target platform.
    
-   This process is slower and recommended for final build testing.
    

 |
| 

**On the fly**

 | 

-   Assets are cooked *at runtime* when requested by the target platform.
    
-   This process is recommended for rapid testing during development.
    

 |

#### Cooking by the Book

To cook content by the book, follow these steps:

1.  From the Unreal Editor’s main toolbar, open the **Platforms** menu.
    
    [![Unreal Editor Platforms Menu](https://dev.epicgames.com/community/api/documentation/image/650d1a69-1d11-441b-8512-05dd940fa429?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/650d1a69-1d11-441b-8512-05dd940fa429?resizing_type=fit)
    
2.  From the list, select a target platform. This only cooks content for the selected target platform. Under **Content Management**, click **Cook Content**.
    
    [![Unreal Editor Cook Content](https://dev.epicgames.com/community/api/documentation/image/e8b80e53-4a20-4e19-b01a-d56335e97061?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e8b80e53-4a20-4e19-b01a-d56335e97061?resizing_type=fit)
    
    Once you click Cook Content, a popup dialog will appear in the bottom-right corner of the Unreal Editor. This displays cooking progress and completion or failure states.
    
    While cooking content, the dialog displays **Cooking content for \[target platform\]**.
    
    [![Cooking Content](https://dev.epicgames.com/community/api/documentation/image/5cb2bf60-a096-4a96-a11e-2e72b141cbaa?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5cb2bf60-a096-4a96-a11e-2e72b141cbaa?resizing_type=fit)
    
    Once cooking is complete, the dialog displays **Cooking complete!**
    
    [![Cooking Complete](https://dev.epicgames.com/community/api/documentation/image/fae11676-0196-4057-9d01-2cdfa97280e4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fae11676-0196-4057-9d01-2cdfa97280e4?resizing_type=fit)
    

#### Cooking on the Fly

To enable cooking on the fly, follow these steps:

1.  From the Unreal Editor’s main toolbar, open the **Platforms** menu.
    
    [![Unreal Editor Platforms Menu](https://dev.epicgames.com/community/api/documentation/image/7eac8dc2-200d-4519-b9bb-0703103421da?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7eac8dc2-200d-4519-b9bb-0703103421da?resizing_type=fit)
    
2.  In the menu, check the **Enable cooking on the fly** checkbox.
    
    [![Platforms Cooking On The Fly](https://dev.epicgames.com/community/api/documentation/image/869278d0-59ab-4b71-b4a9-fd371bbb57ff?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/869278d0-59ab-4b71-b4a9-fd371bbb57ff?resizing_type=fit)
    

With cooking on the fly enabled, cooking can now be performed using the same steps as [Cooking by the Book](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#cooking-by-the-book-br).

## Build Configurations

In order to package a project, you must choose a **build configuration**. A build configuration is a preset that determines how your project is compiled, and what code and content is made available.

Each configuration is useful at different stages in development because they prioritize different factors, including:

-   Performance
    
-   Level of optimization
    
-   Project file size
    
-   Access to debugging tools
    

For example, the **Shipping** configuration is ideal for distributing games where players should not have access to game-breaking console commands. **Debug** and **Development**, which include console commands, are ideal for optimizing and testing a game during development.

For a comparison of all build configurations, see the table below:

| Build Configuration | Description | Development Stage | Example Use |
| --- | --- | --- | --- |
| 
**Debug**

 | 

-   Builds both engine and project source code.
    
-   Disables optimizations. This makes your project larger and slower, but simpler to debug.
    
-   Includes all additional information and debug symbols.
    

 | 

Development. This configuration is unsuitable for distribution.

 | 

-   Engine and project debugging.
    
-   Slowest debugging configuration.
    

 |
| 

**DebugGame**

 | 

-   Builds project source code.
    
-   Disables optimizations.
    
-   Includes some additional information and debug symbols.
    

 | 

Development. This configuration is unsuitable for distribution.

 | 

-   Project debugging
    
-   Faster performance than Debug.
    
-   Not available for Blueprint-only projects.
    

 |
| 

**Development** (default)

 | 

-   Enables all but the most time-consuming optimizations.
    
-   Includes minimal debugging information.
    
-   Enables you to see code changes made to your project reflected in the Editor.
    

 | 

Development. This configuration is unsuitable for distribution.

 | 

-   Testing during development.
    
-   Faster performance than Debug and DebugGame.
    

 |
| 

**Test**

 | 

-   Includes debugging tools, such as console commands, stats, and profiling tools.
    
-   Enables all optimizations.
    

 | 

Used for testing builds internally without full debugging tools overhead.

 | 

-   QA testing your project.
    
-   Similar to Shipping but with lower performance.
    

 |
| 

**Shipping**

 | 

-   Disables console commands, stats, and profiling tools that are not intended for end-users.
    
-   Enables all optimizations.
    

 | 

Distribution. This configuration is unsuitable for development.

 | 

-   Shipping a project to users.
    
-   Fastest performance.
    

 |

For more information on Build Configurations, see [Build Configurations Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/build-configurations-reference-for-unreal-engine).

## Packaging Settings

Presets such as build configurations, and many other options for customizing the packaging process, can be found in **Project Settings > Packaging**. 

This window is accessible from two locations in the Unreal Editor:

-   From the Editor’s main toolbar, click the **Platforms** menu. Then, click **Packaging Settings**.
    
    [![Unreal Editor Packaging Settings](https://dev.epicgames.com/community/api/documentation/image/84148d77-7ff6-40d1-9777-013533cb6f2b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/84148d77-7ff6-40d1-9777-013533cb6f2b?resizing_type=fit)
    
-   From the Editor’s menu bar, click **Edit > Project Settings**. The **Project Settings** window will open. In the left-hand navigation menu, click **Packaging**.
    
    [![Project Settings Packaging](https://dev.epicgames.com/community/api/documentation/image/e61ec49b-e154-4918-8580-9aee88a9a7a2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e61ec49b-e154-4918-8580-9aee88a9a7a2?resizing_type=fit)
    

The Packaging section includes, but is not limited to, options for:

-   Custom build presets
    
-   Build configurations
    
-   Build targets
    
-   Debug symbols
    
-   Executables
    
-   Localization
    
-   Compression
    
-   Cooking
    
-   Configuration files (`.ini`)
    
-   Shaders
    
-   Archive filetypes (Pak, Chunk, Utoc, and Ucas)
    
-   The [Zen Storage Server](https://dev.epicgames.com/documentation/en-us/unreal-engine/zen-storage-server-for-unreal-engine)
    
-   Movies (for example, a pre-rendered movie that plays prior to gameplay)
    

For a detailed explanation of the options available in Packaging, see the Packaging section of [Project](https://dev.epicgames.com/documentation/en-us/unreal-engine/project-section-of-the-unreal-engine-project-settings).

## Let's Package a Project

In this tutorial, you’ll learn how to package a project for Windows using the **Package** build operation and **Development** build configuration.

You’ll put the theory that you’ve learned in the previous sections into practice by completing the following tasks:

1.  [Set a Game Default Map](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#setting-a-game-default-map)
    
2.  [Set a Build Configuration](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#setting-a-build-configuration)
    
3.  [Create a Packaged Project](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#creating-a-packaged-project)
    
4.  [Run, Test, and Exit Your Executable](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#running-and-exiting-your-executable)
    

By the end of the tutorial, you will have a game executable that you can run, test, and exit. This workflow mimics what it’s like to put an Unreal Engine game through testing during production.

To complete this tutorial you will need:

-   A machine running Windows
    
-   The Unreal Engine
    
-   An Unreal Engine project using the **First Person** template in the **Arena Shooter** variant.
    

In this tutorial, your game executable will use the same name as your project. This tutorial will use the name "MyProject" as an example.

[![Unreal Project Browser](https://dev.epicgames.com/community/api/documentation/image/a95bbd38-8b36-4268-ab95-c7b9a612930b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a95bbd38-8b36-4268-ab95-c7b9a612930b?resizing_type=fit)

### Before You Begin

Open your project in the Unreal Editor.

### Setting a Game Default Map

The **Game Default Map** is the map that loads when your packaged project launches. Every project must set a Game Default Map prior to packaging — without it, there’s nothing for the project to load at runtime.

If a Game Default Map is not set, the project will display a black screen when launched. The exception to this rule is when using a project template, which sets a Game Default Map automatically.

You'll change the map in the following steps:

1.  From the Editor’s menu bar, click **Edit > Project Settings**.
    
    [![Unreal Editor Project Settings](https://dev.epicgames.com/community/api/documentation/image/d60a7de0-68b3-4006-be24-5addf2c6bd49?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d60a7de0-68b3-4006-be24-5addf2c6bd49?resizing_type=fit)
    
2.  In the **Project Settings** window, under the **Project** heading in the left-hand navigation menu, click **Maps & Modes**.
    
    [![Project Settings Maps And Modes](https://dev.epicgames.com/community/api/documentation/image/0f8b7c3e-96ad-4f72-ae81-d832f31679f4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0f8b7c3e-96ad-4f72-ae81-d832f31679f4?resizing_type=fit)
    
3.  Expand the **Default Maps** heading and click the **Game Default Map** dropdown menu. Search for `Lvl_ArenaShooter` and select it.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/aa963d49-7b27-42e2-8899-a8801781060d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/aa963d49-7b27-42e2-8899-a8801781060d?resizing_type=fit)
    

You can also set the map by selecting it in the **Content Browser**, then click the **Use Selected Asset from Content Browser** icon in the Project Settings window.

### Setting a Build Configuration

The **build configuration** determines how your project is compiled. Every project must have a build configuration set prior to packaging. Unreal Engine will default to the **Development** configuration unless you change it.

1.  While still in the **Project Settings** window, click **Packaging** from the left-hand navigation menu.
    
    [![Project Settings Packaging](https://dev.epicgames.com/community/api/documentation/image/bbba631e-42df-491c-9099-69da52714516?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bbba631e-42df-491c-9099-69da52714516?resizing_type=fit)
    
2.  Expand the **Project** heading. Verify that the **Build Configuration** is set to **Development**. If it’s not, click the dropdown menu and set it to Development.
    
    [![Project Settings Build Configurations](https://dev.epicgames.com/community/api/documentation/image/dd86d353-66ae-4775-94ea-736b435545dd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dd86d353-66ae-4775-94ea-736b435545dd?resizing_type=fit)
    

By using the Development configuration, you can access the in-game console during runtime. You’ll use the in-game console to execute console commands later in this tutorial.

The **in-game console** is a command line interface that allows you to interact with the engine during runtime.

### Creating a Packaged Project

Packaging creates a standalone executable or application from an Unreal Engine project. In this case, you’ll package for the target platform Windows, and create an executable that you’ll launch later in this tutorial.

To package a project, follow these steps:

1.  In the Editor’s main toolbar, click the **Platforms** menu. Under **Content/SDK/Device Management**, you’ll see a list of platforms. For the purpose of this tutorial, select **Windows**.
    
    [![Unreal Editor Platforms Windows](https://dev.epicgames.com/community/api/documentation/image/9647e17a-c12d-4245-ad25-daad36b8ca3a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9647e17a-c12d-4245-ad25-daad36b8ca3a?resizing_type=fit)
    
    Depending on which platform you're developing for, and which SDKs you have installed, the platforms listed under **Content/SDK/Device Management** can look different.
    
2.  In the new context menu, under **Binary Configuration**, verify that **Use Project Setting (Development)** is selected. The parentheses show which build configuration is currently selected in the packaging settings.
    
    [![Platforms Binary Configuration](https://dev.epicgames.com/community/api/documentation/image/e0b921da-e78b-4252-9fcd-70510cba483f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e0b921da-e78b-4252-9fcd-70510cba483f?resizing_type=fit)
    
    You can quickly change your build configuration from the **Platforms** menu without going back to **Project Settings**.
    
3.  Under **Content Management**, select **Package Project**.
    
    [![Platforms Package Project](https://dev.epicgames.com/community/api/documentation/image/86a0bae8-dfca-4131-8505-87c3d2f873fb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/86a0bae8-dfca-4131-8505-87c3d2f873fb?resizing_type=fit)
    
4.  In the **Package project** dialog, choose or create a folder to use as the **staging directory** on your drive — where the project’s packaged files will be saved. Click **Select Folder** to confirm the staging directory and initiate the packaging process.
    

Once the process has begun, a popup dialog called **Packaging project for \[selected target platform\]** appears in the bottom-right corner of the Unreal Editor.

[![Packaging GIF](https://dev.epicgames.com/community/api/documentation/image/d7ba6195-3380-43fe-b0ce-1fbccc4fe715?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d7ba6195-3380-43fe-b0ce-1fbccc4fe715?resizing_type=fit)

At any time during the packaging process, you can open the **Output Log** by clicking the **Show Output Log** link on the pop-up dialog. The log window displays tasks that the engine performs during the packaging process, including logging errors.

[![](https://dev.epicgames.com/community/api/documentation/image/92774841-e42a-4555-9b84-6318775d39aa?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/92774841-e42a-4555-9b84-6318775d39aa?resizing_type=fit)

Once the process is complete, you’ll see one of the following messages indicating that packaging has completed or failed.

|  |  |
| --- | --- |
| 
[![Packaging Complete](https://dev.epicgames.com/community/api/documentation/image/02d720ca-4dd7-4e6b-bcd5-f8c2a517deab?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/02d720ca-4dd7-4e6b-bcd5-f8c2a517deab?resizing_type=fit)



 | 

[![Packaging Failed](https://dev.epicgames.com/community/api/documentation/image/5deee5b9-d9d2-4e8a-850c-d5e5a553f6ef?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5deee5b9-d9d2-4e8a-850c-d5e5a553f6ef?resizing_type=fit)



 |

#### (Optional) Canceling the Packaging Process

You can stop the packaging process at any time by clicking the **Cancel** button on the pop-up dialog.

[![Packaging Cancel](https://dev.epicgames.com/community/api/documentation/image/8635bb67-3b59-4d36-aa09-d3ed955da1d2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8635bb67-3b59-4d36-aa09-d3ed955da1d2?resizing_type=fit)

Once the cancellation is successful, you’ll see the following message in the bottom-right corner of the Unreal Editor.

[![Packaging Canceled](https://dev.epicgames.com/community/api/documentation/image/d5c2b9c3-a563-43dc-b2b4-73fee4aff5b0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d5c2b9c3-a563-43dc-b2b4-73fee4aff5b0?resizing_type=fit)

#### (Optional) Debugging Packaging Errors

The [Output Log](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#the-output-log) and the [Message Log](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#the-message-log) both display packaging errors. During the packaging process, you can click the **Show Output Log** link on the pop-up dialog to open the **Output Log**.

[![Packaging Show Output Log](https://dev.epicgames.com/community/api/documentation/image/083dc7ee-668f-4f93-b6ca-96a071d6438a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/083dc7ee-668f-4f93-b6ca-96a071d6438a?resizing_type=fit)

You can also access either of these logs at any time by clicking **Window > Message Log** or **Window > Output Log** from the Editor’s menu bar.

[![Windows Message Log](https://dev.epicgames.com/community/api/documentation/image/afd282cc-58db-411e-baf5-73714674aca3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/afd282cc-58db-411e-baf5-73714674aca3?resizing_type=fit)

##### The Output Log

The **Output Log** is a log of real-time messages from the engine that displays debugging information, compiler messages, warnings, error messages, and event and asset loading details.

Because it’s a real-time log, it can provide additional context clues to what was happening before, during, and after packaging.

##### The Message Log

The **Message Log** stores important messages, such as errors and warnings. It can help you identify where to start your debugging investigation. You can look under the **Packaging Results** heading in the left-hand navigation menu to see any listed errors or warnings you may need to address.

[![Message Log](https://dev.epicgames.com/community/api/documentation/image/6b50aac4-db5f-4d96-8b85-178da260d610?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6b50aac4-db5f-4d96-8b85-178da260d610?resizing_type=fit)

### Running and Exiting Your Executable

Once you’ve packaged your project, follow these steps to run, test, and exit it:

1.  Navigate to the folder you specified as your staging directory — where your packaged project files are saved.
    
    [![Packaged Executable](https://dev.epicgames.com/community/api/documentation/image/947ba1ad-0464-4658-b5a5-fd4f1ec746e5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/947ba1ad-0464-4658-b5a5-fd4f1ec746e5?resizing_type=fit)
    
    The Pak files previously mentioned in this guide can be found in the staging directory under **\[Project Name\] > Content > Paks**.
    
2.  Run your project by double-clicking the executable (`.exe`) file. The executable will have the same name as your Unreal Engine project.
    
3.  When the project loads, you’ll see a windowed version of the Game Default Map. You can now test the executable by moving around the level and interacting with pickups.
    
4.  To exit your executable, open the in-game console’s command line by pressing the **Backtick (\`)** key. In the command line, type one of the following console commands and press **Enter**:
    
    -   `quit`
        
    -   `exit`
        
    
    [![Command Line](https://dev.epicgames.com/community/api/documentation/image/871d0fb9-70b8-43d3-a06f-82f426d65834?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/871d0fb9-70b8-43d3-a06f-82f426d65834?resizing_type=fit)
    

Exiting a running executable can differ depending on what type of build configuration you use. For example, if you use the **Shipping** configuration (which does not have access to the in-game console) your project must include a user interface option, such as a button, to exit from within the application.

For more information about console commands in Unreal Engine, see [Console Commands Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-console-commands-reference).

## Using the Unreal Automation Tool

The **Unreal Automation Tool (UAT)** is a host program and a set of utility script libraries that can manipulate Unreal Engine projects.

For example, when you package a project, the Automation Tool executes the command `BuildCookRun` — the underlying script for all build operations. By completing the [Package a Project](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project#let-s-package-a-project) tutorial, you have already employed the Automation Tool.

The Automation Tool is useful for scripting unattended processes in C#, such as cooking and running automation tests for Continuous Integration (CI) pipelines.

For more information on the UAT, see [Automation Tool Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-automation-tool-overview-for-unreal-engine).

## Using the Project Launcher

The **Project Launcher** is a tool that’s used to create custom **Launch Profiles**. Custom Launch Profiles give you automated control over the build, cook, package, and deploy operations for multiple platforms in one location. This allows for efficiency and iteration during development and testing.

To access the Project Launcher in Unreal Engine, click the **Platforms** button in the Editor’s main toolbar. Under **Options and Settings**, click **Project Launcher**.

[![Platforms Project Launcher](https://dev.epicgames.com/community/api/documentation/image/5c547c3a-f75c-40d9-ba15-9737e3119da6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5c547c3a-f75c-40d9-ba15-9737e3119da6?resizing_type=fit)

For more information on using the Project Launcher, see [Project Launcher](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-project-launcher-in-unreal-engine).

## Project Distribution

Distributing, or shipping, refers to releasing your project for users on digital distribution platforms and occurs near the end of the development pipeline.

Depending on which target platform you’re developing for, many digital distribution platforms are available. For example, projects for desktop platforms can be distributed on the **Epic Games Store** or Steam. Alternatively, iOS and Android projects can be distributed on the App Store or Google Play Store.

Each digital distribution platform has a unique workflow, requirements, and legal agreements for shipping projects. Shipping an Unreal Engine project to the Epic Games Store comes with certain benefits. For more information about shipping to the Epic Games Store, see [Distribute on Epic Games](https://store.epicgames.com/en-US/distribution).

For more information about your target platform and associated digital distribution platforms, see [Sharing and Releasing Projects](https://dev.epicgames.com/documentation/en-us/unreal-engine/sharing-and-releasing-projects-for-unreal-engine).

## Additional Information

-   [Sharing and Releasing Projects](https://dev.epicgames.com/documentation/en-us/unreal-engine/sharing-and-releasing-projects-for-unreal-engine)
    
-   [Mobile Optimization Guides](https://dev.epicgames.com/documentation/en-us/unreal-engine/debugging-and-optimization-for-mobile-in-unreal-engine)
    
-   [Project Launcher](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-project-launcher-in-unreal-engine)
    
-   [Content Cooking](https://dev.epicgames.com/documentation/en-us/unreal-engine/cooking-content-in-unreal-engine)
    
-   [Preparing Assets for Chunking](https://dev.epicgames.com/documentation/en-us/unreal-engine/preparing-assets-for-chunking-in-unreal-engine)
    
-   [Cooking and Chunking](https://dev.epicgames.com/documentation/en-us/unreal-engine/cooking-content-and-creating-chunks-in-unreal-engine)
    
-   [Build Configurations Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/build-configurations-reference-for-unreal-engine)
    
-   [Console Commands Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-console-commands-reference)
    
-   [Zen Storage Server](https://dev.epicgames.com/documentation/en-us/unreal-engine/zen-storage-server-for-unreal-engine)
    
-   [Distribute on Epic Games](https://store.epicgames.com/en-US/distribution)
    
-   [Accessing Unreal Engine Source Code on Github](https://www.unrealengine.com/en-US/ue-on-github)
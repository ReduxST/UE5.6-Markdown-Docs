# Linux Development Quickstart

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/linux-development-quickstart-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/linux-development-quickstart-for-unreal-engine)  
**Processed:** 2025-06-14 16:33:40

---

Unreal Engine (UE) supports development on Linux devices using either builds created from source or pre-compiled, **installed builds**. This page provides instructions on how to set up Unreal Engine on Linux, including your development environment and build pipeline. When you finish this tutorial, you will be ready to develop applications in Unreal Engine using your Linux machine.

## 1\. Recommended Software and Hardware

Unreal Engine is compatible with a variety of Linux distributions and IDEs, as long as they meet these minimum requirements:

| Running the Engine |   |
| --- | --- |
| 
**Operating System**

 | 

Rocky Linux 8 / Redhat Linux 8 or newer

 |
| 

**Linux Kernel Version**

 | 

kernel 4.18 or newer

 |
| 

**Additional Dependencies**

 | 

glibc 2.28 or newer

 |

If either Unreal Editor or installations of UE games take a very long time on startup, check that your `glibc` is version 2.35 or newer, as earlier versions have a slow implementation of `dlopen`.

We recommend your system meet the following standard so that **Unreal Editor** performs smoothly:

|  |  |
| --- | --- |
| 
**Recommended Operating System**

 | 

Ubuntu 22.04

 |
| 

**Processor**

 | 

Quad-core Intel or AMD, 2.5 GHz or faster

 |
| 

**Memory**

 | 

32 GB RAM

 |
| 

**Graphics Card**

 | 

GeForce 2080

 |
| 

**Graphics RAM**

 | 

8 GB or more

 |
| 

**RHI Version**

 | 

Vulkan: AMD (RADV minimum 24.2.8+, recommended 25.0.0+) and NVIDIA (570+)

 |

The Vulkan rendering hardware interface (RHI) used on Linux is not friendly to low amounts of VRAM compared with other backends. We strongly recommend using a dedicated GPU with a high amount of VRAM.

To set up your development environment, we recommend the following software, which we test with most frequently:

| Developing with the Engine |   |
| --- | --- |
| 
**Operating System**

 | 

Ubuntu 22.04, Rocky Linux 8

 |
| 

**Compiler**

 | 

clang 18.1.0

 |
| 

Optional

 |  |
| 

**IDE**

 | 

Visual Studio Code, Rider

 |

Refer to the documentation for your Linux distribution or IDE for further information on how to set them up. While setting up your OS and hardware is outside the scope of this documentation, setting up your IDE to work with Unreal Engine is covered below.

## 2\. Install Unreal Engine

You can set up Unreal Engine on Linux either by installing a pre-compiled build, or by building the engine from source.

### 2a. Download an Installed Build

The simplest option for running Unreal Engine is to use an Installed Build. To download and install one, follow these steps:

Unreal Engine on Linux supports precompiled installed builds as well as source code builds. For information about using source builds, refer to [Building Unreal Engine from Source](https://dev.epicgames.com/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine).

To use a precompiled build, follow these steps:

1.  Open the [Unreal Engine for Linux](https://www.unrealengine.com/en-US/linux) page. It will prompt you to to create or sign into an Epic Games account. If you already have one, sign in to access the page. If you don't have an account, click **Sign Up** to create one.
    
    [![Log in or sign up](https://dev.epicgames.com/community/api/documentation/image/3f3e7322-a09d-4bd6-a1bb-8b793e24b69d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3f3e7322-a09d-4bd6-a1bb-8b793e24b69d?resizing_type=fit)
    
    You can sign up for an Epic Games account with your email, or with a supported social media or gaming platform account.
    
    [![Choose how to sign in](https://dev.epicgames.com/community/api/documentation/image/324b1ab1-4101-43b9-8a3a-94bfef7e1cee?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/324b1ab1-4101-43b9-8a3a-94bfef7e1cee?resizing_type=fit)
    
2.  Download the `.zip` file containing the version of Unreal Engine that you need.
    
    [![Download UE](https://dev.epicgames.com/community/api/documentation/image/eec9eed6-0919-42d2-bf35-872021e9fd5e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/eec9eed6-0919-42d2-bf35-872021e9fd5e?resizing_type=fit)
    
3.  Unzip the contents of the `.zip` file to your desired installation directory.
    
4.  Run `Engine/Binaries/Linux/UnrealEditor` from the Terminal to launch Unreal Engine.
    

### 2b. Build Unreal Engine from Source

To install Unreal Engine from source, refer to [Downloading Unreal Engine Source Code](https://dev.epicgames.com/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine). Once you have compiled the engine, run `Engine/Binaries/Linux/UnrealEditor` from the Terminal to launch Unreal Editor.

## 3\. Setting Up a New Project

Refer to the instructions in [Creating a New Project in Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine) for information on how to set up a new project. You don't need a specific template or project type for the purposes of this tutorial, but you should make sure it has **C++** enabled if you are setting up your environment for C++.

## 4\. Set Up Your Development Environment (C++)

If you are planning to develop C++ projects, you need to set up the clang toolchain and an IDE to work with Unreal Engine. While we don't require a specific IDE, we recommend using Visual Studio Code or Rider. This section provides instructions that are specific to Visual Studio Code, as it provides a common development environment for other operating systems as well.

1.  Install the custom clang toolchain for your setup. See [Linux Development Requirements](https://dev.epicgames.com/documentation/en-us/unreal-engine/linux-development-requirements-for-unreal-engine?application_version=5.5) for more information.
    
2.  Locate your Unreal Engine install directory and open `Build/BatchFiles/Linux`, then run `SetupToolchain.sh`.
    
3.  Download and install VS Code as well as the official C / C++ extension pack and C# extension. These are required for reading the source code for both Unreal Engine and its Build Tools.
    
4.  Either open Unreal Editor, open your **Editor Preferences**, and set your Source Code editor to Visual Studio Code, or modify `BaseEngine.ini` to include the following:
    
    C++
    
    `[/Script/SourceCodeAccess.SourceCodeAccessSettings]          PreferredAccessor=VisualStudioCode`
    
    \[/Script/SourceCodeAccess.SourceCodeAccessSettings\] PreferredAccessor=VisualStudioCode
    
    Copy full snippet(2 lines long)
    
5.  Run `GenerateProjectFiles.sh -vscode` to generate the VS Code workspace for either your engine distribution (in the case of a source code build) or your project. Add `-project=(path to your project)` to choose a specific project.
    

For information about configuring VS Code with IntelliSense and other helpful utilities, see [Setting Up VS Code for Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-visual-studio-code-for-unreal-engine).

## 5\. Build a Project

Now that your environment is fully set up, you should run a test build of your project to ensure your workflow is fully functioning.

### 5a. Build a Project In Unreal Editor

Open your project in Unreal Editor, then click the **Platforms** dropdown and click **Linux** \> **Package Project**. If your system is configured correctly, Unreal Engine will build, cook, and package your project.

### 5b. Build a Project Through the Command Line

To build a project through the Command Line, use the RunUAT script's **BuildCookRun** command detailed in the [Build Operations](https://dev.epicgames.com/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine) guide. The following is an example of a working BuildCookRun command:

C++

`[UE Root Directory]/RunUAT BuildCookRun -Build -Cook -Stage -Package -Run -Project=[ProjectName]`

\[UE Root Directory\]/RunUAT BuildCookRun -Build -Cook -Stage -Package -Run -Project=\[ProjectName\]

Copy full snippet(1 line long)

Alternatively, you can use the Turnkey command line to start the same process.

C++

`[UE Root Directory]/RunUAT Turnkey -command=ExecuteBuild -platform=Linux -Project=[ProjectName]`

\[UE Root Directory\]/RunUAT Turnkey -command=ExecuteBuild -platform=Linux -Project=\[ProjectName\]

Copy full snippet(1 line long)

Normally, you need to use RunUAT from your Unreal Engine source directory. To make this command simpler to run, define a `$UE_ROOT` environment variable. This makes it possible to use RunUAT with a command such as `$UE_ROOT/RunUAT BuildCookRun` instead of providing the entire path to the RunUAT script.
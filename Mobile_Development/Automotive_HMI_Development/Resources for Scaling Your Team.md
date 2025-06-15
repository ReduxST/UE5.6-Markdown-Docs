# Resources for Scaling Your Team

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/resources-for-scaling-your-unreal-engine-team](https://dev.epicgames.com/documentation/en-us/unreal-engine/resources-for-scaling-your-unreal-engine-team)  
**Processed:** 2025-06-14 16:47:13

---

Projects can face scaling challenges as their code and asset counts grow alongside their team size. To ensure your project runs as smoothly as possible, Epic Games provides a variety of tools alongside UE that can help with:

-   Distributing the engine and your project to your team.
    
-   Reducing compilation and packaging times.
    
-   Reducing the amount of hard drive space your project takes up.
    
-   Reducing the sync time for pulling updated code and assets from version control.
    
-   Setting up an automated build pipeline.
    
-   Setting up an automated testing pipeline.
    

All of this serves to decrease the friction each team member feels when working with Unreal Engine, and to decrease the iteration time for building, testing, and changing features.

### Manage Your Project With Version Control Software

*Version control* is an essential part of any game development project. A version control server stores a centralized, authoritative copy of the code and files for your project, while version control clients provide a way for team members to access and update those files. A “repository” is a distinctly versioned grouping of the files that are stored on a version control server, and “workspaces” are the client-side directories that each store that client’s copy of a particular repository.

A version control integration provides ways to:

-   Pull a copy of the project to a local machine.
    
-   Review and commit code and assets.
    
-   Separate workstreams to prevent conflicts.
    
-   Check out, lock, and release files to prevent multiple team members from working on the same file.
    
-   Compare (diff) and merge files.
    

Additionally, version control keeps a running list of the changes committed to the repository, making it possible to easily roll back to an earlier version of assets or code if a change causes problems.

UE supports the following version control integrations:

-   Perforce
    
-   Git with GitLFS
    
-   Subversion
    
-   Diversion
    

Setting up one of these for your project should be the first thing you do before anyone starts working on assets or code. All of them are acceptable, but Epic Games primarily uses Perforce, and many features in this guide revolve around UE's Perforce integration. Once your project has a repository, you can integrate it with the Content Browser to check out and manage files directly from within Unreal Editor. 

For more information about how to use version control with UE, see the \[source control\](understanding-the-basics\\source-control) page and the \[Collaboration and Version Control\](setting-up-your-production-pipeline\\collaboration-in-unreal-engine) section.

### Distribute Your Project With Unreal Game Sync

**Unreal Game Sync** (**UGS**) is a client that interfaces with the Perforce, Unreal Build Tool, and your IDE (if applicable) to make it easy for team members to download or compile working builds of your project. Once you have UGS set up, users can select their `.uproject` file, see a list of builds for that project, and find builds that are verified as working. If you have an IDE installed, you can then pull and build the source files with a single command. If you don't, you can find builds that come with pre-built binaries and download those instead.

For more information, see the [UGS documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-ugs-for-unreal-engine).

### Create Offline Installers For Your Team

If you have forked and customized your engine source, you may want  to create an **installed build**, and package it as an **offline installer** of Unreal Engine. To learn more about creating offline installers, see the [Creating Installed Builds](https://dev.epicgames.com/documentation/en-us/unreal-engine/create-an-installed-build-of-unreal-engine) and [Installed Builds reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/installed-build-reference-guide-for-unreal-engine) pages.

### Reduce Excessive C++ Compilation With Unreal Engine Modules and ICWYU

The more C++ code you have in your project, the longer it will take to compile from your IDE. Therefore, it's typical for C++ compilation times to increase over the course of a project. For especially large projects, this can hamper iteration time for programmers.

UE's architecture breaks code up into modules to mitigate this issue. When you organize your code into modules, only the code in the module you're working on will recompile, while other modules will remain untouched. There are other benefits to using modules as well, which you can read about in the [Unreal Engine Modules](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-modules) section and [Editor Modules](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-editor-modules-for-customizing-the-editor-in-unreal-engine) page.

UE's codebase also uses an **Include What You Use** (**IWYU**) paradigm, which can also reduce build times by using `#include` statements and forward declarations more efficiently. For more information, see the [Include What You Use](https://dev.epicgames.com/documentation/en-us/unreal-engine/include-what-you-use-iwyu-for-unreal-engine-programming) page.

### Create Automated Builds With UAT, BuildGraph, and Horde

While you can package projects from Unreal Editor, the [BuildCookRun](https://dev.epicgames.com/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine) command for **Unreal Automation Tool** (**UAT**) is the underlying mechanism for creating packaged builds, and you can access it with any command line interface for your operating system. UAT has many scripts that can help automate the build process in scenarios where it isn’t viable to use a GUI, such as setting up a build server to automatically compile each submission to your version control system. You can script your own automated build pipeline with UAT's BuildCookRun command for a direct and simple approach, or you can use [BuildGraph](https://dev.epicgames.com/documentation/en-us/unreal-engine/buildgraph) to set up a more detailed system of automated builds. 

[Horde](https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-in-unreal-engine) is a robust continuous integration suite built on top of the BuildGraph framework, and includes a variety of tools for monitoring build health, integrating with task tracking software, managing remote testing devices, and providing detailed analytics and logs. As an added benefit, Horde also provides support for [Unreal Build Accelerator (UBA)](https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-unreal-build-accelerator-and-remote-compilation-tutorial-for-unreal-engine), which can improve compilation speed by distributing work across several servers and/or workstations.

If you want to customize your build pipeline, see the [Unreal Build System](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-unreal-engine-build-pipeline) section for a full reference for Automation Tool and Build Tool.

## Speed Up Cook Time With Multi-Process Cook

When you package a build, UE cooks your project's assets for your target platform, converting them to a format that is compatible with it and applying any compression settings you have set for it. Normally, this is a single process, but to speed up cook time you can enable multi-process cooking and configure the number of concurrent cook processes you want to use. See the [Multi-Process Cook](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-multi-process-cooking-for-unreal-engine) guide for more information.

## Streamline Asset Management With Virtual Assets

As the number and size of assets in your project grows, it can dramatically slow down the time it takes for team members to update their project from source control, as well as increase the amount of hard drive space a local copy of the project uses.

To counteract this, Unreal Engine supports **Virtual Assets**. These separate assets' main data from the metadata they use to display in your editor's content browser. When your team members sync the project, they only sync the metadata, which uses a much smaller amount of space than the full asset. When they need to actually access the asset to view or change it, UE pulls its bulk data from your team's repository or a **Derived Data Cache** (**DDC**) on-demand.

For more information, see the [Virtual Assets](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-assets-in-unreal-engine) documentation.

### Reduce Editor Shader Compile Times With Derived Data Cache

Many assets in UE use **derived data**. For example, when you create materials, Unreal needs to compile shaders afterward before the materials can fully display. The files in your version control system hold the instructions needed to create the shader which are common across all platforms and conducive to editing; derived data exists as a distinct concept and mechanism both because storing it in the same file as its origin data can make your repository burdensomely large, and because the exact format of a compiled shader can be different depending on which hardware and operating system you’re using. As your project or team gets larger, this can become a cumbersome process when you need to fetch large changes, especially if you need to re-download your project from scratch.

**Derived Data Caches** (**DDCs**) act as a secondary repository specifically for this type of derived data. When one user compiles or cooks an asset, they add the derived data to the DDC. Then, when other users with compatible hardware sync the asset, UE can pull both the asset and its derived data – meaning that they don't have to re-compile it from scratch. Unlike Version Control, DDCs usually do not retain every version of every file ever submitted, keeping only the most recent data up to a specified limit. In the rare circumstance someone needs to check out a very old version of the project, the derived data can always be regenerated. You can deploy a wide variety of shared DDCs in different locations relative to your staff, and define rules for how your team members access them to ensure they pull from the fastest and most reliable sources.

For more information about using DDCs, see the [Derived Data Cache documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-derived-data-cache-in-unreal-engine). UE supports multiple methods of hosting a shared DDC, but we recommend [Zen Storage Server](https://dev.epicgames.com/documentation/en-us/unreal-engine/zen-storage-server-for-unreal-engine).

### Scale Your Testing With Automated Tests

UE has a variety of automated testing frameworks for testing code in different contexts. These can help you detect bugs in your code earlier and more frequently, and give QA testers more room to focus on user experience issues. For more information, see the [Automation Test Framework](https://dev.epicgames.com/documentation/en-us/unreal-engine/automation-test-framework-in-unreal-engine) section.
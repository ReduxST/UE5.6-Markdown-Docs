# Horde UnrealGameSync Tutorial

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-unrealgamesync-tutorial-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-unrealgamesync-tutorial-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:26

---

## Introduction

Projects built with Unreal Engine typically require close collaboration between artists, designers and engineers - especially with technologies such as Blueprint, which allow interop of C++ code and gameplay scripting.

Coordinating these development efforts can be challenging due to the way that different developers interact with the revision control system - engineers may modify code and build their own editor, then submit assets created with those code changes, for example - and artists need to be able to sync and use those same assets in lock-step, without having to navigate a code IDE.

**UnrealGameSync** (often abbreviated as **UGS**) is a tool to provide a unified frontend to developers syncing a project from **Perforce**, providing content creators and engineers with the same view of the repository. Engineers can use it to version their editor correctly for editing assets, and content creators can use it to sync pre-built editor binaries produced by Horde's build automation system. The interface provides an overview of the health of the project and the state of recent CI builds, and acts as a jumping-off point for launching other tools.

Epic Games uses UnrealGameSync for development on all internal projects, such as Fortnite. More information about UnrealGameSync can be [found here](/documentation/en-us/unreal-engine/unreal-game-sync-ugs-for-unreal-engine).

The graphical UnrealGameSync client is only available on Windows. A command line version is available for use on MacOS and Linux.

![UnrealGameSync](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efb65482-9b1e-42ad-bccc-6b2606f8d810/unrealgamesync-main.png)

## Prerequisites

-   Horde Server installation (see the [Horde Installation Tutorial](/documentation/en-us/unreal-engine/horde-installation-tutorial-for-unreal-engine)).

## Installation (Windows)

1.  Navigate to the `Tools > Downloads` page on the Horde dashboard.
2.  Click the `Download` button to the right of the `UnrealGameSync` item, and run the downloaded installer.
3.  After installation, you'll be prompted to configure auto-update settings for UnrealGameSync. Select 'Horde' and enter the path to your Horde server. This will also configure UnrealGameSync to fetch build information and metadata from other users from Horde.
    
    You can modify this later using the `Options > Application Settings...` dialog inside UnrealGameSync.
    
4.  Select `Open Project...`, and select a project you already have synced locally, or create a new workspace with the project to sync.

## Installation (Mac)

1.  Install the [.NET 8 Runtime](https://dotnet.microsoft.com/en-us/download) and [Helix Command Line Tools](https://www.perforce.com/products/helix-core-apps/command-line-client).
    
2.  Open a terminal and run:
    
    ```shell
         `curl "{{ HORDE_SERVER_URL }}/api/v1/tools/ugs-cmd?action=download" -o ~/ugs.zip      unzip -eo ~/ugs.zip -d ~/ugs/      ~/ugs/ugs install      source ~/.zshrc`
    Copy full snippet
    ```
    curl "{{ HORDE\_SERVER\_URL }}/api/v1/tools/ugs-cmd?action=download" -o ~/ugs.zip unzip -eo ~/ugs.zip -d ~/ugs/ ~/ugs/ugs install source ~/.zshrc
3.  Run `ugs -help` for information on available commands.
    

## Installation (Linux)

1.  Install the [.NET 8 Runtime](https://dotnet.microsoft.com/en-us/download) and [Helix Command Line Tools](https://www.perforce.com/products/helix-core-apps/command-line-client).
    
2.  Open a terminal and run:
    
    ```shell
         `curl "{{ HORDE_SERVER_URL }}/api/v1/tools/ugs-cmd?action=download" -o ~/ugs.zip      unzip -eo ~/ugs.zip -d ~/ugs/      ~/ugs/ugs install      source ~/.bashrc`
    Copy full snippet
    ```
    curl "{{ HORDE\_SERVER\_URL }}/api/v1/tools/ugs-cmd?action=download" -o ~/ugs.zip unzip -eo ~/ugs.zip -d ~/ugs/ ~/ugs/ugs install source ~/.bashrc
3.  Run `ugs -help` for information on available commands.
    

## Server Setup

### Default Perforce Server

-   If your whole team uses the same Perforce server, you can configure UGS with a default value by modifying the server's [globals.json](/documentation/en-us/unreal-engine/horde-orientation-for-unreal-engine) file. As long as UGS is configured to use your Horde server, it will query this property on startup.
    
    ```
          `"parameters": {           "ugs":            {               // Set the default Perforce server for anyone using UGS.               "defaultPerforceServer": "perforce:1666"           }       }`
    Copy full snippet
    ```
    "parameters": { "ugs": { // Set the default Perforce server for anyone using UGS. "defaultPerforceServer": "perforce:1666" } }

### Editor Builds

UnrealGameSync was originally created with small teams in mind, where artists would be able to sync and build code code changes locally without any infrastructure (eg. a CI/CD system) set up. While it can still be used in this way, for larger teams it's typically easier to have Horde's build automation system generate editor builds centrally.

UnrealGameSync can query Horde for available editor builds (often referred to aspre-compiled binaries or PCBs). These builds can be stored and discovered on the Horde server automatically. Earlier builds of UnrealGameSync required storing these binaries in a zip file in Perforce; this is no longer necessary.

The example stream configuration referenced from Horde's [build automation](/documentation/en-us/unreal-engine/horde-build-automation-tutorial-for-unreal-engine) tutorial guide includes an **Incremental Build** job template which will compile and upload these binaries using the `Engine/Build/Graph/Examples/BuildEditorAndTools.xml` [BuildGraph](/documentation/en-us/unreal-engine/buildgraph-for-unreal-engine) script.

Once you've built your project's editor on Horde, check the `Options > Sync Precompiled Binaries` option to download them rather than building locally.

### Badges

You can surface information from Horde's build automation system directly in UGS by using the BuildGraph `<Label>` element.
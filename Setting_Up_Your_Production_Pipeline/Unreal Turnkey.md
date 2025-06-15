# Unreal Turnkey

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/automating-platform-and-sdk-management-with-unreal-turnkey](https://dev.epicgames.com/documentation/en-us/unreal-engine/automating-platform-and-sdk-management-with-unreal-turnkey)  
**Processed:** 2025-06-14 16:09:22

---

**Turnkey** is a system introduced in **Unreal Engine 5** that automates most of the steps required for setting up platform support, including finding source files for installing SDKs and flashing dev kits.

Once your organization has set up a filesource repository for Turnkey, individual team members can use a one-click process to set up their system for any target platform. The guides listed on this page will show you how to host SDKs for Turnkey, and how to use Turnkey to download and install them on individual instances of Unreal Engine.

## Overview

Turnkey is an **AutomationTool** script, accessed through `RunUAT.bat`, featuring many tools you can use to interact with SDKs. It accesses the repository you set up for your organization, then automatically downloads files and sets up SDKs from that repository.

When you run Turnkey to install an SDK, it performs the following processes:

-   Turnkey starts up and scans for SDKs using the information provided by `TurnkeyManifest.xml`.
-   Turnkey selects a platform based on the user's input.
-   The build system tells Turnkey what versions of the SDK are valid for the current Unreal Engine version.
-   The best SDK is selected from all of the valid SDKs available.
    -   Turnkey uses a series of platform-specific rules to convert the version numbers to integers, and the largest number within the range of valid SDKs is selected. These rules are specified in the `*PlatformSDK.cs` files.
-   Turnkey downloads the SDK files to the user's machine.
    -   If the SDK files are contained in a `.zip` file, they will be automatically decompressed in a temporary location.
-   The build system installs the downloaded SDKs.

This provides a way to quickly set up your Unreal Engine project even if there are a large number of available SDK versions, and streamlines maintenance whenever you need to update your available SDKs.

## Setting Up Turnkey

To use Turnkey, you need to host your SDKs in a filesource repository, then set up `TurnkeyManifest.xml` and `TurnkeyStudioSettings.xml` files with the necessary information for Turnkey to discover them.

The pages listed below provide instructions on how to set up each of these components, as well as how to structure directories so that Turnkey's automation will recognize your SDK versions.

## Usage

Once you have set up Turnkey for your organization, users can interact with it either directly from within Unreal Engine, or using `RunUAT.bat` with a command-line interface. The pages listed below contain information about how to use each of these.
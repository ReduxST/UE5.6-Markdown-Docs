# Supporting Universal Binaries for macOS

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/supporting-universal-binaries-for-macos-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/supporting-universal-binaries-for-macos-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:12

---

With the introduction of Apple's M1 processor, Macs from 2021 onward are manufactured using the ARM64 architecture. Meanwhile, the previous generation of Intel-based Macs use an x86-64 architecture.

Although Apple provides an instruction translator called **Rosetta2** to support legacy applications, Apple's storefronts require developers to provide a single universal binary for games that features slices for both architectures. This ensures the best possible performance and stability on both generations of hardware. This page provides information about Unreal Engine's compatibility with both architectures as well as instructions on how to accommodate universal binaries.

## Prerequisites

The instructions on this page assume that you are building your projects using Xcode on macOS. You should also familiarize yourself with [**Unreal Automation Tool**](/documentation/en-us/unreal-engine/unreal-automation-tool-for-unreal-engine) (UAT) and the **BuildCookRun** command before proceeding.

## Configuring Your macOS Architecture

You can specify your target architecture for builds in several ways:

-   In UAT, use the `-specifiedarchitecture` or `-architecture=` parameter to set the architecture you want to compile with.
-   In Xcode, select your target device from the dropdown at the top of the IDE.
-   In Unreal Editor, click Platforms > macOS and choose

The following are the valid architectures for Apple devices:

| Architecture | Compatible Devices |
| --- | --- |
| `x86_64` | MacOS devices using Intel processors. |
| `arm64` | MacOS devices using M1 and M2 processes or newer. |
| `arm64+x86_64` | All MacOS devices. |

## Universal Binary Support for Unreal Editor

In UE 5.2+, macOS builds of Unreal Editor distributed with the Epic Games Launcher are built with universal binaries. Unreal Editor will automatically use whichever slice is appropriate for your device's architecture.

When you build your editor from source in Xcode, it will automatically use the x64 architecture, but you can set the architecture to `arm64+x86_64` to build the editor with universal binaries instead.

To build your editor for x86 instead, change your target device from **My Mac** to **My Mac (Rosetta)**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f7e2ddd-98a7-4b75-a40f-f26194853697/mymacrosetta.png)

## Creating Binaries for ARM64 and x86-64

To build a project with universal binaries, use `arm64+x86_64` as your architecture in `BuildCookRun`.

```
	`-specifiedarchitecture=arm64+x86_64`
Copy full snippet
```
\-specifiedarchitecture=arm64+x86\_64

This will build a project that includes slices for both ARM64 and x86-64 architectures. You can distribute these builds to either type of device, and they will use the appropriate binaries for their architecture automatically.
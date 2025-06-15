# AutoSDK Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-autosdk-system-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-autosdk-system-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:18

---

The **AutoSDK** system provides a mechanism for distributing target platform SDKs and configuring them for use by the engine on demand. It was designed for build machines to serve multiple branches with different SDK requirements without needing to manually manage installed packages, but may also be used by developers that do not require a full SDK install. Typically, only a minimal toolset is available by default (for example, a compiler or deployment software).

[UnrealBuildTool](/documentation/en-us/unreal-engine/unreal-build-tool-in-unreal-engine), [AutomationTool](/documentation/en-us/unreal-engine/unreal-automation-tool-for-unreal-engine), and the Unreal Editor are all designed to work seamlessly with AutoSDK, and the switch between SDKs is handled by UnrealBuildTool (UBT), which is invoked by the other tools.

For any engine verison, UnrealBuildTool has a preferred SDK version that it will attempt to use. These versions are typically defined by classes derived from `UEBuildPlatform` in the UBT source code.

## Setup

Epic is not able to distribute SDKs for legal reasons, so this directory tree serves a template showing how to structure it. We recommend you start with an empty AutoSDK folder and copy files from here as you add a particular SDK version.

Do not configure the AutoSDK system to use this folder. It is just a template, and the system will not work without adding additional files.

So that multiple branches on a single machine can share it, the AutoSDK folder should be submitted to source control separately to the game or engine code.

Any developer wishing to use AutoSDK can sync it and set the `UE_SDKS_ROOT` environment variable to point to the path on their local machine for UBT, which contains it.

## Layout

The AutoSDK directory structure is loosely defined and generally left to the discretion of each platform, but the directory structure follows this general pattern.

| Directory Structure | Definition |
| --- | --- |
| `/HostPlatform/` | Host platform that the SDKs can be used on. |
| `/HostPlatform/TargetPlatform/` | Directory containing the "TargetPlatform" SDKs for "HostPlatform" (for example, "/HostWin64/Android/"). |
| `/HostPlatform/TargetPlatform/1.0/` | Directory containing the "TargetPlatform" 1.0 SDK for "HostPlatform". |
| `/HostPlatform/TargetPlatform/1.0/Setup.bat` | Optional batch file that is run when setting up this SDK. "setup.sh" on Mac/Linux. |
| `/HostPlatform/TargetPlatform/1.0/Unsetup.bat` | Optional batch file that is run when removing this SDK. "unsetup.sh" on Mac/Linux. |

When run, Setup.bat will output a text file to the same directory called `OutputEnvVars.txt`, containing a list of environment variables to set in the form of `NAME=VALUE` as well as special directives to modify the `PATH` environment variable, such as `ADDPATH=Foo` and `STRIPPATH=Foo`.

Setup scripts written by Epic for supported SDK versions are included under this directory.

## Platforms

More information about adding SDKs for each platform is given by README.md files in HostPlatform/TargetPlatform subfolders.
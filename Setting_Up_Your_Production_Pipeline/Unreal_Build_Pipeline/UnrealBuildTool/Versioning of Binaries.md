# Versioning of Binaries

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-version-binaries-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-version-binaries-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:39

---

The **Unreal Engine (UE)** **BuildID** system mitigates potential errors that may result from outdated DLL files. This system not only prevents crashes or failed library linkage, but also hard-to-track bugs that may arise from stale binaries, by loading only DLLs that were compiled at the same time as the executable file itself. The Build ID is typically generated automatically at compile-time, producing a new, unique value every time the Engine is built. However, you can override it with a manually specified value.

## Automatically-Generated Build ID

At build time, every output directory that contains at least one compiled DLL receives a JSON file with the `.modules` extension, such as `UnrealEditor.modules`. This file lists each Module in the directory and the associated DLL for that Module, as well as a GUID for the build itself. Every time the Engine compiles, it generates a new GUID, so that DLLs from other compilation sessions will be recognizable, and the Engine can ignore them. When using source control to maintaining a binary build, you must check in the executable, all DLLs, and their associated `.modules` files together to ensure that the Build ID matches.

## Manually-Specified Build ID

It is possible to force your Build ID to a specific value. You can accomplish this by adding a `BuildId` entry (as a string variable) to your `Build/Build.version` JSON file, but it is not recommended, as it removes the check to prevent using incompatible Modules. It is particularly easy to run outdated code if using a forced Build ID with Plugins that may be shared between multiple Projects.
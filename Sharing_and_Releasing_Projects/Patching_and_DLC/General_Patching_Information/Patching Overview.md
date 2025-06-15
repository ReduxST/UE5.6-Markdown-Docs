# Patching Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/updating-unreal-engine-projects-with-patches-after-release](https://dev.epicgames.com/documentation/en-us/unreal-engine/updating-unreal-engine-projects-with-patches-after-release)  
**Processed:** 2025-06-14 16:57:44

---

Once you have released your project, you will probably make updates to it after the initial release. This process is known as **patching**. Patching usually includes new content that addresses known issues, or that fixes vulnerabilities in the original release.

## Different Methods for Patching

There are several methods for creating patches, but they all use one of two approaches. One approach keeps files from the original release or previous patches, but adds a pointer to new content. The other approach is to transform the content in the original build using a binary patch.

You can build patches in **Unreal Engine** (UE) for many different platforms. However, it does not support distribution of patches for your project. Each platform has their own system for uploading patch files, and for distributing those patch files to users. For information on these platform-specific distribution systems, see the documentation for that platform's **Software Development Kit (SDK)**.

## Platform-Agnostic Patching Method

There is a method for creating patches in Unreal Engine that will technically work on any platform. This method packages the entire build with new content, while the changes between the two builds are placed in a sidecar file that is added to the original file. The new **PAK** file is labeled with a `_p` suffix. For example, if the original build file is called `MyGamesStuff.pak`, your patch file would be called `MyGamesStuff_p.pak`.

### Windows Patching

Windows uses the method described in [Platform-Agnostic Patching Method](/documentation/en-us/unreal-engine/updating-unreal-engine-projects-with-patches-after-release#platform-agnosticpatchingmethod) .

For more information on platform-agnostic patching, see [How to Create a Patch](/documentation/en-us/unreal-engine/how-to-create-a-patch-in-unreal-engine).
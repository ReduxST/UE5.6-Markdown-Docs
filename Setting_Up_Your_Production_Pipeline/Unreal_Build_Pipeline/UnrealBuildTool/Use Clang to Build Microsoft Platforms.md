# Use Clang to Build Microsoft Platforms

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/use-clang-to-build-microsoft-platforms-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/use-clang-to-build-microsoft-platforms-in-unreal-engine)  
**Processed:** 2025-06-14 16:57:51

---

**Unreal Engine (UE)** supports using the **Clang** compiler on Windows to build [supported Microsoft platforms](/documentation/en-us/unreal-engine/sharing-and-releasing-projects-for-unreal-engine#microsoftwindowsandxboxconsoles). You can enable Clang with:

-   [Build Configuration](/documentation/en-us/unreal-engine/use-clang-to-build-microsoft-platforms-in-unreal-engine#buildconfiguration)
-   [Command-Line Arguments](/documentation/en-us/unreal-engine/use-clang-to-build-microsoft-platforms-in-unreal-engine#command-linearguments)
-   [Engine Configuration](/documentation/en-us/unreal-engine/use-clang-to-build-microsoft-platforms-in-unreal-engine#engineconfiguration)

This page also includes a table of additional options, such as specifying:

-   Clang linker
-   Clang version
-   MSVC version
-   Toolchain version

For more information, see the [Additional Options](/documentation/en-us/unreal-engine/use-clang-to-build-microsoft-platforms-in-unreal-engine#additionaloptions) section below. As of UE 5.3, the latest supported version of Clang is [Clang 16](https://releases.llvm.org/16.0.0/tools/clang/docs/index.html).

## What is Clang

Clang is a front-end compiler that compiles C, C++, Objective-C, and Objective-C++ into machine code. Clang is an alternative to the MSVC (Microsoft Visual C++) compiler.

## Install Clang

You can install Clang through [Visual Studio](https://learn.microsoft.com/en-us/cpp/build/clang-support-msbuild?view=msvc-170) or directly from the [LLVM Downloads](https://releases.llvm.org/download.html) page.

## Enable Clang

Once you have installed Clang, follow any one of the methods below to enable Clang in your Unreal project.

### Build Configuration

To enable Clang in [Build Configuration](/documentation/en-us/unreal-engine/build-configuration-for-unreal-engine), navigate to an engine `BuildConfiguration.xml` file, and add the following:

```
`<?xml version="1.0" encoding="utf-8" ?> <Configuration xmlns="https://www.unrealengine.com/BuildConfiguration"> 	... 	<WindowsPlatform>       		<Compiler>Clang</Compiler> 	</WindowsPlatform> ... </Configuration>`
Copy full snippet
```
<?xml version="1.0" encoding="utf-8" ?> <Configuration xmlns="https://www.unrealengine.com/BuildConfiguration"> ... <WindowsPlatform> <Compiler>Clang</Compiler> </WindowsPlatform> ... </Configuration>

### Command-Line Arguments

To enable Clang with [Command-Line Arguments](/documentation/en-us/unreal-engine/command-line-arguments-in-unreal-engine), pass the `-Compiler=Clang` option.

### Engine Configuration

To enable Clang in [Engine Configuration](/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine), navigate to an engine configuration file, such as `DefaultEngine.ini`, and add the following:

```
`[/Script/WindowsTargetPlatform.WindowsTargetSettings] CompilerVersion=Clang`
Copy full snippet
```
\[/Script/WindowsTargetPlatform.WindowsTargetSettings\] CompilerVersion=Clang

## Additional Options

The following options assume that:

-   Build Configuration options are added inside the `<WindowsPlatform>...</WindowsPlatform>` section of `BuildConfiguration.xml`.
-   Engine Configuration options are added to the `[/Script/WindowsTargetPlatform.WindowsTargetSettings]` section of an engine configuration file, such as `DefaultEngine.ini`.

| **Option** | **Build Configuration** | **Command-Line Argument** | **Engine Configuration** |
| --- | --- | --- | --- |
| Clang linker | `<bAllowClangLinker>true</bAllowClangLinker>` | `-ClangLinker` | `bAllowClangLinker=true` |
| Clang Compiler Version | `<CompilerVersion>Latest</CompilerVersion>` | `-CompilerVersion=Latest` | `CompilerVersion=Latest` |
| MSVC Version | `<Toolchain>VisualStudio2022</VisualStudio>` | `-VCToolchain=VisualStudio2022` | `Toolchain=VisualStudio2022` |
| Toolchain Version | `<ToolchainVersion>Latest</ToolchainVersion>` | `-VCToolchainVersion=Latest` | `ToolchainVersion=Latest` |

### Clang Linker

The Clang Linker is a boolean option that determines whether the Clang Linker is used when compiling with Clang.

Epic does not use the Clang linker for Microsoft platforms and it is not currently tested.

### Clang Compiler Version

The Clang compiler version is a string option that determines which version of the specified compiler is used. The options include:

-   Specific version number: Use the exact version specified, for example, "16.0.0".
-   Latest: Use the newest installed version.

### MSVC Version

The MSVC Toolchain is a string option that determines which toolchain is used. The options include:

-   VisualStudio2022

### Toolchain Version

The Toolchain version is a string option that determines which version of the MSVC toolchain is used. The options include:

-   Specific version number: Use the exact version specified, for example, "14.37.32822".
-   Latest: Use the newest installed version.
-   Preview: Use the newest installed preview version.

## More Information

Follow these links for information about:

-   [Windows Platform](/documentation/en-us/unreal-engine/build-configuration-for-unreal-engine#windowsplatform) section of [Build Configuration](/documentation/en-us/unreal-engine/build-configuration-for-unreal-engine)
-   [Command-Line Arguments](/documentation/en-us/unreal-engine/command-line-arguments-in-unreal-engine)
-   [Engine Configuration Files](/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine)
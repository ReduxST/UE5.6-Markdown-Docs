# Third-Party Libraries

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/integrating-third-party-libraries-into-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/integrating-third-party-libraries-into-unreal-engine)  
**Processed:** 2025-06-14 16:31:18

---

This document explains how to integrate third-party libraries, including standard patterns for adding libraries, special considerations for dynamic libraries, dependency staging, and helpful information for errors you may encounter while integrating a third-party library into your Unreal project.

The **Unreal Engine (UE)** source code includes several third-party libraries, which are stored under `UnrealEngine/Engine/Source/ThirdParty/..` This is a convention for engine modules, and not required. When developing plugins that use third-party libraries, it is more convenient to include the third-party software within the plugin directory.

## Third-Party Plugin Template

The plugin browser in the editor has a template for integrating third-party libraries. To create a new plugin using this, select **New Plugin** from the plugin browser window and scroll down to the **Third Party Plugin** template.

## Module Setup

Regular Unreal Engine C++ modules are configured using a `.build.cs` file, and third-party libraries are no different. To create a module that doesn't have any source code and exists for consumption by other modules, create a `.build.cs` for your plugin like this:

```
	`using System; 	using System.IO; 	using UnrealBuildTool;  	public class MyThirdPartyLibrary : ModuleRules 	{ 		public MyThirdPartyLibrary(ReadOnlyTargetRules Target) : base(Target) 		{ 			Type = ModuleType.External;  			// Add any macros that need to be set 			PublicDefinitions.Add("WITH_MYTHIRDPARTYLIBRARY=1");  			// Add any include paths for the plugin 			PublicIncludePaths.Add(Path.Combine(ModuleDirectory, "inc"));  			// Add any import libraries or static libraries 			PublicAdditionalLibraries.Add(Path.Combine(ModuleDirectory, "lib", "foo.a")); 		} 	}`

Copy full snippet
```
using System; using System.IO; using UnrealBuildTool; public class MyThirdPartyLibrary : ModuleRules { public MyThirdPartyLibrary(ReadOnlyTargetRules Target) : base(Target) { Type = ModuleType.External; // Add any macros that need to be set PublicDefinitions.Add("WITH\_MYTHIRDPARTYLIBRARY=1"); // Add any include paths for the plugin PublicIncludePaths.Add(Path.Combine(ModuleDirectory, "inc")); // Add any import libraries or static libraries PublicAdditionalLibraries.Add(Path.Combine(ModuleDirectory, "lib", "foo.a")); } }

The `.build.cs` should be in a normal folder where the engine looks for modules, such as `Engine/Source` or `MyProject/Source`.

The **ModuleType.External** setting tells the engine not to look for (or compile) source code. It will use the other settings you define in that file by adding the listed include paths to the compile environment, setting the appropriate macros, and linking against the given static libraries.

## Dynamic Libraries

### Windows

Windows has a fairly inflexible model for loading DLLs. Each executable or DLL stores a list of the DLLs it depends on in its *import table*, and the OS scans this list when loading the module in order to satisfy those dependencies.

The names of dependency DLLs are stored by name only (for example, without any path information), and the operating system searches a short list of paths to try to find them. Since this happens without the application being able to specify the location of dependent DLLs, it can be the source of obscure errors at startup.

#### FPlatformProcess::GetDllHandle

Any DLL loads explicitly triggered by the engine use the `FPlatformProcess::GetDllHandle()` function. This has special logic to read each DLLs import table before loading it, and attempts to resolve any DLL dependencies to files in the engine's list of search paths (for example, all project, engine, and plugin "Binaries" directories).

When the operating system comes to load the new DLL, if a DLL of the same name is already in memory, it will link against that rather than trying to load a new module from disk.

The `GetDllHandle` function produces a lot of verbose output to the log if it fails to load a dependency, which can be very valuable in tracking down errors.

#### Delay Loading DLLs

If the DLL exists in a path not normally searched by the engine, an alternative strategy is to delay load it. Since the operating system only attempts to load the DLL the first time you call a function in it, you can execute explicitly logic to load it from a particular location. When the OS finally comes to doing the delay load, it will find the existing DLL with the same name already loaded into the process, and resolve to that instead of searching on disk.

Delay loading works by pointing imported functions to a thunk function that loads the real DLL. After the real DLL has been loaded, the import table is modified to point to the real DLLs function addresses rather than the thunk functions, and execution continues as normal.

This mechanism is not possible if you access variables in the DLL. The linker will give you an error if you try to delay load a DLL that is referenced in this way.

Delay-loaded DLLs can be specified from a `build.cs` file using a declaration like this:

```
	`PublicDelayLoadDLLs.Add("foo.dll")`

Copy full snippet
```
PublicDelayLoadDLLs.Add("foo.dll")

Note that a path to the DLL is unnecessary (only the name is used) since the linker does not concern itself with how the operating system resolves the DLL dependencies it adds to the import table.

#### Debugging DLL Loading Problems

[Dependency Walker](http://www.dependencywalker.com/) is useful for examining the DLLs and functions imported from a module. The verbose engine log output also includes the "Dependency Walker" tool.

### macOS

macOS executables and dylibs store the list of the dylibs they depend on in the form of install names. The install name can be an absolute or relative path to the dylib, or a path relative to one of three install paths: `@executable_path`, `@load_path` or `@rpath`. The most flexible of these options is `@rpath`, and that's what Unreal Engine uses.

[UnrealBuildTool](/documentation/en-us/unreal-engine/unreal-build-tool-in-unreal-engine) will automatically add `RPATH` search paths to the executable and dylibs it builds for all the third-party dylibs that are outside of `Engine/Source` and `MyProject/Source` subfolders. Storing third-party dylibs in `Source` subfolders is supported, but not recommended, as these folders are not part of the packaged game or binary version of the plugin, so the build system needs to handle them differently, copy them to a different location, among other things.

Install names are read from dylibs during linking, so the third-party library needs to have its install name set to `@rpath/libfoo.dylib`. This can be done in two ways, either by using `-install_name` linker option when building the library, or by using `install_name_tool` to modify it after the dylib was created, like this:

```
	`install_name_tool -id @rpath/libfoo.dylib /path/to/libfoo.dylib`

Copy full snippet
```
install\_name\_tool -id @rpath/libfoo.dylib /path/to/libfoo.dylib

For frameworks, you should use `PublicFrameworks` instead of `PublicAdditionalLibraries` in the `.build.cs` file, but other than that, the same rules apply, so it's best to use `@rpath` for the framework install name as well.

#### Delay Loading DLLs

Delay loading DLLs is not fully supported on macOS.

There's no equivalent of Windows `/DELAYLOAD`, so only one specific use of this feature is supported on macOS: linking with a library that may be unavailable on runtime. To implement that, UE uses weak linking.

#### Debugging dylib Loading Problems

From the command line, `otool` is useful to examine an executable or a dylib and look at its runtime dependencies. In particular, the `-L` and `-l` options are useful when debugging loading problems.

| Command | Description |
| --- | --- |
| `otool -L libname.dylib` | Lists the install names and version numbers of all the dylibs the executable or dylib depends on. In case of a dylib, the first item on the list is its own install name. |
| `otool -l libname.dylib` | Displays all load commands of the file. Look for `LC_LOAD_DYLIB` and `LC_RPATH` to see what the dynamic linker will try to load automatically and what the `RPATH` search paths are. |

### Linux

There is no way to change the paths in which `dlopen` searches at runtime, so all paths to search for Linux will be set under the `RPATH` for each module. You can use `readelf` to find the full `RPATH` list that is searched.

#### FPlatformProcess::GetDllHandle

All Unreal Engine modules will be dlopened as `RTLD_LAZY | RTLD_LOCAL`, while non-UE modules will all be first loaded as `LAZY | LOCAL` then re-opened as `LAZY | RTLD_GLOBAL`. This can cause specific issues where multiple UE modules have the same global symbol in which they will link to their local symbol versus a single global one, leading to odd crashes where global systems seem uninitialized. You can use `gdb` to print out locations it thinks it has stored versus the pointer you have of the global. If they are different, you most likely have multiple global definitions and modules binding to different ones.

#### Debugging SO Loading Problems

| Tool | Linux Manual Page | Brief Description |
| --- | --- | --- |
| ldd | http://man7.org/linux/man-pages/man1/ldd.1.html | This will tell you runtime dependencies, and possibly any missing dependencies. |
| nm | http://man7.org/linux/man-pages/man1/nm.1p.html | This is similar to "Dependency Walker", which can tell you about exported symbols (and if needed, all symbols). |
| readelf | http://man7.org/linux/man-pages/man1/readelf.1.html | Another tool to dump info about exported symbols and elf section offsets, among other things. |
| LD\_DEBUG | http://man7.org/linux/man-pages/man8/ld.so.8.html | Another way to figure out which symbols are being bound to which dynamic library. |
| strace | http://man7.org/linux/man-pages/man1/strace.1.html | This is a great tool to figure out the runtime system calls being used. This can tell which paths are being attempted to open/read from for `dlopen`. |

## Runtime Dependencies

To stage your third-party DLL next to the executable when you package your game, you can declare it as a runtime dependency from your `build.cs` file:

```
	`RuntimeDependencies.Add(Path.Combine(PluginDirectory, "Binaries/Win64/Foo.dll"));`

Copy full snippet
```
RuntimeDependencies.Add(Path.Combine(PluginDirectory, "Binaries/Win64/Foo.dll"));

This assumes that the DLL already exists in the given directory, and that the plugin will manually load it from that location. If you want to have the DLL copied to the same output directory as the executable at build time, you do so via an overload of the `RuntimeDependencies.Add` method:

```
	`RuntimeDependencies.Add("$(TargetOutputDir)/Foo.dll", Path.Combine(PluginDirectory, "Source/ThirdParty/bin/Foo.dll"));`

Copy full snippet
```
RuntimeDependencies.Add("$(TargetOutputDir)/Foo.dll", Path.Combine(PluginDirectory, "Source/ThirdParty/bin/Foo.dll"));

Other variables can be used for output paths of the DLL:

| Variable | Description |
| --- | --- |
| `$(EngineDir)` | The engine directory |
| `$(ProjectDir)` | Directory containing the project file |
| `$(ModuleDir)` | Directory containing the `.build.cs` file |
| `$(PluginDir)` | Directory containing the `.uplugin` file |
| `$(BinaryOutputDir)` | Directory containing the binary that this module is compiled into (for example, the path to the DLL for editor builds, and path to the executable (EXE) for packaged builds) |
| `$(TargetOutputDir)` | Directory containing the executable (including in editor builds) |

The `RuntimeDependencies` field is not limited to staging DLLs; you can also use it to inject additional files into the staging process. Those files can be stored in Unreal's [PAK files](/documentation/en-us/unreal-engine/API/Runtime/PakFile), or kept loose on disk. DLLs are loaded by the operating system, so they can't normally be stored in the PAK file.

```
	`RuntimeDependencies.Add(Path.Combine(PluginDirectory, "Extras/..."), StagedFileType.UFS);`

Copy full snippet
```
RuntimeDependencies.Add(Path.Combine(PluginDirectory, "Extras/..."), StagedFileType.UFS);

Possible values for StagedFileType are:

| Value | Description |
| --- | --- |
| `StagedFileType.UFS` | Only accessed through Unreal filesystem functions, and may be included in a PAK file. |
| `StagedFileType.NonUFS` | Must be kept as part of the loose filesystem. |
| `StagedFileType.DebugNonUFS` | Debug file which must be kept as part of the loose filesystem. Will not be included unless debug files are set to be staged. |
| `StagedFileType.SystemNonUFS` | System file which must be kept as part of the loose filesystem. System files are not subject to automatic remapping or renaming by the platform layer. |

## Troubleshooting

### Windows.h

The standard Windows header (`Windows.h`) is not included by default in most UE code. If you need it for third-party libraries, include it through the `WindowsHWrapper.h` file from the `Core` module.

```
	`#include "Windows/WindowsHWrapper.h"`

Copy full snippet
```
#include "Windows/WindowsHWrapper.h"

Many Windows functions are defined as macros for switching between ANSI and Unicode variants, which can create issues when unrelated code defines symbols with the same name. To prevent this, we undefine many macros defined by `Windows.h`. We recommend that you explicitly call the `...A` and `...W` variants of functions where possible (for example, `GetCommandLineA()` or `GetCommandLineW()`).

Windows macros for `TRUE` and `FALSE` are not portable and are redefined to a value that causes a compile error if used. If you need to enable them for a block of code, wrap it in includes of `AllowWindowsPlatformTypes.h` and `HideWindowsPlatformTypes.h`, like this:

```
	`#include "Windows/AllowWindowsPlatformTypes.h" 	int Foo = TRUE; 	#include "Windows/HideWindowsPlatformTypes.h"`

Copy full snippet
```
#include "Windows/AllowWindowsPlatformTypes.h" int Foo = TRUE; #include "Windows/HideWindowsPlatformTypes.h"

Similarly, Windows macros for atomic functions conflict with function names defined in `WindowsPlatformAtomics.h`. To restore those defines to their original values, include `AllowWindowsPlatformAtomics.h/HideWindowsPlatformAtomics.h`:

```
	`#include "Windows/AllowWindowsPlatformAtomics.h" 	//Code using InterlockedIncrement, ... 	#include "Windows/HideWindowsPlatformAtomics.h"`

Copy full snippet
```
#include "Windows/AllowWindowsPlatformAtomics.h" //Code using InterlockedIncrement, ... #include "Windows/HideWindowsPlatformAtomics.h"

### C++ Warnings and Errors

The Unreal Engine codebase has many warnings treated as errors by default. To relax some of these restrictions for third-party code, there are cross-platform macros to temporarily disable common warnings:

```
	`THIRD_PARTY_INCLUDES_START 	#include <openssl.h> 	THIRD_PARTY_INCLUDES_END`

Copy full snippet
```
THIRD\_PARTY\_INCLUDES\_START #include <openssl.h> THIRD\_PARTY\_INCLUDES\_END

### Default Packing and Alignment

For legacy reasons, Unreal Engine forces 4-byte packing on Win32. This can result in hard-to-debug alignment issues in classes that use 8-byte types such as doubles or longs. To restore the default packing around third-party code that defines 8-byte types in public structs, use the following macros:

```
	`PRAGMA_PUSH_PLATFORM_DEFAULT_PACKING 	#include <thirdparty.h> 	PRAGMA_POP_PLATFORM_DEFAULT_PACKING`

Copy full snippet
```
PRAGMA\_PUSH\_PLATFORM\_DEFAULT\_PACKING #include <thirdparty.h> PRAGMA\_POP\_PLATFORM\_DEFAULT\_PACKING

### RTTI Build Error

Linking your binary from source files compiled with different RTTI (run-time type information) flags may cause build errors on Windows. If you encounter RTTI build errors, you can either define a helper macro to mix RTTI on/off modules or, if you're building from source, you can enable RTTI for the entire engine by setting the `bForceEnableRTTI` to `true` in `TargetRules.cs`.

#### Linux

Linux does not allow mix and matching of RTTI modules. So if you have a module with RTTI, you need to enable it for the engine.

#### Dynamic Cast Error

If you use dynamic cast on an object type that is not a **UObject** type when RTTI is off, you will encounter the "can't use dynamic\_cast when RTTI is disabled error" because in `CoreUObject/Public/Templates/Casts.h`, `#define dynamic_cast` redirects **CUObject** modules. For UObject types, dynamic cast uses Unreal Engine's reflection system, but for other types, it uses regular `dynamic_cast`.
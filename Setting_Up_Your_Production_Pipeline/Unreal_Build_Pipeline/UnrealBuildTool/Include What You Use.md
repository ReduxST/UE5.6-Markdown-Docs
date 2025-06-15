# Include What You Use

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/include-what-you-use-iwyu-for-unreal-engine-programming](https://dev.epicgames.com/documentation/en-us/unreal-engine/include-what-you-use-iwyu-for-unreal-engine-programming)  
**Processed:** 2025-06-14 16:30:54

---

**Include What You Use (IWYU)**, as the name implies, means that **Unreal Engine (UE)** source code only includes the dependencies that it needs to compile. The purpose of IWYU is to avoid including monolithic header files, such as `Engine.h` or `UnrealEd.h`, thereby mitigating superfluous dependencies. The following reference guide tells you what it means to IWYU, including a high-level explanation of how to enable IWYU, ensuring that your project adheres to IWYU conventions. Additionally, if you opt into using IWYU mode for your game project or projects, you will learn some general tips that will help you get the most out of working in IWYU mode.

IWYU mode is disabled by default for games and game plugins; however, IWYU mode is enabled by default for the Engine and Engine plugins.

## What it Means to IWYU

In previous versions of Unreal Engine, the majority of engine functionality was included via large, module-centric header files, such as `Engine.h` and `UnrealEd.h` and fast compile times were dependent on those files being compiled quickly through **Precompiled Header (PCH)** files. As the engine grew, this became a bottleneck.

With IWYU, every file includes only what it needs, and any PCH file we choose to use, purely acts as a layer of optimization on top of the underlying source files. They can be modified to minimize build times, independently of changing the source files themselves, and without affecting whether the code compiles successfully or not.

When writing IWYU code, there are four specific conventions that we adopt:

1.  All header files include their required dependencies.
2.  `*.cpp` files include their matching `*.h` files first.
3.  Precompiled Header (PCH) files are no longer explicitly included.
4.  Monolithic header files are no longer included.

### IWYU Conventions

The following descriptions of IWYU conventions should give you a good idea about what it means to IWYU.

1.  All header files include their required dependencies.
    
    -   There is a **Core Minimal** header file (`CoreMinimal.h`) containing a set of ubiquitous types (including `FString`, `FName`, `TArray`, etc.) from UE's Core programming environment.
    -   The `CoreMinimal.h` header file (located under the UE root directory at `\Engine\Source\Runtime\Core\Public\CoreMinimal.h`) is included first by most of the Engine's header files.
    -   Within the `Core` module, most header files include the `CoreTypes.h` header file first. This only includes typedefs for primitive C++ types, UE build macros, and directives to configure the compile environment.
        
        The main takeaway is that every header file now includes everything that it needs to compile.
        
2.  `*.cpp` files include their matching `*.h` file first.
    
    -   To verify that all of your source files include all of their required dependencies, compile your game project in non-unity mode with PCH files disabled.
3.  PCH files are no longer explicitly included.
    
    -   Although PCH files are still used, they're force-included on the compiler command line by Unreal Build Tool (UBT).
4.  Monolithic header files are no longer included.
    
    -   The compiler will emit a warning if your Engine code includes monolithic header files (such as `Engine.h` or `UnrealEd.h`).
    
    Monolithic header files still exist in Unreal Engine for compatibility with game projects, and (by default) a warning will not be emitted if your game projects include them.
    

## Verifying IWYU is Enabled

Before establishing IWYU conventions, UE code typically included a PCH file at the top of every C++ file, which is contrary to what a developer wants their IWYU compliant code to include. Following IWYU conventions, PCH files can be thought of as layers of compile-time optizations that are applied separately from how the code was originally authored. So, rather than composing and including PCH files, we leave it to UBT to decide which PCH file to use (if any).

If you want to verify that IWYU is enabled, ensuring that a module complies with IWYU conventions, open the module's `*.build.cs` file and verify that `PCHUsage` is set to `PCHUsageMode.UseExplicitOrSharedPCHs`.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87d988d8-d7a6-41e7-bc17-2630417abfe2/exampleplugin_pchusage.png)

Setting `PCHUsage` to `PCHUsageMode.UseExplicitOrSharedPCHs` creates an explicit PCH file for a module only if it has a `PrivatePCHHeaderFile` setting in the module's `*.build.cs` file. Otherwise, the module will share a PCH with another module, saving the tool from generating more PCH files than necessary. Also, keep in mind that when you enable `UseExplicitOrSharedPCHs` mode, the source file must include its matching header file. Alternatively, if you want a module to opt-out of complying with IWYU conventions, you can set `PCHUsage` to `PCHUsageMode.UseSharedPCHs`.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b9c0f4f-b19b-442a-a06b-82c83771cd1b/exampleplugin_usesharedpchs.png)

### Running in IWYU Mode

If you are running your game in IWYU mode, you will need to ensure that your `.cpp` file or files include their corresponding `.h` file or files first. This is a useful practice, because it enables the compiler to ensure that the `.h` file includes all of its required dependencies (when PCH files and unity builds are disabled). Unreal Build Tool (UBT) will emit a warning if you do not include the matching header file first (for its corresponding `.cpp` file).

If you want to disable the compiler from emitting warnings, you can set `bEnforceIWYU` to `false` in the module's `*.build.cs` file.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e66f2df-48ee-484c-8e86-56adb98d8322/modulebuildcs_benforceiwyufalse.png)

If you want to disable the warning for an entire target, you can set `bEnforceIWYU` to false in the `*.target.cs` file.

## General Tips

If you want your game to opt-in to IWYU, there are a few tips to keep in mind:

1.  Include `CoreMinimal.h` at the top of each header file.
2.  To verify that all of your source files include all of their required dependencies, compile your game project in non-unity mode with PCH files disabled.
3.  If you need to access `UEngine` or `GEngine`, which are defined in `Runtime\Engine\Classes\Engine\Engine.h`, you can `#include Engine/Engine.h` (distinguishing from the monolithic header file, which is located at `Runtime\Engine\Public\Engine.h`).
4.  If you use a class that the compiler doesn't recognize, and don't know what you need to include may be missing the header file. This is especially the case if you are converting from non-IWYU code that compiled correctly. You can look up the class in the API Documentation, and find the necessary modules and header files at the bottom of the page.
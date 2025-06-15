# Module Properties

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/module-properties-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/module-properties-in-unreal-engine)  
**Processed:** 2025-06-14 16:36:47

---

**Modules** are the building blocks of **Unreal Engine (UE)**. The engine is implemented as a large collection of modules, and games supply their own modules to augment them. Each module encapsulates a set of functionality, and can provide a public interface and compile environment (with macros, include paths, and so on) for use by other modules.

Modules are declared through C# source files with a `.build.cs` extension, and are stored under your project's `Source` directory. The C++ source code belonging to a module is stored next to to the `.build.cs` file, or in subdirectories of it. Each `.build.cs` file declares a class deriving from the `ModuleRules` base class, and sets properties controlling how it should be built from its constructor. These `.build.cs` files are compiled by **Unreal Build Tool (UBT)** and constructed to determine the overall compile environment.

The typical structure for a `.build.cs` file is as follows.

C++

`using UnrealBuildTool; 	using System.Collections.Generic; 	public class MyModule : ModuleRules 	{ 		public MyModule(ReadOnlyTargetRules Target) : base(Target) 		{ 			// Properties and settings go here 		} 	}`

using UnrealBuildTool; using System.Collections.Generic; public class MyModule : ModuleRules { public MyModule(ReadOnlyTargetRules Target) : base(Target) { // Properties and settings go here } }

Copy full snippet(9 lines long)

### Read-Only Properties

$ IsPlugin (Boolean): True if a Plugin contains this module

$ Logger (ILogger): Accessor for the target logger

$ HasPackageOverride (Boolean): Returns true if there has been an override type specified on this module

$ ForceIncludeFiles (List<String>): Header files that should be force included for every source file in this module.

$ SDKVersionRelevantPlatforms (List<UnrealTargetPlatform>): If this contains a platform and the project has had it's SDK version overriden from default, this module will be compiled as a project module, instead of shared engine module

$ StaticAnalyzerCheckers (HashSet<String>): The static analyzer checkers that should be enabled rather than the defaults. This is only supported for Clang. See https://clang.llvm.org/docs/analyzer/checkers.html for a full list. Or run: 'clang -Xclang -analyzer-checker-help' or: 'clang -Xclang -analyzer-checker-help-alpha' for the list of experimental checkers.

$ StaticAnalyzerDisabledCheckers (HashSet<String>): The static analyzer default checkers that should be disabled. Unused if StaticAnalyzerCheckers is populated. This is only supported for Clang. See https://clang.llvm.org/docs/analyzer/checkers.html for a full list. Or run: 'clang -Xclang -analyzer-checker-help' or: 'clang -Xclang -analyzer-checker-help-alpha' for the list of experimental checkers.

$ StaticAnalyzerAdditionalCheckers (HashSet<String>): The static analyzer non-default checkers that should be enabled. Unused if StaticAnalyzerCheckers is populated. This is only supported for Clang. See https://clang.llvm.org/docs/analyzer/checkers.html for a full list. Or run: 'clang -Xclang -analyzer-checker-help' or: 'clang -Xclang -analyzer-checker-help-alpha' for the list of experimental checkers.

$ StaticAnalyzerPVSDisabledErrors (HashSet<String>): The PVS Studio analysis errors that should be disabled.

$ AutoSdkDirectory (String): The AutoSDK directory for the active host platform

$ EngineDirectory (String): The current engine directory

$ PluginDirectory (String): Property for the directory containing this plugin. Useful for adding paths to third party dependencies.

$ ModuleDirectory (String): Property for the directory containing this module. Useful for adding paths to third party dependencies.

$ TestsDirectory (String): Returns module's low level tests directory "Tests".

$ IsVcPackageSupported (Boolean): Returns if VcPkg is supported for the build configuration.

### Read/Write Properties

$ StaticAnalyzerRulesets (HashSet<FileReference>): The static analyzer rulesets that should be used to filter warnings. This is only supported for MSVC. See https://learn.microsoft.com/en-us/cpp/code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run

$ AllowedRestrictedFolders (List<String>): List of folders which are allowed to be referenced when compiling this binary, without propagating restricted folder names

$ AliasRestrictedFolders (Dictionary<String, String>): Set of aliased restricted folder references

$ PublicIncludePathModuleNames (List<String>): List of modules names (no path needed) with header files that our module's public headers needs access to, but we don't need to "import" or link against.

$ PublicDependencyModuleNames (List<String>): List of public dependency module names (no path needed) (automatically does the private/public include). These are modules that are required by our public source files.

$ PrivateIncludePathModuleNames (List<String>): List of modules name (no path needed) with header files that our module's private code files needs access to, but we don't need to "import" or link against.

$ PrivateDependencyModuleNames (List<String>): List of private dependency module names. These are modules that our private code depends on but nothing in our public include files depend on.

$ CircularlyReferencedDependentModules (List<String>): Only for legacy reason, should not be used in new code. List of module dependencies that should be treated as circular references. This modules must have already been added to either the public or private dependent module list.

$ PublicSystemIncludePaths (List<String>): List of system/library include paths - typically used for External (third party) modules. These are public stable header file directories that are not checked when resolving header dependencies.

$ PublicIncludePaths (List<String>): (This setting is currently not need as we discover all files from the 'Public' folder) List of all paths to include files that are exposed to other modules

$ InternalIncludePaths (List<String>): (This setting is currently not need as we discover all files from the 'Internal' folder) List of all paths to include files that are exposed to other internal modules

$ PrivateIncludePaths (List<String>): List of all paths to this module's internal include files, not exposed to other modules (at least one include to the 'Private' path, more if we want to avoid relative paths)

$ PublicSystemLibraryPaths (List<String>): List of system library paths (directory of .lib files) - for External (third party) modules please use the PublicAdditionalLibaries instead

$ PrivateRuntimeLibraryPaths (List<String>): List of search paths for libraries at runtime (eg. .so files)

$ PublicRuntimeLibraryPaths (List<String>): List of search paths for libraries at runtime (eg. .so files)

$ PublicAdditionalLibraries (List<String>): List of additional libraries (names of the .lib files including extension) - typically used for External (third party) modules

$ PublicDebugVisualizerPaths (List<String>): List of additional debug visualizers (.natvis and .natstepfilter) exposed to other modules - typically used for External (third party) modules

$ DependenciesToSkipPerArchitecture (Dictionary<String, List<UnrealArch>>): Per-architecture lists of dependencies for linking to ignore (useful when building for multiple architectures, and a lib only is needed for one architecture), it's up to the Toolchain to use this

$ PublicPreBuildLibraries (List<String>): List of additional pre-build libraries (names of the .lib files including extension) - typically used for additional targets which are still built, but using either TargetRules.PreBuildSteps or TargetRules.PreBuildTargets.

$ PublicSystemLibraries (List<String>): List of system libraries to use - these are typically referenced via name and then found via the system paths. If you need to reference a .lib file use the PublicAdditionalLibraries instead

$ PublicFrameworks (List<String>): List of XCode frameworks (iOS and MacOS)

$ PublicWeakFrameworks (List<String>): List of weak frameworks (for OS version transitions)

$ PublicAdditionalFrameworks (List<Framework>): List of addition frameworks - typically used for External (third party) modules on Mac and iOS

$ AdditionalBundleResources (List<BundleResource>): List of addition resources that should be copied to the app bundle for Mac or iOS

$ TypeLibraries (List<TypeLibrary>): List of type libraries that we need to generate headers for (Windows only)

$ PublicDelayLoadDLLs (List<String>): List of delay load DLLs - typically used for External (third party) modules

$ PrivateDefinitions (List<String>): Private compiler definitions for this module

$ PublicDefinitions (List<String>): Public compiler definitions for this module

$ DynamicallyLoadedModuleNames (List<String>): Addition modules this module may require at run-time

$ RuntimeDependencies (RuntimeDependencyList): List of files which this module depends on at runtime. These files will be staged along with the target.

$ AdditionalPropertiesForReceipt (ReceiptPropertyList): List of additional properties to be added to the build receipt

$ ExternalDependencies (List<String>): External files which invalidate the makefile if modified. Relative paths are resolved relative to the .build.cs file.

$ SubclassRules (List<String>): Subclass rules files which invalidate the makefile if modified.

$ GenerateHeaderFuncs (List<ValueTuple<String, Action<ILogger, DirectoryReference>>>): A list of subdirectory names and functions that are invoked to generate header files. The subdirectory name is appended to the generated code directory to form a new directory that headers are generated inside.

$ Name (String): Name of this module

$ Type (ModuleType): Type of module

$ OverridePackageType (PackageOverrideType): Overridden type of module that will set different package flags. Cannot be used for modules that are a part of a plugin because that is set in the \`.uplugin\` file already.

$ BinariesSubFolder (String): Subfolder of Binaries/PLATFORM folder to put this module in when building DLLs. This should only be used by modules that are found via searching like the TargetPlatform or ShaderFormat modules. If FindModules is not used to track them down, the modules will not be found.

$ OptimizeCode (CodeOptimization): When this module's code should be optimized.

$ OptimizationLevel (OptimizationMode): Allows fine tuning optimization level for speed and\\or code size. This requires a private PCH (or NoPCHs, which is not recommended)

$ FPSemantics (FPSemanticsMode): Allows overriding the FP semantics for this module. This requires a private PCH (or NoPCHs, which is not recommended)

$ PrivatePCHHeaderFile (String): Explicit private PCH for this module. Implies that this module will not use a shared PCH.

$ SharedPCHHeaderFile (String): Header file name for a shared PCH provided by this module. Must be a valid relative path to a public C++ header file. This should only be set for header files that are included by a significant number of other C++ modules.

$ ShortName (String): Specifies an alternate name for intermediate directories and files for intermediates of this module. Useful when hitting path length limitations.

$ PCHUsage (PCHUsageMode): Precompiled header usage for this module

$ bTreatAsEngineModule (Boolean): Whether this module should be treated as an engine module (eg. using engine definitions, PCHs, compiled with optimizations enabled in DebugGame configurations, etc...). Initialized to a default based on the rules assembly it was created from.

$ bValidateFormatStrings (Boolean): Emits compilation errors for incorrect UE\_LOG format strings.

$ bValidateInternalApi (Boolean): Emits deprecated warnings\\errors for internal API usage for non-engine modules

$ DefaultBuildSettings (BuildSettingsVersion): Which engine version's build settings to use by default.

$ IncludeOrderVersion (EngineIncludeOrderVersion): What version of include order to use when compiling this module. Can be overridden via -ForceIncludeOrder on the command line or in a module's rules.

$ bUseRTTI (Boolean): Use run time type information

$ bVcRemoveUnreferencedComdat (Boolean): Whether to direct MSVC to remove unreferenced COMDAT functions and data.

$ bCodeCoverage (Boolean): Enable code coverage compilation/linking support.

$ bUseAVX (Boolean): Obsolete: Direct the compiler to generate AVX instructions wherever SSE or AVX intrinsics are used, on the platforms that support it. Note that by enabling this you are changing the minspec for the PC platform, and the resultant executable will crash on machines without AVX support.

$ MinCpuArchX64 (Nullable<MinimumCpuArchitectureX64>): Direct the compiler to generate AVX instructions wherever SSE or AVX intrinsics are used, on the x64 platforms that support it. Note that by enabling this you are changing the minspec for the PC platform, and the resultant executable will crash on machines without AVX support.

$ bEnableBufferSecurityChecks (Boolean): Enable buffer security checks. This should usually be enabled as it prevents severe security risks.

$ bEnableExceptions (Boolean): Enable exception handling

$ bEnableObjCExceptions (Boolean): Enable objective C exception handling

$ bEnableObjCAutomaticReferenceCounting (Boolean): Enable objective C automatic reference counting (ARC) If you set this to true you should not use shared PCHs for this module. The engine won't be extensively using ARC in the short term Not doing this will result in a compile errors because shared PCHs were compiled with different flags than consumer

$ DeterministicWarningLevel (WarningLevel): How to treat deterministic warnings (experimental).

$ ShadowVariableWarningLevel (WarningLevel): How to treat shadow variable warnings

$ bWarningsAsErrors (Boolean): Whether to enable all warnings as errors. UE enables most warnings as errors already, but disables a few (such as deprecation warnings).

$ UnsafeTypeCastWarningLevel (WarningLevel): How to treat unsafe implicit type cast warnings (e.g., double->float or int64->int32)

$ UndefinedIdentifierWarningLevel (WarningLevel): Indicates what warning/error level to treat undefined identifiers in conditional expressions.

$ bEnableUndefinedIdentifierWarnings (Boolean): Enable warnings for using undefined identifiers in #if expressions

$ ModuleIncludePathWarningLevel (WarningLevel): How to treat general module include path validation messages

$ ModuleIncludePrivateWarningLevel (WarningLevel): How to treat private module include path validation messages, where a module is adding an include path that exposes private headers

$ ModuleIncludeSubdirectoryWarningLevel (WarningLevel): How to treat unnecessary module sub-directory include path validation messages

$ bDisableStaticAnalysis (Boolean): Disable all static analysis - clang, msvc, pvs-studio.

$ bStaticAnalyzerExtensions (Boolean): Enable additional analyzer extension warnings using the EspXEngine plugin. This is only supported for MSVC. See https://learn.microsoft.com/en-us/cpp/code-quality/using-the-cpp-core-guidelines-checkers This will add a large number of warnings by default. It's recommended to use StaticAnalyzerRulesets if this is enabled.

$ bUseUnity (Boolean): If unity builds are enabled this can be used to override if this specific module will build using Unity. This is set using the per module configurations in BuildConfiguration.

$ bMergeUnityFiles (Boolean): Whether to merge module and generated unity files for faster compilation.

$ MinSourceFilesForUnityBuildOverride (Int32): The number of source files in this module before unity build will be activated for that module. If set to anything besides -1, will override the default setting which is controlled by MinGameModuleSourceFilesForUnityBuild

$ MinFilesUsingPrecompiledHeaderOverride (Int32): Overrides BuildConfiguration.MinFilesUsingPrecompiledHeader if non-zero.

$ NumIncludedBytesPerUnityCPPOverride (Int32): Overrides Target.NumIncludedBytesPerUnityCPP if non-zero.

$ bBuildLocallyWithSNDBS (Boolean): Module uses a #import so must be built locally when compiling with SN-DBS

$ bEnableNonInlinedGenCppWarnings (Boolean): Enable warnings for when there are .gen.cpp files that could be inlined in a matching handwritten cpp file

$ IsRedistributableOverride (Nullable<Boolean>): Redistribution override flag for this module.

$ bLegalToDistributeObjectCode (Boolean): Whether the output from this module can be publicly distributed, even if it has code/ dependencies on modules that are not (i.e. CarefullyRedist, NotForLicensees, NoRedist). This should be used when you plan to release binaries but not source.

$ bEnforceIWYU (Boolean): Enforce "include what you use" rules when PCHUsage is set to ExplicitOrSharedPCH; warns when monolithic headers (Engine.h, UnrealEd.h, etc...) are used, and checks that source files include their matching header first.

$ IWYUSupport (IWYUSupport): Allows "include what you use" to modify the source code when run. bEnforceIWYU must be true for this variable to matter.

$ bAddDefaultIncludePaths (Boolean): Whether to add all the default include paths to the module (eg. the Source/Classes folder, subfolders under Source/Public).

$ bIgnoreUnresolvedSymbols (Boolean): Whether to ignore dangling (i.e. unresolved external) symbols in modules

$ bPrecompile (Boolean): Whether this module should be precompiled. Defaults to the bPrecompile flag from the target. Clear this flag to prevent a module being precompiled.

$ bUsePrecompiled (Boolean): Whether this module should use precompiled data. Always true for modules created from installed assemblies.

$ bAllowConfidentialPlatformDefines (Boolean): Whether this module can use PLATFORM\_XXXX style defines, where XXXX is a confidential platform name. This is used to ensure engine or other shared code does not reveal confidential information inside an #if PLATFORM\_XXXX block. Licensee game code may want to allow for them, however.

$ bDisableAutoRTFMInstrumentation (Boolean): Disables AutoRTFM instrumentation to this module only when AutoRTFMCompiler is enabled

$ PrecompileForTargets (PrecompileTargetsType): Which targets this module should be precompiled for

$ bRequiresImplementModule (Nullable<Boolean>): Whether this module requires the IMPLEMENT\_MODULE macro to be implemented. Most UE modules require this, since we use the IMPLEMENT\_MODULE macro to do other global overloads (eg. operator new/delete forwarding to GMalloc).

$ bLegacyPublicIncludePaths (Boolean): Whether this module qualifies included headers from other modules relative to the root of their 'Public' folder. This reduces the number of search paths that have to be passed to the compiler, improving performance and reducing the length of the compiler command line.

$ bLegacyParentIncludePaths (Boolean): Whether this module qualifies included headers from other modules relative to the parent directory. This reduces the number of search paths that have to be passed to the compiler, improving performance and reducing the length of the compiler command line.

$ bValidateCircularDependencies (Boolean): Whether circular dependencies will be validated against the allow list Circular module dependencies result in slower builds. Disabling this option is strongly discouraged. This option is ignored for Engine modules which will always be validated against the allow list.

$ CppStandard (Nullable<CppStandardVersion>): Which stanard to use for compiling this module

$ CStandard (Nullable<CStandardVersion>): Which standard to use for compiling this module

$ ModuleSymbolVisibility (SymbolVisibility): Control visibility of symbols
# Build Configuration

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/build-configuration-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/build-configuration-for-unreal-engine)  
**Processed:** 2025-06-14 16:11:13

---

In addition to being added to the generated **Unreal Engine (UE)** project under the `Config/UnrealBuildTool` folder, **Unreal Build Tool (UBT)** reads settings from XML config files in the following locations on Windows:

-   `Engine/Saved/UnrealBuildTool/BuildConfiguration.xml`
    
-   `<USER>/AppData/Roaming/Unreal Engine/UnrealBuildTool/BuildConfiguration.xml`
    
-   `My Documents/Unreal Engine/UnrealBuildTool/BuildConfiguration.xml`
    
-   `<PROJECT_DIRECTORY>/Saved/UnrealBuildTool/BuildConfiguration.xml`
    

On Mac, the following paths are used instead:

-   `/Users/<USER>/.config/Unreal Engine/UnrealBuildTool/BuildConfiguration.xml`
    
-   `/Users/<USER>/Documents/Unreal Engine/UnrealBuildTool/BuildConfiguration.xml`
    
-   `<PROJECT_DIRECTORY>/Saved/UnrealBuildTool/BuildConfiguration.xml`
    

On Linux, the following paths are used instead:

-   `/home/<USER>/.config/Unreal Engine/UnrealBuildTool/BuildConfiguration.xml`
    
-   `/home/<USER>/Documents/Unreal Engine/UnrealBuildTool/BuildConfiguration.xml`
    
-   `<PROJECT_DIRECTORY>/Saved/UnrealBuildTool/BuildConfiguration.xml`
    

Use the `<PROJECT_DIRECTORY>/Saved/UnrealBuildTool/BuildConfiguration.xml` directory for project-specific build configuration where `<PROJECT_DIRECTORY>` is the path to your project's directory.

Keep reading to learn more about the following properties, which help to set and customize build configurations.

### BuildConfiguration

$ bIgnoreOutdatedImportLibraries : Whether to ignore import library files that are out of date when building targets. Set this to true to improve iteration time. By default, we do not bother re-linking targets if only a dependent .lib has changed, as chances are that the import library was not actually different unless a dependent header file of this target was also changed, in which case the target would automatically be rebuilt.

$ bPrintDebugInfo : Whether debug info should be written to the console.

$ bAllowHybridExecutor : Whether the hybrid executor will be used (a remote executor and local executor). No longer supported.

$ RemoteExecutorPriority : Priority order for remote executors (XGE, SNDBS, FASTBuild, UBA)

$ bAllowUBAExecutor : Whether the UnrealBuildAccelerator executor will be used.

$ bAllowUBALocalExecutor : Whether the UnrealBuildAccelerator (local only) executor will be used.

$ bAllowXGE : Whether XGE may be used if available, default is true.

$ bAllowFASTBuild : Whether FASTBuild may be used if available, default is true.

$ bAllowSNDBS : Whether SN-DBS may be used if available, default is true.

$ bUseUBTMakefiles : Enables support for very fast iterative builds by caching target data. Turning this on causes Unreal Build Tool to emit 'UBT Makefiles' for targets when they are built the first time. Subsequent builds will load these Makefiles and begin outdatedness checking and build invocation very quickly. The caveat is that if source files are added or removed to the project, UBT will need to gather information about those in order for your build to complete successfully. Currently, you must run the project file generator after adding/removing source files to tell UBT to re-gather this information.

Events that can invalidate the 'UBT Makefile':

Adding/removing .cpp files

Adding/removing .h files with UObjects

Adding new UObject types to a file that did not previously have any

Changing global build settings (most settings in this file qualify)

Changed code that affects how Unreal Header Tool works

You can force regeneration of the 'UBT Makefile' by passing the '-gather' argument, or simply regenerating project files.

This also enables the fast include file dependency scanning and caching system that allows Unreal Build Tool to detect out of date dependencies very quickly. When enabled, a deep C++ include graph does not have to be generated, and instead, we only scan and cache indirect includes for after a dependent build product was already found to be out of date. During the next build, we will load those cached indirect includes and check for outdatedness.

$ MaxParallelActions : Number of actions that can be executed in parallel. If 0 then code will pick a default based on the number of cores and memory available. Applies to the ParallelExecutor, HybridExecutor, and LocalExecutor

$ bAllCores : Consider logical cores when determining how many total cpu cores are available.

$ bCompactOutput : Instruct the executor to write compact output e.g. only errors, if supported by the executor. This field is used to hold the value when specified from the command line or XML

$ bArtifactRead : If set, artifacts will be read

$ bArtifactWrites : If set, artifacts will be written

$ bLogArtifactCacheMisses : If true, log all artifact cache misses as informational messages

$ ArtifactDirectory : Location to store the artifacts.

$ bUseUnityBuild : Whether to unify C++ code into larger files for faster compilation.

$ bForceUnityBuild : Whether to force C++ source files to be combined into larger files for faster compilation.

$ DefaultWarningLevel : Default treatment of uncategorized warnings

$ DeprecationWarningLevel : Level to report deprecation warnings as errors

$ bShowIncludes : Print out files that are included by each source file

$ bDebugBuildsActuallyUseDebugCRT : Enables the debug C++ runtime (CRT) for debug builds. By default we always use the release runtime, since the debug version isn't particularly useful when debugging Unreal Engine projects, and linking against the debug CRT libraries forces our third party library dependencies to also be compiled using the debug CRT (and often perform more slowly). Often it can be inconvenient to require a separate copy of the debug versions of third party static libraries simply so that you can debug your program's code.

$ bLegalToDistributeBinary : Whether the output from this target can be publicly distributed, even if it has dependencies on modules that are in folders with special restrictions (eg. CarefullyRedist, NotForLicensees, NoRedist).

$ bForceNoAutoRTFMCompiler : Whether to use force AutoRTFM Clang compiler off.

$ bUseAutoRTFMVerifier : Whether to enable emitting AutoRTFM verification metadata

$ bUseInlining : Enable inlining for all modules.

$ bUseDebugLiveCodingConsole : Whether to enable support for live coding

$ bUseXGEController : Whether the XGE controller worker and modules should be included in the engine build. These are required for distributed shader compilation using the XGE interception interface.

$ bUseAdaptiveUnityBuild : Use a heuristic to determine which files are currently being iterated on and exclude them from unity blobs, result in faster incremental compile times. The current implementation uses the read-only flag to distinguish the working set, assuming that files will be made writable by the source control system if they are being modified. This is true for Perforce, but not for Git.

$ bAdaptiveUnityDisablesOptimizations : Disable optimization for files that are in the adaptive non-unity working set.

$ bAdaptiveUnityDisablesPCH : Disables force-included PCHs for files that are in the adaptive non-unity working set.

$ bAdaptiveUnityDisablesProjectPCHForProjectPrivate : Backing storage for bAdaptiveUnityDisablesProjectPCH.

$ bAdaptiveUnityCreatesDedicatedPCH : Creates a dedicated PCH for each source file in the working set, allowing faster iteration on cpp-only changes.

$ bAdaptiveUnityEnablesEditAndContinue : Creates a dedicated PCH for each source file in the working set, allowing faster iteration on cpp-only changes.

$ bAdaptiveUnityCompilesHeaderFiles : Creates a dedicated source file for each header file in the working set to detect missing includes in headers.

$ MinGameModuleSourceFilesForUnityBuild : The number of source files in a game module before unity build will be activated for that module. This allows small game modules to have faster iterative compile times for single files, at the expense of slower full rebuild times. This setting can be overridden by the bFasterWithoutUnity option in a module's Build.cs file.

$ bRequireObjectPtrForAddReferencedObjects : Require TObjectPtr for FReferenceCollector API's. (Needed for compatibility with incremental GC.)

$ bValidateFormatStrings : Emits compilation errors for incorrect UE\_LOG format strings.

$ bWarningsAsErrors : Whether to enable all warnings as errors. UE enables most warnings as errors already, but disables a few (such as deprecation warnings).

$ UnsafeTypeCastWarningLevel : Indicates what warning/error level to treat unsafe type casts as on platforms that support it (e.g., double->float or int64->int32)

$ bUndefinedIdentifierErrors : Forces the use of undefined identifiers in conditional expressions to be treated as errors.

$ UndefinedIdentifierWarningLevel : Indicates what warning/error level to treat undefined identifiers in conditional expressions.

$ PCHPerformanceIssueWarningLevel : Indicates what warning/error level to treat potential PCH performance issues.

$ ModuleIncludePathWarningLevel : How to treat general module include path validation messages

$ ModuleIncludePrivateWarningLevel : How to treat private module include path validation messages, where a module is adding an include path that exposes private headers

$ ModuleIncludeSubdirectoryWarningLevel : How to treat unnecessary module sub-directory include path validation messages

$ bRetainFramePointers : Forces frame pointers to be retained this is usually required when you want reliable callstacks e.g. mallocframeprofiler

$ bUseFastMonoCalls : New Monolithic Graphics drivers have optional "fast calls" replacing various D3d functions

$ NumIncludedBytesPerUnityCPP : An approximate number of bytes of C++ code to target for inclusion in a single unified C++ file.

$ bDisableModuleNumIncludedBytesPerUnityCPPOverride : Disables overrides that are set by the module

$ bStressTestUnity : Whether to stress test the C++ unity build robustness by including all C++ files files in a project from a single unified file.

$ bDetailedUnityFiles : Whether to add additional information to the unity files, such as '\_of\_X' in the file name. Not recommended.

$ bDisableDebugInfo : Whether to globally disable debug info generation; Obsolete, please use TargetRules.DebugInfoMode instead

$ DebugInfo : How much debug info should be generated. See DebugInfoMode enum for more details

$ DebugInfoLineTablesOnly : True if only debug line number tables should be emitted in debug information for compilers that support doing so. Overrides TargetRules.DebugInfo See https://clang.llvm.org/docs/UsersManual.html#cmdoption-gline-tables-only for more information

$ bDisableDebugInfoForGeneratedCode : Whether to disable debug info generation for generated files. This improves link times and reduces pdb size for modules that have a lot of generated glue code.

$ bOmitPCDebugInfoInDevelopment : Whether to disable debug info on PC/Mac in development builds (for faster developer iteration, as link times are extremely fast with debug info disabled).

$ bUsePDBFiles : Whether PDB files should be used for Visual C++ builds.

$ bUsePCHFiles : Whether PCH files should be used.

$ bDeterministic : Set flags require for deterministic compiling and linking. Enabling deterministic mode for msvc disables codegen multithreading so compiling will be slower

$ bChainPCHs : Whether PCHs should be chained when compiling with clang.

$ bForceIncludePCHHeadersForGenCppFilesWhenPCHIsDisabled : Whether PCH headers should be force included for gen.cpp files when PCH is disabled.

$ bPreprocessDepends : Generate dependency files by preprocessing. This is only recommended when distributing builds as it adds additional overhead.

$ StaticAnalyzer : Whether static code analysis should be enabled.

$ StaticAnalyzerOutputType : The output type to use for the static analyzer. This is only supported for Clang.

$ StaticAnalyzerMode : The mode to use for the static analyzer. This is only supported for Clang. Shallow mode completes quicker but is generally not recommended.

$ StaticAnalyzerPVSPrintLevel : The level of warnings to print when analyzing using PVS-Studio

$ bStaticAnalyzerProjectOnly : Only run static analysis against project modules, skipping engine modules

$ bStaticAnalyzerIncludeGenerated : When enabled, generated source files will be analyzed

$ MinFilesUsingPrecompiledHeader : The minimum number of files that must use a pre-compiled header before it will be created and used.

$ bForcePrecompiledHeaderForGameModules : When enabled, a precompiled header is always generated for game modules, even if there are only a few source files in the module. This greatly improves compile times for iterative changes on a few files in the project, at the expense of slower full rebuild times for small game projects. This can be overridden by setting MinFilesUsingPrecompiledHeaderOverride in a module's Build.cs file.

$ bUseIncrementalLinking : Whether to use incremental linking or not. Incremental linking can yield faster iteration times when making small changes. Currently disabled by default because it tends to behave a bit buggy on some computers (PDB-related compile errors).

$ bAllowLTCG : Whether to allow the use of link time code generation (LTCG).

$ bPreferThinLTO : When Link Time Code Generation (LTCG) is enabled, whether to prefer using the lighter weight version on supported platforms.

$ ThinLTOCacheDirectory : Directory where to put the ThinLTO cache on supported platforms.

$ ThinLTOCachePruningArguments : Arguments that will be applied to prune the ThinLTO cache on supported platforms. Arguments will only be applied if ThinLTOCacheDirectory is set.

$ bPGOProfile : Whether to enable Profile Guided Optimization (PGO) instrumentation in this build.

$ bPGOOptimize : Whether to optimize this build with Profile Guided Optimization (PGO).

$ bCodeCoverage : Whether the target requires code coverage compilation and linking.

$ bSupportEditAndContinue : Whether to support edit and continue.

$ bOmitFramePointers : Whether to omit frame pointers or not. Disabling is useful for e.g. memory profiling on the PC.

$ bShaderCompilerWorkerTrace : If true, then enable Unreal Insights (utrace) profiling in the build for the Shader Compiler Worker (defines USE\_SHADER\_COMPILER\_WORKER\_TRACE=1).

$ bUseSharedPCHs : Enables "Shared PCHs", a feature which significantly speeds up compile times by attempting to share certain PCH files between modules that UBT detects is including those PCH's header files.

$ bUseShippingPhysXLibraries : True if Development and Release builds should use the release configuration of PhysX/APEX.

$ bUseCheckedPhysXLibraries : True if Development and Release builds should use the checked configuration of PhysX/APEX. if bUseShippingPhysXLibraries is true this is ignored.

$ bCheckLicenseViolations : Tells the UBT to check if module currently being built is violating EULA.

$ bBreakBuildOnLicenseViolation : Tells the UBT to break build if module currently being built is violating EULA.

$ bUseFastPDBLinking : Whether to use the :FASTLINK option when building with /DEBUG to create local PDBs on Windows. Fast, but currently seems to have problems finding symbols in the debugger.

$ bCreateMapFile : Outputs a map file as part of the build.

$ bAllowRuntimeSymbolFiles : True if runtime symbols files should be generated as a post build step for some platforms. These files are used by the engine to resolve symbol names of callstack backtraces in logs.

$ PackagePath : Package full path (directory + filename) where to store input files used at link time Normally used to debug a linker crash for platforms that support it

$ CrashDiagnosticDirectory : Directory where to put crash report files for platforms that support it

$ bCheckSystemHeadersForModification : Whether headers in system paths should be checked for modification when determining outdated actions.

$ bFlushBuildDirOnRemoteMac : Whether to clean Builds directory on a remote Mac before building.

$ bPrintToolChainTimingInfo : Whether to write detailed timing info from the compiler and linker.

$ bParseTimingInfoForTracing : Whether to parse timing data into a tracing file compatible with chrome://tracing.

$ bPublicSymbolsByDefault : Whether to expose all symbols as public by default on POSIX platforms

$ MSVCCompileActionWeight : The weight(cpu/memory utilization) of a MSVC compile action

$ ClangCompileActionWeight : The weight(cpu/memory utilization) of a clang compile action

$ CppStandardEngine : Which C++ standard to use for compiling this target (for engine modules)

$ CppStandard : Which C++ standard to use for compiling this target (for non-engine modules)

$ CStandard : Which C standard to use for compiling this target

$ MinCpuArchX64 : Direct the compiler to generate AVX instructions wherever SSE or AVX intrinsics are used, on the x64 platforms that support it. Ignored for arm64. Note that by enabling this you are changing the minspec for the target platform, and the resultant executable will crash on machines without AVX support.

$ ActionStallReportTime : Number of second of no completed actions to trigger an action stall report. If zero, stall reports will not be enabled.

$ ActionStallTerminateTime : Number of second of no completed actions to trigger to terminate the queue. If zero, force termination not be enabled.

$ bStopSNDBSCompilationAfterErrors : When enabled, SN-DBS will stop compiling targets after a compile error occurs. Recommended, as it saves computing resources for others.

$ bXGENoWatchdogThread : Whether to use the no\_watchdog\_thread option to prevent VS2015 toolchain stalls.

$ bShowXGEMonitor : Whether to display the XGE build monitor.

$ bStopXGECompilationAfterErrors : When enabled, XGE will stop compiling targets after a compile error occurs. Recommended, as it saves computing resources for others.

$ BaseLogFileName : Specifies the file to use for logging.

$ IWYUBaseLogFileName : Specifies the file to use for logging.

$ bStripSymbols : Whether to strip iOS symbols or not (implied by Shipping config).

$ bUseDSYMFiles : Enables the generation of .dsym files. This can be disabled to enable faster iteration times during development.

$ bSkipClangValidation : Disables clang build verification checks on static libraries

$ bEnableAddressSanitizer : Enables address sanitizer (ASan). Only supported for Visual Studio 2019 16.7.0 and up.

$ bEnableLibFuzzer : Enables LibFuzzer. Only supported for Visual Studio 2022 17.0.0 and up.

$ bEnableThreadSanitizer : Enables thread sanitizer (TSan).

$ bEnableUndefinedBehaviorSanitizer : Enables undefined behavior sanitizer (UBSan).

$ bEnableMemorySanitizer : Enables memory sanitizer (MSan)

$ bTuneDebugInfoForLLDB : Turns on tuning of debug info for LLDB

$ bDisableDumpSyms : Whether to globally disable calling dump\_syms

$ bWriteSolutionOptionFile : Whether to write a solution option (suo) file for the sln.

$ bVsConfigFile : Whether to write a .vsconfig file next to the sln to suggest components to install.

$ bAddFastPDBToProjects : Whether to add the -FastPDB option to build command lines by default.

$ bUsePerFileIntellisense : Whether to generate per-file intellisense data.

$ bEditorDependsOnShaderCompileWorker : Whether to include a dependency on ShaderCompileWorker when generating project files for the editor.

$ TempDirectory : If set TMP\\TEMP will be overidden to this directory, each process will create a unique subdirectory in this folder.

$ bDeleteTempDirectory : If set the application temp directory will be deleted on exit, only when running with a single instance mutex.

### UEBuildConfiguration

$ bForceHeaderGeneration : If true, force header regeneration. Intended for the build machine.

$ bDoNotBuildUHT : If true, do not build UHT, assume it is already built.

$ bFailIfGeneratedCodeChanges : If true, fail if any of the generated header files is out of date.

$ bAllowHotReloadFromIDE : True if hot-reload from IDE is allowed.

$ bForceDebugUnrealHeaderTool : If true, the Debug version of UnrealHeaderTool will be built and run instead of the Development version.

$ bUseBuiltInUnrealHeaderTool : If true, use C# UHT internal to UBT

$ bWarnOnCppUnrealHeaderTool : If true, generate warnings when C++ UHT is used

### WindowsPlatform

$ MaxRootPathLength : Maximum recommended root path length.

$ MaxNestedPathLength : Maximum length of a path relative to the root directory. Used on Windows to ensure paths are portable between machines.

$ bIgnoreStalePGOData : If -PGOOptimize is specified but the linker flags have changed since the last -PGOProfile, this will emit a warning and build without PGO instead of failing during link with LNK1268.

$ bUseFastGenProfile : If specified along with -PGOProfile, then /FASTGENPROFILE will be used instead of /GENPROFILE. This usually means that the PGO data is generated faster, but the resulting data may not yield as efficient optimizations during -PGOOptimize

$ PreMergedPgdFilename : If specified along with -PGOOptimize, will use the specified per-merged pgd file instead of the usual pgd file with loose pgc files.

$ bPGONoExtraCounters : If specified along with -PGOProfile, prevent the usage of extra counters. Please note that by default /FASTGENPROFILE doesnt use extra counters

$ bSampleBasedPGO : If specified along with -PGOProfile, use sample-based PGO instead of instrumented. Currently Intel oneAPI 2024.0+ only.

$ Compiler : Version of the compiler toolchain to use on Windows platform. A value of "default" will be changed to a specific version at UBT start up.

$ CompilerVersion : The specific compiler version to use. This may be a specific version number (for example, "14.13.26128"), the string "Latest" to select the newest available version, or the string "Preview" to select the newest available preview version. By default, and if it is available, we use the toolchain version indicated by WindowsPlatform.DefaultToolChainVersion (otherwise, we use the latest version).

$ ToolchainVersion : The specific msvc toolchain version to use if the compiler is not msvc. This may be a specific version number (for example, "14.13.26128"), the string "Latest" to select the newest available version, or the string "Preview" to select the newest available preview version. By default, and if it is available, we use the toolchain version indicated by WindowsPlatform.DefaultToolChainVersion (otherwise, we use the latest version).

$ bVCFastFail : True if /fastfail should be passed to the msvc compiler and linker

$ bVCExtendedWarningInfo : True if /d2ExtendedWarningInfo should be passed to the compiler and /d2:-ExtendedWarningInfo to the linker

$ bClangStandaloneDebug : True if optimizations to reduce the size of debug information should be disabled See https://clang.llvm.org/docs/UsersManual.html#cmdoption-fstandalone-debug for more information

$ bAllowClangLinker : True if we should use the Clang linker (LLD) when we are compiling with Clang or Intel oneAPI, otherwise we use the MSVC linker.

$ WindowsSdkVersion : The specific Windows SDK version to use. This may be a specific version number (for example, "8.1", "10.0" or "10.0.10150.0"), or the string "Latest", to select the newest available version. By default, and if it is available, we use the Windows SDK version indicated by WindowsPlatform.DefaultWindowsSdkVersion (otherwise, we use the latest version).

$ bWriteSarif : Whether .sarif files containing errors and warnings are written alongside each .obj, if supported

$ bUpdatedCPPMacro : Enables updated \_\_cplusplus macro (/Zc:\_\_cplusplus).

$ bStrictInlineConformance : Enables inline conformance (Remove unreferenced COMDAT) (/Zc:inline).

$ bStrictPreprocessorConformance : Enables new preprocessor conformance (/Zc:preprocessor). This is always enabled for C++20 modules.

$ bStrictEnumTypesConformance : Enables enum types conformance (/Zc:enumTypes) in VS2022 17.4 Preview 4.0+.

$ bStrictODRViolationConformance : Enables enforcing standard C++ ODR violations (/Zc:checkGwOdr) in VS2022 17.5 Preview 2.0+

$ bStripPrivateSymbols : Whether to request the linker create a stripped pdb file as part of the build. If enabled the full debug pdb will have the extension .full.pdb

$ bNoLinkerDebugInfo : If you supply -NoDebugInfo, windows platforms still create debug info while linking. Set this to true to not create debug info while linking in this circumstance

$ PCHMemoryAllocationFactor : Determines the amount of memory that the compiler allocates to construct precompiled headers (/Zm).

$ AdditionalLinkerOptions : Allow the target to specify extra options for linking that aren't otherwise noted here

$ bReducedOptimizeHugeFunctions : Whether to reduce optimizations for huge functions over an instruction threshold to improve compile time https://devblogs.microsoft.com/cppblog/msvc-backend-updates-in-visual-studio-2019-versions-16-3-and-16-4/

$ ReducedOptimizeHugeFunctionsThreshold : The instruction threshold to use when reducing optimizations for huge functions, default 20000.

$ bClangTimeTrace : (Experimental) Appends the -ftime-trace argument to the command line for Clang to output a JSON file containing a timeline for the compile. See http://aras-p.info/blog/2019/01/16/time-trace-timeline-flame-chart-profiler-for-Clang/ for more info.

$ bCompilerTrace : Outputs compile timing information so that it can be analyzed.

$ bSetResourceVersions : If enabled will set the ProductVersion embeded in windows executables and dlls to contain BUILT\_FROM\_CHANGELIST and BuildVersion Enabled by default for all precompiled and Shipping configurations. Regardless of this setting, the versions from Build.version will be available via the BuildSettings module Note: Embedding these versions will cause resource files to be recompiled whenever changelist is updated which will cause binaries to relink

$ InlineFunctionExpansionLevel : Which level to use for Inline Function Expansion when TargetRules.bUseInlining is enabled

$ ToolChain : Version of the toolchain to use on Windows platform when a non-msvc Compiler is in use, to locate include paths etc.

$ ToolchainVersionWarningLevel : Warning level when reporting toolchains that are not in the preferred version list

$ bStrictConformanceMode : Enables strict standard conformance mode (/permissive-).

$ bDisableVolatileMetadata : Volatile Metadata is enabled by default and improves x64 emulation on arm64, but may come at a small perfomance cost (/volatileMetadata-).

### TargetRules

$ bCompileChaosVisualDebuggerSupport : Whether to compile in Chaos Visual Debugger (CVD) support features to record the state of the physics simulation

### ModuleConfiguration

$ DisableMergingModuleAndGeneratedFilesInUnityFiles : List of modules that disables merging module and generated cpp files in the same unity files.

$ DisableUnityBuild : List of modules to disable unity builds for

$ EnableOptimizeCode : List of modules to enable optimizations for

$ DisableOptimizeCode : List of modules to disable optimizations for

$ OptimizeForSize : List of modules to optimize for size. This allows the target to override module optimization level Note that this may disable PCH usage if a private PCH is not provided

$ OptimizeForSizeAndSpeed : List of modules to optimize for size and speed. This allows the target to override module optimization level Note that this may disable PCH usage if a private PCH is not provided

### UnrealBuildAccelerator

$ bStoreObjFilesCompressed : Store object (.obj) compressed on disk. Requires uba to do link step where it will decompress obj files again

$ bDisableRemote : When set to true, UBA will not use any remote help

$ bForceBuildAllRemote : When set to true, UBA will force all actions that can be built remotely to be built remotely. This will hang if there are no remote agents available

$ bForcedRetry : When set to true, actions that fail locally with UBA will be retried without UBA.

$ bForcedRetryRemote : When set to true, actions that fail remotely with UBA will be retried locally with UBA.

$ bStrict : When set to true, all errors and warnings from UBA will be output at the appropriate severity level to the log (rather than being output as 'information' and attempting to continue regardless).

$ bStoreRaw : If UBA should store cas compressed or raw

$ bLinkRemote : If UBA should distribute linking to remote workers. This needs bandwidth but can be an optimization

$ StoreCapacityGb : The amount of gigabytes UBA is allowed to use to store workset and cached data. It is a good idea to have this >10gb

$ MaxWorkers : Max number of worker threads that can handle messages from remotes.

$ SendSize : Max size of each message sent from server to client

$ Host : Which ip UBA server should listen to for connections

$ Port : Which port UBA server should listen to for connections.

$ RootDir : Which directory to store files for UBA.

$ bUseQuic : Use Quic protocol instead of Tcp (experimental)

$ bLogEnabled : Enable logging of UBA processes

$ bPrintSummary : Prints summary of UBA stats at end of build

$ bLaunchVisualizer : Launch visualizer application which shows build progress

$ bResetCas : Resets the cas cache

$ TraceFile : Provide custom path for trace output file

$ bDetailedTrace : Add verbose details to the UBA trace

$ bDisableWaitOnMem : Disable UBA waiting on available memory before spawning new processes

$ bAllowKillOnMem : Let UBA kill running processes when close to out of memory

$ OutputStatsThresholdMs : Threshold for when executor should output logging for the process. Defaults to never

$ bWriteToDisk : Skip writing intermediate and output files to disk. Useful for validation builds where we don't need the output

$ bDisableCustomAlloc : Set to true to disable mimalloc and detouring of memory allocations.

$ Zone : The zone to use for UBA.

$ bUseCrypto : Set to true to enable encryption when transferring files over the network.

$ bUseKnownInputs : Set to true to provide known inputs to processes that are run remote. This is an experimental feature to speed up build times when ping is higher

$ ActionsOutputFile : Write yaml file with all actions that are queued for build. This can be used to replay using "UbaCli.exe local file.yaml"

$ bDetailedLog : Set to true to see more info about what is happening inside uba and also log output from agents

$ Cache : Address of the uba cache service. Will automatically use cache if connected

$ WriteCache : Set cache to write instead of fetch

$ CacheMaxWorkers : Max number of cache download tasks that can execute in parallel

$ ReportCacheMissReason : Report reason a cache miss happened. Useful when searching for determinism/portability issues

$ bDisableHorde : Disable horde all together

### TestTargetRules

$ bCompileChaosVisualDebuggerSupport : Whether to compile in Chaos Visual Debugger (CVD) support features to record the state of the physics simulation

### FASTBuild

$ FBuildExecutablePath : Used to specify the location of fbuild.exe if the distributed binary isn't being used

$ bEnableDistribution : Controls network build distribution

$ FBuildBrokeragePath : Used to specify the location of the brokerage. If null, FASTBuild will fall back to checking FASTBUILD\_BROKERAGE\_PATH

$ FBuildCoordinator : Used to specify the FASTBuild coordinator IP or network name. If null, FASTBuild will fall back to checking FASTBUILD\_COORDINATOR

$ bEnableCaching : Controls whether to use caching at all. CachePath and FASTCacheMode are only relevant if this is enabled.

$ CacheMode : Cache access mode - only relevant if bEnableCaching is true;

$ FBuildCachePath : Used to specify the location of the cache. If null, FASTBuild will fall back to checking FASTBUILD\_CACHE\_PATH

$ bForceRemote : Whether to force remote

$ bStopOnError : Whether to stop on error

$ MsvcCRTRedistVersion : Which MSVC CRT Redist version to use

$ CompilerVersion : Which MSVC Compiler version to use

### ParallelExecutor

$ MaxProcessorCount : Maximum processor count for local execution.

$ ProcessorCountMultiplier : Processor count multiplier for local execution. Can be below 1 to reserve CPU for other tasks. When using the local executor (not XGE), run a single action on each CPU core. Note that you can set this to a larger value to get slightly faster build times in many cases, but your computer's responsiveness during compiling may be much worse. This value is ignored if the CPU does not support hyper-threading.

$ MemoryPerActionBytes : Free memory per action in bytes, used to limit the number of parallel actions if the machine is memory starved. Set to 0 to disable free memory checking.

$ ProcessPriority : The priority to set for spawned processes. Valid Settings: Idle, BelowNormal, Normal, AboveNormal, High Default: BelowNormal or Normal for an Asymmetrical processor as BelowNormal can cause scheduling issues.

$ bStopCompilationAfterErrors : When enabled, will stop compiling targets after a compile error occurs.

$ bShowCompilationTimes : Whether to show compilation times along with worst offenders or not.

$ bShowPerActionCompilationTimes : Whether to show compilation times for each executed action

$ bLogActionCommandLines : Whether to log command lines for actions being executed

$ bPrintActionTargetNames : Add target names for each action executed

$ bUseActionWeights : Whether to take into account the Action's weight when determining to do more work or not.

$ bShowCPUUtilization : Whether to show CPU utilization after the work is complete.

### SNDBS

$ bAllowOverVpn : When set to false, SNDBS will not be enabled when running connected to the coordinator over VPN. Configure VPN-assigned subnets via the VpnSubnets parameter.

$ VpnSubnets : List of subnets containing IP addresses assigned by VPN

\### Horde

$ Server : Uri of the Horde server

$ Token : Auth token for the Horde server

$ OidcProvider : OIDC id for the login to use

$ Pool : Pool for the Horde agent to assign if no override current platform doesn't have it set

$ LinuxPool : Pool for the Horde agent to assign when on Linux

$ MacPool : Pool for the Horde agent to assign when on Mac

$ WindowsPool : Pool for the Horde agent to assign when on Windows

$ Requirements : Requirements for the Horde agent to assign

$ Cluster : Compute cluster ID to use in Horde. Set to "\_auto" to let Horde server resolve a suitable cluster. In multi-region setups this is can simplify configuration of UBT/UBA a lot.

$ LocalHost : Which ip UBA server should give to agents. This will invert so host listens and agents connect

$ MaxCores : Max cores allowed to be used by build session

$ StartupDelay : How long UBT should wait to ask for help. Useful in build configs where machine can delay remote work and still get same wall time results (pch dependencies etc)

$ AllowWine : Allow use of Wine. Only applicable to Horde agents running Linux. Can still be ignored if Wine executable is not set on agent.

$ ConnectionMode : Connection mode for agent/compute communication for valid modes.

$ Encryption : Encryption to use for agent/compute communication. Note that UBA agent uses its own encryption. for valid modes.

$ UBASentryUrl : Sentry URL to send box data to. Optional.

### XGE

$ bAllowOverVpn : When set to false, XGE will not be enabled when running connected to the coordinator over VPN. Configure VPN-assigned subnets via the VpnSubnets parameter.

$ VpnSubnets : List of subnets containing IP addresses assigned by VPN

$ bAllowRemoteLinking : Whether to allow remote linking

$ bUseVCCompilerMode : Whether to enable the VCCompiler=true setting. This requires an additional license for VC tools.

$ MinActions : Minimum number of actions to use XGE execution.

$ bUnavailableIfInUse : Check for a concurrent XGE build and treat the XGE executor as unavailable if it's in use. This will allow UBT to fall back to another executor such as the parallel executor.

### BuildMode

$ bIgnoreJunk : Whether to skip checking for files identified by the junk manifest.

### ProjectFileGenerator

$ DisablePlatformProjectGenerators : Disable native project file generators for platforms. Platforms with native project file generators typically require IDE extensions to be installed.

$ Format : Default list of project file formats to generate.

$ bGenerateIntelliSenseData : True if intellisense data should be generated (takes a while longer).

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bAllDocumentationLanguages : True if all documentation languages should be included in generated projects, otherwise only INT files will be included.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeBuildSystemFiles : True if build system files should be included.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeLocalizationFiles : True if we should include localization files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ bKeepSourceSubDirectories : True if we should reflect "Source" sub-directories on disk in the primary project as project directories. This (arguably) adds some visual clutter to the primary project but it is truer to the on-disk file organization.

$ Platforms : Names of platforms to include in the generated project files

$ Configurations : Names of configurations to include in the generated project files. See UnrealTargetConfiguration for valid entries

$ bGatherThirdPartySource : If true, we'll parse subdirectories of third-party projects to locate source and header files to include in the generated projects. This can make the generated projects quite a bit bigger, but makes it easier to open files directly from the IDE.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

$ bIncludeTestAndShippingConfigs : Whether we should include configurations for "Test" and "Shipping" in generated projects. Pass "-NoShippingConfigs" to disable this.

$ bIncludeDebugConfigs : Whether we should include configurations for "Debug" and "DebugGame" in generated projects. Pass "-NoDebugConfigs" to disable this.

$ bIncludeDevelopmentConfigs : Whether we should include configurations for "Development" in generated projects. Pass "-NoDevelopmentConfigs" to disable this.

$ bVisualStudioLinux : True if visual studio project should be generated in linux mode.

### IOSToolChain

$ bUseDangerouslyFastMode : If this is set, then we do not do any post-compile steps -- except moving the executable into the proper spot on Mac.

### WindowsTargetRules

$ ObjSrcMapFile : Whether we should export a file containing .obj to source file mappings.

### CLionGenerator

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### CMakefileGenerator

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### CodeLiteGenerator

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### #EddieProjectFileGenerator

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### KDevelopGenerator

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### MakefileGenerator

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### QMakefileGenerator

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### RiderProjectFileGenerator

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### VSCodeProjectFileGenerator

$ IncludeAllFiles : Includes all files in the generated workspace.

$ AddDebugAttachConfig : Whether VS Code project generation should include debug configurations to allow attaching to already running processes

$ AddDebugCoreConfig : Whether VS Code project generation should include debug configurations to allow core dump debugging

$ NoCompileCommands : Do not create compile commands json files with compiler arguments for each file; works better with VS Code extension using UBT server mode.

$ UseVSCodeExtension : Create a workspace file for use with VS Code extension that communicates directly with UBT.

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### VCMacProjectFileGenerator

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### VSWorkspaceProjectFileGenerator

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### VCProjectFileGenerator

$ Version : The version of Visual Studio to generate project files for.

$ MaxSharedIncludePaths : Puts the most common include paths in the IncludePath property in the MSBuild project. This significantly reduces Visual Studio memory usage (measured 1.1GB -> 500mb), but seems to be causing issues with Visual Assist. Value here specifies maximum length of the include path list in KB.

$ ExcludedIncludePaths : Semi-colon separated list of paths that should not be added to the projects include paths. Useful for omitting third-party headers (e.g ThirdParty/WebRTC) from intellisense suggestions and reducing memory footprints.

$ ExcludedFilePaths : Semi-colon separated list of paths that should not be added to the projects. Useful for omitting third-party files (e.g ThirdParty/WebRTC) from intellisense suggestions and reducing memory footprints.

$ bBuildUBTInDebug : Forces UBT to be built in debug configuration, regardless of the solution configuration

$ bBuildLiveCodingConsole : Whether to include a dependency on LiveCodingConsole when building targets that support live coding.

$ bMakeProjectPerTarget : Whether to generate a project file for each individual target, and not include e.g. Editor/Client/Server in the Configuration.

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### XcodeProjectFileGenerator

$ bIncludeDocumentation : True if we should include documentation in the generated projects.

$ bUsePrecompiled : True if build targets should pass the -useprecompiled argument.

$ bIncludeEngineSource : True if we should include engine source in the generated solution.

$ bIncludeShaderSource : True if shader source files should be included in generated projects.

$ bIncludeConfigFiles : True if we should include config (.ini) files in the generated project.

$ bIncludeTemplateFiles : True if we should include template files in the generated project.

$ bIncludeEnginePrograms : True if we should include program projects in the generated solution.

$ IncludeCppSource : Whether to include C++ targets

$ bIncludeDotNetPrograms : True if we should include csharp program projects in the generated solution. Pass "-DotNet" to enable this.

$ bIncludeTempTargets : Whether to include temporary targets generated by UAT to support content only projects with non-default settings.

$ PrimaryProjectName : Name of the primary project file -- for example, the base file name for the Visual Studio solution file, or the Xcode project file on Mac.

$ bPrimaryProjectNameFromFolder : If true, sets the primary project name according to the name of the folder it is in.

### SourceFileWorkingSet

$ Provider : Sets the provider to use for determining the working set.

$ RepositoryPath : Sets the path to use for the repository. Interpreted relative to the Unreal Engine root directory (the folder above the Engine folder) -- if relative.

$ GitPath : Sets the path to use for the Git executable. Defaults to "git" (assuming it is in the PATH).

### RemoteMac

$ ServerName : These two variables will be loaded from the XML config file in XmlConfigLoader.Init().

$ UserName : The remote username.

$ SshPrivateKey : If set, instead of looking for RemoteToolChainPrivate.key in the usual places (Documents/Unreal, Engine/UnrealBuildTool/SSHKeys or Engine/Build/SSHKeys), this private key will be used.

$ RsyncAuthentication : The authentication used for Rsync (for the -e rsync flag).

$ SshAuthentication : The authentication used for SSH (probably similar to RsyncAuthentication).

### Log

$ bBackupLogFiles : Whether to backup an existing log file, rather than overwriting it.

$ LogFileBackupCount : The number of log file backups to preserve. Older backups will be deleted.

### Telemetry

$ Providers : Providers to load opt-in telemetry connection information from ini. If unset, or the provider categories do not contain connection info, no telemetry will be sent.
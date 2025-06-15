# Console Commands Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-console-commands-reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-console-commands-reference)  
**Processed:** 2025-06-14 16:56:29

---

| **Command** | **Description** |
| --- | --- |
| `a.AuditLoadedAnimGraphs` | Audit memory breakdown of currently loaded anim graphs. Writes results to the log. |
| `a.Sharing.Enabled` | Arguments: 0/1 Controls whether the animation sharing is enabled. |
| `a.Sharing.ToggleVisibility` | Toggles the visibility of the Leader Pose Components. |
| `abtest` | Provide two console commands or 'stop' to stop the abtest. Frames are timed with the two options, logging results over time. |
| `Accessibility.DumpStatsSlate` | Writes memory stats for Slate's accessibility data stored to LogAccessibility. |
| `Accessibility.DumpStatsWindows` | Writes to LogAccessibility the memory stats for the platform-level accessibility data (Providers) required for Windows support. |
| `ACL.ListAnimSequences` | Dumps statistics about animation sequences to the log. |
| `ACL.ListCodecs` | Dumps statistics about animation codecs to the log. |
| `ACL.SetDatabaseVisualFidelity` | Sets the visual fidelity of all ACL databases. Argument: Highest (default if no argument is provided), Medium, Lowest |
| `AddWork` |   |
| `ai.debug.nav.DirtyAreaAroundPlayer` | Dirty all tiles in a square area around the local player using provided value as extent (in cm), using 10 meters if not specified. |
| `ai.debug.nav.DrawDistance` | Sets the culling distance used by the navmesh rendering for lines and labels. |
| `AnimRecorder.SampleRate` | Argument: valid Frame Rate format. Sets the sample frame-rate for the animation recorder system |
| `AssetManager.AssetAudit` | Dumps statistics about assets to the log. |
| `AssetManager.DumpAssetDependencies` | Shows a list of all primary assets and the secondary assets that they depend on. Also writes out a .graphviz file |
| `AssetManager.DumpAssetRegistry` | Prints entries in the asset registry. Arguments are required: ObjectPath, PackageName, Path, Class, Tag, Dependencies, PackageData. |
| `AssetManager.DumpAssetRegistryInfo` | Dumps extended info about asset registry to log |
| `AssetManager.DumpBundlesForAsset` | Shows a list of all bundles for the specified primary asset by primary asset id (i.e. Map:Entry) |
| `AssetManager.DumpLoadedAssets` | Shows a list of all loaded primary assets and bundles |
| `AssetManager.DumpReferencersForPackage` | Generates a graph viz and log file of all references to a specified package |
| `AssetManager.DumpTypeSummary` | Shows a summary of types known about by the asset manager |
| `AssetManager.FindDepChain` | Finds all dependency chains from assets in the given search path, to the target package. Usage: `FindDepChain TargetPackagePath SearchRootPath (optional: -hardonly/-softonly)`. For example: `FindDepChain /game/characters/heroes/muriel/meshes/muriel /game/cards` |
| `AssetManager.FindDepClasses` | Finds all dependencies of a certain set of classes to the target asset. Usage: `FindDepClasses TargetPackagePath ClassName1 ClassName2 etc (optional: -hardonly/-softonly)`. For example: `FindDepChain /game/characters/heroes/muriel/meshes/muriel /game/cards` |
| `AssetManager.LoadPrimaryAssetsWithType` | Loads all assets of a given type |
| `AssetManager.UnloadPrimaryAssetsWithType` | Unloads all assets of a given type |
| `AssetRegistry.Debug.FindInvalidUAssets` | Finds a list of all assets which are in UAsset files but do not share the name of the package |
| `AssetRegistry.DumpAllocatedSize` | Dump the allocations of the asset registry state to the log |
| `AssetRegistry.DumpState` | Dump the state of the asset registry to a file. Pass `-log` to dump to the log as well. Extra string parameters: All, ObjectPath, PackageName, Path, Class, Tag, Dependencies, DependencyDetails, PackageData, AssetBundles, AssetTags |
| `AssetRegistry.GetByClass` | `<ClassName>` Query the asset registry for assets matching the supplied class |
| `AssetRegistry.GetByName` | `<PackageName>` Query the asset registry for assets matching the supplied package name |
| `AssetRegistry.GetByPath` | `<Path>` Query the asset registry for assets matching the supplied package path |
| `AssetRegistry.GetByTag` | `<TagName> <TagValue>` Query the asset registry for assets matching the supplied tag and value |
| `AssetRegistry.GetDependencies` | `<PackageName>` Query the asset registry for dependencies for the specified package |
| `AssetRegistry.GetReferencers` | `<ObjectPath>` Query the asset registry for referencers for the specified package |
| `AssetRegistry.ScanPath` | `<PathToScan>` Scan the given filename or directoryname for package files and load them into the assetregistry. Extra string parameters: `-forcerescan`, `-ignoreDenyLists`, `-asfile`, `-asdir` |
| `AssetTools.LogFolderPermissions` | Logs the read and write permissions for folders |
| `au.3dVisualize.Attenuation` | Whether or not attenuation spheres are visible when 3d visualize is enabled. 0: Not Enabled, 1: Enabled |
| `au.AudioSourceManager.HangDiagnostics` |   |
| `au.AudioThreadCommand.ChokeCommandQueue` |   |
| `au.AudioThreadCommand.ChokeMPSCCommandQueue` |   |
| `au.AudioThreadCommand.SpamCommandQueue` |   |
| `au.ClearMutesAndSolos` | Clears any solo-ing/mute-ing sounds |
| `au.debug.bufferdiagnostics` | Enables per buffer sample diagnostics (Nans/denorms/Infs) |
| `au.Debug.Modulation` | Post Audio Modulation information to viewport(s). 0: Disable, 1: Enable (Optional) `-AllViews`: Enables/Disables for all viewports, not just those associated with the current world |
| `au.Debug.PlaySoundCue` | Plays a SoundCue: `-Name <SoundName>`: If a debug sound with the short name is specified in AudioSettings, plays that sound. `-Path <ObjectPath>`: Finds SoundCue asset at the provided path and if found, plays that sound. `-Radius <Distance>`: If set, enables sound spatialization and sets radial distance between listener and source emitting sound. `-Azimuth <Angle>`: If set, enables sound spatialization and sets azimuth angle between listener and source emitting sound (in degrees, where 0 is straight ahead, negative to left, positive to right). `-Elevation <Angle>`: If set, enables sound spatialization and sets azimuth angle between listener and source emitting sound (in degrees, where 0 is straight ahead, negative to left, positive to right). `-AllViews`: If option provided, plays sound through all viewports. `-LogSubtitles`: If option provided, logs sounds subtitle if set. |
| `au.Debug.PlaySoundWave` | Plays a SoundWave: `-Name <SoundName>`: If a debug sound with the short name is specified in AudioSettings, plays that sound. `-Path <ObjectPath>`: Finds SoundWave asset at the provided path and if found, plays that sound. `-Radius`: If set, enables sound spatialization and sets radial distance between listener and source emitting sound. `-Azimuth <Angle>`: If set, enables sound spatialization and sets azimuth angle between listener and source emitting sound (in degrees, where 0 is straight ahead, negative to left, positive to right). `-Elevation <Angle>`: If set, enables sound spatialization and sets azimuth angle between listener and source emitting sound (in degrees, where 0 is straight ahead, negative to left, positive to right). `-AllViews`: If option provided, plays sound through all viewports. -LogSubtitles: If option provided, logs sounds subtitle if set |
| `au.Debug.SoundCues` | Post SoundCue information to viewport(s). 0: Disable, 1: Enable. (Optional) `-AllViews`: Enables/Disables for all viewports, not just those associated with the current world |
| `au.Debug.SoundMixes` | Post SoundMix information to viewport(s). 0: Disable, 1: Enable. (Optional) `-AllViews`: Enables/Disables for all viewports, not just those associated with the current world |
| `au.Debug.SoundReverb` | Post SoundReverb information to viewport(s). 0: Disable, 1: Enable (Optional) `-AllViews`: Enables/Disables for all viewports, not just those associated with the current world |
| `au.Debug.Sounds` | Post Sound information to viewport(s). 0: Disable, 1: Enable (Optional) `-AllViews`: Enables/Disables for all viewports, not just those associated with the current world |
| `au.Debug.SoundWaves` | Post SoundWave information to viewport(s). 0: Disable, 1: Enable (Optional) `-AllViews`: Enables/Disables for all viewports, not just those associated with the current world |
| `au.Debug.StopSound` | Stops debug sound. -AllViews: If option provided, stops all debug sounds in all viewports. |
| `au.Debug.Streaming` | Post Stream Caching information to viewport(s). 0: Disable, 1: Enable (Optional) `-AllViews`: Enables/Disables for all viewports, not just those associated with the current world |
| `au.DumpActiveSounds` | Outputs data about all the currently active sounds. |
| `au.DumpBakedAnalysisData` | debug command to dump the baked analysis data of a sound wave to a csv file. |
| `au.MetaSound.Experimental.OperatorPool.SetMaxNumOperators` | Set the maximum number of operators in the MetaSound operator cache. |
| `au.Metasound.Profiling.AddNodes` | Adds the specified node class name(s) to the list of metasound nodes that will be profiled and visible in Insights. |
| `au.Metasound.Profiling.ListNodes` | Lists the node class names that will be profiled and visible in Insights. |
| `au.Metasound.Profiling.RemoveNodes` | Removes the specified node class name(s) (or ALL if no names are provided) from the list of node types that will be profiled and visible in Insights. |
| `au.Modulation.SetPitchRange` | Sets max final modulation range of pitch (in semitones). Default: 96 semitones (+/- 4 octaves) |
| `au.ReportAudioDevices` | This will log any active audio devices (instances of the audio engine) alive right now. |
| `au.SourceFadeMin` | Sets the length (in samples) of minimum fade when a sound source is stopped. Must be divisible by 4 (vectorization requirement). Ignored for some procedural source types. (Default: 512, Min: 4). |
| `au.spatialization.ListAvailableSpatialPlugins` | This will output a list of currently available/active spatialization plugins |
| `au.spatialization.SetCurrentSpatialPlugin` | Attempt to swap to the named spatialization plugin (au.spatialization.ListAvailableSpatialPlugins to see what is availible) |
| `au.streamcaching.FlushAudioCache` | This will flush any non retained audio from the cache when Stream Caching is enabled. |
| `au.streamcaching.ResizeAudioCacheTo` | This will try to cull enough audio chunks to shrink the audio stream cache to the new size if neccessary, and keep the cache at that size. |
| `au.streamcaching.StartProfiling` | This will start a performance-intensive profiling mode for this streaming manager. Profile stats can be output with audiomemreport. |
| `au.streamcaching.StopProfiling` | This will start a performance-intensive profiling mode for this streaming manager. Profile stats can be output with audiomemreport. |
| `au.submix.drawgraph` | Draws the submix heirarchy for this world to the debug output |
| `AudioThread.TaskPriority` | Takes a single parameter of value `High`, `Normal`, `BackgroundHigh`, `BackgroundNormal` or `BackgroundLow`. |
| `bp.AuditFunctionCallsForBlueprint` | Audit all functions called by a specified blueprint. Single argument supplies the asset to audit. Writes results to the log. |
| `bp.AuditThreadSafeFunctions` | Audit currently loaded thread safe functions. Writes results to the log. |
| `BP.DumpAllRegisteredNamespacePaths` | Dumps all registered namespace paths. |
| `BP.ToggleUsePackagePathAsDefaultNamespace` | Toggle the use of a type's package path as its default namespace when not explicitly assigned. Otherwise, all types default to the global namespace. |
| `c.ToggleGPUCrashedFlagDbg` | Forcibly toggles the 'GPU Crashed' flag for testing crash analytics. |
| `CancelAllTasks` |   |
| `CollectionManager.Add` | Adds the specified object path to the specified collection |
| `CollectionManager.Create` | Creates a collection of the specified name and type |
| `CollectionManager.Destroy` | Deletes a collection of the specified name and type |
| `CollectionManager.Remove` | Removes the specified object path from the specified collection |
| `Collision.ListChannels` | ListChannels |
| `Collision.ListComponentsWithResponseToProfile` |   |
| `Collision.ListObjectsWithCollisionComplexity` |   |
| `Collision.ListProfiles` | ListProfiles |
| `Collision.ListProfilesWithResponseToChannel` |   |
| `ContentBrowser.Debug.ConvertInternalPathToVirtual` | Convert internal path |
| `ContentBrowser.Debug.TryConvertVirtualPath` | Try to convert virtual path |
| `ControlRig.Hierarchy.Trace` | Traces changes in a hierarchy for a provided number of executions (defaults to 1). You can use ControlRig.Hierarchy.TraceCallstack to enable callstack tracing as part of this. |
| `ControlRig.LoadAllAssets` | Loads all control rig assets. |
| `CoreUObject.AttemptToFindShortTypeNamesInMetaData` | Finds short type names stored in known MetaData entries |
| `CoreUObject.AttemptToFindUninitializedScriptStructMembers` | Finds USTRUCT() structs that fail to initialize reflected member variables |
| `CPUTime.Dump` | Usage `-Delay=[NumSeconds=30]` If Delay==0, disables printing the CPU usage to the log If Delay>0, starts printing the average CPU usage from the last n frames, clamps between 10 and 300 |
| `CreateDummyFileInPersistentStorage` | Create a dummy file with specified size in specified persistent storage folder |
| `CsvCategory` | Changes whether a CSV category is included in captures. |
| `CsvProfile` | Starts or stops Csv Profiles |
| `CustomTimeStep.reset` | Resets the current custom step. |
| `D3D12.DumpRayTracingGeometries` | Dump memory allocations for ray tracing resources. |
| `D3D12.DumpRayTracingGeometriesToCSV` | Dump all memory allocations for ray tracing resources to a CSV file on disc. |
| `D3D12.DumpTrackedAllocationCallstacks` | Dump all tracked d3d12 resource allocation callstacks. |
| `D3D12.DumpTrackedAllocations` | Dump all tracked d3d12 resource allocations. |
| `D3D12.DumpTrackedResidentAllocationCallstacks` | Dump all tracked resident d3d12 resource allocation callstacks. |
| `D3D12.DumpTrackedResidentAllocations` | Dump all tracked resisdent d3d12 resource allocations. |
| `D3D12.RayTracing.SerializeScene` | Serialize Ray Tracing Scene to disk. |
| `DDC.LoadReplay` | Loads a cache replay file created by `-DDC-ReplaySave=<Path>` |
| `DDC.MountPak` | Mounts read-only pak file |
| `DDC.UnmountPak` | Unmounts read-only pak file |
| `Demo.ActorPrioritizationEnabled` | Set whether or not actor prioritization is enabled on demo driver of the current world. |
| `Demo.CheckpointSaveMaxMSPerFrame` | Set max checkpoint record time in MS on demo driver of the current world. |
| `Demo.MaxDesiredRecordTimeMS` | Set max desired record time in MS on demo driver of the current world. |
| `Demo.SetLocalViewerOverride` | Set first local player controller as the viewer override on demo driver of the current world. |
| `Demo.TestWriteEvent` | Add or update a test replay event on the currently recording replay, with an optional argument for event size in bytes |
| `diff` | diff two assets against one another. format: `'diff <lhs> <rhs>` |
| `dp.Override.Restore` | Restores any cvars set by dp.Override to their previous value |
| `DumpCCmds` | Lists all CVars (or a subset) and their values. Can also show help, and can save to .csv. Usage: `DumpCCmds [Prefix] [-showhelp] [-csv=[path]]` If -csv does not have a file specified, it will create a file in the Project Logs directory |
| `DumpConsoleCommands` | Dumps all console vaiables and commands and all exec that can be discovered to the log/console |
| `DumpCVars` | Lists all CVars (or a subset) and their values. Can also show help, and can save to .csv. Usage: `DumpCVars [Prefix] [-showhelp] [-csv=[path]]` If -csv does not have a file specified, it will create a file in the Project Logs directory |
| `DumpDetailedPrimitives` | Writes out all scene primitive details to a CSV file |
| `DumpGPU` | Dump one frame of rendering intermediary resources to disk. |
| `DumpLevelCollections` | Dump level collections in the current world. |
| `DumpLightmapSizeOnDisk` | Dumps the size of all loaded lightmaps on disk (source and platform data) |
| `DumpLLM` | Logs out the current and peak sizes of all tracked LLM tags |
| `DumpNiagaraWorldManager` | Dump Information About the Niagara World Manager Contents |
| `DumpPackagePayloadInfo` | Writes out information about a package's payloads to the log. |
| `DumpPersistentStorage` | Dumps PersistentStorage |
| `DumpPrimitives` | Writes out all scene primitive names to a CSV file |
| `dumpticks` | Dumps all tick functions registered with FTickTaskManager to log. |
| `DumpUnbuiltLightInteractions` | Logs all lights and primitives that have an unbuilt interaction. |
| `DumpVisibleActors` | Dump visible actors in current world. |
| `Editor.AsyncAssetCompilationFinishAll` | Finish all assets compilations |
| `Editor.AsyncAssetDumpStallStacks` | Dump all the callstacks that have caused waits on async compilation. |
| `Editor.AsyncSkinnedAssetCompilationFinishAll` | Finish all skinned assets compilations |
| `Editor.AsyncSoundWaveCompilationFinishAll` | Finish all soundwaves compilations |
| `Editor.AsyncStaticMeshCompilationFinishAll` | Finish all static meshes compilations |
| `Editor.AsyncTextureCompilationFinishAll` | Finish all textures compilations |
| `Editor.Debug.SlowTask.Simulate` | Runs a busy loop for N seconds. Will tick the slow task every 100ms until it is complete |
| `Editor.EnableInViewportMenu` | Enables the new in-viewport property menu |
| `Editor.ObjectReverseLookupValidate` | Compare objects contained in the reverse lookup against the old scanning method to see if there is any discrepenties. |
| `Editor.ResizeMainFrame` |   |
| `EditorDomain.DumpClassDigests` | Write to the log the digest information for each class. |
| `EnableGDT` | Toggles Gameplay Debugger Tool |
| `EnhancedInput.DumpKeyProfileToLog` |   |
| `EnhancedInput.SaveKeyProfilesToSlot` | Save the user input settings object with the Save Game to slot system |
| `FindRedundantMICS` | Looks at all loaded MICs and looks for redundant ones. |
| `FName.Dump` | Dump all base FName strings to a file. Pass -num=n to dump the most recent n names. |
| `FName.DumpNumbered` | Dump all numbered FNames to a file (only when UE\_FNAME\_OUTLINE\_NUMBER is set). Pass -num=n to dump the most recent n names. |
| `FName.HashCsv` | Write FName hash stats to a csv file. |
| `FName.List` | List all base FName strings to the output device. Pass -num=n to list the most recent n names. |
| `FName.ListNumbered` | List all numbered FNames to the output devicce (only when UE\_FNAME\_OUTLINE\_NUMBER is set). Pass -num=n to list the most recent n names. |
| `FName.Stats` | Write FName stats to the output device. |
| `foliage.Freeze` | Useful for debugging. Freezes the foliage culling and LOD. |
| `foliage.LogFoliageFrame` | Useful for debugging. Logs all foliage rendered in a frame. |
| `foliage.RebuildFoliageTrees` | Rebuild the trees for non-grass foliage. |
| `foliage.Test` | Useful for debugging. |
| `foliage.ToggleVectorCull` | Useful for debugging. Toggles the optimized cull. |
| `foliage.UnFreeze` | Useful for debugging. Freezes the foliage culling and LOD. |
| `FontAtlasVisualizer` | Displays the Slate font atlas visualizer |
| `ForceBuildStreamingData` | Forces streaming data to be rebuilt for the current world. |
| `fx.DumpCompileIdDataForAsset` | Dumps data relevant to generating the compile id for an asset. |
| `fx.DumpEmitterDepencenciesInFolder` | Dumps emitter dependencies for all systems in the supplied folder and sub-folders. |
| `FX.DumpNCPoolInfo` | Dump Niagara System Pooling Info |
| `fx.DumpNiagaraScalabilityState` | Dumps state information for all Niagara Scalability Mangers. |
| `fx.DumpPSCPoolInfo` | Dump Particle System Pooling Info |
| `fx.DumpPSCTickStateInfo` | Dumps state information for all current Particle System Components. |
| `fx.DumpRapidIterationParametersForAsset` | Dumps the values of the rapid iteration parameters for the specified asset by path. |
| `fx.InvalidateCachedScripts` | Invalidate Niagara script cache by making a unique change to NiagaraShaderVersion.ush which is included in common.usf.To initiate actual the recompile of all shaders use recompileshaders changed" or press "Ctrl Shift .". The NiagaraShaderVersion.ush file should be automatically checked out but it needs to be checked in to have effect on other machines." |
| `fx.InvalidateNiagaraPerfBaselines` | Invalidates all Niagara performance baseline data. |
| `fx.LoadAllNiagaraSystemsInFolder` | Loads all niagara systems in the supplied directory and sub-directories. |
| `fx.Niagara.DataChannels.DumpWriteLog` | Dump all the currently stored writes to the log (see fx.Niagara.DataChannels.FrameDataToCapture on how many frames are captured) |
| `fx.Niagara.DataChannels.ResetLayoutInfo` | Resets all data channel layout info used by data interfaces to access data channels. |
| `fx.Niagara.Debug.Hud` | Set options for debug hud display |
| `fx.Niagara.Debug.KillSpawned` | Kills all spawned compoonents |
| `fx.Niagara.Debug.PlaybackMode` | Set playback mode 0 - Play 1 - Paused 2 - Step |
| `fx.Niagara.Debug.PlaybackRate` | Set playback rate |
| `fx.Niagara.Debug.SpawnComponent` | Spawns a NiagaraComponent using the given parameters |
| `fx.Niagara.DumpComponents` | Dump Information about all Niagara Components |
| `fx.Niagara.FixDuplicateVariableGuids` | Validates and fixes the script guids of a given script, if duplicates exist. |
| `fx.Niagara.RenderTarget.OverrideFormat` | Optional global format override for all Niagara render targets |
| `fx.Niagara.Scalability.CullingMode` | Set scalability culling mode 0 - Enabled. Culling is enabled as normal. 1 - Paused. No culling will occur but FX will still be tracked internally so culling can be resumed correctly later. 2 - Disabled. No culling will occur and no FX will be tracked. Culling may not work correctly for some FX if enabled again after this. |
| `fx.Niagara.SetOverridePlatformName` | Sets which platform we should override with, no args means reset to default |
| `fx.Niagara.SetOverrideQualityLevel` | Sets which quality level we should override with, no args means clear the override and return to non overriden quality level). Valid levels are 0-4 (Low-Cinematic) |
| `fx.Niagara.TaskPriorities.Dump` | Dump currently set priorities |
| `fx.Niagara.TaskPriorities.RunTest` | Run a test set of priorites |
| `fx.Niagara.ValidateDuplicateVariableGuids` | Validate the script guids of a given script. |
| `fx.NiagaraEditor.ReinitializeStyle` | Reinitializes the style for the niagara editor module. Used in conjuction with live coding for UI tweaks. May crash the editor if style objects are in use. |
| `fx.NiagaraEditorWidgets.ReinitializeStyle` | Reinitializes the style for the niagara editor widgets module. Used in conjuction with live coding for UI tweaks. May crash the editor if style objects are in use. |
| `fx.ParticlePerfStats.RunTest` | Runs for a number of frames then logs out the results. Arg0 = NumFrames. Arg1 = Gather World Stats (default 0). Arg2 = Gather System Stats (default 1). Arg3 = Gather Component Stats (default 0). |
| `fx.PreventAllSystemRecompiles` | Loads all of the systems in the project and forces each system to refresh all it's dependencies so it won't recompile on load. This may mark multiple assets dirty for re-saving. |
| `fx.PreventSystemRecompile` | Forces the system to refresh all it's dependencies so it won't recompile on load. This may mark multiple assets dirty for re-saving. |
| `fx.PSCMan.Dump` | Dumps state information for all current Particle System Managers. |
| `fx.RebuildDirtyScripts` | Go through all loaded assets and force them to recompute their script hash. If dirty, regenerate. |
| `FX.RestartAll` | Restarts all particle system components |
| `fx.TestCompileNiagaraScript` | Compiles the specified script on disk for the niagara vector vm |
| `fx.UpgradeAllNiagaraAssets` | Loads all Niagara assets and preforms any data upgrade processes required. This may mark multiple assets dirty for re-saving. |
| `GameplayMediaEncoder.Initialize` | Constructs the audio/video encoding objects. Does not start encoding |
| `GameplayMediaEncoder.Shutdown` | Releases all systems. |
| `GameplayMediaEncoder.Start` | Starts encoding |
| `GameplayMediaEncoder.Stop` | Stops encoding |
| `GameplayTags.DumpTagList` | Writes out a csvs with all tags to Reports/TagList.csv, Reports/TagReferencesList.csv and Reports/TagSourcesList.csv |
| `GameplayTags.PackingTest` | Prints frequency of gameplay tags |
| `GameplayTags.PrintNetIndices` | Prints net indices for all known tags |
| `GameplayTags.PrintReplicationFrequencyReport` | Prints the frequency each tag is replicated. |
| `GameplayTags.PrintReplicationIndicies` | Prints the index assigned to each tag for fast network replication. |
| `GameplayTags.PrintReport` | Prints frequency of gameplay tags |
| `gc.CalculateHistorySize` |   |
| `gc.DebugGraphHide` | Hide GC debug graph. |
| `gc.DebugGraphShow` | Show GC debug graph. (See also: DebugGraphSafeDurationThresholdMs) |
| `gc.DumpMemoryStats` | Print GC memory usage |
| `gc.DumpRefsToCluster` | Dumps references to all objects within a cluster. Specify the cluster name with Root=Name. |
| `gc.DumpSchemaStats` | Print GC schema statistics |
| `gc.FindStaleClusters` | Dumps all clusters do output log that are not referenced by anything. |
| `gc.GenerateReachabilityStressData` | Allocate deeply-nested UObject tree to stress test reachability analysis. |
| `gc.HistorySize` |   |
| `gc.ListClusters` | Dumps all clusters do output log. When 'Hiearchy' argument is specified lists all objects inside clusters. |
| `gc.SuggestClusters` | Searches for assets which contain many internal objects which are not clustered. |
| `gc.UnlinkReachabilityStressData` | Unlink previously-generated reachability analysis stress test data for collection in the next cycle. |
| `gdt.Enable` | Enable Gameplay Debugger Tool |
| `gdt.EnableCategoryName` | Enables/disables categories matching given substring. Use: `gdt.EnableCategoryName <CategoryNamePart> [Enable]` |
| `gdt.fontsize` | Configures gameplay debugger's font size. Usage: `gdt.fontsize <fontSize> (default = 10)` |
| `gdt.SelectLocalPlayer` | Selects the local player for debugging |
| `gdt.SelectNextRow` | Selects next row |
| `gdt.SelectPreviousRow` | Selects previous row |
| `gdt.Toggle` | Toggles Gameplay Debugger Tool |
| `gdt.ToggleCategory` | Toggles specific category index |
| `geomcache.TriggerBulkDataCrash` | Test a crash searializing large bulk data object |
| `geometry.DynamicMesh.ClearDebugMeshes` | Discard all debug meshes currently stored in the FDynamicMesh3 Global Debug Mesh set. This command only works in the Editor. |
| `GeometryCollection.BuildProximityDatabase` | Build the Proximity information in the GeometryGroup for the selected collection. |
| `GeometryCollection.ClusterAlongYZPlane` | Debuigging command to split the unclustered geometry collection along the YZPlane. |
| `GeometryCollection.CreateFromSelectedActors` | Creates a GeometryCollection from the selected Actors that contain Skeletal and Statict Mesh Components |
| `GeometryCollection.CreateFromSelectedAssets` | Creates a GeometryCollection from the selected Skeletal Mesh and Static Mesh Assets |
| `GeometryCollection.DeleteCoincidentVertices` | Delete coincident vertices on a GeometryCollection. WARNING: The collection can be very large. |
| `GeometryCollection.DeleteGeometry` | Delete geometry by transform name. |
| `GeometryCollection.DeleteHiddenFaces` | Delete hidden faces on a GeometryCollection. WARNING: The collection can be very large. |
| `GeometryCollection.DeleteStaleVertices` | Delete stale vertices on a GeometryCollection. WARNING: The collection can be very large. |
| `GeometryCollection.DeleteZeroAreaFaces` | Delete zero area faces on a GeometryCollection. WARNING: The collection can be very large. |
| `GeometryCollection.Heal` | Tries to fill holes in go. |
| `GeometryCollection.PrintDetailedStatistics` | Prints detailed statistics of the contents of the collection. |
| `GeometryCollection.PrintDetailedStatisticsSummary` | Prints detailed statistics of the contents of the selected collection(s). |
| `GeometryCollection.PrintStatistics` | Prints statistics of the contents of the collection. |
| `GeometryCollection.SelectAllGeometry` | Select all geometry in hierarchy. |
| `GeometryCollection.SelectInverseGeometry` | Deselect inverse of currently selected geometry in hierarchy. |
| `GeometryCollection.SelectLessThenVolume` | Select all geometry with a volume less than specified. |
| `GeometryCollection.SelectNone` | Deselect all geometry in hierarchy. |
| `GeometryCollection.SetNamedAttributeValues` | Command to set attributes within a named group. |
| `GeometryCollection.SetupNestedBoneAsset` | Converts the selected GeometryCollectionAsset into a test asset. |
| `GeometryCollection.SetupTwoClusteredCubesAsset` | Addes two clustered cubes to the selected actor. |
| `GeometryCollection.ToString` | Dump the contents of the collection to the log file. WARNING: The collection can be very large. |
| `GeometryCollection.WriteToHeaderFile` | Dump the contents of the collection to a header file. WARNING: The collection can be very large. |
| `GeometryCollection.WriteToOBJFile` | Dump the contents of the collection to an OBJ file. WARNING: The collection can be very large. |
| `GPUDebugCrash` | Crash GPU intentionally for debugging. |
| `grass.DumpExclusionBoxes` | Print the exclusion boxes, debugging. |
| `grass.DumpGrassData` | Dumps a report of all grass data being currently used on landscape components. \[Optional: `-csv -detailed -byproxy -bycomponent -bygrasstype -full`\] `-csv`: formats the report in a CSV-friendly way. `-fullnames`: displays the listed objects' full names, rather than the user-friendly version. `-showempty`: will dump info even from components with no grass data. `-detailed`: shows a detailed report of all grass data, for all grass types, in all landscape components. `-byproxy`: shows a report of grass data per landscape proxy. `-bycomponent`: shows a report of grass data per landscape component. `-bygrasstype`: shows a report of grass data per grass type. `-full`: enables all sub-reports. If no report type option specified, assume full report is requested. |
| `grass.FlushCache` | Flush the grass cache, debugging. |
| `grass.FlushCachePIE` | Flush the grass cache, debugging. |
| `help` | Outputs some helptext to the console and the log |
| `HighlightRecorder.Pause` | Pauses recording of highlight clip |
| `HighlightRecorder.Resume` | Resumes recording of highlight clip |
| `HighlightRecorder.Save` | Saves highlight clip, optional parameters: filename (test.mp4 by default) and max duration (float (secs) duration of ring buffer by default) |
| `HighlightRecorder.Start` | Starts recording of highlight clip, optional parameter: max duration (float, 30 seconds by default) |
| `HighlightRecorder.Stop` | Stops recording of highlight clip |
| `HighResShot` | High resolution screenshots. Usage: `HighResShot ResolutionX(int32)xResolutionY(int32) Or Magnification(float) [CaptureRegionX(int32) CaptureRegionY(int32) CaptureRegionWidth(int32) CaptureRegionHeight(int32) MaskEnabled(int32) DumpBufferVisualizationTargets(int32) CaptureHDR(int32)]`. Example: `HighResShot 500x500 50 50 120 500 1 1 1` |
| `Ias.AbandonCache` | Abandon the local file cache |
| `Input.+action` | Provide the named action with a constant input value each frame |
| `Input.+key` | Provide the named key with a constant input value each frame |
| `Input.-action` | Stop forcing the named action value each frame |
| `Input.-key` | Stop forcing the named key each frame |
| `Input.ListAllHardwareDevices` | Log all the platform's currently available FHardwareDeviceIdentifier |
| `ism.Editor.DumpISMPartitionActors` | Output stats about ISMPartitionActor(s) |
| `Landscape.ClearDirty` | Clears all Landscape Dirty Debug Data |
| `landscape.DumpLODs` | Will dump the current status of LOD value and current texture streaming status |
| `Landscape.FixSplines` | One off fix for bad layer width |
| `Landscape.Patches` | Show/hide Landscape patches |
| `Landscape.Static` | Enable/disable Landscape static drawlists |
| `LazyLoad.PrintUnresolvedObjects` | Prints a list of all unresolved objects from the object handle index. |
| `LevelEditor.ToggleImmersive` | Toggle 'Immersive Mode' for the active level editing viewport |
| `ListTimers` |   |
| `LiveCoding` | Enables live coding support |
| `LiveCoding.Compile` | Initiates a live coding compile |
| `LLMSnapshot` | Takes a single LLM Snapshot of one frame. This command requires the commandline -llmdisableautopublish |
| `LoadPackage` | Loads packages by names. Usage: `LoadPackage <package name> [<package name> ...]` |
| `LoadPackageAsync` | Loads packages async by names. Usage: `LoadPackageAsync <package name> [<package name> ...]` |
| `LoadTimes.DumpReport` | Dumps a report about the amount of time spent loading assets |
| `LoadTimes.DumpTracking` | Dump high level load times being tracked |
| `LoadTimes.DumpTrackingLow` | Dump low level load times being tracked |
| `LoadTimes.Reset` | Resets accumulated report data |
| `LoadTimes.ResetTracking` | Reset load time tracking |
| `LoadTimes.StartAccumulating` | Starts capturing fine-grained accumulated load time data |
| `LoadTimes.StopAccumulating` | Stops capturing fine-grained accumulated load time data and dump the results |
| `Localization.DumpLiveTable` | Dumps the current live table state to the log, optionally filtering it based on wildcard arguments for 'Namespace', 'Key', or 'DisplayString', eg) -Key=Foo, or -DisplayString=This is some text", or -Key=Bar\*Baz -DisplayString="This is some other text"" |
| `LogCountedInstances` | Dumps count of all tracked FInstanceCountingObject's |
| `ls.PrintNumLandscapeShadows` | Prints the number of landscape components that cast shadows. |
| `MainFrame.ToggleFullscreen` | Toggles the editor between full screen" mode and "normal" mode. In full screen mode the task bar and window title area are hidden." |
| `mallocleak.clear` | Clears recorded allocation info |
| `mallocleak.report` | Writes malloc leak reports |
| `mallocleak.start` | Starts tracking allocations. Args -report=\[secs\] -size=\[filter\] |
| `mallocleak.stop` | Stops tracking allocations |
| `MallocStomp.OverrunTest` | Overrun test for the FMallocStomp |
| `MallocStomp2.Disable` | Disable MallocStomp2 |
| `MallocStomp2.Enable` | Enable MallocStomp2 |
| `MallocStomp2.MaxSize` | Set the maximum size MallocStomp2 should track |
| `MallocStomp2.MinSize` | Set the minimum size MallocStomp2 should track |
| `MallocStomp2.OverrunTest` | Overrun test for the FMallocStomp2 |
| `MappedFileTest` | Tests the file mappings through the low level. |
| `Memory.StaleTest` | Test for Memory.UsePurgatory. \*\*\* Will crash the game! |
| `Memory.UsePoison` | Uses the poison malloc proxy to check if things are relying on uninitialized or free'd memory. |
| `Memory.UsePurgatory` | Uses the purgatory malloc proxy to check if things are writing to stale pointers. |
| `merge` | Either merge three assets or a single conflicted asset. format: 'merge  \[-o out\_path\]' or 'merge \[-o out\_path\]' |
| `MessageBus.UDP.ClearDenyList` | Clear the UDP socket deny list. |
| `Metadata.Dump` | Dump all MetaData |
| `net.ActorReport` |   |
| `Net.CreateBandwidthGenerator` |   |
| `net.DeleteDormantActor` | Lists open actor channels |
| `net.DisconnectSimulatedConnections` | Disconnects some simulated connections (0 = all) |
| `net.DumpRelevantActors` | Dumps information on relevant actors during next network update |
| `net.ForceOnePacketPerBunch` | When set to true it will enable AutoFlush on all connections and force a packet to be sent for every bunch we create. This forces one packet per replicated actor and can help find rare ordering bugs |
| `Net.GenerateConstantBandwidth` | Deliver a constant throughput every tick to generate the specified Kilobytes per sec. Usage: Net.GenerateBandwidth KilobytesPerSecond |
| `Net.GeneratePeriodicBandwidthSpike` | Generates a spike of bandwidth every X milliseconds. Usage: Net.GeneratePeriodicBandwidthSpike SpikeInKb PeriodInMS |
| `Net.Iris.DebugNetInternalIndex` | Specify an internal index that we will break on (or none to turn off). |
| `Net.Iris.DebugNetRefHandle` | Specify a NetRefHandle ID that we will break on (or none to turn off). |
| `Net.Iris.PrintAlwaysRelevantObjects` | Prints the list of netobjects always relevant to every connection |
| `Net.Iris.PrintDynamicFilterClassConfig` | Prints the dynamic filter configured to be assigned to specific classes. |
| `Net.Iris.PrintNetCullDistances` | Prints the list of replicated objects and their current netculldistance. |
| `Net.Iris.PrintRelevantObjects` | Prints the list of netobjects currently relevant to any connection |
| `Net.Iris.PrintRelevantObjectsToConnection` | Prints the list of replicated objects relevant to a specific connection. OptionalParams: WithFilter |
| `Net.Iris.PrintReplicatedObjects` | Prints the list of replicated objects registered for replication in Iris |
| `net.ListActorChannels` | Lists open actor channels |
| `net.ListNetGUIDExports` | Lists open actor channels |
| `net.ListNetGUIDs` | Lists NetGUIDs for actors |
| `net.Packagemap.FindNetGUID` | Looks up object that was assigned a given NetGUID |
| `net.PrintNetConnections` | Prints information on all net connections of a NetDriver. Defaults to the GameNetDriver. Choose a different driver via NetDriverName= or NetDriverDefinition= |
| `Net.PushModelPrintHandles` | Prints the list of replicated objects relevant to a specific connection |
| `net.SimulateConnections` | Starts a Simulated Net Driver |
| `net.TestObjRefSerialize` | Attempts to replicate an object reference to all clients |
| `NetEmulation.DropAnyUnreliable` | Drop any sent unreliable RPCs. (optional)`<0-100>` to set the drop percentage (default is 20). |
| `NetEmulation.DropNothing` | Disables any RPC drop settings previously set. |
| `NetEmulation.DropUnreliableOfActorClass` | Drop random unreliable RPCs sent on actors of the given class type. `<ActorClassName>` Class name to match with (can be a substring). (optional)`<0-100>` to set the drop percentage (default is 20). |
| `NetEmulation.DropUnreliableOfSubObjectClass` | Drop randomly the unreliable RPCs of a subobject of the given class. `<SubObjectClassName>` The name of the RPC (can be a substring). (optional)`<0-100>` to set the drop percentage (default is 20). |
| `NetEmulation.DropUnreliableRPC` | Drop randomly the unreliable RPCs of the given name. `<RPCName>` The name of the RPC (can be a substring). (optional)`<0-100>` to set the drop percentage (default is 20). |
| `NetEmulation.Off` | Turn off network emulation |
| `NetEmulation.PktDup` | Simulates sending/receiving duplicate network packets |
| `NetEmulation.PktEmulationProfile` | Apply a preconfigured emulation profile. |
| `NetEmulation.PktIncomingLagMax` | Sets maximum incoming packet latency |
| `NetEmulation.PktIncomingLagMin` | Sets minimum incoming packet latency |
| `NetEmulation.PktIncomingLoss` | Simulates incoming packet loss |
| `NetEmulation.PktJitter` | Simulates outgoing packet jitter |
| `NetEmulation.PktLag` | Simulates network packet lag |
| `NetEmulation.PktLagMax` | Sets maximum outgoing packet latency) |
| `NetEmulation.PktLagMin` | Sets minimum outgoing packet latency |
| `NetEmulation.PktLagVariance` | Simulates variable network packet lag |
| `NetEmulation.PktLoss` | Simulates network packet loss |
| `NetEmulation.PktOrder` | Simulates network packets received out of order |
| `NetTrace.SetTraceVerbosity` | Start NetTrace with given verbositylevel. |
| `NiagaraDebugHud` | Shorter version to quickly toggle debug hud modes No value will toggle the overview on / off A numberic value selects which overmode to set, where 0 is off |
| `NiagaraReportSystemMemory` | Dumps some rough information about system memory breakdown |
| `online.ResetAchievements` | Reset achievements for the currently logged in user. |
| `p.chaos.dumphierarcystats` | Outputs current collision hierarchy stats to the output log |
| `p.Chaos.StartVDRecording` | Turn on the recording of debugging data |
| `p.Chaos.StopVDRecording` | Turn off the recording of debugging data |
| `p.Chaos.VD.SetCVDDataChannelEnabled` | Turn on or off a CVD Data Channel. Argument 1 is true or false, Argument is a comma separated list of channel names. Example: p.Chaos.VD.SetCVDDataChannelEnabled true SceneQueries,Integrate |
| `p.Chaos.VD.SpawnNewCVDInstance` | Opens a new CVD windows wothout closing an existing one |
| `p.ChaosCloth.Ispc` | Enable or disable ISPC optimizations for cloth simulation. |
| `p.DumpPhysicalMaterialMaskData` | Outputs the current mask data for the specified physical material mask asset to the log. |
| `PackageName.ConvertFilenameToLongPackageName` | Prints the corresponding packagename for a filename at a given localpath, according to the current registered mount points. Prints empty string if not mounted. |
| `PackageName.ConvertLongPackageNameToFilename` | Prints the corresponding local filename for a given packagename, according to the current registered mount points. Prints empty string if not mounted. |
| `PackageName.DumpMountPoints` | Print registered LongPackagePath mount points |
| `PackageName.RegisterMountPoint` | `<RootPath> <ContentPath>` // Register a LongPackagePath mount point |
| `PackageName.UnregisterMountPoint` | `<RootPath> <ContentPath>` // Remove a LongPackagePath mount point |
| `PackageTools.ReloadPackage` | Force a reload of the named package, e.g. PackageTools.ReloadPackage /Game/MyAsset |
| `pak.AsyncFileTest` | Read a block of data from a file using an AsyncFileHandle. params: `<filename> <size> <offset>` |
| `pak.TestRegisterEncryptionKey` | Test dynamic encryption key registration. params: `<guid> <base64key>` |
| `PakFileTest` | Tests the low level filesystem by mounting a pak file and doing multithreaded loads on it forever. Arg should be a full path to a pak file. |
| `PersistentStorageCategoryStats` | Get the stat of each persistent storage stats |
| `r.AOListMemory` |   |
| `r.AOListMeshDistanceFields` |   |
| `r.CopyLockedViews` | Copies all locked views in to a string that r.LockView will accept to reload them. |
| `r.DumpBufferPoolMemory` | Dump allocation information for the buffer pool. |
| `r.DumpPipelineCache` | Dump current cache stats. |
| `r.DumpRenderTargetPoolMemory` | Dump allocation information for the render target pool. |
| `r.DumpShadows` | Dump shadow setup (for developer only, only for non shiping build) |
| `r.FlushMaterialUniforms` |   |
| `r.HLOD` | Single argument: 0 or 1 to Disable/Enable HLOD System Multiple arguments: force X where X is the HLOD level that should be forced into view |
| `r.HLOD.ListUnbuilt` | Lists all unbuilt HLOD actors in the world |
| `r.InvalidateCachedShaders` | Invalidate shader cache by making a unique change to ShaderVersion.ush which is included in common.usf.To initiate actual the recompile of all shaders use recompileshaders changed" or press "Ctrl Shift .". The ShaderVersion.ush file should be automatically checked out but it needs to be checked in to have effect on other machines." |
| `r.ListSceneColorMaterials` | Lists all materials that read from scene color. |
| `r.MeshDrawCommands.DumpStats` | Dumps all of the Mesh Draw Command stats for a single frame to a csv file in the saved profile directory. |
| `r.RayTracing.UpdateCachedState` | Update cached ray tracing state (mesh commands and instances). |
| `r.RecompileRenderer` | Recompiles the renderer module on the fly. |
| `r.RecreateRenderStateContext` | Recreate render state. |
| `r.ResetRenderTargetsExtent` | To reset internal render target extents |
| `r.ResetViewState` | Reset some state (e.g. TemporalAA index) to make rendering more deterministic (for automated screenshot verification) |
| `r.RHI.Name` | Show current RHI's name |
| `r.RHISetGPUCaptureOptions` | Utility function to change multiple CVARs useful when profiling or debugging GPU rendering. Setting to 1 or 0 will guarantee all options are in the appropriate state. r.rhithread.enable, r.rhicmdbypass, r.showmaterialdrawevents, toggledrawevents Platform RHI's may implement more feature toggles. |
| `r.RHIThread.Enable` | Enables/disabled the RHI Thread and determine if the RHI work runs on a dedicated thread or not. |
| `r.SceneCapture.DumpMemory` | Editor specific command to dump scene capture memory to log |
| `r.SetFramePace` | Set a target frame rate for the frame pacer.To set 30fps: r.SetFramePace 30"" |
| `r.SetNearClipPlane` | Set the near clipping plane (in cm) |
| `r.ShaderCompiler.PrintStats` | Prints out to the log the stats for the shader compiler. |
| `r.ShaderPipelineCache.Close` | Close the current pipeline file cache. |
| `r.ShaderPipelineCache.Open` | Close and reopen the user cache. |
| `r.ShaderPipelineCache.Save` | Save the current pipeline file cache. |
| `r.ShaderPipelineCache.SetBatchMode` | Sets the compilation batch mode, which should be one of: Pause: Suspend precompilation. Background: Low priority precompilation. Fast: High priority precompilation. |
| `r.Shadow.Virtual.Visualize.DumpLightNames` | Dump light names with virtual shadow maps (for developer use in non-shipping builds) |
| `r.SkylightRecapture` | Updates all stationary and movable skylights, useful for debugging the capture pipeline |
| `r.TextureProfiler.DumpRenderTargets` | Dumps all render targets allocated by the RHI. Arguments: -CombineTextureNames Combines all textures of the same name into a single line of output -CSV Produces CSV ready output |
| `r.TextureProfiler.DumpTextures` | Dumps all textures allocated by the RHI. Does not include render targets Arguments: -CombineTextureNames Combines all textures of the same name into a single line of output -CSV Produces CSV ready output |
| `r.TogglePreCulledIndexBuffers` | Toggles use of preculled index buffers from the command 'PreCullIndexBuffers' |
| `r.VT.Dump` | Dump a whole lot of info on the VT system state. |
| `r.VT.DumpPoolUsage` | Dump detailed info about VT pool usage. |
| `r.VT.Flush` | Flush all the physical caches in the VT system. |
| `r.VT.FlushAndEvictFileCache` | Flush both the virtual texture physcial page cache and disk file cache |
| `r.VT.ListPhysicalPools` | Dump a whole lot of info on the VT system state. |
| `r.VT.SaveAllocatorImages` | Save images showing allocator usage. |
| `r.VT.ShowDecodeErrors` | Highlight virtual textures with decode errors in hot pink. |
| `Reattach.Components` | Useful for debugging, reattaches all components. Parameter needs to be the class name. Example: Reattach.Components class=SkeletalMeshComponent |
| `Reattach.MaterialInstances` | Useful for debugging, reattaches all materials. Optional parameter can be a materialinstance name (e.g. DecoStatue\_Subsurface0). |
| `Reattach.Materials` | Useful for debugging, reattaches all materials. Optional parameter can be a material name (e.g. DecoStatue\_Subsurface0\_Inst). |
| `RedirectCollector.ResolveAllSoftObjectPaths` | Attempts to load / resolve all currently referenced Soft Object Paths |
| `RedirectToFile` | Creates a file inside Project's Saved folder and outputs command result into it as well as into the log. Usage: `RedirectToFile <filepath/filename> <command> [command arguments]` Example: `RedirectToFile Profiling/CSV/objlist.csv obj list -csv -all` Directory structure under Project/Saved folder specified by `<filepath>` will be created for you if it doesn't exist. |
| `ReferenceInfo` | Outputs reference info for selected actors to a log file. Syntax is: `ReferenceInfo [-depth=<depth value>] [-nodefault] [-noscript]` |
| `ReloadGlobalShaders` | Reloads the global shaders file |
| `rhi.DumpMemory` | Dumps RHI memory stats to the log |
| `rhi.DumpResourceCounts` | Dumps RHI resource counts to the log |
| `rhi.DumpResourceMemory` | Dumps RHI resource memory stats to the log Usage: `rhi.DumpResourceMemory [<Number To Show>] [all] [summary] [Name=<Filter Text>] [Type=<RHI Resource Type>] [Transient=<no, yes, or all> [csv]` |
| `RunTask` |   |
| `SequenceRecorder` | Enables the Sequence Recorder tab |
| `SetGlobalShaderCacheOverrideDirectory` | Set the directory to read the override global shader map file from. |
| `SetThreadConfig` | Sets a thread Priority and/or Affinity. A single arg of default resets all the thread Priorities and Affinities, otherwise \[GT,RT,RHI,Task,TaskBP\] both/either \[TPri\_type\] \[0x\] sets the Priority and/or Affinity. |
| `ShrinkUObjectHashTables` | Shrinks all of the UObject hash tables. |
| `Slate.Commands.ListAll` |   |
| `Slate.Commands.ListBound` |   |
| `Slate.DeleteResources` | Flushes and deletes all resources created by Slate's RHI Resource Manager. |
| `Slate.DumpUpdateList` | (Deprecated) use Slate.InvalidationRoot.DumpUpdateListOnce |
| `Slate.Navigation.Simulate` | Log the result of what the widget may do when it received a navigation event. Use: `Slate.Navigation.Simulate Widget=0x00AABBCCDD Navigation=UINavigationIndex [UserIndex=Number] [Genesis=NavigationGenesisIndex]`. UINavigationIndex use: 0 for Left, 1 for Right, 2 for Up, 3 for Down, 4 for Next, 5 for Previous. NavigationGenesisIndex use: 0 for Keyboard, 1 for Controller, 2 for User. |
| `Slate.TestMessageDialog` |   |
| `Slate.TestMessageLog` |   |
| `Slate.TestNotifications` |   |
| `Slate.TestProgressNotification` |   |
| `Slate.TriggerInvalidate` | Triggers a global invalidate of all widgets |
| `SlateDebugger.Break.OnWidgetBeginPaint` | Break before the widget get painted (must be attached to a debugger). Usage: `[WidgetPtr=0x1234567]\|[WidgetId=12345]` |
| `SlateDebugger.Break.OnWidgetEndPaint` | Break after the widget got painted (must be attached to a debugger). Usage: `[WidgetPtr=0x1234567]\|[WidgetId=12345]` |
| `SlateDebugger.Break.OnWidgetInvalidation` | Break when the widget get invalidated (must be attached to a debugger). Usage: `[WidgetPtr=0x1234567]\|[WidgetId=12345] [Reason=Paint\|Volatility\|ChildOrder\|RenderTransform\|Visibility\|AttributeRegistration\|Prepass\|All]` |
| `SlateDebugger.Break.RemoveAll` | Remove all request to break. |
| `SlateDebugger.Event.DisableAllFocusFilters` | Disable all focus filters |
| `SlateDebugger.Event.DisableAllInputFilters` | Disable all input filters |
| `SlateDebugger.Event.EnableAllFocusFilters` | Enable all focus filters |
| `SlateDebugger.Event.EnableAllInputFilters` | Enable all input filters |
| `SlateDebugger.Event.SetFocusFilter` | Enable or Disable specific focus filters |
| `SlateDebugger.Event.SetInputFilter` | Enable or Disable specific input filters |
| `SlateDebugger.Event.Start` | Starts the debugger. |
| `SlateDebugger.Event.Stop` | Stops the debugger. |
| `SlateDebugger.Invalidate.SetInvalidateRootReasonFilter` | Enable Invalidate Root Reason filters. Usage: `SetInvalidateRootReasonFilter None\|ChildOrder\|Root\|ScreenPosition\|Any` |
| `SlateDebugger.Invalidate.SetInvalidateWidgetReasonFilter` | Enable Invalidate Widget Reason filters. Usage: `SetInvalidateWidgetReasonFilter None\|Layout\|Paint\|Volatility\|ChildOrder\|RenderTransform\|Visibility\|Any` |
| `SlateDebugger.Invalidate.Start` | Start the Invalidation widget debug tool. It shows widgets that are invalidated. |
| `SlateDebugger.Invalidate.Stop` | Stop the Invalidation widget debug tool. |
| `SlateDebugger.InvalidationRoot.Start` | Start the Invalidation Root widget debug tool. It shows when Invalidation Roots are using the slow or the fast path. |
| `SlateDebugger.InvalidationRoot.Stop` | Stop the Invalidation Root widget debug tool. |
| `SlateDebugger.InvalidationRoot.ToggleLegend` | Option to display the color legend. |
| `SlateDebugger.InvalidationRoot.ToggleWidgetNameList` | Option to display the name of the Invalidation Root. |
| `SlateDebugger.Paint.LogOnce` | Log the names of all widgets that were painted during the last update. |
| `SlateDebugger.Paint.Start` | Start the painted widget debug tool. Use to show widget that have been painted this frame. |
| `SlateDebugger.Paint.Stop` | Stop the painted widget debug tool. |
| `SlateDebugger.Paint.ToggleWidgetNameList` | Option to display the name of the widgets that have been painted. |
| `SlateDebugger.Start` | Alias to 'SlateDebugger.Event.Start'. |
| `SlateDebugger.Stop` | Alias to 'SlateDebugger.Event.Stop'. |
| `SlateDebugger.Update.SetWidgetUpdateFlagsFilter` | Enable or Disable specific Widget Update Flags filters. Usage: `SetWidgetUpdateFlagsFilter [None] [Tick] [ActiveTimer] [Repaint] [VolatilePaint] [Any]` |
| `SlateDebugger.Update.Start` | Start the update widget debug tool. It shows when widgets are updated. |
| `SlateDebugger.Update.Stop` | Stop the update widget debug tool. |
| `SlateDebugger.Update.ToggleLegend` | Option to display the color legend. |
| `SlateDebugger.Update.ToggleUpdateFromPaint` | Option to also display the widgets that do not have an update flag but are updated as a side effect of an other widget. |
| `SlateDebugger.Update.ToggleWidgetNameList` | Option to display the name of the widgets that have been updated. |
| `sm.DerivedDataTimings` | Dumps derived data timings to the log. |
| `SparseDelegateReport` | Outputs a report of what sparse delegates are bound. `SparseDelegateReport [name=<ObjectName>] [delegate=<DelegateName>] [class=<ClassName>] -details` |
| `spawnactortimer` | Allows recording of spawn actor times. |
| `StartWorkTest` |   |
| `Stat MapBuildData` |   |
| `stats.NamedEvents` | `<on/off>` Enables or disables the Named Events. |
| `stats.VerboseNamedEvents` | `<on/off>` Enables or disables the Verbose Named Events. |
| `StopWorkTest` |   |
| `SynthBenchmark` | Run simple benchmark to get some metrics to find reasonable game settings automatically Optional (float) parameter allows to scale with work amount to trade time or precision (default: 10). |
| `TaskGraph.ABTestThreads` | Takes two 0/1 arguments. Equivalent to setting TaskGraph.UseHiPriThreads and TaskGraph.UseBackgroundThreads, respectively. Packages as one command for use with the abtest command. |
| `TaskGraph.Benchmark` | Prints the time to run 1000 no-op tasks. |
| `TaskGraph.NumWorkerThreadsToIgnore` | Used to tune the number of task threads. Generally once you have found the right value, PlatformMisc::NumberOfWorkerThreadsToSpawn() should be hardcoded. |
| `TaskGraph.Randomize` | Useful for debugging, adds random sleeps throughout the task graph. |
| `TaskGraph.TaskThreadPriority` | Sets the priority of the task threads. Argument is one of belownormal, normal or abovenormal. |
| `TaskGraph.TestLockFree` | Test lock free lists |
| `TaskGraph.TestLowToHighPri` | Test latency of high priority tasks when low priority tasks are saturating the CPU |
| `TextAssetTool` | \-- |
| `TextureAtlasVisualizer` | Displays the Slate texture atlas visualizer |
| `tick.AddIndirectTestTickFunctions` | Add no-op ticks to test performance of ticking infrastructure. |
| `tick.AddTestTickFunctions` | Add no-op ticks to test performance of ticking infrastructure. |
| `tick.RemoveTestTickFunctions` | Remove no-op ticks to test performance of ticking infrastructure. |
| `TimecodeProvider.reset` | Resets the current timecode provider. |
| `TimedMemReport.Delay` | Determines how long to wait before getting a memreport. < 0 is off |
| `ToggleForceDefaultMaterial` | Render all meshes with the default material. |
| `ToggleLight` | Toggles all lights whose name contains the specified string |
| `ToggleReversedIndexBuffers` | Render static meshes with negative transform determinants using a reversed index buffer. |
| `ToggleShadowIndexBuffers` | Render static meshes with an optimized shadow index buffer that minimizes unique vertices. |
| `ToolMenus.Edit` | Experimental: Enable edit menus mode toggle in level editor's windows menu |
| `ToolMenus.RefreshAllWidgets` | Refresh All Tool Menu Widgets |
| `Trace.Bookmark` | \[Name\] - Emits a TRACE\_BOOKMARK() event with the given string name. |
| `Trace.Disable` | \[ChannelSet\] - Disables a set of channels. ChannelSet is comma-separated list of trace channels/presets to be disabled. If no channel is specified, it disables all channels. |
| `Trace.Enable` | \[ChannelSet\] - Enables a set of channels. ChannelSet is comma-separated list of trace channels/presets to be enabled. |
| `Trace.File` | \[Path\] \[ChannelSet\] - Starts tracing to a file. ChannelSet is comma-separated list of trace channels/presets to be enabled. Either Path or ChannelSet can be excluded. |
| `Trace.Pause` | Pauses all trace channels currently sending events. |
| `Trace.Resume` | Resumes tracing that was previously paused (re-enables the paused channels). |
| `Trace.Screenshot` | \[Name\] \[ShowUI\] Takes a screenshot and saves it in the trace. Ex: Trace.Screenshot ScreenshotName true |
| `Trace.Send` | `<Host> [ChannelSet]` - Starts tracing to a trace store. `<Host>` is the IP address or hostname of the trace store. `[ChannelSet]` is comma-separated list of trace channels/presets to be enabled. |
| `Trace.SnapshotFile` | \[Path\] - Writes a snapshot of the current in-memory trace buffer to a file. |
| `Trace.SnapshotSend` | `<Host> <Port>` - Sends a snapshot of the current in-memory trace buffer to a server. If no host is specified 'localhost' is used. |
| `Trace.Start` | \[ChannelSet\] - (Deprecated: Use Trace.File instead.) Starts tracing to a file. ChannelSet is comma-separated list of trace channels/presets to be enabled. |
| `Trace.Status` | Prints Trace status to console. |
| `Trace.Stop` | Stops tracing profiling events. |
| `TraceFilter.FlushState` | Flushes the current trace filtering state to the output log. |
| `TrackAsyncLoadRequests.Dump` | Dump tracked async load requests and reset tracking |
| `TrackAsyncLoadRequests.DumpToFile` | Dump tracked async load requests and reset tracking |
| `TrackAsyncLoadRequests.Reset` | Reset tracked async load requests |
| `TriggerFailedWindowsRead` | Tests low level IO errors on Windows |
| `TypedElements.OutputRegistredTypeElementsToClipboard` | Output a debug string to the clipboard and to the log. It contains the names of the Typed Elements registred and their Interfaces. For each Interface it also provide the path of the class that implements it. |
| `UAssetLoadTest` | Continuously load assets and GC in the backgroud. Debugging option, this may or may not work with all assets. The test runs forever. If no arg is given all assets in /Game/Content are scanned. |
| `ValidatePackagePayloads` | Checks all payloads that a package references and makes sure that they are valid |
| `VerifyPersistentStorageCategory` | `VerifyPersistentStorageCategory <Category>` |
| `VI.ForceMode` | Toggles viewport interaction on desktop |
| `Vis` | short version of visualizetexture |
| `VisRT` | GUI for visualizetexture |
| `VisualGraphUtils.ControlRig.TraverseHierarchy` | Traverses the hierarchy for a given control rig |
| `VisualGraphUtils.Object.CollectReferences` | Traces all references of an object |
| `VisualGraphUtils.Object.CollectTickables` | Traces all tickables of an object |
| `VisualGraphUtils.Object.LogClassNames` | Logs all class path names given a partial name |
| `VisualGraphUtils.Object.LogInstancesOfClass` | Logs all instances of a given class |
| `VisualizeTexture` | To visualize internal textures |
| `voice.sendLocalTalkersToEndpoint` | This will send audio output for all outgoing voip audio to the named endpoint. if given no arguments, this will disconnect all external endpoints. |
| `voice.sendRemoteTalkersToEndpoint` | This will send audio output for all incoming voip audio to the named endpoint. if given no arguments, this will route voice output through the game engine. |
| `VREd.ForceVRMode` | Toggles VREditorMode, even if not in immersive VR |
| `VREd.ToggleDebugMode` | Toggles debug mode of the VR Mode |
| `Widget.DumpTemplateSizes` | Dump the sizes of all widget class templates in memory |
| `WidgetReflector` | Displays the Slate widget reflector |
| `WidgetReflector.TakeSnapshot` | Take a snapshot and save the result on the local drive. ie. WidgetReflector.TakeSnapshot \[Delay=1.0\] \[Navigation=false\] |
| `WindowsApplication.ApplyLowLevelMouseFilter` | Applies Low Level mouse filter that filters out mouse inputs that act like touch inputs |
| `WindowsApplication.RemoveLowLevelMouseFilter` | Removes Low Level mouse filter that filters out mouse inputs that act like touch inputs |
| `WorldMetrics.SelfTest` | Toggles the World Metrics Subsystem self-test. |
| `wp.Editor.DumpActorDesc` | Dump a specific actor descriptor on the console. |
| `wp.Editor.DumpActorDescs` | Dump the list of actor descriptors in a CSV file. |
| `wp.Editor.DumpClassDescs` | Dump the list of class descriptors in a CSV file. |
| `wp.Editor.DumpStreamingGenerationLog` | Dump the streaming generation log. |
| `wp.Editor.HLOD.DumpStats` | Write various HLOD stats to a CSV formatted file. |
| `wp.Editor.ToggleShowEditorProfiling` | Toggles showing editor profiling stats. |
| `wp.Runtime.DebugFilterByCellName` | Filter debug diplay of world partition streaming by full or partial cell name. Args \[cell name\] |
| `wp.Runtime.DebugFilterByDataLayer` | Filter debug diplay of world partition streaming by data layer. Args \[datalayer labels\] |
| `wp.Runtime.DebugFilterByRuntimeHashGridName` | Filter debug diplay of world partition streaming by grid name. Args \[grid names\] |
| `wp.Runtime.DebugFilterByStreamingStatus` | Filter debug diplay of world partition streaming by streaming status. Args \[streaming status\] |
| `wp.Runtime.DrawWorldPartitionIndex` | Sets the index of the wanted partitioned world to display debug draw. Sets < 0 to display debug draw all registered partitioned worlds. |
| `wp.Runtime.DumpDataLayers` | Dumps data layers to the log |
| `wp.Runtime.DumpStreamingSources` | Dumps active streaming sources to the log |
| `wp.Runtime.DumpWorldPartitions` | Dumps active world partitions to the log |
| `wp.Runtime.HLOD` | Turn on/off loading & rendering of world partition HLODs. |
| `wp.Runtime.OverrideRuntimeSpatialHashLoadingRange` | Sets runtime loading range. Args `-grid=[index] -range=[override_loading_range]` |
| `wp.Runtime.SetDataLayerRuntimeState` | Sets Runtime DataLayers state. Args `[State = Unloaded, Loaded, Activated] [DataLayerNames]` |
| `wp.Runtime.SetLogWorldPartitionVerbosity` | Change the WorldPartition log verbosity. |
| `wp.Runtime.ToggleDataLayerActivation` | Toggles DataLayers active state. Args \[DataLayerNames\] |
| `wp.Runtime.ToggleDrawDataLayers` | Toggles debug display of active data layers. |
| `wp.Runtime.ToggleDrawDataLayersLoadTime` | Toggles debug display of active data layers load time. |
| `wp.Runtime.ToggleDrawLegends` | Toggles debug display of world partition legends. |
| `wp.Runtime.ToggleDrawRuntimeCellsDetails` | Toggles debug display of world partition runtime streaming cells. |
| `wp.Runtime.ToggleDrawRuntimeHash2D` | Toggles 2D debug display of world partition runtime hash. |
| `wp.Runtime.ToggleDrawRuntimeHash3D` | Toggles 3D debug display of world partition runtime hash. |
| `wp.Runtime.ToggleDrawStreamingPerfs` | Toggles debug display of world partition streaming perfs. |
| `wp.Runtime.ToggleDrawStreamingSources` | Toggles debug display of world partition streaming sources. |
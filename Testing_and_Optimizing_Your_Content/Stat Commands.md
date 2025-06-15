# Stat Commands

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:04

---

To profile their **Unreal Engine (UE)** projects, developers can enter the following **stat commands** into the console while running their game in **Play In Editor (PIE)** mode.

Click for full image.

To locate a stat command from the Editor's **Stat** menu, select the dropdown arrow next to the **Viewport Setting** button.

Click for full image.

Running the editor with the `LOG` command enables developers to record useful information from a stat **dump**, and to do so, enable the editor (game project) to generate a log file by running it with the `LOG` command (for example, `UnrealEditor.exe -silent LOG=MyLog.txt`).

## Stat Command Table

Type `stat` followed by a space and any of these commands to activate them:

| Command Name | Command Description |
| --- | --- |
| **AI** | Displays Perception System and Overall AI performance information. |
| **AI\_EQS** | Displays performance, debug, and memory statistics for the Environment Query System (EQS). |
| **AIBehaviorTree** | Displays performance and memory statistics for Behavior Tree. |
| **AICrowd** | Displays performance and step information for the Crowd Manager. |
| **Anim** | Shows how long skinned meshes are taking to compute per tick. |
| **AsyncLoad** / **AsyncLoadGameThread** | Displays Async loading performance statistics. |
| **Audio** / **AudioThreadCommands** | Audio statistics, such as wave instances or buffer performance. |
| **Canvas** | Canvas statistics, showing performance information for Canvas user interface items, such as tiles, borders, and text. |
| **Collision** / **CollisionTags** | Displays performance, debug, and memory information for collisions. |
| **CommandListMarkers** | Displays a list of commands with their performance information. |
| **Component** | Displays a list of components with their performance information. |
| **Compression** | Displays compression statistics. |
| **CPULoad** | Shows CPU utilization. |
| **CPUStalls** | Shows information about CPU stalls. |
| **D3D11RHI** | Displays Direct3D 11 RHI statistics. |
| **DDC** | Displays Derived Data Cache (DDC) statistics. |
| **DumpHitches** | Anytime a "hitch" is detected based on `t.HitchFrameTimeThreshold`, it will be written to the log. |
| **Dumpticks** | Dumps info about tick functions. |
| **Engine** | Shows general rendering stats like frame time as well as counters from the number of triangles being rendered. |
| **FPS** | Displays Frames per Second (FPS) counter. |
| **Game** | Gives feedback on how long the various Gameplay Ticks are taking. |
| **GameplayTags** | Displays Gameplay Tag information. |
| **GC** | Displays garbage collection statistics. |
| **GeometryCache** | Shows performance and memory statistics for the Geometry Cache system. |
| **GPU** | Displays GPU statistics for the frame. |
| **GPUParticles** | Displays performance information for GPU particles. |
| **Help** | Lists all stat commands. |
| **Hitches** | Set `t.HitchFrameTimeThreshold` to define the time in seconds that is considered a hitch. Will also dump all hitches to the log/visual studio debug, for example `[0327.87] LogEngine:Warning: HITCH @ 00m:01s:643ms,1643,72,2.` |
| **IMEWindows** | Displays information for the Windows Text Input Method System. |
| **InitViews** | Displays information on how long visibility culling took and how effective it was. Visible section count is the single most important stat with respect to rendering thread performance, and that is dominated by Visible Static Mesh Elements under STAT INITVIEWS; however, Visible Dynamic Primitives also factors in. |
| **KismetCompiler** | Displays Kismet Compiler information. |
| **KismetReinstancer** | Displays Kismet Reinstancer information. |
| **[Levels](/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine#levels)** | Displays Level Streaming information. |
| **LightRendering** | Gives feedback on how long lighting and shadows are taking to render. |
| **LinkerCount** | Displays Linker counter. |
| **LinkerLoad** | Displays Linker Load information. |
| **List**  | Display groups of statistics or saved sets or statistics within a specified group with usage `<Groups/Sets/Group>`. |
| **LLM** | Displays Low Level Memory Tracker (LLM) counters. |
| **LLMFull** | Displays full group of LLM counters. |
| **LLMOverhead** | Displays LLM overhead counters. |
| **LLMPlatform** | Displays LLM platform counters. |
| **LoadTime** / **LoadTimeVerbose** | Shows load time performance information. |
| **MapBuildData** | Displays the map's build data. |
| **MathVerbose** | Shows performance information of math operations. |
| **Memory** | Shows statistics on how much memory is being used by various subsystems in Unreal Engine. |
| **MemoryAllocator** | Shows memory allocation information. |
| **MemoryPlatform** | Shows memory platform information. |
| **MemoryStaticMesh** | Shows memory statistics about static meshes. |
| **NamedEvents** | Enables named events for external profilers. |
| **Navigation** | Shows performance and memory information for the navigation system. |
| **NET** | Displays networking system statistics. |
| **Object** / **ObjectVerbose** | Displays object memory and performance information. |
| **Online** | Shows online system counters. |
| **Pakfile** | Displays Pakfile system statistics. |
| **ParallelCommandListMarkers** | Displays a list of parallel commands with their performance information. |
| **Particles** | Shows particle system performance information. |
| **Physics** | Displays physics performance statistics. |
| **PhysXTasks** | Displays PhysX task information. |
| **PhysXVehicleManager** | Displays PhysX Vehicle Manager statistics. |
| **PlayerController** | Displays PlayerController performance information. |
| **Quick** | Quickly displays groups of overall performance data. |
| **RenderTargetPool** | Shows memory and performance statistics for Render Target Pool. |
| **RenderThreadCommands** | Lists render thread commands with performance information. |
| **RHI** | Displays RHI memory and performance statistics. |
| **RHICMDLIST** | Shows RHI command list with performance statistics. |
| **SceneMemory** | Shows scene memory counters. |
| **SceneRendering** | Shows general rendering statistics. This is a good starting point to find general areas of slow performance in the rendering process. |
| **SceneUpdate** | Displays information about updating the world, including the time taken to add, update, and remove lights as well as add and remove primitives in the scene. |
| **Script** | Shows script statistics. |
| **ShaderCompiling** | Displays shader compiling information. |
| **Shaders** | Shows shader compression statistics. |
| **ShadowRendering** | Shows how long shadow calculations are taking, separate from actual shadow render time which is covered in **stat LightRendering**. |
| **Slate** / **SlateVerbose** | Displays Slate performance statistics. |
| **SlateMemory** | Shows Slate memory counters. |
| **SoundCues** | Shows active SoundCues. |
| **SoundMixes** | Shows active SoundMixes. |
| **Sounds** | 
`<?> <sort=distance|class|name|waves|default> <-debug> <off>`   
Shows active SoundCues and SoundWaves.



 |
| **SoundWaves** | Shows active SoundWaves. |
| **SplitScreen** | Shows Split Screen information. |
| **[StartFile](/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine#startfile)** | 

Starts a statistics capture, creating a new file in the Profiling directory.

Stop this operation with the **stat StopFile** command.



 |
| **StatSystem** | Shows performance and memory information for the Stat System. |
| **[StopFile](/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine#stopfile)** | Finishes statistics capture that was started by the **stat StartFile** command, closing the file that was created in the Profiling directory. |
| **Streaming** | Displays basic statistics on streaming assets, like how much memory streaming textures are using, or how many streaming textures there are in the scene. |
| **StreamingDetails** | More detailed statistics on streaming, like breaking down general texture streaming into more specific groups (lightmaps, static textures, and dynamic textures). |
| **StreamingOverview** | Shows an overview of statistics on streaming assets. |
| **TargetPlatform** | Shows target platform information. |
| **TaskGraphTasks** | Shows performance data for TaskGraph tasks. |
| **Text** | Shows performance statistics for text. |
| **TextureGroup** | Displays texture group memory counters. |
| **Threading** | Displays threading information. |
| **ThreadPoolAsyncTasks** | Shows ThreadPool Async task counters. |
| **Threads** | Displays thread information. |
| **Tickables** | Shows performance statistics for Tickables. |
| **TickGroups** | Shows performance statistics for Tick groups. |
| **UI** | Shows UI performance information. |
| **[Unit](/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine#unit)** | 

Overall frame time as well as the game thread, rendering thread, and GPU times.

This is a great stat command to start with because it helps developers focus their profiling work.



 |
| **UnitGraph** | To see a graph with the stat unit data, use **stat Raw** to see the unfiltered data. |
| **UObjectHash** | Displays hashed UObject information. |
| **UObjects** | Shows performance statistics for UObjects in the game. |

## Select Commands

### Levels

The **stat levels** command displays level streaming information, which are grouped under the persistent level.

#### Use Case

This command is useful for developers wanting to view a list of currently active levels, including whether they are visible, pre-loading, loading, or unloading. Additionally, this command displays how many seconds it took to go from a load request to load finish.

#### Usage

To view streaming level information, enter `stat levels` into **PIE Console**. To determine what state a level is in, refer to the [Level Color Codes](/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine#levelcolorcodes) table below.

##### Level Color Codes

  

| Color Code | Description |
| --- | --- |
| **Green** | Level is loaded and visible. |
| **Red** | Level is unloaded. |
| **Orange** | Level is in the process of being made visible. |
| **Yellow** | Level is loaded but not visible. |
| **Blue** | Level is unloaded but still residing in memory, and it will be cleaned up when garbage collection occurs. |
| **Purple** | Level is pre-loading. |

### StartFile

Click for full image.

The **stat startfile** command starts a statistics capture, and creates a new file in a **Profiling** directory. Typically, the engine saves statistics captures under `<PROJECT_DIRECTORY>\Saved\Profiling\UnrealStats`.

#### Use Case

To profile a project's performance with **Session Frontend Profiler,** capture statistical samples and log them to `*.uestats` files.

#### Usage

To capture and log statistics to a `*.uestats` file, enter `stat startfile` into **PIE Console**.

To prevent `StartFile` from bloating the disk with large `uestats` files, run `stat StopFile`. Additionally, even if PIE Mode is closed, `StartFile` continues running in the background, which can result in bloated log files, so make sure to run the `StopFile` command to stop logging the project's performance.

#### Loading Statistics

To load statistics into **Session Frontend Profiler**:

1.  From the **Unreal Editor Menu Bar**, select **Tools > Session Frontend**.
2.  With **Session Frontend** open, select the **Profiler** tab.
3.  To open a file for profiling, select **Load**. A **File Explorer** winow will appear for you to select the `uestats` file you wish to open for profiling.
4.  After selecting a `uestats` file, click **Open** to load the file.

##### End Result

After **Session Frontend** loads the file, the capture data is visible in the **Profiler** for further analysis. Read the [Profiler Tool Reference](/documentation/en-us/unreal-engine/using-the-unreal-frontend-tool) to learn more about reviewing profile captures in **Session Frontend**.

### StopFile

Click for full image.

The **stat stopfile** command stops a statistics capture that was started by the **StartFile** command. Additionally, the **StopFile** command closes the file that was created in the `Profiling` directory.

#### Use Case

To prevent StartFile from bloating the disk with large `uestats` files, run stat **StopFile**. Additionally, even if PIE Mode is closed, StartFile will continue running in the background, which can result in bloated log files, so make sure to run the StopFile command to stop logging the project's performance.

#### Usage

To stop capturing and logging statistics, enter `stat stopfile` into **PIE Console**.

### Unit

#### Use Case

Typically, developers want to determine if a bottleneck (negative performance impact) exists in the **Game** thread, in the **Draw** (rendering) thread, or on the **GPU**. 

Click for full image.

The **stat unit** command displays performance information for the project's **Frame**, **Game**, **Draw**, **GPU**, **RHIT**, and **DynRes** threads.

#### Statistics

| Name | Description |
| --- | --- |
| **Frame** | Frame time is the total amount of time spent generating one frame of the game. Since both the Game and Draw threads sync up before finishing a frame, Frame time is often close to the time being shown in one of these threads. |
| **Game** | If Frame time is close to Game time, the game's performance is likely being bottlenecked (negatively impacted) by the game thread. |
| **Draw** | If Frame time is close to Draw time, the game's performance is likely being bottlenecked by the rendering thread |
| **GPU** | GPU time measures how long the video card takes to render the scene. Since GPU time is synced to the frame, it will likely be similar to Frame time. |
| **RHIT** | Typically, RHI Thread time is synced to the frame, and it will likely be similar to Frame time. |
| **DynRes** | 
If supported (and enabled), [Dynamic Resolution](/documentation/en-us/unreal-engine/dynamic-resolution-in-unreal-engine) shows Primary Screen Percentage by Secondary Screen Percentage.



 |

#### Usage

To determine the project's bottleneck, launch the game in a non-debug build, and enter `stat unit` into **PIE Console**.
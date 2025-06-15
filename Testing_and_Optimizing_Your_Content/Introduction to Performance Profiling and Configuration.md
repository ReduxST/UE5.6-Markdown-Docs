# Introduction to Performance Profiling and Configuration

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/introduction-to-performance-profiling-and-configuration-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/introduction-to-performance-profiling-and-configuration-in-unreal-engine)  
**Processed:** 2025-06-14 16:31:40

---

*Performance* describes how smoothly your project runs on your target hardware. Unreal Engine simulates real time by repeatedly drawing, or *rendering*, an image of the game world to your screen. Like a flipbook, the engine displays frames in rapid succession, creating the effect of motion. Performance of the frames being rendered can be measured in a couple of ways: by *Frames Per Second* and by looking at *Frame Time*. These can help you understand your application's performance to target a certain number of frames per second, and where time within those frames is being spent, which is measured in milliseconds.

The more frames you render within a second, the smoother the motion looks to the user, and the more responsive the application feels. Generally, applications will target 30, 60, and 120 frames per second when considering their performance budget and target hardware. To provide the best possible user experience, you want your framerate to be higher, but you also want it to be consistent. This document provides a primer of rendering performance considerations, as well as a walkthrough of several tools to analyze and manage your Unreal Engine application's rendering performance.

## Understanding Performance

A lot of logic in Unreal Engine depends on two things: 

-   What's happening in the current frame
    
-   How much time has passed since the previous frame
    

As a few examples, as a frame renders, the following things could occur:

-   The user might move a character or vehicle.
    
-   The user might interact with an object.
    
-   AI-controlled entities may move around or perform a variety of actions.
    
-   The user's UI might change.
    
-   An object onscreen may step forward in its animation, or possibly blend multiple animations together.
    
-   Physics simulations might change the position or rotation of physics objects.
    

Each of these operations adds extra work that your computer has to do while it draws each frame. Furthermore, you can make the process of drawing each frame more or less complex with a variety of rendering settings. Some possible adjustments include the following:

-   Increase the detail of objects and textures, which makes your computer spend longer calculating each related pixel’s final color.
    
-   Add postprocessing effects, which each add extra passes that must be run on the image at various stages of rendering.
    
-   Use higher-fidelity lighting and shading, which makes scenes look more realistic, but also increases the complexity of lighting calculations.
    

The more things you tell your application to do each frame, the longer it will take to render a single frame. If your frames take a particularly long time to render, it will slow your overall framerate down, making your application look less smooth and feel less responsive.

### Measuring Frames Per Second and Frame Time

To keep track of **Frames Per Second** and **Frame Time**, you can enable these measurements to show in the Viewport. In the viewport hamburger menu, enable **Show FPS**, click **Stat** > **Engine**, and enable **FPS** and **Unit**.

[![The hamburger viewport menu, with FPS and Unit enables.](https://dev.epicgames.com/community/api/documentation/image/edfa7949-9ef7-405f-986c-c6b4c1d81d19?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/edfa7949-9ef7-405f-986c-c6b4c1d81d19?resizing_type=fit)

[![The FPS and Unit measurements in the viewport.](https://dev.epicgames.com/community/api/documentation/image/4aeb1608-ebcb-4ada-a458-d807216827f5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4aeb1608-ebcb-4ada-a458-d807216827f5?resizing_type=fit)

### Hardware Limitations and Framerate Drops

A slow framerate is the product of too much processing occurring during a single frame, usually by operations that repeat themselves every time a frame draws onscreen. You can imagine each frame you're rendering as a train that you've scheduled to leave the station, followed by another train a few milliseconds later. With this train, however, all passengers who have purchased a ticket must board the train before it can leave. Each operation you do during that frame, whether it's gameplay or rendering logic, is like another passenger that has to get onboard. 

When you spend too much time processing during a single frame, it's like holding up the train because you're trying to board too many passengers, and they haven't all gotten on the train yet. This prevents the next train from being able to come in. The result onscreen is a *framerate drop*. These can occur momentarily, resulting in *hitches* where the screen noticeably hangs on a frame for a moment too long, or they can consistently occur each frame, resulting in an overall low framerate.

Any of the following computing resources can potentially cause a bottleneck:

-   **CPU**: The central processing unit (CPU) of your computer is doing too many operations on one or more threads during a single frame. This indicates that the UI, gameplay logic, or other core logic of your application are running inefficiently, or that you're performing too many of these operations during a single frame.
    
-   **GPU**: The graphics processing unit (GPU) of your computer is doing too many operations during a single frame. This indicates that your game's rendering or post-processing are running inefficiently, or that the GPU is otherwise tasked with too many operations to keep up with.
    

-   **Memory Size (RAM)**: Your computer's Random Access Memory (RAM) is full, preventing operations from being completed until it is cleared out. This tends to result in an out of memory exception and a crash rather than a performance hitch. Some systems like garbage collection or asset streaming are elastic, which dynamically delay clean-up work. When RAM fills up, such systems must perform clean-up and re-population operations more frequently, which add to the CPU workload.
    
-   **Memory Speed (RAM)**: CPUs operate on small chunks of data that are physically colocated with the cores, exchanging these chunks of data with the RAM as needed. These operations can occur much more quickly than the exchange of chunks between the CPU and RAM (for example, a CPU might be able to perform 20 manipulations of loaded data in the same amount of time it takes to load a new piece of data).  The slower the RAM is, and the more frequently the logic needs to switch between which contiguous chunk of memory it needs to interact with, the more time CPU cores will spend doing nothing, idling as they wait for the memory bus.
    
-   **GPU Memory (VRAM)**: Your GPU's RAM is full, preventing operations from being completed until it is cleared out. This usually results from overloading texture memory, as textures take up a large amount of space.
    
-   **Hard drive access**: Objects have to load from your hard drive or other storage device before they can be added to memory. If you have to access your storage device very frequently, it will prevent operations from completing.
    
-   **Network Bandwidth**: Your computer's internet connection is slow or unreliable, resulting in more CPU work each frame spent piecing together or re-sending reliable packets, in bursts of work that otherwise might have been spread across many frames, or simply in choppy visuals despite the lack of local performance bottlenecks.
    

### CPU-Bound vs. GPU-Bound

We describe applications as being bound by either the CPU or GPU depending on which one has the tighter margin for performance. If your CPU is more likely to cause bottlenecks, it's *CPU-bound*. If your GPU is more likely to cause bottlenecks, it's *GPU-bound*. If you have Vsync turned on, and both the CPU and GPU are capable of producing frames faster than the monitor is capable of displaying them, your application would be *display-bound*. Often this will depend on your target platform and its resources.

### Processing Spikes

A processing *spike* refers to a sudden, brief increase in the amount of time that either your CPU or GPU is spending during a frame.

### Expensive vs. Inexpensive Operations

In general terms, an *expensive* operation takes a relatively large amount of computing resources to execute. This could mean larger amounts of processing time, or larger amounts of memory. *Inexpensive* operations do not require a large amount of computing resources. These terms are often used to compare processes that do similar operations. 

### Memory in Realtime Applications

Anything that you can process or render exists in your application's memory, with some exceptions for things like virtual geometry in Nanite, which stream directly from a solid state hard drive (SSD). An easy way to think of it is that if you can see it and move it onscreen, a copy of it exists in your computer's memory, and the object's rendering resources, like textures, shaders, and meshes, exist in your GPU memory.

### Performance and Power Usage

Power usage varies depending on your hardware architecture, but in general, running a heavier processing load and rendering more frames per second both contribute to higher power consumption. In Mobile and HMI settings, the power consumption of your device is a major concern, therefore you are strongly incentivized to make your application run as efficiently as possible. Players may negatively rate games that use their phone battery faster than other games. Additionally, causing the phone to heat up by using more energy can activate thermal throttling, which forces the CPU to run more slowly until the phone cools back down again.

## Profiling Tools

Profiling is the act of analyzing your application's use of system resources, such as CPU or GPU processing, memory usage, or network bandwidth. Unreal Engine provides several sets of profiling tools:

|  |  |
| --- | --- |
| 
Tool

 | 

Description

 |
| 

Unreal Insights

 | 

Record and review performance data on a frame-by-frame basis.

 |
| 

Stat Commands

 | 

Display performance statistics onscreen.

 |

For information about using Unreal Insights with Android devices, see the [Unreal Insights on Android Devices](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-unreal-insights-to-profile-android-games-for-unreal-engine) page.  

You can also use a third-party tool for profiling, including the following:

|  |  |
| --- | --- |
| 
Tool

 | 

Description

 |
| 

[RenderDoc](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-renderdoc-with-unreal-engine)

 | 

Debug single-frame captures of your application's graphics.

 |
| 

[Perfetto](https://perfetto.dev/)

 | 

Create a full system profile and process trace data.

 |

Keep in mind that profiling uses the same CPU, RAM, and disk that the game is also using. Running your game with a profiler attached will cause it to have slightly worse performance. This can be a good thing, though, as it results in a scenario where appearing to hit your performance goals actually means you have surpassed them, leaving some free resources with which the game can remain on target in cases of unforeseen system variability.

### Unreal Insights

[Unreal Insights](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-unreal-insights-to-profile-android-games-for-unreal-engine) is a robust and powerful suite of profiling tools available in Unreal Engine, offering tools for profiling individual threads, memory usage, and network bandwidth. You can see how many milliseconds each individual operation takes on the CPU or GPU, how much memory is being allocated in Memory Insights, and a breakdown of telemetry and packet data in Network Insights. There are also specialized modes for profiling task graphs, context switches, and Slate UI elements, which can help you perform a in-depth analysis of your application's performance.

### Stat Commands

**Stats** refers to a series of console commands you can use within a running UE application to output statistics to the screen. There are stat commands for a wide variety of operations and systems, including but not limited to:

-   Memory tracking
    
-   GPU and CPU load
    
-   Gameplay ticks
    
-   UI
    
-   Animations
    

While using the Stat commands isn't as robust as working with Unreal Insights or RenderDoc, it is the quickest way to get data about what's happening in your application while you are running or testing it.

For an exhaustive list of Stat Commands, see the [Stat Commands](https://dev.epicgames.com/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine) page.

### RenderDoc

[RenderDoc](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-renderdoc-with-unreal-engine) is an open-source graphics debugger which can attach to UE and provide output of single-frame captures.  It can do many operations, including the following:

-   Inspecting textures, models, or shaders.
    
-   Showing individual draw events.
    
-   Providing a breakdown of your application's pipeline state at the moment you capture a frame.
    

While Unreal Insights can give you a general idea of what rendering operations are taking the largest amount of processing and memory resources, RenderDoc is more suited to getting a detailed diagnostic of rendering operations and spotting the exact places where bugs are occurring. For example, if you see rendering artifacts on your target device but not in Play-In-Editor, you can use RenderDoc to capture a frame on both, compare their data, and see what's happening differently between them that causes artifacts to appear.

## Performance Configuration Tools

Many instructions for adjusting your project's rendering and [scalability settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/scalability-in-unreal-engine) refer to *console commands* and *variables*. This section provides an introduction on how to use them and resources for understanding them in depth.

### Console Commands and Variables

The *console* is a command line inside Unreal Engine that you can use to change settings, run debug commands, and get information while the game is running. You can use console commands in Unreal Editor or in a Developer or Debug build of a packaged project by pressing the **tilde** (~) key. This brings up the command line and prompts you to type in your command.   

[![The command line in Unreal Engine](https://dev.epicgames.com/community/api/documentation/image/7953f959-c88b-446e-838c-9b980059f25d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7953f959-c88b-446e-838c-9b980059f25d?resizing_type=fit)

Commands in UE support a search/autocomplete feature, so you can type a partial command to narrow down a list of the possible commands you're looking for. For example, if you type Stat, a list of Stat Commands appears.

*Console Variables*, or *CVars*, are config variables that you can edit using console commands. You can directly change CVars in the console by typing the config path of the variable, then providing the value you want to set that variable to. For example:

Command Line

```code
`r.TemporalAA.Quality 0`
```

r.TemporalAA.Quality 0

Copy full snippet(1 line long)

The command above sets the `r.TemporalAA.Quality` CVar to 0, effectively deactivating temporal anti-aliasing. This makes edges of objects appear more rigid and pixelated.

See the following pages for more information about the console:

-   [Console Variables and Commands](https://dev.epicgames.com/documentation/en-us/unreal-engine/console-variables-cplusplus-in-unreal-engine) – An overview of how to work with the console in detail.
    
-   [Console Commands Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-console-commands-reference) – A full list of console commands.
    
-   [Console Variables Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-console-variables-reference) – A full list of console variables.
    
-   [Console Variables Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/console-variables-editor) – A plugin for editing console variables directly from Unreal Editor.
    

You can also use console commands in Blueprint and C++ to change variables at any time, even when the console is disabled in shipping builds. This can be useful for selectively scaling your settings while your application is running.

### Output Log

When working with the console in Unreal Editor, it will be easier to understand what's going on by displaying the Output Log, which contains a record of commands and logs.

To view the Output Log in Unreal Editor, click **Window** > **Output Log**. The Output Log will then dock at the bottom of your editor.

[![The Output Log](https://dev.epicgames.com/community/api/documentation/image/5959e8fb-b5fa-4c76-b8fb-bbaf602840e3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5959e8fb-b5fa-4c76-b8fb-bbaf602840e3?resizing_type=fit)

Saved log files appear in the `Saved/Logs` folder of your project.

### Config Files

Console Variables are stored in your config (`.ini`) files as key-value pairs, providing default settings for builds of your game. See [Configuration Files](https://dev.epicgames.com/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine) for more information.

### Device Profiles

Device Profiles are configuration files that contain settings for a specific device your project is targeting. This can be as broad as a large bucket of devices, such as `Android_Mid`, or as precise as individual pieces of hardware. Each device profile has a series of settings overrides that take effect only for that specific device.

Unreal Engine's device profiles mainly revolve around GPU families, such as the Adreno 7xx series, but you can add custom device profiles of your own and define rules for it as needed for your supported hardware. 

For more information, see [Customizing Device Profiles and Scalability on Android](https://dev.epicgames.com/documentation/en-us/unreal-engine/customizing-device-profiles-and-scalability-in-unreal-engine-projects-for-android).

## Further Reading

See [Common Performance Considerations](https://dev.epicgames.com/documentation/en-us/unreal-engine/common-memory-and-cpu-performance-considerations-in-unreal-engine) for more information about situations and factors that can affect your application's performance.

## Tips and Best Practices

### Test Early and Test Often

When testing, anticipate that your project will encounter bugs that are specific to each individual platform that you support. While Unreal Editor strives to provide an accurate preview, there is no substitute for profiling directly on your target hardware. The longer you go without testing on your hardware, the more likely that bugs will emerge that you are not aware of.
# Common Performance Considerations

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/common-memory-and-cpu-performance-considerations-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/common-memory-and-cpu-performance-considerations-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:21

---

Each section below outlines a situation that can impact your application's performance, and gives guidelines for alternative approaches and workarounds that can help deal with any issues you may be experiencing.

## Before You Proceed

If you are unfamiliar with performance profiling in Unreal Engine, we strongly recommend that you read [Introduction to Performance Profiling and Configuration](https://dev.epicgames.com/documentation/en-us/unreal-engine/introduction-to-performance-profiling-and-configuration-in-unreal-engine) to establish foundational knowledge in this topic before you continue reading the sections below.

## Managed Objects, Garbage Collection, and Processing Spikes

In Unreal Engine, **UObjects** and any classes derived from them (such as Actors and Data Assets) are *managed* by the engine's *garbage collector*. The garbage collector periodically cleans up UObjects that are deleted in the World, and cleans up any existing references to that object.

By comparison, standard C++ objects are *unmanaged*. This means that when you delete or null a copy of an object, you have to manually clean up references to it. This introduces risk if not handled carefully, as any gap in your cleanup logic can result in memory leaks (if objects aren't cleaned up) and invalid references (if objects are deleted but references linger).

Support for managed objects introduces some extra memory usage. UObjects carry additional metadata like an `FName` and an `Outer` reference which take up additional memory. The garbage collector has to run every so often to automatically clean up objects, so a back-end system has to be able to monitor all the places objects are being referenced. Processing spikes often occur during frames when the garbage collector runs, especially if your application has destroyed a large number of objects recently. 

You can configure garbage collection in **Project Settings** > **Engine** > **Garbage Collection**, including the interval of garbage collection, the maximum amount of objects it can clean up at any given time, and other settings for how garbage collection processes. While it is unlikely you need to fine-tune early in your project, this provides options for tailoring the way Unreal Engine's garbage collector behaves to your project's unique needs.

[![The project settings for engine garbage collection.](https://dev.epicgames.com/community/api/documentation/image/18f5df29-bc3b-4b40-995d-e177960539af?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/18f5df29-bc3b-4b40-995d-e177960539af?resizing_type=fit)

It is recommended that you rely on the automatic garbage collection. If necessary, you can also manually call the garbage collector using the **Collect Garbage** node in Blueprint, or the `UObjectGlobals::CollectGarbage` function in C++.

[![The Collect Garbage node](https://dev.epicgames.com/community/api/documentation/image/c7bfdceb-94d8-4523-aa9f-6a815de46906?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c7bfdceb-94d8-4523-aa9f-6a815de46906?resizing_type=fit)

This will cause a processing spike, but there might be times when calling garbage collection manually will save you from accumulating garbage in the background, causing a larger spike when it runs automatically later on. 

Manual garbage collection is appropriate in the following situations:

-   When the program is in a state where, from a UX perspective, frame spikes are more tolerable, such as during a loading screen. This reduces the chance occurring during a state where it would be more noticeable or intolerable.
    
-   Before an operation that allocates a lot of memory, if you discover while testing that the operation can cause out-of-memory crashes or page swapping hitches unless garbage collection is performed immediately beforehand.
    

## Creating and Destroying Objects vs. Object Pooling

To create an object, your computer must allocate a new block of memory to hold a copy of the object, then initialize it alongside any sub-objects that it requires. When destroying an object, you must delete that information, de-allocate it, and clear any references to that object that may exist elsewhere in your application's code.

Both of these operations can be fairly expensive, especially when their initialization involves coordination with other systems.  For the most part, Unreal Engine is efficient enough at handling these operations that you can use them safely in a lot of contexts on PC and consoles, but in projects with a limited margin for processing on the CPU, you may want to use *object pooling* instead. Object pooling is the act of creating all the copies of an object that you need upfront, allocating them in memory, and then keeping them disabled or hidden until they are needed. 

The more high-level an object is, the more expensive it will be to create and destroy. Pooling is more likely to be useful for Actors than it is for Components, and more likely to be useful for Components than it is for other UObjects. This is because the cost of creating an actor also entails inserting it into the World’s list of actors, creating its components, and registering itself and its components with additional infrastructure like rendering and physics. When it comes to C++ structures that don’t interact with additional classes upon creation and destruction, an attempt at pooling them may actually end up being less efficient than allowing the system allocator to recycle their raw memory.

As an example, think about a weapon that fires projectiles. It's fairly common for a weapon to spawn a projectile when it fires, then the projectile destroys itself when it impacts with another object.

With object pooling, instead of spawning a new projectile every time you need to fire one, your weapon would pre-spawn the maximum number of projectiles it could possibly have active at any given time, then hide and disable them. This group of disabled projectiles is the object pool. When your weapon fires a projectile, it would take the projectile out of the pool, move it to the end of the weapon, un-hide and enable it, and initialize it in the proper direction. Then, when the projectile impacts a target, it would hide and disable itself and return itself to the pool to be re-used again later.

[![](https://dev.epicgames.com/community/api/documentation/image/d4c1d170-107c-4f5a-8745-1ab45a45714b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d4c1d170-107c-4f5a-8745-1ab45a45714b?resizing_type=fit)

The benefit of object pools is that you don't need to create or destroy objects, which saves a great deal of processing time spent initializing and cleaning them up. The trade-off is that they use up memory that would otherwise be unoccupied, even when objects in the pool are inactive. However, in many situations you would need to leave room for the maximum number of objects the pool needs anyway. Additionally, the memory for these objects also remains more stable since you allocate and clean it up in large chunks rather than smaller ones, reducing the possibility of *memory fragmentation*.

## On-Tick Logic vs. Callbacks, Timers, and Scheduled Logic

The Tick event in tickable UObjects and Actors provides a way to create logic that repeats every frame. This is useful for handling realtime movement. However, using Tick for routines that are occasional rather than continuous can result in wasteful CPU usage.

In particular, it is often suboptimal to use logic that checks if a variable has changed on each frame, such as in the following example. One class uses Tick to repeatedly check to see when another class's variable changes.

C++

AMyActor class

```code
`UCLASS() class AMyActor : public AActor { 	GENERATED_BODY() public: 	//Set this reference in the details panel. 	UPROPERTY(BlueprintReadOnly, EditAnywhere) 	AChildActor* ChildActor;  protected:`

```

Expand codeCopy full snippet(23 lines long)

C++

AChildActor class

```code
`UCLASS() class AChildActor : public AActor { 	GENERATED_BODY() public: int32 getMyInt(){ 	return MyInt; } private: 	int32 myInt = 0;`

```

Expand codeCopy full snippet(11 lines long)

Instead of using tick to monitor the value, you can create a custom setter function to wrap around the operation to change the variable, then call another function or event that performs the needed logic only when you change that value.

The following example includes the classes from the last example, but now uses a callback to perform an action only when a variable has changed:

C++

AMyActor class

```code
`UCLASS() class AMyActor : public AActor { 	GENERATED_BODY()  public: 	void OnChildIntChanged(int32 NewValue) { 		if (newValue > 3) 		{`

```

Expand codeCopy full snippet(20 lines long)

C++

AChildActor class

```code
`UCLASS() class AChildActor : public AActor { 	GENERATED_BODY()  public: 	//Set this reference in the details panel. 	UPROPERTY(BlueprintReadOnly, EditAnywhere) 	AMyActor* ParentActor;`


```

Expand codeCopy full snippet(24 lines long)

This ensures that the logic only runs when your variable changes instead of querying a value each frame.

However, the event-driven approach can be less optimal depending on how often the condition changes. If an event is fired multiple times per frame, or if a function is attached to many events which might all change on the same frame, then it can be more efficient to use **Tick**, or to use the "command pattern". This avoids calculating results that just end up being overwritten before they are rendered.

When you want to schedule an event to occur after a set period of time, you can start a **Timer**, which will temporarily track the time elapsed until it is finished, then clean itself up. Alternatively, you can use the **Delay** node in a Blueprint Event graph.

If you need logic to reoccur frequently, but don't need it to occur every frame, consider making it occur on a certain interval of frames or seconds. You can do this in individual objects and Actor components by setting their tick interval to a certain number of seconds. Alternatively, you can create intervals for subsets of the logic in your **Tick** function. While you still need to accumulate and reset a variable to do this, it's still cheaper than running the logic on every frame.

## Asynchronous vs. Synchronous Logic

*Synchronous* logic refers to completing actions from beginning to end, in sequence. Most logic that you write in Blueprint or C++ will be synchronous by default. For instance, if you create an event in Blueprint, but don't add any Delay nodes, timers, or gameplay tasks, all the logic stemming from that Blueprint event will execute at once on the same frame. The frame can't finish processing until that logic finishes executing. When you are running extensive operations, especially on large data sets or large objects that must load or unload from memory, this can introduce significant processing spikes.

*Asynchronous* logic refers to completing actions in parallel, either literally at the same time (on separate CPU cores), or logically at the same time (interlaced into smaller chunks that are technically executed synchronously at a low level). An asynchronous operation runs until it is complete, while the main program continues running without waiting for the operation to catch up. Typically, asynchronous operations use callbacks to signal when they are completed.

Several frameworks within Unreal Engine, such as the World Partition system and various on-demand content delivery systems, are already asynchronous. For your own projects, consider implementing asynchronous logic to distribute operations over a period of time so as to avoid putting too much weight on a single operation or frame. 

As an example, you might need to load and instantiate a large number of enemies – say, 30 or more – in a wave-based defense game. Because creating a new Actor at runtime is already expensive, trying to process all of them on the same frame is very cumbersome. Instead, you could create an async operation to spawn only up to 5 enemies per frame until it has reached the specified limit or exhausted all of the specified spawn-locations This would result in all 30 enemies spawning over the course of 6 frames, at which point you would signal that the mass spawning operation is completed. While this dramatically eases the workload of spawning so many enemies, most players won't notice the duration over which spawning occurred, as it happens over a tenth or a fifth of a second.

## Parallel Processing in Unreal Engine

Parallel processing is a type of asynchronous processing where actions are processed on the same computer but in different threads or CPU cores. Some examples of parallel processing in Unreal Engine include:

-   Resolving soft pointers.
    
-   Loading levels and assets in the background.
    
-   Asynchronously loading assets from an online content delivery system.
    

A *thread* is a dedicated path for processing instructions, either on your CPU or your GPU. Most CPUs have multiple *cores*, which are themselves individual processors, and each core can have multiple threads. Taking advantage of parallel processing is key in ensuring that a program does not bottleneck on CPU processes, especially as it handles more complex tasks and larger amounts of data.

### Notable Processing Threads

Unreal Engine has dedicated threads for the following:

| Thread Name | Description |
| --- | --- |
| 
Game

 | 

Handles UObject and Actor logic in C++ and Blueprint, as well as UI logic. Most programming you do will occur on this thread.

 |
| 

Rendering

 | 

Converts scene structure into draw commands.

 |
| 

RHI

 | 

Sends draw commands to the GPU.

 |
| 

Task Pools

 | 

Handles various tasks in reusable threads.

 |
| 

Audio

 | 

Processing for sound and music.

 |
| 

Loading

 | 

Handles loading and unloading of data.

 |

You can see these threads in Unreal Insights' **Timing Insights** window. 

Because the game thread handles a large amount of logic, it is important to profile and optimize your code carefully.

### Creating Your Own Threaded Logic

UE has several resources for adding your own parallel processing logic:

-   [Tasks System](https://dev.epicgames.com/documentation/en-us/unreal-engine/tasks-systems-in-unreal-engine) provides a robust and relatively lightweight framework for dividing up logic into tasks that can be executed in parallel on separate threads.
    
-   [FRunnable](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Core/HAL/FRunnable?application_version=5.5) provides the most direct, low-level interface for executing a function on an arbitrary thread. This should be avoided unless you know what you’re doing, and have justification for using a dedicated thread instead of the thread pool.
    

Use caution when creating your own threaded logic, as it can result in *race conditions*, where errors occur if operations happen in an unexpected order.  

Additionally, the [Threaded Rendering](https://dev.epicgames.com/documentation/en-us/unreal-engine/threaded-rendering-in-unreal-engine) page provides insight into rendering-specific threaded logic.

## Shader Compilation, Framerate Hitches, and PSO Caching

Unreal Engine compiles material instructions into shaders to prepare them for execution on the GPU. While materials' overall performance improves significantly once compilation is finished, the act of compiling shaders can result in significant processing spikes, which in turn causes momentary but noticeable framerate hitches.

To counteract this, UE implements **PSO caching**. You can either [gather PSOs manually](https://dev.epicgames.com/documentation/en-us/unreal-engine/manually-creating-bundled-pso-caches-in-unreal-engine) by playing and testing your application, or use [PSO precaching](https://dev.epicgames.com/documentation/en-us/unreal-engine/pso-precaching-for-unreal-engine) to automatically generate them. In either case, the idea is to make a recording of every possible state that your graphics card will render when the application is running, then cache that data and bundle it up to use in subsequent builds. This dramatically reduces the amount of shader compilation that has to happen at runtime, as you can load most of them in advance instead, and therefore reduces the amount of hitching users experience when loading new areas and materials.
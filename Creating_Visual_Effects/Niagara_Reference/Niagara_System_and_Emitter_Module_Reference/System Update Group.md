# System Update Group

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/system-update-group-reference-for-niagara-effects-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/system-update-group-reference-for-niagara-effects-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:26

---

**System Update** modules are called in every frame, per system. Modules in this section should update new values for this frame. Modules are executed in order from the top to the bottom of the stack.

Each of the module types in the System Update group has its own section in this document, with tables that describe how that module functions. Keep in mind that you can create custom modules for any part of a Niagara system or emitter. The ones listed here are just the ones that are automatically included with Unreal Engine 4.

## System State Module

Below is a table describing the various parameters that can be set for the System State module.

| Parameter | Description |
| --- | --- |
| **Inactive Response** | 
This setting determines what happens when the emitter enters the Inactive state. Inactive means the emitter is dormant and no longer able to spawn or manage particles. Options are:

-   **Complete**: Emitters will finish, then the system is killed.
-   **Kill**: System and emitters are both killed immediately.



 |
| **Loop Behavior** | This setting indicates how many times the loop repeats. |
| **Loop Duration** | This setting establishes the duration of the life cycle. It can be initialized with a random number, but by default the initial duration value persists as the duration of all the following loop iterations. |
| **Recalculate Duration Each Loop** | Check this box if you want to calculate a new duration for each loop iteration. |
| **Loop Delay** | If you want to delay the loop, check this box and enter a value for how long the loop lasts. |
|   |   |

## New Scratch Pad Module

Selecting this item in the **Add** (Plus sign) menu opens the **Scratch Pad** panel (by default this docks next to the **System Overview**) and places a **Scratch Pad module** in the **Selection** panel. You can also open the Scratch Pad panel by using **Windows > Scratch Pad**. However, by placing a Scratch Pad module in the stack, any modules or dynamic inputs you create in the Scratch Pad are automatically connected to your script. If you open the Scratch Pad panel using the Windows menu, any items you create there will have to be added to your script manually.

## Set New or Existing Value Directly

Selecting this item from the **Add** (Plus sign icon) menu places a **Set Parameter** module in the **Selection** panel. Click the **Plus sign** (**+**) icon to select **Add Parameter** or **Create New Parameter**.

### Add Parameter

When you select **Set Specific Parameter**, you select from the parameters listed. This adds a **Set Parameter** module to the System Update group.

Some of these parameters can be set or modified in other modules. Some are only set using a Set Variable module.

| Parameter | Description |
| --- | --- |
| **System.Age** | This parameter defines the age of the named system. |
| **System.CurrentLoopDelay** | This parameter defines the current amount of delay before the named system's current loop repeats. |
| **System.CurrentLoopDuration** | This parameter defines the duration of the named system's loop. |
| **System.ExecutionState** | 
This affects the state of the system. Valid value choices are:

-   Active
-   Inactive
-   InactiveClear
-   Complete



 |
| **System.ExecutionStateSource** | This indicates the source of an execution state setting. It is used to allow scalability to change the state, but only if the state has not been defined by something with higher precedence. |
| **System.LocalSpace** | 

This parameter defines whether the position of particles is respective to the world origin or the owning Niagara Component's location. Settings are:

-   **False**: Particle position is in WorldSpace and will be relative to the World origin. A particle with position **0,0,0** will render at the World origin.
-   **True**: Particle position is in LocalSpace and will be relative to the owning Niagara Component's location. A particle with position **0,0,0** will render at the owning Niagara Component's location.



 |
| **System.LoopCount** | This parameter defines how many times the system's loop repeats. |
| **System.LoopedAge** | This parameter calculates the age of the system relative to its current loop. For example, if a system has been active for **8** seconds and it loops every **5** seconds, the system's LoopedAge will be **3** seconds. LoopedAge returns to 0 every time a system loops. |
| **System.NormalizedLoopAge** | This parameter calculates the age of the system relative to its current loop, normalized from **0** to **1**. NormalizedLoopAge is expressed as **LoopedAge** divided by **CurrentLoopDuration**. If a system has been active for **8** seconds and it loops every **5** seconds, the system's LoopedAge will be **3**. The system's NormalizedLoopAge will be **0.6**. |
| **System.ExecutionState** | 

This affects the state of the system. Valid value choices are:

-   **Active**
-   **Inactive**
-   **InactiveClear**
-   **Complete**



 |
| **System.ExecutionStateSource** | This variable is linked to the ENiagaraExecutionStateSource parameter, which indicates the source of a system execution state setting. It is used to allow scalability to change the state, but only if the state has not been defined by something with higher precedence. |
|   |   |

### Create New Parameter

When you select **Create New Parameter**, you select from the parameters listed. This adds a **Set Parameter** module to the System Update section.

| Parameter | Type | Description |
| --- | --- | --- |
| **Audio Oscilloscope** | **Data interface** | This adds a new Audio Oscilloscope data interface module to the emitter. The Audio Oscilloscope module can directly access the waveform data of the audio signal. |
| **Audio Spectrum** | **Data interface** | This adds a new Audio Spectrum data interface module to the emitter. The Audio Spectrum module can drive a visualization based on how loud the audio is at specific frequencies. |
| **Bool** | **Primitive** | This adds a Set Variable module that has a true/false checkbox. |
| **Camera Query** | **Data Interface** | This adds a new Camera Query data interface module to the emitter. This data interface can be used to retrieve camera information (camera position, rotation, FOV, etc) for the specified controller index. |
| **ENiagaraBooleanLogicOps** | **Enum** | 
This is an enumeration used by various modules and dynamic inputs that want to test using boolean logic:

-   **Greater Than**
-   **Greater Than Or Equal To**
-   **Equal To**
-   **Not Equal To**



 |
| **ENiagaraCoordinateSpace** | **Enum** | 

This is an enumeration used by various modules and dynamic inputs to distinguish between coordinate spaces:

-   **Simulation**: If the emitter is set to Local, use Local. Otherwise, use World.
-   **World**: In the world space of the game.
-   **Local**: In the coordinate space of the owning component.



 |
| **ENiagaraExecutionState** | **Enum** | This enumeration type is used by parameters that manage system or emitter execution states, such as **Emitter.ExecutionState** or **System.ExecutionState**. |
| **ENiagaraExecutionStateSource** | **Enum** | This indicates the source of an execution state setting. It is used to allow scalability to change the state, but only if the state has not been defined by something with higher precedence. |
| **ENiagaraExpansionMode** | **Enum** | 

This enumeration is used by location modules to determine where the origin point of expansion is:

-   **Inside**
-   **Centered**
-   **Outside**



 |
| **ENiagaraOrientationAxis** | **Enum** | 

This is an enumeration used by several modules to determine which axis to do calculations with:

-   **X Axis**
-   **Y Axis**
-   **Z Axis**



 |
| **ENiagaraRandomnessMode** | **Enum** | 

This enumeration is used by location modules to determine where the origin point of expansion is:

-   **Inside**
-   **Centered**
-   **Outside**



 |
| **Float** | **Primitive** | This creates a float value variable. |
| **Grid2D Collection** | **Data Interface** | This is used with simulation stages. It enables the user to read or write to a 2D array of data, and then iterate over each pixel in the grid during a simulation stage. |
| **Int32** | **Primitive** | This creates an integer variable. |
| **Linear Color** | **Primitive** | This creates an RGBA color variable, represented as a color picker. |
| **Matrix** | **Primitive** | This creates a 4x4 matrix variable. |
| **Mesh Tri Coordinate** | **Struct** | This is a simple struct containing a triangle index along with a barycentric coordinate on the face of that triangle. |
| **Neighbor Grid 3D** | **Data Interface** | This is used with simulation stages. It enables the user to read or write to a 3D array of data, and then iterate over each pixel in the volume during a simulation stage. |
| **Niagara ID** | **Struct** | This is a two-part struct used to track particles. It allows fast access to this particle's data. It is always unique among currently living particles, but will be reused after the particle dies. **AcquireTag** is a unique tag for when this ID was acquired. It allows us to differentiate between particles when one dies and another particle reuses the dead particle's index. |
| **Occlusion Query** | **Data Interface** | 

This adds a new Occlusion Query data interface module to the emitter. The data interface is used to read depth buffer occlusion information.

This can only be used with GPU emitters.

 |
| **Quat** | **Primitive** | This creates a quaternion variable, used to represent rotations. |
| **Simple Counter** | **Data Interface** | 

This adds a new Simple Counter data interface module to the emitter. This data interface enables you to increment a thread-safe counter.

This can only be used with CPU emitters.

 |
| **Particle Attribute Reader** | **Data Interface** | This adds a new Particle Attribute Reader data interface to the emitter. The data interface can be used to query particle payload values from other emitters, and can sometimes be easier to use than Events. |
| **Spawn Info** | **Struct** | This is a structure used in spawning to specify the **Count** of particles to create, **InterpStartDt** or offset from the current frame begin time to start spawning, **IntervalDt** defining the time gap between particles being spawned, and **SpawnGroup** allowing spawned particles to belong to different categories. |
| **Vector** | **Primitive** | This creates a three-channel set of floats. |
| **Vector 2D** | **Primitive** | This creates a two-channel set of floats. |
| **Vector 4** | **Primitive** | This creates a four-channel set of floats. |
| **Vector Field** | **Data Interface** | This is a data interface with functions to query a vector field. |
| **Volume Texture Sample** | **Data Interface** | This adds a new Volume Texture data interface module to the emitter. You can use this to sample a volume texture. |
|   |   |   |
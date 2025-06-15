# System Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/system-settings-reference-for-niagara-effects-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/system-settings-reference-for-niagara-effects-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:22

---

The System Settings group contains **User Parameters**, and **System Properties**.

## User Parameters

User Parameters can only be set from outside the Niagara simulation, such as from Blueprint logic or C++ code. This section displays User Parameters that have been created.

## System Properties Item

By default, the **System Properties** item is included in every created system, even if you create an empty one. The System Properties item contains the following base parameters.

| Parameter | Description |
| --- | --- |
| Debug |   |
| **Dump Debug System Info** | This checkbox indicates whether the debug information for the System is written to the log each frame. This is useful for tracking down really strange behavior but is very verbose. |
| **Dump Debug Emitter Info** | This checkbox indicates whether the debug information for the Emitter is written to the log each frame. This is useful for tracking down really strange behavior but is very verbose. |
| System |   |
| **Effect Type** | Click the dropdown to select an Effect Type to apply to the system. Effect Types are a useful way of organizing settings for a class of visual effects. For example, you might want to control the scalability settings for all Weapon Impacts, and those settings can be stored in a Weapon Impact Effect Type asset. |
| **Scalability Overrides** | 
This is where you can set overrides related to performance on different platforms.

These are overrides of the defaults specified in the Effect Type above.

 |
| **Fixed Bounds** | This checkbox enables or disables fixed bounds. If this is enabled, you can set the minimum and maximum fixed bounds for the entire system. It is also possible to set fixed bounds for individual emitters in their Emitter Properties item. |
| Performance |   |
| **Auto Deactivate** | This checkbox enables or disables automatic deactivation of emitters in the system. If enabled, it will deactivate the system if all the emitters in the system are not spawning particles, regardless of particle lifetime settings. |
| **Max Pool Size** | This value is the maximum number of components of this system that are kept resident in the world component pool. |
| Warmup |   |
| **Warmup Time** | 

This is the system warmup time in seconds. This value is used to calculate the Warmup Tick Count setting, if Warmup Tick Count is not set manually. It rounds down to the nearest multiple of the Warmup Tick Delta value.

Be careful using this, because it can lead to hitches.

 |
| **Warmup Tick Count** | 

This is the number of ticks to process for warmup. You can set this manually, or have it set by using the Warmup Time setting.

Be careful using this, because it can lead to hitches.

 |
| **Warmup Tick Delta** | This is the delta time to use for Warmup Ticks. |
| Asset Options |   |
| **Expose to Library** | If this setting is enabled, this system is exposed to the library. This means that by default it will show up in the menu when you add a module. |
| **Is Template Asset** | If this setting is enabled, it indicates that this system is a template that is exposed in the new System Wizard. Assets created from templates will not inherit from a parent Emitter, so these assets start without any inheritance connections. |
| **Template Asset Description** | This is the description displayed next to the System or Emitter in the new System Wizard. |
| Emitter |   |
| **Bake Out Rapid Iteration** | This checkbox enables or disables baking rapid iteration parameters into a normal compile. Making this change can improve performance, but will make iterating on the asset significantly more difficult. |
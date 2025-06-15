# Emitter Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/emitter-settings-reference-for-niagara-effects-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/emitter-settings-reference-for-niagara-effects-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:57

---

## Emitter Properties Item

![Emitter Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/148b0331-5037-466c-ac4a-45c543f1d110/01-emitter-properties-item.png)

By default, the **Emitter Properties** item is included in every created emitter, even if you create an empty one. The Emitter Properties item contains the following base parameters.

| Parameter | Description |
| --- | --- |
| Emitter |   |
| **Local Space** | This setting toggles whether the particles within this emitter are relative to this emitter or to the global space. |
| **Determinism** | This setting toggles whether the random number generator (RNG) will be deterministic or non-deterministic globally. Any random calculation that is set to the emitter defaults will inherit this setting. You can still set individual random numbers to be deterministic or non-deterministic. In this case, deterministic means that the RNG will return results for the same configuration of the emitter, as long as the delta time is not variable. Any changes to the emitter's individual scripts will adjust the results. |
| **Random Seed** | If the **Determinism** setting is enabled, this is an emitter-based seed for the deterministic random number generator. |
| **Sim Target** | This determines whether the simulation is performed on the CPU or the GPU. |
| **Fixed Bounds** | This setting determines whether the fixed bounds can be edited. If it is enabled, there are Minimum and Maximum X, Y, and Z settings that can be adjusted. |
| **Interpolated Spawning** | When this setting is enabled, this emitter will spawn using interpolated parameter values, and it will perform a partial update at spawn time. This has a significant additional cost for spawning, but it will produce much smoother spawning for high spawn rates, erratic frame rates, and fast moving emitters. |
| **Requires Persistent ID** | When this is enabled, all particles emitted will be assigned a persistent ID. |
| **Combine Event Spawn** | This setting allows event based spawning to be combined into a single spawn. |
| Scalability |   |
| 
![Scalability Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3eb00bc9-78d9-42c4-8c6c-c388b6af535e/02-scalability-settings.png)

For Scalability, there are five general settings: **Low**, **Medium**, **High**, **Epic**, and **Cinematic**. You can click to enable or disable a category for a particular emitter. Each category also has a dropdown menu listing various platforms that can display graphics at a particular level. You can include or exclude specific platforms in a category, instead of just enabling or disabling that category.

Consoles and some mobile platforms will not be displayed unless you set up the appropriate configuration and device profiles.

 |   |
| **Setting** | **Platforms to Include or Exclude** |
| **Low** | 

-   Windows
-   Mac
-   Linux
-   Android



 |
| **Medium** | 

-   Windows
-   iOS
-   Mac
-   Linux
-   Android



 |
| **High** | 

-   Windows
-   Mac
-   Linux



 |
| **Epic** | 

-   Windows
-   TVOS
-   Mac
-   Linux



 |
| **Cinematic** | 

-   Windows
-   Mac
-   Linux



 |
| Asset Options |   |
| 

![Asset Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b84194e4-585a-45f7-8db9-9aaa5f73ca28/03-asset-options.png)

 |   |
| **Library Visibility** | This setting allows you to change if this emitter is exposed to the library , or should be explicitly hidden. |
| **Template Specification** | This setting toggles whether this emitter is a standart parent emitter, a template or a behaviour example. |
| **Template Asset Description** | If you identify this emitter as a Template Asset, you can click the icon on the right to find additional settings for **Inline Text** and **Referenced Text**. |
| **Category** | You can add the category to collate this emitter into for 'add new emotter dialogs'. |
|   |   |
# Dynamic Resolution

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dynamic-resolution-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dynamic-resolution-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:26

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f80e53c-63e3-4e22-9a3a-4210a6c86d6d/dynamicres_fn1.png "DynamicRes_FN1.png")

**Dynamic Resolution** adjusts the primary screen percentage according to the previous frames' GPU workload. The resolution adjusts (as needed) based on a heuristic, for example, when there are too many objects on the screen, or if there is an expensive effect that suddenly enters the frame. The GPU rendering time will increase, and the resolution of the screen will be lowered to maintain the targeted frame rate.

## Enabling Dynamic Resolution

### Enabling Dynamic Resolution At Runtime

Dynamic Resolution can be enabled by getting a boolean on the **Game User Settings** node. It can be set when using either Blueprint or C++.

In **Blueprint**, enable dynamic resolution by using the **Game User Settings** node to opt into the feature like so:

![The Game User Settings node in Blueprint provides access to Dynamic Resolution settings.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7be9998-cc98-42c8-8c75-c7ecc7de8afd/dynamicresblueprint.png)

In **C++**, the boolean value can be set in *UGameUserSettings* like so:

```
	`GEngine->GetDynamicResolutionStatus()->SetEnabled(true);`

Copy full snippet
```
GEngine->GetDynamicResolutionStatus()->SetEnabled(true);

Use **false** for *SetEnabled* to disable it.

Game thread logic has the final programmatic control over when to actually enable or disable dynamic resolution, so if it's enabled at runtime using Blueprint that will take precedent over setting it in code. To restore game user settings to its original state, use the following:

```
	`GEngine->GameUserSettings->ApplyNonResolutionSettings();`
Copy full snippet
```
GEngine->GameUserSettings->ApplyNonResolutionSettings();

### Controlling Dynamic Resolution With Operation Mode

You can use **Operation Mode** to set how Dynamic Resolution can be overridden and used in your game. To control this, in your project's per-platform configuration profile (or device profile) for your platform (Xbox One, PlayStation 4, etc), you can use the following console command:

```
	`r.DynamicRes.OperationMode`

Copy full snippet
```
r.DynamicRes.OperationMode

Use one of the following values to set how the Operation Mode works for your project's platform:

-   **1** enables Dynamic Resolution based on the Game User Settings state (set in C++ or in Blueprint).
-   **2** enables Dynamic Resolution regardless of the Game User Settings state.

After enabling Dynamic Resolution, the following console variables set the minimum and maximum screen percentages, and the maximum budget of any given frame before it lowers the resolution. There are default values that are in place until you do set them:

| Console Variable | Default Value | Description |
| --- | --- | --- |
| **r.DynamicRes.MinScreenPercentage** | 50 | Sets the minimum screen percentage to use. |
| **r.DynamicRes.MaxScreenPercentage** | 100 | Sets the maximum primary screen percentage that is used to allocate render targets. |
| **r.DynamicRes.FrameTimeBudget** | 33.3 | Sets the budget of the frame (in milliseconds). |

You can use the Device Profiles window in Unreal Engine to set up the configuration files and manage them for you. You can access this window through the file menu by selecting **Edit > Developer Tools > Device Profiles**.

### Pausing and Resuming Dynamic Resolution

At times, you may need dynamic resolution enabled for project but not in areas like the main lobby. Dynamic resolution can be paused and resumed alongside Operation Mode. The following console variable can be used to set the Operation Mode of Dynamic Resolution:

```
	`r.DynamicRes.OperationMode`

Copy full snippet
```
r.DynamicRes.OperationMode

| Value | Description |
| --- | --- |
| **0** | Disabled (Default) |
| **1** | Enabled based on the setting used in GameUserSettings. |
| **2** | Enabled regardless of the setting used by GameUserSettings. |

The table below outlines the different states that are available when a specific operation mode is enabled or disabled and how GameUserSettings is affected:

|   | Game User Settings = False |   | Game User Settings = True |   |
| --- | --- | --- | --- | --- |
|   | **Paused** | **Not Paused** | **Paused** | **Not Paused** |
| **OperationMode=0** | No | No | No | No |
| **OperationMode=1** | No | No | No | Yes |
| **OperationMode=2** | No | Yes | No | Yes |

In **C++**, you can use the following functions to control and check the status of dynamic resolution:

| Action | C++ Function |
| --- | --- |
| **Pause** | GEngine->PauseDynamicResolution(); |
| **Resume** | GEngine->ResumeDynamicResolution(); |
| **Check Status (Disabled/Enabled or Paused)** | GEngine->GetDynamicResolutionStatus(); |

In Blueprint, the functionality provided by the C++ functions in this table for **Pause** and **Resume** can be achieved by enabling or disabling the node **Set Dynamic Resolution Enabled**. To check the status, use the node **Is Dynamic Resolution Enabled**.

## Using Stats for Dynamic Resolution

There are several stat screens that you can enable to debug performance with Dynamic Resolution. You can enable them by opening the console using the backtick ( **\`** ) key and entering one of the following commands:

-   **Stat Unit** is used to look at the overall frame time as well as the game thread, rendering thread, and GPU times.
-   **Stat UnitGraph** is used to see a graph with the Stat Unit data.
-   **Stat Raw** outputs unfiltered data using Stat UnitGraph.

### Stat Unit

When **Stat Unit** is called, you can immediately see if dynamic resolution is enabled for your scene by referencing the **DynRes** line.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddf15417-6087-4644-8c35-59cea4dc2eee/dynresoff.png "DynResOFF.png")

Once enabled, **DynRes** label will show the [Primary Screen Percentage](/documentation/en-us/unreal-engine/screen-percentage-with-temporal-upscale-in-unreal-engine) and the [Secondary Screen Percentage](/documentation/en-us/unreal-engine/screen-percentage-with-temporal-upscale-in-unreal-engine#secondaryspatialupscale) :

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9abc5d6e-77ec-4055-adb5-fad042349c5c/dynreson.png "DynResON.png")

The primary screen percentage is displayed here for the X and Y so that you don't forget that it is scaled on both axes. The number of pixels drawn by the GPU is actually proportional to **Screen Percentage x Screen Percentage**.

An example would be 1920x1080 or 1280x720.

### Stat UnitGraph and Stat Raw

When **Stat UnitGraph** is called, a graph will be drawn to show the [Primary Screen Percentage](/documentation/en-us/unreal-engine/screen-percentage-with-temporal-upscale-in-unreal-engine) chosen by dynamic resolution.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1eba3a58-ddbd-4e13-8e3e-21900be99906/statunitgraph.png "StatUnitGraph.png")

1.  Timings (Filtered or Raw)
2.  Target Frame Time Threshold
3.  Dynamic Resolution Max Screen Percentage
4.  Dynamic Primary Screen Percentage Curve

The UnitGraph can show the primary screen percentage that is chosen by Dynamic Resolution. However, that curve is proportional to the amount of pixels drawn by the GPU using Screen Percentage x Screen Percentage.

Additionally, you can get unfiltered (raw) timings in the UnitGraph by using **Stat Raw** to toggle between filtered and unfiltered. The timings label of the graph will change to indicate that it's displaying raw timings.

Raw Timings

Filtered Timings

Toggle between filtered and unfiltered timings by using the console window. Before **Stat Raw** can toggled, **Stat UnitGraph** must first be entered.

## Dynamic Resolution Cruising

The implementation of Dynamic Resolution in Unreal Engine is a little different than others that have been used before because we allow for the resolution to change as needed within a given range rather than being constrained to a single resolution (1080p, 900p, 720p). In this example graph, this model demonstrates what the console variables control. It demonstrates how dynamic resolution automatically adjusts within a given range (3) when everything is running fine and not over budget for the given frame. Think of this range as the cruising altitude for an airplane where it can move freely around this altitude range for an ideal speed to get to its destination. Like the airplane, the resolution does the same thing by going up and down as need to maintain a good balance of resolution and adequate performance.

This model is for demonstration and doesn't consider everything that is happening in a given scene. For example, it does not capture what the GPU not being synced with the CPU would look like, or even that the heuristic is making the right guess of how much to change the resolution. It's purpose is to clearly demonstrate the "ideal" circumstances to show how the dynamic resolution console variables operate.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dcb4db7-cde1-48eb-a2fc-be35eb987336/framegpugraph.png "FrameGPUGraph.png")

| Reference Number | Console Variable | Description |
| --- | --- | --- |
| **1** | r.DynamicRes.FrameTimeBudget | The frame's time budget measured in milliseconds (ms). |
| **2** | r.DynamicRes.TargetedGPUHeadRoom | The headroom left for the GPU to increase before going over budget (in percentages of the frame's budget). This will likely depend on the shipping platform or according to what rendering features are enabled. For example, motion blur needs additional room for cost to account for fast rotation of camera movements. |
| **3** | r.DynamicRes.ChangePercentageThreshold | The minimal changes that are required in percentage to actually resize the allocation. It is useful to not constantly change between a very close resolution size. If the value is too small, it may end up constantly changing the resolution, and if it's too large, it may cause a higher risk to go over the GPU budget. |
| **4** | r.DynamicRes.MinResolutionChangePeriod | The minimum number of frames before any resolution changes are allowed. This command has multiple purposes. These include having a better reliability of the heuristic to model the GPU consumption at a given primary screen percentage despite the measurements noise, being able to avoid [Temporal Upsample's](/documentation/en-us/unreal-engine/screen-percentage-with-temporal-upscale-in-unreal-engine#temporalanti-aliasingupsample) input sample offset interference that can occur between per-frame offset jittering, and the changing resolution that can be responsible for anti-aliasing divergence. |

You can also use the following console variables to adjust the history of the heuristic used for dynamic resolution and a screen percentage to use if you're CPU bound instead of GPU bound:

| Console Variable | Description |
| --- | --- |
| **r.DynamicRes.HistorySize** | The number of frames in the heuristic frame history. If it's too short, the history may be too noisy for the heuristic to be reliable, or if it's too long there may be very delayed adjustments. |
| **r.DynamicRes.CPUBoundScreenPercentage** | The primary screen percentage that should be targeted when you are bound by the CPU. It's useful to set a lower screen percentage to decrease the resolution on platforms where the CPU and GPU are sharing the same memory bandwidth. |

### Over Budget Panic

If you find that dynamic resolution is going over budget very quickly, like during a camera cut or when an expensive visual effect happens, the heuristic that is used can't actually predict when this will happen. In these cases, a "panic" switch is used to quickly lower the resolution when it does happen to reduce the number of frames that are over budget. If the heuristic finds that N (some number) consecutive frames with the available GPU timings is over budget, it is going to immediately adapt the resolution to combat these over budget timings. It will also perform an automatic history reset so that the previously less expensive frame timings do not influence the heuristic for the more expensive frames.

Use the following console command to control the maximum number of consecutive frames the GPU can be over budget before flipping the "panic" switch to lower the resolution:

```
	`r.DynamicRes.MaxConsecutiveOverbudgetGPUFrameCount`

Copy full snippet
```
r.DynamicRes.MaxConsecutiveOverbudgetGPUFrameCount

In this graph, the frame receives a sudden jump that puts it over the set budget of 33.3 ms for more than two frames consecutively. The panic switch is activated to quickly lower the resolution so that the frame is no longer over budget.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8601a9b5-b160-45c6-a278-491b5fc62123/overbudgetpanicgraph.png "OverBudgetPanicGraph.png")

1.  Max Consecutive GPU Frames that are over budget.
2.  The frame latency between detection and resolution change caused by the GPU being not synchronized with the render thread.
3.  Panic detection happens to trigger the drop in frames.
4.  The resolution change occurs for the given frames.

In the following captures (taken from the Infiltrator demo that is available on the **Learn** tab of the Epic Games Launcher), the **Stat Raw** command is used to clearly identify scene behavior when there is a camera cut or when an expensive visual effect happens on the screen:

Click image for full size.

1.  After the camera cut, the frame becomes significantly more expensive to render, at least for a few frames.
2.  Dynamic resolution has a panic reaction and quickly lowers the resolution to compensate before gradually rising back to normal again.

Click image for full size.

1.  A visual effect happens that is more expensive to render causing a spike that is the allotted frame budget for more than a couple of frames.
2.  Dynamic resolution acts quickly by lowering the resolution before gradually rising back to normal again.

## Testing Content with different Primary Screen Percentages

If your project has enabled dynamic resolution, you'll need to test it and make sure that it doesn't look significantly different than intended when using a lower primary screen percentage. At lower resolutions, some details can be lost and your assets may not retain the look that you intend them to have. For this very reason, all Editor Viewport can set a Screen Percentage using a slider for testing.

Click image for full size.

Use the slider to apply a higher or lower screen percentage to the viewport and check your level content accordingly. Artists, particularly, should use the slider to check their content at the high and low ranges of the screen percentages that will be used for the project.

![Editor Screen Percentage: | 100 (default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02396042-0d25-41f9-97d2-d13f4c8ceb3a/screenpercentage100.jpg)

![Editor Screen Percentage: | 50](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47faad2c-5bb0-408f-80f3-06db5870adbc/screenpercentage50.jpg)

When adjusting the screen percentage slider, the viewport (lower-right) will display any value for Screen Percentage that is higher than 100. This is meant as a reminder that the viewport screen percentage value has been changed to one that is not default and can potentially cause performance issues since it's using a higher than normal resolution.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8a31a09-6a9f-4d65-b3fb-828da3dfe90a/editor_screenpercentageindicator.png "Editor_ScreenPercentageIndicator.png")

Screen Percentage values higher than the default value can cause sluggishness or a decrease in performance for the Editor. When this happens, try resetting the value to the default of 100.

## Supported Platforms for Dynamic Resolution

The following platforms are supported

-   Microsoft's Xbox One, Xbox Series S, and Xbox Series X
-   PlayStation 4 and PlayStation 5 (excluding PSVR)
-   Nintendo Switch

Additional platform support is planned for future Engine releases.

Enabling dynamic resolution for platforms that are not on this allowlist is dangerous and can have unintended consequences. This could include having the wrong GPU timings which could unnecessarily drop the resolution or increase the resolution too much and drop frames. Ultimately, it could ruin the gameplay experience. By default, the Engine does not allow you to use dynamic resolution on platforms that are not on this allowlist.

## Replacing Dynamic Resolution Heuristic in C++

The engine-provided render thread heuristic is completely self-contained within **DynamicResolution.cpp**. The architecture is set up so that it allows the heuristic to be fully replaceable by Plugins in game code.

For example, if your project needs to replace the default heuristic because you want to do something like game play code giving hints of what is going to happen in the next frame, you can rewrite the entire heuristic to do just that. By implementing `IDynamicResolutionState` and `ISceneViewFamilyScreenPercentage`, you can replace the default dynamic resolution states, like the example below:

```
	`GEngine->ChangeDynamicResolutionStateNextFrame(new FMyGameSpecificDynamicResolutionState());`

Copy full snippet
```
GEngine->ChangeDynamicResolutionStateNextFrame(new FMyGameSpecificDynamicResolutionState());

The renderer will now work with **ResolutionFraction** to avoid the divide by 100 everywhere in the screen percentage math. It is named **fraction** instead of "scale" because the upscale ratio is done by the TAA upsample or the spatial upscale is actually represented by 1 divided by the Resolution Fraction, like so:

```
	`Resolution Fraction = Screen Percentage/100 = 1/Upscaling Factor`
Copy full snippet
```
Resolution Fraction = Screen Percentage/100 = 1/Upscaling Factor

## Limitations of Dynamic Resolution

The following are some current limitations of Dynamic Resolution:

-   It is not supported for use with multi-world Play-In-Editor by design.
-   When TAAU is enabled, it will work with VR. Multi-Sample Anti-Aliasing (MSAA) support will follow in a future release.
-   The API is fully compatible with the mobile renderer. However, there hasn't been an effort to maintain the view size not being equal to the render target buffer size that is set by the primary screen percentage upper bound.
-   Gaussian Depth of Field (DoF) and [Distance Field Ambient Occlusion](/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine) (DFAO) have issues with resolution changes.

## Frequently Asked Questions

The following are some general frequently asked questions regarding dynamic resolution:

**Can the heuristic for Dynamic Resolution be replaced?**

Yes, it was designed to be modular and pluggable in C++. Unreal Engine only maintains a single heuristic, but the architecture allows for the creation of a standalone custom heuristic with custom game thread events that could be triggered by gameplay code or Sequencer.

**Does dynamic resolution work with any arbitrary secondary screen percentage?**

Yes. This can be achieved by using the console variable **r.SecondaryScreenPercentage.GameViewport.**

For additional information, see the [Screen Percentage with Temporal Upsample](/documentation/en-us/unreal-engine/screen-percentage-with-temporal-upscale-in-unreal-engine) page.

**Is it possible to control the dynamic resolution of the secondary screen percentage?**

No, it's not possible and is by design. You would not want to change the size of Temporal Anti-Aliasing history and is why you should not need to dynamically change the secondary screen percentage.

**Why is the function in FPostProcessSettings for ScreenPercentage ignored by dynamic resolution?**

This was part of the previous mechanism where screen percentage could be configured in the settings for a Post Process Volume to manually scale up or down. With dynamic resolution, there is no need to set that any longer since it is automatically handled according to the GPU workload.

**Why is there not an optional show flag for dynamic resolution in the Editor?**

Because it happens globally and at game thread discretion. The screen percentage show flag will only toggle the [Primary Screen Percentage](/documentation/en-us/unreal-engine/screen-percentage-with-temporal-upscale-in-unreal-engine#primaryscreenpercentage).

**Why is dynamic resolution not supported in Editor viewports?**

Currently, dynamic resolution is only supported for Xbox One ,PlayStation 4, and Nintendo Switch which don't use PIE. When it is available for platforms (Vulkan, D3D12), you will be able to use it in the Editor with PIE.

**Can the Primary and Secondary Screen Percentages be accessed in Materials?**

No they cannot. Materials should be rendering independently of the resolution.
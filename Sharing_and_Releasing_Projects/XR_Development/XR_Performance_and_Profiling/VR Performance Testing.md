# VR Performance Testing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/vr-performance-testing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/vr-performance-testing-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:49

---

In general, maintaining VR frame rates is extremely challenging even on recommended hardware. Frame rate consistency is more important than in regular real-time rendering as dropping frames can make your experience uncomfortable for the user.

With that in mind, you need to leave yourself a buffer to ensure you can absorb frames which may run longer than average. We don't allow pipelining multiple frames due to the input/tracking latency it would introduce. This means the game thread is only one frame ahead of the render thread at all times and the GPU and render thread are in sync on the same frame. You have slightly less than 11ms of GPU time, because of the overhead of reprojection. Long frame times in the game thread due to gameplay code overhead, the render thread due to draw call overhead, or the GPU due to transform or shading overhead can cause you to miss frame time. All three need to be considered and balanced.

If you follow the console variable settings in the [Best Practices guide](/documentation/en-us/unreal-engine/xr-best-practices-in-unreal-engine), your render thread performance should be around where it needs to be for performance. From there, it's important to optimize your content and gameplay code to ensure that you make frame rate. On the content side, keep everything as simple as it can be.

General practices for simplifying content include the following.

-   Avoid dynamic lights and shadows.
-   Avoid heavy use of translucency.
-   Instance in visible batches. If one element of your instanced group is visible, the whole group will be drawn.
-   Make LODs for everything.
-   Keep material complexity and number of materials per object low.
-   Bake out anything that you can get away with.
-   Avoid large geometry that can encompass the player.
-   Use precomputed visibility volumes where possible.

See the [Bullet Train](https://s3.amazonaws.com/epiccms_epiccms_bucket/Resources/files/Going+Off+the+Rails.zip) and [Showdown](https://cdn2.unrealengine.com/Resources/files/UE4-Integration-and-Demos_OC-100270768.pptx) slide decks for examples of how Epic has produced content for virtual reality that looks more complex than it actually is. Also, be aware that most screen space tricks don't behave as you'd expect in stereo. They generally look flat or simply wrong.

Be sure to profile your work throughout the project and ensure you're always maintaining frame rate. Slowly adding complexity until you reach a tipping point is much easier to manage than trying to find areas to scale back down to meet the target performance a few days before shipping.

Reducing draw calls really comes down to two techniques. Make sure that you combine as many materials as possible and make sure to make heavy use of instanced static mesh components. Again, when instancing, remember that whatever is instanced will always be drawn in its entirety if one part is visible. This can greatly diminish the benefits of instancing in certain cases, so be sure to instance in batches where most of the objects in the batch will likely be visible or invisible from the same point.

The other thing that you may consider doing is using cull volumes to ensure that non-visible rooms are completely culled out when outside of them. Our occlusion is slightly more liberal in what it chooses to draw, and cull volumes help make this a bit more conservative in those choices. Additionally, you can toggle visibility on Actors (or entire sublevels) to get the same effect, if your content is built like that.

Another important thing to remember is that if something has an alpha of zero, it may still be drawn. So, if you don't want to render it, be sure to actually hide it to prevent it from being rendered.

## Getting General Stats

Both Oculus and SteamVR provide external tools to watch the performance. It is advisable to use these to see actual frame timings with the compositor overhead.

From the UE4 side, when in the game, there are a few ways to get general stats:

| Console Command | Description |
| --- | --- |
| stat unit | This will give you general game thread, draw thread, and GPU time, as well as overall frame timing. This is most useful for gathering whether the total frametime is where it needs to be, and what the game thread time is, but it should not be used for Draw Thread and GPU time. |
| startfpschart / stopfpschart | If you want to get an idea of what percentage of time is spent above 90Hz, you can run these commands. It'll capture and aggregate stats data over the window between when you started and stopped, and then dump a file that has bucketed framerate information. Note that since sometimes the game reports slightly under 90Hz when actually at 90, it's best to check the 80+ buckets to determine the actual time spent at framerate. |
| stat gpu | This command, added in 4.14, gives similar stats to the GPU profiler, but in a form that you can watch and monitor from in the game. Great for checking quick costs on GPU work. |

### Real-Time GPU Profiler

To use the new real-time GPU profiler, type `stat gpu` in the game or editor. The stats are cumulative and non-hierarchical, so you can see the major categories without having to dig down through a tree of events. For example, shadow projection is the sum of all the shadow projections for all lights (across all the views).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a475d863-eaef-46ce-9f35-fcd3a0b80b91/statgpu.png)

The realtime stats are particularly useful if you want to gather stats during gameplay (e.g. for graphing later). You can use the realtime display to profile features enabled on console variables or quality settings, or for in-editor optimization where you want to see the results instantly.

Stats are declared in code as float counters, e.g.: `DECLARE_FLOAT_COUNTER_STAT(TEXT("Postprocessing"), Stat_GPU_Postprocessing, STATGROUP_GPU);`

Renderthread code blocks can be instrumented with `SCOPED_GPU_STAT` macros, which work similarly to `SCOPED_DRAW_EVENT`, e.g.: `SCOPED_GPU_STAT(RHICmdList, Stat_GPU_Postprocessing);`

Unlike the draw events, GPU stats are cumulative. You can add multiple entries for the same stat, and these will get aggregated.

Anything not marked up explicitly should be included in the catch-all `[unaccounted]` stat. If that gets high, then it indicates something is not being caught in the explicit stats and more tracking macros should be added.
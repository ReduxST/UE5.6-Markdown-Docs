# VR Profiling Interpretations and Considerations

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/vr-profiler-interpretations-and-considerations-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/vr-profiler-interpretations-and-considerations-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:50

---

While [profiling tools](/documentation/en-us/unreal-engine/vr-profiling-tools-in-unreal-engine) can provide data about how your project is performing in VR, there are some points to consider when interpreting those values.

Delays can appear in odd places in the GPU and CPU profilers, most often as occlusion or scene graph traversal time. If those numbers are abnormally high, it's possible that it's a false positive.

Often when profiling, you'll notice that you pop between 90 Hz and 45 Hz. The difference is accounted for because the Compositor acts much like a vsync. If you miss framerate, it delays you until the next frame entirely. So, you tend to go down in brackets of 90 / n, where n is a whole number. Because the fps reporting is an average, it won't always report as a whole number, unless the drop is sustained. If you're bouncing back and forth between making framerate and not, you may see some fraction of a jump.

If you'd like to remove this for testing, sometimes it's useful to run the game emulating stereo rendering, instead of running in the device itself. To do so:

-   Launch the game with `-game -emulatestereo -res=2160x1200` on the commandline
-   Ensure vsync is off with `r.vsync 0` in the console
-   Update the screen percentage to emulate the oversampling we have to do for VR with `r.screenpercentage 137` in the console

This will emulate the GPU and CPU performance characteristics without the annoyances of the variable framerate.

It's worth explicitly noting that if you're hitting 90 frames a second most of the time, and then make a change and notice a drastic drop, you're probably falling prey to the Compositor "vsync" issue noted above. As soon as you tip over the cliff, you'll see drastic changes in numbers.
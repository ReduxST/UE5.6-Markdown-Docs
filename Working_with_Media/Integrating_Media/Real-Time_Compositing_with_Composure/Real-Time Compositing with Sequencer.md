# Real-Time Compositing with Sequencer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:53

---

[Sequencer](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview), our in-engine cinematic editor, can be used in conjunction with the Composure compositing system. 

![Using Composure with Sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa214da4-16c5-41a7-8aeb-ea880c777505/composure-sequencer.gif "composure-sequencer.gif")

Primarily, Sequencer can be used to: 

1.  Control the scene camera (referenced by the compositing system).
    
2.  Render out composites and their contributing pieces, including Arbitrary Output Values (AOVs). This can be useful for compositing outside of the engine.
    

## Rendering Out Elements and AOVs

Any Composure element can be added to a sequence to indicate that its output should be exported when rendering out the sequence using the **Render Movie Settings** dialog with the **ComposureExport** output format.

Click image to expand.

When such elements are rendered as part of this process, their final output will be written out to disk as an EXR image using the filename format specified in the dialog. Additional format specifiers can be included in the directory and filename options for the **{element}** and **{pass}**.

When multiple elements are included for **Export Output** in Sequencer, they will write over the same image file if **{element}** is not included in the name.

Click image to expand.

Additional AOVs to be exported with each element can be specified on each element by configuring the **Buffers to Export** on any CG Capture.

![Buffers to Export](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/076de18e-85e5-4cb2-95b2-570791c1ea8e/buffers-to-export.gif "buffers-to-export.gif")

Custom AOVs may be implemented by adding new Buffer Visualization materials, and adding them to the `[Engine.BufferVisualizationMaterials]` config section with the following format:

`CustomAOV=(Material="/Game/AOVs/CustomAOV.CustomAOV", Name=LOCTEXT("CustomAOV", "CustomAOV"))`
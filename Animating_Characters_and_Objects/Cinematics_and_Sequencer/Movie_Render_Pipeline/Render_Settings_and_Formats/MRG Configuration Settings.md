# MRG Configuration Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mrg-configuration-settings-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mrg-configuration-settings-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:20

---

## Screen Traces

Lumen has some screen tracing elements enabled by default. This can interfere with some of the layer visibility settings being invoked by the graph. For example, if you would like your character to be visible to reflections and global illumination but hidden from primary pixels on a given layer, having Screen Traces enabled will cause the character to now show up in the Lumen Scene as desired, so it is recommended that you disable them.

There are several ways to disable Lumen screen traces.

-   You can invoke the cvars:
    
    -   `r.Lumen.Reflections.ScreenTraces 0`
        
    -   `r.Lumen.ScreenProbeGather.ScreenTraces 0`
        
-   You can disable them in the showflags both with a console command
    
    -   `ShowFlag.LumenScreenTraces 0`
-   And in the MRG Deferred Rendering node under the Show Flags section, which can also be promoted to a variable.
    

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/369bbc43-8604-4897-8565-1222a97adcee/image_0.png)

-   As of 5.4, Screen Trace boolean parameters have been added to the Post Process Volume in both the Lumen Global Illumination and Lumen Reflections sections.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51dbd095-ce23-40bf-b862-fb889445a3df/image_1.png)

Here is a visual example of how Screen Traces can interfere with Affect Indirect Lighting While Hidden. In this first image, we see a sphere being reflected into the mirror surface underneath.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/286e83f1-08d1-4225-8ade-b1528b181304/image_2.png)

When we enable Affect Indirect Lighting While Hidden and disable Visible we see the reflection disappear because it is being drawn using Screen Space reflections.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64223054-3f11-4bef-8caa-357f0399cd6f/image_3.png)

But if we disable Screen Traces in the Post Process Volume you see the reflection reappear.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a3e0615-4b82-47ec-88c0-ad0919a845f5/image_4.png)

Comparison:

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/326189e2-f62b-48c9-ad5e-bd65d54e370a/image_5.png)

Disabling Lumen Screen Traces can change the look of your scene, so it is recommended to set these as you are lighting your level rather than purely as something toggled at render time.

## Tone Curve

When working with **translucent actors** it is advised that you **disable Tone Curve** due to the fact that the alpha is pre-multiplied before curves/encodings are applied in the engine. So if you have a tone curve applied and try to render a partly translucent object on its own layer it will look differently when composited than what you see in-Engine. In this case, Tone Curve gives you non-linear colors which is undesirable for this type of composite. When using your own OCIO configuration, it will likely be necessary to disable the Tone Curve.

## Allow OCIO

The **Allow OCIO on the Deferred** and **Path Traced Rendering** nodes offer an opt-out (defaults to on) for data-oriented Render Layers that are handled via Show Flags and Material Modifiers where OCIO would not be desirable.

## Groom

-   There are times when rendering Groom with motion blur in multiple layers can create some incorrect results. Consider trying the command `MoviePipeline.FlushLayersDebug 1` to see improvements.
    
-   To improve any halo around the groom when using holdouts consider the `r.HairStrands.HoldoutMode 1` command.
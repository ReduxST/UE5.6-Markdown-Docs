# Scalability Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/scalability-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/scalability-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:47:54

---

The Scalability settings allow you to adjust the quality of various features in order to maintain the best performance for your game on different platforms and hardware.

## Scalability Settings

Accessing the Scalability settings in the editor is done through the **Settings** menu in the toolbar. The **Engine Scalability Settings** contains shortcuts to the most commonly used setting defined in the BaseScalability.ini file, while **Material Quality Level** sets the global material quality setting.

## Resolution Scale

Unreal Engine 4 can render a scene in lower resolution and scale the image up to the target resolution. As 2D User interfaces usually costs less performance and suffers more from lower resolution, Unreal Engine 4 does not apply this technique to UI. There is a minor cost for the up-sampling pass, but usually, it is worth the effort.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e29eb620-f191-40dc-8624-377f3df094bd/sc_00007.png)

Left: 50% no AA, Middle: 50% with AA, Right: 100% (no resolution scale) with AA

Having a softer input image helps the up-sampling step. This means this scalability options benefits from another scalability option: the anti-aliasing quality.

This setting can be accessed with the **r.ScreenPercentage** console variable. It takes in a value from 10-100 with -1 also equaling 100%.

## View Distance

Objects can be culled based on their distance to the viewer. By default, all objects are not distance culled (Desired max draw distance of 0). On top of the designer specified value, there is a global scalability setting working like a multiplier (**r.ViewDistanceScale**). Here you can see some grass objects (Desired max draw distance of 1000):

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a18a4bac-e4e3-4fdc-85d1-dba3eee17b4a/sc_00006.png)

left: r.ViewDistanceScale 0.4, middle: r.ViewDistanceScale 0.7, right: r.ViewDistanceScale 1.0 (default)

## Anti-Aliasing

From the left: r.PostProcessAAQuality 0 to 6. The first 3 equal the Low, Medium, High, Epic settings in the View -> Scalability Options -> AA settings.

Adjusting the Anti-Aliasing quality level using the **r.PostProcessAAQuality** console command will adjust the quality of whichever Anti-Aliasing method you are using (FXAA or Temporal AA). For either Anti-Aliasing method, a value of 0 used with **r.PostProcessAAQuality** will disable the effect. For FXAA, the effect of values 2, 4, and 6, can be seen in the above image; the smoothing of jagged edges becomes better and better. Values above 6 have no effect.

For Temporal AA, there is a trade off between fill speed of the effect and quality, the higher the value you use. *r.PostProcessAAQuality* 2 with Temporal AA is fast to settle but jitter caused by the effect will be more pronounced. *r.PostProcessAAQuality* 4 will settle slower but will not jitter.

## Post Processing - sg.PostProcessQuality

sg.PostProcessQuality set from 0 on the left to 3 on the right.

The **View** -> **Engine Scalability Settings** -> **Post Processing** option adjusts the quality of the Post Processing effects in accordance with the settings found in the BaseScalability.ini file located in \[UE\_InstallPath\]/Engine/Config folder. With the **Low** setting equating to *sg.PostProcessQuality* 0 and **Epic** to *sg.PostProcessQuality* 3.

| sg.PostProcessQuality 0 | sg.PostProcessQuality 1 |
| --- | --- |
| 
```
	`r.MotionBlurQuality=0 	r.BlurGBuffer=0 	r.AmbientOcclusionLevels=0 	r.AmbientOcclusionRadiusScale=1.7 	r.DepthOfFieldQuality=0 	r.RenderTargetPoolMin=300 	r.LensFlareQuality=0 	r.SceneColorFringeQuality=0 	r.EyeAdaptationQuality=0 	r.BloomQuality=4 	r.FastBlurThreshold=0 	r.Upscale.Quality=1 	r.Tonemapper.GrainQuantization=0`
Copy full snippet
```
r.MotionBlurQuality=0 r.BlurGBuffer=0 r.AmbientOcclusionLevels=0 r.AmbientOcclusionRadiusScale=1.7 r.DepthOfFieldQuality=0 r.RenderTargetPoolMin=300 r.LensFlareQuality=0 r.SceneColorFringeQuality=0 r.EyeAdaptationQuality=0 r.BloomQuality=4 r.FastBlurThreshold=0 r.Upscale.Quality=1 r.Tonemapper.GrainQuantization=0

 | 

```
	`r.MotionBlurQuality=3 	r.BlurGBuffer=0 	r.AmbientOcclusionLevels=1 	r.AmbientOcclusionRadiusScale=1.7 	r.DepthOfFieldQuality=1 	r.RenderTargetPoolMin=350 	r.LensFlareQuality=0 	r.SceneColorFringeQuality=0 	r.EyeAdaptationQuality=0 	r.BloomQuality=4 	r.FastBlurThreshold=2 	r.Upscale.Quality=2 	r.Tonemapper.GrainQuantization=0`
Copy full snippet
```
r.MotionBlurQuality=3 r.BlurGBuffer=0 r.AmbientOcclusionLevels=1 r.AmbientOcclusionRadiusScale=1.7 r.DepthOfFieldQuality=1 r.RenderTargetPoolMin=350 r.LensFlareQuality=0 r.SceneColorFringeQuality=0 r.EyeAdaptationQuality=0 r.BloomQuality=4 r.FastBlurThreshold=2 r.Upscale.Quality=2 r.Tonemapper.GrainQuantization=0

 |

| sg.PostProcessQuality 2 | sg.PostProcessQuality 3 |
| --- | --- |
| 
```
	`r.MotionBlurQuality=3 	r.BlurGBuffer=-1 	r.AmbientOcclusionLevels=2 	r.AmbientOcclusionRadiusScale=1.5 	r.DepthOfFieldQuality=2 	r.RenderTargetPoolMin=400 	r.LensFlareQuality=2 	r.SceneColorFringeQuality=1 	r.EyeAdaptationQuality=2 	r.BloomQuality=5 	r.FastBlurThreshold=3 	r.Upscale.Quality=2 	r.Tonemapper.GrainQuantization=1`
Copy full snippet
```
r.MotionBlurQuality=3 r.BlurGBuffer=-1 r.AmbientOcclusionLevels=2 r.AmbientOcclusionRadiusScale=1.5 r.DepthOfFieldQuality=2 r.RenderTargetPoolMin=400 r.LensFlareQuality=2 r.SceneColorFringeQuality=1 r.EyeAdaptationQuality=2 r.BloomQuality=5 r.FastBlurThreshold=3 r.Upscale.Quality=2 r.Tonemapper.GrainQuantization=1

 | 

```
	`r.MotionBlurQuality=4 	r.BlurGBuffer=-1 	r.AmbientOcclusionLevels=3 	r.AmbientOcclusionRadiusScale=1.0 	r.DepthOfFieldQuality=2 	r.RenderTargetPoolMin=400 	r.LensFlareQuality=2 	r.SceneColorFringeQuality=1 	r.EyeAdaptationQuality=2 	r.BloomQuality=5 	r.FastBlurThreshold=7 	r.Upscale.Quality=3 	r.Tonemapper.GrainQuantization=1`
Copy full snippet
```
r.MotionBlurQuality=4 r.BlurGBuffer=-1 r.AmbientOcclusionLevels=3 r.AmbientOcclusionRadiusScale=1.0 r.DepthOfFieldQuality=2 r.RenderTargetPoolMin=400 r.LensFlareQuality=2 r.SceneColorFringeQuality=1 r.EyeAdaptationQuality=2 r.BloomQuality=5 r.FastBlurThreshold=7 r.Upscale.Quality=3 r.Tonemapper.GrainQuantization=1

 |

## Shadows - sg.ShadowQuality

sg.ShadowQuality set from 0 on the left to 3 on the right.

The **View** -> **Engine Scalability Settings** -> **Shadows** option adjusts the quality of dynamic shadows in accordance with the settings found in the BaseScalability.ini file located in \[UE\_InstallPath\]/Engine/Config folder. With the **Low** setting equating to *sg.ShadowQuality* 0 and **Epic** to *sg.ShadowQuality* 3.

| sg.ShadowQuality 0 | sg.ShadowQuality 1 |
| --- | --- |
| 
```
	`r.LightFunctionQuality=0 	r.ShadowQuality=0 	r.Shadow.CSM.MaxCascades=1 	r.Shadow.MaxResolution=512 	r.Shadow.RadiusThreshold=0.06 	r.Shadow.DistanceScale=0.6 	r.Shadow.CSM.TransitionScale=0`
Copy full snippet
```
r.LightFunctionQuality=0 r.ShadowQuality=0 r.Shadow.CSM.MaxCascades=1 r.Shadow.MaxResolution=512 r.Shadow.RadiusThreshold=0.06 r.Shadow.DistanceScale=0.6 r.Shadow.CSM.TransitionScale=0

 | 

```
	`r.LightFunctionQuality=1 	r.ShadowQuality=2 	r.Shadow.CSM.MaxCascades=1 	r.Shadow.MaxResolution=1024 	r.Shadow.RadiusThreshold=0.05 	r.Shadow.DistanceScale=0.7 	r.Shadow.CSM.TransitionScale=0.25`
Copy full snippet
```
r.LightFunctionQuality=1 r.ShadowQuality=2 r.Shadow.CSM.MaxCascades=1 r.Shadow.MaxResolution=1024 r.Shadow.RadiusThreshold=0.05 r.Shadow.DistanceScale=0.7 r.Shadow.CSM.TransitionScale=0.25

 |

| sg.ShadowQuality 2 | sg.ShadowQuality 3 |
| --- | --- |
| 
```
	`r.LightFunctionQuality=1 	r.ShadowQuality=5 	r.Shadow.CSM.MaxCascades=2 	r.Shadow.MaxResolution=1024 	r.Shadow.RadiusThreshold=0.04 	r.Shadow.DistanceScale=0.85 	r.Shadow.CSM.TransitionScale=0.8`
Copy full snippet
```
r.LightFunctionQuality=1 r.ShadowQuality=5 r.Shadow.CSM.MaxCascades=2 r.Shadow.MaxResolution=1024 r.Shadow.RadiusThreshold=0.04 r.Shadow.DistanceScale=0.85 r.Shadow.CSM.TransitionScale=0.8

 | 

```
	`r.LightFunctionQuality=1 	r.ShadowQuality=5 	r.Shadow.CSM.MaxCascades=4 	r.Shadow.MaxResolution=1024 	r.Shadow.RadiusThreshold=0.03 	r.Shadow.DistanceScale=1.0 	r.Shadow.CSM.TransitionScale=1.0`
Copy full snippet
```
r.LightFunctionQuality=1 r.ShadowQuality=5 r.Shadow.CSM.MaxCascades=4 r.Shadow.MaxResolution=1024 r.Shadow.RadiusThreshold=0.03 r.Shadow.DistanceScale=1.0 r.Shadow.CSM.TransitionScale=1.0

 |

## Textures - sg.TextureQuality

A modern rendering engine requires a lot more GPU memory (textures, meshes, GBuffer, Depth Buffer, Shadow maps). Some of those scale with the screen resolution (e.g. GBuffer), others with specific quality settings (e.g. Shadow maps). Another large amount comes from the used textures (usually compressed and streamed). You can instruct the streaming system to be more aggressive in management (smaller pool size, culling unused textures) or to have less or more detail in the mip level computation. This can have effects on the image quality, how much you can notice texture streaming artifacts and how smooth the game runs (updates require expensive memory transfers). The results can vary, depending on the media (e.g. faster/lower hard drive /SSD). Streaming from a DVD/Blu-Ray adds much more latency so you should try to avoid that.

The texture quality also affects the texture filtering mode (r.MaxAnisotropy). Limiting the anisotropic sample count reduces texture bandwidth, but does not save texture memory.

| sg.TextureQuality 0 | sg.TextureQuality 1 |
| --- | --- |
| 
```
	`r.Streaming.MipBias=2.5 	r.MaxAnisotropy=0 	r.Streaming.PoolSize=200`
Copy full snippet
```
r.Streaming.MipBias=2.5 r.MaxAnisotropy=0 r.Streaming.PoolSize=200

 | 

```
	`r.Streaming.MipBias=1 	r.MaxAnisotropy=2 	r.Streaming.PoolSize=400`
Copy full snippet
```
r.Streaming.MipBias=1 r.MaxAnisotropy=2 r.Streaming.PoolSize=400

 |

| sg.TextureQuality 2 | sg.TextureQuality 3 |
| --- | --- |
| 
```
	`r.Streaming.MipBias=0 	r.MaxAnisotropy=4 	r.Streaming.PoolSize=700`
Copy full snippet
```
r.Streaming.MipBias=0 r.MaxAnisotropy=4 r.Streaming.PoolSize=700

 | 

```
	`r.Streaming.MipBias=0 	r.MaxAnisotropy=8 	r.Streaming.PoolSize=1000`
Copy full snippet
```
r.Streaming.MipBias=0 r.MaxAnisotropy=8 r.Streaming.PoolSize=1000

 |

The effect of this feature is heavily dependent on your game and hardware. If you do not have many textures, to the point where loading and using the full resolution mip maps does not use all of the memory pool Unreal Engine 4 has devoted to textures, you will not actually see a difference between high and low settings (outside of the change to the Anisotropy settings).

## Effects - sg.EffectsQuality

The **View** -> **Engine Scalability Settings** -> **Effects** option adjusts the quality of many different types of effects in accordance with the settings found in the BaseScalability.ini file located in \[UE\_InstallPath\]/Engine/Config folder. With the **Low** setting equating to sg.EffectsQuality 0 and **Epic** to sg.EffectsQuality 3.

| sg.EffectsQuality 0 | sg.EffectsQuality 1 |
| --- | --- |
| 
```
	`r.TranslucencyLightingVolumeDim=24 	r.RefractionQuality=0 	r.SSR=0 	r.SceneColorFormat=3 	r.DetailMode=0 	r.TranslucencyVolumeBlur=0 	r.MaterialQualityLevel=0`
Copy full snippet
```
r.TranslucencyLightingVolumeDim=24 r.RefractionQuality=0 r.SSR=0 r.SceneColorFormat=3 r.DetailMode=0 r.TranslucencyVolumeBlur=0 r.MaterialQualityLevel=0

 | 

```
	`r.TranslucencyLightingVolumeDim=32 	r.RefractionQuality=0 	r.SSR=0 	r.SceneColorFormat=3 	r.DetailMode=1 	r.TranslucencyVolumeBlur=0 	r.MaterialQualityLevel=1`
Copy full snippet
```
r.TranslucencyLightingVolumeDim=32 r.RefractionQuality=0 r.SSR=0 r.SceneColorFormat=3 r.DetailMode=1 r.TranslucencyVolumeBlur=0 r.MaterialQualityLevel=1

 |

| sg.EffectsQuality 2 | sg.EffectsQuality 3 |
| --- | --- |
| 
```
	`r.TranslucencyLightingVolumeDim=48 	r.RefractionQuality=2 	r.SSR=0 	r.SceneColorFormat=3 	r.DetailMode=1 	r.TranslucencyVolumeBlur=1 	r.MaterialQualityLevel=1`
Copy full snippet
```
r.TranslucencyLightingVolumeDim=48 r.RefractionQuality=2 r.SSR=0 r.SceneColorFormat=3 r.DetailMode=1 r.TranslucencyVolumeBlur=1 r.MaterialQualityLevel=1

 | 

```
	`r.TranslucencyLightingVolumeDim=64 	r.RefractionQuality=2 	r.SSR.Quality=1 	r.SceneColorFormat=4 	r.DetailMode=2 	r.TranslucencyVolumeBlur=1 	r.MaterialQualityLevel=1`
Copy full snippet
```
r.TranslucencyLightingVolumeDim=64 r.RefractionQuality=2 r.SSR.Quality=1 r.SceneColorFormat=4 r.DetailMode=2 r.TranslucencyVolumeBlur=1 r.MaterialQualityLevel=1

 |

## Detail Mode

Each placed Actor has a **Detail Mode** property in the **Rendering** category. Essentially this setting defines the minimum detail level for an Actor to render.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/edbecc69-5558-4c8f-8cbf-cb6cceb7bd20/sc_00008.png)

The scalability mode can be changed from the console:

```
	`r.DetailMode 1`

Copy full snippet
```
r.DetailMode 1

With *r.DetailMode* 0 = low, *r.DetailMode* 1 = medium and, *r.DetailMode* 2 = high detail modes.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73b1669c-4e91-4516-adb4-14b2d0d414de/sc_00005.png)

It is easy to use this to disable decals, detail objects, lights or individual particle effects. Make sure to only use this on objects that have no effect on gameplay, otherwise, you will run into problems with network gameplay, save games, or consistency.

## Material Quality Level

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e97784a-cab1-403b-9279-75fe2dabbbe4/scaler_viewmatqual.png)

Materials can use the **Quality Switch** Material Expression node to disable some expensive Material parts that have a minor effect on the final look. To see the effect of this, you need to toggle to the **Low Quality** mode.

Setting the **Material Quality Level** to low or high determines which expressions get evaluated for this material (the low or high pin). The default pin will fill in either high or low (or both) if they have no inputs. This material contains 2 reasonably high-cost Perlin noise operations when set to high:

This example is to simply show off the **Material Switch Node**. The **Noise** nodes are really expensive making them really good for this example, but they should be used sparingly as there are cheaper ways to get this effect.

left: Material Quality Level set to low, right: Material Quality Level set to high

left: Material Quality Level set to low, right: Material Quality Level set to high. Shader Complexity mode shows that the high quality material is more costly than other shaders, with darker greens meaning more costly shaders.

Using the quality switch causes more shaders to be compiled (shader permutation).

This feature is not for distance LOD as you cannot have two quality levels at the same time. The feature can be used to reduce:

-   Shader computations (e.g. disable fuzz layer).
    -   Use **Shader Complexity** (**Alt+8** in the editor) mode and instruction count to verify your optimization.
-   Texture lookups (e.g. no detail bump map).
-   Memory bandwidth (e.g. using fewer textures).
    -   You would need to profile on actual hardware to verify this.

Most material editor outputs only affect the pixel shader. World position offset and all tessellation outputs affect the other shader types. Pixels shaders only cost a lot if they occupy large portions of the screen (skybox for example), while other shaders only matter if the object is not culled (inside the view, not hidden behind opaque objects).

## Skeletal Mesh LOD Bias

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89e43647-fe59-468c-b6e0-5ac409b06651/sc_skeletal.png)

Skeletal meshes can have static Level of Details models. With the console variable **r.SkeletalMeshLODBias**, it is possible to globally bias the LOD level. Depending on the quality of your first or second LOD, it might be a good idea to have this option in the scalability settings. Here you can see the scalability setting on top of the distance dependent LOD.

## Grass and Foliage Scalability

The **View** -> **Engine Scalability Settings** -> **Foliage** option adjusts how many foliage meshes are rendered at one time in accordance with the settings found in the BaseScalability.ini file located in \[UE\_InstallPath\]/Engine/Config folder. With the **Low** setting equating to FoliageQuality 0 and **Epic** to FoliageQuality 3.

For Foliage Static Meshes to work with the Scalability settings you must enable the **Enable Density Scaling** option. You can read more about how to set this up in the [Foliage Instanced Meshes](/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine) documentation.

| FoliageQuality 0 | FoliageQuality 1 |
| --- | --- |
| 
```
	`[FoliageQuality@0] 	foliage.DensityScale=0 	grass.DensityScale=0`
Copy full snippet
```
\[FoliageQuality@0\] foliage.DensityScale=0 grass.DensityScale=0

 | 

```
	`[FoliageQuality@1] 	foliage.DensityScale=0.4 	grass.DensityScale=0.4`
Copy full snippet
```
\[FoliageQuality@1\] foliage.DensityScale=0.4 grass.DensityScale=0.4

 |

| FoliageQuality 2 | FoliageQuality 3 |
| --- | --- |
| 
```
	`[FoliageQuality@2] 	foliage.DensityScale=0.8 	grass.DensityScale=0.8`
Copy full snippet
```
\[FoliageQuality@2\] foliage.DensityScale=0.8 grass.DensityScale=0.8

 | 

```
	`[FoliageQuality@3] 	foliage.DensityScale=1.0 	grass.DensityScale=1.0`
Copy full snippet
```
\[FoliageQuality@3\] foliage.DensityScale=1.0 grass.DensityScale=1.0

 |

## Customizing Scalability Settings

You can customize any of the Scalability Settings that are used in your Unreal Engine project. In the following example we will add and the change the Scalability Settings for the Foliage by doing the following:

1.  Go to your projects **Config** folder and create a new **.INI** file called **DefaultScalability.ini**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6de937a2-a66a-43f3-97fb-0509ed9fe489/fgc_config_location.png)
2.  Open up the newly created **DefaultScalability.ini** file and add the following lines of code to it.
    
    ```
             `[FoliageQuality@0]          foliage.DensityScale=.25          grass.DensityScale=.25 		          [FoliageQuality@1]          foliage.DensityScale=0.50          grass.DensityScale=0.50 		          [FoliageQuality@2]          foliage.DensityScale=0.75          grass.DensityScale=0.75 		          [FoliageQuality@3]          foliage.DensityScale=1.0          grass.DensityScale=1.0`
    		
    Copy full snippet
    ```
    \[FoliageQuality@0\] foliage.DensityScale=.25 grass.DensityScale=.25 \[FoliageQuality@1\] foliage.DensityScale=0.50 grass.DensityScale=0.50 \[FoliageQuality@2\] foliage.DensityScale=0.75 grass.DensityScale=0.75 \[FoliageQuality@3\] foliage.DensityScale=1.0 grass.DensityScale=1.0
3.  Save the file and now when the Scalability settings for **Foliage** are changed, the amount of Foliage and Landscape Grass Static Meshes that are spawned will be reduced or increased based on which setting was picked.
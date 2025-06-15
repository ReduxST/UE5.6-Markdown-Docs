# Reflections Captures

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/reflections-captures-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/reflections-captures-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:15

---

**Reflection Capture** Actors are probes that can be placed around the world to capture a static image of the area they cover. This reflection method reprojects the captured cubemap onto surrounding reflective materials. It is a low-cost method of reflections with no runtime performance cost.

## Reflection Capture Shapes

There are currently two reflection capture shapes: sphere and box. The shape is very important because it controls what part of the level is captured into the cubemap, what shape the level is reprojected onto in reflections, and which part of the level can receive reflections from that cubemap (area of influence).

### Sphere shape

The sphere shape is currently the most useful. It never matches the shape of the geometry being reflected but has no discontinuities or corners, therefore, the error is uniform.

![Sphere Shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acf17925-7308-4f2b-b7cc-17311cc2ea2e/01-capt-refl-sphere-shape.png)

The sphere shape has an orange influence radius that controls which pixels can be affected by that cubemap, and the sphere that the level will be reprojected onto.

Smaller captures will override larger ones, so you can provide refinement by placing smaller captures around the level.

### Box shape

The box shape is very limited in usefulness and generally only works for hallways or rectangular rooms. The reason is that only pixels inside the box can see the reflection, and at the same time all geometry inside the box is projected onto the box shape, creating significant artifacts in many cases.

![Box Shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4f84d1e-4ca7-42b9-8f83-3cf634036626/02-capt-refl-box-shape.png)

The box has an orange preview for the projection shape when selected. It only captures the level within **Box Transition Distance** outside this box. The influence of this capture fades in over the transition distance as well, inside the box.

## Setting Up a Level to use the Reflection Environment

The first step toward having good reflections is setting up diffuse lighting including indirect lighting through the use of lightmaps. The [Lightmass](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine#precomputedglobalillumination) page contains more info on how to accomplish this if you are unfamiliar with using it. Common errors preventing Lightmass indirect lighting from working after a build include but are not limited to the following:

-   A shadow casting skybox.
-   Lack of a **LightmassImportanceVolume**.
-   Missing or incorrectly setup lightmap UVs.
-   Having **Force No Precomputed Lighting** set to **True** in the **World Properties**.

Since the level's diffuse color is what will be reflected through the Reflection Environment you will need to do the following for the best results.

-   Ensure significant contrast between directly lit and shadowed areas.
-   Remember that the bright diffuse lit areas are what will show up clearly in reflections.
-   Darker shadowed areas are where the reflections will be most visible.
-   Use the Lit viewmode together with the Specular show flag disabled to see the level as the reflection captures see it.

It is also extremely important to setup your level's Materials to work well with the Reflection Environment by keeping the following in mind.

-   A flat, mirror surface will reveal the inaccuracies of combining cubemaps projected onto simple shapes.
-   Curvy geometry or rough surfaces can both obscure these artifacts and provide convincing results.
-   It is important to use detail Normal maps and specify some degree of roughness on Materials that will be used in flat areas as this will help them better show off reflections.

|   |   |   |
| --- | --- | --- |
| ![Curvy and Sharp](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9668347-b092-4e03-9758-7a02fda2489d/03-capt-refl-curvy-sharp.png) | ![Flat and Rough](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3c0b25c-d20b-458e-b963-2f56a591f6cd/04-capt-refl-flat-rough.png) | ![Flat and Sharp](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9e40e72-9a7a-4c38-b8ad-6b518df9f090/05-capt-refl-flat-sharp.png) |
| Smooth surface but curvy geometry: Good quality reflections | Rough surface but flat geometry: Good quality reflections | Smooth surface AND flat geometry: Evident that reflections do not match up |

Place reflection captures in the areas that you want to have reflections. Try to place the sphere captures such that the part of the level you want to reflect is contained just inside their radius since the level will be reprojected onto that sphere shape. Try to avoid placing captures too close to any level geometry, as that nearby geometry will dominate and block important details behind it.

## Glossy Indirect Specular

In technical terms, the Reflection Environment provides indirect specular. We get direct specular through analytical lights, but that only provides reflections in a few bright directions. We also get specular from the sky through a Sky Light, but that does not provide local reflections since the Sky Light cubemap is infinitely far away. Indirect specular allows all parts of the level to reflect on all other parts, which is especially important for Materials like metal which have no diffuse response.

![Diffuse Only](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32cf9566-d972-450b-80f6-316b81af72e5/06-capt-refl-diffuse-only.png)

![Reflection Only](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4b1017f-8e49-40c8-8d1e-c201ed380031/07-capt-refl-reflection-only.png)

**Full lighting**

![Full Scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e0df3a0-b157-40ff-913a-31d8c5eb53b3/08-capt-refl-complete-scene.png)

The Reflection Environment works by capturing the static level at many points and reprojecting it onto simple shapes like spheres in reflections. Artists choose the capture points by placing **Reflection Capture** Actors. Reflections update in real time during editing to aid in placement but are static at runtime. Projecting the captured level onto simple shapes gives approximate parallax for the reflection. Each pixel blends between multiple cubemaps to get the final result. Smaller ReflectionCapture Actors override larger ones, so you can refine reflection parallax accuracy in areas as needed. For example, you might place a capture at the center of a room and then refine the reflection by placing smaller captures at the corners of the room.

Materials with varying glossiness are supported by generating blurry mipmaps from the captured cubemaps.

![Varying Glossiness](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1971f94c-3052-4fb8-a9d9-9bab6184cfc9/09-capt-refl-varying-glossiness.png)

However, just using the cubemap reflections on a very rough surface results in an overly bright reflection that has significant leaking due to lack of local occlusion. This is solved by reusing the lightmap data generated by Lightmass. The cubemap reflection is mixed together with the lightmap indirect specular based on how rough the material is. A very rough material (fully diffuse) will converge on the lightmap result. This mixing is essentially combining the high detail part of one set of lighting data (cubemaps) with the low-frequency part of another set of lighting data (lightmaps).

For this to work correctly, though, only indirect lighting can be in the lightmap. This means that only the indirect lighting from Stationary lights can improve the quality of reflections on rough surfaces. **Static light types should not be used together with the Reflection Environment as they will put direct lighting in the lightmap.** Note that this mixing with the lightmap also means that the map must have meaningful indirect diffuse lighting and that lighting must already be built to see results.

![Reflections on a rough surface with no shadowing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dcc3792c-eb37-4001-87cd-a115cae1b6f0/10-capt-refl-rough-with-no-shadow.png)

![Rough with Shadowing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90f6294a-a29d-4b04-89b8-91c6d1cb3203/11-capt-refl-rough-with-shadow.png)

## Reflection Capture Lightmap Mixing

When you use Reflection Capture Actors, UE mixes the indirect Specular from the Reflection Capture with the indirect Diffuse lighting from lightmaps. This helps to reduce leaking since the reflection cubemap was only captured at one point in space, but the lightmaps were computed on all the receiver surfaces and contain local shadowing information.

![Reduce Lightmap Mixing On Smooth Surfaces Off](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36038ca2-1042-4073-86bc-aef59c2f23d6/12-capt-refl-rlm-on-sm-off.png)

![Reduce Lightmap Mixing On Smooth Surfaces On.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8166d9be-95d3-4947-80fa-cafdaa76f42b/13-capt-refl-rlm-on-sm-on.png)

While lightmap mixing works well for rough surfaces, this method breaks down on smooth surfaces as reflections from Reflection Capture Actors no longer match reflections from other methods like Screen Space Reflections or Planar Reflections. Because of this, lightmap mixing is no longer applied to very smooth surfaces. A surface with Roughness value of 0.3 will get full lightmap mixing, fading out to no lightmap mixing by Roughness 0.1 and below. This also allows Reflection Captures and Screen Space Reflections to match better and make it harder to spot transitions between the two.

### Lightmap Mixing and Existing Content

By default, lightmap mixing will be enabled which means it will affect existing content. In cases where you had reflections leaking on smooth surfaces, that leaking will be more apparent. To solve this, you can either place additional Reflection Capture Actors around the level to help reduce the leaking. Or you can revert to the old lightmap mixing behavior. For this click **Edit** on the **Main** menu panel and select **Project Settings**.

![Open Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6713680f-3b72-4099-a34b-2ed99979497c/14-capt-refl-open-project-settings.png)

Navigate to the **Engine > Rendering > Reflections** and then un-check **Reduce lightmap mixing on smooth surfaces**.

Click image for full size.

You can fine tune the amount of lightmap mixing that will take place by adjusting the following commands using the UE console.

-   **r.ReflectionEnvironmentBeginMixingRoughness (default = 0.1)**
-   **r.ReflectionEnvironmentEndMixingRoughness (default = 0.3)**
-   **r.ReflectionEnvironmentLightmapMixBasedOnRoughness (default = 1)**
-   **r.ReflectionEnvironmentLightmapMixLargestWeight (default = 1000)**

## Editing Reflection Probes

When making edits to Reflection Probes there are a number of different things that you must remember to do to ensure that you get the results you are after. In the following section we will cover what these things are and how you can make sure you are getting the best quality reflections in your projects.

### Using a Custom HDRI Cubemap in a Reflection Probe

Reflection Probes have the ability to not only specify which cubemap they should be using for reflection data but also what size that cubemap should be. Previously UE hard-coded the resolution of the cooked cubemaps reflection probes would use. Now developers can choose the resolution that best suits their needs based on performance, memory, and quality tradeoffs. Below is a comparison image that shows the difference between using the **Captured Scene** option versus the **Specified Cubemap** option.

![Captured Scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9d8019b-08b2-408d-b96d-623c2ec895f0/16-capt-refl-capture-scene.png)

![Specified Cubemap](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f30b7df-0be6-4025-b854-04d7d37d1f15/17-capt-refl-specified-cubemap.png)

To specify a custom HDRI Cubemap for your project's Reflection Probes to use you will need to do the following:

1.  First, make sure that you have an HDRI Cubemap Texture available for use. If you do not have an HDRI Cubemap Texture in your project, one comes bundled with the Starter Content called **HDRI\_Epic\_Courtyard\_Daylight**.
    
    ![Select HDRI Asset in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/201a3992-e5e6-4353-bcdd-7691333711f6/18-capt-refl-select-hdri.png)
2.  Navigate to the **Place Actors** panel and in the **Visual Effects** tab, select and drag a **Sphere Reflection Capture** Actor to the Level.
    
    Click image for full size.
    
3.  Select a **Reflection Probe** Actor that has been placed in the Level and in the **Details** panel under the **Reflection Capture** section change the **Reflection Source Type** from **Captured Scene** to **Specified Cubemap**
    
    Click image for full size.
    
4.  With the Reflection Probe still selected in the Level, go to the **Content Browser** and select the HDRI Texture you want to use. Then in the **Reflection Capture** Actor, under the **Reflection Capture** drag the HDRI Texture from the **Content Browser** to the **Cubemap** input.
    
    Click image for full size.
    
5.  Click **Build** on the **Main** menu panel and select **Build Reflection Capture** to use the new HDRI Cubemap Texture that was just specified.
    
    Click image for full size.
    

### Adjusting Reflection Probe Resolution

You can globally adjust the resolution of the HDRI Cubemaps that are used for the Reflection Capture Actors by doing the following:

1.  Open up your **Project settings** by going to the **Main Toolbar** and then selecting **Edit > Project Settings**.
    
    ![Open Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78eb4201-d095-40d0-b657-ba1badc1bc01/14-capt-refl-open-project-settings.png)
2.  From the **Project Settings** menu go to the **Engine > Rendering** section and then look for the **Reflections** option. By adjusting the **Reflection Capture Resolution** option you can increase or decrease the size of the HDRI Cubemap Texture that was specified.
    
    Click image for full size.
    
    Please note that the Cubemap Resolution will only work with numbers that are powers of 2 like 16, 64, 128, 256, 512, and 1024. When using values other than a power of 2, it will be rounded to the nearest accepted resolution value. Also, be extremely careful when using high resolution values as it will dramatically affect performance due to the GPU memory requirements.
    

The following images show what how the reflections will look when the Reflection Capture Resolution is set to **1**, **4**, **8**, **16**, **32**, **64**, **128**, **256**, **512** and **1024**.

         ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a44895e-d931-4cff-9b96-f23de401aab6/33-capt-refl-rcr-1.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3758aa60-0eb4-4a02-948e-6c370602a515/34-capt-refl-rcr-2.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8150ed6b-d713-465b-a379-034a76a44d04/35-capt-refl-rcr-3.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60fe57b7-b406-492d-93cb-9bcfac68eabc/36-capt-refl-rcr-4.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58cb3aa6-9ce5-41aa-9fb8-6ef1416a8392/37-capt-refl-rcr-5.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae0a83bd-8837-4266-b510-2af7ff989c73/38-capt-refl-rcr-6.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89a0808b-04c9-45ab-9b10-5138b5342052/39-capt-refl-rcr-7.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0210d20f-6c32-4e48-ba8f-b5dcafcaa832/40-capt-refl-rcr-8.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ca0524a-1c82-4cf5-bff8-27ef97a6e021/41-capt-refl-rcr-9.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af869fd1-9e91-4b22-8353-64e76566f0d6/42-capt-refl-rcr-10.png)

**Drag the slider to see how the different resolutions affect the look of the reflection.**

### Adjusting Skylight Reflection Resolution

Like with the Reflection Probes, Skylights also have the ability to define and adjust the resolution of the HDRI cubemap that they use for reflections. To utlize this functionality in your UE project you will need to do the following:

1.  From the **Place Actors** panel in the **Lights** tab, select and then drag a **Skylight** into your Level.
    
    Click image for full size.
    
2.  Select the Skylight and in the **Details** panel under the **Light** section, disable the **Real Time Capture** and then change the **Source Type** to **SLS Specified Cubemap**.
    
    Click image for full size.
    
3.  Click on the drop down box in the **Cubemap** section and select an HDRI cube map from the list.
    
    ![Select HDRI cubemap texture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1826f36-f0a0-4a97-aa25-97d337da0ae6/26-capt-refl-select-cubemap-texture.png)
4.  After the cubemap has been selected you can adjust its resolution by changing the value in the **Cubemap Resolution** input.
    
    ![Change Cubemap Resolution](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58cd4bbd-e4c2-4616-a99a-1e6a82dc9573/27-capt-refl-change-cubemap-resolution.png)
    
    Please note that the Cubemap Resolution will only work with numbers that are powers of 2 like 16, 64, 128, 256, 512, and 1024. When using values other than a power of 2, it will be rounded to the nearest accepted resolution value. Also, be extremely careful when using high resolution values as it will dramatically affect performance due to the GPU memory requirements.
    

### Blending Multiple Reflection Probe Data

You can blend between multiple different cubemap reflections by providing the Reflection Capture Actors with different HDRI cubemaps. To accomplish this in your UE project all you need to is the following:

1.  First, make sure that you have at least one **Reflection Probe** added to your Level and that you have changed the **Reflection Source Type** to **Specified Cubemap** and input an HDRI Texture into the **Cubemap** input.
    
    Click image for full size.
    
2.  Duplicate or add a new Reflection Probe to the Level and position / adjust its **Influence Radius** it so that part of it's yellow influence radius is intersecting with the first Reflection Probe.
    
    Click image for full size.
    
3.  Select the newly duplicated / created Reflection Probe Actor and in the **Details** panel under the **Cubemap** section change the HDRI cubemap to a different one.
    
    Click image for full size.
    
4.  Click **Build** on the **Main** menu panel and select **Build Reflection Capture** to use the new HDRI Cubemap Textures that were just specified.
    
    Click image for full size.
    

### Visualizing

The Reflection Override viewmode has been added to make it easier to see how well the reflections are set up. This viewmode overrides all normals to be the smooth vertex normal, and makes all surfaces fully specular and completely smooth (mirror like). Limitations and artifacts of the Reflection Environment are also clearly visible in this mode so it is important to switch to Lit periodically to see what the reflections look like in normal conditions (bumpy normals, varying glossiness, dim specular).

![Reflection Override](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a59d053-2e58-42fc-b7c3-c00da7f6f52b/32-capt-refl-reflection-override.png)

Some new show flags have been added which are useful for isolating down the components of the lighting:

| Flag | Description |
| --- | --- |
| **Lighting Components > Diffuse** | Disabling diffuse will hide diffuse contribution from all lighting methods. |
| **Lighting Components > Specular** | Disabling specular will hide specular contribution from all reflection methods. |
| **Lighting Features > Reflection Environment** | This will disable the Reflection Environment feature, but other reflection features will still be active (SSR, analytical specular). |

## Performance Considerations

The Reflection Environment cost is only dependent on how many captures influence the pixels on the screen. It is very similar to deferred lighting in this sense. Reflection captures are bounded by their influence radius and therefore they are culled very efficiently. Glossiness is implemented through the cubemap mipmaps so there is little performance difference between sharp or rough reflections.

## Limitations

-   Reflections through this method are approximate. Specifically, the reflection of an object will rarely match up with the actual object in the level due to projection onto simple shapes. This tends to create multiple versions of that object in reflections as many cubemaps are being blended together. Flat, smooth surfaces that cause mirror reflections will show the error very noticeably. Use detail normal maps and roughness to help break up the reflection and these artifacts.
-   Capturing the level into cubemaps is a slow process which must be done outside of the game session. This means dynamic objects cannot be reflected, although they can receive reflections from the static level. If quality is a consideration, light functions can be enabled (`r.reflectioncapture.enablelightfunctions 1`) to improve volume and complex lighting capture at lighting build, or level start.
-   Only the level's diffuse is captured to reduce error. Purely specular surfaces (metals) will have their specular applied as if it were diffuse during the capture.
-   There can be significant leaking when there are different lighting conditions on both sides of a wall. One side can be setup to have correct reflections, but it will always leak into the other side.
-   Due to DX11 hardware limitations, the cubemaps used to capture the level are all 128 on each side, and the world can have at most 341 reflection captures enabled at one time.
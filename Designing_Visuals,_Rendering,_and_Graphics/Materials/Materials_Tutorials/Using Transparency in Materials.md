# Using Transparency in Materials

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-transparency-in-unreal-engine-materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-transparency-in-unreal-engine-materials)  
**Processed:** 2025-06-14 17:02:22

---

When creating certain surface types such as water or glass, you need the ability to make the surface not only see through, but also give the surface a sense of depth and color. In the real world, these properties are referred to as **Transparency** or **Opacity** and the two often used interchangeably to describe the same thing. In Unreal Engine, **Transparency** and **Opacity** have two distinct meanings.

-   **Transparency** is used to define whether or not a surface can be seen through.
-   **Opacity** is used to define degree to which a surface transmits light. In other words, the opacity value determines how transparent or opaque (how see-through / hon see-through ) a surface is.

In the following tutorial you will learn everything you need to know about how to use transparency in your Unreal Engine Materials.

## Transparency

**Transparency** is the term used to describe a surface's ability to block or allow the passage of light. For example, a brick is an object that has no transparency. Stained glass transmits some but not all light, and therefore it is a surface with transparency. You can use transparency to simulate a variety of different real world surface types, including those listed below.

-   Hair
-   Glass
-   Water
-   Smoke or Fire Visual Effects
-   Clouds
-   Impact Decals
-   Foliage

## Transparency and Opacity

In Unreal Engine, transparency works by assigning each pixel an **Opacity** value between 0 and 1. When **Opacity** is 1, the surface is fully opaque, meaning it blocks 100% of the light that hits it. When **Opacity** is 0, the surface allows all light to pass through. Opacity values between 0 and 1 yield pixels that are partially see-through. The image below shows opacity values increasing from 0 to 1 on a Static Mesh.

![Opacity values scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9a492a7-18b4-4e32-9fb0-047a65b0292a/trans_opacity_settings.png)

You can also define opacity with a greyscale texture. The image below demonstrates how a texture can help define which parts of a mesh should have transparency and how transparent they should be. The texture is a gradient that goes from black at the top (or fully transparent) to white at the bottom (or fully opaque). The areas in the middle have a varying degree of opacity based on how close to black or white the pixel in the texture is.

![Opacity ramp](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3fda9b33-afae-417b-8ed3-eeaa0935b8fa/trans_ramp_example.png)

## Using Transparency in Materials

You can set up transparent Materials using the following steps:

This tutorial uses assets from the Unreal Engine **Starter Content**. If you did not include the Starter Content in your project, read the [Migrating](/documentation/en-us/unreal-engine/migrating-assets-in-unreal-engine) content page for information about how to move content between projects. This way you can add the Starter Content to your current project and not have to make a new one.

1.  First **Right-Click** in the **Content Browser** and then select **Material** from the **Create Basic Asset** section of the context menu.
    
    ![Create new Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/958c6a4f-778c-40bc-9220-ba732e826bac/create-material.png)
2.  Name the Material **TransparentMaterial** and then open it by **Double-Clicking** the Material thumbnail in the **Content Browser**. The Material Editor opens.
    
3.  Click in the background of the Material Graph to display the Material properties in the **Details** panel. Under the **Material** section change the **Blend Mode** from **Opaque** to **Translucent**.
    
    ![Set translucent blend mode in details properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d8a8eb9-700f-4bf6-aabe-1103697be3c0/translucent-blend-mode.png)
4.  Now that the **Blend Mode** has been correctly set, add the following Material expressions to your graph. You can find the nodes by typing their names into the search bar in the Material palette. Once found **Left-click** and drag them from the palette into the Material Graph.
    
    -   **Vector Parameter** x 1
    -   **Scalar Parameter** x 1
    
    ![Add parameter expressions to graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/889c16d5-bbfd-4316-9cf3-fd39367ab3e2/add-parameter-expressions.png)
5.  Rename the Vector Parameter node to **BaseColor** and give it a color value. Connect the output of the Vector Parameter node into the **Base Color** input on the Main Material Node.
    
6.  Rename the Scalar Parameter to **Opacity** and give it a default value of 0.5. Plug the Scalar Parameter into the **Opacity** input on the Main Shader Node.
    
    ![Completed transparent graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b508cf4-f982-453d-8e40-075dae215a0d/default-transparency-value.png)
7.  Click **Apply** and then **Save** in the Material Editor toolbar to compile the Material and save the asset.
    
    ![Apply and Save Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0a0a9b6-58ba-4375-9b6b-20f18b24e705/save-apply.png)
8.  Find the **TransparentMaterial** asset in the **Content Browser**, right-click the thumbnail and select **Create Material Instance** in the context menu.
    
    ![Create Material Instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/154f2f55-e3fa-494a-aca9-7e2c0bb64b85/create-material-instance.png)
9.  Inside the **Content Browser**, navigate to the **Shapes** folder in the Starter Content. Left-click and drag the **Shape\_Sphere** Static Mesh into the viewport and release the left mouse button to spawn it in the level.
    
    ![Add sphere to level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81e161bb-42af-462e-8ac1-b47cfafa6c23/place-sphere-in-level.png)
10.  Find the **TransparentMaterial\_Instance** asset in the Content Browser. Left-click and drag the Material instance onto the sphere and release the left mouse button to apply it to the mesh.
    
    ![Apply Material to object](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a91edbab-4d1a-4573-a173-137c9e91bfff/apply-transparent-material.png)
11.  Open the Material Instance by **Double-Clicking** on it in the **Content Browser**. In the Material Instance Editor, override the **OpacityAmount** parameter by checking the box next to the parameter name. Once enabled you can adjust the value of **OpacityAmount** to change how transparent the object will be.
    

## Transparency & Reflections

Objects that make use of transparency can display scene reflections if the following options are set. However keep in mind that having a lot of translucent Materials that have reflections enabled could cause performance issues.

1.  Open the **TransparentMaterial** that was created above by **double-clicking** it in the **Content Browser**. In the **Details** panel under the **Translucency** category, change the **Lighting Mode** from **Volumetric NonDirectional** to **Surface TranslucencyVolume**.
    
    ![Surface translucency volume settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/414aa772-2cc1-451a-85e9-5572d5a90890/surface-translucency-volume.png)
2.  Inside the Material Graph, select the **OpacityAmount** parameter and duplicate it twice by pressing **CTRL + D** on the keyboard. When completed, your Material Graph should look something like this.
    
    ![Duplicate Material expressions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e6a90fc-414e-4868-a76b-8204aea27b42/duplicate-expression.png)
3.  Rename the new Material Expression nodes to **Metallic** and **Roughness**. Set the default value of the **Metallic** Material Expression to 1.0 and set the default value of **Roughness** to 0. Then connect each Material Expression node to the corresponding input on the Main Material Node.
    
    ![Translucent reflective Material graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab47be85-8d32-4b90-8878-5a2df49227ea/metallic-roughness-defaults.png)
4.  Click **Apply** and **Save** the Material Editor toolbar and then close the Material Editor.
    
    ![Apply and Save Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d266d25-c8e5-4641-9d2b-60362fcd0d3e/save-apply.png)
5.  You should now be able to see reflections on the spheres in your level.
    
    ![Transparent Material with reflections in level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36daeb5d-d4a5-4ecb-bc98-5af02a3323a7/transparent-reflective-example.png)

By adjusting the parameters of the Material Instance, you can make the Transparency have extremely different looking results.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00cac85a-d785-4581-8c7d-f90372f56c47/trans_reflection_different_results.png)

## Tinted or Colored Transparency

With the **Thin Transparent** Shading Model and Material expression, you can accurately represent tinted and colored transparent Materials, such colored glass and plastics. This Shading Model enables white specular highlights with correctly tinted background color for transparent surfaces.

![Standard Translucent Shading Model](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fadaeef6-3578-4d2d-a29d-5d6539fbfe37/transparency.png)

![Thin Translucent Shading Model](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c870a340-d14b-43a8-9ce5-7a5f3fd449d8/thintransparency.png)

An example of a Thin Translucent Material Graph is shown below.

Click to enlarge image.

Configure the Material with the following properties in the **Details** panel:

-   Change the **Blend Mode** to **Translucent.**
-   Change the **Shading Model** to **Thin Translucent.**
-   In the Translucency category, change the **Lighting Mode** to **Surface ForwardShading.**

Add a **Thin Translucent Material** expression to the graph and connect a Constant3Vector or a Vector Parameter to the input. This node controls color tint of the transparent surface.

## Translucent Colored Shadows

Translucent Materials are able to cast colored shadows with light transmission in some cases. The amount of light that passes through the Material is determined by its opacity values and how much light is being cast onto the Material.

![Translucent colored shadows](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5ee3474-7c91-461e-82fa-65083e84b500/colored-translucent-shadows.png)

Translucent colored shadows is currently only achievable with [Static Lighting](/documentation/en-us/unreal-engine/static-light-mobility-in-unreal-engine) and [Lightmass](/documentation/en-us/unreal-engine/lightmass-basics-in-unreal-engine).

For additional information and usage, see [Using Colored Translucent Shadows](/documentation/en-us/unreal-engine/using-colored-translucent-shadows-in-unreal-engine).

## Transparency & Performance

![Shader complexity viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc8ffd1b-0d72-4e98-94b2-2337a589589c/trans_shader_complexity.png)

Transparency, especially lit transparency, can quickly become a performance bottleneck if there are too many transparent objects in a scene. The term used to describe this problem is overdraw. **Overdraw** occurs when you have lots of objects with Transparency rendering on top of one another. The reason overdraw causes such a performance problem is because the cost of redering transparency becomes more and more expensive for each successive layer of transparency that you introduce.

To help you better identify whether this issue is happening and where, Unreal Engine has a special view mode called **Shader Complexity** mode. Shader Complexity mode shows you how complex a given surface is to render by using colors to show complexity. The more green that you see, the cheaper things are to render. The more red that you see, the more expensive that frame is to render. Use the following steps to enable Shader Complexity view mode.

1.  To enable **Shader Complexity**, click the **View Mode** option at the top of the Editor Viewport. By default the view mode is set to **Lit**.
    
    ![View modes menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/604480ba-da30-4377-945d-540fb90db34d/view-modes-menu.png)
2.  Select the **Shader Complexity** option from the context menu.
    
    ![Toggle shader complexity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4dbafdc8-58d4-440b-943a-33545e9fdebb/shader-complexity-toggle.png)
3.  After activating the **Shader Complexity** view mode, the level viewport should look like the video below.
    

Overdraw is demonstrated very clearly in the video as the camera rotates around the transparent spheres in the level. When the spheres are all displayed side by side, there is no overdraw and the viewport is mostly green. When all six spheres are all in the same line of sight, the areas with the most overlap turn bright red to indicate overdraw. While it is not 100 percent possible or advisable to get rid of all overdraw, this view mode can make it very helpful when trying to figure out exactly where your performance issues could be coming from.

## Translucency Sort Priority

When there are multiple transparent objects in a scene close together, you may notice that the engine sometimes has issues determining which object to render in front or behind the other transparent objects. The following example demonstrates this happeing using the Materials from above and the lit steam VFX from the Starter Content.

Notice how the steam initially renders in front of the meshes and then suddenly pops behind each sphere. To prevent this from happening, the **Translucency Sort Priority** needs to be set so that the VFX of the smoke will always render on top of other translucency in the scene. To change the **Translucency Sort Priority** on the VFX, do the following.

1.  First select the object or objects that you want to render on top of all other Translucency in the level. In this case, select the VFX particle system.
    
    ![Select particle system in viewport.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16ad5729-0b9c-43a5-9e6a-7d06fb27701a/select-particle-system.png)
2.  In the **Details** panel, navigate to the **Rendering** section and then expand the **Advanced** subcategory.
    
    ![Advanced rendering settings in Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bc10454-0dc9-4a90-842b-9ff99865bb8c/advanced-rendering-settings.png)
3.  From the new list of options, look for **Translucency Sort Priority** and then input a value of **100**.
    
    ![Translucency sort priority settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/711bdbce-ec6c-40c3-a054-a8f6ad9c9669/translucency-sort-priority-settings.png)
    
    By default, everything that is added to a level has a **Translucency Sort Priority** of 0. If you want something that is transparent to always draw over the top of everything else that is transparent, use positive numbers. If you want something that is transparent to always draw behind everything else that is transparent, use negative numbers.
    
4.  Now check out the steam VFX in the scene. With a **Translucency Sort Priority** set to 100, the steam will always draw on top of the other translucent objects.
    
5.  Setting the **Translucency Sort Priority** to -100 makes it so that the steam always draws behind other translucent objects.
    

While adjusting the **Translucency Sort Priority** can fix sorting issue in the level, it could introduce new sorting issues when spawning effects or objects during game play. Because of this, it is a good idea to define what **Translucency Sort Priority** number to use and where. For example, you could say that all spawned effects will have a **Translucency Sort Priority** of 100. So, if there are some sorting issues in the level, you can adjust the objects in the levels **Translucency Sort Priority** to be any number up to 99. This way, the spawned game effects will always render on top of everything else no matter what **Translucency Sort Priority** objects in the level have.

## Conclusion

Transparency is a very powerful tool that can help to make your 3D projects come to life. Remember to try and keep the number of transparent objects that use reflections to a minimum whenever possible, as this can easily affecct performance. Finally, make sure to regularly check Shader Complexity mode both in the editor and during game play to make sure that transparency overdraw is kept to a minimum.
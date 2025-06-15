# Using Colored Translucent Shadows

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-colored-translucent-shadows-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-colored-translucent-shadows-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:30

---

This tutorial explains how to configure an Unreal Engine Material to cast colored translucent shadows. There are many applications where this feature is useful, but a common example is the colored light transmitted through stained glass windows.

![Stained Glass example image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/700089f5-3634-48d6-bbcc-7b0c1f899566/translucent_t.jpg)

Translucent shadow color in Unreal Engine.

## Translucent Shadow Color

Translucent Shadow Color is the term used to describe how shadows can be tinted by the color of translucent surfaces they travel through. This is also known as **transmission**. The amount of colored light that is transmitted through a Material is determined by its **Opacity** value between 0 and 1, and the intensity of the light cast onto the Material.

-   For example, if the Opacity value is set to **0**, the Material is fully transparent and would not transmit any color or cast any shadows.
-   If the Opacity is set to **1**, the Material is fully opaque and transmits no light at all.
-   When the Opacity value is something **between 0 and 1**, the light transmitted through that object is tinted by the **Base Color** of the Material, and the shadows inherit some of the color.

### Compatibility with Various Lighting Systems

Translucent Shadow Color is not supported by every one of Unreal Engine's lighting and [global illumination](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine) systems. The chart below breaks down which lighting features support translucent colored shadows.

| Lighting System | Translucent Colored Shadows |
| --- | --- |
| CPU Lightmass | Yes, Static lights only |
| GPU Lightmass | Yes, Static lights only |
| Lumen Global Illumination | No |
| Hardware Ray Tracing | No |
| Path Tracer | Yes, requires Thin Translucent Shading Model |

The notable omission on this list is **Lumen Global Illumination**, which does not currently support translucent shadow color.

Because [Lumen Global Illumination](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) is enabled by default in all new UE5 projects, this means you will need to manually disable Lumen in either the **Project Settings** or **PostProcessVolume** if you want to use colored translucent shadows in your Level.

The sections below explain how to setup a scene and Material to cast translucent colored shadows.

## Disabling Lumen in UE5

Use the following steps to disable Lumen Global Illumination in the current Level.

1.  Click the **Create** icon in the toolbar and select **Volumes** > **PostProcessVolume**.
    
    ![Create PostProcessVolume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f7a5b08-5c6e-47ae-8248-7a6c73a97b25/add-post-process-volume.png)
2.  Select the PostProcessVolume in the Level, and in the Details Panel search for **"extent"**. Enable the **Infinite Extent (Unbound)** setting so the PostProcessVolume affects the whole Level.
    
    ![Enable Infinite Extent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abce051e-c95d-4ec0-a2c5-1bfe825f9a8f/infinite-extent-unbound.png)
3.  Search for **Global Illumination** in the Details Panel. Enable the **Method** setting, and use the drop-down to change the Global Illumination Method from **Lumen** to **None**.
    
    ![Global Illumination Method](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a647cb3b-0156-4068-b23f-a4779e7ec7e6/global-illumination-method.png)
    
    This setting disables dynamic Global Illumination in the current Level, however you can still use Lightmass to bake Global Illumination from Static lights.
    

## Lighting Setup

The most important consideration with regard to lighting is that you can only cast colored translucent shadows from a Light Actor with its **Mobility** set to **Static**. You can use any of the following light types.

-   Directional Light
-   Point Light
-   Spot Light
-   Rect Light

All examples on this page use a Directional Light in the Unreal Engine **Time of Day** Level template. Select the **Directional Light** in the Outliner, and change the **Mobility** to **Static** in the Details Panel.

![Static light Mobility](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41d95298-c4e4-4518-ae53-b0e0d27bb6f5/light-mobility-static.png)

Indirect lighting can wash out colored shadows, making them appear less saturated than the Base Color of the Material. If you are having trouble seeing colored translucent shadows in your Level, consider reducing the **Indirect Lighting Intensity** of your light source, or try using a dimmer environment.

## Material Setup

### Material Properties

You can use any of the Blend Modes and Shading Models listed below to cast colored translucent shadows.

-   **Blend Mode:** Translucent, Additive, AlphaComposite, or Modulate
-   **Shading Model:** Default Lit, Unlit, or Thin Translucent

Using the **Modulate** Blend Mode will require you to disable **Mobile Separate Translucency** in the Details Panel properties.

#### Two Sided

Enabling the **Two Sided** property is optional, but it is necessary if you intend the player to view both sides of the mesh with the Material. If **Two Sided** is disabled, the light must be cast onto the visible side of the Material in order for it to cast colored shadows.

### Creating a Lit Translucent Material

1.  Create a new **Material** asset and open it in the [Material Editor](/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide). Click anywhere in the Material Graph to display the [Material Properties](/documentation/en-us/unreal-engine/unreal-engine-material-properties) in the Details Panel.
2.  In the Details Panel, change the **Blend Mode** to **Translucent**.
    
    ![Change Blend Mode to Translucent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0dce96f-c37b-438e-8b59-5af5b737daf9/translucent-blend-mode.png)
3.  Enable the **Two Sided** Material property (optional).
    
    ![Enable Two Sided option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e7c2bac-3908-4b0d-876f-19ecffe3ecc6/enable-two-sided.png)
4.  Scroll down and expand the **Translucency** section. Set the **Lighting Model** to **Surface Translucency Volume**.
    
    ![Translucency Lighting Mode drop-down](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d69888da-6e11-412e-8f8c-8a8ec0d620b7/translucency-lighting-mode.png)
5.  Add a **Texture Sample** to the Material Graph. This example uses a colorful geometric pattern to simulate a stained glass window, but any colorful texture will work. Images with highly saturated colors will produce more vibrant shadows than images with low saturation. Connect the **RGB** Output of the Texture Sample to the **Base Color** input on the [Main Material Node](/documentation/en-us/unreal-engine/using-the-main-material-node-in-unreal-engine).
    
    ![Stained Glass Texture Sample](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b796c77a-41b0-442d-83c2-e8c3070b9f8c/stained-glass-texture.png)
6.  Create a **Scalar Parameter** and rename it **Opacity**. Select the Scalar Parameter and set the **Default Value** to a value between 0 and 1 in the Details Panel. You can also set the **Slider Max** value to **1** to limit the value range of the Opacity slider.
    
    ![Scalar Parameter values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/539becc3-4b20-4c63-906b-f41f47742ae9/scalar-values.png)
7.  Connect the Scalar Parameter to the **Opacity** input. Your Material Graph should look like the image below.
    
    ![Default Lit Material Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24ac0df2-be73-4fa1-970b-ce70cef859ab/default-lit-graph.png)
8.  Click **Apply** and **Save** in the Toolbar to compile the Material and save the asset.
    
    ![Compile and save Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0150c8ce-e118-4ee8-bc87-8262ce9e5872/save-and-apply.png)

## Build Lighting

Close the Material Editor and apply the Material to a Static Mesh in your Level. This example uses a simple plane from the Unreal Engine Starter Content. The Directional Light is angled roughly perpendicular to the plane so the shadow will fall directly onto the ground below.

In the Toolbar go to **Build** > **Build Lighting Only** to bake your lighting. Colored translucent shadows should appear when the Lightmass build finishes.

![Build Lightmass for Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9a4464c-f1a8-47ea-9a07-50ad9a3a56d1/build-lighting-only.png)

### Shadow Sharpness

Several things can affect the sharpness of the shadows, including the lightmap resolution of the mesh receiving the transmitted shadow color, the source angle of the light, and the quality of the texture sample. If your result is blurry and unfocused like the image below, it is very likely the lightmap resolution is too low on the receiving mesh.

![Blurry lighmass results](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91f9e6e3-848b-461e-83c0-3b555599a727/insufficient-lightmass-resolution.png)

Select the Static Mesh upon which the shadows are falling—in this case the Floor asset. In the Details Panel, scroll down to the **Lighting** section. Enable the **Overriden Light Map Res** setting, and enter new Light Map resolution.

![Override Lightmass Resolution](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a66c83c7-ed98-42d2-a722-be0100a24d5d/overridden-lightmass-res.png)

Depending on the size of the static mesh, you may need a relatively large resolution to see sharp shadows. The slider below shows what happens when the Light Map resolution is gradually increased.

   ![Light Map resolution 1024](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/792f725d-f35b-49db-8ab7-6053e429dfb7/lm-256.png) ![Light Map resolution 1024](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9df28c98-1ca8-4620-bcb0-9e7e0d039647/lm-1024.png) ![Light Map resolution 2048](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2aab92f8-95bb-4d72-ad7e-f2ed824fc4cb/lm-2048.png) ![Light Map resolution 3072](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8e37962-b087-4a85-8df2-53033a9b6710/lm-3072.png)

**Light Map resolution increased from 256 to 1024, 2048 and finally 3072.**

In this case there is a drastic improvement from **256** up to **2048**, but diminishing returns when the resolution is pushed to 3072. Larger Light Maps have a performance cost, so be careful not to use a higher resolution than is necessary.

## Material Variations

### Opacity and Shadow Saturation

The Opacity value of the Material will affect the saturation and intensity of the shadows. In the comparison below, the three slides show what happens when the **Opacity** value is increased from 0.2 to 0.9. In an outdoor environment like this, the colored shadows are easier to see with higher Opacity values. However, in a dim interior lower opacity values may yield better results.

  ![Opacity Value 0.2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41e3ded7-43c8-4fa3-97cc-7d81d0c69c92/opacity-02.png) ![Opacity Value 0.5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4bbe5ca7-6400-499a-a0d8-f423474a574d/opacity-05.png) ![Opacity Value 0.5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/139de39d-7f3b-416b-9eab-3bc2ff122cca/opacity-09.png)

**Material Opacity at 0.2, 0.5, and 0.9.**

### Masked Opacity

Opacity masks work as expected when casting colored translucent shadows. You can use the alpha channel of a texture, or plug a black and white texture into the **Opacity** input to control which parts of the Material are visible and cast shadows. If you are unfamiliar with the process, read more about [texture masking here](/documentation/en-us/unreal-engine/using-texture-masks-in-unreal-engine).

The example below shows a masked Material casting colored translucent shadows. None of the Material properties were changed, but the Material graph was modified as shown below.

![Colored Shadows with Opacity Mask](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4935cef6-7f67-45a4-8866-ad89dcee27d4/masked-graph.png)

Instead of plugging the **Opacity** Scalar Parameter directly into the Main Material Node, it is multiplied by a black and white Texture Sample. The black regions of the mask are transparent, while the white circular region is visible.

This is the result after the lighting is rebuilt.

![Colored translucent shadows from masked Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eeda7a78-53a5-448f-b30d-57df8665e953/masked-result.png)

## Colored Shadows with the Path Tracer

The Path Tracer is Beta feature and requires several settings to be enabled in Project Settings. Read about enabling the Path Tracer [on this page](/documentation/en-us/unreal-engine/path-tracer-in-unreal-engine).

Dynamic colored shadows are supported by the Path Tracer, but only when the Material uses the **Thin Translucent** Shading Model. Follow the steps below to modify the above Material so it can cast colored translucent shadows with the Path Tracer.

1.  Click anywhere in the background of the Material Graph to display the Material Properties in the Details Panel.
2.  Change the **Shading Model** to Thin Translucent.
    
    ![Thin Translucent Shading Model](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06fde025-df21-4d53-a136-e1e809850a54/thin-translucent-sm.png)
3.  Scroll down to the **Translucency** section and change the **Lighting Mode** to **Surface Forward Shading**.
    
    ![Surface Forward Shading](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41205efd-f179-4724-9cdb-8f375aa22a29/surface-forward-shading.png)
4.  Search for "thin translucent" in the right-click menu or Material Palette and add a **ThinTranslucentMaterialOutput** node to your graph.
    
    ![Thin Translucent Material Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7c1cd81-34e3-4e7a-9489-9c93f9c95f48/thin-translucent-node.png)
5.  Drag a second connection from the **RGB** output of the Texture Sample to the **Transmittance Color** input on the Thin Translucent Material node. The rest of the graph is unchanged from previous examples, and should look like the image below.
    
    ![Thin Translucent Material Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8f5c168-5950-409d-87df-88743ef50eed/thin-translucent-material-graph.png)
6.  Compile the Material and apply it to a mesh in your Level.

The video below shows the results of the Thin Translucent stained glass Material when the Path Tracer is enabled. The colored shadows are fully dynamic in Path Tracing mode and update immediately if the plane or light source are rotated. The video also demonstrates what happens when changes are made to the Opacity of the Material and Source Angle of the Directional Light.
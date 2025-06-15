# Using Refraction

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-refraction-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-refraction-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:46

---

When light passes from one medium to another, say from air to water, the direction that that light is traveling is altered where the two mediums meet. This lighting phenomenon is referred to as refraction and happens because the speed of a light wave can change when the light passes into a different type of Material. In Unreal Engine you can simulate this lighting phenomena in your Materials by using the **Refraction** input on the [Main Material Node](/documentation/en-us/unreal-engine/using-the-main-material-node-in-unreal-engine).

## Refraction

**Refraction** is the term used to describe the change in direction of a light wave due to a change in its transmission medium. In other words, when light comes in contact with certain surfaces, like water or glass, the light is bent or redirected because those surfaces affect the speed at which light travels through them.

You can see a classic example of refraction by dipping a pencil into a bowl of water. The pencil will appear to bend or change directions at the spot where the pencil intersects the water. The illustration below shows how refraction works.

![Refraction illustration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4f24b39-96f8-40b7-9481-6ff32df731cc/r_refraction_example.png)

**X** shows the true physical position of the pencil when it is dipped in water. The light rays from the submerged portion of the pencil are refracted at the air-water interface, changing speed and direction. From the camera's perspective, the pencil appears to bend at the surface of the water, with the tip appearing at position **Y** instead of its true position **X**.

## Index of Refraction or IOR

**Index of Refraction** or IOR is an optical measurement that describes the extent to which light is bent, or refracted, when it enters a particular Material. Index of refraction can be measured, and real-world values for common surfaces are well known. When creating refractive Materials in Unreal Enging, it is best to use real-world IOR values to give your Materials a better sense of realism. The table below lists measured IOR values for some common surface types.

| Material | IOR Value |
| --- | --- |
| **Air** | 1.00 |
| **Water** | 1.33 |
| **Ice** | 1.31 |
| **Plexiglass** | 1.49 |
| **Glass** | 1.52 |
| **Diamond** | 2.42 |

## Using Refraction in Materials

Follow the instructions below to create a Material that uses refraction.

This tutorial uses assets from the Unreal Engine Starter Content. If you did not include the Starter Content in your project, read the [Migrating Assets](/documentation/en-us/unreal-engine/migrating-assets-in-unreal-engine) page to learn how to migrate the Starter Content into your current project.

1.  **Right-click** in the **Content Browser** and select **Material** from the Create Basic Asset section in the context menu. Rename the Material **RefractionMaterial**.
    
    ![Create Material asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2a80ac6-b288-4b79-95f0-2300fa03df20/create-material.png)
2.  **Double-click** the Material asset to open it in the Material Editor.
    
    ![Open Refraction Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33484bf1-a3ee-44ea-8f83-e81506e00d95/double-click-open.png)
3.  In the Details Panel, change the **Blend Mode** from **Opaque** to **Translucent.** Expand the Translucency section and change the **Lighting Model** from **Volumetric Non Directional** to **Surface Translucency Volume**. Changing these settings will enable the **Refraction** pin on the Main Material Node. When completed, your **Details** panel properties should look like this.
    
    ![Details panel properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6393b850-eabd-42f7-b176-3b06cc349fb0/details-panel-properties.png)
4.  Search for the following Material Expression nodes and add them to your graph in the quantites listed below. Your Material Graph should look like the image below.
    
    -   **Constant** x 3
    -   **Scalar Parameter** x 2
    -   **Lerp** x 1
    -   **Fresnel** x 1
    
    ![Material Graph with required nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3b30d59-72a4-489a-ab54-ba296bd7f220/required-nodes.png)
5.  Begin wiring up the Material as shown below. Change the Constant value flowing into Base Color and Metallic to **1**. Rename one of the Scalar Parameters **Opacity,** give it a default value of **0.3** and connect it to the Opacity input.
    
    ![Base Color, Metallic, Roughness nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c55eefe3-b8a2-47a2-afee-74f3c8a1f064/pbr-values.png)
6.  Rename the second Scalar Parameter **IOR** and change its default value to **1.52** (the IOR of glass). Finish wiring up the Material as shown in the outlined portion of the image.
    
    ![Fresnel refraction logic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44c71e9d-c4ae-4322-bc35-1647a2f28042/fresnel-logic.png)
    
    Because glass does not refract light the same way from all viewing angles, a **Fresnel** Material Expression is used to blend between the two values in the **Lerp** node. Glass does not refract as much light when viewed straight-on, but produces noticeable refraction at glancing angles. The Fresnel node reproduces this effect — the **Constant** value in input A is mapped to the center of the Material, and the **IOR parameter** in input B is mapped to the edges where the sphere curves away from the camera.
    
    Read the page on [Using Fresnel in Materials](/documentation/en-us/unreal-engine/using-fresnel-in-your-unreal-engine-materials) for a better understanding of how the Fresnel Material Expression works.
    
7.  Click **Apply** and **Save** in the Toolbar to compile the Material and save the asset. After the Material is saved you can close the Material Editor.
    
    ![Compile and save Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/863c1261-c37d-4e22-aaec-a476372915e3/save-and-apply.png)
8.  Find the **RefractionMaterial** asset in the Content Browser, **right-click** on the thumbnail and select **Create Material Instance** from the context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35464128-e502-4fc2-8366-8c104e96fb05/create-material-instance.png)
9.  Drop a few objects into your scene to test the Material. The example below uses assets from the **Shapes** folder in the **Starter Content**, but any object is suitable. Drag the **RefractiveMaterial\_Inst** asset from the Content Browser onto the meshes in your scene. Note how the sphere appears to refract light at the edges, but not in the center where the geometry is directly in front of the camera. This is the result of the Fresnel logic described above.
    
    ![Apply refractive Material instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7d83b9c-9e3b-4221-a972-e113deeee854/apply-refractive-material.png)
10.  Double click on the **RefractionMasterial\_Inst** to open it in the Material Instance Editor. Enable the **IOR parameter** by checking the box next to the parameter name. Once enabled, you can set the IOR to different values to simulate different surface interaction. The video below shows how the refraction changes when the value is set to 1.0 (air), 1.33 (water), 1.52 (glass), and 2.42 (diamond).
    

## Refraction Tips & Tricks

This section presents some ways you can use Refraction in combination with other aspects of the Material Editor to create complex and interesting refractive surfaces.

### Refraction & Normal Maps

Adding an option to use a normal map with your refractive Material will yield some very interesting results, especially in areas where the Normal map has a lot of interesting detail. Follow the steps below to modify the **RefractiveMaterial** created above so that it works with normal maps.

1.  First find a normal map to use. For this example, **T\_Water\_N** from Starter Content was used, however any normal texture will work. Open the **RefractionMaterial** asset and drag the normal texture from the **Content Browser** into the Material Graph.
    
    ![Add normal map to graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f47a2cb3-50d4-4004-a054-ea982ed582df/add-normal-map.png)
2.  **Right-click** on the normal map Texture Sampler and select **Convert to Parameter.** Rename the parameter **Normal Map** and connect it to the **Normal** input on the Main Material Node. By parameterizing the texture, you give artists a way to override it in a [Material Instance](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) without editing the parent Material.
    
3.  Click **Apply** and **Save** in the Toolbar and then close the Material.
    
    ![Compile and save Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a05a016-4859-4c64-bdfb-1bfd178e2d3d/save-and-apply.png)
4.  In the Material Instance Editor you should now see the **Normal Map** parameter listed under Global Texture Parameter Values. You can override the Normal Map by enabling the parameter and choosing a different texture from the drop-down menu.
    
    ![Normal Map parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66b01cd6-2325-4bde-8789-bacee314f8f4/normal-map-parameter.png)
5.  By changing the Normal map, you can change the Material's refraction in interesting ways. Here are some examples using only the Normal maps you can find in the Textures folder of the Starter Content.
    
    ![Normal Map examples](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24af5f24-42bf-428e-91ae-e5985dce895a/r_reflection_-_normal_maps.png)

### Refraction and Movement

Combining refraction with motion is a key component in many types of Materials. Ripples on water are one example, but the technique is similarly useful in a lot of VFX Materials such as heat haze, distortion from a large explosion, or energy effects.

The graph below shows one way to add organic looking motion to the normals. Duplicate the normal map, and connect them to the A and B inputs on a Lerp node. Add two **Panner** Material Expressions to the graph and connect them to the UVs of the normal map textures.

![Normal map animation graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/050e15a6-a35a-48b3-88a6-7c01c2f8225c/normal-map-animation.png)

Change the values in the **Panner** nodes to add motion to the textures. Making some of the values negative moves the texture in the opposite direction, and is a good way to create organic, random looking motion. Here are the values used for the two Panners in this example.

![Panner motion values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f653f189-ce26-4df1-926e-a813f29aa243/panner-values.png)

The result is shown in the video below. In its current state it resembles an oily, metallic looking fluid, but with some modifications it could be the basis for a water Material.

### Refraction Depth Bias

**Refraction depth bias** is a way to prevent closer objects from rendering into the distorted surface at acute viewing angles. However this can increases the disconnect between the surface and where the refraction starts. You can adjust the **Refraction Depth Bias** in the following two places.

-   **Material Editor** - You can find the **Refraction Depth Bias** in the **Details** panel under the Material section. You will need to press the white triangle (Highlighted in Green) to expose this property.
    
    ![Refraction Depth Bias in Material Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/213cbbb2-cfed-4924-8233-d73f6c40c5d1/refraction-depth-bias.png)
-   **Material Instance Editor** - You can find the **Refraction Depth Bias** in the **General** section of the **Details** panel.
    
    ![Refraction Depth Bias in Instance Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4881bad7-53dc-4d23-9ea0-b5e050f3bf2e/refraction-depth-bias-instance.png)

## Conclusion

Adding refraction to your Materials is a great way to get realistic looking results for translucent Materials like glass and water. Remember to consult the choart at the top of the document and use correct IOR values for the type of surface you are trying to simulate. IOR values come from real world measurements, so pushing the IOR higher or lower than what it is supposed to be is not recommend if you are striving for realism. In VFX and other looser applications of refraction, you can of course experiment and use values that suit your desired aesthetic.
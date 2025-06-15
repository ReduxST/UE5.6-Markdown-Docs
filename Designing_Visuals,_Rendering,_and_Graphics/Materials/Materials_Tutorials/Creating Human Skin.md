# Creating Human Skin

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-human-skin-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-human-skin-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:33

---

![Not using SubsurfaceProfile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ff88467-3616-4ec5-b6ce-76b3df2762b7/results_1.png)

![Using SubsurfaceProfile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49e944da-c285-4e97-aa1a-a627b08c6bd6/results_2.png)

Getting Human skin to look correct when rendered is a very complex topic with no single perfect solution for getting correct results. Because of this, please treat the following information *as a starting point* for your work as many things are needed in order to achieve a realistic looking image. This is because our eyes are very well trained at detecting subtle details in human faces. Getting it right is challenging but once the tools are mastered, they can be applied in many other cases.

## Setup

Before we get to making the Material, first we should gather some reference. This is because it is usually best to start with multiple photo references that have multiple lighting situations so you can verify how the material looks under different lighting conditions. If at all possible, having scanned and calibrated source data would be ideal as this will help to make sure that you are getting the best possible results. When viewing your content inside the editor, make sure to disable the **Editor Eye Adaptation** for a more controlled environment: *Edit Menu > Project Settings > Rendering > Default Post Processing Settings > Auto Exposure*

A calibrated environment can be helpful in making sure that you get the colors correct but it is not required.

For the following example, we will be working with the Skin Rendering Content example. If have not done so, please go ahead and download the Content Examples from the Marketplace now and open up the Skin Rendering Map. Also please keep in mind that the images in this document are explicitly low resolution and are not meant to be used as source work.

It is extremely important that you make sure the Normal Map is correctly setup for use inside Unreal Engine. Some engines use a Normal Map where the green channel has been inverted. You can check to see if the green channel of your Normal Map has been inverted or not by comparing the colors in the following image to your Normal.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5bfb6f23-7f7a-490b-bdcf-68daddb84a12/normalsetup.png)

Here is a list of some things that you need to be aware of before you begin to create your Skin Textures and Materials.

-   Remember that when creating textures, it would be ideal if you start with very high resolution textures (e.g. 2Kx2K or higher) as this will give the best results.
-   For faster iteration, it is best to create a Material Instance and expose Scalar and Vector Parameters for faster and easier tweaking as the Material does not need to be recompiled during tweaking.
-   Keep in mind that assets should be verified in multiple lighting conditions to ensure that they are correct. Even having Eye Adaptation enabled in the Post Process Volume can make a huge difference in how things look in the end.
-   To avoid shadow artifacts will require extra effort because you will need to tweak things like shadow bias or use a more focused spot light cone for better lighting resolution.
-   When tweaking, it might be useful to zoom in by adjusting the editor FOV as there will be no clipping through geometry and less distortions.
-   The editor Field Of View(FOV) can be adjusted by clicking on the Drop Down Arrow that is next to the icon that says Perspective and then adjusting the FOC value using the mouse.
    
    ![Adjust FOV](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2407ccd2-13b4-48ee-a34e-9735ce2997bc/adjust-fov.png)
-   When viewing your work, you might notice that the streaming system does not take the zoom into account and could blur your texture when you do not want to. This was an intentional design decision made for 3D games but this could change at some point in the future. To prevent this from happening, you can change the texture Streaming Distance Multiplier on the mesh instance.

## Material

Below is an image of the completed Material from the Content Example map. While this Material does look complex, we will be breaking down what each section of the Material does in the following sections.

Click image for full size.

### Base Color

![Base Color graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be68eb98-1f46-4cac-9a77-cd15654a8d6c/base-color-graph.png)

One of the first things that needs to be understood is that from a very far distance, the Subsurface Scattering effect is harder to perceive. This means that it is best to have the Base Color of your texture looking right when viewed in the distance. You could also use a grayscale texture to darken the base color and the specular (caused by occlusion) to give an overall better look to the skin. You can also add some Vector and Scalar controls to adjust the color and power of the skin to help you further tweak to get the look you are after.

### Roughness

![Roughness graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07ce088a-0f81-4d58-8246-de85064c704c/roughness-graph.png)

For skin, it is best to start with a constant Roughness value of around 0.4 and tweak from there. Keep in mind that the actual value depends on scale/distance, age, and wet/dryness of the skin that you are trying to simulate.

Unlike other textures, we explicitly want to have the mip maps look different. This is how such a mip chain can look like:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fd251ae-9b82-4b84-ba22-de1ee450fa03/detailroughness.png)

Notice that the smaller mips have a brighter grey value meaning the material transitions towards a more rougher material. Also keep in mind that this texture can be put into a channel of another texture (saving a texture lookup and texture memory). Ideally this texture should have the same resolution as the Normal Map texture.

### Specular

![Spec Modulation Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4ce69fc-9a22-455b-bedc-42767131fccc/pore-spec-modulation-graph.png)

The Specular value for the skin is set at a value **0.35**. The number 0.35 was used as it was derived from real world Specular values that were measured and then converted into ranges that we use.

### Normal

Click image for full size.

In order for your Normal Map to work correctly for skin, you need to make sure that your Normal map meets the following criteria.

-   The Normal Map that is used for the face should only contain details about wrinkles. Pore details should be done with a tiling texture as you can get better results this way.
-   When combining the object's Normal map with the Detail Normal map, make sure that you use the Material Function BlendAngleCorrectedNormals to combine as you will yield better results. It is also very useful to expose parameters to adjust the mixing of the Normal maps. You can take the detail normal map value, add some scalar value to the z component and normalize. This way you can transition to a flat detail Normal Map from your regular one.
-   As skin has different shading properties in different areas, it is best to combine the Roughness with an object mapped (non-tiled) texture. As the detail Normal map causes the roughness to go up in the distance, we need to compensate for that. We also need to verify the shading at multiple scales / view distances to ensure that it looks good at all distances from the camera.
-   Modern real-time rendering implements shading with per pixel lighting. Normally this leads to very high quality results but for very detailed Normal maps. By using Mip Maps, we avoid shimmering and get a better performance but Mip Mapping does not work well for Normal maps as details in lower mips simply do not exist and the surface appears much more shiny than it should be. To counter that effect, we can adjust the roughness accordingly. This does not capture anisotropic details but for non-directional features, it is a good approximation.

### Opacity

![Opacity graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/297cf39c-b90a-437b-8ec9-a7d415ba9d55/opacity-graph.png)

The Opacity input controls that amount of Subsurface Scattering that is taking place. A value of 1 or pure white means that the Subsurface Scattering should come through at full power. A value of 0 or pure black means no Subsurface Scattering should come through.

### Pores

Click image for full size.

Having the Pores in the skin is a very important detail in getting realistic looking skin. However because the pore detail needs to be very fine, it is very difficult to get the needed quality by just adding the Pores to the base Normal Map.

Adding the Pores as separate tillable textures makes them stand out better but also makes adjusting them is much easier.

For the Pore tiling detail variation in this shader, a TexCoord Material Expression was multiplied with a Scalar Parameter so that inside of the Material Instance we would be able to title the Pores as needed.

Here is a look at what the Pore Mask and Normal Texture Maps look like when viewed close up.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a916548a-1d01-48bc-b285-903c9058a5e4/detailspec.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c6f746d-99e5-4640-b62e-7ec1d9ca74d8/detailnormal.png)

Because pores are little sunken in to the surface areas when viewed from a grazing angle they are actually less visible. We can mimic that fading out the pore contribution based on the angle the surface is viewed. This computation is similar to Fresnel and was implemented like this in the SkinMaster Material.

![Fresnel Mask](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab29937e-d2de-4ea5-be87-614182f47cbf/fresnel-mask.png)

The Material graph components for the skin pores and fresnel effect are blended back into the broader graph using the logic shown below.

Click image for full size.

## Using a Subsurface Profile

The Subsurface Profile is what makes the skin really look like skin. To use a Subsurface Profile in your Material, you just need to supply your Material or Material Instance with the Subsurface Profile that you want to use.

To change this in a Material, all you need to do is supply the Subsurface Profile that you wish to use in the **Details** panel of Material Editor.

![Add Subsurface Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8b796e3-0ee4-41be-b688-5487125de68e/subsurface-profile.png)

To change what Subsurface Profile is used inside of a Material Instance all you need to do is first check the **Override Subsurface Profile** and then supply the Subsurface Profile that you want to use in the **Subsurface Profile** section of the Material Instance.

Click image for full size.

## Useful links

The following links are to external sites that contain a wealth of information on how to create very realistic looking character for games.

[Next Generation Character Rendering](http://www.iryoku.com/stare-into-the-future)

## Conclusion

Setting up and getting skin to render correctly is a long and involved process that will take some time to get just right. Remember that this guide should only be used to help point you in the right direction when it comes to setting up skin. If you find that by using a slightly different setup than what was presented here gives you the results you are looking for that is okay. Again the above information is not something that you have to follow to the letter when setting up skin but should be considered more like guidelines to follow.
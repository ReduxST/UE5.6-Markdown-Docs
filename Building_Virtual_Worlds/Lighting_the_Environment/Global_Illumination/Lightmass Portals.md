# Lightmass Portals

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/lightmass-portals-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/lightmass-portals-in-unreal-engine)  
**Processed:** 2025-06-14 16:33:37

---

![Banner image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7612e765-e9b8-475c-a8b3-d52324e40375/lightmass-portals-banner.png)

When gathering lighting, Lightmass can backtrack to Point, Spot and Directional light sources using photons from the Photon Mapping technique. This means that it can find small windows where light is entering from these light types and resolve the incoming lighting with high-quality. However, SkyLights and Emissive meshes don't support photon emission efficiently, so Lightmass can only find the small important lighting features with brute force. This manifests as splotchy artifacts around indoor corners. To help Lightmass better understand where the light should be coming from, you can place **Lightmass Portals** Actors around the areas that are critical to lighting. In the following document, we will take a look at setting up and using Lightmass Portals in your Unreal Engine projects.

## How It Works

From a high-level, Lightmass Portals work in the following manner:

-   Lightmass Portals are most useful when a scene is lit using a [Skylight](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine), HDR image or a Static Mesh that is set to [Use Emissive for Static Lighting](/documentation/en-us/unreal-engine/using-the-emissive-material-input-in-unreal-engine#usingemissivematerialstolighttheworld) checked.
    
    Click for full image.
    
-   Lightmass Portals are placed and in the level and scaled to fit any open areas that are important to the final lighting.
    
    ![Example of the scene with Lightmass Portals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c5a1683-e8b4-4ab5-bcd7-4d70390cf80d/02-lightmass-portals-example-scene.png)
-   When Lightmass is building the light, the Lightmass Portals tell Lightmass that more light rays should come from this area yielding higher quality light and shadows.
    
    ![Scene without Portals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01c1f189-f679-4821-bd05-6dd9149af2b5/03-lightmass-portals-result-without.png)
    
    ![Scene with Portals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/709088ce-36ea-46f4-993f-22f683506e4e/04-lightmass-portals-result-with.png)
    

## Steps

To use Lightmass Portals in your projects, you will need to do the following.

1.  From the **Place Actors** panel, search for **Lightmass Portal** and then drag the **Lightmass Portal Actor** into your **Level** to place it.
    
    Click for full image.
    
2.  Using the **Move**, **Rotate** and **Scale** tools, position and scale the Lightmass Portal to be about the same size or slightly smaller than the opening or area you want Lightmass to focus more rays towards.
    
    ![Adjusting position and scaleof the Lightmass Portal Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d53c77f-49ff-4694-8637-2742ba28367f/06-lightmass-portals-adjusting-actor.png)
3.  Click the **Build** in the **Main** menu panel, select **Build** and change the **Lighting Quality** to **Production**.
    
    ![Enable production lighting quality](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d63f843b-89a3-4685-a038-89e132bd04cc/07-lightmass-portals-lighting-quality.png)
4.  When that has all been completed, click the **Build** in the **Main** menu panel and select **Build All Levels** to start the Lightmass lighting build.
    
    ![Build the Lightmass lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae51a761-5a64-4a89-acda-a563faecd694/08-lightmass-portals-build.png)

## End Result

Once your Lightmass build has completed, you will have something similar to the following image.

![Scene without Portals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73ab3150-4a4b-4cf8-b36e-e4b740184ea7/09-lightmass-portals-off.png)

![Scene with Portals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba390b6f-6a9d-422d-bc60-912528c3b046/10-lightmass-portals-on.png)

If you take a close look at the **Without Portals** image, you will notice that there is a lot of noise in the image, especially in the darker areas when compared to the **With Portals** image.

## Known Issues and Limitations

-   Lightmass Portals work by forcing Lightmass to send rays toward the portal. Because of this, you should only use Lightmass Portals on small levels and only for lighting that is critical to the scene. Failing to do this (and adding too many Lightmass Portals) can drastically increase your Lightmass build times.
    
-   Only use Lightmass Portals on very small levels as Lightmass Portals are not occluded by anything. Using them in big open world-type levels will result in longer-than-needed light baking times.
    
-   If you are using Static Meshes for Emissive light casters and the results are noisy, place a Lightmass Portal around the area where the Static Meshes' light is supposed to be emitted from.
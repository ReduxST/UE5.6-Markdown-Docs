# Lightmass Basics

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/lightmass-basics-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/lightmass-basics-in-unreal-engine)  
**Processed:** 2025-06-14 16:33:35

---

![Banner Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c340e8f4-bbbb-4ab4-b278-1e89d0ef108f/lightmass-basics-banner.png)

**Lightmass** creates lightmaps with complex light interactions like area shadowing and diffuse interreflection. It is used to precompute portions of the lighting contribution of lights with stationary and static mobility.

## Lightmass Importance Volume

Many maps have meshes out to the edge of the grid in the editor, but the actual playable area that needs high quality lighting is much smaller. Lightmass emits photons based on the size of the level, so those background meshes will greatly increase the number of photons that need to be emitted, and lighting build times will increase. The Lightmass Importance Volume controls the area that Lightmass emits photons in, allowing you to concentrate it only on the area that needs detailed indirect lighting. Areas outside the importance volume get only one bounce of indirect lighting at a lower quality.

![Example of the Lightmas Importance Volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/010a6e16-80b2-4ab6-ae2c-1b8652d02b8f/01-lightmass-basics-importance-volume.png)

You can add a Lightmass Importance Volume to a level by dragging a **Lightmass Importance Volume** object from the **Volumes** tab of the **Place Actors** panel into the level then scaling it to the needed size.

![Adding a Lightmass Importance Volume to a level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6e71098-6e12-4cb3-bf8f-71c29a75de0e/37-lightmass-global-illum-add-lightmass-volume.png)

You can also convert a Brush into a Lightmass Importance Volume by clicking the **Convert Actor** drop down box inside the **Details** panel under **Actor**.

![Convert a Bush into a Lightmass Importance Volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76f245eb-5cee-4af4-a511-6fd89667c11c/38-lightmass-global-illum-convert-brush-actor.png)

After clicking the drop down box, a menu will appear where you can select the type of Actor to replace the Brush with.

![The drop down box of convert settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bebe7d98-4e63-4ca0-a032-4c7e3bbbdb30/39-lightmass-global-illum-convert-dropdown.png)

If you place multiple Lightmass Importance Volumes, most of the lighting work will be done with a bounding box that contains all of them. However, Volume Lighting Samples are only placed inside the smaller volumes.

## Building

1.  Click the **Build** in the **Main** menu panel and select **Build Lighting Only**, also you can choose **Build All Levels**.
    
    ![Select Build Lighting Only option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf4f5c6e-62ce-49da-8839-90fb2f31aa34/02-lightmass-basics-build-options.png)
2.  A dialog like this will appear at the bottom right of the screen.
    
    ![Lighting Build process in progress](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39abb13f-7372-44a2-b208-114b44233a29/03-lightmass-basics-build-progress.png)
3.  Click **Keep** when it finishes.
    
    ![Lighting Build process completed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95c61214-32eb-4474-a04b-bc4cefe2a989/04-lightmass-basics-build-completed.png)

And that is it. Depending on the number of lights, quality mode, the size of the level, what portions are contained within a Lightmass Importance Volume, and if other computers are available for the Swarm client to use, this process could take a few minutes or possibly substantially longer.

## Quality Modes

![Lighting quality build modes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea70803a-460e-49d3-bdb9-388e4f91f4d2/05-lightmass-basics-quality-modes.png)

These presets are about time versus quality. The **Preview** setting will render quickly and will give an ok representation of most baked direct lighting, while the **Production** setting renders more slowly, but gives a more realistic look while also correcting for various light bleed errors.

-   **Production** - Looks awesome, takes a while.
-   **High** - Looks good, takes some time.
-   **Medium** - Looks better, takes a bit longer to calculate.
-   **Preview** - Gets the point across, but at least it is fast.

These are just the presets, there are a vast number of settings that can be tweaked to get the desired lighting for your game. See the [Lightmass](/documentation/en-us/unreal-engine/cpu-lightmass-global-illumination-in-unreal-engine) documentation for more info on how to fine tune **Lightmass** settings.
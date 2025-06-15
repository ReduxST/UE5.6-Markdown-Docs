# Landscape Collision Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-collision-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-collision-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:04

---

## Landscape Collision

The Unreal Engine 5 (UE5) Landscape system enables you to specify the detail level of the geometry used for both simple and complex collisions for the entire Landscape as a whole or on a per-Component basis. In the following sections, we will go over how to use the system as well as any relevant information you must know before using this in your UE5 projects.

For this example, we are using the Content Examples project, specifically the Landscapes map, that can be found in the **Learn** tab of the UE5 Launcher.

### Collision Mip Level

If you select any Landscape Actor that has been placed in a level and go to the **Details** panel, under the **Collision** section you will find two settings called **Collision Mip Level** and **Simple Collision Mip Level**.

<table class="table" style="--columns-count: 2;"><tbody><tr><td><strong>Collision Mip Level</strong></td><td>The Collision Mip Level sets the complexity of the <strong>Complex</strong> collision that is used for the Landscape. Setting Collision Mip Level to <strong>0</strong>, the default, will give you a very accurate Landscape collision at the expense of memory. Setting this value to <strong>5</strong>, the maximum setting, will make the Landscape collision cheaper, but the accuracy of the collision will suffer.<div><block-slider-sequence-md count="6" slider-sequence-id="VC"><div class="img-list"><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4f64cea-5c3e-491d-b53b-9d94d0c7bb5d/01-collision-mip-level-0.png" alt="Collision Mip Level 0" loading="lazy" title="Collision Mip Level 0" width="800" class="img"> <img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddd8baff-a47e-4b9c-aac5-94a002203ab8/02-collision-mip-level-1.png" alt="Collision Mip Level 1" loading="lazy" title="Collision Mip Level 1" width="800" class="img"> <img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/287c03dc-56cd-4fa4-8a71-453270c1d5a9/03-collision-mip-level-2.png" alt="Collision Mip Level 2" loading="lazy" title="Collision Mip Level 2" width="800" class="img"> <img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90ac78f7-1557-4f95-b322-445da374c7f4/04-collision-mip-level-3.png" alt="Collision Mip Level 3" loading="lazy" title="Collision Mip Level 3" width="800" class="img"></div><p class="caption"><strong>Drag the slider to adjust the Collision Mip Level from 0 to 5</strong></p></block-slider-sequence-md></div></td></tr><tr><td><strong>Simple Collision Mip Level</strong></td><td>The Simple Collision Mip Level sets the complexity of the <strong>Simple</strong> collision that is used for the Landscape. Setting Simple Collision Mip Level to <strong>0</strong>, the default, will give you a very accurate Landscape collision at the expense of memory. Setting this value to <strong>5</strong>, the maximum setting, will make the Landscape collision cheaper, but the accuracy of the collision will suffer.<div><block-slider-sequence-md count="6" slider-sequence-id="PC"><div class="img-list"><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21268a9c-b064-41bb-8eb9-7db01999886d/07-simple-collision-mip-level-0.png" alt="Simple Collision Mip Level 0" loading="lazy" title="Simple Collision Mip Level 0" width="800" class="img"> <img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2466541e-7828-4651-b270-7038278917c6/08-simple-collision-mip-level-1.png" alt="Simple Collision Mip Level 1" loading="lazy" title="Simple Collision Mip Level 1" width="800" class="img"> <img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46821b3e-ad3c-4cab-951c-9bdecf07b10f/09-simple-collision-mip-level-2.png" alt="Simple Collision Mip Level 2" loading="lazy" title="Simple Collision Mip Level 2" width="800" class="img"> <img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3450db54-39d9-4674-9be1-471d4c63518f/10-simple-collision-mip-level-3.png" alt="Simple Collision Mip Level 3" loading="lazy" title="Simple Collision Mip Level 3" width="800" class="img"></div><p class="caption"><strong>Drag the slider to adjust the Simple Collision Mip Level from 0 to 5</strong></p></block-slider-sequence-md></div></td></tr></tbody></table>

### Viewing Collision Mip Level

You can visualize the Landscape collision geometry using the Playeer Collision Viewmode. To enable this view mode, go to the **View Mode** menu in the Editor viewport toolbar and select either **Player Collision** or **Visibility Collision**.

Click image for full size.

<table class="table" style="--columns-count: 2;"><tbody><tr><td><strong>Player Collision</strong></td><td>The <strong>Player Collision</strong> view mode displays the Simple Collision Mip Level. <img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a9ed814-08ee-4bb6-ae46-610aa01a5222/14-cml-player-collision.png" alt="Collision Mip Level Player Collision" loading="lazy" title="Collision Mip Level Player Collision" width="700"></td></tr><tr><td><strong>Visibility Collision</strong></td><td>The <strong>Visibility Collision</strong> view mode displays the Collision Mip Level. <img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5e843b8-169b-4638-9d91-919ecfb6f481/15-cml-visibility-collision.png" alt="Collision Mip Level Visibility Collision" loading="lazy" title="Collision Mip Level Visibility Collision" width="700"></td></tr></tbody></table>

### Adjusting the Landscape Collision Mip Level

To set the complexity for both simple and complex Landscape collision you will need to do the following:

1.  Select your Landscape Terrain in the Editor viewport. In the **Details** panel, expand the **Collision** section.
    
    Click for full image.
    
2.  Under the **Collision** section, find the **Collision Mip Level** option. Set the value from **0** to **5** and then press the **Enter** key to apply the change. The gray collision mesh in the level updates automatically to reflect the changes.
    
    ![Collision Mip Level 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eab40592-99f5-48ff-9612-2345daedba93/17-collision-mip-level-0.png "Collision Mip Level 0")
    
    ![Collision Mip Level 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ce22ac6-1ab7-4659-be31-dca6f9a9dff9/18-collision-mip-level-5.png "Collision Mip Level 5")
    

### Mixing Collision Mip Level Options

You can set the complexity of both the simple and complex Landscape collision meshes to provide a better balance between performance and accuracy. To set the simple and complex collision levels independently in your project you will need to do the following:

1.  Select your Landscape and in the **Details** panel and expand the **Collision** section.
    
    Click for full image.
    
2.  Set the **Collision Mip Level** to a value of **0** and **Simple Collision Mip Level** to a value of **2**.
    
    Click for full image.
    

In the following image comparison, you can see what happens to the Landscape collision when the Collision Mip Level and Simple Collision Mip Level are set to different values.

![Player Collision|Simple Collision Mip Level = 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f95fb924-902a-4f9d-b057-e2969b63dd3b/21-simple-collision-mip-level-2.png "Player Collision Simple Collision Mip Level 2")

![Visibility Collision|Collision Mip Level = 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80502a7c-536d-4c4d-859c-e9c60858abc2/22-collision-mip-level-0.png "Visibility Collision Collision Mip Level 0")

For most cases, you will want to leave the **Collision Mip Level** at 0 and then use 1 or 2 for the **Simple Collision Mip Level**. Using any higher numbers will start to show inaccuracies between the player and collision.

### Setting Collision Mip Level Per Landscape Components

You can set the Collision Mip Level collision for individual Landscape Components which enables you to reduce the Landscape collision complexity even further in non-playable areas of the level.

To set the Collision Mip Level for an individual component in your project, you will need to do the following:

1.  From the **Modes** dropdown, click on the Landscape option and make sure the **Manage** tab is selected.
    
    Click for full image.
    
    Click for full image.
    
2.  Select a few Landscape components by clicking on them with the **Left Mouse Button**. The selected Landscape Components are highlighted in red.
    
    Click for full image.
    
3.  In the **Details** panel, expand the **Landscape Component** section and change both the **Collision Mip Level** and **Simple Collision Mip Level** to **5**.
    
    Click for full image.
    
4.  In the Landscape **Manage** section under **Tool Settings**, press the **Clear Component Selection** button to deselect any currently selected Landscape components.
    
    Click for full image.
    
5.  Select a few more Landscape components and this time set both Collision Mip levels to a value of 2.
    
    Click for full image.
    

In the following image, the Collision Mip level for each of the four outlined Landscape Component has been set to a different level.

Click for full image.

| Number | Collision Mip Level |
| --- | --- |
| 1 | 3 |
| 2 | 4 |
| 3 | 5 |
| 4 | 2 |
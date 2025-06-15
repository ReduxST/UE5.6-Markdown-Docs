# Procedural Foliage Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-foliage-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-foliage-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:34

---

In this Quick Start tutorial we will take a look at how the **Procedural Foliage Tool** works. Over the course of this Quick Start tutorial you will learn how to create, set up, and spawn an entire forest's worth of trees inside of UE5 using only the Procedural Foliage tool. You will also be introduced to key properties and settings that will help you shape your virtual forest to fit your project's needs.

![Final Product](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/febee554-d0d9-4888-9f1f-83f59fb575be/01-t-pf-qs-final-product.png "Final Product")

You will also be exposed to all of the required Assets and properties the Procedural Foliage tool requires to function correctly and deliver the results you want. When you have completed this Quick Start you will have a new level that should look similar to the image above.

### Prerequisites

Before you can use the Procedural Foliage tools in your project, you must first enable them by doing the following.

1.  From the **Main Menu** open the **Edit** menu then click on **Editor Preferences**.
    
    Click image for full size.
    
2.  Inside of the Editor Preferences **right - click** on the **Experimental** section.
3.  Enable the Procedural Foliage option by clicking on the checkmark box next to the word **Procedural Foliage**.
    
    Click image for full size.
    

You will also need to download the **Open World Demo Collection** content pack from the **Unreal Engine Marketplace** as some of the content from the collection will be used in the following Quick Start. Once the Open World Demo Collection is downloaded add it to the project that you are using to follow along with this Quick Start by doing the following.

1.  From the Epic Games Launcher in the Marketplace locate and then download the **Open World Demo Collection**.
    
    Click image for full size.
    
2.  Go the **Library** section of the launcher and then under **Vault** section locate the Open World Demo Collection .
    
    Click image for full size.
    
3.  Click on the button that says **Add to Project**.
    
    Click image for full size.
    
4.  You will then be shown a list of projects that you can add this to, select the project that you are using to follow along with this Quick Start and then press the **Add to Project** button
    
    Click image for full size.
    

## 1 - Creating Foliage Type Actors

In this step you will create a new Level, Landscape Terrain, and all of the Assets the Procedural Foliage Tool requires.

1.  Create a new level using the **Default Template** as a base.
    
    Click image for full size.
    
2.  Add a new **Landscape Actor** to the level by first selecting **Landscape** in the **Modes** dropdown menu to open the **Landscape Panel**, and then clicking the **Create** button to add the Landscape Actor to the level.
    
    Click image for full size.
    
    Using a Landscape Terrain Actor quickly provides you with a very large area to spawn your forest on.
    
    Click image for full size.
    
    If you are not familiar with how Landscape Terrain works or would like to learn more, please refer to [Landscape Outdoor Terrain](/documentation/en-us/unreal-engine/landscape-outdoor-terrain-in-unreal-engine) for more information.
    
3.  Create a new Procedural Foliage Spawner by **right-clicking** in the **Content Browser**, expanding the **Foliage** section, and then clicking on the **Procedural Foliage Spawner**.
    
    Click image for full size.
    
4.  Name the Procedural Foliage Spawner in this example **PFS\_Example** or something similar.
    
    Click image for full size.
    
5.  Drag the Procedural Foliage Spawner from the **Content Browser** into the level and position it so that it is in the center of the level or at **0,0,200** in the X, Y, and Z axis.
    
    Click image for full size.
    
6.  Scale the Procedural Foliage Spawner to **100,100,10** in the X, Y, and Z axis to create a large area to spawn your forest in.
    
    Click image for full size.
    
7.  Now that we have our spawner, we need to give it some Foliage to spawn. To do this, **right - click** in the **Content Browser** expanding the **Foliage** section and then click on **Static Mesh Foliage**. Name the Static Mesh Foliage **Tree\_00** or something similar.
    
    Click image for full size.
    
8.  If you have not done so already, save your work and level by pressing the **Save All** button to save all content and the **Save** button to save the level. When prompted for a level name use the name **PFT\_00**. At this point you should have something that looks similar to the image below.
    
    Click image for full size.
    

## 2 - Telling the Spawner What to Spawn

In the following section we will cover how to set up the **Foliage Type Actors** to work with the Procedural Foliage Spawner. You will continue to work with the **PFT\_00** level that was created in the last step.

1.  Open up the **Procedural Foliage Spawner** by **double - clicking** in the Content Browser.
    
    Click image for full size.
    
2.  Add a new item to the **Foliage Types** array by clicking the **Plus Sign** icon that is to the right of the **Foliage Types** menu option.
    
    Click image for full size.
    
3.  In the Content Browser, select the Tree\_00 Static Mesh Foliage and drag it into the **Foliage Type Object**, or press the **Arrow** icon, to load the selected Static Mesh Foliage into the Procedural Foliage Spawner.
    
    Click image for full size.
    
4.  Open up the Tree\_00 Static Mesh Foliage by **double - clicking** on it in the Content Browser.
    
    Click image for full size.
    
5.  At the top of the Tree\_00 Static Mesh Foliage, locate the **Mesh** section and then click on the drop down menu that says **None**.
    
    Click image for full size.
    
6.  Locate the **HillTree\_02** Static Mesh from the **Open World Demo Collection** either by typing "HillTree\_02" as the search term or by scrolling through the list, and load it by clicking on it.
    
    Click image for full size.
    
7.  Back in the viewport select the **Procedural Foliage Spawner** that was placed in the level and then expand the **Procedural Foliage** section under the **Details** panel.
    
    Click image for full size.
    
8.  Under the **Procedural Foliage** section click on the **Resimulate** button and you should now see the Procedural Foliage Spawner densely packed with tress like in the image below.
    
    Click image for full size.
    
    In order to see the proper results, you will need to click on **Build** in the **Main Toolbar** to rebuild the lighting every time you use the Resimulate button to create or alter the Procedural Foliage . This can take a long time due to the large number of static meshes involved.
    

## 3 - Tweaking Foliage Type Object Properties

**Foliage Type Objects** (both Static Mesh Foliage and Actor Foliage) come with a number of different properties that you can adjust to control anything from how the Foliage Type Objects are placed on other objects in the level to how the Foliage Type Objects will grow and spread throughout the Foliage Spawner. In the following section we will take a look at what properties are available in **Foliage Type Objects** and how you can manipulate these properties to get the results you desire. You will continue to work with the **PFT\_00** level that was used in the last step.

1.  Open up the Tree\_00 Static Mesh Foliage.
    
2.  Expand the **Placement** section and make sure that both **Align to Normal** and **Random Yaw** are enabled.
    
    Click image for full size.
    
    The Placement section is where you can adjust how a Foliage Type Object's meshes are placed on objects in the level.
    
3.  Under the **Procedural** section of the Static Mesh Foliage expand the **Collision** section and set the **Shade Radius** to **50**.
    
    Click image for full size.
    
    The Collision section determines which Foliage Type Objects should be removed when two Foliage Type Objects are competing for the same spawn location or relative space. When a Virtual Seed's collision radius overlaps an existing collision or shade radius from another Foliage Type Object's Virtual Seed, one Virtual Seed will be replaced or killed based on which Foliage Type Object has the higher priority.
    
4.  Select the Procedural Foliage Spawner that was placed in the level and under the Procedural Foliage section click on the Resimulate button.
    
    Click image for full size.
    
5.  Back in the Tree\_00 Static Mesh Foliage collapse the Collision section and expand the **Clustering** section, then set **Num Steps** to **0**, so that we get trees that are all the same size and age and then press the Resimulate button. When completed you should have something that looks similar to the image below.
    
    Click image for full size.
    
    Clustering uses a number of properties such as density, age, and proximity to help determine how the specified Foliage Type Object's mesh instances should be placed, grouped and spread around inside of the Procedural Foliage Spawner.
    
6.  While we now have some space in between our trees, the overall density is still a little too high. To fix this, set the **Initial Seed Density** to **0.25** and then click on the Resimulate button.
    
    Click image for full size.
    
7.  As you can see, setting the Initial Seed Density to 0.25 greatly reduced the density of our forest because we are only growing and spreading trees for a single year. To fix this set the Num Steps back to **3**, which will grow and spread the trees for 3 years, and then click on the Resimulate button.
    
    Click image for full size.
    
8.  Expand the **Growth** section then set the following parameters to the following settings.
    
    -   **Max Age**: **20.0**
    -   **Procedural Scale Max**: **10.0**
        
        Click image for full size.
        
        The Growth section allows you to adjust how a Foliage Type Object's mesh instances will grow and get bigger over time.
        
9.  Finally in the **Instance Settings** under the **Cull Distance** option, set the **Max** value to **20,000** and then click on the Resimulate button. When completed you should have something that looks similar to the image below.
    
    Click image for full size.
    
    The Instance Settings allows you to adjust how a Foliage Type Object's mesh instances will be displayed in the level. Inside the Instance Settings you can set or adjust many different properties like Cull Distance, Shadowing, and Collision.
    

## 4 - Using Multiple Foliage Type Objects

Adding another species of tree to your virtual forest will greatly help to increase the realism and overall look and feel. Luckily, the **Procedural Foliage Spawner** allows for you to spawn multiple **Foliage Type Objects** resulting in one single **Procedural Foliage Spawner** being able to spawn an entire forest with a multitude of different trees. In the following section we will take a look at how you can set up a Procedural Foliage Spawner to work with multiple Foliage Types. You will be continuing to work with the **PFT\_00** level that was used in the last step.

1.  Inside of the Content Browser select the Tree\_00 Static Mesh Foliage and then press **Ctrl + W** on the keyboard to duplicate it using **Tree\_01** as the name.
    
    Click image for full size.
    
2.  Open the newly created Tree\_01 Static Mesh Foliage and under the Mesh section change the mesh to the **ScotsPineTall\_01** Static Mesh.
    
    Click image for full size.
    
3.  Open up the Procedural Foliage Spawner from the Content Browser and expand the Foliage Types section.
    
    Click image for full size.
    
4.  Click on the Plus sign icon to add the option to input another Foliage Type Object.
    
    Click image for full size.
    
5.  In the Content Browser, select the Tree\_01 Static Mesh Foliage and drag it into the Foliage Type Object, or press the Arrow icon, to load the selected Static Mesh Foliage into the Procedural Foliage Spawner.
    
    Click image for full size.
    
6.  Select the Procedural Foliage Spawner that was placed in the level and then click on the Resimulate button. When completed you should see something like the following image.
    
    Click image for full size.
    
7.  To make the forest look more interesting open up the Tree\_01 Static Mesh Foliage and adjust the following parameters with the following values. The numbers and options that are listed below were selected because they will produce a forest that has interesting clustering and growth interaction with the Static Mesh Foliage instances that are already in use. However please feel free to experiment with these numbers and settings till you get something that suits your needs.
    
    -   **Num Steps:** 4
    -   **Initial Seed Density:** 0.125
    -   **Average Spread Distance:** 100
    -   **Can Grow in Shade:** Enabled
    -   **Spawns in Shade:** Enabled
    -   **Max Age:** 15
    -   **Overlap Priority:** 1
    -   **Procedural Scale:** Max 5.0
8.  Once the settings have been adjusted click on the **Resimulate** button on the Procedural Foliage Spawner and you should now have something that looks similar to the image below.
    
    Click image for full view.
    

## 5 - Implementing Procedural Foliage Blocking Volumes

The **Procedural Foliage Blocking Volume** is a Volume Actor that can be placed in a level and scaled to a desired size which will prevent the Procedural Foliage Spawner from spawning any Foliage Type Objects inside of the bounds of the Procedural Foliage Blocking Volume. In the following section we will go over how you can add a **Procedural Foliage Blocking Volume** to your level and use it to prevent Foliage meshes from spawning. You will be continuing to work with the **PFT\_00** level that was used in the last step.

1.  First find the **Procedural Foliage Blocking Volume** by searching for it in the **Place Actors** panel using **Proc** as the search term.
    
    Click image for full size.
    
2.  Select the Procedural Foliage Blocking Volume and then drag it from the Place Actors panel into the level.
    
    Click image for full size.
    
3.  To stop foliage meshes from being spawned in the back portion of the Procedural Foliage Spawner move and scale the Procedural Foliage Blocking Volume using the following location and scale values.
    
    -   **Location X:** 5430.0 cm
    -   **Location Y:** -3900.0 cm
    -   **Location Z:** 200.0 cm
    -   **Scale X:** 41.75
    -   **Scale Y:** 65.5
    -   **Scale X:** 41.75
        
        Click image for full size.
        
4.  Now select the Procedural Foliage Spawner in the level and then in the Details click on the Resimulate button. When the Resimulate is completed you should now be missing the entire back section of trees that were intersecting with the Procedural Foliage Blocking Volume.
    
    Click image for full size.
    
    In the following image we can see the before and after results.
    
    | Image Number | Results |
    | --- | --- |
    | 1: | Before Procedural Foliage Blocking Volume is added |
    | 2: | After Procedural Foliage Blocking Volume is added |
    

## 6 - On Your Own!

Now that you have seen that power the Procedural Foliage tool offers, try using the tools listed below in conjunction with what you just learned about the Procedural Foliage tool to try and make a level that looks like the following image.

![On Your Own](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac596572-4efd-41d0-9bdf-8be51c901793/44-t-on-your-own.png "On Your Own")

-   Try using Foliage Actors instead of Static Mesh Foliage.
    
-   Use the [Grass Tool](/documentation/en-us/unreal-engine/grass-quick-start-in-unreal-engine) to make the Landscape look like it is densely covered in grass, flowers and bushes.
    
-   Define the look and feel of the Landscape terrain using the [Landscape Sculpt](/documentation/en-us/unreal-engine/landscape-sculpt-mode-in-unreal-engine) tools add things like hills, mountains and lakes.
    
-   Give the surface of the Landscape more visual variety and detail by creating a [Landscape Material](/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine) that has multiple Textures that can be painted on the Landscape terrain.
    
-   Adjust the [Directional Light](/documentation/en-us/unreal-engine/directional-lights-in-unreal-engine) to make the level lighting resemble lighting that happens in the early morning or late afternoon.
    
-   Set up the level lighting to use a completely dynamic based lighting solution that will make use of dynamic shadows as well as [Ray Traced Distance Field Soft Shadows](/documentation/en-us/unreal-engine/distance-field-soft-shadows-in-unreal-engine).
    
-   Try using the [Foliage System](/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine) tools to remove or tweak the placement, rotation and scale of the Foliage meshes that are placed by the Procedural Foliage tool so that you can get the exact look you are going for.
    
-   Show off your creation to others by using a [Camera](/documentation/en-us/unreal-engine/camera-actors-in-unreal-engine) in conjunction with [Sequencer](/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine) to render out a video of your level for you to share with the world.
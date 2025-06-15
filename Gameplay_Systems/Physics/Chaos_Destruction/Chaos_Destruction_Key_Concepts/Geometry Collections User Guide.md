# Geometry Collections User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-collections-user-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-collections-user-guide)  
**Processed:** 2025-06-14 16:25:33

---

You can find similar information in video format in the Epic Developer Community site by watching the [Chaos Destruction - Geometry Collections](https://dev.epicgames.com/community/learning/tutorials/yrXz/chaos-destruction-geometry-collections) tutorial.

Destruction within the Chaos system starts with a **Geometry Collection** Asset. These assets can be built from one or more Static Meshes, Blueprints with Static Mesh components, and even other Geometry Collections.

Once you have a Geometry Collection, you can break it apart using the [Fracture Mode](/documentation/en-us/unreal-engine/destruction-overview) and define the settings that determine how it breaks apart.

In this guide you will learn how to create Geometry Collections from different source objects that can be used with the Chaos Destruction system, as well as best practices for ensuring the best simulation results.

## Create Geometry Collections

### Create Geometry Collection Assets

Follow these steps to create a Geometry Collection asset.

1.  Select a compatible Actor in the scene, click the **Mode** dropdown and select **Fracture**.
    
    ![Select the Fracture mode from the Select Mode dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6a0e479-8479-4fa0-90ea-79a74e51206f/destruction-geo-col-2.png)
    
    This will open the **Fracture Mode** windows that contain all the tools for fracturing your mesh. Alternatively, you can press **Shift-6** to switch to the Fracture Mode.
    
    Click for full view.
    
2.  In the **Generate** section, click **New** to create a new **Geometry Collection**.
    
    ![Click New to create a new Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aabfe638-4ac4-4b90-81a6-7f1a37e2dcfb/destruction-geo-col-4.png)
    
    This asset type will be saved in the Content Browser and will be used to create your fractured mesh.
    
    1.  (1) Select the directory location where the Geometry Collection will be saved.
        
    2.  (2) Enter the name for the Geometry Collection asset.
        
    3.  (3) Click Create Geometry Collection.
        
        ![Select the directory location, enter a name for your asset and click Create Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe368e1b-32fc-435d-bce6-8607fb423f67/destruction-geo-col-5.png)
    4.  Click Save All in the Content Browser to save the new Geometry Collection asset.
        
        ![Click Save All in the Content Browser to save the new Geometry Collection asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99ea1254-199c-4f24-9af0-b73bd59e6f30/destruction-geo-col-6.png)
3.  The Actor you selected in the scene is replaced with the Geometry Collection in the level.
    
    ![The Static Mesh is replaced with the Geometry Collection in the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/855b10c1-1b8b-4bbe-b777-fb278d03019e/destruction-geo-col-7.png)

These steps can be used to create Geometry Collections from any combination of assets.

### Create a Geometry Collection from Static Meshes

You can create Geometry Collections by combining any number of Static Meshes in your Level.

When creating Geometry Collections from a single Static Mesh, select a Static Mesh Actor and follow the steps mentioned above. The selected Static Mesh Actor will be replaced by the new Geometry Collection in the level.

![The Static Mesh is replaced with the Geometry Collection in the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78661b36-bb48-46bd-b69d-798ca23cdd21/destruction-geo-col-7.png)

Geometry Collections can be created from any combination of Static Meshes. Select multiple Static Mesh Actors in the Level and follow the steps detailed in Create Geometry Collection Assets.

When selecting multiple Static Meshes, the first selected Actor is used to create the Geometry Collection's pivot point.

![The Static Meshes are replaced with the Geometry Collection in the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df9447c8-c576-4c36-8a4d-0505a185df66/destruction-geo-col-16.png)

### Create a Geometry Collection from a Blueprint Actor

You can create Geometry Collections by combining **Blueprint Actors** that have one or more **Static Mesh components**. Their Static Mesh components are treated as regular Static Meshes when converted to a Geometry Collection.

The example below is a Blueprint Asset that has two Static Mesh components.

Click for full view.

You can convert a Blueprint Asset to a Geometry Collection by dragging it into the Level and following the steps in Creating Geometry Collections.

Click for full view.

You can also combine Blueprint Actors with Static Meshes or other Blueprint Actors by selecting them and following the steps in Create Geometry Collection Assets.

![The Blueprint and Static Mesh are replaced with the Geometry Collection in the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68f49ce6-7584-4e1c-b15d-ecda19b06af5/destruction-geo-col-16.png)

### Create a Geometry Collection from other Geometry Collections

You can create new Geometry Collections from other Geometry Collections following the same process. Drag one or more Geometry Collection Assets into the Level, select them and follow the steps in Creating Geometry Collection Assets.

Click for full view.

## Fracture Geometry Collections

Now that you have a Geometry Collection, you can break it apart using the [Fracture Mode](/documentation/en-us/unreal-engine/destruction-overview). This mode contains different types of fracture methods, as well as methods of clustering and editing fractured pieces.

In this guide you will use the standard **Uniform Voronoi** method. With this method you define a minimum and maximum number of sites to create cell volumes for fracturing. For more details about the various fracturing methods available read the [Fracturing Geometry Collections User Guide](/documentation/en-us/unreal-engine/fracturing-geometry-collections-user-guide).

Follow these steps to fracture a Geometry Collection:

1.  Select a Geometry Collection in the Level, click the **Mode** dropdown and select **Fracture**.
    
    ![Select the Fracture mode from the Select Mode dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0886c382-26d6-4f99-8687-39efb6ff35bf/destruction-geo-col-2.png)
    
    Click for full view.
    
2.  Go to the **Fracture** section and click the **Uniform** fracture button.
    
    ![Click the Uniform fracture button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38f837db-47dc-4002-9182-c5e0d2e1cc19/destruction-geo-col-9.png)
3.  Leave the default settings as they appear and click **Fracture**.
    
    ![Click Fracture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ea5d403-406d-4968-88af-3c023c20a3c3/destruction-geo-col-10.png)
    
    You can learn more about the fracturing process by referring to the [Fracturing Geometry Collections User Guide](/documentation/en-us/unreal-engine/fracturing-geometry-collections-user-guide) tutorial.
    
4.  Select the **Geometry Collection** and move it above the ground. Click the **Play Mode options** button and select **Simulate** or **Selected Viewport** to see the results.
    
    ![Click Simulate from the Play Modes option menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a761376c-988c-4fae-af55-856291d4c3b0/destruction-geo-col-12.png)

The Geometry Collection fractures on impact.

![The column falls to the ground and fractures on impact](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/256a8d9f-3aed-488d-9019-d08adacc1b5f/destruction-geo-col-fall.gif)

## Change the Materials of Geometry Collections

Now that you know how to fracture Geometry Collections, you might want to change how the fractured pieces look for the external and internal surfaces.

1.  Follow these steps to show the Geometry Collection with its original Materials:
    
    1.  Select a Geometry Collection and use the Level **Details** panel.
        
    2.  In the **Chaos Physics** section, expand the **General** options.
        
    3.  **Deselect** the **Show Bone Colors** checkbox.
        
        ![Show bone colors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d69cbc21-9030-4dba-9eb0-c81ef685d7a3/destruction-geo-col-24a.png)
        
        ![Do not show bone colors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee55c1f2-661c-4210-804d-1c6f0918cbad/destruction-geo-col-24b.png)
        
2.  In the **Materials** section, each original Material ID has been duplicated from the source Asset.
    
    In the example below, **Element 1** and **Element 3** have been duplicated from **Element 0**, and **Element 2** to represent the internal surfaces when you created the Geometry Collection.
    
    ![In the example below, Element 1 and Element 3 have been created as duplicates of Element 0, and Element 2, respectively](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43370e2c-2cf6-4bdb-95cb-caf915de468a/destruction-geo-col-25.png)
3.  Replace the Materials in **Element 1** and **Element 3** to affect how the internal surfaces look. In the example below, red and green Materials have been added to those slots.
    
    ![Replace the Materials in Element 1 and Element 3 to affect how the internal surfaces look](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15ab3a86-d2d1-46fc-8a89-6fc9283c9db4/destruction-geo-col-26.png)
4.  Click the **Play Mode** options button and select **Simulate** or **Selected Viewport** to see the results.
    
    ![Click Simulate from the Play Modes option menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/869a3db7-67b6-47c8-b161-f60fd0b68bd3/destruction-geo-col-12.png)
    
    You can see that the internal surfaces now use the newly added Materials.
    
    ![The column falls to the ground and fractures on impact](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5858517-e4db-4bea-8c91-9366fbb7680a/destruction-geo-col-fall-2.gif)
    
    You can also change the Materials directly inside the Geometry Collection. Double click the **Geometry Collection** in the **Content Browser** to open it.
    
    ![Double click the Geometry Collection in the Content Browser to open it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1498cd45-a84f-43b8-95e3-79226163509d/destruction-geo-col-27.png)
    1.  Scroll down to the **Materials** section and replace the Materials in **Index \[1\]** and **Index \[3\]**.
        
        ![Replace the Materials in Index [1] and Index [3]](destruction-geo-col-28.png)
    2.  Save the Geometry Collection and close the window.
        

## Best practices when creating Geometry Collections

Consider the following when creating your Geometry Collections.

### Geometry Collections should be "water tight"

Actors used to create the Geometry Collection should be "water tight," meaning they have no open faces or edges. Objects with open faces will perform worse when simulating and return unpredictable results.

![Static Mesh with a hole](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/640ac59c-daa4-4d45-b5fc-35736c3bc757/destruction-geo-col-29a.png)

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d63e13e-f4cd-4df3-921d-e7edd3a313bc/destruction-geo-col-29b.png)

### Geometry Collections should not have intersecting geometry

Objects that make up a Geometry Collection should not intersect each other. Because each Geometry Collection is an individual object which can be simulated, the Chaos Solver will try to push each object away from the other once simulation starts. This can cause erratic and unpredictable results.

![Example of two Static Meshes that are overlapping](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6c6198c-9e4f-4707-b9f0-dd5518e16ed4/destruction-geo-col-30.png)

Objects with overlapping geometry will be pushed away from each other.

![Objects with overlapping geometry will be pushed away from each other](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e65ff7e-eaa5-40c2-9eeb-06ce832c1e40/destruction-geo-col-fall-3a.gif)

Objects without overlapping geometry simulate correctly.

![Objects without overlapping geometry simulate correctly](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c8b75e7-6198-4087-b300-e13bf8aca54f/destruction-geo-col-fall-3b.gif)
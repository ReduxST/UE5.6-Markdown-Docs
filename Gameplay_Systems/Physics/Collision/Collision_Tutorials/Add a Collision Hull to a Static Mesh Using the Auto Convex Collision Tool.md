# Add a Collision Hull to a Static Mesh Using the Auto Convex Collision Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/add-a-collision-hull-to-a-static-mesh-using-the-auto-convex-collision-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/add-a-collision-hull-to-a-static-mesh-using-the-auto-convex-collision-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:04:44

---

In the following How-To we will take a look at using the Auto Convex Collision tool to automatically create collision for Static Meshes.

The Auto Convex Tool also uses a newer version of [V-HACD library](https://github.com/kmammou/v-hacd) that should give more accurate results.

## Steps

1.  First open up the Static Mesh you want to add collision to in the Static Meshes Editor. For this example, we will be using the **SM\_Rock Mesh** that comes with the Starter Content.   
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/436db27a-ccb4-4e7b-9e26-eb7bed1c7a68/ht_addconvexhulls_01.png "HT_AddConvexHulls_01.png")
    
2.  Next, open up the Auto Convex Collision tool by going to **Collision > Auto Convex Collision**. This will open up the Auto Convex Collision in the lower right-hand corner of the Static Mesh Editor.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7c9abae-fb05-4e48-ab05-7abce94fd08f/ht_addconvexhulls_02.png "HT_AddConvexHulls_02.png") 
    
3.  Inside of the Auto Convex Collision tool set the following parameters with the following settings:  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c19fec7d-4055-49bb-b6f2-1247b3bd4feb/ht_addconvexhulls_03.png "HT_AddConvexHulls_03.png")
    
    | Property Name | Value |
    | --- | --- |
    | **Hull Count** | 32 |
    | **Max Hull Verts** | 16 |
    | **Hull Precision** | 50,000 |
    
4.  When all of the above settings have been input, click the **Apply** button to begin the collision creation process.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fdab84c-8688-4ab4-85b8-aca8acfde746/ht_addconvexhulls_07.png "HT_AddConvexHulls_07.png") 
    
    Computation of the collision will now run as background task in the Static Mesh Editor. The progress of the collision creation will be shown in the following progress window.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc836d27-7ec1-448e-9bd5-d81935a05273/ht_addconvexhulls_06.png "HT_AddConvexHulls_06.png")
    

## End Result

When completed you can view the new collision, if not already enabled, by clicking on the Collision icon and then selecting the Simple Collision option from the drop-down list. 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca9a861d-af2c-4d84-9b9c-4e7eb1e77d02/ht_addconvexhulls_05.png "HT_AddConvexHulls_05.png") ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e02d088-f020-44c7-925d-231bb9aa22f3/ht_addconvexhulls_04.png "HT_AddConvexHulls_04.png")

The following image sequence shows what type of results you get when increasing the values of the Auto Convex Collision from the default settings to the maximum settings allowed.

  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/522dc1d9-1f48-496f-98ec-6216da111726/ht_addconvexhulls_default.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66e942c1-1749-4a50-a0c5-c9e9d0dd8731/ht_addconvexhulls_medium.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40e336dd-ecb1-4db0-b6aa-e8abd12e1851/ht_addconvexhulls_high.png)

Auto Convex Collision Settings Results
# Improving Normals

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/improving-normals-with-the-proxy-geometry-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/improving-normals-with-the-proxy-geometry-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:35

---

The extreme constraints on Fortnite memory usage call for very efficient use of Level of Detail (LOD) meshes. For most of the proxies, very small Base Color Textures where generated and no Normal map is used. Because of this, this approach requires the highest quality normals on the proxy mesh itself. In the following How-To we will take a look at how you can specify how the Normals of a Static Mesh are calculated when using the Proxy Geometry tools.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6fe7b7b-728f-4d0c-8c95-cc27ef2b0eb6/hardedgesplit_10.png)

## Steps

In the following section we will take a look at how you can adjust the manner in which the generated Static Meshes Normals are calculated when using the Proxy Geometry tool.

1.  First locate an object that requires you to create a Proxy Static Mesh for it. For this example, the following small house was constructed using only Static Meshes that can be found in the Starter Content.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1dfb5abb-58d3-43dd-8d4b-c9cbe22eda36/gapfilling_01.png "GapFilling_01.png")
2.  Next, open up the **Merge Actor** tool by going to **Window > Developer Tools > Merge Actors**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c16738b-75cf-42d8-a8b0-09bb50692656/gapfilling_02.png "GapFilling_02.png")
3.  Inside the level, select all the Static Mesh Actors that make up the object for which you want to generate new geometry.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/719ea367-bbcf-4940-90f9-edd904011525/gapfilling_03.png "GapFilling_03.png")
4.  In the Merge Actor tool, click the **second icon** to access the Proxy Geometry tool and then expand the **Proxy Settings**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6124fee0-b54d-4549-a318-670f1160bb50/gapfilling_04.png "GapFilling_04.png")
5.  Under the Proxy Settings, expand the **Material Settings** section and disable the **Normal Map** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2057107b-9bc5-47f2-ae5a-e352f5ee96e0/hardedegesplit_01.png "HardEdegeSplit_01.png")
    
    If you don't disable the Normals here, you will not see the correct results because you will be seeing the Normals from the Normal map, and not from the generated Static Mesh.
    
6.  Next, click the box next to the **Hard Edge Angle** option to disable it. This disables all normal calculations on the generated Static Mesh.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/edcae68c-21a2-4f07-8d59-94d42cc9ccd7/hardedegesplit_02.png "HardEdegeSplit_02.png")
7.  Next, click the **Merge Actors** button and input a name and location in the **Content Browser** for the newly created Static Mesh. Then click the **Save** button to start the merging process.
    
8.  Once everything has completed, open up the newly created Static Mesh, which should look something like the following image.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/965afb34-a7b0-4942-9378-f1a9b469ae91/hardedegesplit_03.png "HardEdegeSplit_03.png")
9.  The above image is not what we want; we want the generated object to have Normals that look almost identical to the Normals of the object that it was generated from. To fix this issue, go to the Merge Actor tool and re-enable the Hard Edge Angle option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f49f1e23-3d11-4f3f-9e7f-4fdeabdcec8a/hardedegesplit_04.png "HardEdegeSplit_04.png")
10.  Once the Hard Edge Angle has been re-enabled, re-run the Merge Actors tool. When it has completed, you should now have a building that looks like the following image:
    

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bd95c0e-6992-4bd5-b59d-095533051456/hardedegesplit_05.png "HardEdegeSplit_05.png")

## End Results

Getting the best results is going to take some time and iteration as each object could require slightly different settings to get the best results. Also keep in mind that when you are specifying a value for the Hard Edge Angle you could increase or decrease the number of vertices that are used in the generated Static Mesh. The following image comparison shows what happens a Static Mesh and it's vertices when setting the Hard Edge Angle to values of **0**, **5**, **10**, **50**, **80**, **130**, and **180**.

      ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a75ed0a-c1ea-4859-9f2f-dfd48f97994b/hardedgesplit_0.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a61a321-104f-402b-911b-d086168a1e5c/hardedgesplit_5.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41681f89-22c5-4328-bad8-07937303376a/hardedgesplit_10.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8579495-a0a5-444f-999a-02dc666fa474/hardedgesplit_50.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/365d1fd9-4c8d-454c-873a-3747fb994153/hardedgesplit_80.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e74e420f-1d6e-46fc-9ff5-3f334efc3c5c/hardedgesplit_130.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f22fee0a-840a-4158-9a1b-7ecd5bc3e371/hardedgesplit_180.png)

The following image comparison shows the different shading and vertex counts when setting the Hard Edge Angle to values of 0, 5, 10, 50, 80, 130, and 180.
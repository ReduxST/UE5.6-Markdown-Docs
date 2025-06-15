# Adjusting Proxy Geometry Screen Size

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/adjusting-proxy-geometry-screen-size-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/adjusting-proxy-geometry-screen-size-in-unreal-engine)  
**Processed:** 2025-06-14 16:05:08

---

In the following How - To we, will take a look at using the **Spatial Sampling Distance** override parameter to manually adjust the feature minimum size that the system captures when it re-meshes all the Objects (before it simplifies). 

## Steps

1.  First, inside of any Unreal Engine 5 (UE5) level, select a few Static Meshes to work with.
    
    Click image for full size.
    
2.  With the Static Meshes still selected open up the **Merge Actors** tool by going to  **Tools.**  Then from the displayed list, select the **Merge Actors** tool.
    
    Click image for full size.
    
3.  When the Merge Actors tool opens, click on the **2nd** icon to access the **Proxy Geometry** tools. Then under **Proxy Settings**, expand the **Material Settings** section.
    
    Click image for full size.
    
4.  Locate the **Override Spatial Sampling Distance** parameter and click on the box next to its name to enable it.
    
    Click image for full size.
    
5.  Set the value of Override Spatial Sampling Distance to 100 and then press the **Merge Actors** button.
    
    Click image for full size.
    
    By default, the system computes a guess at this size based on the bounding box of the geometry and the requested **Screen Size**. If you look in the **Window > Developer Tool > Output Log**, you will see that the actual number used by the system will be written out. The larger this number is, the less simplification will be performed. The smaller the number is, more simplification will be performed.
    
6.  Specify a name and location for the newly created Static Mesh and then press the **Save** button to begin the Proxy Geometry creation process.
    
    Click image for full size.
    

## End Result

When the process has completed you will now have a new Static Mesh, Material and Textures of all the Static Meshes you had selected in the first step of this How - To. The images below demonstrate the effects of setting the Override Spatial Sampling Distance to different values has on the created Static Mesh.

    ![Override Spatial Sampling Distance Original](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6df43147-22d3-46c0-a6e3-26ac7d211563/07-override-spatial-sampling-distance-original.png "Override Spatial Sampling Distance Original") ![Override Spatial Sampling Distance = 0.5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8aa20bae-5d41-4f16-8457-e19926c7c5c5/08-override-spatial-sampling-distance-0-5.png "Override Spatial Sampling Distance = 0.5") ![Override Spatial Sampling Distance = 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2680098-300f-4ef5-9aff-fff7cc126142/09-override-spatial-sampling-distance-1.png "Override Spatial Sampling Distance = 1") ![Override Spatial Sampling Distance = 10](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a16aeb71-2817-44bb-89bb-3df2d58a3617/10-override-spatial-sampling-distance-10.png "Override Spatial Sampling Distance = 10") ![Override Spatial Sampling Distance = 100](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d21c997a-2a52-425b-8c22-7fc72ddddf15/11-override-spatial-sampling-distance-100.png "Override Spatial Sampling Distance = 100")

Override Spatial Sampling Distance = 0.5 | Override Spatial Sampling Distance = 1 | Override Spatial Sampling Distance = 10 | Override Spatial Sampling Distance = 100
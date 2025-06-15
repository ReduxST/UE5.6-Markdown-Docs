# Eye-Dome Lighting Mode for Point Clouds

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/eye-dome-lighting-mode-for-point-clouds-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/eye-dome-lighting-mode-for-point-clouds-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:06

---

**Eye-Dome Lighting (EDL)** is a lighting model that accentuates the shapes of objects within a point cloud by grouping objects that are close together and shading their outlines, which enhances depth perception. EDL is implemented as a post-process Material and requires a Post Process Volume to work. It does not use any engine light sources, so it can be used with the unlit rendering method.

EDL can be used with Ambient Occlusion but this may produce an excessively dark image.

## Steps

1.  Add a Post Process Volume to your Level. From the **Place Actors** panel, search for **Post Process Volume** and drag it into your Level.
    
    Click image for full size.
    
2.  Select the Post Process Volume and, in its **Details** panel, scroll to the **Rendering Features** category.
    
3.  Expand **Post Process Materials** and click the **plus (+)** icon to add a new Material to the array.
    
4.  From the drop down-menu of the new Material you added, select **Asset reference**.
    
    Click image for full size.
    
5.  Click the **None** dropdown. Then enable **Engine Content** and **Plugin Content** to be visible.
    
    Click image for full size.
    
6.  Click the **None** dropdown menu again. Then, select one of the two following options:
    
    -   **M\_PP\_EDL\_MainPass** - This will apply the EDL to every object in the Level, not just point clouds. If you only display point cloud elements, this is the recommended option.
    -   **M\_PP\_EDL\_CustomPass** \- This will apply the EDL only to objects using **Custom Depth Pass**. This option is recommended if you want to selectively apply EDL.
        
        Enabling Custom Depth Pass will increase the performance cost.
        
7.  To apply the EDL to the whole Level, enable the **Infinite Extent (Unbound)** option on the post-processing volume.
    
    Click image for full size.
    

## Result

EDL has been applied to the Level. Notice the change to edges of objects in the level and how this enhances depth perception.

![Before applying EDL](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b7e3932-c6ae-486b-8503-8bc58cb9e9ac/ue5_05-before-applying-edl.png)

![After applying EDL](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d99df1d6-9b32-4c75-a63e-2a723df1a3f6/ue5_06-after-applying-edl.png)
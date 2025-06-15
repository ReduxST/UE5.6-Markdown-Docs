# Proxy Geometry Shadows

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/proxy-geometry-shadows-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/proxy-geometry-shadows-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:04

---

Calculating dynamic shadows for dense geometry or many small meshes combined can have a high performance cost. Using shadows cast by proxy geometry is a method to reduce that cost, by creating a single, simplified mesh to cast the shadow rather than calculating the individual shadows for more complex meshes or multiple smaller meshes.

An example use case is an apartment building that's made up of many different windows, walls, balconies and other high detail features.

To optimize dynamic shadows using proxy shadows:

1.  In the **Details** panel under **Lighting**, disable **Cast Shadows** on all your meshes for which you want the proxy geometry to cast shadows instead.
    
    ![Disable Cast Shadows under Lighting in the Detail panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b13a8db-642c-411f-ae8d-f18b8d225d74/proxy-shadow-lighting.png)
2.  Add a lower-detail version of the meshes. A proxy shadow caster mesh can be created with the **Merge Actor** tool (using the **Proxy Mesh** tab) if the shape is more organic or complex, but for a square building a regular scaled-up cube will work fine. Refer to the [Proxy Geometry Overview](/documentation/en-us/unreal-engine/proxy-geometry-tool-overview-in-unreal-engine) for more information.
    
    ![The Merge Actor tool Proxy Mesh tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b98ea157-ba6d-4ce7-b4cb-b8410aff8964/merge-actor-proxy.png)
3.  Leave **Cast Shadows** enabled on the proxy shadow caster.
    
4.  In the **Details** panel under **Rendering**, disable **Render in Main Pass** on the proxy shadow caster.
    
    ![Disable Render in Main Pass under Rendering in the Detail panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a7633be-1359-4368-93d4-6a73bc4ebd8f/proxy-shadow-render.png)
5.  Make sure the proxy shadow caster is properly aligned with the visible, higher-detail original.
    

This technique can also work very well for distant objects with **Far Cascade** shadow maps enabled.

Now, the building will appear as if it's casting a shadow but it will be much cheaper and faster to render than before.
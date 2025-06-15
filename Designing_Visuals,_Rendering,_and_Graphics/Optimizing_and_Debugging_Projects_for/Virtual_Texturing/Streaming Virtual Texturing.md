# Streaming Virtual Texturing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/streaming-virtual-texturing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/streaming-virtual-texturing-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:47

---

**Streaming Virtual Texturing** (SVT) is an alternative way to stream textures in your project from disk. SVT has several advantages—along with some disadvantages—when compared to existing mip-based [Texture Streaming](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-streaming-in-unreal-engine) in Unreal Engine.

Traditional mip-based texture streaming performs offline analysis of material UV usage and then at runtime decides which mip levels of a texture to load based on object visibility and distance. This process can be limiting because streaming data considered is the full texture mip levels.

When using high-resolution textures, loading a higher mip level of a texture can potentially have significant performance and memory overhead. Also, the CPU makes mip-based texture streaming decisions using CPU-based object visibility and culling.

Visibility is more conservative—meaning your system is more likely than not to load something—to avoid objects popping into view. So, if even a small part of the object is visible, the entire object is considered visible. The object loaded including any associated textures that may be required to stream in.

In contrast, the virtual texturing system only streams in parts of the textures that UE requires for it be visible. It does this by splitting all mip levels into tiles of a small, fixed size. The GPU determines which of the visible tiles are accessed by all visible pixels on the screen. This means that when UE considers an object to be visible, it's communicated to the CPU which loads the required tiles into a GPU memory cache. No matter the size of the texture, the fixed tile size of the SVTs only considers the ones that are visible. Tile GPU computes visibility using standard depth buffers causing SVT requests to only happen for visible parts that affect pixels.

## Converting Textures and Materials

Enabling virtual texturing for your project means that Textures and Materials require some setup to work correctly; the Texture must enable **Virtual Texture Streaming** support, and the Material's **Texture Samples** are required to use a **Virtual** Sampler Type instead of a non-Virtual one.

Choose from the options below to properly set up your textures and materials for use with SVT.

### Conversion Menu Option

1.  Select any Texture Asset in the Content Browser that you want to convert to use SVT.
    
2.  Right-click to open the context menu and select **Convert to Virtual Texture**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/9112912a-6adc-4ddd-8e75-6d6686889547?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9112912a-6adc-4ddd-8e75-6d6686889547?resizing_type=fit)
    
    This menu option also enables you to convert from a virtual texture to a regular texture as well.
    
3.  The **Convert To** window lists any Texture(s) that you have selected and any Materials that reference them.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/e080bea5-44c9-47f6-9ccc-38ad43c941c6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e080bea5-44c9-47f6-9ccc-38ad43c941c6?resizing_type=fit)
    
4.  Click **Ok** to start the conversion process.
    

During the conversion process, Texture Assets will have **Virtual Texture Streaming** enabled for them in their Texture Editor settings. Materials that reference the selected texture(s) will convert the Texture Sample nodes to use the **Virtual** Sampler Type instead of the non-Virtual Sampler Type.

### Manual Conversion

1.  Open the **Texture Editor** for a given Texture Asset by double-clicking it in the Content Browser.
    
2.  In the **Details** panel under **Texture**, enable **Virtual Texture Streaming**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/af57e1d9-dd32-48db-9097-2784e3d36932?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/af57e1d9-dd32-48db-9097-2784e3d36932?resizing_type=fit)
    

Enabling this without using the [conversion menu option](https://dev.epicgames.com/documentation/en-us/unreal-engine/streaming-virtual-texturing-in-unreal-engine) above will immediately invalidate any existing Materials that reference a converted texture. You should open any Materials that reference the offending texture and set the Texture Sample node to use the correct **Virtual** Sampler Type. For example, a virtual texture should use a Sampler Type of **Virtual Color** instead of **Color**.

When you encounter a Texture Sample node that is not using the correct Sampler Type, UE will display an error message in the **Stats** panel and along the bottom of the node, like this:

[![](https://dev.epicgames.com/community/api/documentation/image/09393432-636b-4f1f-a8e4-362301178f6e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/09393432-636b-4f1f-a8e4-362301178f6e?resizing_type=fit)

1.  The error message identifies the wrong **Sampler Type** for the assigned VT Texture Sample expression.
    
2.  Change the Texture Sample's **Sampler Type** to be one of the **Virtual** types.
    
3.  The VT Texture Sample correctly renders, indicated by the "VT" in the lower-right of the expression.
    

When adding a virtual texture to a Material Graph, UE assigns the Virtual sampler type automatically. However, should you make the expression a Texture Sample Parameter that you can use in Material Instances, keep in mind that the base material applies the Virtual sampler type to all child instances. Remember that you cannot assign a virtual texture to a texture parameter slot that's not already of Virtual type in the base Material.

## UDIM Support

U-Dimension (or "UDIM") is a texture naming convention that enables multiple texture images to map to separate UV regions on a Static Mesh or Skeletal Mesh model. When using the UDIM naming convention, UE will import groups of image files as a single Virtual Texture Asset.

Virtual texturing support for UDIMs is beneficial for a couple of reasons:

-   It works with many separate, smaller textures instead of extremely large textures.
    
-   Each UDIM image can have a different resolution enabling virtual textures that have non-uniform pixel density.
    

For example, if you import a UDIM virtual texture made up of four image files—two 2048x2048 and two 128x128 textures—arranged in a 2x2 pattern, the virtual texture logically samples these images like a single 4098x4098 texture. UE will stretch the smaller 128x128 images to fill the same area as the larger 2048x2048 images without disk or runtime memory usage affected. Having the smaller 128x128 textures fill a 2048x2048 texture resolution doesn't consume any memory in this case.

For additional information on UDIM workflows, see [The Foundry's UDIM Workflow](https://learn.foundry.com/modo/901/content/help/pages/uving/udim_workflow.html) tutorial.

Start using UDIM textures with virtual texturing in your own projects by using this naming convention:

C++

`BaseName.####.[Support Image Format]`

BaseName.####.\[Support Image Format\]

Copy full snippet(1 line long)

For example:

C++

`MyTexture.1001.png`

MyTexture.1001.png

Copy full snippet(1 line long)

When UE imports an image matching this naming convention, it scans the source folder for any additional images matching the same **BaseName** followed by a different coordinate number. For each image that is located, the four-digit number defines the location where UE should map the image. Importing traditional textures map to the mesh UVs in the range of 0-1, however, UDIM image maps to a UV 0-1 space based on its defined UV coordinate.

During import, UDIM textures are flipped vertically because when sampling UVs in Unreal Enigne, the top-left coordinates are (0,0). The UVs of meshes that use UDIM textures are also adjusted on import to work correctly with the orientation of the imported UDIM texture. So, once imported into the engine, the UVs for sampling UVs like the texture above in a material would look like this:

[![](https://dev.epicgames.com/community/api/documentation/image/e650df0e-f425-4420-ab91-bb0172b1ef4a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e650df0e-f425-4420-ab91-bb0172b1ef4a?resizing_type=fit)

## Performance and Cost

Measure the performance and cost of virtual texturing in your project using the sections below:

### Stat Virtual Texturing

Open the console using the backtick (\`) key and enter the following commands to enable their stats information:

Use `stat virtualtexturing` to see details about the virtual texturing scene cost in milliseconds (ms) and counters for page tables.

[![](https://dev.epicgames.com/community/api/documentation/image/5cea1a63-a062-450c-ad55-637bad5f7728?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5cea1a63-a062-450c-ad55-637bad5f7728?resizing_type=fit)

Use `stat virtualtexturememory` to display relevant memory counters related to the use of virtual texturing in the current scene.

[![](https://dev.epicgames.com/community/api/documentation/image/3857c1ab-af93-4741-a4c0-fe0225ab9390?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3857c1ab-af93-4741-a4c0-fe0225ab9390?resizing_type=fit)

### Streaming Virtual Texturing Visualization

Use the console command `r.VT.Borders 1` to draw a mip visualization grid on Materials that use streaming virtual textures.

[![](https://dev.epicgames.com/community/api/documentation/image/a89eeb4d-abfd-40a9-b7b2-531dec65d28a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a89eeb4d-abfd-40a9-b7b2-531dec65d28a?resizing_type=fit)

Use `r.VT.Borders 0` to hide the grid when you no longer need it.

### Material Lookups and Stacks

Sampling from a virtual texture in your materials is more expensive than sampling a traditional texture. You can break the cost of virtual texturing into two categories:

-   **Lookups** happen for each Virtual Texture your project samples in the Material Graph.
    
-   **Stacks** combine Virtual Textures when your project uses the same UVs and Sampler Source.
    

Virtual Textures will always be more expensive than traditional textures sample. There will always be at least two texture fetches and some math instructions. However, some of that cost is amortized by combining the stacks (up to 8) for the VT texture samples that use the same UVs and Sampler Source.

In this simple Material example, UE is sampling two VT Texture Sample expressions using default UVs. A **Virtual Texture Lookup** is added for each lookup of that texture sample and since both are using a single UV, they are combined into a single **Virtual Texture Stack**:

[![](https://dev.epicgames.com/community/api/documentation/image/9f89d8c7-6047-4f26-bfab-8f672fabf7d9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9f89d8c7-6047-4f26-bfab-8f672fabf7d9?resizing_type=fit)

However, if your project uses different UVs, the cost increases with two **Virtual Texture Stack** fetches:

[![](https://dev.epicgames.com/community/api/documentation/image/7326b94a-4d9f-4fef-a812-b52319c79980?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7326b94a-4d9f-4fef-a812-b52319c79980?resizing_type=fit)

The first example uses three texture fetches total: two lookups and one stack. Because the VT samples use the same UVs, UE combines their stacks to save a texture fetch. In the second example, there is a total of four texture fetches: two lookups and two stacks. The VT Texture Samples use different UVs for the Base Color and Normal Texture Samples meaning they cannot be combined into a single stack.

### Additional Material Notes

-   UE splits streaming virtual textures into fixed size tiles for each texture, no matter its size. It also limits the lowest resolution mip by the tile size. In many cases, this won't be an issue, however, textures with a lot of noise or high detail may exhibit aliasing or Moiré effects due to lack of low-resolution mips. Keep in mind that this also poses potential GPU performance cost, although that can be difficult to measure in practice.
    

## Limitations

In general, virtual textures are interchangeable with regular textures with exception that there are some limitations and added cost:

-   Texture dimensions must be a power of 2 but UE does not require them to be square by nature. However, they utilize memory more efficiently in the current implementation.
    
-   Support for trilinear filtering between mips is done in a stochastic manor. When using Temporal Anti-Aliasing (TAA), it is nearly indistinguishable from regular trilinear filtering but can introduce some visible noise in cases.
    
-   UE limits support for anisotropic filtering by the size of the **Tile Border** setting. The default value of 4 allows for less anisotropic filtering than is typical for textures but increasing this value increases memory usage.
    
-   VT streaming is reactive by nature, meaning that the CPU doesn't know it needs to load a given VT tile until after it has already been required by a rendered frame. So, as the camera moves through the scene, some visible popping in may occur, especially as higher resolution VT tiles are loaded.
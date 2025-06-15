# HDRI Backdrop Visualization Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hdri-backdrop-visualization-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/hdri-backdrop-visualization-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:27:22

---

It's often desirable to showcase a model in a visually rich context with minimal effort, and using a High Dynamic Range (HDR) image as a backdrop is a common technique to achieve this.The key benefits of using an HDR image as a backdrop for product visualization is that it's relatively quick to set up, it's customizable, and provides beautiful illumination and reflections. However, using an HDR image as a background is not sufficient on its own. For the result to be plausible, there needs to be a fake ground plane that acts as a shadow catcher to ground the object in the HDR image's environment when being lit, creating consistency between the place object for visualization with the background.

The **HDRI Backdrop** Actor enables you to do all of this and more, improving your product visualization workflow. It automatically handles the following:

-   Background mesh (such as a sky dome or custom geometry)
-   Ambient lighting from a Dynamic Sky Light
-   Dynamic reflections
-   Ground projection with shadow catching

## Enabling HDRI Backdrop

Before you can use this Asset, you need to enable the **HDRI Backdrop** Plugin for your Project.

1.  Open your Project in the **Unreal Editor**.
    
2.  Click the **Edit** in the **Main** menu panel and select **Plugins**.
    
3.  Under the **Rendering** category, locate the **HDRI Backdrop** Plugin and check its **Enabled** box.
    
    Click image for full size.
    
4.  Click **Restart Now** to restart your Project and apply the changes.
    
    Click image for full size.
    

## Workflow

1.  Import a spherical HDR image that uses latitude and longitude into the **Content Browser**. You can do this by using the Import Button, Right-Click context menu, or Drag-and-Drop methods.
    
    Once imported, be sure to set the appropriate **Maximum Texture Size** and **Mip Gen Settings** for the HDR image in the Texture Editor. For additional information, see the [HDR Image Setup](/documentation/en-us/unreal-engine/hdri-backdrop-visualization-tool-in-unreal-engine#hdrimagesetup) section of this page.
    
    Use [HDRI Haven's](https://hdrihaven.com) site to download some interesting HDR images for free, or you can use some of the ones available in that work well with the HDRI Backdrop Actor. Use the Content Browser's **View Options** to enable **Show Engine Content** and **Show Plugin Content** to display **Cubemap** Assets available for use. The engine includes some by default that are stored in the `DatasmithContent Content/Textures` folder.
    
2.  Click the **File** in the **Main** menu panel and select **New Level**. Then, in the **New Level** window, select **Empty Level**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b12c7ed7-e5ca-4334-a92a-9c7501c682c5/03-hdri-new-empty-level.png)
3.  In the **Place Actors** panel under **Lights**, click and drag the **HDRI Backdrop** asset into the **Level Viewport**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42dde220-bb16-4d17-bcfd-83937eabc536/04-hdri-drag-into-level.png)
4.  With the HDRI Backdrop asset selected in your level, use the **Details** panel to set the following:
    
    Click image for full size.
    
    1.  **Cubemap:** Choose a cubemap from the available options or drag one from the **Content Browser** onto this slot.
        
        Use the **Mesh** assignment parameter to select an appropriate mesh when using cubemaps that don't display well with a dome or spherical shaped mesh, such as a warehouse or boxed style space.
        
    2.  **Size:** Adjust the value here to set the size of the mesh that the HDR image is being projected onto.
        
    3.  **Projection Center:** Select the 3D gizmo to move the projection center to match your camera placement and adjust as needed to reduce skewing and stretching of the HDR image on the backdrop.
        
        See the [HDRI Backdrop Settings](/documentation/en-us/unreal-engine/hdri-backdrop-visualization-tool-in-unreal-engine#hdribackdropsettings) section of this page for further details about these and other settings you can adjust.
        
5.  Optionally, add a **Light Source** and set it to **Movable** if you want dynamic shadows in your visualization.
    
    Click image for full size.
    

### HDR Image Setup

When you import an HDR image as an Unreal Asset, it isn't modified by the HDRI Backdrop Actor. You need to manually apply several settings in the [Texture Editor](/documentation/en-us/unreal-engine/texture-asset-editor-in-unreal-engine) first:

Click image for full size.

1.  The **Imported**, **Displayed**, and **Max-In-Game** resolution of this HDR image.
    
2.  The **Mip Gen Settings** should be set to **NoMipmaps** to use the full quality.
    
3.  The **Maximum Texture Size** should match the larger resolution value of the imported HDR image — 4096 in this example.
    

If you do not change these values, your HDR image will not appear correctly. It will have low resolution and look muddy.

### HDR Image Backdrop Mesh Setup

Not all HDR images are created equal and may require their own custom geometry to project onto. In the Editor, there are several backdrop meshes to choose from, in addition to the HDR images provided.

Before you can see the available Static Meshes in the asset selection drop-down window, you must first use the **Settings** to enable **Show Engine Content** and **Show Plugin Content**.

Click image for full size.

Use the asset selection box next to **Mesh** to choose an environment mesh to project the HDR image onto. This can be any Static Mesh, such as custom geometry you've created or one of the three that are provided in the engine.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29c14f57-a11d-4487-960f-9cf6f2db5fc4/09-hdri-mesh-selecting.png)

| Backdrop Mesh | Mesh | Description |
| --- | --- | --- |
| **EnviroDome** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af3c5933-ba28-4521-b237-259c98f66355/10-hdri-sky-dome.png) | A sky dome mesh with a ground plane that is ideal for large exterior environment HDR images. |
| **EnviroBoxSharp** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c83c6afc-bf92-417e-ad0f-49e48874a0f4/11-hdri-enviro-box-sharp.png) | A box environment with hard edges that is ideal for interior environments, like a warehouse or space with walls that are well defined. |
| **EnviroBox** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09e8a084-66f5-457c-88ac-ae07f4868319/12-hdri-enviro-box.png) | A box environment with smoothed edges that is ideal for studio-like environments, often ones like those with single color backdrop cloths. |

Below, these examples demonstrate each Mesh backdrop included with the Engine:

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e5a258d-466a-4508-80dc-86ec4f654137/13-hdri-scene-sky-dome.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04792b40-6a31-4592-b3d3-e12d1fb98918/14-hdri-scene-box-sharp.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c3ba5a6-31c6-49fa-9e5b-3e25d19cf4c1/15-hdri-scene-box-smooth.png) |
| Default EnviroDome | EnviroBoxSharp | EnviroBox |

## HDRI Backdrop Settings

The following settings can be set, enabled, and adjusted from the **Details** panel of the HDRI Backdrop asset when selected in your level:

| Property | Description |
| --- | --- |
| **Cubemap** | Assign an imported HDR image that will be projected onto the ground and backdrop, and is used by the built-in Sky Light source. |
| **Intensity** | 
Sets the intensity of the embedded Sky Light and how emissive the backdrop HDR image is. Higher values result in brighter ambient lighting being samples from the HDR image (cd/m2).

Note that the physical lighting units are measured in cd/m2, like the Sky Light or Emissive Materials. Sun and Sky sources have that range in the thousands of units, which it does hand-in-hand with physical cameras where the Exposure Value (EV) are in the range of EV100:14 (see the "Sunny 16" rule). However, with the HDRI Backdrop asset, it is not required to use physically correct values, but you may need to set the EV to something significantly lower than the EV100:14. It's also worth noting that some HDR images range from 0 to 5.0 or greater than 5 cd/m2 while others are ranging from 0 to 100K units. This means that when you swap HDR images, there may be a noticeable difference in brightness changing.



 |
| **Size** | Sets the size (in meters) of the mesh used to project the HDR image. It controls the diameter of the backdrop mesh and should be adjusted based on the HDR image used, the horizon height, and the content in the scene. For most exterior scenes, a typical size should be approximately 100 meters. |
| **Projection Center** | Defines the projection point of the HDR image. |
| **Lighting Distance Factor** | Specifies the ground area that will be affected by lighting and shadows. Lit areas will have slightly different shading depending on the intensity and other lighting parameters in the scene. This enables the lit area range to blend smoothly around the camera to reduce shading differences with the background HDR projection. |
| **Use Camera Projection** | Disables ground tracking and enables the HDR image to follow the camera. |
| **Mesh** | Specify a custom Static Mesh object to use as a backdrop from which the HDR image is projected. |

### Projection Center

The Projection Center of the HDR image on the backdrop should be set to match the height of the camera used to capture the image.

Select the 3D gizmo to define the central location of the projection in 3D space:

Or, you can manually enter these values in the transform text boxes (however, for the smoothest interaction, it's recommended to use the 3D gizmo in the **Viewport**):

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aeb6f89e-90bb-4b14-b0df-d57cd6900ffe/16-hdri-project-centr-setting.png)

-   Z (Height) should be approximately 90 centimeters (cm), which is the average height of a camera tripod used to capture the HDR image. However, the height depends on the height of the camera that was used to capture the image, so you may need a different value.
-   X and Y enables you to offset the projection origin. In most instances, this shouldn't be changed.

### Lighting Distance Factor

You can add your own lighting to your scene and adjust any of the parameters, however, there may be instances where the lighting and shadow intensity differs from the backdrop. The **Lighting Distance Factor** enables you to define the ground area around the camera to blend the scene's lighting and shadows to reduce these differences.

![Lighting Distance Factor: 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/948ad70a-6dc7-480e-bc83-117db61894ca/17-hdri-lighting-dist-factor-0.png)

![Lighting Distance Factor: 0.5 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ed19d17-e711-44df-975b-e5d83345704d/18-hdri-lighting-dist-factor-1.png)

The **Lighting Distance Factor** value is a percentage of the Dome's **Size** value. A typical value would be around 0.5, or a little higher. Artifacts can happen if this is not used carefully. When set too high, a horizontal line will appear at the backdrop edge, and lower values will help to resolve these artifacts.

In instances where compositing shadows and ambient occlusion (AO) on the backdrop is not needed, you can set the value to 0.

## Additional Notes

Below are some additional notes and suggestions when working with the HDRI Backdrop asset:

-   **Interaction with the Sky Light Actor**
    
    When adding the HDRI Backdrop to your scene, it creates a dynamic [Sky Light](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine) as a sub-component. If a regular Sky Light exists, it should be deleted. Otherwise, the scene will have multiple Sky Lights which will affect performance, quality, and the desired result in the scene.
    
-   **HDR Image Stretching**
    
    To achieve the best result with minimal stretching, the Camera should be placed and looking around the origin of the projection. Adjusting the [Projection Center](/documentation/en-us/unreal-engine/hdri-backdrop-visualization-tool-in-unreal-engine#projectioncenter) reduces the stretching in favor of relative scaling.
    
-   **Ray Tracing Features**
    
    The HDRI Backdrop works with all of Unreal Engine's light types along with supported [Hardware Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) features. The HDRI Backdrop Blueprint includes a Sky Light component by default with **Cast Ray Tracing Shadow** enabled, which is the prerequisite to do proper image-based lighting (IBL) with ray tracing.
    
    Also, keep in mind, that additional Ray Tracing features can be enabled and set in a Post Process Volume, when adding one to your scene. You can control Ambient Occlusion, Global Illumination, Translucency, and Reflections.
    
-   **Intensity, HDR Content, and Exposure**
    
    The HDR image is fed into and driven by a Sky Light. The content of the HDR image will greatly affect the brightness of the scene. The HDRI Backdrop asset doesn't attempt to perform normalizations of the pixel values in the HDR image to provide a *stable* intensity regardless of its content. This means that when you switch between different HDR images, you will need to adjust the Intensity since this is not handled automatically. However, this may be added in a future release.
    
-   **High Precision Normals**
    
    Changing this G Buffer format option encodes the `Default` format at 16 bits per-channel. It produces higher quality reflections along smooth, high-poly geometry. When using the default format, you may see artifacts that present themselves as wavy reflections across these smooth, reflective surfaces.
    
    In the **Project Settings** under **Rendering > Optimizations**, use the **GBuffer Format** dropdown to select **High Precision Normals**.
    
    ![High Precision Normals: Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/942ba9a2-1eb8-4423-b246-1f5bcf1c81b5/19-hdri-high-precision-normal-0.png)
    
    ![High Precision Normals: Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0883daf8-cf3e-4672-91ad-32b429e340c5/20-hdri-high-precision-normal-1.png)
    
-   **Reflection Capture Resolution**
    
    Changing this value enables you to have high quality reflections from Cubemaps and HDR images projected onto the skydome and Reflection Capture Actors in the scene.
    
    In the **Project Settings** under the **Rendering > Reflections** category, set a power of 2 value for your desired **Reflection Capture Resolution**. This resolution will automatically apply to all reflection captures placed in your scene. For the **Sky Light**, you can set the maximum resolution value you want to use.
    
    ![Reflection Capture Resolution: 128 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8a54584-7634-44e9-abb4-f78e84e488c9/21-hdri-refl-capture-resolution-128.png)
    
    ![Reflection Capture Resolution: 1024](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ca2f990-f151-4452-a6a8-1471a7993973/22-hdri-refl-capture-resolution-1024.png)
    

## Additional Resources

-   NASA's Juno 3D Model provided by "[NASA 3D Resources](https://nasa3d.arc.nasa.gov/detail/eoss-juno)."
-   HDR Images provided by "[HDRI Haven](https://hdrihaven.com)."
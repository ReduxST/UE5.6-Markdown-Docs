# Mobile Depth of Field

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mobile-depth-of-field-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mobile-depth-of-field-in-unreal-engine)  
**Processed:** 2025-06-14 16:36:25

---

The following depth of field (DOF) method provides an optimized and low-cost depth of field effect for mobile platforms using the Forward rendering path.

## Gaussian

Gaussian depth of field has been removed for use with the **Deferred Renderer** and **Desktop Forward Renderer** and only supports mobile platforms. To use this Gaussian DOF while working in Editor on a desktop computer, enable one of the mobile platform previewers using the [Mobile Previewer](/documentation/404).

The **Gaussian** depth of field method blurs the scene using a standard [Gaussian blur](https://en.wikipedia.org/wiki/Gaussian_blur) (or smoothing) function. Gaussian DOF blur foreground and background uses a fixed-size Gaussian blur kernel, which is very fast on lower-end hardware, such as mobile. This enables performance to be maintained with lower overhead costs where performance is critical.

![No Depth of Field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de97a6e1-6034-49b2-b419-57f1b9271f33/image_0.png)

![Gaussian Depth of Field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2e0113b-b934-4ab8-b1cd-5d2432ab4bf5/image_1.png)

## Visualizing Depth of Field

These layers, including transition regions, can be visualized using the **Depth of Field layers** show flag in the Level Viewport under **Show > Visualize**.

![Final Scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a0dd33c-deed-49dc-af7c-f75c9b769e6b/image_2.png)

![Depth of Field Visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c80f531-29bb-43c7-ae7d-a3d28b307a99/image_3.png)

Visualizing the **Depth of Field Layers** also includes useful information relevant to the DOF method selected by including the properties and their currently set values.

![Information relevant to the DOF method selected by including the properties and their currently set values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c111feb1-0814-498e-b698-ef9c91b47d0f/ue5_1-image-4.png)

## Focal Distance

The **Focal Distance** represents the focal region and the angle of view that will be captured. A longer focal length has a shallow depth of field causing objects to be more blurred outside of the focal region while shorter focal lengths have a wider depth of field with sharper focus and fewer objects out of focus. The f-stop number can stay the same and changing the lens size adjusts how shallow or wide the depth of field effect is.

Click image for full size.

Once you've set the **Focal Distance** and the **Focal Region**, you can use the **Near Transition** and **Far Transition** to adjust the distance between the focal region and the fully blurred scene. In addition, you can even adjust the **Near Blur Size** and the **Far Blur Size** to further tweak the look of Gaussian DOF.

![Gaussian DOF](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1787b0af-b7c4-4952-ba46-ff6e6e965387/image_6.png)

Gaussian DOF with adjusted values for Near/Far Transition and Blur Size to produce a nice depth of field effect.

In this example, the following values have been set to produce a soft depth of field effect for near and far regions.

-   Focal Distance: **215**
    
-   Scale: **2500**
    
-   Near Transition: **500**
    
-   Far Transition: **400**
    
-   Near Blur Size: **2.0**
    
-   Far Blur Size: **2.5**
    

## Available Settings

The Gaussian DOF settings and properties can be found under the Post Process Volume's **Details** panel in the **Lens** category under **Mobile Depth of Field**.

| Property | Description |
| --- | --- |
| **High Quality Gaussian DOF on Mobile** | Enables HQ Gaussian on high-end mobile platforms. |
| **Focal Region** | Artificial region where all content is in focus starting after DepthOfFieldFocalDistance. This value is measured in Unreal Units (cm). |
| **Near Transition Region** | The distance in Unreal Units from the focal region on the side nearer to the camera over which the scene transitions from focused to blurred when using Bokeh or Gaussian DOF. |
| **Far Transition Region** | The distance in Unreal units from the focal region on the side farthest from the camera over which the scene transitions from focused to blurred when using Bokeh or Gaussian DOF. |
| **Scale** | This blends the DOF in the scene. A value of 0 turns it off. |
| **Near Blur Size** | 
The maximum size (in percent of the view width) of the near blur for Gaussian-based DOF.

Note that performance cost scales with size.



 |
| **Far Blur Size** | 

The maximum size (in percent of the view width) of the far blur for Gaussian-based DOF.

Note that performance cost scales with size.



 |
| **Occlusion** | The occlusion tweak factor of 1. Using a value of 0.18 gets natural occlusion and a value of 0.4 solves layer color leaking issues. |
| **Sky Distance** | 

Artificial distance to allow the skybox to be in focus (for example, 200000 units), where values less than 0 will disable the feature.

Note that this feature can cost performance.



 |
| **Vignette Size** | 

Artificial circular mask to (near) blur content outside the radius diameter in percent of the screen width.

It adds performance costs if the mask is used.



 |
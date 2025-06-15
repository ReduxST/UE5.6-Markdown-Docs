# Adding Detail Textures

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/adding-detail-textures-to-unreal-engine-materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/adding-detail-textures-to-unreal-engine-materials)  
**Processed:** 2025-06-14 16:05:01

---

When viewing a Material very closely, you will notice that the textures used in the Material can break down and become pixelated. To optimize performance, textures are often scaled to a resolution that looks good from moderate distances, but may not hold up to close scrutiny.

To address this issue, you can use what is known as a **detail texture** to prevent a Material from looking pixelated when it is viewed very closely.

## Detail Texturing

**Detail texturing** allows you to give the illusion of more detail in a texture by layering a highly repeated diffuse and normal texture over the object's original diffuse and normal textures. This gives the illusion of greater detail at close range than usually would be possible.

Here is an example of detail texturing in action.

[![Brick Material with and without detail texture](https://dev.epicgames.com/community/api/documentation/image/882565ac-19b7-4196-b528-3c14d4c82ae3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/882565ac-19b7-4196-b528-3c14d4c82ae3?resizing_type=fit)

On the left side (labeled 1), the Material uses a detail texture to add additional high-frequency details to the surface. On the right side (labeled 2) the Material does not use a detail texture. Note that the image on the left appears sharper and more detailed than the image on the right.

## Detail Texturing Node Breakdown

If you search in the **Palette** or context menu for "detail texturing", you will find a **Detail Texturing** Material Function. While this is not the only way that you can apply detail textures to Materials, it is the fastest from a workflow perspective, since all the logic is contained within the [Material Function](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-functions-in-unreal-engine). All you need to provide is texture inputs.

[![Detail Texturing Material Function node](https://dev.epicgames.com/community/api/documentation/image/f6c4d63c-6369-4059-8dea-5444f45cef43?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f6c4d63c-6369-4059-8dea-5444f45cef43?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Scale (S)**

 | 

This sets the scale of the detail texture. Bigger numbers result in more titling smaller numbers results in less titling.

 |
| 

**Diffuse (V3)**

 | 

This is the input for the Diffuse Texture.

 |
| 

**DetailDiffuse (T2d)**

 | 

This is the input for the Diffuse Detail Texture. This input can only accept a Texture Object.

 |
| 

**DiffuseIntensity (S)**

 | 

This controls the intensity of the Detail Diffuse Texture.

 |
| 

**Normal (V3)**

 | 

This is the input for the Normal Map Texture.

 |
| 

**DetailNormal (T2D)**

 | 

This is the input for the Normal Map Detail Texture. This input can only accept a Texture Object.

 |
| 

**NormalIntensity (S)**

 | 

This controls the intensity of the Detail Normal Map Texture.

 |

### Converting Texture Sample to Texture Objects

In order for the Detail Texturing Material Function to work correctly, you will need to convert the Textures you want to use as the Detail Textures from regular Texture Samples into Texture Objects. Use the following steps to do this.

1.  Find the Texture Sample you want to use as a detail texture.
    
    [![Regular texture sample](https://dev.epicgames.com/community/api/documentation/image/dec2efc8-4707-44f7-8c70-ae8f663f08b2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dec2efc8-4707-44f7-8c70-ae8f663f08b2?resizing_type=fit)
    
2.  Right click on the Texture Sample node and select **Convert To Texture Object** from the context menu.
    
    [![Convert Texture Sample to Texture Object](https://dev.epicgames.com/community/api/documentation/image/2bb6296b-e05f-45e6-a8c6-566adf1c974f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2bb6296b-e05f-45e6-a8c6-566adf1c974f?resizing_type=fit)
    
3.  The Texture Sample is converted to a Texture Object.
    
    [![Texture Object node](https://dev.epicgames.com/community/api/documentation/image/c12fc106-b7a5-448f-a1fb-979a297524fe?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c12fc106-b7a5-448f-a1fb-979a297524fe?resizing_type=fit)
    

## How to Use Detail Texturing in your Material

There are two ways you can configure a Material to use Detail Texturing, and both of these are documented below. The main difference between the two methods is whether to use the premade Detail Texturing Material Function, or to create the detail texturing logic manually in the Material graph. Neither option is better or worse, as they produce the same results in the end. The method you choose to use depends on the needs of the specific Material and project.

All of the content used in the following sections is available in the Unreal Engine **Starter Content.** While the techniques that are shown here will work with any Textures, if you want to follow along, make sure your project includes the **Starter Content**.

Create a new Material to use for testing. **Right-click** in the **Content Browser** and choose **Material** from the Create Basic Asset section in the context menu. Give the Material a descriptive name like **DetailTexturing**.

[![Create new Material](https://dev.epicgames.com/community/api/documentation/image/7a548a6b-6948-4e29-9540-55a6832a0d1f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7a548a6b-6948-4e29-9540-55a6832a0d1f?resizing_type=fit)

### Using The Detail Texturing Material Function

1.  Open the Material by **double-clicking** the asset in the **Content Browser.** The Material Editor opens.
    
2.  Find the following four textures in the Starter Content. Drag them from the Content Browser into your Material graph.
    
    -   **T\_Brick\_Clay\_Old\_D**
        
    -   **T\_Brick\_Clay\_Old\_N**
        
    -   **T\_Ground\_Gravel\_D**
        
    -   **T\_Ground\_Moss\_N**
        
    
    When completed, your Material Graph should look like this:
    
    [![Four texture sample nodes](https://dev.epicgames.com/community/api/documentation/image/b0beffad-cfff-4889-a2a4-e8736d2faa19?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b0beffad-cfff-4889-a2a4-e8736d2faa19?resizing_type=fit)
    
3.  **Right-click** in the Material graph and search for "Detail Texturing" in the context Menu. Click on **DetailTexturing** under the Misc category to add the Material Function to your graph.
    
    [![Material Editor right-click search menu](https://dev.epicgames.com/community/api/documentation/image/2a132e62-a971-411f-82c3-1e0a74995e9c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2a132e62-a971-411f-82c3-1e0a74995e9c?resizing_type=fit)
    
4.  A **DetailTexturing** Material Function is created in the Material Graph.
    
    [![DetailTexturing Material Function in graph](https://dev.epicgames.com/community/api/documentation/image/08c33161-24b5-4b71-b38c-b64dd57a523b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/08c33161-24b5-4b71-b38c-b64dd57a523b?resizing_type=fit)
    
5.  In this example the **T\_GroundGravel\_D** and **T\_Ground\_Moss\_N** will be used as detail textures. In order to connect detail textures to the Material Function they must be converted to Texture Objects. Right-click on **T\_GroundGravel\_D** and **T\_Ground\_Moss\_N** and convert them to Texture Objects.
    
    [![Detail textures converted to texture objects](https://dev.epicgames.com/community/api/documentation/image/0f26920f-c202-4c92-b31f-345d7310e0c8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0f26920f-c202-4c92-b31f-345d7310e0c8?resizing_type=fit)
    
6.  Connect all the nodes as shown below. The two brick textures should connect to the **Diffuse** and **Normal** inputs, and the two Texture Objects should connect to the **DetailDiffuse** and **DetailNormal** pins. Pass the Diffuse output into Base Color and the Normal output into the Normal input on the Main Material Node.
    
    [![Material Function wired](https://dev.epicgames.com/community/api/documentation/image/bbe96671-c2c8-4642-a448-8b7b9b21e692?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bbe96671-c2c8-4642-a448-8b7b9b21e692?resizing_type=fit)
    
7.  Additonal values are needed to control the scale and intensity of the textures. You could use either a **Constant** Material Expression or **Scalar Parameter** for these inputs. This example uses three Scalar Parameters named **Scale,** **Diffuse Intensity,** and **Normal Intensity.** The default value in all three of these nodes is set to **1.**
    
    [![Three scalar parameters](https://dev.epicgames.com/community/api/documentation/image/e1750f44-688f-4e8a-8943-e1d02ea16d7f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e1750f44-688f-4e8a-8943-e1d02ea16d7f?resizing_type=fit)
    
8.  Connect the Scalar Parameters to their corresponding inputs. When completed, your Material Graph should look like this.
    
    [![Final Material graph](https://dev.epicgames.com/community/api/documentation/image/940ce941-1376-403f-bad2-2e88fd10e326?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/940ce941-1376-403f-bad2-2e88fd10e326?resizing_type=fit)
    
9.  By adjusting the values in the Scalar Parameters, you can modify how the Detail Textures will look. Here is an example of what happens when you set the Scale to a value of 1, then 5, and finally 10. The detail texture tiles more times across the mesh, meaning the texture itself appears smaller or finer.
    
    [![Detail tiling at different scales](https://dev.epicgames.com/community/api/documentation/image/ff4d8c8e-80f8-433c-bacd-85a687c401cf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ff4d8c8e-80f8-433c-bacd-85a687c401cf?resizing_type=fit)
    

### Setting Up Detail Texturing Manually

If for whatever reason you cannot use the **Detail Texturing** Material Function, you can build this functionality inside the Material Graph using Material Expression nodes and the directions below.

1.  Duplicate the first Material in the **Content Browser** by right-clicking the thumbnail and choosing **Duplicate** from the context menu. Rename the new Material **DetailTexturing\_02** and double-click to open it in the Material Editor.
    
    [![Create another Material](https://dev.epicgames.com/community/api/documentation/image/c587c8b8-6c8e-41d1-8581-ff43ead4890f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c587c8b8-6c8e-41d1-8581-ff43ead4890f?resizing_type=fit)
    
2.  Delete everything except the four textures. You also need to convert the two Texture Objects back to Texture Samples. Right click each Texture Object node and choose **Convert to Texture Sample** from the context menu.
    
    [![Convert to texture sample](https://dev.epicgames.com/community/api/documentation/image/39bb7d5e-34e7-4726-bf6d-9d2d84991fbb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/39bb7d5e-34e7-4726-bf6d-9d2d84991fbb?resizing_type=fit)
    
3.  The following Material Expression nodes are needed to create detail texturing manually. You can find each of the following by searching for them in the **Palette** or using the search bar in the **right-click** context menu.
    
    -   **Texture Coordinate** x 1
        
    -   **Clamp** x 1
        
    -   **Scalar Parameter** x 2
        
    -   **Add** x 2
        
    -   **Multiply** x 3
        
    
    When completed, the Material Graph should look like this.
    
    [![All required Material expression nodes](https://dev.epicgames.com/community/api/documentation/image/6f4f5ecf-3fed-4fef-adb7-8dfdc1d0c480?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6f4f5ecf-3fed-4fef-adb7-8dfdc1d0c480?resizing_type=fit)
    
4.  After you add all the nodes to your graph, begin connecting them as shown. The image below shows the correct configuration for the Base Color portion of the graph. When completed, the Material Graph should look like this.
    
    [![Base Color Material Graph](https://dev.epicgames.com/community/api/documentation/image/df781f89-42c6-4675-938e-28a9d8183a68?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/df781f89-42c6-4675-938e-28a9d8183a68?resizing_type=fit)
    
    *Click image to enlarge.*
    
5.  The logic created in the Base Color section to control texture scale can be reused with the normal maps. Connect the nodes as shown below.
    
    [![Normal Map section](https://dev.epicgames.com/community/api/documentation/image/ca284c45-8fba-4154-bbff-5dc589a12413?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ca284c45-8fba-4154-bbff-5dc589a12413?resizing_type=fit)
    
    *Click image to enlarge.*
    
6.  With the Base Color and Normal map now all connected together, the Material is now ready to be compiled, saved, and used.
    
    [![Final Material setup](https://dev.epicgames.com/community/api/documentation/image/aea89f05-1ebc-4d24-ad10-9e329ff9bdec?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/aea89f05-1ebc-4d24-ad10-9e329ff9bdec?resizing_type=fit)
    
    *Click image to enlarge.*
    

## Detail Texturing Tip & Tricks

The following section covers some tips and tricks on different ways you can use detail texturing in your Materials.

### Distance Based Detail Texturing

When dealing with large surfaces, such as terrain, you may notice that even though your textures tile seamlessly there is noticeable repetition that weakens the appearance of the texture, especially when viewed in the distance.

To fix this, you can modify the Detail Material that was created previously to allow it to display one texture when the camera is close and another texture when the camera is far away. This is often referred to as distance-based texture blending. You can implement this by following the instructions below.

1.  First duplicate the **DetailTexturing\_02** Material and rename it **DistanceFade**. Open the Material.
    
2.  You can delete most of the node connections from the original Material, but do not delete the four textures. You should also keep the section labeled **Scale Controls** below. Search for and add the following Material Expressions to your graph.
    
    -   World\_Position x 1
        
    -   Camera\_Position\_WS x 1
        
    -   Distance x 1
        
    -   Divide x 1
        
    -   Power x 1
        
    -   Clamp x 1
        
    -   Constant x 2
        
    
    When completed, the Material Graph should look like this.
    
    [![Distance fade nodes](https://dev.epicgames.com/community/api/documentation/image/a1ead2a5-4c7f-4620-9955-ac1c51269529?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a1ead2a5-4c7f-4620-9955-ac1c51269529?resizing_type=fit)
    
3.  Change the values in the two **Constant** Material expressions to **512** and **4**, and then connect the nodes in the configuration shown below. The distance at which the texture blend occurs is controlled by the first **Constant** that is plugged into the **Divide** Material expression (set to 512 in the example image). The Material graph shown below provides all the logic needed to blend textures based on distance.
    
    [![Distance fade Material logic](https://dev.epicgames.com/community/api/documentation/image/ce167908-251b-444d-8469-226aa907d29e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ce167908-251b-444d-8469-226aa907d29e?resizing_type=fit)
    
4.  You can now connect the distance fade logic to the rest of the gaph. First add two **Linear Interpolate (Lerp)** nodes to the graph. The Alpha input on the Lerp nodes will drive the transition between the two textures. Finish wiring up the Material as shown below.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/aac38c61-c2ee-4be0-9789-b832f891771c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/aac38c61-c2ee-4be0-9789-b832f891771c?resizing_type=fit)
    
5.  To preview the effect, hold down the **Right Mouse Button** in the Material preview viewport and move the mouse up and down to zoom in and out. When the camera is 512 units away from the sphere, the Material will transition from brick to gravel. If you can't see this happening, you can adjust the value in the **Constant** plugged into the Divide node. Reducing the value from 512 to something smaller will cause the transition to occur sooner.
    

## Conclusion

Detail Texturing is a very powerful tool that can improve the appearance of Materials by supplementing the base textures with highly repeated detail textures. Keep in mind that Detail Texturing can only help to hide pixilation to a certain point, and allowing the player's camera to zoom into objects to an unreasonable degree can negate the benefits of detail texturing. Also remember that adding detail texturing could add two or more additional texture lookups to your Material, which may present performance or memory issues, especially on mobile platforms.
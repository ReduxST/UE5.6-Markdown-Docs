# Previewing and Applying your Materials

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/previewing-and-applying-your-materials-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/previewing-and-applying-your-materials-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:15

---

Previewing and applying your Materials is of critical importance to the Material creation process because it allows you see the results of the changes you make in the Material Graph. This is something you should do quite often to make sure that you are getting the exact results you want. This guide explains how to preview your Materials in the Material Editor viewport, and then shows how to apply a Material to meshes in Unreal Engine.

## Previewing in the Material Editor Viewport

The easiest way to preview a Material is in the Material Editor **viewport** window. The viewport window has a number of different options to customize the look and feel of the preview environment. The image below shows a breakdown of the viewport and its various options.

![Material Editor Viewport breakdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e96a9313-ee86-47cd-894b-43fb45dcaec6/material-editor-viewport-ue5.png)

| Number | Property | Description |
| --- | --- | --- |
| 1 | Viewport Options | This menu contains a toggle to turn the Realtime preview on and off. Also contains viewport statistics, layout options, and field of view (FOV) settings. |
| 2 | Viewport Types | Switch between perspective and orthographic viewports. |
| 3 | View Modes | Choose from available View Modes and change exposure settings. |
| 4 | Viewport Show Flags | Show or hide the background, grid, and viewport stats. |
| 5 | Preview Mesh | This is a preview mesh that you can use to examine how your Material will look on different objects. |
| 6 | Preview Mesh Options | Select from five different preview mesh options: cylinder, sphere, plane, cube, or a custom mesh. |

While inside the Material Editor, hover your mouse cursor over any icon to display a tooltip description explaining what each of the properties does. Some of these tooltips contain links to relevant documentation.

While you are creating your Materials in the Material Editor, the viewport window will show your changes immediately if you have the **Realtime** option enabled. Realtime is enabled by default. You can toggle this option on and off from the **Viewport Options** menu.

![Realtime Preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92a541a0-ebde-4dfd-9ebb-2bc960d9b96a/toggle-realtime.png)

Adjust the values in any Material Expression currently hooked up to the [Main Material Node](/documentation/en-us/unreal-engine/using-the-main-material-node-in-unreal-engine) to preview changes in the viewport.

When making changes to your Material Network, it can take some time for the changes to render correctly in the viewport. The more complex a Material becomes, the longer it can take for the preview window to update. If you find that you need a quicker update, consider making your Material into a [Material Instance](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine).

### Preview Scene Settings

The **Preview Scene Settings** panel enables you to quickly preview your Materials in a variety of different environments and lighting conditions. This gives you a better understanding of how your Material will interact with light as the conditions change.

Go to **Window > Preview Scene Settings** in the menu bar enable the panel.

![Enable the Preview Scene Settings panel.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbca3b39-edbd-4bdb-88ba-28eaffe132bd/open-preview-scene-settings.png)

The **Preview Scene Settings** panel opens in the bottom left corner of the Material Editor next to the Details tab.

![Preview Scene Settings interface options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e193922-a1ea-41b4-943f-cd06808dea3d/preview-scene-settings-tab.png)

Preview Scene Settings contains options to alter the color, direction, and intensity of the viewport lighting. You can also change the background, and add basic post-processing effects.

This lets you view a Material under very different lighting conditions without changing anything in the Level.

![Default viewport settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e61e98d6-ac82-41e4-b315-c41dda2d93fd/preview-scene-settings-compare-01.png)

![Modified preview scene settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/721752df-6690-41b6-ba9f-cc50ca83d6ce/preview-scene-settings-compare-02.png)

### Previewing a Specific Node in the Material Graph

There are times when you may want to see the results of a single node in your Material graph. For example, if you are creating a Material that uses the [Fresnel Material expression](/documentation/en-us/unreal-engine/using-fresnel-in-your-unreal-engine-materials), you might want to preview the node so you can accurately fine-tune the falloff of the Fresnel effect.

**Right-click** a Material Expression and choose **Start Previewing Node** from the menu to preview that node in the viewport.

![Start previewing a Material Expression node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a72fea9-d7d7-45f2-a8c5-a2aafe2c3210/start-previewing-node.png)

The Fresnel node turns blue to indicate that it is currently being previewed. In the preview viewport you can clearly see the boundary of the Fresnel effect without any visual interference from other attributes like textures or reflections.

![Fresnel node preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8f29e94-4a89-474b-8328-e6a8fd805135/node-preview-fresnel.png)

To stop previewing a node, **right-click** it and choose **Stop Previewing Node.**

![Stop previewing Material node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6fde9ca8-e24d-40cd-9cf2-653c2d393cf5/stop-previewing-node.png)

### Previewing Materials on a Custom Mesh

The Material Editor viewport provides four built-in preview mesh options: cylinder, sphere, plane, and cube. You can also preview your Material on a custom mesh.

1.  Select any **Static Mesh** in the Content Browser.
    
    ![Select Static Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d37a832-d121-446b-82e4-016d34814673/stairs-static-mesh.png)
2.  Click the teapot icon in the bottom right corner of the Material Editor viewport to use the selected Static Mesh as the preview object.
    
    ![Custom Material Editor preview mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/775884fe-ccd6-408a-881b-b77bae5ccc77/custom-mesh-preview.png)

## How to Apply Your Materials

### Compile and Save

The Material Editor viewport preview updates continually as you make changes to the Material network. However, before you can apply a Material to an object and view it within your level, it needs to be **compiled**. To compile a Material, click the **Apply** or **Save** button on the left side of the Material Editor toolbar.

![Material Editor Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bedfd3ea-8c48-4140-bd6c-58c812a6432f/save-and-apply.png)

This will update the Material to include the changes you were just previewing. You can then apply it to a mesh and view it in the Level.

There are two main ways that you can apply Materials to objects in Unreal Engine:

### Drag-and-Drop

Select a Material from the **Content Browser** and then drag it directly onto any object in the Level.

1.  Left-click and drag a Material from the Content Browser onto an object. Release the left mouse button while hovering over an object to apply the Material.
    
    ![Apply a material by drag-and-drop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97b6febc-9113-41af-8a6d-2efef0ca3526/drag-onto-actor.png)
2.  The new Material is applied to the object.
    
    ![New material applied to mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d693077-07fa-4302-a9d6-c8dee6d99a9e/apply-mat-result.png)

### Apply a Material from the Details Panel

You can also apply a Material from the object's **Details** panel by clicking the **Use selected asset from Content Browser** button like in the following example:

1.  Select a Material in the Content Browser.
    
    ![Select Material in Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46e20fc2-fbe3-48d6-ac9a-b946e339a787/select-material-content-browser.png)
2.  Select an Actor in the viewport.
    
    ![Select Actor in viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e41a30bd-4cae-4aa6-b85b-bc3a871ef1ae/select-actor.png)
3.  Click the **Use Selected Asset from Content Browser** button in the Materials section of the object's **Details** panel.
    
    ![Use Selected Asset from Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1ac3fc9-d085-459a-8442-9b4754209f5e/assign-material-from-details-panel.png)
4.  The new Material is applied to the object.
    
    ![New Material on mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7705404d-f6e2-42e8-850a-cb6f7feb3e82/new-material-applied.png)

## Previewing Material Parameters in the Level

The following feature requires you to use Scalar or Vector parameters, which can be updated dynamically without recompiling a Material. Read the documentation about [Material Instances](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) to learn about parameterization.

You can adjust **Scalar** and **Vector** parameters inside the Material Editor and see the results instantly in all 3D viewports.

This is especially useful for [Material Functions](/documentation/en-us/unreal-engine/unreal-engine-material-functions-overview) that implement layers, as you can see the results of a tweak to the layer on all the Materials using that function instantly instead of having to wait for the Material to recompile.

To preview parameters in the Level, create a parameterized Material using Scalar or Vector Parameters and apply it to an object in your scene.

1.  First make sure that the Material that you want to preview is applied to something in the level.
    
2.  Inside the Material, make sure that you are using **Scalar** or **Vector Parameters** as inputs for the properties you want to change. Previewing like this will not work with **Constant** Material Expression nodes. Only **parameters** can be previewed in the Level without recompiling the Material. Make sure your parameters have unique, descriptive names.
    
3.  To see the changes happen in real time in the Level viewport, adjust the value of the Scalar or Vector parameters inside the Material. The adjustments that you make are displayed, in real time, in the Level viewport.
    

## Conclusion

As you can see, there are a number of different ways to preview and apply your Unreal Materials to ensure you are getting the desired results. Make sure you preview your Materials often, and consider adjusting the Preview Scene settings to see your Material in different lighting conditions. Remember that when you are finished editing a Material, you must click **Apply** and **Save** in the Toolbar to recompile, otherwise you run the risk of losing your work.

![Save and Apply Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6052a576-f13c-40bc-a4df-676243367fa9/save-and-apply.png)
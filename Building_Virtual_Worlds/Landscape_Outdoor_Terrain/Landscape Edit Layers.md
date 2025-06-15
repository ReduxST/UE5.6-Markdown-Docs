# Landscape Edit Layers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-edit-layers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-edit-layers-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:07

---

**Landscape Edit Layers** enables you to edit Landscape Heightmaps and paint landscapes using non-destructive layers, and you can add multiple layers to your landscape that can be edited independently from each other. You can also reserve a layer for splines, which enables you to add and paint splines non-destructively. Adding, moving, and editing these splines automatically updates the non-destructive layer.

To use Landscape Edit Layers, check **Edit Layers** under the **Manage** tab when creating a new Landscape. Layers cannot be added retroactively to an existing Landscape; you will always need to create a new Landscape to use them in your project.

Click image for full size.

Toggling the layer system off after using the system results in the Editor destructively removing all layer data.

## Adding Layers to Your Landscape

Instead of having one layer to sculpt a heightmap or paint materials, you can now add multiple layers to your landscape. These new layers function as a foundation for sculpting and painting a landscape, which allows you to manipulate and maintain landscapes more efficiently.

By default, you will always have one layer (Layer1), which is the initial base layer. To add a new layer, **right-click** the existing layer and select **Create**. You can also **Rename** a layer from this menu.

We recommend renaming your layers so you know which is the base layer, and which layers are ones you added. You can add as many layers to the landscape as you want.

Click image for full size.

## Managing Layers

There are several options for managing your layers, which include: locking/unlocking layers, hiding/unhiding layers, and highlighting your layer with Layer Contribution.

### Locking and Unlocking Layers

You can lock layers by selecting the **Lock** icon. The closed lock indicates the layer cannot be edited, and the open lock indicates the layer can be edited.

Click image for full size.

### Hiding and Unhiding Layers

If you want to exclude a layer from blending, you can select the eye icon to **Hide** the layer.

Click image for full size.

### Highlighting Layers

To highlight your layer, you can turn on **Layer Contribution**. By highlighting your layer, you can see the entirety of your sculpted layer. The highlight will remain on your layer until you turn it off. To turn on Layer Contribution, navigate to **Lit > Vizualizers > Layer Contribution**. To see the layer's contribution to a heightmap, select the layer in **Sculpt** mode. To see the layer's contribution to a paint layer, select the layer in **Paint** mode.

Use a combination of these tools to effectively sculpt and paint your heightmap. For example, if you decide to paint Layer1 and do not lock your Base Layer, you can paint both layers. By hiding Layer1 you can see where you painted onto the Base Layer. However, if you lock the Base Layer before painting Layer1, the Base Layer will not have any changes.

## Editing Layers

There are several ways you can edit your layer, which include: ordering layers, adjusting the alpha layer blending, and using the Erase tool.

### Ordering Layers

You can drag and drop layers in any order. When you move layers, the order in which those layers display in the viewport changes.

Click image for full size.

### Adjusting Alpha Layer Blending

You can change the blending for each layer by adding or subtracting from the **Alpha** value. The viewport displays changes to the values in real time.

Click image for full size.

Each layer has two Alpha values, one to control heightmap blending and the other to control paint layers blending. Setting a negative heightmap Alpha value will result in a subtractive blend. Paint layers each have an additional flag to determine if blending is additive or subtractive.

![Subtractive blend checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b02f21fe-5075-4119-94fc-51980a12be30/08-paintsub.png "Subtractive blend checkbox")

### Erasing Height in Layers

If you use the Erase Tool on the layer, the sculpting reverts to the default layer height. Layer Contribution can be helpful when using the Erase Tool because the layer is easy to identify.

Click image for full size.

## Using Non-Destructive Splines

Splines can now be created and managed in their own layer, separate from the base layer of the heightmap. This means that you can now edit, change, and move splines non-destructively and the landscape will terraform automatically.

To add a spline, first add a new layer. Right-click to Rename the layer, and then select **Reserve for Splines**. Select **Continue** at the prompt.

Click image for full size.

Click image for full size.

You can edit splines using the Details panel, and adjust the spline using the Transform Controls. Changing the layer order also affects splines, which means parts of the spline can be hidden by the landscape depending on the layer order.

## Additional Information

There are additional features to Landscape Edit Layers that enable you to build on your landscape easily and non-destructively. See the following features for additional information:

-   [Landscape Blueprint Brushes](/documentation/en-us/unreal-engine/landscape-blueprint-brushes-in-unreal-engine)
# Using Dual Normals with Clear Coat

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-dual-normals-with-clear-coat-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-dual-normals-with-clear-coat-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:04

---

When using the **Clear Coat** Shading Model, you can enable an option to use a second normal map for the surface beneath the clear coat layer. This option provides a more accurate model for complex Materials like carbon fiber, in which the underlying layer has different geometric surface properties than the clear coat layer. This tutorial covers how you can enable dual normals in the **Clear Coat Shading Model** and how to use this feature in your projects.

## What the Second Normal Does

The comparison below shows what happens when a second normal map is added to a carbon fiber Material using the Clear Coat Shading Model.

![Clear Coat Bottom Normal Off](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd1016cc-7e4e-4e09-bdd4-c4cc6b43750a/dual_cc_off.png)

![Clear Coat Bottom Normal On](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/550cc25c-7d9d-445e-a6d2-599f2679ad39/dual_cc_on.png)

In the image on the left, **Clear Coat Bottom Normal** is turned off. While the surface under the Clear Coat is interacting with the lighting, the light is only affecting the surface in one direction. This makes the surface appear flat and smooth, which is inaccurate for carbon fiber which should have an alternating woven pattern.

In the image on the right, **Clear Coat Bottom Normal** is enabled. You will notice that the light is now interacting with the carbon fiber weave, producing an alternating pattern of highlights and shadows with a sense of directionality.

## Required Files

To follow this tutorial, you will need to download, extract, and then import the following texture files into your Unreal Engine project. If you are unfamilar with how to do this, read the [Texture Import Guide](/documentation/en-us/unreal-engine/textures-in-unreal-engine#importingtextures) for more information.

**[Required Textures Download](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/f3a7d1d8-91df-41d5-95ed-7b5210d193e7/clearcoatdualnormaltextures.zip)** (Right-click and save link as.)

## Enabling the Clear Coat Second Normal Option

To use two sets of normals in the Clear Coat Shading Model, you will need to enable the feature in the Project Settings.

1.  From the **Main Toolbar** go to **Edit** > **Project Settings**.
    
    ![Open Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d630fed-cc00-470f-94e0-bc5014b255bc/open-project-settings.png)
2.  In the Project Settings window, go to **Rendering** > **Materials** and then check the box next to **Clear Coat Enable Second Normal** option to enable the feature.
    
    ![Enable Clear Coat Second Normals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a8af977-136c-40f7-b632-3aed1c940eab/enable-clear-coat-second-normals.png)
3.  You must restart the Editor to finish enabling the feature. Click **Restart Now** in the dialog when prompted.
    
    ![Restart the Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79cd5445-d3c5-4269-9e48-74288859cac8/restart-editor.png)

## Using the Clear Coat Second Normal Option

Use the following steps to create a Clear Coat Material that uses a second normal map for the underlying layer.

1.  Right-click in the **Content Browser** and select **Material** in the **Create Basic Asset** section of the context menu.
    
    ![Create new Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54082432-9d7c-4a5b-aa63-eef3bf333486/create-material.png)
2.  Give the Material asset a descriptive name like like **ClearCoat\_DualNormals.** Double-click the Material to open it in the Material Editor.
    
    ![Rename Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84c8f8db-1ea7-4e45-9a4f-496bf66b47ff/material-asset.png)
3.  In the Material Editor, click anywhere in the Material Graph to display the Material Properties in the Details Panel. Change the **Shading Model** of the Material from Default Lit to **Clear Coat**.
    
    ![Clear Coat Shading Model](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33ff454c-fa9b-4d10-ab88-03ec09dc9301/shading-model-clear-coat.png)
4.  Add four **Scalar Parameter Expression** nodes to the Material Graph. Give them the follwing names and Default Values, then connect them to the Main Material Node so they match the image below.
    
    | Material Expression Type | Name | Default Value |
    | --- | --- | --- |
    | Scalar Parameter | Base Color | 0.04 |
    | Scalar Parameter | Metallic | 1.0 |
    | Scalar Parameter | Clear Coat | 1.0 |
    | Scalar Parameter | Clear Coat Roughness | 0.1225 |
    
    ![Add Scalar Parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f9a76cd-3219-443d-9541-5d4b82ec2672/add-scalar-parameters.png)
5.  To setup the **Roughness** section of the Material, add the following Material Expressions to the graph. Change the name and default value of each Scalar Parameter so they match the table below. After renaming the parameters, connect all the Material Expressions so your graph matches the image beneath the table.
    
    | Material Expression Type | Name | Default Value |
    | --- | --- | --- |
    | Scalar Parameter | Roughness Scaling | 30.0 |
    | Scalar Parameter | Roughness Min | 0.1 |
    | Scalar Parameter | Roughness Max | 1.349 |
    | Texture Sample | N/A | T\_CarbonFiber\_R\_00 |
    | Texture Coordinate | N/A | N/A |
    | Multiply | N/A | N/A |
    | Linear Interpolate | N/A | N/A |
    
    ![Roughness Material Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9289eeb-e918-4164-95be-c508ed8a610c/roughness-section.png)
6.  Since this Material uses two normal maps, you will need to create two different **Normal map** sections in the Material Graph. The first section will define the normals of the Clear Coat surface and will require the following Material Expression nodes. Rename the Scalar Parameters and set their Default Values according to the table. Connect the Material Expressions so they match the image below.
    
    | Material Expression Type | Name | Default Value |
    | --- | --- | --- |
    | Scalar Parameter | Clear Coat Normal Strength | 0.98 |
    | Scalar Parameter | Clear Coat Normal Scaling | 30.0 |
    | Texture Sample | N/A | T\_CarPaint\_N\_00 |
    | Texture Coordinate | N/A | N/A |
    | Multiply | N/A | N/A |
    | FlattenNormal | N/A | N/A |
    
    ![Clear Coat Normals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/139ec14a-9052-4de8-8632-17d792a69707/clear-coat-normals.png)
7.  The second normal map will define the carbon fiber surface that is beneath the clear coat. Add the Material Expressions listed below, and give them the following names and default values. Connect the Material Expression nodes so that they match the image below.
    
    | Material Expression Type | Name | Default Value |
    | --- | --- | --- |
    | Scalar Parameter | Carbon Fiber Scaling | 30.0 |
    | Scalar Parameter | Carbon Fiber Strength | 0.5 |
    | Texture Sample | N/A | T\_CarbonFiber\_N\_00 |
    | Texture Coordinate | N/A | N/A |
    | Multiply | N/A | N/A |
    | FlattenNormal | N/A | N/A |
    | ClearCoatBottomNormal (ClearCoatNormalCustomOutput) | N/A | N/A |
    
    Click image for full size.
    
    Make sure you have added the **ClearCoatBottomNormal** Material Expression node to the Material Graph and that you have connected the Normal map you want to use to its input. Failing to do this will result in you not being able to see the second Normal map in your Material.
    
8.  With all the individual sections of the Material Graph now complete, connect the output of the **Lerp** in the Roughness section to the **Roughness** input on the Main Material Node. Connect the output of the **FlattenNormal** node to the **Normal** input on the Main Material Node. You do not need any additional connections for the carbon fiber normal map, because it is already connected to the **ClearCoatBottomNormal** custom output node. The final Material Graph is pictured below.
    
    Click image for full size.
    
9.  Click **Apply** and **Save** in the Material Editor toolbar to compile the Material and save the asset. The finished carbon fiber Material should look like the preview shown below.
    
    ![Final Carbon Fiber Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc4fbac3-4c5b-4da6-84eb-bbfa2afa145e/save-and-apply-carbon-fiber.png)
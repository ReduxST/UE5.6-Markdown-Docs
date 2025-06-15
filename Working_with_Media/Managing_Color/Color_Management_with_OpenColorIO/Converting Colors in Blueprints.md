# Converting Colors in Blueprints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/converting-colors-in-unreal-engine-blueprints](https://dev.epicgames.com/documentation/en-us/unreal-engine/converting-colors-in-unreal-engine-blueprints)  
**Processed:** 2025-06-14 16:16:08

---

You can apply [OpenColorIO](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) (**OCIO**) color transformations with **Blueprints** on any input texture, including a **MediaTexture** that plays back a video source, and get the converted results in a **RenderTarget**. This page shows how to use the **Apply Color Space Transform** Blueprint function in your project.

## Prerequisites

You must set up the following in your project to complete the sections below:

-   An **OpenColorIO Configuration Asset**. Refer to the [OpenColorIO Quick Start](/documentation/en-us/unreal-engine/opencolorio-quick-start-for-unreal-engine) for steps on creating this Asset.
    
-   A **Blueprint Class**, created from a **Blueprint Actor** that has an **Event Tick**.
    

## Using the Apply Color Space Transform Function

Follow these steps to apply color conversions with Blueprints. These steps use the **EditorUtilityActor** Blueprint Class as an example.

1.  Double-click your **Blueprint Class** to open it in the **Blueprint Editor**.
    
2.  In the **My Blueprint** panel, under **Variables > Components**, click **Add (+) Variable** to create a new variable. Name the new variable **InputTexture**.
    
    ![Add new variable in Blueprint Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e4a72ea-c694-40b9-99b6-d51c8b88d999/add-new-variable.png)
3.  Next to the new InputTexture variable, click **Make Public** to make it visible outside this Blueprint.
    
    ![InputTexture variable set to public](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2d71326-81b1-4279-8f8a-37d6b76b79ae/make-variable-public.png)
4.  Set the **Variable Type** for the variable InputTexture to **Object Types > Texture > Object Reference**.
    
    ![Setting InputTexture variable type to Texture Object Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fd3bf3e-9c50-4065-baae-6ae2d0df119c/set-inputtexture-variable-type-texture.png)
5.  Create two more variables and make them public:
    
    -   **OutputTexture** with the Variable Type **Texture Render Target 2D > Object Reference**
        
    -   **ColorConversionSettings** with the Variable Type **Open Color IOColor Conversion Settings**.
        
    
    ![Blueprint with all variables created](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/465ef34c-51e5-436b-b729-0e3833ffbe82/ocio-variables-created.png)
6.  Drag the **InputTexture** variable into the **Event Graph**, and choose **Get InputTexture**. This creates a new InputTexture node in the Event Graph.
    
    ![InputTexture variable dragged into Event Graph to create Get InputTexture node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/055b503d-49cf-42b1-9906-17beb2cf02fe/get-inputtexture-node.png)
7.  Repeat the process for the **OutputTexture** and **ColorConversionSettings** variables.
    
    ![Blueprint nodes created from all the variables](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4cd1b555-dc39-465d-bb86-ea7063475a1b/blueprint-ocio-nodes-created.png)
8.  Right-click within the **Event Graph**, and add a new **Apply Color Space Transform** node.
    
    ![Apply Color Space Transform node created](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfc0b022-721c-4fa8-bdb0-ed2f54968d86/apply-color-space-transform-node.png)
9.  Connect the nodes together:
    
    -   Connect the **output execution pin** from the pre-supplied **Event Tick** node to the **input execution pin** of the **Apply Color Space Transform** node.
        
    -   Connect the **output data pin** of the **InputTexture** node to the **Input Texture input data pin** on the **Apply Color Space Transform** node.
        
    -   Connect the **output data pin** of the **Output Texture** node to the **Output Render Target** **input data pin** on the **Apply Color Space Transform** node.
        
    -   Connect the **output data pin** of the **Color Conversion Settings** node to the **Conversion Settings input data pin** of the **Apply Color Space Transform** node.
        
    
    ![Blueprint nodes connected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ee34215-f14e-4a30-8be1-b3f1c154d36b/blueprint-nodes-connected.png)
10.  **Compile** and **Save** the Blueprint. Close the Blueprint Editor.
    
11.  Drag your **Blueprint Asset** into the level to create its **Actor**.
    
12.  In the **Outliner**, select your **Blueprint Actor** to open its **Details** panel.
    
13.  In the **Details** panel, expand the **Default** section, and set **Input Texture** to your desired input file.
    
14.  Create a **Render Target Asset** in the **Content Browser**, and set **Output Texture** to point to the new Render Target Asset.
    
    ![Details panel of the Blueprint Class Actor with all the variables assigned](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6050482-0046-4fa7-9484-cb8659a29f61/blueprint-class-variables-assigned.png)
15.  In the **Details** panel of the **Blueprint Actor,** expand the **Color Conversion Settings** section. Set **Configuration Source** to your OpenColorIO Configuration Asset, and adjust the **Source Color Space** and **Destination Color Space** to match the color space of the input and output media.
    
16.  Drag your **Render Target Asset** onto an **Actor** in the Level to preview your media with the color transformation. You can continue to adjust the Source Color Space and Destination Color Space settings to preview different outputs.
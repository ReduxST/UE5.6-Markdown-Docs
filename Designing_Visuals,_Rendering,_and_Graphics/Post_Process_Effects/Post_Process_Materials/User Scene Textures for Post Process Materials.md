# User Scene Textures for Post Process Materials

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/post-process-material-user-scene-textures-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/post-process-material-user-scene-textures-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:04

---

**User Scene Textures** are user-defined transient render targets that can be written and read in post process materials, making it possible to support multi-pass post process effects.

This guide demonstrates how you can use User Scene Textures to create a variable blur effect on screen whereby there is no blur in the middle of the screen and varying amounts of blur towards the outer edge of the screen. The blur effect is achieved by interpolating between the original scene color and two downsampled and blurred User Scene Textures, each generated with a two-pass separable gaussian filter. This method can provide better efficiency than a single-pass blur.

![With the Variable Blur Post Process Material Effect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5712e835-6330-4157-b9e1-ec4ea8a41e6d/ust-comparison-1.png)

![Without any Post Process Materials Applied](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e65cb70-9397-4a88-9144-bb4e5a28a6c5/ust-comparison-2.png)

In this guide, you’ll set up the following:

-   A material to downsample and blur user scene textures.
-   Materials to blur along the horizontal and vertical parts of the screen.
-   Multiple material instances to create the read and write elements of User Scene Textures.
-   Explore some debugging options for this type of effect with console commands and material logic.

## Preliminary Material Creation

To begin with, you’ll start by creating three separate materials. Each of these materials will be used to build out the different elements needed to create a variable blur post process effect. This starts with one material to downsample, and two materials to each blur the horizontal and vertical components of the effect. These materials will be used later in this guide to create material instances to read and write to User Scene Textures that will create this multi-pass effect.

Follow these steps to get started creating this effect:

1.  In the **Content Browser**, click the **Add (+)** button and create three **Materials**.
2.  **Name** each material as follows:
    1.  Downsample
    2.  BlurHoriz
    3.  BlurVert

You should have three materials that look like this:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fde0fd40-929b-4cc2-9121-07087bfb1ddb/ust-material-creation.png)

### Setting Up the Downsample Material

Follow these steps to create the Downsample material:

1.  Open the **Downsample** material.
2.  In the **Details** panel, set the following:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdb04e51-0468-45f3-bd8b-1fad602f3710/ust-downsample-1.png)
    1.  **Material Domain:** Post Process
    2.  **Blendable Location:** Scene Color Before Bloom
    3.  **User Scene Texture:** Output
        1.  This is used to write to a user scene texture called “Output”.
    4.  **User Texture Divisor:** 2, 2 ( for both values)
        1.  This tells the material to downsample by a factor of two in both the X and Y dimensions.
    5.  **Resolution Relative To Input:** Input
        1.  This is used in steps of setting up these materials. However, if not set, the User Texture Divisor scales relative to the absolute screen resolution.
3.  In the Material Graph, right-click and add a **User Scene Texture** node.
4.  With the User Scene Texture node selected, use the **Details** panel to set the following parameters:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eec2eaee-84e4-4b10-b6de-3cd3ec423472/ust-downsample-2.png)
    1.  **User Scene Texture:** Input
    2.  **Filtered:** Checked
        1.  This should be checked because it is performing a bilinear downsample, and this can help avoid artifacts.
5.  Connect the **Color** output of the **User Scene Texture** node to the **Emissive Color** input on the main material node.
6.  Click **Save**.

At this point, the Preview window displays an error message once the User Scene Texture node is created. It indicates that there’s a missing input. This is a debug display that is useful for creating post process materials that have User Scene Textures because it shows the different passes that are running and what their inputs and outputs are.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12a2dbd0-da39-4640-a45f-32b0185eb64b/ust-downsample-3.png)

### Setting Up the BlurHoriz Material

Follow these steps to create a material to blur the horizontal component:

1.  Open the **BlurHoriz** material.
2.  In the **Details** panel, set the following:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ea7820b-16ec-49ed-9c52-0b9a13f25166/ust-blurhoriz-1.png)
    1.  **Material Domain:** Post Process
    2.  **Blendable Location:** Scene Color Before Bloom
    3.  **User Scene Texture:** Output
        1.  This is used to write to a user scene texture called “Output”.
    4.  **Resolution Relative To Input:** Input
        1.  This is used in steps of setting up these materials. However, if not set, the User Texture Divisor scales relative to the absolute screen resolution.
    5.  **Disable Pre Exposure Scale:** Checked
        1.  This material doesn’t set the User Texture Divisor because the blur is being done at the same resolution. Effectively, 0 is the same as 1 in this case when left unset.
3.  In the Material Graph, right-click and add a **User Scene Texture** node.
4.  With the User Scene Texture node selected, use the **Details** panel to set the following parameters:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d5f2b0b-d1b1-43a7-ad56-19c04d372004/ust-blurhoriz-2.png)
    1.  **User Scene Texture:** Input
    2.  **Filtered:** Checked
    3.  **Clamped:** Checked
5.  Pull off the **Color** pin of the User Scene Texture node and add a **Custom** node. This will be used to write some custom HLSL code for this material.
6.  With the Custom node selected, use the **Details** panel to set the following:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01539bc4-43f6-4d8f-9663-3b07aa850464/ust-blurhoriz-3.png)
    1.  **Input Name:** Tex
        1.  This input is used to fetch the ID to pass to the SceneTextureFetch function in the Custom HLSL node, and works with SceneTexture or UserSceneTexture nodes attached to the input pin.
    2.  In the Code field, copy in the following HLSL code:
        
        ```
             `// Gaussian blur with linear sampling      float offset[3] = { 0.0, 1.3846153846, 3.2307692308 };      float weight[3] = { 0.2270270270, 0.3162162162, 0.0702702703 };                   float3 Color = SceneTextureFetch(Tex.ID, float2(0,0)) * weight[0];                   for (int i=1; i<3; i++)      {          Color += SceneTextureFetch(Tex.ID, + float2(offset[i], 0.0)) * weight[i];      Color += SceneTextureFetch(Tex.ID, - float2(offset[i], 0.0)) * weight[i];      }      return Color;`
        Copy full snippet
        ```
        // Gaussian blur with linear sampling float offset\[3\] = { 0.0, 1.3846153846, 3.2307692308 }; float weight\[3\] = { 0.2270270270, 0.3162162162, 0.0702702703 }; float3 Color = SceneTextureFetch(Tex.ID, float2(0,0)) \* weight\[0\]; for (int i=1; i<3; i++) { Color += SceneTextureFetch(Tex.ID, + float2(offset\[i\], 0.0)) \* weight\[i\]; Color += SceneTextureFetch(Tex.ID, - float2(offset\[i\], 0.0)) \* weight\[i\]; } return Color;
7.  Connect the **Custom** output to the main material’s **Emissive Color** input.
8.  Click **Save**.

This post process effect example uses custom HLSL, so it’s important to note that **Disable Pre Exposure Scale** needs to be set because this setting disables some logic that affects scaling of some inputs and outputs of post process materials. You otherwise have to take this into consideration when writing custom HLSL (regular node logic generates code to scale and unscale automatically where needed). Besides avoiding complexity in custom HLSL, there is also a minor performance benefit. It’s generally recommended to disable pre-exposure scale when working with User Scene Textures and custom HLSL.

You can preview the results of the HLSL at this point in the Preview window of the material by changing the “User Scene Texture” field in the User Scene Texture node from “Input” to “SceneColor”. This is a special input that uses the default scene color for this state where it is in the pipeline.

In the **User Scene Texture** node Details panel, set **UserSceneTexture** to `SceneColor`, and **Save** the material.

Once it compiles, your Preview window shows the result of this custom HLSL code. The edges of the sphere should be blurred around the outer edges and the center part of the window is less blurry, like this example (change it back to Input when done):

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af2f57a2-ae86-426d-a38c-41b5e165c25e/ust-blurhoriz-4.png)

*With and without these changes to test the material in the Preview window.*

### Setting Up the BlurVert Material

Follow these steps to create a material to blur the vertical component:

1.  Open the **BlurVert** material.
2.  In the **Details** panel, set the following:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46720886-fc62-4c6b-b82d-5275af5f8fbc/ust-blurvert-1.png)
    1.  **Material Domain:** Post Process
    2.  **Blendable Location:** Scene Color Before Bloom
    3.  **User Scene Texture:** Output
        1.  This is used to write to a user scene texture called “Output”.
    4.  **Resolution Relative To Input:** Input
        1.  This is used in steps of setting up these materials. However, if not set, the User Texture Divisor scales relative to the absolute screen resolution.
    5.  **Disable Pre Exposure Scale:** Checked
        1.  This material doesn’t set the User Texture Divisor because the blur is being done at the same resolution. Effectively, 0 is the same as 1 in this case when left unset.
3.  In the Material Graph, right-click and add a **User Scene Texture** node.
4.  With the User Scene Texture node selected, use the **Details** panel to set the following parameters:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e82c1fb-03dd-4a7a-9770-ca7f4337bfbf/ust-blurvert-2.png)
    1.  **User Scene Texture:** Input
    2.  **Filtered:** Checked
    3.  **Clamped:** Checked
5.  Pull off the **Color** pin of the User Scene Texture node and add a **Custom** node. This will be used to write some custom HLSL code for this material.
6.  With the Custom node selected, use the **Details** panel to set the following:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65e0cbde-0ac9-4ab4-8d9a-6b8a121509c8/ust-blurvert-3.png)
    1.  **Input Name:** Tex
        1.  This input is used to fetch the ID to pass to the SceneTextureFetch function in the Custom HLSL node, and works with SceneTexture or UserSceneTexture nodes attached to the input pin.
    2.  In the Code field, copy in the following HLSL code:
        
        ```
             `// Gaussian blur with linear sampling      float offset[3] = { 0.0, 1.3846153846, 3.2307692308 };      float weight[3] = { 0.2270270270, 0.3162162162, 0.0702702703 };                   float3 Color = SceneTextureFetch(Tex.ID, float2(0,0)) * weight[0];                   for (int i=1; i<3; i++)      {          Color += SceneTextureFetch(Tex.ID, + float2(0.0, offset[i])) * weight[i];      Color += SceneTextureFetch(Tex.ID, - float2(0.0, offset[i])) * weight[i];      }      return Color;`
        Copy full snippet
        ```
        // Gaussian blur with linear sampling float offset\[3\] = { 0.0, 1.3846153846, 3.2307692308 }; float weight\[3\] = { 0.2270270270, 0.3162162162, 0.0702702703 }; float3 Color = SceneTextureFetch(Tex.ID, float2(0,0)) \* weight\[0\]; for (int i=1; i<3; i++) { Color += SceneTextureFetch(Tex.ID, + float2(0.0, offset\[i\])) \* weight\[i\]; Color += SceneTextureFetch(Tex.ID, - float2(0.0, offset\[i\])) \* weight\[i\]; } return Color;
7.  Connect the **Custom** output to the main material’s **Emissive Color** input.
8.  Click **Save**.

This material is set up just like the **BlurHoriz** material in the previous section. The only difference between these two materials is the HLSL code to change the order in which the coordinates are set up for the positive and negative `SceneTextureFetch` offsets. These HLSL line edits switch the UV offsets from horizontal to vertical when sampling the input texture:

```
`Color += SceneTextureFetch(Tex.ID, + float2(0.0, offset[i])) * weight[i]; Color += SceneTextureFetch(Tex.ID, - float2(0.0, offset[i])) * weight[i];`
Copy full snippet
```
Color += SceneTextureFetch(Tex.ID, + float2(0.0, offset\[i\])) \* weight\[i\]; Color += SceneTextureFetch(Tex.ID, - float2(0.0, offset\[i\])) \* weight\[i\];

## Setting Up the User Scene Texture Material Instances

With the foundational materials setup, you’ll use these to create several material instances from them to read and write to User Scene Textures to create the horizontal and vertical parts of the screen that are blurred, and how much these passes contribute to the blurring applied through a post process volume for the final effect.

### Creating the Horizontal Blur Material Instances

In this step, you’ll use the **BlurHoriz** material to create a set of material instances to set up some basic information to read and write to User Scene Textures for the horizontal blurring components of this variable blur effect.

#### HalfA Blur Horizontal Material Instance

This first material instance is created from the **Downsample** material. This material instance will take an input called Scene Color and writes an output called HalfA.

1.  In the Content Browser, right-click on the **Downsample** material and click **Create Material Instance**. Name it “HalfA”.
2.  Open the material instance **HalfA**.
3.  In the Material Instance Editor in the **Details** panel, set the following under the **Post Process Overrides** category:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04c3d7e1-382b-47e3-9909-11ae2493d431/ust-horiz-mi-ha-1.png)
    1.  **Input:** SceneColor
    2.  **User Scene Texture Output:** HalfA
4.  **Save** the material instance.

#### HalfB Blur Horizontal Material Instance

This second material instance is created from the **BlurHoriz** material. This material instance will use HalfA as its input to write an output called HalfB.

1.  In the Content Browser, right-click on the **BlurHoriz** material and click **Create Material Instance**. Name it “HalfB”.
2.  Open the material instance **HalfB**.
3.  In the Material Instance Editor in the **Details** panel, set the following under the **Post Process Overrides** category:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/766d4610-baf7-473e-a37c-3475e3e3778c/ust-horiz-mi-hb-1.png)
    1.  **Input:** HalfA
    2.  **User Scene Texture Output:** HalfB
4.  **Save** the material instance.

At this point, you now have two material instances (HalfA and HalfB) set up, it’s useful to turn on the user scene texture debug display in the Preview window with the console command `r.PostProcessing.UserSceneTextureDebug 1`. This display shows how the User Scene Textures are being read from and written to for this variable blur post process material you are setting up.

When this display is enabled, the Preview window outlines the different passes that are running for this material. In the HalfB material instance, this shows that the HalfA material instance generates an output called HalfA and HalfB reads and generates output for HalfA.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bdfa4137-187f-4c3e-bdc1-682697e42155/ust-horiz-mi-hb-2.png)

### Creating the Vertical Blur Material Instances

In this set of steps, you’ll use the **BlurVert** material to create a set of material instances to set up some basic information to read and write to User Scene Textures for the vertical blurring components of this variable blur effect.

#### HalfC Blur Vertical Material Instance

This first vertical material instance is created from the **BlurVert** material. It takes an input called HalfB and writes an output called HalfC.

1.  In the Content Browser, right-click on the **BlurVert** material and click **Create Material Instance**. Name it “HalfC”.
2.  Open the material instance **HalfC**.
3.  In the Material Instance Editor in the **Details** panel, set the following under the **Post Process Overrides** category:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/143bf8bc-0dcd-473c-b3e6-9a9622db34c4/ust-horiz-mi-hc-1.png)
    1.  **Input:** HalfB
    2.  **User Scene Texture Output:** HalfC
4.  **Save** the material instance.

This completes the set of half-res materials for HalfA, HalfB, and HalfC.

#### QuarterA Blur Vertical Material Instance

This second vertical material instance is created from the **Downsample** material. It writes outputs for a quarter resolution chain that takes input from HalfC and outputs to QuarterA.

1.  In the Content Browser, right-click on the **Downsample** material and click **Create Material Instance**. Name it “QuarterA”.
2.  Open the material instance **QuarterA**.
3.  In the Material Instance Editor in the **Details** panel, set the following under the **Post Process Overrides** category:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30abb91e-6603-43bb-b174-c7e7bbe35c02/ust-vert-mi-qa-1.png)
    1.  **Input:** HalfC
    2.  **User Scene Texture Output:** QuarterA
4.  **Save** the material instance.

#### QuarterB Blur Vertical Material Instance

This third vertical material instance is created from the **BlurHoriz** material. It takes an input called QuarterA and writes an output called QuarterB.

1.  In the Content Browser, right-click on the **BlurHoriz** material and click **Create Material Instance**. Name it “QuarterB”.
2.  Open the material instance **QuarterB**.
3.  In the Material Instance Editor in the **Details** panel, set the following under the **Post Process Overrides** category:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d83088d1-f4a9-4654-97cd-4a1675a69475/ust-vert-mi-qb-1.png)
    1.  **Input:** QuarterA
    2.  **User Scene Texture Output:** QuarterB
4.  **Save** the material instance.

#### QuarterC Blur Vertical Material Instance

This fourth, and final, material instance is created from the **BlurVert** material. It takes an input called QuarterB and writes an output called QuarterC.

1.  In the Content Browser, right-click on the **BlurVert** material and click **Create Material Instance**. Name it “QuarterC”.
2.  Open the material instance **QuarterC**.
3.  In the Material Instance Editor in the **Details** panel, set the following under the **Post Process Overrides** category:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/131bc6a0-e595-45b2-8472-0d31be04f013/ust-vert-mi-qc-1.png)
    1.  **Input:** QuarterB
    2.  **User Scene Texture Output:** QuarterC
4.  **Save** the material instance.

This completes the set of quarter-res material instances for QuarterA, QuarterB, and QuarterC.

### Material Instance Half-Res and Quarter-Res Results

Once each of these material instances are set up to read and write User Scene Textures, each should show their result in their Preview window. This should look similar to the examples below, where blur is applied in varying amounts based on the user scene textures the material instance is reading and writing to up to that point in the chain.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f726d877-07de-4c19-aead-4005917cfaf8/ust-halfres-quarterres-1.png)

You can see how all of these material instances work with one another when the user scene texture debug display is enabled. For example, in the QuarterC preview window below, you will see a debug display showing how all the inputs and outputs are chained together to create the layers of this variable blur effect.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1c1697d-71a9-462c-9e6a-e917ff51f4d9/ust-halfres-quarterres-2.png)

## Setting Up a Variable Blur Material

Now that you have all the material instances set up that have the half-res and quarter-res downsampled and blurred user scene textures, you need to create a material that ties all of these elements together to create the variable blur effect to use with a post process volume.

### Creating a Triple Bilinear Lerp Material Function

Before you create the material that ties all these components together, you’ll first need to create a custom material function that interpolates between the half-res and quarter-res user scene textures, alpha to control parts of the screen affected, and the scene texture input for the post process material.

1.  In the **Content Browser**, click the **Add (+)** button and create a **Material Function**.
2.  **Name** the material function “TripleBilinearLerp”.
3.  Open the **Material Function**.
4.  Recreate the material graph below.
    
    Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_1" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_1'" Begin Object Class=/Script/Engine.MaterialExpressionLinearInterpolate Name="MaterialExpressionLinearInterpolate\_0" ExportPath="/Script/Engine.MaterialExpressionLinearInterpolate'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_1.MaterialExpressionLinearInterpolate\_0'" End Object Begin Object Name="MaterialExpressionLinearInterpolate\_0" ExportPath="/Script/Engine.MaterialExpressionLinearInterpolate'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_1.MaterialExpressionLinearInterpolate\_0'" A=(Expression="/Script/Engine.MaterialExpressionFunctionInput'MaterialGraphNode\_2.MaterialExpressionFunctionInput\_0'") B=(Expression="/Script/Engine.MaterialExpressionFunctionInput'MaterialGraphNode\_3.MaterialExpressionFunctionInput\_1'") Alpha=(Expression="/Script/Engine.MaterialExpressionSaturate'MaterialGraphNode\_8.MaterialExpressionSaturate\_0'") MaterialExpressionEditorX=96 MaterialExpressionEditorY=208 MaterialExpressionGuid=A8ED16194716D3B0CDA15C8D7C97D4D4 Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionLinearInterpolate'MaterialExpressionLinearInterpolate\_0'" NodePosX=96 NodePosY=208 NodeGuid=94A2C1E74424AB6F129C92A158EB6D29 CustomProperties Pin (PinId=985B04384243B156488DAE92605517A7,PinName="A",PinType.PinCategory="optional",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="0.0",LinkedTo=(MaterialGraphNode\_2 B3ABD15A414088DF1DA1B0B3A0844C02,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=61EAAD244DF5C6E7D51F51895AC08C8E,PinName="B",PinType.PinCategory="optional",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="1.0",LinkedTo=(MaterialGraphNode\_3 B11BDA6643D7D29138E2B996602F6620,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=5E45AE2047B136732D420A878357167A,PinName="Alpha",PinType.PinCategory="optional",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="0.5",LinkedTo=(MaterialGraphNode\_8 4E34FD8047F1D50EDF8060AF8586922C,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=9F1246224CE0D8BA02D772A3023712F2,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_4 29A394C2458439B512865A8386BC3644,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_2" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_2'" Begin Object Class=/Script/Engine.MaterialExpressionFunctionInput Name="MaterialExpressionFunctionInput\_0" ExportPath="/Script/Engine.MaterialExpressionFunctionInput'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_2.MaterialExpressionFunctionInput\_0'" End Object Begin Object Name="MaterialExpressionFunctionInput\_0" ExportPath="/Script/Engine.MaterialExpressionFunctionInput'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_2.MaterialExpressionFunctionInput\_0'" Preview=(Expression="/Script/Engine.MaterialExpressionConstant4Vector'MaterialGraphNode\_11.MaterialExpressionConstant4Vector\_0'",Mask=1,MaskR=1,MaskG=1,MaskB=1,MaskA=1) InputName="A" Id=A30BA5064D1E14D22C4E02A871B09C34 InputType=FunctionInput\_Vector4 MaterialExpressionEditorX=-272 MaterialExpressionEditorY=128 MaterialExpressionGuid=F8E23BAC48D726B95A0BAE8888680A02 Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionFunctionInput'MaterialExpressionFunctionInput\_0'" NodePosX=-272 NodePosY=128 NodeGuid=D772B9CF4765C291A372E7B9ED106984 CustomProperties Pin (PinId=C2013CF4493F250AF21655B833569255,PinName="Preview",PinType.PinCategory="optional",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_11 FEA99DF24557E46A117D28B908B129BF,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=B3ABD15A414088DF1DA1B0B3A0844C02,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_1 985B04384243B156488DAE92605517A7,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_3" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_3'" Begin Object Class=/Script/Engine.MaterialExpressionFunctionInput Name="MaterialExpressionFunctionInput\_1" ExportPath="/Script/Engine.MaterialExpressionFunctionInput'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_3.MaterialExpressionFunctionInput\_1'" End Object Begin Object Name="MaterialExpressionFunctionInput\_1" ExportPath="/Script/Engine.MaterialExpressionFunctionInput'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_3.MaterialExpressionFunctionInput\_1'" Preview=(Expression="/Script/Engine.MaterialExpressionConstant4Vector'MaterialGraphNode\_12.MaterialExpressionConstant4Vector\_1'",Mask=1,MaskR=1,MaskG=1,MaskB=1,MaskA=1) InputName="B" Id=EE5FC89E4FCC14C6E933819A9B93DF50 InputType=FunctionInput\_Vector4 MaterialExpressionEditorX=-272 MaterialExpressionEditorY=320 MaterialExpressionGuid=81E560EC40903A2A9CB00C8DB9495CC7 Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionFunctionInput'MaterialExpressionFunctionInput\_1'" NodePosX=-272 NodePosY=320 NodeGuid=E73233D547D31766537DACA2F1BB9FAB CustomProperties Pin (PinId=476E616140410D3053368CB8D0EA2355,PinName="Preview",PinType.PinCategory="optional",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_12 44E3A31E46CE6C8CCE79B1956158F613,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=B11BDA6643D7D29138E2B996602F6620,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_1 61EAAD244DF5C6E7D51F51895AC08C8E,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_4" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_4'" Begin Object Class=/Script/Engine.MaterialExpressionLinearInterpolate Name="MaterialExpressionLinearInterpolate\_1" ExportPath="/Script/Engine.MaterialExpressionLinearInterpolate'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_4.MaterialExpressionLinearInterpolate\_1'" End Object Begin Object Name="MaterialExpressionLinearInterpolate\_1" ExportPath="/Script/Engine.MaterialExpressionLinearInterpolate'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_4.MaterialExpressionLinearInterpolate\_1'" A=(Expression="/Script/Engine.MaterialExpressionLinearInterpolate'MaterialGraphNode\_1.MaterialExpressionLinearInterpolate\_0'") B=(Expression="/Script/Engine.MaterialExpressionFunctionInput'MaterialGraphNode\_5.MaterialExpressionFunctionInput\_2'") Alpha=(Expression="/Script/Engine.MaterialExpressionSaturate'MaterialGraphNode\_10.MaterialExpressionSaturate\_1'") MaterialExpressionEditorX=208 MaterialExpressionEditorY=352 MaterialExpressionGuid=DA2117CE4D4A9EF16C183FBCAC0EA4B7 Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionLinearInterpolate'MaterialExpressionLinearInterpolate\_1'" NodePosX=208 NodePosY=352 NodeGuid=43D7D2E44239AE53D96505BE1DD84A45 CustomProperties Pin (PinId=29A394C2458439B512865A8386BC3644,PinName="A",PinType.PinCategory="optional",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="0.0",LinkedTo=(MaterialGraphNode\_1 9F1246224CE0D8BA02D772A3023712F2,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=33EFD05349E465E86D66AC8ABB711C2E,PinName="B",PinType.PinCategory="optional",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="1.0",LinkedTo=(MaterialGraphNode\_5 1E9CE5E04B304004FED9B098053CDCA0,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=F3EB71E641D3ACB629195690430FEACC,PinName="Alpha",PinType.PinCategory="optional",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="0.5",LinkedTo=(MaterialGraphNode\_10 AB99B08745C6FF72A1B353804432D33F,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=6D99616E4C79A88FE905C8A11ABEEFB3,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_0 B640EB3E41FB872DF2BC29B49F1C086C,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_5" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_5'" Begin Object Class=/Script/Engine.MaterialExpressionFunctionInput Name="MaterialExpressionFunctionInput\_2" ExportPath="/Script/Engine.MaterialExpressionFunctionInput'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_5.MaterialExpressionFunctionInput\_2'" End Object Begin Object Name="MaterialExpressionFunctionInput\_2" ExportPath="/Script/Engine.MaterialExpressionFunctionInput'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_5.MaterialExpressionFunctionInput\_2'" Preview=(Expression="/Script/Engine.MaterialExpressionConstant4Vector'MaterialGraphNode\_13.MaterialExpressionConstant4Vector\_2'",Mask=1,MaskR=1,MaskG=1,MaskB=1,MaskA=1) InputName="C" Id=BC7361C744FA6B9F29B67C925B79A4EE InputType=FunctionInput\_Vector4 MaterialExpressionEditorX=-272 MaterialExpressionEditorY=496 MaterialExpressionGuid=54CBBA134D385DA6F2E0E5BE3E75ED14 Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionFunctionInput'MaterialExpressionFunctionInput\_2'" NodePosX=-272 NodePosY=496 NodeGuid=0232CDFF483F8B81A908788ABA536C23 CustomProperties Pin (PinId=3EBBB1CD41DE42002F9969A0781E31EF,PinName="Preview",PinType.PinCategory="optional",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_13 BBE7B94E4BCA23CFBA928083F2730D3F,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=1E9CE5E04B304004FED9B098053CDCA0,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_4 33EFD05349E465E86D66AC8ABB711C2E,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_6" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_6'" Begin Object Class=/Script/Engine.MaterialExpressionFunctionInput Name="MaterialExpressionFunctionInput\_3" ExportPath="/Script/Engine.MaterialExpressionFunctionInput'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_6.MaterialExpressionFunctionInput\_3'" End Object Begin Object Name="MaterialExpressionFunctionInput\_3" ExportPath="/Script/Engine.MaterialExpressionFunctionInput'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_6.MaterialExpressionFunctionInput\_3'" Preview=(Expression="/Script/Engine.MaterialExpressionConstant'MaterialGraphNode\_14.MaterialExpressionConstant\_0'") InputName="Alpha" Id=077E90F14D801B92EF0AE5BB1BF365A3 InputType=FunctionInput\_Scalar MaterialExpressionEditorX=-272 MaterialExpressionEditorY=688 MaterialExpressionGuid=4D27CDA24EE0A0DA8EAFD7ABC62DE98A Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionFunctionInput'MaterialExpressionFunctionInput\_3'" NodePosX=-272 NodePosY=688 NodeGuid=5E20351F425DF761FE7B2091A3547CC6 CustomProperties Pin (PinId=F22CBC7E4B9374D1155C4B8124274F0F,PinName="Preview",PinType.PinCategory="optional",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_14 9F19F2524D1F3E07365FB1A3AFA7B18F,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=714CED574BF646A4A29BA3934518A104,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_7 0AF3C5304FACAE045A1C139C3AA4F72A,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_7" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_7'" Begin Object Class=/Script/Engine.MaterialExpressionMultiply Name="MaterialExpressionMultiply\_0" ExportPath="/Script/Engine.MaterialExpressionMultiply'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_7.MaterialExpressionMultiply\_0'" End Object Begin Object Name="MaterialExpressionMultiply\_0" ExportPath="/Script/Engine.MaterialExpressionMultiply'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_7.MaterialExpressionMultiply\_0'" A=(Expression="/Script/Engine.MaterialExpressionFunctionInput'MaterialGraphNode\_6.MaterialExpressionFunctionInput\_3'") ConstB=2.000000 MaterialExpressionEditorX=-16 MaterialExpressionEditorY=672 MaterialExpressionGuid=C63EA0854FFA9DAD435AF9A617769EC1 Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionMultiply'MaterialExpressionMultiply\_0'" NodePosX=-16 NodePosY=672 NodeGuid=C9EAA4D2423EC0DEFB0609948EA3136E CustomProperties Pin (PinId=0AF3C5304FACAE045A1C139C3AA4F72A,PinName="A",PinType.PinCategory="optional",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="0.0",LinkedTo=(MaterialGraphNode\_6 714CED574BF646A4A29BA3934518A104,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=681D235A42DE8088980B3AA913BA3A00,PinName="B",PinType.PinCategory="optional",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="2.0",PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=54572CE941A329E5EB3BD4AF21CE4FF1,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_8 E613D6D64982D5A4C5B98AB1502ED50E,MaterialGraphNode\_9 BDE789E245713C3BE15E1F9CDA1A5D11,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_8" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_8'" Begin Object Class=/Script/Engine.MaterialExpressionSaturate Name="MaterialExpressionSaturate\_0" ExportPath="/Script/Engine.MaterialExpressionSaturate'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_8.MaterialExpressionSaturate\_0'" End Object Begin Object Name="MaterialExpressionSaturate\_0" ExportPath="/Script/Engine.MaterialExpressionSaturate'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_8.MaterialExpressionSaturate\_0'" Input=(Expression="/Script/Engine.MaterialExpressionMultiply'MaterialGraphNode\_7.MaterialExpressionMultiply\_0'") MaterialExpressionEditorX=-16 MaterialExpressionEditorY=384 MaterialExpressionGuid=9586172B4C3CF8D9DE92FCA4FE4E58BC Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionSaturate'MaterialExpressionSaturate\_0'" NodePosX=-16 NodePosY=384 NodeGuid=FADAC2FE4813C61BBF743FBEDAA6C0CB CustomProperties Pin (PinId=E613D6D64982D5A4C5B98AB1502ED50E,PinName="Input",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),PinType.PinCategory="required",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_7 54572CE941A329E5EB3BD4AF21CE4FF1,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=4E34FD8047F1D50EDF8060AF8586922C,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_1 5E45AE2047B136732D420A878357167A,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_9" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_9'" Begin Object Class=/Script/Engine.MaterialExpressionSubtract Name="MaterialExpressionSubtract\_0" ExportPath="/Script/Engine.MaterialExpressionSubtract'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_9.MaterialExpressionSubtract\_0'" End Object Begin Object Name="MaterialExpressionSubtract\_0" ExportPath="/Script/Engine.MaterialExpressionSubtract'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_9.MaterialExpressionSubtract\_0'" A=(Expression="/Script/Engine.MaterialExpressionMultiply'MaterialGraphNode\_7.MaterialExpressionMultiply\_0'") MaterialExpressionEditorX=192 MaterialExpressionEditorY=672 MaterialExpressionGuid=24F7B33C4448C051B6688D919FF0FEC1 Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionSubtract'MaterialExpressionSubtract\_0'" NodePosX=192 NodePosY=672 NodeGuid=0F409348433EEDB78314DA9DE740EBDF CustomProperties Pin (PinId=BDE789E245713C3BE15E1F9CDA1A5D11,PinName="A",PinType.PinCategory="optional",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="1.0",LinkedTo=(MaterialGraphNode\_7 54572CE941A329E5EB3BD4AF21CE4FF1,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=5FC6EF1B4936F28C559AEDB1D6F9F32B,PinName="B",PinType.PinCategory="optional",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="1.0",PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=CD3916D044075FBAF46A51AB8D91B59F,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_10 E53A4D004989C469B01334A62051D7DA,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_10" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_10'" Begin Object Class=/Script/Engine.MaterialExpressionSaturate Name="MaterialExpressionSaturate\_1" ExportPath="/Script/Engine.MaterialExpressionSaturate'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_10.MaterialExpressionSaturate\_1'" End Object Begin Object Name="MaterialExpressionSaturate\_1" ExportPath="/Script/Engine.MaterialExpressionSaturate'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_10.MaterialExpressionSaturate\_1'" Input=(Expression="/Script/Engine.MaterialExpressionSubtract'MaterialGraphNode\_9.MaterialExpressionSubtract\_0'") MaterialExpressionEditorX=160 MaterialExpressionEditorY=544 MaterialExpressionGuid=B524AC184E3FAAF5D8047DBBA5DAE752 Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionSaturate'MaterialExpressionSaturate\_1'" NodePosX=160 NodePosY=544 NodeGuid=367B05C8472F60143DCDDAB83923609E CustomProperties Pin (PinId=E53A4D004989C469B01334A62051D7DA,PinName="Input",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),PinType.PinCategory="required",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_9 CD3916D044075FBAF46A51AB8D91B59F,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=AB99B08745C6FF72A1B353804432D33F,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_4 F3EB71E641D3ACB629195690430FEACC,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_11" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_11'" Begin Object Class=/Script/Engine.MaterialExpressionConstant4Vector Name="MaterialExpressionConstant4Vector\_0" ExportPath="/Script/Engine.MaterialExpressionConstant4Vector'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_11.MaterialExpressionConstant4Vector\_0'" End Object Begin Object Name="MaterialExpressionConstant4Vector\_0" ExportPath="/Script/Engine.MaterialExpressionConstant4Vector'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_11.MaterialExpressionConstant4Vector\_0'" Constant=(R=1.000000,G=0.000000,B=0.000000,A=0.000000) MaterialExpressionEditorX=-480 MaterialExpressionEditorY=128 MaterialExpressionGuid=D81F4D5B414E726D2178A1981EA27379 Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionConstant4Vector'MaterialExpressionConstant4Vector\_0'" NodePosX=-480 NodePosY=128 NodeGuid=0859F26B475C4E0BCB676E80E99DB1AA CustomProperties Pin (PinId=A05A04F6462E420EA9266896AD498F9E,PinName="Constant",PinType.PinCategory="optional",PinType.PinSubCategory="rgba",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="(R=1.000000,G=0.000000,B=0.000000,A=0.000000)",PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=True,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=FEA99DF24557E46A117D28B908B129BF,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="rgba",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_2 C2013CF4493F250AF21655B833569255,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=BF2E16FB4C5650EE38E0E59B00D843BF,PinName="Output2",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=2FE03B274BF8D6B10F9AF893C049F6C3,PinName="Output3",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="green",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=D5D7DFD34FF03718BFBF63B494606FBD,PinName="Output4",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="blue",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=587B663848AF9B58644098BC45084BA6,PinName="Output5",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="alpha",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_12" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_12'" Begin Object Class=/Script/Engine.MaterialExpressionConstant4Vector Name="MaterialExpressionConstant4Vector\_1" ExportPath="/Script/Engine.MaterialExpressionConstant4Vector'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_12.MaterialExpressionConstant4Vector\_1'" End Object Begin Object Name="MaterialExpressionConstant4Vector\_1" ExportPath="/Script/Engine.MaterialExpressionConstant4Vector'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_12.MaterialExpressionConstant4Vector\_1'" Constant=(R=0.000000,G=1.000000,B=0.000000,A=0.000000) MaterialExpressionEditorX=-480 MaterialExpressionEditorY=336 MaterialExpressionGuid=C7157E0A4D4A53576E90B9A7A64F4A43 Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionConstant4Vector'MaterialExpressionConstant4Vector\_1'" NodePosX=-480 NodePosY=336 NodeGuid=A61C84424BE1D388A10F269545DAFE72 CustomProperties Pin (PinId=131EEEA740E6263459B16D9EAF0BA074,PinName="Constant",PinType.PinCategory="optional",PinType.PinSubCategory="rgba",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="(R=0.000000,G=1.000000,B=0.000000,A=0.000000)",PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=True,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=44E3A31E46CE6C8CCE79B1956158F613,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="rgba",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_3 476E616140410D3053368CB8D0EA2355,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=A6D76C8046AF1F736DE9A0A16F6948B4,PinName="Output2",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=AE6EB9FF40BD22D8BFAE2DBD34350C11,PinName="Output3",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="green",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=06F867094DDBB3230FB1E0BB5C98BE71,PinName="Output4",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="blue",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=BAF9E4DA499D1A5D68E7BC8264692A9A,PinName="Output5",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="alpha",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_13" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_13'" Begin Object Class=/Script/Engine.MaterialExpressionConstant4Vector Name="MaterialExpressionConstant4Vector\_2" ExportPath="/Script/Engine.MaterialExpressionConstant4Vector'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_13.MaterialExpressionConstant4Vector\_2'" End Object Begin Object Name="MaterialExpressionConstant4Vector\_2" ExportPath="/Script/Engine.MaterialExpressionConstant4Vector'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_13.MaterialExpressionConstant4Vector\_2'" Constant=(R=0.000000,G=0.000000,B=1.000000,A=0.000000) MaterialExpressionEditorX=-480 MaterialExpressionEditorY=544 MaterialExpressionGuid=52F4C90141136B86C3CEAFA28ABF3B76 Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionConstant4Vector'MaterialExpressionConstant4Vector\_2'" NodePosX=-480 NodePosY=544 NodeGuid=D96C87E54C93786F8A3C77A59290B3BB CustomProperties Pin (PinId=F854AB3343B54FA41D385FB150BCC91C,PinName="Constant",PinType.PinCategory="optional",PinType.PinSubCategory="rgba",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="(R=0.000000,G=0.000000,B=1.000000,A=0.000000)",PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=True,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=BBE7B94E4BCA23CFBA928083F2730D3F,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="rgba",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_5 3EBBB1CD41DE42002F9969A0781E31EF,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=C06357F349FCD1FBCCC84695B57393A4,PinName="Output2",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=FF35CD014403EE8D9F1E96AB7F23F8E5,PinName="Output3",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="green",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=11D60F2546BF8949C83A0A9CAAF5C02D,PinName="Output4",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="blue",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=5147C1F34D09D137037B5CB31497CCFC,PinName="Output5",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="mask",PinType.PinSubCategory="alpha",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object Begin Object Class=/Script/UnrealEd.MaterialGraphNode Name="MaterialGraphNode\_14" ExportPath="/Script/UnrealEd.MaterialGraphNode'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_14'" Begin Object Class=/Script/Engine.MaterialExpressionConstant Name="MaterialExpressionConstant\_0" ExportPath="/Script/Engine.MaterialExpressionConstant'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_14.MaterialExpressionConstant\_0'" End Object Begin Object Name="MaterialExpressionConstant\_0" ExportPath="/Script/Engine.MaterialExpressionConstant'/Engine/Transient.Material\_0:MaterialGraph\_0.MaterialGraphNode\_14.MaterialExpressionConstant\_0'" R=0.250000 MaterialExpressionEditorX=-480 MaterialExpressionEditorY=768 MaterialExpressionGuid=86ED9CB24534A6796328A78FD5473DA0 Material="/Script/Engine.Material'/Engine/Transient.Material\_0'" End Object MaterialExpression="/Script/Engine.MaterialExpressionConstant'MaterialExpressionConstant\_0'" NodePosX=-480 NodePosY=768 NodeGuid=C9716D6341ACD51A1AA8CCA8837358DF CustomProperties Pin (PinId=3D84EFAC4C0A27D392F358BC1808AAC3,PinName="Value",PinType.PinCategory="optional",PinType.PinSubCategory="red",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultValue="0.25",PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=True,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) CustomProperties Pin (PinId=9F19F2524D1F3E07365FB1A3AFA7B18F,PinName="Output",PinFriendlyName=NSLOCTEXT("MaterialGraphNode", "Space", " "),Direction="EGPD\_Output",PinType.PinCategory="",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(MaterialGraphNode\_6 F22CBC7E4B9374D1155C4B8124274F0F,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,) End Object
    
    1.  For each of the **FunctionInput** nodes, you’ll need to set the following for each:
        1.  The first three will use the **Input Name A**, **B**, or **C** and their **Input Type** is **Function Input Vector 4**.
        2.  The last one’s **Input Name** is **Alpha** and the **Input Type** is **Function Input Scalar**.
    2.  Alternatively, you can copy the code from the image above and paste it directly into your graph of your material function.
5.  Connect the **Lerp** to the **Output Result** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d537f8e0-d3f8-45d9-9213-a32b6fa0a169/ust-mf-tripbilinear-2.png)
6.  **Save** and **Close** the Material Function Editor.

### Creating a Material with Variable Blur using User Scene Textures

This is the final material you’ll create that ties all these components together for the variable blur post process effect. The TripleBilinearLerp material function uses the half-res and quarter-res user scene textures to create the variable blur effect on screen, and you’ll use the Alpha input to control areas of the screen affected by the blur effect across the center, middle, and outer edges of the screen.

1.  In the **Content Browser**, click the **Add (+)** button and create a **Material**. Name the material “BlurApply”.
2.  Open the **BlurApply** material.
3.  In the **Details** panel, set the following:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e756619-17c5-4b0e-96e7-ddf8986e2ec2/ust-mat-variableblur-1.png)
    1.  **Domain:** Post Process
    2.  **Blendable Location:** Scene Color Before Bloom
4.  In the graph, drag in the **TripleBilinearLerp** material function you created in an earlier step.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50176cbe-d160-44fb-a423-b3931c8f7b0a/ust-mat-variableblur-2.png)
5.  Add a **Scene Texture** input data expression. In the **Details** panel, set **Scene Texture Id** to **PostProcessInput0**.
    
    The PostProcessInput0 is the same as SceneColor but for post process materials.
    
6.  Connect the **Color** output of the **SceneTexture:PostProcessInput0** node to the **A** input of the **TripleBilinearLerp** material function node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e82315aa-c4bc-432a-b9c3-9ac88d75ea0e/ust-mat-variableblur-3.png)
7.  Add two **User Scene Texture** nodes. For each, set the following in the Details panel:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3efe2c3-7c6e-40cc-b61c-50e60b6c4d1f/ust-mat-variableblur-4.png)
    1.  **User Scene Texture:** This feeds in the half-res and quarter-res user scene textures. Name one **HalfC** and the other **QuarterC**.
    2.  **Filtered:** Checked
    3.  **Clamped:** Checked
8.  Connect the **Color** output of the **UserSceneTexture:HalfC** node to the **B** input of the **TripleBilinearLerp** node.
9.  Connect the **Color** output of the **UserSceneTexture:QuarterC** node to the **C** input of the **TripleBilinearLerp** node.
10.  In the graph, add a **Constant** node. Leave its value 0.
11.  Connect the **Constant** to the **Alpha** input of the **TripleBilinearLerp** node.
    
    This ensures the material will compile before moving onto the next section of this guide.
    
12.  Connect the **TripleBilinearLerp** output to the **Emissive Color** input on the main material node.
13.  Click **Apply** to compile the material.

You should have something that looks like this now in the material graph below:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a437196c-1811-4d4a-993c-6d94d918a802/ust-mat-variableblur-5.png)

In the Preview window, you may notice that there is a `Red: Missing Input` error message for the `HalfC` user scene texture input in the **QuarterA** material instance. This error happens because QuarterA is using the HalfC input before it’s actually been written. The Preview window isn’t capable of handling multi-level dependencies. But, you can fix this issue manually by setting priorities for some of the passes in the materials.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c54b0e94-2fa5-4cfa-92e1-e1006941a2c5/ust-mat-variableblur-6.png)

To set the material priorities, follow these steps:

1.  Open the quarter-res passes for **QuarterA**, **QuarterB**, and **QuarterC**.
2.  In the **Details** panel for each of these material instances under the **Post Process Overrides**, check the box next to **Blendable Priority**.
3.  Set the **Blendable Priority** to **1** for each quarter-res instance.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c631af2b-4afa-4df1-972f-e3977a70c5f8/ust-mat-variableblur-7.png)
4.  **Save** and **Close** each material instance.
5.  Open the **BlurApply** material.
6.  In the **Details** panel, set the **Blendable Priority** to **2**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9978da74-a637-45a5-838c-cc4314a5df1f/ust-mat-variableblur-8.png)
7.  Click **Apply** to compile the material.

In the Preview window, the error message should be resolved, like the example below. This change makes it so that all the passes run **after** the half-res passes, guaranteeing that the half-res output has been created before it’s needed.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/716e67e7-3ff1-458f-a1f0-d84df9d86c22/ust-mat-variableblur-9.png)

#### Adding Variable Blur to the Material with Parameters

In the previous section, a Constant value was used to compile the material and get a result. However, we can use that Alpha input with some logic to actually vary the blur across the screen with some unblurred parts in the middle of the screen, medium blurred part around the screen, and heavier blurred outer edge of the screen to create this variable blur effect.

1.  Delete the **Constant** node plugged into the **Alpha** input of the **TripleBilinearLerp** node.
2.  Drag off the **Alpha** input on the **TripleBilinearLerp** node and add a **Multiply** node.
3.  Drag off the **A** input of the **Multiply** node and add a **Length** expression.
4.  Drag off the input of the **Length** node and add a **Subtract** node.
5.  On the **Subtract** node, set the value of **B** input to **0.5**.
    1.  This moves the location of the blur in screen space to the center of the frame.
6.  Drag off the **A** input of the **Subtract** node and add a **Screen Position** node.
7.  Click **Apply** to compile the material.

Your graph should look similar to this now:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0e102d0-8150-44db-9c4a-673f341ee675/ust-mat-variableblur-parameters-1.png)

Adjust the value for the **B** input values on the **Multiply** of the **Alpha** to control the intensity of the blur happening on screen.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4167196-0871-4dd3-ad3f-47ad74c70970/ust-mat-variableblur-parameters-2.png)

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2de03434-1e1e-41a2-8189-bac03b5dffee/ust-alpha-mult-1.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/796a2d37-d424-4b2f-b149-353700d1efcb/ust-alpha-mult-2.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8923939-5891-476b-810a-a7c4e3131aca/ust-alpha-mult-3.png) |
| Alpha Multiply: 1.0 | Alpha Multiply: 1.5 | Alpha Multiply: 2.0 |

You can create an area at the center of the screen where no blur is happening by adding a **Subtract** node before the **Multiply** node for finer control of this effect.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1104cf3d-7216-4b50-bafb-7f75434d2256/ust-mat-variableblur-parameters-3.png)

Incrementally adjusting the value of **B** on the **Subtract** node scales the area at the center of the screen where no blur is happening.

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5179aeef-c00f-4fe7-b425-f4a9c6428bd0/ust-subtract-1.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b5c23cb-c2cc-49c2-a1bb-8f9c942d7793/ust-subtract-2.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70db6b41-6ae4-40d4-84ed-309023add9da/ust-subtract-3.png) |
| Subtract: 0.0 (No Effect) | Subtract: 0.1 | Subtract: 0.25 |

To learn how you can set up some material logic to visually inspect where blur is being applied to the screen with this effect, see the [Applying Color to Debug the Material Effect](/documentation/en-us/unreal-engine/post-process-material-user-scene-textures-in-unreal-engine#applyingcolortodebugthematerialeffect) section of this page.

## Adding the Post Process Materials to a Post Process Volume

The final step is to set up and add the post process materials to a post process volume in the scene to see the variable blur post process effect working.

1.  Add a **Post Process Volume** to your scene and scale it to encompass a large enough area to see the effect when applied.
    
    You can check the box for **Infinite Extent (Unbound)** to have the volume cover the entire world rather than just its bounding box.
    
2.  In the **Details** panel under **Rendering Features**, expand the **Post Process Materials** section.
3.  Click the **Add (+)** icon next to the **Array** to add a new Post Process Material element. Repeat this step until you have **7** array elements.
4.  Next to each of the array elements, click the dropdown and choose **Asset Reference**.
5.  Next to each of the array elements, click the dropdown and assign each of the **Post Process Materials** you created throughout this guide. They should be assigned in this order since they will be run in this order:
    1.  HalfA
    2.  HalfB
    3.  HalfC
    4.  QuarterA
    5.  QuarterB
    6.  QuarterC
    7.  BlurApply

Your the Post Process Materials array should look like this now:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b21801e-392c-4866-8740-174152faec79/ust-ppm-ppv-1.png)

When applied to the post process volume, the effect can look like this, with an unblurred center, medium blurred middle, and heavier blurred outer edge.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e9e469b-ccc9-4e44-b688-a08115a93f44/ust-example-fp.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ddc4c01-78d4-410b-a372-639f3b347bdd/ust-example-tp.png) |
| First Person Template | Third Person Template |

At first glance, it may be hard to see what parts of the screen have no blur, a medium blur, or heavy blur. You can use some material logic to visually inspect where blur is applied by following the directions in the [Applying Color to Debug the Material Effect](/documentation/en-us/unreal-engine/post-process-material-user-scene-textures-in-unreal-engine#applyingcolortodebugthematerialeffect) section of this page.

### Applying Color to Debug the Material Effect

To make this variable blur effect more visible in the scene, you can apply some color modulation with a little bit of material logic. This will help identify the different levels of blur independently on the screen for their user scene texture inputs.

1.  Open the **BlurApply** material.
2.  On **UserSceneTexture:HalfC** pull off the **Color** output and add a **Multiply** node.
3.  Right-click in the graph and add a **Constant4Vector** and set a color for it.
4.  Connect the **RGBA color pin** to input **B** on the **Multiply** node.
5.  Connect the **Multiply** output to input **B** on the **TripleBilinearLerp** node.
6.  Repeat these steps for **UserSceneTexture:QuarterC** and connect its **Multiply** to input **C** on the **TripleBilinearLerp** node.

You should have something that looks similar to this:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/821bb052-f964-4d10-ab5e-889d42f68329/ust-debug-material-colors-1.png)

This will result in material preview window looking similar to this:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87de5aae-59d5-40f0-a525-a1c8a7e645ad/ust-debug-material-colors-2.png)

Once you have this setup, you can use the **Multiply** node on the **Alpha** input of the **TripleBilinearLerp** to scale up the variable blur effect.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/807c0947-2e3e-4164-9856-7011473323d8/ust-debug-material-colors-3.png)

Below are some examples demonstrating this scaling factor in the material preview window:

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90b1c8e9-82ff-4aa0-ab2e-e5452e1e1981/ust-debugcolors-1.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ecc65e8-b6f0-4057-88e8-6e30d1d092eb/ust-debugcolors-2.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54030b9b-0c8f-42f4-826a-9a681f983265/ust-debugcolors-3.png) |
| Debug Colors Alpha Multiply: 1.0 | Debug Colors Alpha Multiply: 1.5 | Debug Colors Alpha Multiply: 2.0 |

The **Subtract** node helps create a dead space in the center of the frame where there is no blurring at all. Start with a small value and incrementally increase to get a desired dead space.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c0861dd-b963-4de9-aa8f-6c1d3c17f1a1/ust-debug-material-colors-4.png)

Below are some examples with incremental increases to the Subtract value to have no blurring applied to the center of the frame.

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29302a36-c67a-43a5-895f-3d1be5d19082/ust-debugcolors-4.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4c61a38-4f3d-4ad5-bfd2-52cdfffc221f/ust-debugcolors-5.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b73e1d0c-7ed0-4d8e-a0b2-0ffb713143b3/ust-debugcolors-6.png) |
| Debug Coloros Subtract: 0.0 (No Effect) | Debug Colors Subtract: 0.1 | Debug Colors Subtract: 0.25 |

When this material is applied to your Post Process Volume, you can use it to clearly see how the variable blur effect is applied in a game setting, like the ones below using the First Person and Third Person templates.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f57f5755-104e-46de-84f4-e7d1b8388820/ust-debugcolors-7.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fddd57b3-d779-47ae-aafc-a54b4b54f8d0/ust-debugcolors-8.png) |
| First person Template using material debug colors. | Third Person Template using material debug colors. |
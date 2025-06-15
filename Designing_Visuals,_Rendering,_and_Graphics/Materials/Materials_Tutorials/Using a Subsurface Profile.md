# Using a Subsurface Profile

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-a-subsurface-profile-in-your-unreal-engine-materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-a-subsurface-profile-in-your-unreal-engine-materials)  
**Processed:** 2025-06-14 16:58:11

---

The ability to render realistic looking human skin is a must for any modern Video Game engine. To fulfill this need, Unreal Engine now offers a shading method specifically for skin or wax like surfaces called **Subsurface Profile**. While the Subsurface Profile shading model has similar properties to the **Subsurface** shading model, its key difference is in how it renders. SubsurfaceProfile uses a rendering approach that is based in Screen Space because this helps to better display the subtle subsurface effects seen in human skin where backscattering is a secondary effect only seen in few cases like ears for example. The following document will cover what a Subsurface Profile is and how you can use them in your work.

## Enabling Materials to use Subsurface Profiles

Enabling your Material to use a Subsurface Profile can be done in the following few steps.

1.  First create a new Material by **Right-Clicking** in the **Content Browser** and then selecting Material from the **Create Basic Asset** list. Once created, make sure that you name the Material. For this example, the Material will be named **M\_Subsurface\_Profile**. When completed, your **Content Browser** should look like this.
    
    ![Create a new Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82c8d7ed-7721-4824-b5d3-6aeff211f6ad/create-new-material.png)
2.  **Double-click** the Material in the **Content Browser** to open it in the Material Editor.
    
3.  Now with the Material open, we need to change the Material's **Shading Model** from **Default Lit** to **Subsurface Profile** in the Details panel.
    
    ![Enable Subsurface Profile Shading Model](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c24124ae-703c-486d-bc25-085e8375be47/enable-subsurface-profile.png)
4.  At this time, you can assign a **Subsurface Profile** by inputting one into the **Subsurface Profile** section in the **Details** panel.
    
    ![Assign a Subsurface Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f9e3ea6-5289-4722-9497-e86882704da4/select-subsurface-profile.png)
5.  Now the Material is ready to be used with a Subsurface Profile.
    

## Creating Subsurface Profiles

Creating Subsurface Profiles is something that can be accomplished in the following steps.

1.  First **Right-Click** in the **Content Browser**, open the **Materials** context menu, and select the **Subsurface Profile** option.
    
    ![Create subsurface profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fe81c07-e119-4fd0-8a0e-aa9429cd6d31/create-subsurface-profile.png)
2.  Once the Subsurface Profile has been selected and created, you can name it. For this example, we will name our Subsurface Profile **SSP\_00**. Once completed, you should have something that looks like this.
    
    ![Subsurface Profile Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b2866ed-ca38-4918-aa77-66c18e152dc6/ssp-asset.png)

## Creating a Material that Uses a Subsurface Profile

Now that the Material and Subsurface Profile have been created, it is now time to fill them in with data. In the following steps, we will be creating a Material and a Material Instance that can make use of a Subsurface Profile.

1.  Open the **M\_Subsurface\_Profile** Material in the Material Editor if you do not already have it opened.
    
2.  With the Material open, it is time to place down some Material Expression nodes. For this tutorial, we are going to make use of the following nodes.
    
    -   **Vector Parameter** x 1
    -   **Scalar Parameter** x 2
    
    ![Required Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3607dd0-381c-422a-8b10-aa2f13436dac/required-nodes.png)
3.  Now that we have the Material Expression parameter nodes added to the graph, you will need to name them and fill in their default values. For this example, we will be giving the nodes the following names and default values.

| Property Name | Value |
| --- | --- |
| **BaseColor** | R: 1.0 G: 1.0 B: 1.0 |
| **Roughness** | 0.35 |
| **SubsurfaceAmount** | 0.5 |

Connect each of the nodes to their corresponding input on the Main Material Node. When everything has been filled in, your shader graph should look something like this.

![Parameter Default Values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1d7b7ee-eca2-4c06-8209-32fac0fb2af2/parameter-default-values.png)

1.  Now that everything is wired up, you can add your Subsurface Profile to the Material. To do this, first find the **Subsurface Profile** input in the **Material** section of the **Details** panel. Use the drop-down menu to select the **SSP\_00** asset you created earlier, or drag it from the Content Browser directly onto the input.
    
    ![Select Subsurface Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63f94da5-ce90-4074-b320-4e382d0e2c1c/apply-subsurface-profile.png)
    
    If you do not provide a Subsurface profile, a default one will be used. The default one that is used is a close approximation to Caucasian skin.
    
2.  With the Subsurface Profile applied and the Material expressions linked to the main Material node, it is now time to compile the shader and get ready to make a Material Instance out of this Material. When completed with the Material, it should look something like this.
    

## Using a Subsurface Profile in a Material Instance

1.  With the Material now created and compiled, it is now time to make some Material Instances to make tweaking of parameters faster. To make a Material Instance from our Material, first locate the Material in the **Content Browser** and then **Right-Click** on it and select the **Create Material Instance** option. When completed, your **Content Browser** should look something like this.
    
    ![Create Material Instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3955a573-051c-4672-bde9-47f47abe0afd/create-material-instance.png)
2.  Now that the Material Instance has been created, open it up by using the **Left Mouse Button** to **Double-Click** on it in the **Content Browser**. Once open, you should see something that looks like this.
    
3.  To change the Subsurface Profile in a Material Instance, you can enable the **Subsurface Profile** override by checking the box, and then use the drop-down menu to select a different Subsurface Profile asset. Once you click on the input you should see the Subsurface Profiles that are available to choose from.
    
    If you have already supplied a Subsurface Profile in the Parent Material, then you do not need to override it in the Material Instance. This is only if you wish you use a different Subsurface Profile than what is already being used.
    

## Applying a Subsurface Profile Material

1.  Now that the Material Instance has been created, it is now time to test out our new Material. To do this, we first need to create a new blank level to work in by going to the main menu and under the **File** option select **New Level**. When prompted what type of level to select, select the **Empty Level**.
    
    ![Create empty level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3fdc00c3-2bea-421d-81e6-57fe3d65b144/empty-level.png)
2.  To test the Material, we will use a Static Mesh from the Starter Content, lit from the front by a **Point Light**, and from behind with a very bright **Spot Light**. This strong backlighting will help demonstrate how Subsurface Profile Materials can transmit and scatter light. The lighting configuration should look something like the image below.
    
    ![Lighting Configuration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa0f1f2f-17df-4762-a70b-0ec37822f029/lighting-configuration.png)
3.  Find the **SM\_Statue** Asset in the Content Browser under **StarterContent** > **Props** and add it to your Level. The location and rotation settings in our example are shown below.
    
    | Property Name | Value |
    | --- | --- |
    | Location: | X:0, Y: 0, Z:0 |
    | Rotation: | X:0, Y: 0, Z:-23 |
    
4.  Open the **Place Actors** menu and add both a **Point Light** and a **Spot Light** to your level.
    
    ![Add lights to level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5712ddb4-b6ae-4588-b319-ae302ea0b6d1/add-point-and-spot.png)
5.  Select the Point light and configure it with the following settings in the Details Panel.
    
    | Property Name | Value |
    | --- | --- |
    | Location: | X:380, Y: 0, Z:80 |
    | Intensity: | 8.0 cd |
    
    ![Point Light Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54ec804f-10ae-46bd-9a51-2c2d93f5d6b7/point-light-details.png)
6.  Select the Spot Light and configure it with the following settings in the Details Panel.
    
    | Property Name | Value |
    | --- | --- |
    | Location: | X:-650, Y: 100, Z:-75 |
    | Rotation: | X:0, Y:20, Z:0 |
    | Intensity: | 1500 cd |
    
    ![Spot Light Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9c7ce41-66af-4f01-a997-87725cdf11c8/spot-light-details.png)
7.  Apply the **M\_Subsurface\_Profile\_Inst** Material instance to the statue by dragging it from the Content Browser onto the Static Mesh in the Level, or onto both of the statue's Material Elements in the Details panel. Make sure you drag it onto both pieces of the sculpture.
    
    ![Statue details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/827acfca-a858-49fb-8ed2-6a4ec94a8218/apply-material-to-statue.png)
8.  The effect of the Subsurface Profile is most obvious along the edges of the highlight, where the spotlight falls into shadow. Along this contour, you can see the reddish-pink subsurface color coming through, in contrast to the lavender base color of the statue and the intense white highlight.
    

## Adjusting a Subsurface Profile

1.  Once the Material Instance has been applied to the statue, you can adjust the Subsurface Profile settings. To do this, open the Subsurface Profile by double-clicking the **SSP\_00** asset in the Content Browser. You should see something like this being displayed.
    
    ![Subsurface Profile editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f63c708-960c-4ecb-8fa9-1b50bb5e4934/subsurface-profile-editor.png)
    
    You can adjust the properties of the **Subsurface Profile** by changing the values or colors in the editor.
    
    -   **Surface Albedo:** Should match the base color of the corresponding Parent Material as closely as possible.
        
    -   **Mean Free Path Color:** Controls how far light penetrates into the surface for the red, green, and blue channels, and determines the color of the region where light is scattered beneath the surface. Lighter values allow more transmission, black effectively turns off the subsurface scattering.
        
    -   **Mean Free Path Distance:** A distance in world/Unreal units (cm), which scales how far light will penetrate into the surface. Decreasing makes the subsurface region tighter/sharper, increasing this value makes the subsurface region larger and blurrier.
        
2.  Keep in mind that you can adjust the parameters of the Subsurface Profile in real time as demonstrated below.
    

## Tips & Tricks

Because of how Subsurface Profiles render, there are a few Tips & Tricks to getting the most out of using them.

### Scatter Radius

Setting the **Mean Free Path Distance** of the Subsurface profile to a really big number will result in rendering errors as you can see in the following image.

![Scatter Radius example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7b8ad55-d747-4c53-b741-0a603e107155/ssp_big_small_scatter_radius.png)

In the image on the Left, the Mean Free Path Distance was set to 50. Notice how it looks like there are multiple images rendered on the surface. Now take a look at the image on the Right. In this image the Mean Free Path Distance was set to 5.0. Notice how the image looks softer and more natural. This is the type of effect we are trying to achieve.

### Combining a Material Instance with a Subsurface Profile

Combining a Material Instance with a Subsurface profile is a great way to get the most control over your results for a number of reasons.

-   A Material Instance allows you to tweak values in real time which makes seeing your results much quicker.
-   You can use the **Opacity** input to dampen the Subsurface contribution to the surface. However it is recommended that you keep this value at 1 and adjust the parameters inside the Subsurface Profile. Only adjust this value if you find that you cannot get the results you are looking for when adjusting the Subsurface Profile.
-   The **Value** slider of each color picker controls the influence of the Subsurface effect. The closer that this value is set toward white, the more prominent the effect will be. While the closer the value is set to black, the less visible the effect will be.
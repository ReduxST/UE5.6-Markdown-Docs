# Using Subsurface Scattering

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-subsurface-scattering-in-unreal-engine-materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-subsurface-scattering-in-unreal-engine-materials)  
**Processed:** 2025-06-14 17:01:11

---

Subsurface scattering is the term used to describe the lighting phenomenon where light scatters as it passes through a translucent / semi translucent surface.

Unreal Engine offers a special [Shading Model](/documentation/en-us/unreal-engine/shading-models-in-unreal-engine) called [Subsurface](/documentation/en-us/unreal-engine/subsurface-shading-model-in-unreal-engine) that is used specifically for Materials that need this interaction like skin or wax.

The following tutorial will walk you through all you need to know about how to use subsurface scattering in your Materials.

## Enabling the Subsurface Shading Model

Enabling a Material to use the Subsurface shading model can be done a few steps.

1.  First create a new Material by **Right-Clicking** in the **Content Browser** and then selecting Material from the **Create Basic Asset** list. Give the Material a descriptive name like **M\_Subsurface\_Scattering**. When completed, your **Content Browser** should look like this.
    
    ![Create Material asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18e8b339-dc0c-4abb-ba4b-f6d698925ce0/create-new-material.png)
2.  Open up the Material by **Double-Clicking** the asset in the Content Browser.
3.  In the Details Panel of the Material Editor, change the Material's **Shading Model** from **Default Lit** to **Subsurface**.
    
    ![Enable Subsurface Shading Model](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/117954b9-8c27-43f6-9e1e-b10e15a7b177/subsurface-shading-model.png)
4.  The Material is now ready to be used as a Subsurface Material.

## Setting up a Subsurface Material

Continuing with our Material from above that has Subsurface Scattering enabled, let's setup a basic Material so that we can see the Subsurface scattering in action in a level.

1.  We need to place down some Material Expression nodes so that we have something to work with. For this example, we are going to be adding the following nodes.
    
    -   **Vector Parameter** x 2
    -   **Scalar Parameter** x 2
    
    ![Required nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03f7650a-c805-4703-9db3-a7c9a02aafbf/required-nodes.png)
    
    The reason that we are using Parameter Material nodes instead of regular Material nodes is so that we can make a Material Instance out of this Material for easier tweaking inside the editor.
    
2.  Before we start to connect the nodes, we first need to name them as well as set default values for them. The names and default values for the nodes are as follows.
    
    ![Node setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04b5db61-5260-4fe1-8e25-4d883a794307/node-setup.png)
    
    | Property Name | Value |
    | --- | --- |
    | **Base\_Color** | r:1.0, g:1.0, b:1.0 |
    | **Roughness** | 0.35 |
    | **Opacity** | 0.5 |
    | **Subsurface\_Color** | r:1.0, b:0, g:0 |
    
3.  After renaming all four parameter expressions and setting their default values, connect them to their corresponding inputs on the Main Material Node as shown above.
    
4.  Once the nodes have been connected, make sure that you compile the Material by pressing the **Apply** button, and **Save** the Material. Once compiled, you should have something that looks like this.
    
    ![Save Material Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52d57562-dbe3-4c73-9882-8c10fb2c6d59/save-and-apply.png)
5.  Once the Material has been compiled, you can close the Material Editor window. Then inside of the **Content Browser**, select the Material, **Right-Click** on it, and then select the **Create Material Instance** option from the menu.
    
    ![Create Material Instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86c9ff26-d6de-4542-943e-34e54546d6df/create-material-instance.png)

## Testing the Subsurface Material

Now that the Material Instance has been created, you can test the Material in a Level.

1.  To do this, you first need to create a new blank level to work in by going to the main menu and under the **File** option select **New Level**. When prompted what type of level to select, select the **Empty Level**.
    
    ![Create Empty Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bdbf527b-6fe3-4e8a-8c17-9cf90dd14266/new-level-dialog.png)
2.  To test the Material, we will use a Static Mesh from the Starter Content, lit in front by a **Point Light**, and from behind with a very bright **Spot Light**. This strong backlighting will help demonstrate how Subsurface Materials can transmit and scatter light. The lighting configuration should look something like the image below.
    
    ![Lighting Configuration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a1eed1a-28f3-4c94-bb80-b1a4151115f1/lighting-configuration.png)
3.  Find the **SM\_Statue** Asset in the Content Browser under **StarterContent** > **Props** and add it to your Level. The location and rotation settings in our example are shown below.
    
    | Property Name | Value |
    | --- | --- |
    | Location: | X:0, Y: 0, Z:0 |
    | Location: | X:0, Y: 0, Z:-23 |
    
4.  Apply the **M\_Subsurface\_Scatterin\_Inst** Material instance to the statue by dragging it from the Content Browser onto the Static Mesh in the level, or onto both of the statue's Material Elements in the details panel.
    
    ![Statue details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af448fa9-c3bc-45d9-ade0-554d562df435/sm-statue-setup.png)
5.  Open the **Place Actors** menu and add both a **Point Light** and a **Spot Light** to your level.
    
    ![Add lights to level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f99920c4-d971-42c7-a28d-4a387cfccdcc/add-point-and-spot.png)
6.  Select the Point light and configure it with the following settings in the Details Panel.
    
    | Property Name | Value |
    | --- | --- |
    | Location: | X:380, Y: 0, Z:80 |
    | Intensity: | 8.0 cd |
    
    ![Point Light Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0122569b-9165-46ba-8ea1-3fbcbc31b721/point-light-details.png)
7.  Select the Spot Light and configure it with the following settings in the Details Panel.
    
    | Property Name | Value |
    | --- | --- |
    | Location: | X:-650, Y: 100, Z:-75 |
    | Rotation: | X:0, Y:20, Z:0 |
    | Intensity: | 1500 cd |
    
    ![Spot Light Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87840d51-2c87-463d-b318-23f62d20b083/spot-light-details.png)

## Working with the Subsurface Material

Now that the Subsurface Material has been applied, it is time to tweak the settings of the Material Instance.

In the following sections, we will go over how we can control how our Subsurface Material will look and how to tweak the various options in the Material Instance to get the results that we want.

### Opacity Controls

In the current setup of our Subsurface Material, the Opacity input controls the amount of light that we want our object to scatter.

A setting of 0 will allow all light to scatter where a setting of 1 will let no light scatter. The following example shows light being scattered through the statue mesh with the Opacity value set at 0 in the image on the left, 0.35, 0.65, and and 1.0 in the image on the right. Notice as the numbers go from 0 to 1, the amount of light we see passing through the object becomes less and less.

![Subsurface Opacity comparison](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9923bc52-fad6-4dfd-9c52-ab693d8fc5ee/sss-opacity-comparison.png)

While the Opacity does help to get rid of a lot of the scattered light, you might notice that there is still some Subsurface scattering happening. To get completely rid of the effect, you are also going to have to adjust the **Value** of the Subsurface Color (More on this in the Subsurface Color Value section below.)

### Subsurface Color Value

While you can adjust the amount of Subsurface scattering that happens via the Opacity input, you can also adjust this using the **Value** slider in the **Color Picker**.

For example, setting the Opacity to a value of 1.0 and setting the Subsurface Colors Value from White to Black will effectively turn off Subsurface Scattering like in the example below.

  ![Value Slider 01](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/780d6c68-8496-48b4-93f3-9d58a968a50e/subsurface-value-01.png) ![Value Slider 02](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ddfa295-90e9-44c4-8661-d9d2b7c593cd/subsurface-value-02.png) ![Value Slider 03](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07cd6c32-0b50-484a-b878-34f22790dd51/subsurface-value-03.png)

**Subsurface color value at 0, 0.5, and 1.0.**

Here is an example of adjusting the value in real time. Notice how as the Value of the color is adjusted from Red to Black, the amount of Subsurface scattering influence is affected.

## Using a Texture as a Subsurface Influence Mask

You can use a Texture as a Mask to have more control over what areas receive or do not receive Subsurface scattering. To do this, all you need to do is plug the Texture you want to use as the Mask into the **Opacity** Channel of your Material. In the following example, not only are we using a Mask texture, we are also using a Scalar value to control the intensity of the Mask so that we can have more control over the amount of Subsurface scattering that is happening.

![Masked Subsurface graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd84f2ab-7e65-46ba-a17a-d7fb91a159fd/subsurface-masked-graph.png)

Mask textures work based on values going from Black to White. Values that are closer to Black will allow the Subsurface effect to come through while values that are closer to White will not allow the Subsurface effect to come through.

Here is what the Material above, using the Mask Texture, looks like in the level. Notice the Black spots on the cube. Those Black spots are the result of using a pure white value in the Mask Texture.

![Masked Subsurface example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1945a70-da87-4e12-aced-0247f6a2c500/masked-subsurface-scattering.png)
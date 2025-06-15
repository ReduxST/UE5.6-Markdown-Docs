# Your First Graphic with Motion Design

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/your-first-graphic-with-motion-design-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/your-first-graphic-with-motion-design-in-unreal-engine)  
**Processed:** 2025-06-14 17:05:28

---

This tutorial provides a set of step-by-step instructions about how to use Unreal Engine's Motion Design tools to create an animated 2D graphic that you can control in real time, causing it to enter the screen, leave the screen, and transform on screen. This workflow is a foundation you can build on to create more advanced and complex animations in both 2D and 3D using Motion Design.

## Getting Started

This tutorial assumes you are familiar with the content of the [Motion Design Quickstart](/documentation/en-us/unreal-engine/motion-design-quickstart-guide-in-unreal-engine). If you haven't read it already, start there. When you have enabled the required plugins, and reviewed the sections on creating a new level and the Motion Design UI, continue below.

There are two ways to continue with this tutorial, both equally valid.

1.  Use Motion Design in an [existing level](/documentation/en-us/unreal-engine/your-first-graphic-with-motion-design-in-unreal-engine#usemotiondesigninanexistinglevel).
    
2.  Create a new level using the [Motion Design template](/documentation/en-us/unreal-engine/your-first-graphic-with-motion-design-in-unreal-engine#createanewmotiondesignlevel).
    

### Use Motion Design in an Existing Level

Your first option for this tutorial is to open the **Motion Design interface** on an existing level by clicking the **Motion Design** button in the toolbar.

![The Motion Design button in the toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1105496e-1461-450c-a6e1-fa2897ab3e5b/image_0.png)

The Motion Design button in the toolbar.

You can also use the Motion Design tools without changing the entire interface by switching to the **Motion Design Mode** in the Modes dropdown. This Mode can also be opened using SHIFT+9 on your keyboard.

![Motion Design in the Modes menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f85ac04b-e75a-4e49-bc79-c17045c00154/image_1.png)

Motion Design in the Modes menu.

#### Populating an Empty Level with Default Elements in a Motion Design Scene

If you choose the first option above, to start from an empty level, you’ll need to activate **Motion Design** mode by clicking on the button at the top-middle of your screen. By default, when you create an empty new level in Unreal Engine, there are no lights, post-process volumes, or cameras.

![The Motion Design button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95469a55-faae-4a02-bfc5-3ba3f77ff044/image_2.png)

The Motion Design button.

1.  Select which recommended default actors you want to add to your empty level by clicking **Create Defaults**. This opens the **Configure Default Scene Actors** window with several options.
    
    ![The Create Defaults button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24020a29-46b8-42a7-b0c4-a77f629b6d38/image_3.png)
    
    The Create Defaults button.
    
2.  Select which **Motion Design Default Scene Actors** you want to add or replace in your scene and click **Spawn**. For this tutorial, use the default options.
    
    ![The Configure Default Scene Actors window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48122e3d-67f9-41c9-8b84-04da862789ee/image_4.png)
    
    The Configure Default Scene Actors window.
    

The Viewport and Motion Design Outliner then both update with the options you selected.

### Create a New Motion Design Level

For this tutorial, your second option is to create a new level using the Motion Design template.

Create a new level (File > New Level). In the prompt window, select what kind of level you want to create. The **Motion Design** template is used for 2D designs, while **3DMotion Graphics** is used for 3D designs. This tutorial covers 2D design.

-   To follow the steps in this tutorial, select the **Motion Design** template, and click **Create**.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92049515-f0fc-4010-862c-a19afc146035/image_5.png)
    
    Select the Motion Design template.
    

#### Spawn Default Scene Actors

After creating the new level from the Motion Design template, you must configure and spawn your default scene actors.

1.  Click the **Create Defaults** button to open the **Configure Default Scene Actors** window.
    
2.  For this tutorial, you have to use the default options, so click **Spawn** to create the default scene actors.
    
    ![The Configure Default Scene Actors window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df9c202c-8c5d-4b11-99ae-3ea9f2268e52/image_6.png)
    
    The Configure Default Scene Actors window.
    

## Creating an Animated 2D Graphic Using Motion Design

### What You’ll Learn

This section of the tutorial has instructions for using the Motion Design interface features and tools you will use to create an animated 2D graphic. These include:

-   Drawing and customizing 2D primitives.
-   Customizing geometry using the **Material Designer.**
-   Positioning content using Null Actors.
-   Adding text.
-   Constraining text to fit certain background sizes.
-   Controlling text with Remote Control.
-   Playing in a Sequencer animation, stopping it using the Sequencer mark system, then continuing from that mark to play the off-animation.

### Initial Template Edits

After creating your new level, your UE user interface resembles the following image:

![The Motion Design template initial state](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1db7e9b2-bfce-4d23-b503-413e7230274b/image_7.png)

The Motion Design template initial state.

In this tutorial, you are going to create something new, so begin by deleting the graphical elements that spawn automatically with the template.

1.  In the **Motion Design Outliner**, click on the **Starter Content** group
    
2.  Press **delete** on your keyboard, and confirm you want to delete the children of the selected object in the dialogue window.
    

You should now see an empty Viewport similar to the following image.

![The Motion Design template after deleting the Starter Content group](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3946b94a-8352-42d5-8e38-696b06f6609d/image_8.png)

The Motion Design template after deleting the Starter Content group.

The Viewport might display as a black screen. You can switch it to the checkerboard pattern using the **View** options in the lower-right of the Viewport.

You must set your canvas dimensions.

1.  To do so, click the **Camera** button on the upper-left of your Viewport.
    
2.  Select **Ruler Override**.
    
3.  Use the **Resolution** settings to define the size of your canvas according to the requirements of your project.
    
    ![Use Ruler Override to set the size of your canvas](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8529a64-0b08-4bb1-bc78-85085cb672f6/image_9.png)
    
    Use Ruler Override to set the size of your canvas.
    

### Shape Creation and Groups

You can create shapes using the Motion Design toolbox. If this panel is not open, you can access it by clicking the **Mode** dropdown, and selecting **Motion Design**.

![Select Motion Design in the Mode dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c523a7a-2b24-4b82-b8d9-3f6de0adddfd/image_10.png)

Select Motion Design in the Mode dropdown.

You can choose from several shape options. For this tutorial, begin with a **Rectangle**.

-   Double-click the **Rectangle** to spawn one in the center of your canvas.
    
    ![Double-click the Rectangle button to add a rectangle to your canvas](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8387129b-316c-400e-9c47-11d5c1330fd5/image_11.png)
    
    Double-click the Rectangle button to add a rectangle to your canvas.
    
    ![Your newly-created rectangle should resemble this image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3acb3c0-c366-4a8c-9210-fe3e68e9627d/image_12.png)
    
    Your newly-created rectangle should resemble this image.
    

You can customize the shape and properties of your new rectangle (such as slant and bevel) in the Details panel on the lower right side of the interface. You can also change the sizing by clicking and dragging the handles of the newly created shape.

Next, anchor your shape.

1.  In the **Details** panel, select the **Shape** category.
    
2.  Change the **Horizontal Alignment** to **Left**, and the **Vertical Alignment** to **Center**.
    
    ![Changing the horizontal and vertical alignment](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e32feee9-bdfe-41e4-bcb1-03a0b89d7ea1/image_13.png)
    
    Changing the horizontal and vertical alignment.
    

You will eventually have other actors that will move around at the same time as a **Group**.

-   To create a Group, select the rectangle and press CTRL+G on your keyboard, or click the **Group** button found in the Motion Design Outliner.
    
    ![The Group button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7b327e3-a6f0-4a13-a697-b24cb5bba95b/image_14.png)
    
    The Group button.
    
    This creates a null actor parent of the Rectangle actor.
    
    ![The null actor parent of your Rectangle actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87b11423-db83-4963-9520-4c519354fa43/image_15.png)
    
    The null actor parent of your Rectangle actor.
    

In the Details panel, you can experiment with changing the location of the null actor. Changing the null actor’s position does not affect the position of the rectangle actor.

1.  Rename the rectangle to **BG\_Main** by right-clicking it in the **Motion Design Outliner**.
    
2.  Move the rectangle over to the left side of the screen so it is flush with the edge of the canvas.
    
    1.  You can do this using the rectangle geometry, or you can position the rectangle by using its null actor parent.
        
    2.  To do so, select that **null actor**, and rename it to **L3\_BG**.
        
    3.  Using the parent, move the **Location** of the **group** in the **Details** panel.
        
    
    ![Renaming the null actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2a7fa97-786c-4ec9-a3cb-d80f957f40b8/image_16.png)
    
    Renaming the null actor.
    

Your canvas should now resemble the image below.

![Moving the rectangle by moving the group](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b6e08e9-2817-47f1-91c1-ed437d19d8d4/image_17.png)

Moving the rectangle by moving the group.

You can hold down your middle mouse button to pan around the canvas. The shaded areas represent the \_offscreen \_region. In this tutorial, you are going to set up your graphic to slide offscreen, so keep the boundaries of your canvas in mind.

Next, size your rectangle:

1.  Click on the **BG\_Main** actor, and click the **Shape** button.
    
2.  In the Motion Design Outlines, make sure that **Size Type** is set to **Pixels**. This is the first setting under **Shapes**.
    
3.  Unlink your **Pixel Size** property by changing the Pixel Size from **XY** to **Free**.
    
4.  Set the **Pixel Size** property to 1842 x 132.
    
    You can size your shapes using either Unreal units or pixels. This walkthrough assumes you are using pixels, but all the features described here work for both.
    
    ![Setting your unlinked Pixel Size property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e12d1235-dc28-45c8-bdc7-ec7ec6c42dc7/image_18.png)
    
    Setting your unlinked Pixel Size property.
    

You are creating a lower-third graphic, so move the position of the entire group to where they typically live.

-   Select the **null actor** that parents BG\_Main, and set the **Y** position to -160.
    
    ![Setting the position of the null actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2de58515-602f-4704-95ee-7b47cd4a04c0/image_19.png)
    
    Setting the position of the null actor.
    

When everything is positioned, you Viewport should resemble the following image:

![The results of your initial positioning](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/579bc235-f263-40b9-8933-99712a412547/image_20.png)

The results of your initial positioning.

### Customizing the Graphic Using the Material Designer

Next, you will customize the lower third graphic to make it look more interesting than a simple gray box, using the **Material Designer**.

To customize the graphic:

1.  Select the shape, and click on the **Material** button in the **Details** panel.
    
2.  Set the **Material Type** to **Material Designer**.
    
3.  Click the **Edit with Material Designer** button.
    

The **Material Designer** tab should appear in your **Tool Parameters** section. Your Viewport should now resemble the following image:

![Setting up to use the Material Designer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91649adf-22db-4111-aa74-d3aa05fbe5e9/image_21.png)

Setting up to use the Material Designer.

The Material Designer is Motion Design’s layer-based material creation tool. Similar to other layer-based tools, such as graphic editing or photo editing software, each layer has a fill, a mask channel, and an independent opacity value, as well as a full suite of blend modes.

Below is an overview of the Material Designer interface:

![The Material Designer interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c9f187a-861b-408b-962b-2dbe28e142ae/image_22.png)

The Material Designer interface.

#### Interface Key

1.  Switch between a surface or a post-process material.
    
2.  Material type selector. The available options are:
    
    -   Opaque
    -   Masked
    -   Translucent
    -   Additive
    -   Modulate
3.  Adjust the opacity of the entire layer stack.
    
4.  Switch between adjusting the fill or the mask layer stack.
    
5.  Adjust layer opacity, and change the layer’s blend mode.
    
6.  Individual layer control for fill and mask.
    
    -   The chain icon determines whether to link the UVs of the fill and alpha texture.
    -   You can enable or disable either part by clicking on the white dot to the left of the layer thumbnail.
7.  The Viewport Utility Toolbar contains the following tools:
    
    -   Layer FX, which you can use to apply a variety of material effects to a layer.
    -   Add a layer.
    -   Duplicate a layer.
    -   Delete a layer.
8.  Layer settings, such as texture transforms and the ability to clamp a texture.
    

In the Material Designer interface image above, the fill of the layer (the checkerboard icon) is selected, and the image below displays some options to set the layer type. These include:

-   Texture
-   Solid Color
-   Color Atlas
-   Texture Edge Color
-   Gradient
-   Material Function

![Layer type options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b96cdaa-0f85-4fd3-9b57-26bfc268a4e6/image_23.png)

Layer type options.

1.  For now you want a simple solid color, so select **Solid Color**.
    
2.  Next, click the **Color** widget, and set the color in the popup menu.
    
    ![Setting your color using the Color Picker](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b9e581d-7949-44d0-bbd3-4d2b1f5da12a/image_24.png)
    
    Setting your color using the Color Picker.
    
3.  Set your color to green using the following RGB values:
    
    -   R: 0.0
    -   G: 0.441406
    -   B: 0.030081

### Adding a Pattern

Next, you will add a pattern by creating a new layer with the **Add New Layer** button found in the Viewport utility toolbar.

![The Add New Layer button in the Viewport utility toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47f4c9fd-8bd3-4d46-b8c9-d011ba470986/image_25.png)

The Add New Layer button in the Viewport utility toolbar.

By default, it creates a texture. When you click on the dropdown, several options appear.

-   Select a standard linear gradient texture. In the example shown below, the texture is named 2.
    
    ![Selecting a standard linear gradient texture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63f67cc4-1167-4b42-ab91-d7f70cc15de5/image_26.png)
    
    Selecting a standard linear gradient texture.
    

Next, you need to do some rotation and scaling of the UVs to get the type of pattern you want for this walkthrough.

1.  Disable the layer mask for this layer by toggling the mask off and unlinking the scale.
    
    ![Toggle off the mask and unlink the scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7804aa1d-a705-4360-b635-4decee00f447/image_27.png)
    
    Toggle off the mask and unlink the scale.
    
    You can also do this by creating a new layer and choosing **Texture No Alpha**.
    
2.  Set the **Properties** for the texture to the following:
    
    -   Type: Texture
    -   Texture: 2
    -   Offset: 0.0, 0.0
    -   Rotation: 45.0
    -   Scale: 0.035, 0.035
    -   Pivot: 0.5, 0.5
    -   Mirror on X: disabled
    -   Mirror on Y: disabled
    -   Clamp Texture: disabled
    
    ![Your new texture layer's properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7683776-b64f-485c-abcd-1f7c5028388f/image_28.png)
    
    Your new texture layer's properties.
    
3.  Set the **Blend** for the gradient layer to **Multiply** as shown in the image below.
    
    ![Blend layer set to Multiply](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88edde30-11ef-4bd1-8788-603d49c239d4/image_29.png)
    
    Blend layer set to Multiply.
    

Your graphic should now resemble the following image:

![The initial pattern has a harsh gradient](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/edc1ee36-9df2-4a0c-b7e1-89e67ff11dec/image_30.png)

The initial pattern has a harsh gradient.

Next, you need to reduce how harsh the gradient is.

-   Set the **Opacity** (list item 5 on the interface overview above) to 0.11.
    
    ![Reducing the opacity of the pattern softens the gradient](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c436d2a4-5213-48fd-b2db-c02f49fda663/image_31.png)
    
    Reducing the opacity of the pattern softens the gradient.
    

To break up the pattern, fade it toward the left side of the bar.

1.  Return to the layer settings and re-enable the layer mask, but keep the layer UV unlinked.
    
2.  Add another linear gradient to the mask (you can use the same one).
    
3.  Clamp it using the **clamp texture** button in the texture parameters. This prevents it from repeating the texture.
    
4.  Set the following properties on the alpha texture:
    
    -   **Clamp Texture: True**
    -   **Offset: -0.566, 0.0**
    -   **Rotation: 220.0**
    -   **Scale: 3.0, 0.0**

Your result should resemble the following image:

![Your banner after adding a clamped linear gradient](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fcb087a1-4c30-4075-8f06-98a89fc424b1/image_32.png)

Your banner after adding a clamped linear gradient.

Next, you’ll round the edges and skew the shape slightly.

1.  With your shape selected, click the **Shape** button.
    
2.  Select the **Right Slant** property, and set the value to 18.00.
    

**Beveling** works in two ways, independent for each corner or uniformly. For this design, you’ll bevel the top right and bottom right corners.

1.  Expand the options for **Top Right** and **Bottom Right** at the bottom of the **Shape** settings.
    
2.  Set their values as follows:
    
    -   **Type:** Curve In
    -   **Size:** 13.0
    -   **Subdivisions:** 8
    
    ![Your values should match those shown in this screenshot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3af027ef-ee38-4f7e-acc5-11cb61fb478f/image_33.png)
    
    Your values should match those shown in this screenshot.
    

You can change the Viewport background from a checkerboard to solid black in the **Viewport Utility Bar > RGB**. This makes it easier to view your graphic.

![Set the Viewport to a black background using the RGB setting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6c57fd5-61a1-4ecb-a263-31733b2c79b9/image_34.png)

Set the Viewport to a black background using the RGB setting.

1.  To recreate the background bar, **right-click** on your **L3\_BG group** and select **duplicate**. The bar’s color will be white, and the bar itself will be offset slightly.
    
2.  Rename the actor to **L3\_BG\_Bar\_Offset**.
    
3.  Place it below your other bar in the Motion Design Outliner. You should see a bit of flickering, since there is nothing governing the priority of the two bars yet.
    
4.  Select your L3\_BG and L3\_BG\_Bar\_Offset actors, and group them by pressing CTRL+G.
    
5.  **Right-click** your new **null actor** at the root of your group and add a modifier called **Translucent Priority**.
    
    ![Adding the Translucent Priority modifier](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50731b2a-4f00-4a7e-9922-64da352e217f/image_35.png)
    
    Adding the Translucent Priority modifier.
    

The **Translucent Priority** modifier automatically sorts the render priority of translucent objects. The first item on the list renders on top of the next item. You can use this on a large nested group of actors, or on individuals. In this tutorial, you are going to use a translucent object at the top of your Motion Design Outliner, and let the Translucent Priority modifier regulate everything.

Move your graphics so they are offset instead of directly on top of each other.

-   Offset the L3\_BG\_Bar\_Offset so that the **Z value** is **\-170.0**. The result should resemble the following images:

![Your graphic should look like this](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7caeb238-61ba-42ad-a58f-92ef870d841c/image_36.png) ![Your UI should look like this](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b72e597-d73a-49f0-9dee-6e5a6522478c/image_37.png)

Your graphic and UI should look like this.

## Adding Content in Motion Design

Next, you will add a logo and some text to the bar graphics you already created.

### Adding Text to the Layout

To create some text, return to the **Toolbox**.

When working with text, remember that for a given text actor, all the characters will share the same settings. If you want individual characters to use different fonts, colors, sizing, and so on, you need to use separate text actors for each character that requires different settings.

![The Motion Design user interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4575e7f6-5536-4f35-889f-acde01828d6d/image_38.png)

The Motion Design user interface.

The Motion Design interface is fully described in the [Motion Design Quick Start](/documentation/en-us/unreal-engine/motion-design-quickstart-guide-in-unreal-engine).

1.  In the Toolbox (#2 in the image above, to the left of the Viewport), there is an **Actors** button. Click that button to show all of the different types of actors you can add to your design.
    
2.  Double-click on the **Text Actor** to add it to the root level of your Motion Design Outliner.
    
3.  Drag the new Text actor into the null actor group, so it appears in line with your background and your background bar offset.
    
4.  Rename the actor by double-clicking it in your Motion Design Outliner, and call it **Text\_Line\_1**.
    
5.  With your Text\_Line\_1 actor selected, press **CTRL+G** to group it.
    
6.  Name the group **Text\_Lines** so it is identifiable.
    
7.  You want to have two text lines, so right-click and **duplicate** Text\_Line\_1, then rename the duplicate to Text\_Line\_2.
    

### Changing the Font

You can set the font of the text by going into your Motion Design Outliner, selecting one of the text actors, and going into your Details panel. There are several buttons you can select; click on the one called **Text**.

In the Details panel at the bottom, with the Text button selected, you can update the content of the text line by changing the string in the text field. You can also change your font and typeface.

1.  Change the font to Roboto.
    
2.  Change the typeface to Italic.
    
3.  Shift the position of Line 2 down so the lines do not overlap.
    
    ![Setting the font and typeface for your text actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e7e625b-4346-4db0-b83a-22530be47214/image_39.png)
    
    Setting the font and typeface for your text actor.
    

Notice the text is covered by the green bar. You can correct this by using the Translucent Sort Priority modifier that you set up previously. However, to use that modifier your actor must use a translucent material type.

1.  Select one of your text actors, then click on the **Style** button in the Details panel. You’ll see that the Translucency style is set to None, which means the Translucent Sort Priority modifier can't sort it as it is not translucent.
    
2.  Change the style to **Translucent**.
    
3.  Repeat this for the other text actor, and you will now see the text appearing on top of the bar.
    
4.  Selecting the **Text\_Lines** null actor at the root.
    
5.  Click the **General** button in the Details panel.
    
6.  Move the entire group down by shifting the null actor **Location** down, until it overlaps with the bar.
    
7.  Select each text line, and set the **scale** to 0.45 in the transform settings.
    
    ![General text actor settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d487b92-dfda-4866-8ae6-8359b17538c9/image_40.png)
    
    General text actor settings.
    

### Text Layout Tools

You now need to use the **Text Layout Tools.**

-   With the text selected, click on the **Layout** button in the Details panel.
    
    ![Text layout settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73a82c3b-ea73-4c63-856d-419a1c83ec22/image_41.png)
    
    Text layout settings.
    

In this section, you can set a variety of common text properties. You are going to modify a few of them now. Begin with the **Alignment** options.

1.  You want to keep the horizontal alignment of your text left-justified, so do not change that option.
    
2.  Change the vertical alignment of each text line to be centered, so select the third option in the second row.
    

Kerning, Line Spacing, and Word Spacing are also all available here, but you aren’t going to use those now.

1.  Manually position Text\_Line1 and Text\_Line2 apart, so that they aren’t right on top of each other.
    
    You can also use the [**Grid Arrange** modifier](/documentation/en-us/unreal-engine/your-first-graphic-with-motion-design-in-unreal-engine#gridarrangemodifier) to position the text actors.
    
2.  Use the **Max Width** setting to ensure your text stays confined within the layout.
    
3.  Set the value so the text is retained within the borders of your graphics.
    
    You can reduce guessing the required Max Width value by typing a random number until you run off the edge of your layout. Then, you can refine the value until it restricts the text to within your desired bounds.
    
    ![Setting the Max Width value for your text layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd79ef8f-5bfe-4bd1-a4ef-be21720777a2/image_42.png)
    
    Setting the Max Width value for your text layout.
    

Here is a comparison of before and after setting the Max Width value to 1550 and adjusting the text position.

 ![Before](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/359ec0ef-dedb-4d2e-a561-334001b0af3d/image_43.png) ![After](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57c48347-53d5-434e-b09b-8b431013de53/image_44.png)

Before and after adjusting your text layout.

Make sure to leave space to the left of your bar for when you add the logo and show name.

### Grid Arrange Modifier

As mentioned above, another way to space out these two lines of text is to use the **Grid Arrange** modifier. To test it out:

1.  Select the Text\_Lines root actor and then right-click it.
    
2.  Navigate to the modifiers and select **Grid Arrange.**
    
3.  You will see the following interface:
    
    ![The Grid Arrange modifier settings for your text line actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8bac729-04cd-4b8b-bb4d-d16264b301a7/image_45.png)
    
    The Grid Arrange modifier settings for your text line actors.
    

The two settings that you need to learn to use here are the **Count** and **Spread.**

-   Set the **Count** to **(1, 2)** and the **Spread** to **(0.0, 31.0)**.

When you added the Grid Arrange modifier, the Motion Design Outliner changed. Both the eyeball icons for the editor and runtime visibility for the second actor were disabled. This is because the count for both width and height was set to 1, so these settings were no longer required to be visible.

![Text line actor arrangement after changing the Count and Spread settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/960df900-f6d1-4ca3-bc43-b8da4d03c8fc/image_46.png)

Text line actor arrangement after changing the Count and Spread settings.

This change arranged the text actors, spaced them out, and enabled their visibility in the Details panel. For more dynamic layouts, this sort of logic is necessary, but even for a comparatively more static layout like this tutorial project, it’s an effective tool.

You can disable a modifier by clicking the checkmark on either the entire modifier stack or on the individual modifier. This is useful for experimenting and debugging.

### Adding a Logo to the Layout

You will revisit the **Material Designer** here, but before you do, you need to add a piece of geometry to work with.

1.  From the **Toolbox**, add a **rectangle** from the 2D shapes.
    
2.  Double-click the rectangle, select it in your Motion Design Outliner, and create a **group** by pressing CTRL+G on your keyboard.
    
3.  Name the group **Show\_ID**, and name the newly-created rectangle **Logo**.
    
4.  Add two text actors to the group, and name them **Banner\_Line1** and **Banner\_Line2**. You are going to use these for part of your banner.
    
5.  Select the whole Show\_ID group, and drag it above the Text\_Lines group in your Motion Design Outliner.
    

Your Motion Design Outliner should now resemble the following image:

![The Motion Design Outliner after adding the logo actor and banner line text actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3ebc09b-cc14-442e-b0a4-b491939b4f79/image_47.png)

The Motion Design Outliner after adding the logo actor and banner line text actors.

With those elements in place, you can start building your logo. Click on the logo actor you just added and open the **Material Designer**. As a refresher, this means:

1.  Select the actor.
    
2.  Click the **Material** button.
    
3.  Set the **Material Type** to **Material Designer**. Your Material Designer tab now populates to the left of your Motion Design Outliner.
    
    -   This time, you don’t need to unlink the fill and mask. You will apply a texture here that has both channels, so it automatically uses them.
4.  Click the dropdown in the properties, and browse to the **UE\_Logo\_icon-only** asset in the **EDC\_Content** folder. You can also drag and drop the texture onto your canvas.
    
    Your result should resemble this image:
    
    ![Adding the UE_Logo_icon-only asset to the canvas](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58dbc917-97f4-4891-a109-901160b3762d/image_48.png)
    
    Adding the UE\_Logo\_icon-only asset to the canvas.
    
5.  Clamp the texture in the Material Designer property list for that layer.
    
    ![Enable the Clamp Texture setting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/182eaf66-ad83-4364-b1a6-71f1277709f5/image_49.png)
    
    Enable the Clamp Texture setting.
    

You can always check the key and fill of your level by selecting **Alpha** using the **Viewport Utility** **Toolbar**:

![Changing the Viewport to display the Alpha channel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3b77393-c0d6-4929-9d2f-bef3bd584631/image_50.png)

Changing the Viewport to display the Alpha channel.

The Viewport changes to show you a view that resembles this image:

![The Viewport displaying the Alpha channel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ea07dee-383d-482a-92f5-dd5ac1f53d4f/image_51.png)

The Viewport displaying the Alpha channel

Remember to switch the Viewport back to RGB before continuing to work.

Since the **Material Designer** defaults to translucent materials, you can move the logo into your layout, and it will be sorted correctly as long as it is near the top of the list.

1.  Configure the **Banner\_Line1** and **Banner\_Line2** text actors to have the same settings as the two text line actors you created previously.
    
2.  Select each banner line actor, and set them to **Translucent** with an **Opacity** of **1.0**:
    
    ![Banner line text actor style settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79547727-63cf-418e-b3f9-e1c8596d0a51/image_52.png)
    
    Banner line text actor style settings.
    
3.  Move the whole **Show\_ID** group, using either the handles in the Viewport or by using Transform settings under General in the Details panel, so that the logo is on the left side of your graphic. Your interim result will need further adjustment, and should resemble the following image:
    
    ![Work in progress with the banner icon and text needing transforms](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5cedfd91-8dda-46be-83d4-38728292a3e9/image_53.png)
    
    Work in progress with the banner icon and text needing transforms.
    
4.  Click on your logo to select it.
    

If you find selecting a logo is difficult, you might not have **Translucent Selection** enabled. Enable it by pressing the **T** key on your keyboard, and try selecting it again.

You can resize the logo in two ways:

-   Scaling the actual size by using the actor Transform settings under General in the Details panel.
-   Changing the scale value in the Material Designer with Clamp Texture enabled.

For now, resize it by using the actor Transform settings. You will use the Material Designer transforms method later to scale the UVs for animating.

-   In the Details panel, set the **scale** for all three axes to **0.55**.
    
    ![Scaling the logo actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc067d5e-5d38-4726-8470-2f821d87affe/image_54.png)
    
    Scaling the logo actor.
    

Next, you will work on your banner title.

1.  Select Banner\_Line1, and set the text to "The Daily".
    
2.  Set the layout settings for both Banner\_Line1 and Banner\_Line2 to the following:
    
    -   Alignment
        -   Horizontal: Left Justified
        -   Vertical: Centered
    -   Kerning, Line Spacing, and Word Spacing: 0
    -   Max Width, Max Height, Scale Proportionally: Disabled
    
    ![Banner line text actor layout settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17607e2c-83b7-4f62-87ec-b35b8ddacbdd/image_55.png)
    
    Banner line text actor layout settings.
    

You don't need the Max Width setting for the banner line text actors, because when you are working with the completed project you will not be able to edit them.

1.  Scale and reposition your text until your result resembles the following image:
    
    ![Banner icon and text actor after transforms](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7bb9278-c377-4cdd-8135-743acfb5cf41/image_56.png)
    
    Banner icon and text actor after transforms.
    
2.  Change the font of your text to something you like. The examples shown use Roboto Italic for both. Under the Typeface option you can choose between different font weights.
    

![Adjusting the font and typeface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0a0a51d-01fd-45c6-84f6-0341076ad4bf/image_57.png)

Adjusting the font and typeface.

### Viewport Features

The bottom right of the Viewport has several features. For the purposes of this tutorial, only two are relevant: Viewport Snapping and Viewport Guides.

![The bottom right of the Viewport, showing the icons for the features you can access](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94deb8ea-fa3f-4940-bfac-a3fef5bac1d6/image_58.png)

The bottom right of the Viewport, showing the icons for the features you can access.

#### Viewport Snapping

![Viewport snapping options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbaf7a7b-9e6e-41a5-8f90-72ee18df49f6/image_59.png)

Viewport snapping options.

To access Viewport snapping options, right-click on the magnet icon. Each of these is a toggle, and can be configured as you prefer.

-   For this example, right-click on the magnet icon and select **Screen & Guide**.

Left-clicking on the magnet icon disables whichever options you’ve selected.

The grid-and-magnet icon immediately to the right provides the option to snap to a grid of a specified size.

![Specifying a grid size for Viewport snapping](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/325362e3-5f9d-4b47-a1a2-93fd0291b14e/image_60.png)

Specifying a grid size for Viewport snapping.

#### Viewport Guides

To ensure everything is lined up the way you want, you can use Unreal Engine’s built-in guides system. If you click and drag from the rulers at the top and left side of your viewport, you can draw out guides that are useful when you want extra precision.

Drag out two guides to line up with the Unreal Engine logo. To remove a guide, double-click it.

![Using guidelines to arrange actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1972e4c7-49a4-4da2-8f2f-9186be7de4dc/image_61.png)

Using guidelines to arrange actors.

If you have a complex set of guides you want to save, click **Camera** in the Viewport, then select **Guide Presets > Save As**.

![Saving your guide preset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b21351c9-656d-4c3c-befa-b38831261054/image_62.png)

Saving your guide preset.

When you have a saved guide preset, additional options appear under Guide Presets. These are:

-   Active: Identifies which saved preset you are currently using.
-   Save: Save your current preset.
-   Save As: Save your current preset under a new name.
-   Reload: Reloads your current preset settings.
-   You can select a saved guide preset to populate it to the Viewport.

![The additional options available after you have saved a guide preset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95b8bbd9-2b9d-474e-b952-12fd52d91cf7/image_63.png)

The additional options available after you have saved a guide preset.

At this point, your project should resemble this image:

![The banner, text actors, and logo at this point in the tutorial](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7dd522d3-c297-49e7-b7bf-2abe4ad15111/image_64.png)

The banner, text actors, and logo at this point in the tutorial.

Save your work before continuing.

### Background Bar Visual Details

Before continuing, try adding a new texture to the background bar on your own, so that it is not a simple white bar, but instead has some additional detail to make it more visually interesting.

After you are done, read through the steps below to see how you did in comparison. If you had trouble, follow the instructions to modify your background bar.

1.  Select your white bar background, and click the **Material** button in the Details panel.
    
2.  Set the **Material Type** to **Material Designer**.
    
3.  Click **Edit with Material Designer.**
    
    ![The Edit with Material Designer button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2637b19a-588d-4cc4-981c-b4ed4e0d76c5/image_65.png)
    
    The Edit with Material Designer button.
    
4.  Add a texture with no alpha channel.
    
    ![Using the Add Layer menu to add a texture with no alpha channel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d92ab5c-90cf-4a47-83e8-1aaf7e4fd9b2/image_66.png)
    
    Using the Add Layer menu to add a texture with no alpha channel.
    
5.  Change the blend mode to **Multiply** and set your texture controls as follows:
    
    -   Select the texture dropdown, and choose the **linear gradient asset** labeled **2**.
    -   Enable **Clamp Texture**.
    -   Adjust your UV settings for **Offset**, **Rotation**, and **Scale**.
        -   Set Offset to -1.415.
        -   Set Rotation to -90.
        -   Set Scale so that the X value is 0.029, and the Y value is 1.0.
    -   Set the **opacity** to .87.
    
    ![The settings for the new texture with no alpha channel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6120611-75c3-4d80-b86b-b0bae79e31bf/image_67.png)
    
    The settings for the new texture with no alpha channel.
    

Your result should resemble the following image:

![The drop shadow result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1a8f5bf-3aaa-45fa-8ce1-aa25f19d6bc1/image_68.png)

The drop shadow result.

A drop shadow like this doesn’t need to be texture gradient-based, and can use normal scene lighting with a real-time shadow. It involves using duplicate geometry for the green backplate, and setting it to be opaque rather than translucent (translucent materials are incapable of casting shadows). Feel free to experiment!

## Animating your Design

Your objective is now to take what you’ve created, have it slide into view from offscreen, and stop in the center. You will also set up the off-animation, where the graphic will retract back off-screen to the left.

### Animate the Banner Graphic

First, select the entire graphic, and set a keyframe where you want it to land.

1.  Click on the root null actor. In this example, UE automatically named it Null Actor1.
    
    ![The banner graphic null actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b69a39a9-e098-4fbf-b93e-90bc75d4f263/image_69.png)
    
    The banner graphic null actor.
    
2.  In the **Sequencer** panel, advance the playhead to frame 30.
    
3.  Set a keyframe by pressing the **S key** on your keyboard, or by clicking the diamond icon to the right of the **Location** in the **Details** panel **General** settings.
    
    ![The set keyframe diamond icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ed3a58b-1ee0-41e3-9a9a-9225e68478a7/image_70.png)
    
    The set keyframe diamond icon.
    
4.  Click the keyframe to make a new selection section appear.
    
    ![Your new selection section after placing and clicking a keyframe](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a6342e9-768c-483a-b332-a250347b9334/image_71.png)
    
    Your new selection section after placing and clicking a keyframe.
    
5.  In Sequencer, click the pen icon to the left of the Magnet icon to find and enable **Auto-key**. This feature automatically places a keyframe any time you change the value of the track.
    
    ![The Auto-key feature in the menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5625dbf8-bacb-471a-821e-5f714acbf8d0/image_72.png)
    
    The Auto-key feature in the menu.
    
6.  Drag your playhead back to frame 0, and expand your Null Actor1 Transform Location settings in Sequencer:
    
    ![Null actor Transform Location settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e971b15-10a0-4671-b19b-51bd2684e85f/image_73.png)
    
    Null actor Transform Location settings.
    
7.  Change your keyframe **Y value** for the root null actor to **\-1500**. This takes the entire graphic off-screen, and creates a keyframe at that value, because you enabled Auto-key. You can also set that keyframe by changing the value in the Motion Design Outliner, and clicking the keyframe diamond icon.
    
8.  To have your animation ease into frame, click on the keyframe at the beginning of the move (frame 0 in this case). You should see a graph view in your selection section on the right.
    
    ![Graph view of your selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa312cdb-8e6c-4577-a361-20264f5295fd/image_74.png)
    
    Graph view of your selection.
    
9.  Clicking the **Selection** drop down menu shows you several options that will save you time when animating. For this example, select **Cubic**.
    
    ![The Cubic option in the Selection menu options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2be61ebb-7d9b-4bc5-b1be-8bfabe49ea0e/image_75.png) ![The Cubic option in the UI after selecting it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b535589-8bad-46bd-a052-c86634d467b9/image_76.png)
    
    The Cubic option in the Selection menu.
    
    You can click the **Play** button in Sequencer to see how each option looks.
    
10.  Next, add a pause to this animation so that you can start working on animating the off-animation. Move the playhead to frame 30, then right-click on it and select **Add Mark**. This creates a mark labeled **A**. You can change the label by right-clicking the A and changing the **Label** property. For now, A is fine as the label.
    
    ![Add a mark](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf02753b-c2e6-4c4b-b6cf-b14397dd0447/image_77.png)
    
    Add a mark.
    
    ![Your new mark](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/251ad606-a87e-4ab6-b360-79d1f7caca12/image_78.png)
    
    Your new mark.
    
11.  Click the button to open the **Sequence** tab, on the right side of the Sequencer panel.
    
    ![The Sequence tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/250b2ccc-8939-4b50-8312-f0c6b8fe8b1e/image_79.png)
    
    The Sequence tab.
    
12.  Click the **Role** dropdown, and select **Stop**.
    
    Marks can have several roles. These include:
    
    -   Mark (default, no function)
    -   Stop
    -   Pause
    -   Jump
    -   Reverse
    
    ![Mark role options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae781ec9-6017-44a5-ae6b-fc66c4e44473/image_80.png)
    
    Mark role options.
    
    Choosing Stop means the animation will stop at that point, until you choose to continue and start the off-animation you're going to make.
    
13.  Create another keyframe at the current Y location that you already have at frame 50. You can also press ENTER as a shortcut when the track is selected. You can also create the keyframe for your Sequence by clicking the add keyframe button associated with the Y setting in the null actor Transform Location settings, as shown below:
    
    ![The add keyframe button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c06ee6e-9773-413a-99d4-0eadea1e2e4b/image_81.png)
    
    The add keyframe button.
    
14.  Click the first keyframe, press and hold the ALT key, then drag the keyframe to approximately frame 90. This duplicates the original (offscreen) keyframe, and creates a suitable off-animation.
    
15.  Right-click the playhead at frame 70, then select **Set End Time** to remove the unnecessary sections of the timeline.
    

### Animate the Logo

With the bar now animated, your next step is to animate the Unreal Engine logo you created, using the **Material Designer.**

Animating properties using the **Material Designer** is no different than animating any other property; as long as you have a diamond icon next to the property, the workflow is almost identical.

1.  Start by selecting the Logo actor from the Motion Design Outliner.You’re going to give it a scale-down in addition to a fade-in using the layer opacity.
    
    ![Using opacity and scale to create an animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44abb026-408f-4f44-a5cf-94d40462ca74/image_82.png)
    
    Using opacity and scale to create an animation.
    
2.  Keyframe the opacity.
    
    -   Move the **Sequencer playhead** to frame **8**.
    -   Set the **Opacity** value to **0**.
    -   Click the keyframe diamond icon and your sequencer will move to that point. Give yourself about 20 frames for the reveal animation.
    
    ![Keyframing the opacity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28768767-8593-4701-b0cc-575a854181db/image_83.png)
    
    Keyframing the opacity.
    

The images below show the beginning and end values for your move animation. The key changes from beginning to end are as follows:

-   Opacity value 0.0 -> Opacity value 1.0
-   Scale
    -   X value 2.786 -> X value 1.0
    -   Y value 2.786 -> Y value 1.0

 ![Beginning move animation values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4139634-8e35-43bc-9e8b-0198bf66e000/image_84.png) ![End move animation values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5cafaed2-818f-4ef2-8427-c8324b35a0a6/image_85.png)

Beginning and end values for your move animation.

Your next task is animating the logo mask using the opacity tab.

![Using the opacity tab again](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6909226-26e2-499c-8062-1079627b63f1/image_86.png)

Using the opacity tab again.

-   Assign a texture for masking at the level of the entire material (rather than masking only a layer) from this tab.
    
    ![Assign a tearing texture to the material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6380e6d6-57fd-48f4-aa15-4fc831f55a2e/image_87.png)
    
    Assign a tearing texture to the material.
    

By adding this tearing texture to the material, no matter what you do in the underlying RGB tab, the texture will mask it.

What you can do here is limited only by your creativity, and we encourage experimenting with all of the ways you can use keyframes - there’s a huge variety!

## Rigging your Layout and Content with Remote Control

Now that you have designed and animated your graphic, the next step is rigging it to take advantage of **Remote Control**. Remote Control provides a way for you to expose a variety of properties so you can customize them from a central location.

Remote Control also offers a powerful system called **Behaviors**. Behaviors provide for logic operations that offer you even more rigging power. Do you want to switch between different styles (comprising several properties) by controlling the value of a single integer? The combination of Remote Control and Behaviors can help you do so.

-   Begin by selecting the **Remote Control** tab. You can find it right next to the Sequencer tab.
    
    ![Select the Remote Control tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dde1194e-a25a-40be-8a22-cd71945e8b92/image_88.png)
    
    Select the Remote Control tab.
    
-   You can also open it from the main menu under **Window** > **Remote Control Panel**.
    
    ![Open the Remote Control tab from the main menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f7f826b-051d-4692-a5db-91c680c4f20d/image_89.png)
    
    Open the Remote Control tab from the main menu.
    

Every Motion Design level comes equipped with a pre-linked remote control preset. When you open the panel, your interface will resemble the following image:

![The Remote Control panel in its initial state](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fdb86da-5978-40cb-84b1-9400879ccd38/image_90.png)

The Remote Control panel in its initial state.

The Remote Control panel provides a lot of powerful and potentially-complex functionality, but for this use case you only need to use the essential features. You are going to:

-   Control your two text lines.
-   Using a single control, change the text of the show’s branding, the show logo, and the color of the bar itself.

Begin with the two text lines.

-   To **Expose a Property** to **Remote Control**, go into your Motion Design Outliner and select the **Text\_Line\_1** actor.
-   When you look at the Details panel, you will see joystick icons. Navigate to the property settings buttons and click **Text**.

These joystick icons are widespread - Remote Control can control many parts of your project.

![Joystick icons indicate a setting you can control using the Remote Control feature](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0182d907-d362-4471-b00c-823caa6dbb85/image_91.png)

Joystick icons indicate a setting you can control using the Remote Control feature.

Your interface should now resemble the following image. Under the **Properties** column, your text string is exposed and you can edit it. Whatever change you make to the text string is immediately reflected in your viewport.

![Exposed text strings in the Properties column](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0005f8e-c408-4b44-8c85-2714f909680a/image_92.png)

Exposed text strings in the Properties column.

The **Property ID** column on the left will be important once you control the branding on the left side. Property ID is a way to group up your controls that is useful when you have many exposed properties you want to organize. It is a part of the workflow when you want to set multiple properties from a single source, which this tutorial covers later.

The column to the right of **Properties** is where you can add **Controllers** to your setup. **Controllers** provide a simpler, operator-friendly interface.

-   To create a controller for the property you exposed, click and drag the group into the **Controller** column. Your interface should resemble the following image:
    
    ![Create a controller for an exposed property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bae01ce9-61a1-4c11-b171-100e97eb94f3/image_93.png)
    
    Create a controller for an exposed property.
    

Organizing your controllers is important for making your rigging accessible to an operator, and labeling your fields can help you do so. You can edit the Controller ID and Description fields by double-clicking them, then entering a new alphanumeric string as the value. By default, the Controller ID value is **Text**.

1.  Change the Controller ID label to **B100**.
    
2.  Set the Description to **Text - Line 1**.
    

Your interface should now resemble the following image:

![After changing the Controller ID and Description text fields](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b372412f-1d4e-42b5-ac04-aa8cb493dc36/image_94.png)

After changing the Controller ID and Description text fields.

-   Repeat the process for your Line 2 text.

Alternatively, instead of repeating the entire process, you can achieve the same result by a more complex but also more efficient means.

-   Delete the Text\_Line\_2 actor.
-   Copy and paste the Text\_Line\_1 actor.
-   Rename the duplicate actor to Text\_Line\_2.

By doing so, a **Tracker Component** is added to the duplicate actor. This process duplicated the actor, and exposed the same properties to Remote Control. The only additional steps to this workflow you need to do are:

-   Check your grid modifier is still spacing out the lines appropriately.
-   Drag the new actor's exposed group from your **Properties** panel into your **Controller** column.

Your interface should resemble the following image:

![Your interface after creating a second Text_Line actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/012b8f78-cba9-44f6-ad92-1aeabd03bebc/image_95.png)

Your interface after creating a second Text\_Line actor.

-   Test out your remote-controlled properties by changing their values in your Controller Column under the **Input** field.

If everything is configured correctly, the effects of your changes will show immediately. Notice that when you dragged your text from the **Properties** panel into the **Controller,** a **Bind Behavior** was added (you can see it in the above screenshot). There are several of these Behaviors - all of which we designed to offer additional automation and logic to simplify your workflow.

With that in mind, you will rig up the logic that will drive the items on the left side of the bar, using the **Conditional Behavior** in tandem with the **Property ID** system.

-   Start by exposing the properties you will need to work with. Using the same process you just learned with the Text\_Line actors, expose the following properties:

#### The logo

1.  Click on the logo actor in your Motion Design Outliner and open the Material Designer.
    
    ![The button to open the Material Designer associated with your logo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bb1b493-0199-4185-a8de-92d1695e8753/image_96.png)
    
    The button to open the Material Designer associated with your logo.
    
2.  Clicking the Remote Control button associated with the logo texture adds a texture controller to your Remote Control panel.
    
3.  In your Remote Control Properties column, highlight the newly exposed texture. Set your property ID (currently listed as **None**) to **100.Logo**.
    

100 is the most important part here, but you can use a period to further describe the property in case you have multiple images or colors that you want to label and control.

#### The Show Title text

1.  Expose the text fields that comprise **The Daily** and **Hotfix** separately.
    
2.  Assign those to property IDs **100.ShowTitleLine1** and **100.ShowTitleLine2** respectively. Your interface should resemble the following image:
    

![Assigning property IDs to the text fields](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d89a38b2-de00-4415-9a78-6e9d14e8ddc5/image_97.png)

Assigning property IDs to the text fields.

#### The Background Bar Color

1.  Click on your BG\_Main actor, or select it in the Motion Design Outliner. If it didn’t automatically open, go into the Material Designer that you already set up.
    
2.  Click on the green bottom layer, and expand your expose options by clicking the **More (⋮)** menu.
    
    ![The More menu options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4480ea0b-5dbb-4c56-93ed-d0bf6cea0c9e/image_98.png)
    
    The More menu options.
    
3.  Expose the property, and assign it the property ID **100.Background**.
    

Your interface should now resemble this image:

![Your interface after exposing all the properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dee15cc-c681-48af-9620-457a4a59109b/image_99.png)

Your interface after exposing all the properties.

Now that your exposed properties are set up, the next part is to set up controlling several properties from one integer.

1.  Under the **Controller** column, click on the **plus sign** on the left side, and select **Integer**.
    
    ![Controller value options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bbb99e62-2f31-4607-a5dc-f7b6841debfe/image_100.png)
    
    Controller value options.
    
2.  Label the Controller ID **A100** for organization purposes.
    
3.  Use the drag handle to the left of the controller ID field for each line to reorder your list manually.
    
4.  Change the description for this property to read **0 = Show 1** | **1=Show 2**.
    
5.  Select the controller, and click on the plus sign in the **Behavior** column to manually add a behavior.
    
6.  Select **Conditional**, and click on the property.
    
    ![Add the Conditional Behavior](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2615de66-5c39-4a0b-a33c-b4370fa195b9/image_101.png)
    
    Add the Conditional Behavior.
    
    With this selected, you can choose how to evaluate what you are going to add, but leave it set to **\=**.
    
7.  Click the **plus** button next to Actions.
    
    ![Click the plus button at the top of the Actions column to add a new action](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc1a7c1e-72cf-42b8-a84b-9ffcedd9ddd7/image_102.png)
    
    Click the plus button at the top of the Actions column to add a new action.
    
8.  From the menu, select **Add specific ID action** \> **ID: 100**, as shown in the following image:
    
    ![Select a specific ID action using ID: 100](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11df3a51-facf-4229-849a-2b482157a70f/image_103.png)
    
    Select a specific ID action using ID: 100.
    

This collects all the properties with the 100 prefix and adds them all to the Actions column at the same time.

![All the properties with the 100 prefix collected together in the Actions column](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d4e3b30-54d8-4992-9c01-c2018ff09da4/image_104.png)

All the properties with the 100 prefix collected together in the Actions column.

Now, when you set that value to **0** in the **Remote Control** controller, it sets all of those values to whichever values you’ve set up for the selected properties. In this case, make sure you set it so that 0 = the Unreal Logo and the green bar.

1.  Right-click on the group of properties, and choose **Duplicate**.
    
2.  Double-click the **Condition** field of the duplicate group, and set the value to 1.
    

Here’s an example of something you can make using this workflow.

![A completed example using the workflow described here](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8994e27-df90-4291-a5ec-af30bfa8d009/image_105.png)

A completed example using the workflow described here.

Once this is properly set up, when you press 0, you will see the first banner theme, and when you press 1, you will see the other banner theme.

## Using Storm Sync to Package Your Content

### Exporting a .spak File

You can export your content into a lightweight `.spak` file. This is useful in situations where you’re backing up content without source control, or handing a colleague a full scene and all of its dependent files. Here is how to use this feature for your project.

1.  Open the level that you’ve been working on. The example shown here is called `Demo_Working_Project`.
    
2.  Right-click in the viewport and select **Export**:
    
    ![Exporting your project to a .spak file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5aa1ca80-cb09-4811-b94f-0d3085a76e86/image_106.png)
    
    Exporting your project to a .spak file.
    
    UE then auto-collects and displays a full list of required files.
    
    ![An auto-collected list of files for export](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa235780-061f-48f7-89ce-fd101a19d5ad/image_107.png)
    
    An auto-collected list of files for export.
    
3.  Click on **Next**. This sends you to an export option screen where you can name your `.spak` file.
    
    ![Name your exported file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78ee264f-fea1-4f7e-8f65-064887abe195/image_108.png)
    
    Name your exported file.
    
4.  Name your file, and click **Finish**. You should see a message on the lower right that shows you where your file was saved.
    

### Importing a .spak File

To import your `.spak` file, drag the file from the directory where you exported it and drop it into your **Content Browser.** You will be presented with a screen to verify the contents of the file before importing it. If UE detects changes between the files in the `.spak` file and what you have in your project, it lets you know, and imports what has changed. If it’s a brand new set of assets, that change list shows everything.

Here is an example of what the list will look like if you don’t already have any of the files:

![The changelist you will see when importing a project from a .spak file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77ac666e-d313-4252-9e79-8453cf599ae8/image_109.png)

The changelist you will see when importing a project from a .spak file.

Click **Import** to populate your Content Browser with the necessary files.

## Rundown Tool UI Overview

Before starting this section, we strongly recommend a two-monitor setup. This will mean you can use one monitor to operate as an output monitor, while the other functions as a place to operate your graphics. Without a two-monitor setup, you will have difficulty following this tutorial.

With everything set up, all that remains is for you to play out your customized content using the **Rundown** tool.

To begin, create a new Rundown by right-clicking in your Content Browser, and selecting **Motion Design > Motion Design Rundown**.

![Create a new Motion Design Rundown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/850bfab0-dfb0-4f00-9efd-aafc21bb6c74/image_110.png)

Create a new Motion Design Rundown.

You can use the **Rundown** tool to add your levels to a central location and create pages that provide a way for you to rapidly generate content to be played out live. The following workflow will serve as a surface-level, fully local overview of the tool for simple playback.

With the right setup, you can have multiple instances of UE running on a network, where a discoverable instance of UE hosting the project you want to play can be controlled by the UE instance running the Rundown and the Rundown’s preview capability.

![The Motion Design Rundown interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfaf0820-1f17-4203-83e3-6bdd9b053a6e/image_111.png)

The Motion Design Rundown interface.

Here are some aspects of the Rundown tool interface that are key to this tutorial:

1.  Template List: All imported levels are located here, and you can import them by dragging the level from the **Content Browser**.
    
2.  Playback Controls: You can control selected pages from this panel. Taking in/out, continuing, and taking the next item on the Rundown can all be done here. These playback controls refer strictly to actually taking the graphic to air. You can preview before taking by using the Page Preview, which is addressed in item 6.
    
3.  Page List: Dragging any item from the Template List results in creating a page. You can take pages to specific, designated channels. For the purpose of this tutorial, leave it on Channel\_0.
    
4.  Page Details: You can set individual page properties here, such as a text line, integer value, and so on. You can also modify the Page ID and page name from here.
    
5.  Toolbar: The toolbar contains several commonly-used controls, such as saving, adding/removing a new template or page, or setting broadcast settings. There is also a quick access button on the right to Start All Channels and effectively go "on air."
    
6.  Page Preview: Similar to the Playback Controls referenced above, operators can preview the content of a selected page before taking the graphic to air. You can also use **Preview Next** to review the complete list of pages.
    

## Using the Rundown Tool

Begin by adding your level to the Rundown.

1.  Click **Add Template** on the top row, or drag your level directly into the template list.
    
2.  Double-click the **Preview In** button to see what you’re working with.
    

Your result should resemble the following image:

![Previewing your page in the Rundown tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63b60c83-964e-410a-b39f-226c287a1027/image_112.png)

Previewing your page in the Rundown tool.

Previewing doesn’t mean that you have played your graphic out live on air. You’ll notice that the Take In / Take Out buttons are still grayed out (list item 2 in the interface description).

That is because you now need to drag that template into your **Page List.**

1.  Drag the template into your Page List, then click **Continue** on the page preview panel. If everything is functioning correctly, you should see the off-animation that you created animate the graphic away.
    
2.  With your page selected in your Rundown, modify some of the page details.
    
    1.  Change the B100 and B200 values to say something other than the default text.
        
    2.  Click **Preview In** again.
        

Your result should resemble the following image:

![Modifying your page's text in the preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/582d5709-5f3c-4ddc-8e73-e864e04c3bb7/image_113.png)

Modifying your page's text in the preview.

1.  Right-click your 0001 page and select **Duplicate**. You are going to make a variation of that page to further experiment with the controls.
    
2.  On the duplicate page, set the value of your A100 property in your page details to 1 instead of 0. With the logic you have in place, the result of using Preview In for your graphic should resemble the following image:
    
    ![Creating a duplicate page](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b82e9f25-53fb-4352-b764-48ebaad67a3d/image_114.png)
    
    Creating a duplicate page.
    

Now that you have your pages set up and functioning, briefly explore the output of your graphic. For simplicity, this tutorial will focus on a single machine operation where operation and output occur on the same engine.

-   Open your **Broadcast Editor** by clicking the Broadcast button:
    
    ![Open the Broadcast Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06dcecde-27a2-4a65-9e58-dc6ed823b468/image_115.png)
    
    Open the Broadcast Editor.
    

The **Broadcast** window now appears:

![The Broadcast window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/626085e5-3520-44d6-8848-ce6518f0275d/image_116.png)

The Broadcast window.

Under the **Output Devices** list on the right side, you should see the displays that you have available

As mentioned previously, you need more than one display.

1.  Click the display that you want to output to, and drag it into the Channel\_0 viewport. Your result should resemble the following image:
    
    ![The Channel_0 viewport after you drag in your output display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7bb045d-fa07-46bc-86e6-8f71d03c6104/image_117.png)
    
    The Channel\_0 viewport after you drag in your output display.
    
2.  With your output set up, click the **Start All Channels** button.
    
    ![The Start All Channels button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4fee265f-ef0f-47e3-9a1c-64cb0e4dd523/image_118.png)
    
    The Start All Channels button.
    

The screen that you designated for that channel will turn black and show no further activity until you go back to your **Rundown.**

1.  For the purposes of this tutorial, designate the monitor that just went black your **Program display**, and designate the other monitor your **Rundown display**.
    
2.  You are currently **Live**. Look at your Rundown display, and click **Preview In** on one of your pages. It will play out on the preview viewport. Assuming the preview looks correct, click **Take In** on the Rundown display. Your previously dark Program display now shows your lower third graphic.
    

The following image is a composite showing what the display on your two monitors should resemble:

![Your Rundown display on the left, and your Program display on the right](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04919ce5-9a08-4984-830c-b0bd15a6489b/image_119.png)

Your Rundown display on the left, and your Program display on the right.

-   While you are actively outputting to your Program display, select your second page from your Rundown and **Preview In** that page.
    
    ![Preview In the Rundown display without changing the Program display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f474905a-82f7-4b1e-ae99-42071c758720/image_120.png)
    
    Preview In the Rundown display without changing the Program display.
    

You are now previewing the next page while the Live page is actively displaying.

-   Click **Continue** here:
    
    ![The Continue button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8562ca9f-bd02-4276-b187-e535b05334e1/image_121.png)
    
    The Continue button.
    

The graphic on your Program display animates the off-animation, and leaves the display.

-   With your 002 page selected, click **Take In** and your blue lower third graphic will animate to move on to the Program display.

Now that your graphics are set up, play around with the options here to learn how to operate your graphics.

You can call up pages from your page list by using your number pad. CTRL+Enter activates Preview In for that page, and Shift+Enter activates Take In to send that page to your Program display. Hover over the other buttons to see their respective shortcuts.
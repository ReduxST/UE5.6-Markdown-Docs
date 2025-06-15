# Real-Time Compositing Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/real-time-compositing-quick-start-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/real-time-compositing-quick-start-for-unreal-engine)  
**Processed:** 2025-06-14 16:45:49

---

The most basic of composites is the three piece comp: a CG background, a middle media (video) plate, and a CG foreground. In this topic, we'll demonstrate how to use composure to build a basic three piece comp.

## 1 - Load Composure

### Steps

1.  Enable the **Composure Plugin**.
    
    ![Enable plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f020676-6d8e-42f2-9351-47ba742c8ecc/01-enable-plugin_ue5.gif)
2.  Open the compositing tree panel (listed as **Composure Compositing** in the **Window** menu under **Virtual Production** section).
    
    ![Open the compositing tree panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc0c84c5-4cd9-45f1-9288-67101777dd20/02-compositing-tree-panel_ue5.gif)

## 2 - Add a Root Comp Element

Next, add a root Element to the compositing tree. 

### Steps

1.  Right-click in the compositing tree panel, and select **Create New Comp** from the menu. Then, select **Empty Comp Shot** from the **Pick a Comp Class** dialog. 
    
    ![Create New Comp](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc0f78a2-9d98-4b78-a750-e4cb9b0e8535/03-create-new-comp_ue5.gif)
    
    This Element will not render anything immediately as it represents your final composite. This Element will be responsible for combining all of the other Elements.
    
    For portability, make sure your Elements are added to their own sub-level. Since Elements are level actors, this lets you load your compositing tree in other maps.
    

## 3 - Add a Media/Video Element

Once you have a top-level comp Element, you need to add child Elements. Child Elements feed into their parent (for compositing).

### Steps

1.  Add a **Media Plate** to the comp tree.  
    Right-click on the comp Element in the compositing tree panel, and then select **Add Layer Element** from the menu. When prompted to pick a Element type, select **Media Plate**.
    
    ![Add a Media Plate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0057d39b-4272-487b-8b0a-f5fa47f8534f/04-add-media-plate_ue5.gif)
    
    Without a media source, the **Media Plate Element** will be blank. You can set up a default still image (like we have in the GIF above), in your game config file: `[/Script/Composure.ComposureGameSettings] StaticVideoPlateDebugImage="/Game/Path/To/My/TextureAsset"`
    
2.  Set your **Media Source**.   
    By default, your media Element will not be connected to a media source (such as a streaming video). You can apply a media texture to act as an input In the Element's details. Select the new media Element. Then, in the details panel, find the **Media Source** section (under **Composure**→**Inputs**). The **MediaSource** texture property will be empty.
    
    ![Set a Media Source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67c27f2b-2c53-4a53-a68d-3b98bed76aa3/05-media-plate-source_ue5.gif)
    
    Feeding a live video feed into the engine via capture card produces a **Media Texture**. So you hook that into the compositing system in the exact same way. For more details on how to set that up, look into using capture cards with Media Bundles in Unreal Engine.
    
3.  Configure the **Chroma Key Color**.  
    The **Media Plate** Element has a set of predefined transform Passes on it. Those Passes are for adjusting the media image before it gets composited. The first of those passes is for **Chroma Keying**. To pick a **Chroma Key Color**, under **Transform Passes** navigate to the keying Pass, then find the one named **Chroma Keying**. After expanding **Chroma Keying**, you'll find a **Key Colors** property. Add a new **Key Color** using the picker button next to the color box.
    
    ![Configure the Chroma Key Color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2b7af41-7bb3-41c3-a2c8-1492065bc287/06-chroma-key-color_ue5.gif)
    
    Clicking the picker button will open up a large picker window to enable you to select a color. To pick a color, click the mouse anywhere on the image to sample that pixel. Click and dragging will average the sampled pixels together, so you can get a more homogenous chroma color. Once you're happy with the result, click **Accept**.
    
    You can add as many key colors as you wish. This helps when you have multiple shades of green across the backdrop, and keying one color isn't enough. However, for each **Key Color** you add, the Element performs a full Pass, running the keying material once for each color in the list. This may be a performance concern for some.
    
    Along with the key color, there are many other settings that can be adjusted to perfect the keying. Review the **Material Parameters** section inside the Pass.
    
    ![Material Parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c74356e7-d4fd-472a-a0f2-8ff49af48729/07-mat-param-devignette_ue5.gif)
    
    The built-in keyer expects the image to be in linear color space. If your image is coming in in a different color format (such as logC), then you will have to add a colorspace transform before the keying is done. Alternatively, you can replace the keyer with a material of your own.
    
    In addition to the **Chroma Keying Pass**, there is a separate **Despill Pass** for removing green bounce on your subject. For more details on chroma keying and despill, see the blog post [here](https://www.unrealengine.com/en-US/tech-blog/setting-up-a-chroma-key-material-in-ue4).
    
4.  Preview the Results.  
    Sometimes it's hard to get a sense of how good of a job your keyer is doing. For every Element, you can open up a larger preview window, and look at individual color channels for that image.
    
    ![Preview the Results](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eadeff32-21ce-4f38-920e-d275b014417f/08-preview-results_ue5.gif)
    
    The **Key Picker** window and the **Level Editor** preview pane also both have this functionality.
    
    At this point in the process, don't worry if it's not perfect. You can always adjust it later when you preview the whole composited scene.
    

## 4 - Add CG Elements

Similar to adding the media Element, we want to add Elements for foreground and background layers.

### Steps

1.  Add a **CG Layer**.  
    Right-click on the top-level comp Element in the tree panel, and then select **Add Layer Element** from the menu and pick **CG Layer**.
    
    ![Add a CG Layer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecb8cf44-2776-4251-9a17-068896401cad/09-add-cg-layer_ue5.gif)
    
    Add two CG Elements – one for foreground objects, another for background objects, and name them appropriately: fg\_element, and bg\_element.
    
2.  Link to a Scene Camera.  
    CG Elements requires a camera in the world to cue off of – the camera tells them the viewpoint to render from. Without a camera in your scene, CG Elements will display a "Missing Camera" warning message. To resolve this, simply add a camera actor to your scene.
    
    ![Add Cine Camera Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9618153b-263d-49ef-a4dc-efaab5b9a44e/10-cine-camera-actor_ue5.gif)
    
    If there are multiple cameras in your scene, you can specify which one to reference in the Element's details (under **Input**, look for **Camera Source**).
    
3.  Setup Actor Layers.  
    Now that you have two CG Elements (one for foreground, and one for background), you need to specify what scene actors should be rendered to each.  
    For this, we will leverage the level editor's layer system. In our test scene, we've added some basic primitives – a cube, a cone, a sphere, and a cylinder. In this case, the cone and cylinder are in the foreground, and everything else in the background. To start, create an editor layer for just the cone and cylinder.
    
    ![Add Actor Layers](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e2df104-d81c-453c-9e45-07e16974155b/11-layer-actor_ue5.gif)
    
    Now, in the foreground Element (fg\_element), find the **Capture Actors** property (under **Composure**→**Inputs**), and add an entry to it. The **Capture Actors** list specifies what the CG Element should render.
    
    ![Capture Actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47fe1b2b-fc9b-4087-bdc0-ad72d4764ba8/12-fg-layer-actors_ue5.gif)
    
    In the new **Capture Actors** entry, set the **ActorSet** property to the **ConeAndCylinder** layer that we created earlier. Because the entry's **InclusionType** is set to **Include**, it will render only those actors.
    
    | Property | Description |
    | --- | --- |
    | **Include** | Render only the actors in the specified layer. |
    | **Exclude** | Render everything except the actors in the specified layer. |
    
    You can add as many **Capture Actor** layers to the Element as you wish. You can mix/match includes and excludes.  
    For the background Element, we want everything except the **ConeAndCylinder** layer. So we use the same layer, but switch the **InclusionType** to **Exclude**.
    
    For your CG renders to have the proper opacity for compositing, you will need to set **Enable alpha channel support in post processing** to **Linear color space only enable** in project settings:
    
    Click image to expand
    

## 5 - Setup a Compositing Material

Now that you have four Elements (the top-level comp, a **Media Plate**, and two CG Elements), you can layer them all to produce your comp. The top-level comp Element is responsible for merging all of the other Elements. We're going to add a transform Pass to the comp Element and set it up to composite the other three layers.

![Compositing Elements](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10d14610-d09b-4049-a35e-d2690ae4d1fd/14-composure-elements_ue5.png)

### Steps

1.  Add a Comp Transform Pass.  
    Select the comp Element, and then in details find the **Transform Passes** property. Add an entry to the **Transform Passes** list. The default entry is **Custom Material Pass**, which is what we want.
    
    ![Add a Comp Transform Pass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6075a914-4573-4bac-88fb-1cfdcdb854dd/15-comp-transform-pass_ue5.gif)
2.  Create a Comp Material.
    
    -   The new Pass expects a material for rendering. Expand the Pass's details and create a new material for its **Material** property.
        
        ![Create a New Comp Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c358b41d-7508-4642-b5cc-cd9929c6d014/16-create-composure-material.gif)
    -   Set the new material to be a **Post Process** material – this ensures that you're outputting the result to the correct channel.
        
        ![Set a Post Process](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddfcacb5-14df-4a78-8e02-261fbc54128d/17-post-process-material_ue5.gif)
    -   In the new material, we need texture samplers for each of the three sub-Elements. To do this, create three texture sampler parameters and name them to match the child Elements. These texture params will get automatically filled out with the results from the three child Elements. To combine the three Elements all you need are a couple **Over** nodes. The **Over** node takes **input A** and layers it over **input B**, using **input** **A**'s alpha. We want to sandwich the media plate between our two CG layers.
        
        ![Create texture sampler parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/728f5781-af91-4aa8-a4a6-453f88c22443/18-new-sub-elements_ue5.gif)
3.  -   Set one Over node so the media plate (**A**) renders over the bg Element (**B**).
        
    -   Next, use the result from that Over node and plug it into **B** on another Over node.
        
    -   Lastly, put the **fg** Element on top by plugging it into **A** on that second Over node.
        
    -   The second Over node's output should be plugged into the material's **Emissive Color** channel.
        
    -   Save and apply the material.
        

Review your results back in the compositing window. You should have a single image with all three Elements composited together.

The Over node expects a **float4** input, so use the texture sampler's **RGBA** output pin, not its top **RGB** pin.

The Over node uses input **A**'s alpha for Blending. By default, projects are not set up to pipe alpha data through the post process pipeline. So for the CG layers to work, you have to enable this project setting.

Click image to expand

## 6 - Output Your Comp

If you're happy previewing your comp in the editor, then ignore this last step. However, if you want to route the result of your comp to disk or run it out through a capture card, then you will want to use an **Output Pass**.

In this example, we want our comp to be broadcast via a capture card.

### Steps

1.  In the top-level comp Element's details, find the **Outputs** property and add an entry to that list. The default is **Media Capture**, which is what we want.
    
    ![Find the Outputs Property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09314569-41f7-4b64-9de7-7105dd8c2d0f/20-composure-output_ue5.gif)
2.  In the new output Pass, you will need to specify the target in the Pass's **Capture Output** property, and create a new asset for it.
    
    ![Specify the Target](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56ff90fd-7fb6-41ff-8518-b7742b3680fc/21-composure-output-aja_ue5.gif)
    
    Configure this asset for your capture target, and you should be all set. The comp Element should start broadcasting.
    

### Using Sequencer

Alternatively, you can render out comps and AOVs with [Sequencer](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview), our in-engine cinematic editor. For more information, see [Real-Time Compositing with Sequencer](/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine). 

![Using with Sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbb6bb0c-1814-4d3f-bce9-6aef29c4da25/22-composure-sequencer.gif)
# Movie Render Graph Nodes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/movie-render-graph-nodes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/movie-render-graph-nodes-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:15

---

## Globals

Most nodes can be applied to the Globals chain, but some nodes can only be connected to the Globals chain. These settings can only be set **once per render job** and not per layer.

Most of these are present in the Movie Render Queue Preset in previous versions of Unreal Engine. For more information, see the [Cinematic Rendering Image Quality Settings in Unreal Engine](/documentation/en-us/unreal-engine/cinematic-render-settings-and-formats-in-unreal-engine) documentation.

Here you can reference a list of some of the Global Nodes you can use in the Movie Render Graph, and a description of the functionality:

| Node | Description |
| --- | --- |
| **Warm Up Settings** | The warm-up settings have been improved and streamlined by now only having to set one number and whether or not you would like to emulate motion blur. |
| **Global Game Overrides** | This matches the Game Overrides section in the Legacy MRQ UI. This node can be used to increase the rendering quality in various ways at render time in an effort to keep the editor fast to work in. If you are noticing differences between the editor viewport and MRQ renders consider disconnecting/disabling this node to troubleshoot. |
| **Global Output Settings** | 
The Output setting controls your output file's directory, frame rate, and output resolution. File name control is under the File Type node in Movie Render Graph. The **Global Output Settings** node also contains a **Timecode** category with two properties:

-   **Custom Timecode Start**: By default, Movie Render Queue will include whatever timecode data it receives from the Level Sequence being rendered. However, you can override it by selecting **Custom Timecode Start**.
-   **Use DF Timecode if 29.97 fps**: **Drop-frame (DF)** timecode is only applicable when the frame rate is `29.97`. The system defaults to using it when the configuration uses `29.97`. However, if you disable this property, you can choose not use the DF timecode.



 |
| **Sampling Method** | Set your Temporal Sample count here. Temporal Samples can only be applied per render job. Spatial Samples can be applied per layer and are located in the Render Type node. |
| **Camera Settings** | The Camera setting contains settings for the shutter timing and you can specify an overscan percentage to render extra pixels around the edges of your images. |
| **Debug Settings** | This node will allow you to capture Unreal Insights Traces right from Movie Render Queue as well as send the frames to Render Doc. |
| **Apply CVar Preset** | This node will allow you to apply a CVar Preset at render time. You can view a list of the applied presets in the node's **Details** panel. Additionally you can override an individual preset by right-clicking the preset from the list, and selecting the **Override with Set Console Variable Node** option. After selecting the option, a new **Set Console Variable** node will be added to the graph and connected to the **Apply Console Variable Preset** node. It is set to adjust the selected Console Variable and the value from the Preset asset. You can also expose each individual preset by right-clicking the Apply Console Variable Prest node in the graph, and toggling the checkbox adjacent to the specific preset. Additionally you can manually adjust Console Variables from the **Queue** window. |
| **Set CVar Value** | This node will allow you to set a console variable at render time. |
| **Command Line Encoder** | The Command Line Encoder can be used to create your own output format from third-party software, such as FFmpeg. This setting requires an encoder executable and settings to be enabled in your Project Settings. |
| **Execute Script** | The Execute Script is a node that allows you to select a predefined Python UClass that can override pre/post shot and job callbacks. This setting requires creating a specialized class derived from MovieGraphScriptBase. |
| **Set Start/End Console Commands** | You can use this node to add and remove Start and End Console Commands for a given render. |
| **Object IDs** | This node assigns unique IDs to specific objects, so that your render can exclude or include certain objects using that unique ID. |

## Render Layer Nodes

The existence of the **Render Layer node** in your chain will signal for the Movie Render Graph to render this chain. Otherwise, logic will just be executed. The Render Layer Node is useful in Subgraphs or pipeline tools to better control the outcome of your render.

![Render Layer node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d44d443-9ea2-4409-a991-f36b80f053f3/image_0.png "render layer node")

Along with disconnecting the chain from the Outputs tab, you can disable a render in the chain by right-mouse-clicking over the node and selecting the **Disable** property from the context menu.

![Disable Render Layer node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1e0c790-eb00-4e48-b29f-4e74d9de0cae/image_1.png "disable render layer node")

## Per-Layer Nodes

The following nodes are usable per-layer when using the Movie Render Graph.

### Render Type Nodes

You can use both the **Path Traced** and **Deferred** renderer nodes in the Movie Render Graph. You can define which render path you choose by connecting the correlating node in your chain. This can be chosen for each render layer. This means you can have one layer take the Deferred render path and one take the Path Traced render path in the same Render Graph.

![Graph showing Deferred and Path Traced Renderer nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da2872b5-4e53-4c35-bb19-4aef6293665b/image_2.png "deferred and path traced renderer nodes")

#### Deferred Renderer

In the **Deferred Renderer** node you will find many parameters that can override Editor settings at render time, as well as set properties that must apply to all Render Layers. Below is a list of the properties you can use with the Deferred Renderer node.

| Property |
| --- |
| **Spatial Sample Count** |
| **AntiAliasing Method** |
| **Disable Tone Curve** |
| **Allow OCIO** |
| **View Index Mode** |
| 
**Additional Post Process Materials**

Enabling the **Use High Precision (32 bit) Output** property will render your image with a 32-bit color output on a per-PPM basis. PPMs also have a **Name** property, which you can use to define the output name to a friendly, customizable string.



 |
| **Render Show Flags** |

#### Path Traced Renderer

In the **Path Traced Renderer** node you will find many parameters that can override Editor settings at render time. Below is a list of the properties you can use with the Path Traced Renderer node.

| Property |
| --- |
| **Spatial Sample Count** |
| **Denoiser** |
| **Disable Tone Curve** |
| **Allow OCIO** |
| 
**Additional Post Process Materials**

Enabling the **Use High Precision (32 bit) Output** property will render your image with a 32-bit color output on a per-PPM basis. PPMs also have a **Name** property, which you can use to define the output name to a friendly, customizable string.



 |
| **Render Show Flags** |
| **Reference Motion Blur** |

The Path Traced Renderer node also supports the Temporal Denoiser (also known as NFOR). When using the Path Traced Renderer node, the default option is still **Spatial** but you can toggle the Temporal Denoiser using the property in the node's **Details** panel. After enabling the Temporal Denoiser property you can then use the **Frame Count** property to set the number of frames to consider when performing temporal denoising. Higher frame counts will generally result in increased render time.

### Output File Type Nodes

In the Movie Render Graph, you can output using many file types. You can pick the file output type for each render chain.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bfbf38d8-e062-423c-b90f-a2c5ab0a9e3a/image_3.png)

The Movie Render Graph can use the **Output File Type** node to output the following file types.

-   WAV (This can only be applied Globally.)
    
-   PNG
    
-   JPG
    
-   BMP
    
-   EXR
    
-   EXR Multilayer (This can only be applied Globally. The first output will be in the RGBA. Any additional outputs will be listed in their own named layer.)
    

You can define **OpenColorIO (OCIO)** configurations and compression type where applicable. You can also define file naming in the **Output File Type** node's Details panel.

![Details panel for Output File Type node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6109faae-277a-4462-952e-a10cc30c22ba/image_4.png "output file type node's details panel")

You can also state the **File Name** here. The Movie Render Graph defaults to using the **{sequence\_name}.{layer\_name}.{frame\_number}** tokens. Tokens can be used to dictate frame name as well as folder name in the **Global Output Settings** node.

![File Name Format property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b520dcb8-987a-4c1c-a73a-446e1063851d/image_5.png "file name format property")

If you clear the File Name Format property you can then select a different File Name Format from the drop-down menu.

![Select a different File Name Format](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76f2d85c-a526-4c8b-a537-e0ce89594cd7/image_6.png "select a new file name format")

Additionally you can output **Apple ProRes Movie** and **Avid DNxHR Movie** file using their respective **Output Type** nodes. These two nodes are unique to other Output Type nodes, including an additional **Quality** property that you can use to set the options for each codec. You can select from the following Quality options.

**Apple ProRes Movie**

-   Apple ProRes 422 Proxy
-   Apple ProRes 422 LT (Default)
-   Apple ProRes 422
-   Apple ProRes 422 HQ
-   Apple ProRes 4444
-   Apple ProRes 4444 XQ

**Avid DNxHR Movie**

-   DNxHR RGB 444 12-bit
-   DNxHR HQX 10-bit
-   DNxHR HQ 8-bit (Default)
-   DNxHR SQ 8-bit
-   DNxHR LB 8-bit

**Apple ProRes Movie** and **Avid DNxHR Movie** nodes embed timecode as specified in the **Global Output Settings** node.

Both **Apple ProRes Movie** and **Avid DNxHR Movie** nodes are only usable in Windows builds of Unreal Engine.

### Collection Nodes

The Collections node allows you to gather and group different actors based on visibility attributes you would like to override in your level. Examples of this would be Background, Characters, Lights, and Foliage.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ef33340-e178-4e6e-a9f2-e4ca5cfaaa0b/image_7.png)

You will need to give each Collection node its own unique name. Otherwise, Collections of the same name later in the graph will override the original.

#### Condition Groups

Collections have a notion of **Condition Groups**. These are groups where you define the conditions that populate the collection. There are several conditions to choose from to enable you to traverse the level to get the desired actors. The following are the types of conditions you can add to a condition group:

-   **Actor**
-   **Actor Tag Name**
-   **Actor Name**
-   **Actor Type**
-   **Actor Layer**
-   **Component Tag Name**
-   **Component Type**
-   **Editor Folder**
-   **Sublevel**
-   **Data Layer**
-   **Is Spawnable**

To add a Spawnable Actor to a condition group, you must use an Actor Name Condition, or by using the **Is Spawnable** property to include any Spawnable Actor in the scene for a given Shot.

The following are some examples of wildcards used for the **String** data type inputs, such as **Actor Name**, **Actor Tag Name**, and **Component Tag Name**.

-   `Foo*` would match `Foo`, `FooBar`, and `FooBaz`, but **not** `BarFoo`.
    
-   `*Foo*` would match the above in addition to `BarFoo`.
    
-   `Foo?Bar` would match `Foo.Bar` and `Foo_Bar`, but **not** `FooBar`.
    
-   `Foo?` would match `Food`, but **not** `FooBar` or `BarFoo`.
    
-   `Foo???` would match `FooBar` and `FooBaz`, but **not** `Foo` or `Food`.
    
-   `?oo?` would match `Food`, but **not** `Foo`.
    
-   `?Foo*` would match `AFooBar`, but **not** `FooBar`.
    

#### Condition Group Leveraging

You can add multiple conditions per group to create the membership. You can also leverage the conditions with and/or against each other. You can use **Add**, **Subtract**, and **And**.

| Condition |   |
| --- | --- |
| **ADD** | 
The Add condition will add the results of the conditions together.

For example: actor name matches `CHAR_*` **Add** actor is in sublevel `FG_SUBLEVEL`

This would include actors in any sublevel that matched `CHAR_*` and also any actor in the sublevel `FG_SUBLEVEL` regardless of its name.



 |
| **SUBTRACT** | 

The Subtract condition will subtract the condition groups from one another.

For example: actor name matches `CHAR_*` **Subtract** actor is in sublevel `FG_SUBLEVEL`

This would include actors in any sublevel that matched `CHAR_*` but remove any actor in the sublevel `FG_SUBLEVEL`.



 |
| **AND** | 

The And condition will check that both condition groups are met.

For example: actor name matches `CHAR_*` **And** actor is in sublevel `FG_SUBLEVEL`

If you had actors matching `CHAR_*` in other sublevels like `OTHER_SUBLEVEL` then they would not be included, and if other actors in `FG_SUBLEVEL` don't match `CHAR_*` then they too would not be included. So the results would be only where the conditions intersect.



 |

You can even leverage multiple condition groups.

![Use multiple condition groups](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88a229a2-debb-4570-abfc-124b5fe348bc/image_9.png "use multiple condition groups")

Additionally, you can have multiple complicated Condition Groups, and leverage those Groups either with or against each other.

![Multiple condition groups](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94c6589e-a410-4dce-9010-cace5c0332df/image_10.png "multiple condition groups")

#### Condition Group Re-Ordering

If you hover over the left-hand side of a Condition Group or Condition Group Layer you will see ten dots show up in the UI and the mouse cursor icon will turn into a hand. You can then drag and drop to re-order the Condition Groups.

![Reorder Condition Groups](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd3b4a38-5011-4157-8e3b-2d1e2525a95f/image_11.png "reorder condition groups")

#### In-Editor Collection Membership Display

The arrow icon at the top of the details panel will resolve the node and select the actor members in the Engine.

![Resolve conditions and select actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e7ef292-2683-44b2-8a63-705160fa86df/image_12.png "resolve conditions and select actors")

A single actor can be a member of multiple Condition Groups and Collections. The Graph does not limit any membership under the hood and needs to be managed manually.

#### Collection Availability

Collections must be defined in the same chain as the Modifier you want to use them in. If they are outside the chain, you will get an error when you select an unconnected Collection. Collections in Subgraphs are available in Parent Graphs as well.

![Collection availability](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5a96b91-f5fb-4900-9c79-a00efae012c6/image_13.png "collection availability")

#### Spawnables

Due to the transient nature of Spawnables in the Engine, they have somewhat limited support in Movie Render Graph that will likely be improved in the future. In the Collection node, you will need to get the spawnable actors by using an applied Actor Tag.

There is a current limitation on tagged components. Those will not be retained in the level when the actor re-spawns due to Blueprint reconstruction. To tag components, apply these render tags to the asset rather than the actor.

### Modifier Nodes

Modifier nodes are used to control the visibility conditions of Collections. **As with Collections, it is highly recommended to give each Modifier a unique name.**

You set which Collection or Collections the Modifier node can control under the **Collections** section.

![Choose collections controlled by the modifier node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba2bc6c6-7c04-459b-a0b5-a682b2986557/image_14.png "choose collections for modifier node")

Under the Visibility section, there are five attributes and a Material slot that you can control on the actors in the Collection. These parameters coincide with the same parameters on the Actor. The SkyAtmosphere and HeightFog **Render in Main** parameters are equivalent to **Affect Indirect Lighting While Hidden**. The Movie Render Graph makes this connection for you under the hood. Below is a list of these properties and a description of their functionality.

![Settings in the Visibility section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/443eeb80-ebd5-4bdc-b8e1-9d01795ab1bc/image_15.png "settings in the Visibility section")

If you do not see these attributes on a given actor type, that means those types are not supported yet.

| Property | Description |
| --- | --- |
| **Is Hidden (Visible to Camera)** | Controls Collection actor membership visibility. |
| **Cast Shadows** | Controls whether the Collection actor membership will cast a shadow in the level. |
| **Cast Shadows While Hidden (Visible to Shadows)** | Controls the Collection actor membership's ability to still cast a shadow while not being visible to primary pixels. |
| **Affect Indirect Lighting While Hidden (Visible to Indirect)** | Controls whether the Collection actor membership is visible to the Lumen scene, both GI and Reflections, while not visible to primary pixels. |
| **Holdout** | Control whether the Collection actor membership will poke a black hole in the render layer's RGBA. |

#### Using a Modifier Node

Let's take a look at a visual example here in the Meerkat sample project. In the first shot we have the background (BG), an egg, and the meerkat.

![Meerkat and egg in a desert](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c1451d3-efc8-408f-b0b9-eaee59e57e26/image_17.png "meerkat and egg in a desert")

If we toggle the **Visible** flag on the egg we see it disappear along with its shadow and reflections, as well as any sort of GI contribution to the scene.

![Hide the egg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13abd71a-c352-42b0-9451-5ea8ec5b0c2a/image_18.png "hide the egg")

If we enable **Hidden Shadow** on the egg we see the shadow come back.

![Reveal egg's shadow](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/526baf44-fb21-400a-bef7-dff3eb6ce6be/image_19.png "reveal egg's shadow")

Now if we enable the **Lumen Overview** we see that the egg is no longer in the Lumen scene, so it will not cast any reflections or GI.

![Enable Lumen Overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7164452a-8641-4460-9e9d-ecfffa92c747/image_20.png "enable lumen overview")

If we enable **Affect Indirect Lighting While Hidden** and disable **Screen Traces**, we see the egg reappear in the Lumen Scene, along with GI occlusion and reflections in the viewport.

![Enable Indirect Lighting while hidden](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/720999ca-3372-49b7-9426-8ff386cd3c05/image_21.png "enable indirect lighting while hidden")

Now if we turn the **Visibility** back on, disable **Affect Indirect Lighting While Hidden** and **Hidden Shadow**, and enable the **Holdout** parameter you will see the egg has completely blacked out and is not poking a hole in the render. The alpha of this will render black as well.

![Turn visibility back on](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88b9bf17-0b68-4a34-ae36-f8d72e5c8ca4/image_22.png "turn on visibility")

It will still cast a shadow, and looking at the Lumen Scene, we see that the egg is still in there and will cast proper GI and reflections.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5633e3c-a4c7-4d71-bb1b-0366c519944a/image_23.png)

### Burn-In and UI Renderer Nodes

The Burn-In node allows for adding custom watermarks to your render, which would typically be timecode-related. You can choose whether the burn-in is applied to the final image, or rendered to a separate layer. A default BurnIn class is provided that covers the basics of JobName, Date, Level Name, Author, Changelist, and camera information.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa5fe966-11bd-4a84-8579-1a4634160e7e/image_24.png)

**The UI Renderer** node includes UMG widgets within the scene in the rendered output and provides flexibility by allowing the UMG-based elements to be in a separate Render Layer or composited into the final image.

## Output

The output node is what sends the logic to the renderer. To create outputs you need to click on the plus icon in the **Members** tab under the **OUTPUTS** section.

If there is a Render Layer node in the chain plugged into an Output then that chain’s logic will be sent to the renderer. If there is no Render Layer node then the logic will be passed out of the Movie Render Graph, which is useful for pipeline tools and for use with Subgraphs. Outputs without a connection will do nothing.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad8eaf64-49f4-463e-afd4-45d11bd09b92/image_25.png)

## Conditional Nodes

There are some logic nodes that can apply to the Movie Render Graph to control the computing of branches.

### Branch Node

This node takes a True/False boolean as an input to let the Movie Render Graph which branch to compute.

For example, if you want to set up a single render layer but want to be able to choose whether it is rendered with the Pathtracer or the Deferred Path.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77932121-8c47-4155-93b6-30406f7aff90/image_26.png)

### Select Node

This node takes an input to let Movie Render Graph know which branch to compute. You can select the desired data type for the input in the Details Panel of the Select node. If no option is stated the data will flow through the **Default** path.

See the image below for an example.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0af5d42-37bd-47c5-8ca0-be275d0d4222/image_27.png)

## Variables and Exposed Properties

Most nodes in the Movie Render Graph provide the ability to expose some of the properties as pins. This will allow you to **promote** these properties up to be set at the base Movie Render Queue UI rather than being hardcoded inside the Movie Render Graph. If you are familiar with Blueprints, this works similarly.

This is incredibly powerful when working in a source-controlled environment. Rather than having to have a graph per shot, you can expose desired parameters to be set at the job level rather than hard coded into the graph.

For example, if you want to be able to set Temporal Sampling differently for each shot in a sequence without having to make a Movie Render Graph per show, you can right-click on the Sampling Method node and **expose** the **TemporalSampleCount** parameter to a pin on the node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51de2873-dc03-45c0-bd4d-bbf668910ea8/image_28.png)

Then you can **right-click** on the new exposed pin and select **Promote to Variable**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39639057-cac9-427e-a997-9a36e92dc33b/image_29.png)

This will automatically create a variable of the correct data type– in this case, an Integer:

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6606ca86-eb8c-44fa-992e-352910406a23/image_30.png)

This will now be available to be set on the job in your Queue.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/446fbf22-b92e-436a-ae4d-cbaf0dd73459/image_31.png)

Or you can use the **Branch** conditional to pick which Render Layers you want to render without having to dive into the graph asset.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de774efb-8e01-41d5-a086-e913dc4605d9/image_32.png)![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd8e0a4b-72bd-4355-a903-4ae5d5983db2/image_33.png)

## Script Tags

All Nodes in an MRG Graph have a **Script Tags** property that you can use to tag and organize nodes in order to facilitate pipeline tools and use scripts that parse graphs to find particular nodes that may need to access or modify as part of their desired functionality.

## Remove Render Setting

This node can be connected in a parent graph to remove any node of type in the subgraph.

A use case is if a subgraph has a JPG node that you don't want in your parent graph. You can connect the Remove Render Setting node in the parent graph to get rid of the JPG node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/849a025a-d306-45d2-a734-f2075a536124/image_34.png)

## Set Metadata Attributes Node

You can use the **Set Metadata Attributes** Render Layer node to configure custom attributes that will be written as EXR Metadata when rendering to that Output Type. Metadata Attributes are key and value pairs that have EXR as their default prefix. You can use slashes to provide organizational structure for metadata.

File Name Format tokens can be used to provide dynamic metadata. Additionally you can use the **{** key to bring up the dropdown list that appears on the Output Type nodes.

This node is also scriptable and pipelines can automate metadata creation by adding nodes via Python, alleviating the need for custom tools to interject metadata after the EXR is written.

EXR is the only Output Type capable of receiving metadata. Other formats such as JPG, PNG, and TIF do not support metadata.

## Subgraphs

**Subgraphs** were created to give greater flexibility to base graphs in a source-controlled environment. Subgraphs are independently source-controlled Movie Render Graph assets that can be loaded into other Parent Graphs and still apply the logic. Parameters and/or logic can then be added, appended, or overridden.

In this screenshot, we are taking the output of the out\_ENV render layer chain and creating a new Collection. Then splitting the **Bugs** out to their own render layer. This is an example of how an artist can make shot-level changes without having to check out and edit, or duplicate and edit, a sequence-level Movie Render Graph.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02a8a6ca-4659-4c1b-b9cc-917b57f3bc58/image_35.png)

## Graph Evaluation

You can see the results of the graph evaluation by pressing the Evaluate Graph button under the Active Render Settings tab.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d85a8d87-5243-4354-a3b1-56e150773ff9/image_36.png)

The Movie Render Graph is evaluated from the **Output** backward, or from right to left. The graph composes left-to-right, where nodes closest to the Output node 'win' or have the highest precedence

You can see this in action here by breaking a chain and re-evaluating, or by setting the default condition status one way or another on a Branch node:

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83e8dabe-03ef-4b29-96e8-46039394089f/image_37.png) ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6cfcf2eb-0deb-4e53-958d-8ee2d1b92193/image_38.png)

## Supported Actor Types

Movie render graph supports all actor types in Render Layers. However there are a few actor types which require some additional considerations when using **Holdouts** and **Affect Indirect While Hidden**. Here you can reference the Actor types that require additional setup or considerations when using the Movie Render Graph:

| Actor Type | Support Level |
| --- | --- |
| **Translucent Actors** | Holdouts on Translucent Objects will have limitations when used with fog. |
| **Niagara**, **Fluid**, and other **Translucent FX** | When there are multiple HVs in the scene, holdouts can be applied to individual actors only when using the **Deferred Renderer**. When using the **Path Traced Renderer**, setting one HV in the scene to holdout will result in all HVs in the scene rendered as a holdout. |
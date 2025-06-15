# Storing Custom Data in Materials Per-Primitive

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/storing-custom-data-in-unreal-engine-materials-per-primitive](https://dev.epicgames.com/documentation/en-us/unreal-engine/storing-custom-data-in-unreal-engine-materials-per-primitive)  
**Processed:** 2025-06-14 16:52:42

---

With the **Custom Primitive Data** (CPD) workflow, you can use your Materials to store custom data in an index array that is accessible through Blueprint and code. You can use this data to effect changes for scene primitives at runtime.

This is similar to the way [Material Instance Dynamics](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine#materialinstancedynamic) (MID) function, providing a way for you to control parts of your Material graph dynamically at runtime through Scalar and Vector Parameters. The difference is that Custom Primitive Data has the advantage of storing data on the primitives themselves rather than with the Material Instance. This lowers the number of draw calls for similarly placed geometry in your Levels (such as walls, floors, or other duplicated geometry).

## Usage and Workflow

The steps below summarize how you can use Custom Primitive Data to interact with scene primitives.

1.  Create Scalar and Vector Material Parameters to control parts of your Material logic. Enable **Use Custom Primitive Data** on each parameter you want to set and control dynamically.
2.  Give each parameter with Custom Primitive Data enabled a unique **Primitive Data Index** in the Details Panel. You will reference this index in either Blueprint or code.
3.  Use the **Set Custom Primitive Data** nodes in Blueprint to set and control the Material Parameters for the values stored in the custom data array.

### Material Setup

Add **Scalar** and **Vector Parameter** expressions to your graph to control attributes of the Material, like you would in a [Material Instance](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine#materialparameterization).

With a Parameter selected, find the **Use Custom Primitive Data** property in the Details Panel and enable it.

![Enable Custom Primitive Data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96e3e7ca-7582-4669-ac41-c8bff8346201/custom-primitive-data-property.png)

Once enabled, the parameter displays "Custom Primitive Data" below its given name along with its assigned value in the **Primitive Data Index**. This value is also shown on the node itself.

![Custom Primitive Data Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a90060e-2d75-46ab-8390-056a6439f948/custom-primitive-data-enabled.png)

The **Primitive Data Index** value sets the assigned index this parameter is stored in. This index is used to reference the parameter in Blueprint and code.

When assigning an index on a **Scalar** (float) parameter, the index is a single value. When doing the same on a **Vector** parameter, each channel in the parameter is assigned a different value in the Primitive Data Index. In the image above, the Scalar Parameter is assigned to Index 0, while the Vector Parameter is assigned to Index 1, 2, 3, and 4. One index value for each RGBA output.

### Blueprint Usage

You can access scene primitives that use Custom Primitive Data through Blueprint with the following nodes.

-   **Set Custom Primitive Data Float**
-   **Set Custom Primitive Data Vector**

These nodes require no string-matching to parameter names. Instead, they use the assigned **Primitive Data Index** to set and get data in the array per primitive.

![Custom Primitive Data Blueprint nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3405b354-f54f-44db-8e2c-14229f6a599e/custom-primitive-blueprint-nodes.png)

Accessing custom data in this array from a Material is similar to working with Material Parameters in a Material Instance. The difference is that on Parameter nodes, the parameter in the Material must be a string-matched uniform rather than matching a numbered index.

### Actor Defaults Usage

You can setup Custom Primitive Data Default values for an Actor by selecting its Static Mesh Component in the Details panel and expanding the **Custom Primitive Data Defaults** section. Use the **Plus (+)** icon to add elements to the array. The array will populate with named Custom Data Parameters from your Material, along with their Primitive Data Index value.

![Custom Primitive Data Actor Defaults](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cde3e45e-5547-4b14-8e8d-8250d2347c3a/custom-primitive-default-values.png)

Each numbered array element references the Custom Primitive Data Index with the corresponding value. If an index does not exist for the array element, it is ignored. Setting defaults using this method is ideal when you want to manually adjust some values without attaching a Blueprint or making a Material Instance to control them.

## Example Setup

The following example demonstrates use with a simple Material that is driven by several parameters—both Scalar and Vector—to randomly select a color from a Vector Parameter and set the emissivity and object scale of the mesh in the scene. Blueprint is used to drive these three parameters for the stored custom data.

### Material Example Setup

For the Material setup, **Use Custom Primitive Data** is enabled on three parameters in this Material graph.

Click image for full size.

The **Base Color** and **Emissive** intensity are driven by two parameters; a Vector 4 Parameter called "Color Param", and a Scalar Parameter called "Emissive Power."

Click image for full size.

The second part of this graph uses logic to uniformly scale the mesh it's assigned to in the Level. The scalar parameter called "Scale\_XYZ" controls how much the assigned object is scaled.

Click image for full size.

### Blueprint Example Setup

Custom Data on parameters, much like Material Instance Dynamics, provide a way to make changes using Blueprint or code at runtime. The graph below sets and updates values in these Material parameters to randomize the color, emissivity, and initial scale during gameplay.

Click image for full size.

On Event BeginPlay, **Set Custom Primitive Data** nodes are used to set the initial values for the color, scale, and emissivity parameters. The **Data Index** property determines which Material Parameter is targeted by that node.

Click image for full size.

For example, the **Emissive Power** parameter is assigned to Index 4, so its value will be set by the Blueprint node that targets **Data Index 4**.

![Data Index Target](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11195970-fd59-4a7e-b26c-f2f329476588/data-index-target.png)

On **Event Tick**, the Set nodes reference the Primitive Data Index for each Custom Primitive Data Parameter. A new color, emissive intensity, and scale are set at the interval defined in the Delay node. The color is set by combining three random float values into a Vector 4. The emissive power and scale are randomized with the **Random Float in Range** nodes.

Click image for full size.

Be careful when setting up and using Event Tick. For the purposes of this demonstration, it's good for quick tests and debugging, but is not always best for continuous use at runtime.

### Example Result

The result of this example is a Material with three Custom Primitive Data parameters that are controlled by Blueprint to set the color, emissive power, and scale of the Mesh. The values are set at runtime, and then updated randomly every **0.5** seconds, as defined in the Blueprint.

## Material Instance Dynamic Comparison

The setup and usage of Custom Primitive Data is similar to that of [Material Instance Dynamics](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine#materialinstancedynamic). This section compares the Material and Blueprint setup required for each of these to better demonstrate how they are alike and different.

When creating Material Instance Dynamics, the name of the parameter is all that is needed later in Blueprint. The Custom Primitive Data workflow requires that the **Use Custom Primitive Data** option is enabled on each parameter, and that a unique **Primitive Data Index** value is assigned, which is referenced in Blueprint later.

|   |   |
| --- | --- |
| ![Regular Parameter Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/381c801f-e51a-43b6-b141-71c421f10c09/mid-properties.png) | ![Custom Primitive Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f455d7ce-66bd-4cc3-8e68-8080f30e3914/cpd-properties.png) |
| MID Material Parameters | Custom Primitive Material Parameters |

The following images compare the Blueprint setups for Material Instance Dynamics and Custom Primitive Data.

-   **Material Instance Dynamics Workflow:**
    
    Click image for full size.
    
    For additional information on instancing with Materials, see [Instanced Materials](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine).
    
-   **Custom Primitive Data Workflow:**
    
    Click image for full size.
    

The workflow is similar, with the exception that there are some additional steps to take in Blueprint. The MID workflow requires the **Create Dynamic Material Instance** node and some **Set Parameter Value** nodes that reference the string-matched **Parameter Name** found in the Material for the wanted parameter.

If both of these setups are compared in the Level at runtime, they are visually identical. However, Custom Primitive Data comes with performance-saving benefits using the mesh drawing refactor that is covered in the section below.

The cluster of four spheres on the left side of the video use Custom Primitive Data, while the four spheres on the right use Material Instance Dynamics. Note that the result is visually identical.

## Performance

The Custom Primitive Data workflow has the advantage of significantly reducing draw calls for similar geometry in your Level when it is using a Material set up with custom data. Draw calls are reduced using the [Mesh Drawing](/documentation/en-us/unreal-engine/mesh-drawing-pipeline-in-unreal-engine) refactor that automatically dynamically instances scene primitives.

To check how well dynamic instancing is working for your Level, open the console (\`) and enter the command `stat scenerendering`.

This command shows general rendering statistics for your current scene view. It is a good starting point to finding general areas of slow performance in the rendering process, along with counters for the number of mesh draw calls and lights in the scene.

![Stat Command scenerendering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/526c7d99-6613-4332-81e2-32776b3eb89e/render-stats.png)

Default Level scene rendering stats

While working in the Level viewport, press the **G** key to toggle Game View mode, or choose to Play-In-Editor (PIE) or Simulation to get more accurate results. When not using one of these options, other draw calls are being attributed to Editor-only geometry, like icons for the Directional Light.

In this example scene, we start with a floor mesh, the sky sphere mesh in the background, and several duplicated meshes using custom data in their Materials.

![Console command stat rendering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef780f4e-e06c-4b15-bbb5-555d710c2507/cpd_statscenerenderin2a.png)

The scenerendering stats shows the number of draw calls registered in this current view—14 in total.

![Mesh draw calls with dynamic instancing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02bd83c8-3a0f-4414-bb8f-109652775734/cpd_statscenerenderin2.png)

Because the engine automatically dynamically combines draw calls with the Mesh Drawing Policy, it's good to disable dynamic instancing to see how well it's currently working for this scene. Disable it with the following command:

```
    `r.MeshDrawCommand.DynamicInstancing 0`
Copy full snippet
```
r.MeshDrawCommand.DynamicInstancing 0

Notice that the number of `Mesh draw calls` has increased with just a few primitives:

![Mesh draw calls without dynamic instancing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4211d99c-fa2e-43bf-a562-f2d0f2998a20/cpd_statscenerenderin3.png)

To see a more dramatic difference, let's duplicate the meshes some more that are using Custom Primitive Data; 25 spheres with varying sizes, in this case.

![Spheres with custom primitive data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af84db2d-ee3e-4839-8589-52290eb8e689/cpd_statscenerenderin4.png)

-   With dynamic instancing disabled, there are **94 Mesh draw calls**. Using Material Instance Dynamics will give you a similar result because they are not instanced liked Custom Primitive Data.
    
    ![Mesh draw calls with dynamic instancing disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70ab31eb-a026-44f3-bc92-22b8341c6ed9/cpd_statscenerenderin4b.png)
-   Reenabling dynamic instancing now shows **46 Mesh draw calls**.
    
    ![Mesh draw calls with dynamic instancing enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5343463-f53b-4153-8dde-29a83ad1138e/cpd_statscenerenderin4a.png)

When storing custom data in your Materials and using similar geometry in your Level, you can clearly get a difference in the number of draw calls, even over using alternative methods like Material Instance Dynamics.

## Additional Notes

-   **Float Limit of 32**
    -   In a future release, we'll look at making this a Project Setting as a configurable setting.
-   **Support for user-defined default and override of Custom Primitive Data parameter values**
    -   Currently, when setting up a Custom Primitive Data parameter in your Material, the default value is always 0. If you want an initial value set while working in the editor, you can do this using the Construction Script in Blueprint for the mesh that the Material is assigned to.
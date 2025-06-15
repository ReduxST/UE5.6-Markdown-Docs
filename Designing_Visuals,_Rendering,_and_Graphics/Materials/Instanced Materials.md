# Instanced Materials

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine)  
**Processed:** 2025-06-14 16:31:12

---

**Material instancing** in Unreal Engine is used to change the appearance of a Material without incurring an expensive recompilation of the Material.

Whereas a typical Material cannot be changed without recompiling (something that must happen prior to gameplay), a parameterized Material can be edited in a Material instance without such recompilation. This has numerous workflow advantages, and can improve Material performance.

![Material Instance Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64361a69-c612-4b75-bd89-7401ccdad204/material-instance-editor-5-0.png)

A Material instance open in the Material Instance Editor. You can customize the attributes listed under Parameter Groups from this interface.

Certain types of instanced Materials can even change during gameplay in response to in-game events (such as a tree whose Material blackens and chars while it burns). This allows tremendous visual flexibility in your artistic elements.

## Material Inheritance

The relationship between Materials and Material instances is a hierarchical parent-child relationship. A Material instance inherits all of its attributes from the parent (or master) Material. For example, this is the Material graph for one of the chair props found in the starter content:

![Starter content chair material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71d2e973-c251-4216-b625-5597a4930697/starter-chair-material.png)

Any Material instances created from **M\_Chair** inherit all the attributes from the graph shown above.

![Material Inheritance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46848315-f9cd-4571-8dfd-559c268f1eb4/material-inheritance.png)

Note the naming conventions used above. This is a good practice to adopt so that you can easily identify parent Materials and Material instances in the Content Browser.

1.  The prefix **M\_** denotes a parent Material, as in **M\_Chair**.
2.  The prefix **MI\_** denotes a Material instance, as in the two examples pictured right.

Because they inherit their attributes from the parent, newly created Material instances appear identical to the parent Material when applied to objects in the Level. In the image below, the chair on the far left has the parent Material applied while the center and right chairs use unaltered Material instances.

![Material instances on chairs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0972f46c-9b8d-4764-aedb-58d0c611cac3/unaltered-instances-applied-ue5-sm.png)

The key workflow benefit of Material instances is that you can very rapidly customize them the **Material Instance Editor** without ever editing the node graph or recompiling the Material.

In the video below, the two Material instances are opened from the Content Browser, and edited in the Material Instance Editor. Changes appear in the main viewport immediately, whereas a standard Material could take up to a minute to recompile, depending on the complexity.

## Material Parameterization

It is important to know that you cannot edit every single characteristic of a Material instance by default. To make Material attributes editable within an instance, you must designate them as parameters in the parent Material. This is called **parameterizing** your Material.

A parameter is created like any other data node in the Material Editor, and contains the same information as its non-parameterized counterpart.

For example, a **Constant** expression contains a single floating-point value, and is frequently used to control Material inputs like Roughness and Metallic. The parameterized version of this node is called a **Scalar Parameter**.

![Constant and Scalar Parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2944c10-13e1-4fde-a47a-e17dfe0e7a23/constant-vs-scalar.png)

Constant Material expression (1) and Scalar Parameter (2).

Note that the Scalar Parameter also becomes a named value which serves as a conduit to send data values into a Material instance. It is important that you give every parameter a unique, descriptive name in the **Details panel**. Select the node in the Material Graph to access its properties in the Details panel.

![Parameter details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aecf4240-61e9-40e9-9ab2-1093dadea094/parameter-name.png)

In the above example the parameter's name is **Roughness**, and it has a default value of 0.25.

In the simple parameterized Material shown below, a **Vector Parameter** is connected to the Base Color input, while **Scalar Parameters** are plugged into Metallic and Roughness.

![Simple parameterized material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72b5f805-6cb3-4ed9-b342-db202618e708/simple-parameterized-mat-ue5.png)

To further illustrate the idea of parameterization, there is also a constant value of 0.5 passed into the **Specular** input.

When opened in the Material Instance Editor, the three parameters are exposed and editable, whereas the constant is not. Values you want to expose to artists should be parameters, and values that you don't want anyone to change should remain as constants.

![Material Instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ff352ac-4655-49ac-9515-1ba84065463d/material-instance-example-ue5.png)

The parameters for Base Color, Metallic, and Roughness are editable in the Material Instance Editor, while the contant value is not exposed to artists.

## Types of Parameters

Parameters can be used anywhere in your Material graph to drive a wide range of Material effects.

Some of the key parameter types are documented below, and a full list of [Parameter Expressions](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine) is found here.

### Scalar Parameters

A **ScalarParameter** is a parameter that contains a single floating-point value. Scalar parameters can drive any effect based on single values, as seen in the Roughness and Metallic examples above.

Scalar parameters are also frequently used to control the multiplication factor of an attribute.

![Scalar parameter driving emissive power](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f48449c-26c9-4348-a254-2204cb55642d/scalar-parameter-emissive.png)

In this graph, a Scalar parameter is multiplied by a solid color, and the result is plugged into the Emissive Color input. The value in the Scalar Parameter controls the strength of the emissive effect. Higher values increase the emission brightness.

### Vector Parameters

A **VectorParameter** is a parameter that contains a 4-channel vector value, or four floating-point values.

![Vector parameter node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6e1b5ab-a9b6-4b05-993e-fba9dedae2ca/vector-parameter-ue5.png)

These are generally used to provide configurable colors, but could also be used to represent positional data or drive any effect that requires multiple values.

### Texture Parameters

The most commonly used texture parameter is the TextureSampleParameter2D, which allows you to change textures within a Material instance.

![Texture Parameter 2D](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80ab436e-ede3-4ed5-9d17-8c191e9957f4/texture-parameter-2d.png)

There are several additional types of texture parameters available. Each one is specific to the type of texture that it accepts or the manner in which it is being used. For example:

-   TextureSampleParameterCube accepts a TextureCube or cubemap.
-   TextureSampleParameterFlipbook accepts a FlipbookTexture.
-   TextureSampleParameterMeshSubUV accepts a Texture2D that is used for sub-uv effects with a mesh emitter.
-   TextureSampleParameterMeshSubUV accepts a Texture2D that is used for sub-uv blending effects with a mesh emitter.

See the [Material Expression Reference](/documentation/en-us/unreal-engine/unreal-engine-material-expressions-reference) for a complete list of texture parameters.

### Static Parameters

**Static** parameters are applied at compile-time, so they can be edited in the Material Instance Editor but not from script or at runtime.

They can be used to mask out branches of a Material. For example, a **StaticSwitch** parameter takes two inputs. It outputs the frst value if the parameter value is true, and the outputs the second if false. This produces more optimal code as the branch that was masked out by a static parameter is not executed at runtime.

![Static Switch parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc3720db-5ceb-470a-b9b2-05bbbca75c5b/static-switch.png)

See [Static Switch Parameter](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#staticswitchparameter) and [Static Component Mask Parameter](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#staticcomponentmaskparameter) for information on the specific static parameter types.

A new Material is compiled for every combination of static parameters in the base Material that are used by instances.

This can lead to an excessive number of shaders that must compile. Try to minimize the number of static parameters in the Material and the number of permutations of those static parameters that are actually used.

## Constant and Dynamic Instances

There are two types of Material instances available in Unreal Engine:

-   **Material Instance Constant** — Only calculated prior to runtime.
-   **Material Instance Dynamic** — Can be calculated (and edited) at runtime.

### Material Instance Constant

A **Material Instance Constant** is an instanced Material that calculates only once, prior to runtime. This means that it cannot change during gameplay. Although they remain constant throughout your game, they still have the performance advantage of not requiring compilation.

For instance, if your game has a variety of cars with different paint jobs whose colors will not change during gameplay, the best practice approach is to create a master Material that represented the base aspects of a generic car paint. Then create **Material Instance Constants** to represent the variations for different types of car, such as different colors, varying levels of roughness, and so on. This approach was demonstrated with the chair example earlier on this page.

Material Instance Constants are created within the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) and are edited from the [Material Instance Editor](/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui).

### Material Instance Dynamic

A **Material Instance Dynamic** (MID) is an instanced Material that can be calculated during gameplay (at runtime). This means that as you play, you can use script (either compiled code or Blueprint visual script) to change the parameters of your Material, thereby altering your Material throughout the game. The possible applications for this are endless, from showing different levels of damage to changing paint colors in an architectural visualization.

MIDs are created within script, either from a parameterized Material or a Material Instance Constant. In Blueprint, one would take a given Material that had parameterized properties, and feed it through a **Create Dynamic Material Instance** node. The result of that node is then applied to the object in question with a **Set Material** node. This produces a new Material that can be changed during gameplay.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/997f6a1e-5655-456e-9ba1-64fc150d9d3e/constructionscriptformid.png)

## Creating and Using Material Instances

Creating and using Material instances is a two step process. First you must create a parent Material that uses parameter expressions for the properties you want to be able to override in a Material instance. Then you can create a Material Instance and customize the properties in the Material Instance Editor.

To learn how to create a parameterized Material and use it in a Material instance, read here: [Creating and Using Material Instances](/documentation/en-us/unreal-engine/creating-and-using-material-instances-in-unreal-engine).
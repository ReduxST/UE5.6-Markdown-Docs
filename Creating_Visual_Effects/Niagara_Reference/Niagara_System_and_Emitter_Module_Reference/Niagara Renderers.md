# Niagara Renderers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/render-module-reference-for-niagara-effects-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/render-module-reference-for-niagara-effects-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:43

---

Niagara Renderers describe how Unreal Engine should display each spawned particle. Note that this does not have to be visual. Unlike modules, the placement of the renderer in the stack is not necessarily relevant to draw order. These types of renderers are currently supported:

-   **Component Renderer**
-   **Light Renderer**
-   **Mesh Renderer**
-   **Ribbon Renderer**
-   **Sprite Renderer**
-   **Decal Renderer**

![Add a Render module in the Niagara Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eeee29c8-f319-469d-95cb-3974f5bccdca/5-2-010-add-a-renderer.png "Add a Render module in the Niagara Editor")

The following sections list the parameters available in each type of renderer, along with a description of what that parameter does.

## Component Renderer

Features are sometimes made available in an Experimental state so you can try them out, provide feedback, and see what we are planning. **We do not recommend shipping projects with Experimental features.** Please keep in mind that we do not guarantee backward compatibility for assets created at the experimental stage, the APIs for these features are subject to change, and we may remove entire Experimental features or specific functionality at our discretion.

The **Component Renderer** provides a way for you to spawn any type of component, and update its properties with data from the particle simulation.

The Component Type sets which component is used (for example, a Point Light) for the particle simulation and displays properties and settings relevant to it under the **Component Properties** category within the **Details** panel. The properties can be edited directly from this list, and all components spawned by the renderer will be constructed based on these properties.

To inject particle data into the components, use the dropdown menu to the right of a property and select the particle attribute to bind to this property (see the example below). Some component types require a special class as their parent. This means they will not work with the Component Render, but instead may be a subclass of SceneComponent. They can be either a C++ class or a Blueprint. An example of this is the Landscape Component, which needs a LandscapeProxy Actor as its parent.

![Component properties dropdown menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11cceb4c-59d0-4fa5-a2da-4cb6400aa8c8/5-2-020-component-renderer-binding.png "Component properties dropdown menu")

This example uses a Point Light component. The properties displayed vary according to the component selected.

Because the configured bindings are evaluated and updated at the end of every tick after the particle simulation is finished, the Component Renderer can be an expensive operation to run. It should be used with caution.

Currently, only basic Niagara data types can be bound (float, bool, vector, and so on). Structs, objects, and enum properties can be set dynamically.

When using components in your Niagara systems, it's best to keep the component count as low as possible (unless you are working in an environment where performance is less of a concern, such as a cutscene rendered with Sequencer). Since each component has its own tick each frame in addition to the Niagara system, spawning a lot of effects with Component Renderers can impact performance.

In cases where a component does not expose properties, or the one you want to bind to is inside a nested struct, you can create a custom subclass of the component and add the property yourself. An example would be not being able to bind a value to the lighting channels of a Point Light component because they use a custom FLightingChannels struct.

![No suitable binding available message](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1c40ca4-e523-46e4-a597-b6f014824358/5-2-030-no-suitable-binding.png "No suitable binding available message")

However, you can subclass the Point Light component and add the channel properties yourself, then set the active light channels on the component's tick function, like the example below:

Click image for full size.

This enables you to then bind particle values to your properties in the Component Renderer.

The following properties are part of the Component Renderer before setting a **Component Type**.

| Parameter | Description |
| --- | --- |
| **Component Type** | The scene component class to spawn with this renderer. |
| **Component Count Limit** | The maximum number of components that this emitter will spawn or update each frame. |
| **Enabled Binding** | Determines which attribute is used to check if component rendering should be enabled for a particle. This can be used to control the spawn-rate on a per-particle basis. If the binding does not exist, all particles spawn a component. |
| **Assign Components on Particle ID** | If true, then a component will not be automatically assigned to the first particle available, but will try to stick to one particle over its lifetime. Disabling this option is faster, but a particle can get a different component each tick, which can lead to problems with motion blur or flickering. |
| **Only Create Components on Particle Spawn** | If true, then new components can only be created on newly spawned particles. If a particle is not able to create a component on its first frame (for example, because the component limit was reached) then it will be blocked from spawning a component on subsequent frames. |
| **Visualize Components** | If true, then the editor visualization is enabled for the component; this has no effect in a shipped game. For example, the light component shows the active bounds in the editor viewport when this is enabled. |

## Light Renderer

The Niagara Light Renderer module has the following base parameters.

| Parameter | Description |
| --- | --- |
| Light Rendering |   |
| **Use Inverse Squared** | 
This determines whether to use physically-based inverse squared falloff from the light. If this is unchecked, the value from the **Light Exponent Binding** is used instead.

When **Inverse Squared Falloff** is disabled, Linear Falloff is used. Linear Falloff is often easier to use, but can result in a too-bright result. Inverse Squared Falloff produces a more realistic level of brightness.



 |
| **Affects Translucence** | This determines whether lights from this renderer affect translucency. Use with caution: if you enable this, create only a few particle lights; the larger and more numerous they are, the more it will cost. |
| **Radius Scale** | This factor is used to scale each particle light radius. |
| **Color Add** | This is a static color shift that is applied to each rendered light. You can set values for the **X**, **Y**, and **Z** axes. These axes correspond to the **R**, **G**, and **B** color values (**X=R, Y=G, Z=B**); they do not indicate position. |
| Sort Order |   |
| **Sort Order Hint** | By default, emitters are drawn in the order they are added to the stack in a Niagara system. The **Sort Order Hint** value allows you to control the draw order in a more detailed way. Materials of the same type will draw in order from lowest Sort Order value to highest within the system. The default value is **0**. |
| Bindings |   |
| **Light Rendering Enabled Binding** | This defines the attribute used to check whether or not light rendering should be enabled for a particle. By default, this uses the **Particles.LightEnabled** variable if it exists; otherwise it uses the default of **None**. |
| **Light Exponent Binding** | This defines the attribute used for the light's exponent when **Inverse Squared Falloff** is disabled. By default, this uses the variable **Particles.LightExponent** if it exists; otherwise it uses the default of **10**. |
| **Position Binding** | This defines the attribute used for positioning when generating lights. By default, this uses the **Particles.Position** variable if it exists; otherwise it uses the default **Engine.Owner.Position** variable. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Color Binding** | This defines the attribute used for color when generating lights. By default, this uses the **Particles.Color** variable if it exists; otherwise it uses the default of **R: 1, G: 1, B: 1, A: 1**. |
| **Radius Binding** | This defines the attribute used for light radius when generating light. By default, this uses the **Particles.LightRadius** variable if it exists; otherwise it uses the default of **100**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Volumetric Scattering Binding** | This defines the attribute used for the intensity of the volumetric scattering from this light. It scales the light's intensity and color. By default, this uses the **Particles.LightVolumetricScattering** variable if it exists; otherwise it uses the default of **1**. |

## Mesh Renderer

The Niagara Mesh Renderer has the following base parameters.

| Parameter | Description |
| --- | --- |
| Mesh Rendering |   |
| **Particle Mesh** | This determines which Static Mesh will be instanced when rendering mesh particles. By default, the Static Mesh's Material is used. The Material must have the **Niagara Mesh Particles** flag checked. |
| **Override Materials** | When this is checked, it defines an array of Materials that are used instead of the Static Mesh's Material. All Override Materials must have the **Niagara Mesh Particles** flag checked. If the Particle Mesh requires more Materials than exist in this array, or if any entry in this array is set to **None**, the emitter uses the Particle Mesh's existing Material instead. |
| **Facing Mode** | 
This setting determines how the instanced Mesh orients itself relative to the camera. Options are:

-   **Default**: This ignores the camera altogether. The mesh aligns its local-space X-axis with the particle's local-space X-axis, after transforming by the **Particles.Transform** vector (if it exists).
-   **Velocity**: The mesh aligns its local-space X-axis with the particle's **Particles.Velocity** vector.
-   **Camera Position**: The mesh local-space X-axis points toward the camera.
-   **Camera Plane**: The mesh local-space X-axis points towards the closest point on the camera view plane.



 |
| Sorting |   |
| **Sort Mode** | 

This determines how particles are sorted prior to rendering. Options are:

-   **None**: There is no particle sorting.
-   **View Depth**: This sorts by depth to the camera's near plane.
-   **View Distance**: This sorts by the distance to the camera's origin.
-   **Custom Ascending**: This sorts according to a per-particle attribute; lower values are rendered before higher values.
-   **Custom Descending**: This sorts according to a per-particle attribute; higher values are rendered before lower values.



 |
| **Sort Only When Translucent** | If this is checked, particles are only sorted when using a translucent material. |
| Bindings |   |
| **Position Binding** | This defines the attribute used for positioning when generating instanced meshes. By default, this uses the **Particles.Position** variable if it exists; otherwise it uses the default **Engine.Owner.Position** variable. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Color Binding** | This defines the attribute used for color when generating instanced meshes. By default, this uses the **Particles.Color** variable if it exists; otherwise it uses the default of **R: 1, G: 1, B: 1, A: 1**. |
| **Velocity Binding** | This defines the attribute used for velocity when generating instanced meshes. By default, this uses the **Particles.Velocity** variable if it exists; otherwise it uses the default of **X: 0, Y: 0, Z: 0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Mesh Orientation Binding** | This defines the attribute used for orienting meshes when generating instanced meshes. By default, this uses the **Particles.MeshOrientation** variable if it exists; otherwise it uses the default of **X: 0, Y: 0, Z: 0, W: 1**. |
| **Scale Binding** | This defines the attribute used for scale when generating instanced meshes. By default, this uses the **Particles.Scale** variable if it exists; otherwise it uses the default of **X: 1, Y: 1, Z: 1**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Dynamic Material Binding** | This defines the attribute used for dynamic material parameters when generating instanced meshes. By default, this uses the **Particles.DynamicMaterialParameter** if it exists; otherwise it uses the default of **X: 1, Y: 1, Z: 1, W: 1**. |
| **Dynamic Material 1Binding** | This defines the attribute used for dynamic material parameters when generating instanced meshes. By default, this uses the **Particles.DynamicMaterialParameter1** if it exists; otherwise it uses the default of **X: 1, Y: 1, Z: 1, W: 1**. |
| **Dynamic Material 2Binding** | This defines the attribute used for dynamic material parameters when generating instanced meshes. By default, this uses the **Particles.DynamicMaterialParameter2** if it exists; otherwise it uses the default of **X: 1, Y: 1, Z: 1, W: 1**. |
| **Dynamic Material 3Binding** | This defines the attribute used for dynamic material parameters when generating instanced meshes. By default, this uses the **Particles.DynamicMaterialParameter3** if it exists; otherwise it uses the default of **X: 1, Y: 1, Z: 1, W: 1**. |
| **Material Random Binding** | This defines the attribute used for material randoms when generating instanced meshes. By default, this uses the **Particles.MaterialRandom** variable if it exists; otherwise it uses the default of **0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Custom Sorting Binding** | This defines the attribute used for custom sorting. By default, this uses the **Particles.NormalizedAge** variable if it exists; otherwise it uses the default of **0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Normalized Age Binding** | This defines the attribute used for normalized age. By default, this uses the **Particles.NormalizedAge** variable if it exists; otherwise it uses the default of **0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| Sort Order |   |
| **Sort Order Hint** | By default, emitters are drawn in the order they are added to the stack in a Niagara system. The **Sort Order Hint** value allows you to control the draw order in a more detailed way. Materials of the same type will draw in order from lowest Sort Order value to highest within the system. The default value is **0**. |

## Ribbon Renderer

The Niagara Ribbon Renderer has the following base parameters.

| Parameter | Description |
| --- | --- |
| Ribbon Rendering |   |
| **Material** | Select the material used to render the ribbon. |
| **Facing Mode** | 
This setting determines how the ribbon orients itself relative to the camera. Options are:

-   **Screen**: The ribbon faces the screen.
-   **Custom**: This uses **Particles.RibbonFacing** as the facing vector.
-   **Custom Side Vector**: Use **Particles.RibbonFacing** as the side vector, and calculate the facing vector from that.
    
    Using Ribbon Twist with this mode is not supported.



 |
| **UV0 Tiling Distance** | This setting tiles UV channel 0 based on the distance traversed by the ribbon. This disables the offsetting of UVs by age. |
| **UV0 Scale** | This setting defines the scale of UV channel 0 when you are using **Tiling Distance**. |
| **UV0 Offset** | This setting defines the offset used for UV channel 0 when you are using **Tiling Distance**. |
| **UV0 Age Offset Mode** | This setting defines the mode to use when offsetting UV channel 0 by age. This enables smooth texture movement when particles are added and removed at the end of the ribbon. This is not used when the **Ribbon Link Order Binding** is in use, or when **Tiling Distance** is in use. |
| **UV1 Tiling Distance** | This setting tiles UV channel 1 based on the distance traversed by the ribbon. This disables the offsetting of UVs by age. |
| **UV1 Scale** | This setting defines the scale of UV channel 1 when you are using Tiling Distance. |
| **UV1 Offset** | This setting defines the offset of UV channel 1 when you are using Tiling Distance. |
| **UV1 Offset Mode** | This setting defines the mode to use when offsetting UV channel 1 by age. This enables smooth texture movement when particles are added and removed at the end of the ribbon. This is not used when the **Ribbon Link Order Binding** is in use, or when **Tiling Distance** is in use. |
| **Draw Direction** | Draw Direction determines whether the ribbon is rendered Front to Back (from a point far from the camera to a point near the camera), or Back to Front (from a point near the camera to a point far from the camera). However this usually only makes a difference if the material is translucent and the ribbon folds on itself. |
| Tessellation |   |
| **Curve Tension** | This setting defines the curve tension, or how long the curve's tangents are. The setting's value ranges from **0** to **1**. The higher the value, the sharper the curve becomes. |
| **Mode** | 

This setting defines the tessellation mode allowing custom tessellation parameters, or disabling tessellation entirely. Options are:

-   **Automatic**: This uses the default tessellation parameters.
-   **Custom**: This allows customized tessellation parameters.
-   **Disabled**: This disables tessellation.



 |
| **Max Tessellation Factor** | If the **Mode** is set to **Custom**, this defines the custom tessellation factor. Settings range from **1** to **16**. Larger values increase the amount of tessellation. |
| **Use Constant Factor** | If this is checked, the **Max Tessellation Factor** is used. Otherwise, the tessellation factor is adaptively selected based on the parameters below. |
| **Tessellation Angle** | This setting defines the angle (in degrees) at which the tessellation occurs. Settings range from **1** to **180**. Smaller values increase the amount of tessellation. If the setting is **0**, the **Max Tessellation Factor** is used. |
| **Screen Space** | If this is checked, use the ribbon's screen space percentage to adaptively adjust the tessellation factor. |
| Sort Order |   |
| **Sort Order Hint** | By default, emitters are drawn in the order they are added to the stack in a Niagara system. The **Sort Order Hint** value allows you to control the draw order in a more detailed way. Materials of the same type will draw in order from lowest Sort Order value to highest within the system. The default value is **0**. |
| Bindings |   |
| **Position Binding** | This defines the attribute used for positioning when generating ribbons. By default, this uses the **Particles.Position** variable if it exists; otherwise it uses the default **Engine.Owner.Position** variable. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Color Binding** | This defines the attribute used for color when generating ribbons. By default, this uses the **Particles.Color** variable if it exists; otherwise it uses the default of **R: 1, G: 1, B: 1, A: 1**. |
| **Velocity Binding** | This defines the attribute used for velocity when generating ribbons. By default, this uses the **Particles.Velocity** variable if it exists; otherwise it uses the default of **X: 0, Y: 0, Z: 0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Normalized Age** | This defines the attribute used for normalized age when generating ribbons. By default, this uses the **Particles.NormalizedAge** variable if it exists; otherwise it uses the default of **0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Ribbon Twist Binding** | This defines the attribute used for ribbon twist when generating ribbons. By default, this uses the **Particles.RibbonTwist** variable if it exists; otherwise it uses the default of **0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Ribbon Width Binding** | This defines the attribute used for ribbon width when generating ribbons. By default, this uses the **Particles.RibbonWidth** variable if it exists; otherwise it uses the default of **1**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Ribbon Facing Binding** | This defines the attribute used for ribbon facing when generating ribbons. By default, this uses the **Particles.RibbonFacing** variable if it exists; otherwise it uses the default of **X: 0, Y: 0, Z: 1**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Ribbon Id Binding** | This defines the attribute used for ribbon ID when generating ribbons. Uses the **Particles.RibbonID** attribute if it exists, otherwise it uses the default **Index: 0 AcquireTag: 0**. |
| **Ribbon Link Order Binding** | This defines the attribute used for ribbon link order when generating ribbons. By default, this uses the **Particles.RibbonLinkOrder** variable if it exists; otherwise it uses the default of **0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Material Random Binding** | This defines the attribute used for material randoms when generating ribbons. By default, this uses the **Particles.MaterialRandom** variable if it exists; otherwise it uses the default of **0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Dynamic Material Binding** | This defines the attribute used for dynamic material parameters when generating instanced ribbons. Use the **Particles.DynamicMaterialParameter** if it exists, otherwise use the default of **X: 1, Y: 1, Z: 1, W: 1**. |
| **Dynamic Material 1Binding** | This defines the attribute used for dynamic material parameters when generating instanced ribbons. Use the **Particles.DynamicMaterialParameter1** if it exists, otherwise use the default of **X: 1, Y: 1, Z: 1, W: 1**. |
| **Dynamic Material 2Binding** | This defines the attribute used for dynamic material parameters when generating instanced ribbons. Use the **Particles.DynamicMaterialParameter2** if it exists, otherwise use the default of **X: 1, Y: 1, Z: 1, W: 1**. |
| **Dynamic Material 3Binding** | This defines the attribute used for dynamic material parameters when generating instanced ribbons. Use the **Particles.DynamicMaterialParameter3** if it exists, otherwise use the default of **X: 1, Y: 1, Z: 1, W: 1**. |

## Sprite Renderer

The Niagara Sprite Renderer has the following base parameters.

| Parameter | Description |
| --- | --- |
| Sprite Rendering |   |
| **Material** | Select the material used to render the particle. The material selected must have the **Use with Niagara Sprites** flag checked. |
| **Alignment** | This setting defines how the particle alignment is affected by other parameters. For example, the **Unaligned** setting indicates that only **Particle.SpriteRotation** and **FacingMode** parameters affect the alignment of the particle. |
| **Facing Mode** | This setting defines how the sprite particle orients itself relative to the camera. For example, the **Face Camera** setting indicates that the particle's origin will always attempt to align its axes to the camera's axes. |
| **Custom Facing Vector Mask** | This is used as a per-axis interpolation factor, along with the **CustomFacingVector** mode, to determine how the sprite particle orients itself to the camera. You can set the **X**, **Y**, and **Z** axes separately. A setting of **1.0** means the sprite particle is fully facing the custom vector. A setting of **0.0** uses the standard facing strategy. |
| **Pivot in UVSpace** | This setting determines the location of the pivot point for this particle. It follows the Unreal Engine's UV space, which has the upper left of the image at **0,0** and the bottom right of the image at **1,1** with the halfway point being at **0.5,0.5**. |
| **Remove HMD Roll** | Check this box to remove the HMD view roll in VR. |
| **Minimum Facing Camera Blend Distance** | The distance at which the FacingCameraDistanceBlend is fully FacingCamera. |
| **Maximum Facing Camera Blend Distance** | The distance at which FacingCameraDistanceBlend is fully FacingCameraPosition. |
| Sorting |   |
| **Sort Mode** | 
This determines how particles are sorted prior to rendering. Options are:

-   **None**: There is no particle sorting.
-   **View Depth**: This sorts by depth to the camera's near plane.
-   **View Distance**: This sorts by the distance to the camera's origin.
-   **Custom Ascending**: This sorts according to a per-particle attribute; lower values are rendered before higher values.
-   **Custom Descending**: This sorts according to a per-particle attribute; higher values are rendered before lower values.



 |
| **Sort Only When Translucent** | If this is checked, particles are only sorted when you are using a translucent material. |
| Sub UV |   |
| **Sub Image Size** | When you use Subimage lookups for your particles, this setting provides the number of columns (**X**) and rows (**Y**). |
| **Sub UV Blending Enabled** | If this is checked, the Sub Image UV lookup is blended with its next adjacent member, using the fractional part of the SubImageIndex float value as the linear interpolation factor (lerp). |
| Bindings |   |
| **Position Binding** | This defines the attribute used for positioning when generating sprites. By default, this uses the **Particles.Position** variable if it exists; otherwise it uses the default variable **Engine.Owner.Position**. The dropdown shows other variables that have the same data type as **Particles.Position**; however, those options probably do not make sense to use here. |
| **Color Binding** | This defines the attribute used for color when generating sprites. By default, this uses the **Particles.Color** variable if it exists; otherwise it uses the default of **R: 1, G: 1, B: 1, A: 1**. You can use any other attribute of a compatible type instead if you want to customize the data being fed into this renderer. |
| **Velocity Binding** | This defines the attribute used for velocity when generating sprites. By default, this uses the **Particle.Velocity** variable if it exists; otherwise it uses the default of **X: 0, Y: 0, Z: 0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Sprite Rotation Binding** | This defines the attribute used for rotation (in degrees) when generating sprites. By default, this uses the Particles.SpriteRotation if it exists; otherwise it uses the default of 0. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Sprite Size Binding** | This defines the attribute used for size when generating sprites. By default, this uses the **Particle.SpriteSize** variable if it exists; otherwise it uses the default of **X: 50, Y: 50**. You can use any other attribute of a compatible type instead if you want to customize the data being fed into this renderer. |
| **Sprite Facing Binding** | This defines the attribute used for facing when generating sprites. By default, this uses the **Particles.SpriteFacing** variable if it exists; otherwise it uses the default of **X: 1, Y: 0, Z: 0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Sprite Alignment Binding** | This defines the attribute used for alignment when generating sprites. By default, this uses the **Particles.SpriteAlignment** variable if it exists; otherwise it uses the default of **X: 1, Y: 0, Z: 0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Sub Image Index Binding** | This defines the attribute used for sprite sub image indexing when generating sprites. By default, this uses the **Particles.SubImageIndex** variable if it exists; otherwise it uses the default of **0**. You can use any other attribute of a compatible type; however, the options available in the dropdown may or may not make sense to use for this binding. |
| **Dynamic Material Binding** | This defines the attribute used for dynamic material parameters when generating sprites. By default, this uses the **Particles.DynamicMaterialParameter** if it exists; otherwise it uses the default of **X: 1, Y: 1, Z: 1, W: 1**. |
| **Dynamic Material 1Binding** | This defines the attribute used for dynamic material parameters when generating sprites. By default, this uses the **Particles.DynamicMaterialParameter1** if it exists; otherwise it uses the default of **X: 1, Y: 1, Z: 1, W: 1**. |
| **Dynamic Material 2Binding** | This defines the attribute used for dynamic material parameters when generating sprites. By default, this uses the **Particles.DynamicMaterialParameter2** if it exists; otherwise it uses the default of **X: 1, Y: 1, Z: 1, W: 1**. |
| **Dynamic Material 3Binding** | This defines the attribute used for dynamic material parameters when generating sprites. By default, this uses the **Particles.DynamicMaterialParameter3** if it exists; otherwise it uses the default of **X: 1, Y: 1, Z: 1, W: 1**. |
| **Camera Offset Binding** | This defines the attribute used for camera offset when generating sprites. By default, this uses the **Particles.CameraOffset** variable if it exists; otherwise it uses the default of **0**. You can select other compatible attributes from the dropdown menu. |
| **UVScale Binding** | This defines the attribute used for UV scale when generating sprites. By default, this uses the **Particles.UVScale** variable if it exists; otherwise it uses the default of **X: 1, Y: 1**. You can select other compatible attributes from the dropdown menu. |
| **Material Random Binding** | This defines the attribute used for material randoms when generating sprites. By default, this uses **Particles.MaterialRandom** if it exists; otherwise it uses the default of **0**. You can select other compatible attributes from the dropdown menu. |
| **Custom Sorting Binding** | This defines the attribute used for custom sorting. By default, this uses the **Particles.NormalizedAge** variable if it exists; otherwise it uses the default of **0**. You can select other compatible attributes from the dropdown menu. |
| **Normalized Age Binding** | This defines the attribute used for custom sorting. By default, this uses the **Particles.NormalizedAge** variable if it exists; otherwise it uses the default of **0**. You can select other compatible attributes from the dropdown menu. |
| Cutout |   |
| **Use Material Cutout Texture** | If this is checked, use the cutout texture from the Material Opacity Mask; if none exist, use the cutout texture from Material Opacity. |
| **Cutout Texture** | Select the texture to create the bounding geometry from. |
| **Bounding Mode** | Set the number of bounding vertices. More bounding vertices results in reduced overdraw, but adds more triangle overhead. The eight vertex mode is best used when the Sub UV texture has a lot of space to cut out that is not captured by the four vertex mode, and when the particles using the texture will be few and large. |
| **Opacity Source Mode** | 

This setting has the following options:

-   **OSM Alpha**
-   **OSM Color Brightness**
-   **OSM Red Channel**
-   **OSM Green Channel**
-   **OSM Blue Channel**



 |
| **Alpha Threshold** | Alpha channel values larger than the threshold are considered occupied and will be contained in the bounding geometry. Raising this threshold slightly can reduce overdraw in particles using this animation Asset. |
| Sort Order |   |
| **Sort Order Hint** | By default, emitters are drawn in the order they are added to the stack in a Niagara system. The **Sort Order Hint** value allows you to control the draw order in a more detailed way. Materials of the same type will draw in order from lowest Sort Order value to highest within the system. The default value is **0**. |

## Decal Renderer

Use the **Decal Renderer** to spawn and project decals onto surfaces. The Decal Renderer uses the same technology as the Decal Actor. For more information, see [Decal Actors](/documentation/en-us/unreal-engine/decal-actors-in-unreal-engine).

Because decals only show up when they are projected onto a surface, you will not see anything in the Preview window when you add a Decal Renderer. There are two ways around this.

1.  Add the Niagara system to your level.
2.  Add a floor in the Preview window.

If you add the Niagara system to your level, you can open the Niagara Editor in a separate window and place the Niagara Editor and the Level Editor side-by-side to easily tweak the values.

Click image for full size.

If you want to add the floor to the Preview pane, from the Niagara Editor, select **Window > Preview Scene Settings**. From there, you can add the floor and adjust other visual parameters of the preview. The decals will then be projected onto the floor, so long as they are pointing at it.

You can set the following parameters in a Decal Renderer.

| Parameter | Description |
| --- | --- |
| **Material** | Choose the material to bind to that contains your decal. |
| **Material Parameter Binding** | Bind the material to a variable in order to override the material at runtime. |
| **Source Mode** | When set to Particles, decals will be rendered for each particle in the simulation. When set to Emitter, only one decal will be rendered for the emitter. |
| **Renderer Visibility** | Use a renderer visibility tag to show particles with that tag, and hide particles without it. |
| **Decal Screen Size Fade** | Set the decal screen size to reduce the number of small decals shown. |

Use the following bindings with the Decal Renderer. Each binding is linked to default variables, though you can override any of them.

| Binding | Description |
| --- | --- |
| **Position Binding** | Defines the center of the decal. It is bound to the variable `Particles.Position` by default. |
| **Decal Orientation Binding** | Sets the orientation of the decal. It is bound to the variable `Particles.DecalOrientation` if it exists. If it does not, it defaults to the orientation X: -0.5, Y: 0.5, Z: 0.5, W: 0.5. |
| **Decal Size Binding** | Defines the size of the decal. It is bound to the variable `Particles.DecalSize` if it exists. If it does not, it defaults to X: 50, Y: 50, Z: 50. In this case, X is the vertical size. For more information, see [Decal Actors](/documentation/en-us/unreal-engine/decal-actors-in-unreal-engine) |
| **Decal Fade Binding** | Defines the value for the decal's fade. You can query this value using the Decal Lifetime Opacity material node. This defaults to the variable `Particles.DecalFade` if it exists. If it does not, it defaults to 1. |
| **Decal Color Binding** | Defines the color for the decals. This is bound to the variable `Particles.Color` by default. |
| **Decal Visible Binding** | Defines whether the decal should be visible. This works together with `RendererVisibilityTagBinding` to determine visibility. Defaults to the variable `Particles.DecalVisible` if it exists. Otherwise, defaults to true. |
| **Renderer Visibility Tag Binding** | When the Visibility tag returns values, those values are compared to the Renderer Visibility Tag Binding. Defaults to the variable `Particles.VisibilityTag` if it exists, otherwise defaults to 0. |
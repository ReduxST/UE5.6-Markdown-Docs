# Substrate Materials Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:14

---

Substrate is Unreal Engine 5's approach to authoring materials, which replaces the fixed suite of shading models and blend modes, such as Default Lit and Clear Coat, with a more expressive and modular framework.

Certain abstractions of the non-Substrate (or legacy) material system are done away with by Substrate — it replaces them with measured properties of matter. This creates wider parameter space from which to work and makes it possible to more accurately blend between discrete surface types like metal, glass, and plastic. Substrate also streamlines the process of layering materials, making it easier to represent surfaces like liquid on metal, or a clear coat over subsurface scattering.

Materials in Substrate are conceptualized as "slabs of matter." These slabs are a principled BSDF (bidirectional scattering distribution function) representation, parameterized by physical quantities with well-defined units. Materials are expressed as a graph of slabs on which operations are performed (like mixing and layering). Because of their principled representation, Substrate Materials can be simplified according to the capacity of a platform in order to trade visual quality for performance.

## Enabling Substrate

To enable Substrate Materials in your project:

![Enable Substrate Materials](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8078a057-918c-464d-bd4f-58bc16d2f4fb/enable-substrate.png)

1.  Open the **Project Settings** and go to **Engine > Rendering**.
2.  Under the **Substrate** section, enable **Substrate materials (Experimental)**.
3.  Follow the prompts and messages to **Restart** the project.
    
    ![Restart engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88d5191c-2bcf-4f2f-9098-da54230a1fd5/restart-engine.png)
    
    We recommend using **DirectX 12 (DX12)** on Windows. Substrate works with DirectX 11 (DX11) but has several issues and requires further testing. For more information, see the [Limitations and Known Issues](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#limitationsandknownissues) section of this page.
    

### Optional Project Settings and Console Variables

Substrate includes these optional project settings and console variables:

![Substrate optional settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7e89bb3-ed82-4f06-83e0-0a9d87b03d6b/substrate-optional-project-settings.png)

| Property | Description |
| --- | --- |
| Project Settings |   |
| **Substrate opaque material rough reflection** | 
When enabled, rough surfaces coating other materials can blur the lower layers in a physically plausible way.

This feature is experimental.



 |
| **Substrate advanced visualization shaders** | Enabling this option generates shaders required for advanced debugging view modes. These shaders can impact performance and should only be enabled if you need to debug Substrate material topology. For more information, see [Substrate Debug View Modes](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substratedebugviewmodes). |
| Console Variables |   |
| `r.Substrate.BytesPerPixel` | Provides a means to specify the storage bytes-per-pixel of a Substrate material before it is automatically simplified. This variable is set to 80 bytes per pixel by default. You can increase it for complex materials with higher storage requirements. Higher values use more memory, and can affect memory bandwidth and other performance characteristics. The relationship of this variable to performance is very dependent on both the content and the platform. You can specify this value on a per-platform basis in the platform.ini configuration file if necessary. |

### Converting Legacy Materials

Substrate materials **cannot** be reverted to a non-Substrate Material. Conversions are permanent once opened and saved. We advise you to save a backup copy of your project before enabling Substrate.

Existing materials are automatically converted to a Substrate Material when opening them for editing in a Substrate-enabled project. These are converted to a Substrate-style shading network using the **Substrate Shading Models** node.

The example above shows a "legacy" material that has been opened with Substrate enabled for the project and the resulting material graph with nodes now plugged into the Substrate Shading Models node.

Follow these guidelines when enabling Substrate in an existing project:

-   Opening an existing non-Substrate material in a Substrate-enabled project automatically converts it to a "legacy" Substrate material when you save the material. The conversion is permanent and cannot be reverted to a non-Substrate material.
-   Substrate Materials renders black if Substrate is disabled for the project. This includes any legacy Substrate materials that were created from converted materials. You can manually rewire any converted Substrate material to a legacy-style material but this will not get rid of the Substrate nodes that are now in the material graph.

## Substrate's Relationship to Material Layers

Traditional **Material Layering** in Unreal Engine (both [graph-based](/documentation/en-us/unreal-engine/layered-materials-in-unreal-engine) and in the [custom layers GUI](/documentation/en-us/unreal-engine/using-material-layers-in-unreal-engine)) are based on the concept of parameter blending. Each layer defines a pattern graph of parameters which are blended and fed into the final shading model.

There is nothing preventing material layer-driven parameters from feeding into a Substrate-defined shading model. However, you would need to set this logic up manually using the output of a [Material Attribute](/documentation/en-us/unreal-engine/material-attributes-expressions-in-unreal-engine) node in the parent material. A limitation of this approach is that the Material Attributes systems has a fixed list of parameters, but there might not be enough slots to feed into a multi-slab setup with Substrate — it might require using pins arbitrarily and unrelated to their true meaning.

Substrate can natively use [parameter blending](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#parameterblendingwithoperators), as described later in this page, but there is no way to access that functionality from the Material Layers interface. **Unifying Substrate and Material Layers is a strong area of interest for future development.**

## Working with Substrate Materials

Substrate Materials are authored similarly to legacy materials. This section covers the key elements that make up Substrate Materials, including its nodes, blend modes, and details on the types of materials you can create.

### Substrate Material Root Node

Like legacy materials, the **Material Root** node is where Substrate slabs and other Substrate nodes, like operators and building blocks, are fed into.

![Substrate Material Root Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e29c819c-35ff-4178-b18a-ca9ce0ad8f15/material-root-node.png)

Also like legacy materials, you'll use the **Details** panel when the Material Root node is selected to set the **Blend Mode** and other properties that define the look of the material.

![Setting the Substrate Blend Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41c555af-6c0e-4fb8-ac31-0153da384c96/substrate-blend-modes.png)

All Substrate Material graphs must be connected to the **Front Material** input on the Material Root node. This input is the end-point of every Substrate graph.

![Material Root Node Front Material Input](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39524255-a5ef-486f-894f-454d694c8787/material-root-front-material-input.png)

#### Substrate Blend Modes

Substrate uses its own set of [Blend Modes](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substrateblendmodes) to define how the material's color is blended with the background. Legacy material blend modes are limited in how they can mix and blend with one another, thus limiting the types of materials they can create. Substrate offers a broader selection of blend modes that can blend together to create all sorts of materials. This is especially important for achieving physically correct translucent surface shading.

Substrate includes the following Blend Modes:

![Select a Substrate Blend Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8424ca4e-0db5-4a41-b036-fe953e78ebc0/substrate-blend-mode-selection.png)

| Blend Mode | Description |
| --- | --- |
| **Opaque** | Defines a surface through which light neither passes nor penetrates. An opaque surface with coverage of 1. This is the same as the legacy Opaque Blend Mode. |
| **Masked** | Used for materials that need to selectively control visibility in a binary (on / off) fashion. An opaque surface with coverage of 1 or 0. This is the same as the legacy Masked Blend Mode. |
| **TranslucentGreyTransmittance** | A translucent Material with colored surface and coverage, but transmittance reduced to grayscale. This is faster, as it prevents the extra render of post depth-of-field translucency into a modulate pass. This is the fallback Blend Mode for platforms not supporting hardware colored translucency (called dual source color blending). [This is similar to the legacy Translucent Blend Mode](/documentation/en-us/unreal-engine/lit-translucency-in-unreal-engine#thintranslucency). |
| **Additive** | Adds the color of the Material to the color of the background where Final Color = Source Color + Dest color. |
| **ColoredTranslucencyOnly** | Only the transmittance of the Material is used. Surface interactions are reduced to 0. This is the same as the legacy Multiply Blend Mode. |
| **AlphaComposite (Premultiplied Alpha)** | This Blend Mode provides finer control over what parts of a material are blended additively and what parts are blended translucently using the opacity input. Works the same as the legacy Alpha Composite (Premultiplied Alpha) Blend Mode. |
| **AlphaHoldout** | This blend mode holds out the alpha making it possible to punch a hole through objects to reveal the objects behind it. Works the same as the legacy AlphaHoldout Blend Mode. |
| **TranslucentColoredTransmittance** | A fully-featured translucent material with colored surface, coverage, and colored transmittance. This is more expensive when using separate translucency when post depth of field since it will have to render the transmittance component in a separate buffer, similarly to the legacy ThinTranslucent shading model. |

Substrate makes working with translucency more straightforward than traditional materials do — translucent Blend Modes are better defined by their intent. One aspect that remains unchanged between the two is that any translucent Blend Mode must also set a **Lighting Mode** to define how lighting is calculated for its surface. This is important to achieve the correct look for translucent materials.

The vast majority of translucent materials you create will use **Surface Translucency Volume** or **Surface Forward Shading**.

The following Lighting Modes are available to choose from:

| Lighting Modes | Description |
| --- | --- |
| **Volumetric NonDirectional** | Lighting is calculated for a volume without directionality. Use this on particle effects like smoke and dust. This is the cheapest per-pixel lighting method. However, the material normal is not taken into account. |
| **Volumetric Directional** | Lighting is calculated for a volume with directionality so that the normal of the material is taken into account. Note that default particle tangent space is facing the camera, so enable Generate Spherical Particles to get a more useful tangent space. |
| **Volumetric PerVertex NonDirectional** | Same as Volumetric NonDirectional but lighting is only evaluated at vertices so the pixel shader cost is significantly less. Note that lighting still comes from a volume texture, so it is limited in range. Directional Lights become unshadowed in the distance. |
| **Volumetric PerVertex Directional** | Same as Volumetric Directional but lighting is only evaluated at vertices so the pixel shader cost is significantly less. Note that lighting still comes from a volume texture, so it is limited in range. Directional Lights become unshadowed in the distance. |
| **Surface Translucency Volume** | Lighting is calculated for a surface. The light is accumulated in a volume so the result is blurry, and has limited distance but the per-pixel cost is very low. Use this on translucent surfaces like glass and water. Only diffuse lighting is supported. |
| **Surface ForwardShading** | Lighting is calculated for a surface. Use this on translucent surfaces like glass and water. This is implemented with forward shading so specular highlights from local lights are supported, however many deferred-only features are not. This is the most expensive translucency lighting method as each light's contribution is computed per-pixel. |

For some examples of setting up and using translucency in a Substrate Material, see the [Translucency](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#translucencyandblendmodes) section of this page.

### Substrate Slab

The **Substrate Slab** is the elementary building block from which one assembles a Substrate Material. It is designed to be the minimum necessary set of parameters with which the vast majority of material appearances can be achieved. As such, it is the basis of a much more expressive type of appearance authoring.

A slab is a principled representation of a slab of matter that is composed of an **interface** and a **medium**.

![Composition of a Substrate Slab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88a8ef60-93bb-465a-a8b8-2017b9e394db/substrate-slab-composition.png)

The composition of a Substrate Slab: The interface (1) and the medium (2).

1.  The **interface** is the boundary where light interacts with the material's surface. The properties of the interface are primarily defined by the Roughness, Normal, Diffuse Albedo, F0 and F90 values fed into them.
2.  The **medium** is the volume of matter beneath the interface where light is scattered, transmitted, and absorbed. The properties of the medium are primarily defined by the [Mean Free Path](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#subsurfacescatteringandparticipatingmedia) (or MFP) inputs.

The Substrate Slab is a modular replacement for the monolithic Material root node in non-Substrate Materials. It is made up of multiple surface attributes, such as Diffuse, Specular, Roughness, Emissive, Cloth, Anisotropy, and many more. All [Substrate BSDF nodes](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substratebsdfnodes) contain properties that are relevant to their named output for the type of material they produce, such as eye, hair, simple clear coat, and so on.

Traditional Materials relied on their Blend Mode to present inputs that can be used. Substrate uses its different BSDF slabs to define the type of material. And because these are not tied directly to Blend Modes any longer they can be layered and mixed to produce varying types of materials.

|   |   |
| --- | --- |
| ![Legacy Material Root Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3f0beb9-4097-4963-83d0-e7c23532028a/legacy-material-root-node.png) | ![Substrate Slab with Material Root Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4707713-1d1a-4701-8962-22e1fe8375ac/substrate-material-root-node.png) |
| Legacy Material Root Node | Substrate Slab and Material Root Node |

The primary **Substrate Slab BSDF** node used includes the following inputs:

| Substrate Slab Inputs | Definition |
| --- | --- |
| **Diffuse Albedo** | Defines the percentage of light reflected as diffuse from a surface. This is similar to the local base color of the medium. The default value is 0.18. |
| **F0** | Defines the color and brightness of the specular highlight where the surface is perpendicular to the camera. For dielectric Materials (plastics and other non-metals), this value is typically in the 0 - 0.08 range. For metallic Materials it can range up to 1. Gemstones are in a range up to around 0.16. |
| **F90** | Defines the color of the specular highlight where the surface normal is 90 degrees from the camera. In other words, at grazing angles relative to the camera view. Only hue and saturation are perceived, as brightness is fixed at 1.0 This fades to black as F0 drops below 0.02. |
| **Roughness** | Controls how rough the material is. The roughness of the surface from 0 to 1. At 0 (smooth), roughness is a mirror reflection. At 1 (fully rough), roughness is completely matte or diffuse. When anisotropy is used, the roughness value is used along the tangent axis. |
| **Anisotropy** | Controls the anisotropy direction of the Material (-1: highlight aligned to the bi-tangent, 1: highlight is aligned with the tangent). |
| **Normal** | Take the surface normal as input. The normal is considered tangent or world space according to the space properties on the materia root node. This input defines the shading normal per-pixel. |
| **Tangent** | Take a surface tangent as input. The normal is considered tangent or world space according to the space properties on the material root node. This input defines the shading tangent per-pixel. |
| **SSS MFP** | 
Subsurface scattering Mean Free Path (MFP). This controls the density of the material, and influences the absorption and scattering of light by the Material. More precisely, this defines the average distance at which a photon interacts with a particle of matter. This distance is controlled per color channel.

This input is only used when there is not any Subsurface Profile asset assigned to the material root node.



 |
| **SSS MFP Scale** | 

This input scales the subsurface scattering mean free path radius of the subsurface profile to a value between 0 and 1.

This input is only used when there is not any Subsurface Profile asset assigned to the material root node.



 |
| **SSS Phase Anisotropy** | Positive values elongate the phase function along the light direction, causing forward scattering. Negative values elongate the function backward along the light direction, causing back scattering. |
| **Emissive Color** | Controls the emissive color on top of material surfaces. |
| **Second Roughness** | 

Controls the roughness of a secondary specular lobe. At 0 (smooth), roughness is a mirror reflection. At 1 (fully rough), roughness is completely matte or diffuse.

This input does not influence diffuse roughness.



 |
| **Second Roughness Weight** | The mix factor between the primary and secondary specular lobe. The first specular using Roughness has a weight of (1 - SecondRoughnessWeight). Values equal to 0 renders the primary lobe only. 0.5 renders a 50% mix of both roughnesses, and 1.0 renders the secondary lobe only. |
| **Fuzz Roughness** | 

Controls how rough the Fuzz layer is. Fuzz with a roughness of 0 is smooth (shinier) and 1 is fully rough (matte).

If no value is connected to this input, the Roughness input is used instead.



 |
| **Fuzz Amount** | Adds a fuzz-like layer at the interface, causing color retroreflectivity. This controls the amount of fuzz applied on top of a surface layer. Usually used to create fabric Materials. |
| **Fuzz Color** | Defines the color of the fuzz layer. |
| **Glint Density** | 

The logarithm representation of micro facet density on the surface of a material.

Requires `r.Substrate.Glints=1` to be set in the ConsoleVariables.ini configuration file.



 |
| **Glint UVs** | 

Controls the position and scale of glints on the surface of a material.

Requires `r.Substrate.Glints=1` to be set in the ConsoleVariables.ini configuration file.



 |

### Substrate Material Nodes

You can use the following types of nodes to author a Substrate material:

| Type of Node | Description |
| --- | --- |
| [BSDFs](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substratebsdfnodes) | These nodes represent most types of surfaces, from simple materials to more complex ones like hair, eyes, and water. |
| [Operators](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substrateoperatornodes) | These nodes mix and layer multiple Substrate Slab BSDFs to create complex and varied surfaces. |
| [Building Blocks](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substratebuildingblocknodes) | These nodes translate common material types for use with Substrate, like creating a coated layer or the default legacy material shading model of Unreal Engine. |
| [Extras](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substrateextrasnodes) | These nodes define a Material Domain for a Substrate Material, and are directly analogous to their legacy Material Domain namesakes. |
| [Helpers](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substratehelpernodes) | These nodes are used to do some conversion within the material, such as mapping transmittance to Mean Free Path for a Substrate Slab. |

#### Substrate BSDF Nodes

Substrate **BSDF** (Bidirectional Scattering Distribution Function) nodes are used to represent most types of surfaces, they control the visual look of materials you author and automatically set their domain and shading model accordingly. The goal is to remove these aspects from being manually set on the material root node through the Details panel.

Substrate includes the following BSDFs:

![Substrate BSDF Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bdeb349-db88-4a28-ae27-20d8424f3f5f/substrate-bsdf-nodes.png)

The Slab BSDF is the primary node for authoring in Substrate and can be layered with other slabs. The other BSDFs are for specialized use cases and must be used on their own without mixing with other BSDFs.

| Substrate BSDF Node | Description |
| --- | --- |
| **Substrate Slab BSDF** | The principled representation of a slab of matter that aggregates multiple components: diffuse, specular, haziness, cloth fuzz, and anisotropy. It can render effects such as opaque subsurface or translucent scattering and translucent transmittance subsurface scattering. |
| **Substrate Eye BSDF** | A BDFS dedicated to rendering eye materials with Substrate. This includes specific inputs for the cornea and iris. |
| **Substrate Hair BSDF** | A BDFS dedicated to rendering hair materials with Substrate. |
| **Substrate Simple Clear Coat** | Provides a simple and fast way to render a material with a clear top coat. This node uses the Substrate Slab BSDF in the background, but simplifies the workflow for clear coat rendering. It is optimized to render legacy Clear Coat materials. |
| **Substrate SingleLayerWater BSDF** | A BSDF dedicated to rendering of a [Single Layer Water](/documentation/en-us/unreal-engine/single-layer-water-shading-model-in-unreal-engine) material primarily used with the [Water](/documentation/en-us/unreal-engine/water-system-in-unreal-engine) system. |
| **Substrate Unlit BSDF** | 
A BSDF used to render unlit elements with a colored emissive luminance. This Substrate node replaces legacy grayscale opacity with colored transmittance.

If you need to blend an Unlit Slab, use a regular Substrate Slab with only Emissive Color input being used.



 |
| **Substrate Volumetric-Fog-Cloud BSDF** | A BSDF used to represent a participating medium. This node is used to render [Volumetric Fog](/documentation/en-us/unreal-engine/volumetric-fog-in-unreal-engine) and [Volumetric Clouds](/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine). |

#### Substrate Operator Nodes

**Substrate Operator** nodes mix or layer multiple [Substrate Slabs](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substrateslab) to create complex and varied surfaces. If the Substrate Slab represents a piece of matter, Operators present ways to combine those pieces.

The following Substrate Operators are available to choose from:

![Substrate Operator Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b52df41b-4aca-4fe2-9cb1-e3657300a048/substrate-operator-nodes.png)

Substrate Operators do not work with all [Substrate BSDFs](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substratebsdfnodes). Only **Substrate Slab BSDF** and **Substrate Simple Clear Coat** can use these Operator nodes.

| Substrate Operator Node | Description |
| --- | --- |
| **Substrate Coverage Weight** | This operator takes input from a Slab and controls the amount of coverage it has where Weight is the amount of coverage. Reducing the weight reduces the coverage of matter of the slab, meaning you will see through to the matter underneath. This node should be used in conjunction with the Substrate Vertical Layer operator to have opaque matter on top of another, like dust and dirt layers where you want to control how much they cover the surface below. |
| **Substrate Horizontal Blend** | This operator takes input from two Slabs: a Background and Foreground. The Mix input controls how much these two Slabs mix together using a linear interpolation. |
| **Substrate Vertical Layer** | This operator takes input from two Slabs: a Top and Bottom layer. The bottom Slab is coated by the top Slab with the bottom layer's appearance influenced by the properties of the top layer. Use the Top Thickness input to control how thick the top layer is over the bottom. This operator is ideal for creating car paints, wood varnishes, and wetness on a surface. |
| **Substrate Add** | 
This operator takes input from two Slabs and adds them together. The material created is not physically plausible because it creates more outgoing energy from the surface than incoming energy.

This node should be avoided whenever possible.



 |

Operator nodes include an option to blend their background and foreground into a single material when toggling on **Use Parameter Blending**. Because Substrate Operators can create complex material appearances by mixing and layering slabs together, their expense at runtime (primarily due to lighting evaluation) can be costly to performance. Parameter blending is an optimization that trades expensive lighting evaluation for runtime performance and less costly lighting evaluation.

For more information on this parameter blending optimization, see the [Parameter Blending](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#parameterblendingwithoperators) section of this page.

##### Substrate Coverage Weight

The **Substrate Coverage Weight** Operator controls the ratio of two slabs in a vertical layering operation. The **Weight** input drives the coverage of this material when layering together with a [Substrate Vertical Layer Operator](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substrateverticallayer) (like the example below). You can also use the operator to achieve translucent surfaces when using alpha-as-coverage or alpha-as-opacity, similar to how the Translucent Blend Mode uses opacity.

![Substrate Coverage Weight](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/531a4cb6-bccd-41d0-a8db-de5ebc28adde/substrate-coverage-weight.png)

The graph above uses the **Substrate Coverage Weight** Operator, where **Weight** drives the amount of coverage applied over the bottom slab. A weight of 1 is fully opaque, blocking the green textured pattern. 0.5 is 50% transparent, mixing the two materials' colors and showing the texture pattern. 0 is fully transparent and shows only the green textured pattern.

![Substrate Coverage Weight Examples](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2849b4d1-e9d7-4ec7-abd3-44cda7517d16/substrate-coverage-weight-examples.png)

Because the **Weight** input takes a Float3 value, you can also use a texture to drive the amount of coverage applied to the slab when layering materials.

##### Substrate Horizontal Layer

The **Substrate Horizontal Layer** Operator mixes two slabs together, one representing the background and the other the foreground. The **Mix** input controls their mixture ratio using linear interpolation.

![Substrate Horizontal Blend Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1146f187-fe34-4ce5-937e-c846d8d572cf/substrate-horizontal-blend-node.png)

The **Background** input is fully visible when it is **0**, and the **Foreground** is fully visible when it equals **1**. When the mix ratio is **0.5**, the slabs are mixed together, and the mix is evaluated per-pixel. The Mix input can use textures to control the mix ratios, like the example below.

![Substrate Horizontal Blend Example Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1f61be4-24b4-4d25-afcc-32b88eb42721/substrate-horizontal-blend-material-example.png)

##### Substrate Vertical Layer

The **Substrate Vertical Layer** Operator takes a slab on its **Top** and **Bottom** inputs and layers them together. This node takes into account the thickness of the top layer to apply physically correct transmittance and scattering, which is similar to a coating operation, with the top layer covering the bottom layer. The appearance of the Bottom slab is dependent on the properties of the Top slab. If the BSDF passed into the Top input is fully opaque, the bottom slab is not seen at all.

![Substrate Vertical Layer Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16e1f184-42f0-4084-944f-0d31c80990b0/substrate-vertical-layer-node.png)

Vertical layering is particularly useful in situations that call for a transparent, or semi-transparent, top coat over an opaque bottom layer. Examples include car paint, varnished wood surfaces, or wetness on a surface, such as puddles of water.

##### Substrate Add

The **Substrate Add** Operator combines two slabs and outputs their result. This operator is not considered physically plausible because it can produce a material where the outgoing energy from the surface exceeds the incoming energy. It is useful when art direction is more important than being physically plausible. However, to maintain physically accurate surfaces, this operator should be avoided.

![Substrate Add Node Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08ddc8c6-20fc-4799-9ef8-0e16b93216eb/substrate-add-node-example.png)

#### Substrate Building Block Nodes

The **Substrate Building Block** nodes are a set of [Material Functions](/documentation/en-us/unreal-engine/material-functions-in-unreal-engine) that provide translations for some common use cases. Because these are material functions, you can open and inspect them directly.

The following Substrate Building Blocks are available to choose from:

![Substrate Building Block Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c3d39a5-956f-461d-b2c0-a97a41752e1a/substrate-building-block-nodes.png)

| Substrate Building Block Node | Description |
| --- | --- |
| **Substrate Coated Layer** | A material function that creates a coated material made of two slabs layered on each other. It exposes user-friendly parameters to control the coat interface and absorption. |
| **Substrate Standard Surface Opaque** | A material function that creates an uber-shader-like Substrate material with a user-friendly parameterization for opaque surfaces. The parameterization uses industry standard vocabulary and notions. |
| **Substrate Standard Surface Translucent** | A material function that creates an uber-shader-like Substrate material with a user-friendly parameterization for translucent surfaces. The parameterization uses industry standard vocabulary and notions. |
| **Substrate UE4 Default Shading** | A material function that replicates the default shading model with Substrate for diffuse, metallic, and specular parameterization used in non-Substrate Materials. |
| **Substrate UE5 Unlit Shading** | A material function that recreates the UE4 Unlit shading model with Substrate. |

#### Substrate Extras Nodes

The **Substrate Extras** nodes specify the type of material and function it serves, such as setting the Substrate material to be used as a decal or light function. These nodes are directly analogous to non-Substrate Materials that were assigned them as part of their Material Domain.

The following Substrate Extras are available to choose from:

![Substrate Extras Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90c0539d-f6c8-450f-bb74-1f3ab27b0b62/substrate-extras-nodes.png)

These nodes are monolithic and must be used in isolation. They are not compatible with [Substrate Operators](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substrateoperatornodes).

As a good habit, we recommend placing these nodes at the end of the material graph, right before plugging into the **Front Material** input.

| Substrate Extras Node | Description |
| --- | --- |
| **Substrate Convert To Decal** | Any material graph can be used as a decal. This node specifies the material will be converted and used as a Decal material only. |
| **Substrate Light Function** | This node specifies the material will be used as a [Light Function](/documentation/en-us/unreal-engine/using-light-functions-in-unreal-engine) only. It must be used in isolation. |
| **Substrate Post Process** | This node specifies the material will be used as a [Post Process Material](/documentation/en-us/unreal-engine/post-process-materials-in-unreal-engine) only. It must be used in isolation. |
| **Substrate UI** | This node specifies the material will be used as a User Interface element only, such as ones designed to be used with [UMG UI Designer](/documentation/en-us/unreal-engine/umg-editor-reference-for-unreal-engine). It must be used in isolation. |

For example, when using the **Substrate Convert To Decal** node, any Substrate Material can be used as a decal material applied to Mesh Decals and Decal Actors in the scene.

Extras nodes automatically set the **Material Domain** when connected to the **Front Material** input of the **Material Root** node. Some Extras nodes require the [Blend Mode](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substrateblendmodes) to be changed to support the output.

![Substrate Convert-to-Decal example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32f17681-4664-4f8c-8163-569d428ac8e1/substrate-convert-to-decal-node.png)

When using the **Substrate Convert To Decal** node, you must set the Blend Mode to **TranslucentGrey Transmittance**, **Colored Transmittance**, **TranslucentColorTransmittance**, or **AlphaComposite (Premultiplied Alpha)**. Otherwise, an error is displayed in the **Stats** panel of the Material Editor.

#### Substrate Helper Nodes

The **Substrate Helper** nodes are a set of nodes and material functions to perform some conversion or achieve something that legacy materials could do.

![Substrate Helper Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc852aaf-fe16-4ef0-bc78-61a710a01dd7/substrate-helper-nodes.png)

| Substrate Helper Node | Description |
| --- | --- |
| **Substrate Flip Flop** | Controls the surface reflectivity based on the view incident angle. It allows interpolations of a normal-facing color (F0) to a grazing-angle color (F90), based on the view angle, and it controls the interpolation speed with the falloff parameter. |
| **Substrate Haziness-To-Secondary-Roughness** | Compute a second specular lob roughness from a base surface roughness and haziness. This parameterization ensures that the haziness makes sense physically and is perceptually easier to author. |
| **Substrate IOR-To-F0** | Convert a dielectric IOR into a F0 value. |
| **Substrate Metalness-To-DiffuseColorF0** | Convert a metalness parameterization (BaseColor / Specular / Metallic) into DiffuseAlbedo / F0 parameterization. |
| **Substrate Rotation-To-Tangent** | Convert a rotation angle into a tangent vector. |
| **Substrate Thin-Film** | Compute the resulting material specular parameters F0 and F90 according to input surface properties as well as the thin film parameters. |
| **Substrate Transmittance-To-MeanFreePath** | Convert a transmittance color corresponding to a Slab of participating media viewed perpendicularly to its surface. This node directly maps to the Slab BSDF Input. |
| **Substrate View-Dependent-Coverage** | Adapts the coverage based on the view-incident angle. This node is useful for mixing a layer whose thickness is large enough to imply a view-dependent effect. For instance, large grains of dust would have greater occlusion at a grazing angle compared to an incident angle. |

### Additional Notes about Substrate Nodes

-   **Substrate Decal Materials**
    -   Substrate Decals currently use the same features as the legacy Decals blend mode path.
    -   Future versions of Substrate Decals look to offer a more robust feature set similar to other features already available with Substrate, like Layer Translucent Slabs for things like water, blood, and goo. For example, having layers that can erode according to thickness like car paint scratches, ground steps, and tire marks.
-   **Substrate Shading Models Node**
    
    -   Opening any prior created material once Substrate is enabled for your project automatically converts the material to use its slabs. All existing inputs are fed into a **Substrate Shading Model** node.
    
    ![Substrate Shading Models Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23b5bbe5-5519-4cc4-9b20-91d8ffb0511d/substrate-shading-models-node.png)
    
    Avoid manually adding or using this node when creating new Substrate materials.
    

### Substrate Stats Panel

The **Substrate** stats panel is available in the Material Editor below the Material Graph.

![Substrate Stats Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/781b8b69-ca89-4ce7-8523-8548fc0b3a83/substrate-stats-panel-1.png)

The Substrate panel displays stats about the material, simplification, and topology.

![Substrate Stats Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3fec3a9-937a-4d3f-a5a1-211797da804f/substrate-stats-panel-2.png)

### Parameter Blending with Operators

Using multiple BSDFs (Bidirectional Scattering Distribution Functions) per pixel slows the rendering process proportionally to their count in the material graph. It is twice as slow to evaluate the lighting for two BSDFs as it is a single one. This is true for both opaque and translucent surfaces.

Operator nodes include a **Use Parameter Blending** checkbox that attempts to optimize the performance and memory footprint of the material while maintaining the appearance of all the mixing and layer operations in the graph. Only the rightmost Operator node before the Material Root node must have the setting enabled. All other nodes in the graph automatically apply parameter blending.

Parameter blending is a good fallback option when the performance of multiple Slabs in a material is a concern. When enabled, two Slabs are merged into a single Slab that needs only a single lighting evaluation. This merge uses a lot less memory than two individual slabs.

![Substrate Operators Use Parameter Blending checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92420614-d77f-445e-820c-d116b2206845/substrate-use-parameter-blending.png)

The example materials below are taken from [Content Examples Substrate Level](https://www.fab.com/listings/4d251261-d98c-48e2-baee-8f4e47c67091) without and with **Use Parameter Blending** enabled.

This material (M\_Substrate\_ShaderBall\_IceRocks) uses two BSDFs. The left is without any blending and the right is using parameter blending.

![Substrate Parameter Blending Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae496f9f-2caa-4ed1-be96-644a3f499bbc/parameter-blending-example-1.png)

This is a more complex material (M\_Substrate\_ShaderBall\_AnisoOverSSS) that blends four slabs using two Vertical Layer Operators and a single Coverage Weight Operator. The material has a memory cost of 108 bytes per pixel. With Use Parameter Blending enabled, blending on all operators comes down to 28 bytes per pixel. The left material is without any blending and the right uses parameter blending.

![Substrate Parameter Blending Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d606604f-4887-463c-b3a0-47831f31a5b5/parameter-blending-example-2.png)

Aside from Parameter Blending on Operators nodes, you can use one of the following workflows to achieve similar results:

-   Blend the DiffuseAlbedo, F0, F90, Roughness, and other attributes manually in the graph. Pass all the attributes into a single Slab connected to the Front Material input. This approach can work well for isolated cases but may become unmanageable for a large library of complex materials.
-   Use the graph-based [Layered Materials](/documentation/en-us/unreal-engine/layered-materials-in-unreal-engine) workflow. Since it employs material functions to reuse work, this can scale better than the first option.

On lower end platforms, such as mobile, the compiler automatically enables parameter blending for the sake of performance. On intermediate platforms, parameter blending is progressively introduced on the bottom layers of a material in order to remain within the target performance and memory constraints.

### Metalness and Specular Response

The parameterization used by Substrate differs from the DefaultLit Shading Model in non-Substrate (or legacy) materials — there is no longer a Metallic input. This parameterization attempts to do away with abstracted values (like metallic and specular) and moves toward physical properties with real-world units.

The reflective properties and specular response of Substrate Materials are defined with three attributes: DiffuseAlbedo, F0, and F90. Substrate enforces energy conservation automatically, ensuring the specular interface and medium do not add any energy. Therefore, the higher F0 gets, the less visible the diffuse contribution will be.

Metalness is emulated using the **Substrate Metalness-To-DiffuseAlbedo-F0** Helper node. It takes BaseColor, Specular, and Metallic values as inputs and converts them to values which map to **Diffuse Albedo** and **F0** on the Substrate Slab.

![Substrate Metalness-To-DiffuseAlbedo-F0.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff7a3e60-b1be-4229-bd68-7bbc2de2c520/substrate-metalness-example.png)

It's possible to achieve a wide variety of complex material diffuse and specular response to light using the **EdgeColor** or **F90** inputs. For example, a red sphere with cyan-to-yellow perpendicular-to-tangent specular reflections.

![Substrate Metalness-to-DiffuseAlbedo-F0 Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16f6d435-7f70-4f89-a62d-d7db16493ea3/substrate-metalness-example-sphere.png)

**Substrate FlipFlop** Helper nodes are useful for achieving normal-based specular colorization. It controls the specular color of F0 and F90 as a function of NoV with adjustable falloff transition.

### Rough Refraction

Substrate supports rough refraction through translucent objects and layered opaque materials with a translucent top layer. The blurriness of the scene background, as well as the distance to the refracted object, is computed from the primary material roughness when you use distortion / refraction.

#### Translucent Rough Refraction

To create a translucent material with rough refraction, set the following properties in the **Details** panel.

-   **Blend Mode:** TranslucentColoredTransmittance, TranslucentGreyTransmittance, or ColoredTransmittanceOnly.
-   **Refraction Method:** Index of Refraction (IOR), Pixel Normal Offset, or 2D Offset.

Pass values into **Refraction**, **Roughness**, and **SSS MFP**. The graph below produces a simplistic frosted glass result when roughness is greater than 0. A high SSS MFP value is used to create a fully transparent material, while the IOR of 1.514 approximates that of glass.

![Substrate Translucent Rough Refraction Example Graph.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5024586-e994-4558-8176-4d63e74f7166/substrate-translucent-rough-refraction-graph.png)

In the examples below, as the value of Roughness increases (0, 0.2, and 0.6 left to right), objects behind the glass become blurrier.

![Substrate Translucent Rough Refraction Examples.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5836c5a1-35c0-4fe4-a2d5-7c865fac2e71/substrate-rough-refraction-examples.png)

The blurring from rough refraction uses an approximation for accounting for depth behind translucent elements in the scene.

#### Opaque Rough Refraction

Substrate coating layers can blur the layers beneath them based on the roughness and thickness of the top coating layer. This type of refraction is more costly to performance and must be enabled for the project in the Project Settings under the **Engine > Rendering** category. Check the box for **Substrate opaque material rough refraction** to enable this feature.

![Project Setting for Substrate Opaque Rough Refraction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c30f8977-8ca8-498f-b5db-165fa94ea3e0/substrate-opaque-rough-refraction-project-setting.png)

The graph below shows an example using opaque material rough refraction using a vertically layered material with a clear coat on top of an opaque checkerboard.

![Example of using an opaque material rough refractions with Substrate.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cae99c71-55ce-4473-b8c9-79806245ea32/substrate-rough-refraction-graph-inputs.png)

The **Roughness** and **Thickness** parameters determine the strength of the blur being applied to the bottom material layer. Increasing either value increases how blurred the refraction becomes.

You can see this in the examples below, where the clear coat top layer on the left has a roughness and thickness of 0.1. The example on the right has a roughness of 0.8 and a thickness of 6, causing the bottom layer to become blurred.

![Substrate Rough Refractions Thickness Examples](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08d96b8d-1d0a-4530-886b-6ff1b7ea18e4/substrate-rough-refractioin-thickness-example.png)

### Subsurface Scattering and Participating Media

A Substrate Slab contains participating media and can be used to simulate various volumetric appearances.

For instance, if you render an opaque material only, when a slab is at the bottom of the material topology, it is considered for subsurface scattering. There are two things to consider:

-   If a [Subsurface Profile](/documentation/en-us/unreal-engine/subsurface-profile-shading-model-in-unreal-engine) is assigned to a Slab in the Details panel of the Material, the profile is used per pixel. Keep in mind that Subsurface Profiles are **not** blendable.
-   If there is no Subsurface Profile assigned, scattering is determined from the DiffuseAlbedo and SSS MPF properties of the Slab. These properties are blendable.

The **MFP** (or Mean Free Path) of Subsurface Scattering is the distance (in centimeters) that different wavelengths of light will penetrate through a medium before encountering a collision. The example below shows a DiffuseAlbedo (colored white) and a **SSS MFP** (colored red) scaled from 0 to 1, left to right.

![Substrate MFP scaled from 0 to 1.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8decc901-0ae0-4e22-a0aa-db37d9af57dd/substrate-mfp-values.png)

Any slab not at the bottom of an opaque material or used in a translucent one, is considered for a volumetric representation, which also relies on DiffuseAlbedo and SSS MFP attributes. The DiffuseAlbedo represents the medium's base color, accounting for single and multiple scattering.

The **SSS MFP** attribute is a way to control the medium's transmittance for a view perpendicular to a surface — it represents how visible the surface below is.

![Substrate SSS MFP grid of examples.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b250bc93-4584-481a-8db9-ef7a1b33c016/substrate-sss-mfp-grid-examples-1.png)

Examples of a material with transmittance color ranging from black to blue from left to right, and DiffuseAlbedo ranging from black to white from bottom to top.

Vertically layering a Slab on top of another is similar to a coating operation. The visibility of the bottom Slab is dependent on the transmittance of the top Slab. It is possible to reduce the coverage of the top Slab (like at the edge of a puddle of water on a surface) to make it progressively disappear. You can achieved this using a **Coverage Weight** operator node, which is analogous to alpha blending.

![Substrate SSS MFP grid of examples.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4d68d9b-0aab-4451-af03-d2ef5315f816/substrate-sss-mfp-grid-examples-2.png)

Examples of a material with Transmittance ranging from black to blue from left to right, and coverage ranging from 0 to 1 from bottom to top.

To achieve a specific transmittance or scattering color, you should use the **Substrate Transmittance-To-MeanFreePath** Helper node. The MFP is derived for the **TransmittanceColor** to match at normal incidence — when the surface is viewed perpendicularly, along the normal.

The example below shows a blue subsurface scattering on an opaque material that is pink, where the SSS MFP is derived from Transmittance Color.

![Example using Substrate Transmittance-To-MeanFreePath Subsurface Scattering.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04b8041b-0b80-41a3-ada9-7cd058c90627/substrate-transmittance-to-mfp.png)

It is not recommended to directly control MFP when trying to achieve a particular transmittance color because MFP is not a color, it's a measurement of light transport. The relationship between MFP and subsurface scattering color is non-intuitive and non-linear from an artist's perspective.

### Translucency and Blend Modes

Substrate offers more robust options for translucent surface shading than is possible with traditional non-Substrate materials. The list of [Substrate Blend Modes](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#substrateblendmodes) now makes more sense when considering a surface is made of matter (a Substrate Slab).

To create a Translucent Material:

1.  Choose a **Blend Mode** that supports translucency.
    -   Opaque
    -   Masked
    -   TranslucentColoredTransmittance
    -   TranslucentGreyTransmittance
    -   ColoredTransmittanceOnly
    -   AlphaHoldout
2.  With the Material Root node selected, use the **Details** panel to select a **Lighting Mode**. Choose between:
    -   Surface Forward Shading
    -   Surface Translucency Volume — this option supports reflections on the surface.
    -   Volumetric NonDirectional — cheaper to use but does not reflect light.

Below is an example setup of a translucent Substrate material. Its Blend Mode is set to **TranslucentColoredTransmittance** and uses the **Surface ForwardShading** Lighting Mode. It uses a single Slab passed into the Front Material pin of the Material Root node to produce a translucent material that appears opaque.

![Example of an opaque translucent Substrate material.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f302647f-c46f-4d54-9383-67eb3c9add27/substrate-translucent-opaque-example.png)

Using the **Substrate Coverage Weight** Operator between the Slab and the Front Material input controls the transmittance of the material. Use the **Weight** input on the Substrate Coverage Weight node to control how transparent the material is.

![Example of a clear translucent Substrate material.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15a9ca93-5b6c-4652-90a6-95c63e848352/substrate-translucent-material-example.png)

You can use a constant value of 0 to 1 to control the opacity of the entire material (like above) or use a texture (like below) to control parts of the material.

![Example of a masked translucent Substrate material.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/670eba1d-7aa2-4ae2-a0ec-b4624efe27b2/substrate-translucent-masked-example.png)

You can go a step further to create a slab of matter that resembles colored glass by specifying the MFP of the participating medium. This is set up using the **Transmittance-To-MeanFreePath** Helper node, like in the example below, using an orange TransmittanceColor connected to SSS MFP to tint the material orange only in regions where it transmits light. The specified TransmittanceColor is the "target" color, which is reached at the provided thickness input (default is 0.01 centimeters).

![Example of a colored transmittance used with a masked translucent Substrate Material.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd6468f4-7020-4ad4-99c0-e500d0288981/substrate-colored-transmittance-to-mfp.png)

#### Additional Notes about Substrate Translucency

-   Translucent materials do not support Screen Space Subsurface Scattering, even though the Slab is considered a volume of participating medium.

## Substrate Debug View Modes

When using Substrate, it's useful to see how its materials are performing and which would benefit from more attention. Substrate's debug visualization modes are in the **View Modes** dropdown list under the **Substrate** category.

![Select a Substrate Debug View Mode in the Level Editor.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c29f2e43-58b7-419c-9587-6326334388eb/substrate-view-modes-menu.png)

Substrate includes the following visualization modes for debugging:

Click images in the table to enlarge them.

| Debug Visualization | Debug Visualization Name | Description |
| --- | --- | --- |
| 
 | **Material Properties** | Visualize Substrate properties under the mouse cursor. Hover over the pixel you want to inspect with your mouse, and you will see the final packed material closure used for lighting, such as properties, colored weight, enabled features of the material, used bytes, and more. |
| 

 | **Material Count** | Visualize Substrate material count per pixel and color them according to the number of BSDF Slab nodes they are using. |
| 

 | **Material Bytes Count** | Visualize Substrate material footprint per pixel. Materials are color-coded to the number of bytes they are using. You can also hover your mouse over a material to see the bytes per pixel of the material. |
| 

 | **Substrate Info** | This mode summarizes information about the use of Substrate in the project, including information about max memory usage, max bytes per pixel (which is useful for setting simplification thresholds) and enabled Substrate features. |
| Substrate Advanced View Modes |   |   |
| 

 | **Advanced Material Properties** | 

Reports information about the different Substrate Slabs composing the Material currently under the mouse cursor. Each slab is presented separately on screen.

This view mode must be enabled in the Project Settings under the **Engine > Rendering** category with the checkbox **Substrate advanced visualization shaders**.



 |
| 

 | **Material Classification** | 

This mode shows the material complexity per tile and returns a color coded result:

-   **Green** denotes a simple, Disney-like material using a Legacy Slab.
-   **Yellow** indicates a single Slab material with any features but Anisotropy enabled.
-   **Red** indicates that either multiple Slabs are mixed or layered in the tile, or the material has Anisotropy enabled.

You can get a hint at the complexity of a Substrate material by looking at the Slab node to see if it is **Simple**, **Single**, or **Complex**.



 |
| 

 | **Rough Refraction Classification** | 

This mode displays materials that use the Opaque Rough Refraction property. This mode also distinguishes between Substrate materials that have subsurface scattering enabled or disabled.

The tiles shown in some of these visualization modes are used to run optimized post-lighting passes later. These can be useful to optimize your Substrate materials by reducing the number of slabs used and enabled features, and to [use parameter blending on Operators](/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine#parameterblendingwithoperators).

If a material is made of several materials mixed and layered together, but only a single Slab is visible (due to dynamic masking or low transmittance value) for a given pixel, the non-visible Slabs are not shown (or optimized out) of the visualization.



 |

## Limitations and Known Issues

-   Substrates is experimental, so we recommend not using it for any production work.
-   Platform support and testing is currently incomplete. As it moves into Beta and then Production Ready states, more testing coverage will happen.
-   Features and UX are subject to change such that existing assets may behave differently or be invalidated altogether.
-   Mobile is supported when using **Mobile Forward Shading**.
-   Experimental support for Path Tracer.
-   Some platforms and rendering paths, such as DirectX 11 (DX11) and Mac, exhibit issues and may not work entirely.

## Additional Resources

-   [The Future of Materials in Unreal Engine - GDC 2023](https://www.youtube.com/watch?v=joOIBteSo1w)
-   [The State of Unreal Livestream](https://www.youtube.com/watch?v=teTroOAGZjM&t=8982s) — Timestamp: 02:29:42
-   The [Content Examples](https://www.fab.com/listings/4d251261-d98c-48e2-baee-8f4e47c67091) sample project includes a Level named "SubstrateMaterials" where you can explore different examples and demonstrations of how Substrate Materials function.
    
    Using Substrate with the Content Examples project requires you to enable Substrate for the project. Only this map has been validated for use with Substrate enabled. If you are using only a single instance of the Content Examples project, we recommend only enabling Substrate for this level and disabling it anytime you're using the rest of the project.
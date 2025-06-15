# Water Body Actors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/water-body-actors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/water-body-actors-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:58

---

You can use **Water Body Actors** to define the location and shape of the water surface and their transitions in the level. Water bodies are made up of water mesh tiles that are managed by the **Water Mesh Actor**. This actor sets the quality and properties of all water bodies. You can set the water mesh actor up to cover the area where you want water bodies rendered. When you do so, Unreal Engine automatically generates the needed mesh. Rendering all the water bodies as a single water tile mesh allows for smooth and seamless transitions between them.

Water Bodies also determine wave movement and shading of the water surface, as well as the underwater post-processing. Each water body contains information about its depth and flow. You can query these for gameplay usage. For example, you can create physics interactions with the water's surface.

## Types of Water Bodies

There are several types of Water Body Actors to choose from.

-   Water Bodies for **Oceans**, **Lakes**, and **Rivers**. These are all defined using splines that store data about their type.
-   A **Custom** type. This also has a spline for querying data, but you define the shape with a Static Mesh.
-   An **Island**. This is used to raise landscape terrain within a defined spline area.
-   An **Exclusion Volume**. You can use this to create underwater zones where gameplay can act as if it was not under water.

To add a Water Body Actor to your Level:

-   Go to the **Place Actors** panel, select the **Water Body Actor**, and drag and drop it into your level

![Placing a water body in the level.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a23e37f4-f994-4920-afe0-5cf5609a3c61/water-body-placement.png)

Water bodies automatically work with [Landscape Terrain](/documentation/en-us/unreal-engine/landscape-outdoor-terrain-in-unreal-engine) to carve out the terrain beneath them using a Landscape Brush. The Landscape Brush only edits the landscape layer when the Landscape has **Enable Edit Layers** checked.

|   |   |
| --- | --- |
| ![Enable Edit Layers in Landscape Mode.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83476fe0-c770-438d-a8ab-328b4475ceee/enable-edit-layers-landscapemode.png) | ![Enable Edit Layers on the Landscape Actor.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c505f0c-ed69-4c11-b46f-8211d6778617/enable-edit-layers-landscapeactor.png) |
| Enabling Edit Layers on new landscapes in Landscape Mode options. | Enabling Edit Layers on existing Landscape terrains. |

Water Bodies include their own underwater post-processing that happens when the camera moves below the water's surface. This enables you to define the look of water with a subset of the standard post-process settings.

### Ocean Water Body

The **Ocean Water Body** is defined by a closed loop spline that forms a shoreline and renders water out to a far distance from those spline points. The spline points all have the same height placement in the level.

Water Bodies are limited by how far they can reach, or their largest **Extent Size**. However, Ocean Water Bodies can reach this without completely filling the level, leaving a gap between the horizon line and the water depending on the perspective of the camera. **Water Zone** Actors provide an option to fill that gap with a simplified mesh and water material.

The example below demonstrates how the simplified water mesh can fill the empty space without the added cost of a highly tessellated mesh and complex material.

|   |   |
| --- | --- |
| ![Example scene with a far distance mesh.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f3499e3-499b-4a3d-ba5c-cf5b9d087adf/far-distance-mesh-enabled-ground.png) | ![Example scene without a far distance mesh.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09e35ef8-3d0a-4814-9177-93c735dccacb/far-distance-mesh-disabled-ground.png) |
| Ground perspective with a Far Distance Mesh (default) | Ground perspective without a Far Distance Mesh. |

From an aerial perspective, it can be clear where the Ocean Water Body ends. You can use the Far Distance Mesh and match the color of its material to the Ocean Water Body to seamlessly fill the scene. This has less impact on performance.

|   |   |
| --- | --- |
| ![Example scene with a far distance mesh.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4834a67-1296-4445-b7a8-35f180c3dbc3/far-distance-mesh-enabled-air.png) | ![Example scene without a far distance mesh.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df9eee98-5f6f-4a20-9497-1166617a562a/far-distance-mesh-disabled-air.png) |
| Aerial perspective with a Far Distance Mesh (default) | Aerial perspective without a Far Distance Mesh. |

The **Far Distance Mesh** is enabled by default in the **Water Zone** Actor. The **Far Distance Mesh Extent** is already set with a large enough distance to stretch to the world's edge.

To change the size of the extent:

-   Go to the **WaterZone Actor > Rendering > FarDistance**, and change the value for **Far Distance Mesh Extent**.

![Water Zone details FarDistance settings.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa45d54c-314a-4b4f-af79-b73e88d6db63/waterzone-fardistance-settings.png)

By default, the **Water\_FarMesh** material is assigned to the **Far Distance Material** slot. This material matches the default water materials used by the other water bodies ensuring that it will have a consistent look.

For consistency, when you adjust the color or other properties of your ocean water material, make sure to make the same changes to the **Water\_FarMesh** material. Doing so ensures they blend together in the distance.

You can use **Far Distance Mesh Extent** to set how far (in world units) the Far Distance Mesh should extend beyond the Ocean Water Body. Make sure to use a large enough value that the mesh completely fills any gaps between the edge of the Ocean Water Body and the horizon line.

### Lake Water Body

The **Lake Water Body** is defined by its closed loop, which forms the lake and carves out the landscape beneath it. Each of its spline points is limited to having all points reside at the same height, unlike river spline points.

### River Water Body

The **River Water Body** is defined by its open spline with starting and ending points. Rivers carve out the landscape beneath them along the path of the spline. Rivers allow spline points to have varying heights. They do not drive surface motion using waves. Instead, rivers use velocity from the individual points along the spline to drive motion. The velocity is written to a flow map that visually drives the flow of water along the surface in the direction the spline is going.

River Water Bodies act as connections between other water bodies. At the points where lakes and oceans intersect a river, you can use a transitional material to automatically blend them together seamlessly.

![Water Body transition example.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/200830db-d286-4b8b-a23a-620c688b0e1c/water-waterbody-transition.gif)

### Custom Water Body

The **Water Body Custom** uses a Static Mesh with the same water material used by other Water Bodies. It also uses the same meshing system with some added flexibility for customization, such as creating a water surface for a pool. The primary difference is that custom water bodies do not use the [Water Mesh Actor](/documentation/en-us/unreal-engine/water-meshing-system-and-surface-rendering-in-unreal-engine) and therefore do not automatically carve out the terrain. Custom water bodies can use a **Wave Source** from a [Water Wave Asset](/documentation/en-us/unreal-engine/simulating-waves-using-the-water-waves-asset-in-unreal-engine) and underwater post-processing.

### Island Water Body

The **Island Water Body** creates islands based on a spline and includes similar terraforming controls to other water bodies. Their only purpose is to affect the landscape underneath them, to make sure that a given piece of land is always above water. Their terraforming is applied after all other water bodies.

## Water Body Properties

All Water Bodies share core properties that make up the Water Body Component, but there are some settings specific to individual Water Body types.

### Selected Points

The **Selected Points** category enables you to cycle through any of the currently selected Water Body's spline points. Each spline point has properties that include its location, rotation, and type. Some spline points also have Water Body-specific properties, such as Rivers having extra properties to define depth and width.

![Water Body selected spline points.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba98bb1e-f35e-404c-a619-d4302c716951/water-body-spline-points.png)

When a single or all spline points are selected, their properties are displayed below, showing their location, rotation, and type.

Each Water Body has its own [Water](/documentation/en-us/unreal-engine/water-body-actors-in-unreal-engine#water) category of settings that relate to the spline points. These include settings for the velocity and audio intensity. River Water Bodies also include settings for depth and river width. The Depth values are fed to the [Curve](/documentation/en-us/unreal-engine/water-body-actors-in-unreal-engine#curvesettings) controls of the water body.

|   |   |
| --- | --- |
| ![Ocean and Lake Water Body spline properties.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b600db23-d46e-43dc-b9a3-7857084cb362/water-body-ocean-lake-splineproperties.png) | ![River Water Body spline properties.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96869700-854f-4fb4-a375-0ed3fd90f8aa/water-body-river-splineproperties.png) |
| Ocean and Lake Water Body Spline Properties | River Water Body Spline Properties |

| Property | Description |
| --- | --- |
| **Input Key** | The numerical ordering of spline points that make up the Water Body. |
| **Location** | The world location coordinates of the selected spline point relative to its pivot point location. |
| **Rotation** | The relative rotation of the selected spline point. |
| **Arrive Tangent** | This tangent is used when interpolating towards this point. |
| **Leave Tangent** | This tangent is used when interpolating away from this point. |
| Water |   |
| **Depth** | (Rivers Only) Sets the depth of the river at each spline point along the river's path. Depth can be specified individually for each point along the spline. |
| **River Width** | (Rivers Only) Sets the width of the river at each spline point along the river's path. You can specify the width for each individual point along the spline. |
| **Velocity** | (Rivers Only) Sets the directional speed along the river's spline path. Higher values control the speed of the water between each spline point. Positive and negative values control the direction that the water flows along the spline. |
| **Audio Intensity** | Modulates the audio volume level driven by the spline. |

#### River Spline Visualization and Manipulation

Water splines have the same features as generic splines. They have additional manipulators that you can enable through the right-click context menu.

![River Water Body selected spline point visualization options.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3686416-76f3-4673-b6da-1f57a7b0228e/river-water-body-vis-options.png)

-   **Visualize Water Velocity** displays the velocity at each spline through a trio of arrows, which are scaled according to the velocity of the points.
    
    ![River Water Body velocity visualization.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17b9edca-2daf-430c-8ebd-1d46664b47b3/river-waterbody-velocity-vis.png)
-   **Visualize River Width** displays two handles that you can select and drag to edit the width of river water bodies in the viewport.
    
    ![River Water Body width visualization.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6300d848-b3c5-49b5-bac8-92537850c0de/water-watersplinevis-width.gif)
-   **Visualize Depth** displays an additional handle that you can select and drag to edit the depth within the viewport.
    
    ![River Water Body velocity visualization.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be6d09b0-7746-42dc-b2f4-306f949df20c/water-watersplinevis-depth.gif)

You can set a global scale in the Project Settings, under the **Plugins > Water Editor** settings.

### Water

The **Water** category contains information about the selected Water Body. It also lists what **Islands** and **Exclusion Volumes** affect it. Under each of those categories, you can find the index number of the GPU-driven wave data.

![Water Body Water settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e638bbc1-8e42-45a1-b148-116abc0fb3d9/water-settings.png)

This index is automatically used in the default **Water\_Material** to calculate the correct surface waves. You can also manually set it to read from the parent material or any child instances through the scalar parameter called **WaterBodyIndex**.

![Water Material Water Body Index parameter.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5703f8e7-2dbb-4c89-90e8-a71e999bc7c3/water-material-waterbodyindex.png)

| Property | Description |
| --- | --- |
| **Water Body Index** | The index into the GPU where the wave data for each Water Body Actor is stored. This index is automatically used in the water material to calculate the correct surface waves. |
| Advanced Properties |   |
| **Water Body Islands** | An array listing of any Water Body Islands that affect this water body. |
| **Water Body Exclusion Volumes** | An array listing of any Water Body Exclusion Volumes that affect this water body. |
| **Owning Water Zone** | The Water Zone that this Water Body belongs to. |
| **Water Zone Override** | An override to set which of the Water Zones in the world this Water Body should belong to. |
| **Fixed Water Depth** | If the Water Material assigned to this component has Fixed Depth enabled, this is the depth that is passed to the material. |

### Terrain

The **Terrain** category contains settings that change how the Water Body carves the terrain around the water.

For Water Bodies to interact with terrain, the Landscape must have **Enable Edit Layers** checked.

#### Curve Settings

The **Curve Settings** define the shape of the surface that is carved under the water, and primarily provides the water depth profile.

![Water Body Curve settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a82f5db-8bec-497c-a3c2-11d9057d208b/water-body-curve-settings.png)

| Property | Description |
| --- | --- |
| Curve Settings |   |
| **Use Curve Channel** | Toggles the carved surface under the water effect on and off. |
| **Elevation Curve Asset** | Use a Curve Asset to change how the landscape is carved below the water surface. |
| **Channel Edge Offset** | An offset from the edge of the water to where the curve starts. |
| **Channel Depth** | 
Sets the depth of Lake Water Bodies only.

For River Water Bodies, depth is set per spline point.



 |
| **Curve Ramp Width** | The width of the curve (in world units). |

An **Elevation Curve Asset** is defined within a 0 to 1 range on both the X and Y axis. The Y axis represents the water's depth, and is multiplied with the Depth value set on each spline point. The default curve is a simple S curve that works for most cases.

|   |   |   |
| --- | --- | --- |
| ![Float Curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af9458a9-2848-459d-ab9d-c1bc4749ce70/float-curve.png) | ![River Water Body S Curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/292f1114-9288-4baa-b095-9bb8635d1aa3/river-water-body-curve.png) | ![River Water Body hidden surface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a65248c5-cd1a-47e2-b8c7-9207a670b0d9/river-water-body-hidden-surface.png) |
| Float Curve Asset with an "S" Curve | Default S Curve with River Water Body | Default S Curve with River Water Body Surface Hidden |

The bottom-left corner of the curve is at 0,0. This is where the shoreline is located and the upper-right corner of the curve represents the maximum water depth.

For the Depth value that you set on River Water Body spline points to be accurate, you must keep the Y value at **1**.

#### Water Heightmap Settings

| Property | Description |
| --- | --- |
| **Blend Mode** | 
Choose between one of the following blend modes:

-   **Alpha Blend:** Affects the height map of the landscape terrain both upwards and downwards.
-   **Min:** Limits the brush to only lowering the landscape terrain.
-   **Max:** Limits the brush to only raising the landscape terrain.
-   **Adaptive:** Performs an additive blend using a flat Z height as the input. This is useful when you want to preserve underlying detail or ramps that you have added.



 |
| **Invert Shape** | Flips the carved shape inside out so that if you were carving a lake, it would now become an island. |
| Falloff Settings |   |
| **Falloff Mode** | Choose between Angle and Width based falloff for the selected Water Body. See [Falloff Settings](/documentation/en-us/unreal-engine/water-body-actors-in-unreal-engine#falloffsettings). |
| **Falloff Angle** | The angle at which the Water Body blends with the terrain beneath it. |
| **Falloff Width** | The width (in world units) of falloff from the Water Body's edge to the terrain. |
| **Edge Offset** | Applies a flat offset to the edge of the Water Body before the specified falloff begins. It can create a flat shoreline around a Waterbody. |
| **ZOffset** | Applies a Z offset to the height of the water surface for terrain carving. |
| Effects |   |
| **Blurring** | 

The distance field generation process can cause artifacts (such as pinching) that come from aliasing due to texture resolution. A small amount of blurring is applied automatically, but you can make manual adjustments to improve results.

-   **Blur Shape:** Applies a small amount of blurring to the result to avoid artifacts that can occur. You should only disable this if there is a problem that is not automatically resolved.
-   **Radius:** When Blur Shape is disabled, use this to increase or decrease the strength of the blurring that happens.



 |
| **Curl Noise** | This adds procedural distortion to the supplied spline. Two octaves of curl noise are exposed, each with a separate tiling parameter and strength. By default, the amount is set to 0, disabling any curl noise effects. Use the Curl Amount and Curl Tiling to apply different amounts of procedural noise to the result. |
| **Displacement** | 

Use a texture to add some additional detail to the Water Body.



 |
| **Smooth Blending** | 

Applies a smoothing parameter to the inner and outer edge of a Water Body. It is useful for seamlessly blending into nearby terrain for player navigation.

-   **Inner Smooth Distance:** Applies an inner distance (in world units) to a Water Body to blend with the terrain.
-   **Outer Smooth Distance:** Applies an outer distance (in world units) to a Water Body to blend with the terrain.



 |
| **Terracing** | 

This applies steps to the terrain area affected by a Water Body. The terracing can be masked to only occur a specified distance away from the water's edge using a specified alpha range. Terraces can also be blended from sharp to smooth.

-   **Terrace Alpha:** The alpha used for the final application of the terraces. A value of 0 means terracing is disabled. A value of 0.5 means terracing is blended to 50% opacity, and a value of 1 displays full terracing.
-   **Terrace Spacing:** The spacing (in world units) between terrace levels.
-   **Terrace Smoothness:** Terraces are defined by a function that can blend between sharp steps, and smooth curved steps to a linear slope. A value of 0 has sharp terraces. A value of 0.5 has rounded terraces. A value of 1 has no terraces, giving the same result as Terrace Alpha of 0.
-   **Mask Length:** Defines an alpha gradient from the edge of the water to where terraces become their full specified strength.
-   **Mask Start Offset:** An offset to the distance the terrace mask starts from the edge of the Water Body.



 |
| **Layer Weightmap Settings** | 

Each water body contains this array that allows each to affect any number of weight maps. Each item added to the array exposes another Struct of settings for how the weight map will be applied. These controls allow mapping custom gradients from the distance field created for the brush and using textures to break up the results and add noise. Negative opacity is possible for creating subtractive effects.



 |
| **Affects Landscape** | If enabled, the Landscape terrain will be deformed based on the Water Body's placement on top of it, and the landscape height is considered when determining water depth at runtime. |

##### Blend Mode

The **Blend Mode** provides a selection of modes that gives different results for how Water Bodies carve out the landscape terrain beneath them.

You can choose between Blend Modes called **Alpha Blend**, **Min**, **Max**, and **Additive**.

|   |   |   |   |
| --- | --- | --- | --- |
| ![Alpha Blend Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4964dec7-acfa-48cc-a8a0-938d0086ae3a/blend-mode-alpha.png) | ![Min Blend Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e373a8eb-4f86-4fbd-bda8-219d739e7beb/blend-mode-min.png) | ![Max Blend Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc69d36b-452d-43b2-919c-c74c11cea0a5/blend-mode-max.png) | ![Additive Blend Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eecb1cb5-d54b-4435-9490-ba5406ecb7cc/blend-mode-additive.png) |
| Alpha Blend | Min | Max | Additive |

| Property | Description |
| --- | --- |
| **Alpha Blend** | This affects the heightmap both upwards and downwards. |
| **Min** | Limits the brush to only lowering the terrain. |
| **Max** | Limits the brush to only raising the terrain. |
| **Additive** | Performs an additive blend using a flat Z=0 terrain as the input. This is useful when you want to preserve the underlying detail or ramps. |

Most Water Bodies only need to use **Alpha Blend**, since it can both lower and raise the terrain to make sure a foundation exists at the height of the water.

The **Min** and **Max** options are ideally used in situations where you'd want to intersect a river with another water body without having the elevation of one affecting the other. For example, a river intersecting a lake should use a Min blend mode to prevent the river from raising the elevation inside the lake's carved-out terrain.

The **Additive** mode should be saved for special cases where you want to preserve the underlying detail since it does not ensure exact values are written to the landscape terrain.

##### Falloff Settings

The Falloff Settings determine how the Water Body carving blends into the existing terrain. You can customize this in several ways.

You can choose between two **Falloff Modes** called **Angle** and **Width**.

Angle-based falloff extends the object at a specified angle until an intersection with the landscape terrain occurs. Width-based falloff sets a fixed width that is used regardless of intersection with the landscape.

|   |   |
| --- | --- |
| ![Angle-based falloff](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97bb1f33-cd82-4683-b208-626becaf9043/falloff-angle.png) | ![Width-based falloff](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2afe09f-38b4-4562-bed9-34369a8dd0c0/falloff-width.png) |
| Angle-Based Falloff | Width-Based Falloff |

The **Edge Offset** applies a flat edge around the Water Body. This can be useful for flat shores on the sides of rivers, even when the river is carved through a mountain.

|   |   |
| --- | --- |
| ![Edge offset 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07c670d9-b7a1-4d61-9a2e-720d09dca162/edge-offset-0.png) | ![Edget offset 1024](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6666abcb-2d15-41d8-9f0f-a245dd9411f2/edge-offset-1024.png) |
| Edge Offset: 0 | Edge Offset: 1024 |

##### Effects

The **Effects** settings are a powerful sub-category of terrain carving settings. They provide controls to tweak the output and blending of a Water Body into the landscape terrain.

###### Blurring

The **Blurring** settings reduce artifacts that can occur during distance field generation. Such items come from aliasing due to texture resolution. A small amount of blurring is applied automatically, but you can increase or decrease the strength of the blurring by disabling **Blur Shape** and setting a custom **Radius**.

|   |   |
| --- | --- |
| ![Blurring enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52e7a119-3639-4651-8883-427a4a260fb0/blurring-enabled.png) | ![Blurring disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ee8ad18-85e6-4570-8661-1baa93d84d4a/blurring-disabled.png) |
| Blurring Enabled (Default) | Blurring Disabled |

###### Curl Noise

The **Curl Noise** settings add procedural distortion to the Water Body's spline. It uses two octaves of curl noise, each with a separate tiling parameter and strength. By default, the curl noise is set to 0 and the effect is disabled.

The examples below have different **Curl Amounts** and **Curl Tiling** applied.

|   |   |
| --- | --- |
| ![River water body without Curl noise.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a50c798e-2d14-4862-8842-485b7f1ef1c1/river-waterbody-no-curl.png) | ![River water body with Curl applied](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2a5367b-eb28-4853-a04c-681206d5ea7d/river-waterbody-with-curl.png) |
| River Water Body without any Curl noise applied. | River Water Body with Curl 1 and Curl 2 |

**Smooth Blending**

The **Smooth Blending** provides smoothing parameters for the inner and outer edges of a Water Body, which is useful for seamlessly blending into nearby terrain for player navigation.

The example below shows the effect of an increased **Inner Smooth Distance** and **Outer Smooth Distance**.

|   |   |   |   |
| --- | --- | --- | --- |
| ![No Smooth Blending](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8494ee34-87aa-41a6-bbc1-d884e71c6932/smooth-blending-none.png) | ![Inner Smooth Blending](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30831cc4-60da-49ae-ae9e-023e09daecff/smooth-blending-inner.png) | ![Outer Smooth Blending](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba9414f3-cdad-429a-8ee0-1890010b56bb/smooth-blending-outer.png) | ![Inner and Outer Smooth Blending](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d0853ce-8324-43f6-80b7-94053a68d1cd/smooth-blending-inner-outer.png) |
| No Smooth Blending | Inner Smooth Blending | Outer Smooth Blending | Inner and Outer Smooth Blending |

**Terracing**

Terracing applies steps to the terrain area affected by a Water Body. Terracing can be masked to only occur a specified distance away from the water's edge using an alpha range. Terraces can also be blended from sharp to smooth.

Below is an example of various terracing values for smoothness, spacing, and masking working together.

![Examples of different terracing values.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be72687b-9a17-41b8-91f3-6735b646bfd7/terracing-values.png)

You can use the **Mask Length** and **Mask Start Offset** to adjust where the terracing starts within the falloff area.

![Terracing mask length and start offset.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15e65566-2b01-4076-b15f-0b2a688a6cdc/terracing-mask-examples.gif)

### Wave

The **Wave** section defines the waves of the selected Water Body. You can set the depth at which waves are attenuated, their max height bounds, and specify a Water Waves Asset used to drive Gerstner wave properties for a Water Body.

![Water Body Wave settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8e64e34-4539-4e87-a0d0-d35a1d0f69cb/water-wave-settings.png)

The Wave category contains the following:

| Property | Description |
| --- | --- |
| **Wave Attenuation Water Depth** | The depth at which waves start to attenuate, or reduce their force. Waves attenuate the more shallow the water is, and this property determines how shallow the water must be for waves to start attenuating. A value of 0 makeswaves not attenuate based on depth. |
| **Max Wave Height Offset** | This value adds an offset to the automatically calculated max wave height bounds. This offset can help in cases where the automatically calculated max height bounds don't match your waves, like if the water surface is manually altered through the material with World Position Offset or some other means. |
| **Waves Source** | Provides a selection of algorithms for generating waves. The default algorithm is for Gerstner Waves. You can also assign a [Water Wave Asset](/documentation/en-us/unreal-engine/simulating-waves-using-the-water-waves-asset-in-unreal-engine) with your own wave generator that replaces the Gerstner Waves source. |
| **Water Waves Asset** | Assign a custom [Water Wave Asset](/documentation/en-us/unreal-engine/simulating-waves-using-the-water-waves-asset-in-unreal-engine) when **Waves Source** is set to `Water Waves Asset Reference`. |

### Rendering

The **Rendering** category is where all Materials are applied to the Water Body, such as the surface material and the underwater post-process material. This section also contains common rendering properties found on all Actors and Components.

![Water Body Rendering settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f477b279-f172-4d48-8da2-21c4c8c4697a/water-rendering-settings.png)

The properties table below covers water-related properties.

Not all properties are displayed that fall under the **Rendering > Advanced** category. Only the ones directly related to water bodies.

| Property | Description |
| --- | --- |
| **Water Material** | The water material assigned to this Water Body. |
| **Underwater Post Process Settings** | The underwater post process material assigned to this Water Body. |
| **Water Info Material** | The material with which this water body renders into the Water Info Texture. |
| **Water LOD Material** | The material used by this water body when rendered as a Static Mesh. Only applies when the non-tessellated LOD is enabled on the Water Zone. |
| **Water Mesh Override** | Sets a custom mesh to be used instead of the water body's default mesh. |
| **Overlap Material Priority** | Determines which Water Body to use the material from when no transition material is assigned to either Water Body. Higher values are given greater precedence and valid ranges are -8192 to 8191. |
| **Custom Primitive Data Defaults** | Optional values for the custom primitive data of this primitive. These are user-defined. |
| **Visible** | Determines whether or not to completely draw the primitive. When false, the primitive is not drawn and does not cast a shadow. |
| **Actor Hidden in Game** | When enabled, the Actor is only rendered in the Editor and not while in the game. |
| **Editor Billboard Scale** | Sets the scale to apply to any billboard component in the Editor. |
| Advanced Properties |   |
| **Underwater Post Process Settings** | See [Underwater Post Process Settings](/documentation/en-us/unreal-engine/water-body-actors-in-unreal-engine#underwaterpostprocesssettings) below. |
| **Shape Dilation** | Distance by which to expand the water body geometry in the water info texture. This can help alleviate artifacts created by having low-resolution water information. |
| **Always Generate Water Mesh Tiles** | When true, the water mesh always generates tiles for this water body. For example, this can be useful to generate water tiles even when the water material is invalid, for the case where "empty" water tiles are actually desirable. |

Water Bodies have their own default surface material and underwater post-process materials already assigned. You can create your own *water* materials for use with Water Bodies, but we recommend that you use the default water material as a starting point.

River Water Bodies contain two additional material assignment slots for transition materials for **River to Lake** and **River to Ocean**. These transition materials enable the seamless blending of rivers into other Water Body types that it connects to.

![Water Body Transitions Materials slots](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cebb6701-4a15-4970-8638-24d5c69506cc/water-transitions-materials.png)

Below is an example of a River Water Body flowing into an Ocean Water Body with a transition material.

![Water Body River transitions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd0f5549-7871-4325-a40d-4a516b5e2197/water-waterbody-river-transitions.gif)

The **Overlap Material Priority** determines the priority given to that Water Body when it comes to generating water tiles. Higher valued priorities take precedence over others. When a Transition material is not applied to the River Water Body, this property is used to determine the precedence of the overlapping Water Body.

#### Underwater Post Process Settings

The **Underwater Post Process Settings** apply post-processing when the camera goes underwater.

![Underwater Post Processing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f682518-ca61-4302-9f50-84137303865f/underwater-postprocess.png)

| Property | Description |
| --- | --- |
| **Enabled** | Determines whether or not to use underwater post-processing with this Water Body. If your game doesn't need to render underwater, this should be disabled. |
| **Priority** | Specifies the priority of this Water Body's underwater post-processing. In cases where water bodies overlap, the one with the highest priority overrides the lower priority ones. If two or more overlapping volumes have the same priority, the order is undefined. |
| **Blend Radius** | Sets the radius (in world units) around the water body used for blending. It creates a transitional area where the volume renders. |
| **Blend Weight** | The amount of influence this Water Body's underwater post process has. A value of 1 has a full effect.A value of 0 has no effect. |
| **Post Process Settings** | These settings define the look of your underwater post process. The underwater post process includes many of the settings found in the Post Process Volume. For property definitions and examples, see [Post Process Effects](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine). |

## Water Body Exclusion Volume

You can use Water Body Exclusion Volumes to create cavities in any kind of Water Body. This creates underwater zones where gameplay can act as if it was not underwater. For example, you could have an underwater base or tunnel where players can walk as normal.

Like [Geometry Brushes](/documentation/en-us/unreal-engine/geometry-brush-actors-in-unreal-engine), these volumes can be placed using the **Place Actors** panel. You can edit their shapes when the Level Editor has its **Mode** set to **Brush Editing**.

For Water Body Exclusion Volumes to work, you must set which Water Bodies they must ignore by choosing **Exclude All Overlapping Water Bodies** or by adding them to the **Water Bodies to Exclude** array.

![Water Body Exclusion properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3aa9330-6e62-40dc-bcd2-1244148fabcc/water-body-exclusion-properties.png)

| Property | Description |
| --- | --- |
| **Exclude All Overlapping Water Bodies** | This toggle excludes all Water Bodies from visually appearing within the bounds of the exclusion volume. It ensures that Water Data Queries fail so that the requested location is considered outside of the water for all Water Bodies. |
| **Water Bodies to Exclude** | An array listing of specified Water Bodies to exclude by this Water Body Exclusion Volume. It allows for all Water Data Queries to fail so the requested location is considered outside of the water for all listed Water Bodies. |
# Mesh Distance Fields Properties

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mesh-distance-fields-properties-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mesh-distance-fields-properties-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:47

---

The [Mesh Distance Fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine) system in Unreal Engine can be used with various different systems that can be enabled or disabled. You can use these settings and properties to obtain a specific style for your Project, or use them for optimization purposes.

Below you'll find the details about the available menu systems and settings you can use that are specific to Mesh Distance Fields.

## Project Settings

The **Project Settings** panel contains the settings to enable Mesh Distance Field generation for the assets in your Project, as well as some optimization options you can enable to make the use of them more efficient in some cases.

Click **Edit** on the **Main** menu and select **Project Settings** to open it.

![Open Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c66d2a8-056a-4504-9494-e7a2942e3ffe/01-mdf-properties-open-project-settings.png)

Settings for adjusting of the Mesh Distance Fields you can find by clicking  **Rendering > Software Ray Tracing**. The table below details the settings available.

Click image for full size.

| Property | Description |
| --- | --- |
| **Generate Mesh Distance Fields** | 
This determines whether the system will build Static Mesh Distance Fields, which can be used with Distance Field Shadows and Distance Field Ambient Occlusion. Enabling this will increase mesh build times and memory usage, and also requires you to restart the Unreal Editor for it to take effect.

If you enable the **Generate Mesh Distance Fields** setting for your project, you will still have increased memory usage even if you are not using any Distance Field rendering features on any Actors. If you disable this setting and restart the Unreal Editor, Mesh Distance Fields will no longer be loaded, and memory usage will go down.



 |
| **Distance Field Voxel Density** | Determines how the default scale of a mesh convert into distance field voxel dimensions. Changing this will cause all distance fields to be rebuilt. Large values can consume memory very quickly! Changing this setting requires restarting the editor. |

## Light Components

Below are the available [Mesh Distance Field](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine) settings and properties that can be set for each [Light Type](/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine) available.

### Directional Light

Below are the **Directional Light** settings that affect [Distance Field Shadowing](/documentation/en-us/unreal-engine/distance-field-soft-shadows-in-unreal-engine).

![Directional Light settings that affect DFS](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04fd3f89-6432-4400-b4ef-cd24fc1b61dd/03-mdf-properties-direct-light-dfs-settings.png)

| Property | Description |
| --- | --- |
| Light |   |
| **Source Angle** | This is the light source's angle in degrees and is used to support soft area shadows for dynamic shadowing methods using Distance Fields or Capsule Shadows. |
| Distance Field Shadows |   |
| **Distance Field Shadow Distance** | This is the farthest distance that will have Distance Field Shadowing. Distance Field Shadows will also cover the distance between this value and the **Dynamic Shadow Distance Movable Light** for CSM shadows. |
| **Distance Field Shadows** | This will toggle Distance Field Shadows on for the light source. |
| Distance Field Shadows Advanced Properties |   |
| **Distance Field Trace Distance** | This sets a distance in world units for how far shadows can cast from their shadow caster. When using larger values, you will increase the shadowing cost for the scene. |
| **Ray Start Offset Depth Scale** | This controls how large an offset there is for tracing shadows are from the receiving surface as the camera gets further away. This can be used to hide self-shadowing artifacts from low-resolution distance fields on large Static Meshes. |

#### Light Source Angle

The **Light Source Angle** softens or sharpens shadows based on the rotational angle of the light and the value entered. This allows for very soft shadowing to happen for points of the mesh that are farther away from the shadow receiving surface. Shadows closer to the mesh and the receiving surface will be sharper.

![Light Source Angle: | 1 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72c3a34a-5f31-4c27-a0f3-c2ff7c1c8aa6/04-mdf-properties-source-angle-1.png)

![Light Source Angle: | 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8cd71cdd-501f-40bf-b09e-9d1aa474d10c/05-mdf-properties-source-angle-2.png)

The further the shadows stretch away from the mesh, or the farther that they are from the shadow receiving surface, the softer the shadow will become.

#### Cascaded Shadow Maps VS Distance Field Shadows

**Cascaded Shadow Maps** provide very detailed shadowing, but don't work well across extended view distances. **Distance Field Shadows** can cast shadow over a much greater distance more efficiently, but its quality relies heavily on the resolution of the volume texture generated for the Mesh Distance Field. [Mesh Distance Field quality](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine#quality) may require a higher resolution to capture important details that would normally show up with shadow mapping. For this reason, it is recommended to use a combination of Cascaded Shadow Maps for areas close to the camera, and Distance Field Shadowing for farther distances.

![Cascaded Shadow Maps](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9ab2730-8012-4c15-b699-66698cf5c35f/06-mdf-properties-cascaded-shadow-maps.png)

![Distance Field Shadows](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45cd30f2-704e-4515-9b31-9e5e1c860082/07-mdf-properties-distance-field-shadow.png)

Despite the distance of all points of the lift from the ground, the shadow remains crisp and detailed when using Cascaded Shadow Mapping. Distance Field Shadows allow for softening of the shadow, based on the **Light Source Radius** and the distance of the shadow being cast from the surface, which provides a natural look.

#### Distance Field Trace Distance

The **Distance Field Trace Distance** controls how far Distance Field Shadowing can extend for any mesh that is casting shadows. Because shadows can extend along receiving surfaces for very long distances, this can cause Distance Field Shadows to increase performance cost for densely populated scenes. Lowering the Distance Field Trace Distance limits how far any one point of the Distance Field Shadow can be cast from a particular mesh without using a shorter **Distance Field Shadow Distance**.

![Distance Field Trace Distance: | 10000 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd2eb9cc-54a7-478d-a4f7-0921eeabab86/08-mdf-properties-distance-trace-10k.png)

![Distance Field Trace Distance: | 5000](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10f18c12-62ba-41f7-8fa3-c4f15c96acfa/09-mdf-properties-distance-trace-1k.png)

In this example, a very tall tree is being lit by a Directional Light with a shallow angle (like at sunrise or sunset). Lowering the Distance Field Trace Distance limits the top of the tree from casting indefinitely.

### Point/Spot Light

Below are the **Point** and **Spot Light** settings that affect [Distance Field Shadowing](/documentation/en-us/unreal-engine/distance-field-soft-shadows-in-unreal-engine).

![Point and Spot Light settings that affect DFS](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/847626d6-7564-424a-9af0-792145581997/10-mdf-properties-point-spot-light.png)

| Property | Description |
| --- | --- |
| Light |   |
| **Source Radius** | This is used as the size of the light source sphere. When you use larger values, you get a larger penumbra, but it can cause slightly lower performance. |
| Distance Field Shadows |   |
| **Distance Field Shadows** | This controls whether to use Distance Field area shadows. |
| Distance Field Shadows Advanced Properties |   |
| **Ray Start Offset Depth Scale** | This controls how large of an offset Distance Field Shadows have from the receiving surface as the camera gets further away. This can be useful to hide self-shadowing artifacts from low-resolution distance fields on large Static Meshes. |

#### Source Radius

The Light's **Source Radius** is used to soften or sharpen area shadowing by adjusting the size representation of the light source itself. Like the Directional Light's [Light Source Angle](/documentation/en-us/unreal-engine/mesh-distance-fields-properties-in-unreal-engine#lightsourceangle), the shadows will soften as the shadowed point gets farther from a receiving surface.

![Source Radius: | 0 (Default) ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98301b68-b6a7-420e-b663-0acbc283f474/11-mdf-properties-source-radius-0.png)

![Source Radius: | 50 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99077559-392d-4071-9ba5-c8a6ce7826a5/12-mdf-properties-source-radius-50.png)

In this demonstration, the default value of 0 uses a hard-coded Source Radius of 20, to automatically provide soft area shadowing. The larger light source radius of 50 has much softer shadows.

The default Source Radius of 0 has a set hard-coded value of 20. When using a value greater than 0 and less than 20, the area shadows will sharpen accordingly.

#### Traditional Shadow Maps VS Distance Field Shadows

The shadow maps for Point and Spot Lights are very detailed and sharp, similar to Cascaded Shadow Maps for Directional Lights. The quality of Ray Traced Distance Field Shadows relies heavily on the resolution of the volume texture generated for the Mesh Distance Field. [Mesh Distance Field quality](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine#quality) may require a higher resolution to capture important details that would normally show up in a shadow map.

![Traditional Shadow Map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9364704-e92f-4145-8920-0c5d175864b6/13-mdf-properties-shadow-maps.png)

![Distance Field Shadow](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3b9a795-7816-4f81-ade9-359d14873814/14-mdf-properties-distance-field-shadow.png)

Despite the distance of all points of the lift from the ground, the shadow remains crisp and detailed when using shadow mapping. Distance Field Shadows allow for softening of the shadow based on the **Source Radius** and the distance of the shadow being cast from the surface, which provides a natural look.

#### Ray Start Offset Depth Scale

The **Ray Start Offset Depth Scale** controls the ray starting point for the Distance Field Shadows for a receiving surface, as the camera moves farther away. It helps to prevent self-shadowing artifacts that appear from low-resolution Mesh Distance Fields, or from meshes that have complex geometry which can't be reasonably captured in a volume texture.

In some cases, adjusting the [Mesh Distance Field quality](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine#quality) can reduce or remove these artifacts, without adjusting where the ray starts. Keep in mind that you may not want to pay the higher memory cost the generated volume texture would require. Ray Start Offset Depth Scale can help curb that cost for this light.

![Ray Start Offset Depth Scale: | 0.003 (Default) ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a075e580-0b0a-469b-ba7e-cfce5a5d7dc0/15-mdf-properties-ray-start-offset-003.png)

![Ray Start Offset Depth Scale: | 0.007 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2abe0e55-d10c-4622-b4a6-3f7105af090f/16-mdf-properties-ray-start-offset-007.png)

Some self-shadowing artifacts are present in the rock face where it has some crevices and the resolution of the Distance Field doesn't capture that amount of detail. Adjusting the **Ray Start Offset Depth Scale** a minimal amount will change where the shadow trace should begin by moving it inward.

This setting should only be adjusted by small amounts, as this can affect shadowing for any mesh that casts shadows from the light source which has been adjusted. When adjusting this setting, be cautious, and check different areas of your level. This check is especially important for Directional Lights and distance objects where it could have the most impact on visual quality.

### Sky Light

Below are the **Sky Light** settings that affect [Distance Field Ambient Occlusion](/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine) (DFAO). These settings provide the most artistic control of DFAO in your levels.

![Sky Light settings that affect DFS](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77bdb449-4a9c-4c2e-a45f-71aeb3132eea/17-mdf-properties-sky-light-dfs-settings.png)

| Property | Description |
| --- | --- |
| **Occlusion Max Distance** | This is the maximum distance from an occluder to compute occlusion contribution. Raising this value will increase the cost of Distance Field AO, but will allow occlusion from further away. |
| **Occlusion Contrast** | This can be used to raise the contrast of the computed occlusion. |
| **Occlusion Exponent** | This is an exponent applied to AO. Values lower than 1 will brighten the occlusion without losing contact shadows. |
| **Min Occlusion** | This is useful to prevent the occlusion from going fully black when desired. This is also useful to simulate multi-bounce lighting, which would have prevented any areas from going fully black in real life. |
| **Occlusion Tint** | This is constant color used to color the occlusion. This should be black to be physically correct; other values can provide artistic stylization. |
| **Occlusion Combine Mode** | 
This controls how occlusion from Distance Field Ambient Occlusion is combined with Screen Space Ambient Occlusion:

-   **OCM Minimum**: This takes the minimum occlusion value. This is effective for avoiding over-occlusion from multiple methods, but can result in the indoors looking too flat.
-   **OCM Multiply**: This takes the occlusion values from Distance Field Ambient Occlusion and Screen Space Ambient Occlusion and multiplies them. It gives a good sense of depth everywhere, but it can cause over-occlusion. Screen Space Ambient Occlusion should be tweaked to be less strong compared to Minimum.



 |

#### Occlusion Max Distance

The **Occlusion Max Distance** controls the maximum distance between two points, where occlusion of one point can affect another. When you adjust the Occlusion Max Distance, it also adjusts the accuracy that DFAO will have with other objects in the scene, which means you're increasing the performance cost of it as well.

![Occlusion Max Distance: | 1000 (Default) ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c8bc15c-4b4d-4f55-b512-7b46df22fe35/18-mdf-properties-default-view.png)

![Occlusion Max Distance: | 500 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3bd6ca52-5815-4ec3-9948-2564c2ecd5ef/19-mdf-properties-max-distance-500.png)

Lowering the Occlusion Max Distance means that shadowing detail can't be captured for occlusion, since the distance between these points will not cause them to affect the other.

![Occlusion Max Distance: | 1000 (Default) ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82f67c32-6398-45e6-9f68-1d5be82db6b8/18-mdf-properties-default-view.png)

![Occlusion Max Distance: | 1500 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92c5db65-3939-4574-bee2-8598b8274e48/20-mdf-properties-max-distance-1500.png)

Increasing the Occlusion Max Distance will increase the accuracy of occlusion, because more points can be considered for shadowing, but it does come at a higher performance cost.

#### Occlusion Contrast

The **Occlusion Contrast** controls the difference in brightness between objects affected by DFAO.

![Occlusion Contrast: | 0 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89670761-c231-44f6-ba62-d78e85c68f68/18-mdf-properties-default-view.png)

![Occlusion Contrast: | 0.65](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08cb145e-053d-40e0-af07-8a696ae20031/21-mdf-properties-contrast-065.png)

Increasing the value for Contrast darkens a lot of the crevices and areas that are heavily occluded in this scene.

#### Occlusion Exponent

The **Occlusion Exponent** controls the power of the value being applied to the ambient occlusion. Lower values will brighten up the occlusion shadows, without losing the details for any contact shadowing near surfaces.

The Occlusion Exponent uses a default middle-ground value that works well for most scenes. Below are some comparisons of lower and higher range values.

![Occlusion Exponent: | 1 (Default) ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8357a26-e8fe-4f1c-9f61-50175fbb8e79/18-mdf-properties-default-view.png)

![Occlusion Exponent: | 0.6](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9720288b-b571-4a5e-bd6f-4cee59ee114f/22-mdf-properties-exponent-06.png)

With the lower value, occlusion for the scene becomes lighter anywhere that is shadowed using DFAO.

![Occlusion Exponent: | 1 (Default) ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8956bec2-7942-402a-9e47-b1f4e984dea0/18-mdf-properties-default-view.png)

![Occlusion Exponent: | 1.6](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe9be396-1ac7-4b61-b841-494b2a7656ee/23-mdf-properties-exponent-16.png)

With the higher value, occlusion for the scene becomes darker anywhere that is shadowed using DFAO.

#### Min Occlusion

The **Min Occlusion** controls how dark any fully occluded areas can get in your level. It gives artists extra control over lightening DFAO in the occluded areas. This setting works well when used with **Occlusion Max Contrast**. Where occluded areas are darkened too much with Occlusion Max Contrast, you can then use Min Occlusion to lighten the shadowing a bit.

![Min Occlusion: | 0 (Default](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/133cb091-4b3c-4983-b4ca-e75dd0fc84a7/18-mdf-properties-default-view.png)

![Min Occlusion: | 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49d7bcf4-43ac-4334-82e9-f7d7efb69e0f/24-mdf-properties-min-occlusion-05.png)

Here, Min Occlusion brightens up the DFAO occluded areas of the scene.

#### Occlusion Tint

The **Occlusion Tint** affords artists the most control over the look of DFAO by enabling the color for occluded areas to be adjusted.

![Occlusion Tint Color: | Black (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a98d47e-5325-4711-a482-233be979b871/18-mdf-properties-default-view.png)

![Occlusion Tint Color: | Purple](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9a451c5-3924-43dc-b1ef-d58454830081/25-mdf-properties-tint-purple.png)

Only occluded areas that are shadowed by DFAO will be tinted based on the color values used.

#### Occlusion Combine Mode

The **Occlusion Combine Mode** enables you to choose to combine Screen Space Ambient Occlusion with Distance Field Ambient Occlusion in the scene.

![Occlusion Combine Mode: | OCM Minimum](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec9bec8d-5441-45b2-8097-6e29b0f3e288/18-mdf-properties-default-view.png)

![Occlusion Combine Mode: | OCM Multiply](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9269e1ff-9aca-4ada-856c-e840dfd453cc/26-mdf-properties-comb-mode-multiply.png)

## Static Mesh Editor

The **Static Mesh Editor** contains several Actor-specific settings that affect any instance of this Actor placed in your Levels. These Actor-specific settings are within the **Build Settings** and **General Settings** sections of the **Details** panel in the Static Mesh Editor.

Click image for full size.

### Build Settings

The **Build Settings** enable you to control the quality of your Mesh Distance Field, to enable two-sided generation for objects like foliage, and even to assign the Distance Field of another mesh to the current one.

![Build settings that affect DFS](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4888b797-07cf-4e3e-b1ef-0272cfd6c232/28-mdf-properties-build-settings.png)

| Property | Description |
| --- | --- |
| **Distance Field Resolution Scale** | This enables you to adjust the quality of this Actor's generated Mesh Distance Field. This setting has an impact on the size of the volume texture that is created. |
| **Two-Sided Distance Field Generation** | This enables you to control whether the generated Mesh Distance Field should be two-sided or not. This allows for soft shadows in instances where there are multiple planes that would overlap, but it comes at a higher performance cost. |
| **Distance Field Replacement Mesh** | This enables you to select the Distance Field of another Static Mesh to use in place of the current Actor's own Mesh Distance Field. |

### General Settings

In the **General Settings**, you can enable options that are not quality-related. It includes the ability to generate a Mesh Distance Field for a particular mesh, without requiring Mesh Distance Fields to be enabled for the entire project. You can also control the self-shadowing that can occur with Static Meshes that are animated, or that move their vertices inside of the Distance Field.

![General settings that affect DFS](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab051a53-61d7-4558-9d60-994bde9919f5/29-mdf-properties-general-settings.png)

| Property | Description |
| --- | --- |
| **Generate Mesh Distance Field** | This controls whether to generate a Distance Field for this mesh, which can be used with [Distance Field Indirect Shadows](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine). This is ignored if the Project Setting for **Generate Mesh Distance Fields** is enabled. |
| **Distance Field Self Shadow Bias** | This is used for reducing self-shadowing from Distance Field methods when using World Position Offset to animate the mesh's vertices. |

## Actor Components

Below are the available Distance Field settings that can be toggled or overridden for individual Actors placed in your Levels.

![Actor settings that affect DFS](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e53e84c6-27d6-438c-9e06-4a52a759b49f/30-mdf-properties-actor-dfs-settings.png)

| Property | Description |
| --- | --- |
| **Distance Field Indirect Shadow** | This controls whether to use the Mesh Distance Field representation (when present) for shadowing indirect lighting on movable components (such as from lightmaps or skylight). This works like [Capsule Shadows](/documentation/en-us/unreal-engine/capsule-shadows-in-unreal-engine) on Skeletal Meshes, except it uses the Mesh Distance Field, so no physics asset is required. The Static Mesh must have **Generate Mesh Distance Field** enabled in the Build Settings, or the project must have **Generate Mesh Distance Fields** enabled in order for this feature to work. |
| **Override Distance Field Self Shadow Bias** | This controls whether to override the Distance Field Self Shadow Bias setting of the Static Mesh Asset, replacing it with the Distance Field Shadow Bias of this component. |
| **Distance Field Indirect Shadow Min Visibility** | This controls how dark the Distance Field Indirect Shadow can be. |
| **Distance Field Self Shadow Bias** | This is useful for reducing self-shadowing from Distance Field methods when using World Position Offset to animate the mesh's vertices. |
| **Affect Distance Field Lighting** | This controls whether the primitive should affect dynamic Distance Field Lighting methods. This flag also requires that Cast Shadow be enabled. |

#### Distance Field Indirect Shadow Min Visibility

When using [Distance Field Indirect Shadows](/documentation/en-us/unreal-engine/using-distance-field-indirect-shadows-in-unreal-engine), the shadow's tone can be adjusted using the **Distance Field Indirect Shadow Min Visibility** setting. It gives artists more control over how dark these shadows can be, enabling the indirect shadows to blend with the surrounding static shadowing.

![Setting up the Distance Field Indirect Shadow Min Visibility](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93ae1b18-5407-4ab6-baf6-9e055b7ecf54/31-mdf-properties-dfis-min-visibility.png)

![Min Visibility: 0.1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45cec879-53d6-4323-9132-d9eb4ca40da4/32-mdf-properties-dfis-min-visibility-1.png)

![Min Visibility: 0.6](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0b0452d-0f53-4416-9273-27c1261ded22/33-mdf-properties-dfis-min-visibility-2.png)
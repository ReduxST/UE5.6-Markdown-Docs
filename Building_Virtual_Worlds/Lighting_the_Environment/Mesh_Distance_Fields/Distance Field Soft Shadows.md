# Distance Field Soft Shadows

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/distance-field-soft-shadows-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/distance-field-soft-shadows-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:50

---

Shadowing from movable light sources is provided using object Distance Fields for each rigid mesh to compute efficient area shadowing from dynamic light sources. In Unreal Engine, this is called **Distance Field Shadows** (DFS). To calculate shadowing, a ray is traced from the point being shaded through the scene's Signed Distance Fields (SDF) toward each light. The closest distance to an occluding object is used to approximate a cone trace for about the same cost as the ray trace. It allows for high-quality area shadowing from spherical light source shapes.

## Scene Setup

This feature requires that **Generate Mesh Distance Fields** be enabled in your **Project Settings** in the **Rendering** section. See the [Mesh Distance Fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine) page for more information.

To enable Distance Field Shadowing, start by dragging a **Light** into the scene and set its Mobility to **Movable** and then from the Light **Details** panel, enable **Distance Field Shadows**.

![Enable Distance Field Shadowing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/972ad54a-e041-48f0-a64a-6010c68a480c/01-dfss-light-df-settings.png)

For a step-by-step guide, follow the [Using Distance Field Shadowing](/documentation/en-us/unreal-engine/using-distance-field-indirect-shadows-in-unreal-engine) How-To guide to learn more.

### Area Shadowing Settings

Each Light type can use Distance Fields shadows to create soft area shadows. These shadows simulate real-world shadows by retaining sharp contact shadows closer to the base and softening the farther the shadow stretches away.

![Traditional Shadow Map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13386be2-ed8b-418f-a811-4bd9a42f8b56/02-dfss-default-shadow-map.png)

![Distance Field Shadow](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/216db7cc-36f3-478d-b41a-f7b435dbb86a/03-dfss-df-shadow-map.png)

For additional information about Light source settings and additional examples, see the [Mesh Distance Fields Reference](/documentation/en-us/unreal-engine/mesh-distance-fields-properties-in-unreal-engine#lightcomponents) page.

### Point and Spot Light Source Radius

For Point and Spot Lights, the **Source Radius** is used to determine how large shadow penumbras are on a light. Area shadows are computed with sharp contacts that get softer over long distances. On a Point and Spot Light, it is represented by a yellow sphere.

![Source Radius representation of the Point and Spot Light in the Viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2dc946d-db04-4469-8468-d8fc7b262ab0/04-dfss-light-df-settings.png)

The Editor draws the source shape of the light with yellow lines.

The Light's source radius sphere should not be intersecting the scene, or it will cause lighting artifacts.

![Source Radius: | 0 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0819ab7d-6bb4-426b-b250-dbe4341cb0e5/05-dfss-source-radius-0.png)

![Source Radius: | 50 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43e953fe-4a27-4341-9baa-6908c098bf37/06-dfss-source-radius-50.png)

The Distance Field shadows are from a Point Light using a Source Radius to soften the shadows cast by the doorway, bench, and piano on the surrounding geometry.

For additional information about Point and Spot Light settings, see the [Mesh Distance Fields Reference](/documentation/en-us/unreal-engine/mesh-distance-fields-properties-in-unreal-engine) page.

### Directional Light Source Angle

For Directional Lights, the **Light Source Angle** is used to determine how large shadow penumbras are on a light. Distance Field Shadows have very few self-intersection problems and therefore avoid the leaking and over-biasing problems in the distance that traditional shadow mapping would have.

![Source Angle: | 1 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a009cf7-bae3-47ce-9d85-7e887a51cca8/07-dfss-shadow-source-angle-1.png)

![Source Angle: | 3 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c041088-9992-4998-938d-68bb274f3d56/08-dfss-source-angle-3.png)

*Distance Field Shadows from a Directional Light with a Light Source Angle adjusted for softer shadowing.*

In most cases, Cascaded Shadow Maps (CSM) are used to provide dynamic shadowing of a Directional Light. These require rendering the meshes in the scene into several cascade shadow maps (levels of detail for shadowing). The cost of shadowing increases at large shadow distances because of how many meshes and triangles are being rendered into the shadow maps.

Distance Field Shadows work much more gracefully in the distance, doing shadowing work only for visible pixels. Cascaded Shadow Maps can be used to shadow an area near the camera while RTDF shadows will shadow farther regions up to the **Distance Field Shadow Distance** that is set.

![Cascaded Shadow Maps Only ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1da5aeb1-bf42-4180-a0d2-30cedca473c7/09-dfss-cascaded-shadow-maps.png)

![Cascaded Shadow Maps & Distance Field Shadows ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/536d88ee-c1ef-4f10-a83a-4379fa877185/10-dfss-cascaded-and-df-shadows.png)

When Distance Field Shadows are enabled, anything beyond the set value for **Cascaded Shadow Map Distance** will be shadowed using Distance Fields. In the comparison using both CSM and RTDF shadowing, the CSM shadow is set to 1,000 CM (centimeters), which allows for sharp shadowing near the camera with lots of added detail. In the shadowing distance beyond 1,000 CM, RTDF shadowing is used, which shadows objects up to 1.2 KM (kilometers) away. This enables the trees in the far distance to cast shadows when this would be too costly for Cascaded Shadow Maps.

For additional information about Directional Light settings, see the [Mesh Distance Fields Reference](/documentation/en-us/unreal-engine/mesh-distance-fields-properties-in-unreal-engine) page.

## Scene Representation

Each level that you create is made up of all these Mesh Distance Fields for your placed Actors. When Mesh Distance Fields are generate, they are done so "offline" using triangle raytracing that stores the results in a volume texture. Because of this, mesh distance field generation cannot be done at runtime. This method computes the Signed Distance Field rays in all directions to find the nearest surface and stores that information.

You can visualize the Mesh Distance Fields that represent your scene by using the viewport and selecting **Show > Visualize > Mesh Distance Fields**.

|   |   |
| --- | --- |
| 
 | 

 |
| Menu to Enable Visualization | Mesh Distance Field Visualization |

Click images for full size.

When you see areas that are more white than gray, it means that many steps were needed to find the intersection of the mesh surface. Rays at grazing angles to surfaces took many more steps to intersect than would have for a simpler mesh.

### Mesh Distance Field Quality

Distance Field shadow fidelity has a significant impact on shadow accuracy, more so than [Distance Field Ambient Occlusion](/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine). Increased Mesh Distance Field resolution will improve the shadows cast by Static Meshes. Use the Mesh Distance Field Visualization to inspect the quality.

The following example shows scene with Distance Field Shadowing with different Distance Field Resolution.

![Distance Field Resolution: | 1 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c169558-0d9d-4519-b1a4-9b6517cefb84/11-dfss-resolution-1a.png)

![Distance Field Resolution: | 5 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/daa44e34-07a3-4b39-9c95-bba997ac10f3/12-dfss-resolution-1b.png)

The following example shows scene with Mesh Distance Field visualization with different Distance Field Resolution.

![Distance Field Resolution: | 1 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97ef664a-805d-48ff-8b50-5aa0847a7b37/13-dfss-resolution-2a.png)

![Distance Field Resolution: | 5 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad5c6a6f-5308-4dbc-8d4c-8e31d2cd137a/14-dfss-resolution-2b.png)

Shadows for Mesh Distance Fields are computed at half-resolution with a depth-aware upsample. **Temporal Anti-Aliasing** (TAA) does a good job of helping reduce the flickering that can happen with half-resolution but jagged edges can still appear sometimes.

For additional information about Mesh Distance Field quality, see the [Mesh Distance Fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine) page.

## Performance

The following GPU times were done on a Radeon 7870 at a resolution of 1920x1080 in a full game scene:

| Test | Cascaded/Cuebmap Shadow Maps Cost (ms) | Distance Field Shadows Cost (ms) | Percentage (%) Faster |
| --- | --- | --- | --- |
| Directional Light with distance of 10k units, 3 Cascaded Shadow Maps | 3.1 | 2.3 | 25% |
| Directional Light with distance of 30k units, 6 Cascaded Shadow Maps | 4.9 | 2.8 | 43% |
| One Point Light with a large radius | 1.8 | 1.3 | 30% |
| Five Point Lights with a small radius | 3.2 | 1.8 | 45% |

### Optimizations

Below are some things you can do or should consider to optimize Distance Fields shadowing:

-   On a Directional Light, a larger **Source Angle** increases cost as more objects have to be considered for each point being shadowed.
-   Larger values for **Distance Field Shadow Distance** reduce the culling efficiency.
-   Shadows from meshes with **Two-Sided Distance Field Generation** (enabled in the **Build Settings**) will cost more as the resulting shadows are never fully opaque.

## Limitations

Distance Field Shadowing shares the general limitations of the Mesh Distance Fields technique. For more information about these limitations, see the [Mesh Distance Fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine) page.
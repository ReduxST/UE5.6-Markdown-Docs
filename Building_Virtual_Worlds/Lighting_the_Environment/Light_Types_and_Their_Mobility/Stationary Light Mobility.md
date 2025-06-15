# Stationary Light Mobility

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/stationary-light-mobility-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/stationary-light-mobility-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:23

---

Lights that have their Mobility set to **Stationary** are lights that are intended to stay in one position, but are able to change in other ways, such as their brightness and color. This is the primary way they differ from [Static Lights](/documentation/en-us/unreal-engine/static-light-mobility-in-unreal-engine), which cannot change in any way during gameplay.

Of the three light mobilities to choose from, Stationary lights have the highest quality, medium mutability, and medium performance cost.

Stationary Lights use both dynamic and static lighting to achieve its result, with indirect lighting and shadowing being stored within lightmaps for the Level. Direct shadows are stored within shadow maps. These lights make use of Distance Field Shadows, meaning that their shadows can remain crisp even with fairly low lightmap resolutions on lit objects.

## Stationary Direct Lighting

Stationary Lights use both dynamic direct lighting and static indirect lighting to achieve its result. The indirect lighting and shadowing is stored in lightmaps, while direct shadowing is stored in shadow maps. Because Stationary Lights are rendered dynamically using deferred shading, their brightness and color is able to change at runtime, and also support [Light Functions](/documentation/en-us/unreal-engine/using-light-functions-in-unreal-engine) and [IES Profiles](/documentation/en-us/unreal-engine/using-ies-light-profiles-in-unreal-engine) in the same way.

Stationary Lights also have high quality analytical specular, like [Movable Lights](/documentation/en-us/unreal-engine/movable-light-mobility-in-unreal-engine).

![Stationary Directional Light | with Movable objects](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3a44ef0-9969-4e2e-94e6-a6af854991f7/stationary-light-with-movable-objects.png)

![Static Directional Light | with Movable objects](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b81057ce-20dc-4d1b-9321-e8878c72cfd4/static-light-with-movable-objects.png)

## Stationary Light Shadowing

Only four or fewer Stationary Lights can overlap one another or any single piece of geometry in the Level, meaning that in some cases you will have fewer Stationary lights that can overlap in some parts of your Level. Shadowing cannot affect the overlap test, so the Directional Light typically requires a channel from the entire Level it is in, even areas that may be underground or hidden by other geometry. Once the channel limit is reached, only dynamic (or whole scene shadows) are used, which brings with it considerable performance cost.

When the limit of up to four Stationary Lights overlap at any time within a Level, the light icon will change to one with a **Red X** over the offending light until the overlap limit is resolved. There is a **Stationary Light Overlap** visualization mode that highlights offending lights in red until the overlap is resolved.

Enable the **Stationary Light Overlap** visualization from the Level Editor **View Mode > Optimization Viewmodes** dropdown selection.

![level editor menu stationary light overlap visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4a34bf4-8b3a-4938-be17-8d37d47293bf/stationary-light-overlap-visualization-menu.png)

### Stationary Indirect Lighting on Opaque Materials

[Lightmass](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine) generates distance field shadow maps for Stationary Lights on Static objects during the lighting build process. Distance field shadow maps provide accurate shadow transitions, even at lower resolutions, and incur very little runtime cost. For example, lightmaps require uniquely unwrapped UVs on all meshes that have their mobility set to Static and have indirect lighting from a Static or Stationary light source.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b489ff4b-7188-4658-8c8b-bcf45d091734/distancefieldshadows.png)

Accurate shadowing of a Static Mesh Actor onto opaque surfaces.

Lighting must be built to display shadows from Stationary or Static light sources, otherwise dynamic shadows are used.

### Stationary Indirect Lighting on Translucent Materials

Translucency recieves shadowing at low cost with Stationary Lights since Lightmass precomputes a shadow depth map from Static geometry in the Level. That shadow depth is applied to translucency at runtime. This form of shadowing is fairly coarse and only captures shadowing in meters.

![Unshadowed Translucency](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b922f08d-d9e0-4187-9185-410eca9bd3ef/1originalcropped.png)

![Translucency receiving static shadowing | from a Directional Light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b360408a-880f-42d1-93bf-1f60150bcb1b/1shadowedcropped.png)

The resolution of the static shadow depth map is controlled with `StaticShadowDepthMapTransitionSampleDistanceX` and `StaticShadowDepthMapTransitionSampleDistanceY` in the `BaseLightmass.ini` configuration file. It has a default value of 100, meaning one texel every meter.

### Stationary Light Dynamic Shadowing

Dynamic objects, such as Static Meshes with their Mobility set to Movable and Skeletal Meshes, must integrate into the world from shadow maps, which is accomplished with per object shadows. Each Movable object creates two dynamic shadows from a given Stationary Light: a shadow to handle the static world *onto the movable object*, and a shadow to handle the movable object *casting onto the world*.

With this setup, the only shadowing cost for Stationary Lights comes from the Movable objects it affects. It also means the cost can vary from very little to a large amount depending on how many Movable objects there are. With enough Movable objects being affected, it's actually more efficient to use a light with its Mobility set to Movable.

In the example scene below, the spheres have their Mobility set to **Movable** and the rest of the scene geometry is set to

In the example scene below, a Stationary Directional Light is used to light the scene. The spheres have their Mobility set to **Movable** with the rest of the scene set to **Static**. Lighting has been built for the scene. The per object shadow frustums of each Movable sphere integrates seamlessly with the scene by receiving shadows from the objects behind and casting their own shadows that blend with the ones on the ground.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa54d292-769f-4247-9af3-2719adbff85d/dynamicobjectshadowfrustums.png)

Per object shadows used by Movable components apply a shadow map to the object's bounds, therefore the bounds of the object must be accurate. For Skeletal Meshes, this means they should have a Physics Asset. For Particle Systems, a fixed bounding box must be large enough to contain all particles it generates.

#### Stationary Directional Light Dynamic Shadowing

Directional Stationary Lights are special in that they support whole scene shadows through **Cascaded Shadow Maps** at the same time as precomputed static shadowing. This is useful in scenes with lots of animating foliage where you want to have moving shadows around the player but do not want to pay the cost of having many levels of cascaded shadow maps covering a large view range at a larger cost.

A Directional Stationary Light uses Cascaded Shadow Maps for direct shadowing near the player within a specified range with **Dynamic Shadow Distance Stationary Light**. Any shadows beyond this distance fades into precomputed static shadows stored in lightmaps. By default, all Directional Stationary Lights start with a value of 0, meaning there is no dynamic shadowing taking place.

To save performance when you have a lot of Movable objects in the scene but want to use a smaller dynamic shadow distance, enable **Inset Shadows for Movable Objects**. It allows for movable objects to have a shadow even when they are outside of the cascaded shadow maps range and reduces shadowing cost significantly if there are many movable objects in the scene.

### Stationary Light Indirect Shadowing

Stationary Lights store their indirect lighting in lightmaps when lighting is built for the Level, just like Static Lights do. Indirect Lighting cannot be modified without invalidating lighting and needing to be rebuilt with exception to changing the Light's **Intensity** and **Light Color**. However, this does not affect the intensity or colors of the baked shadows.

A **Post Process Volume** does enable indirect shadows intensity and color to be changed using the **Global Illumination** category properties for **Indirect Lighting Color** and **Indirect Lighting Intensity**.

#### Use Area Shadows for Stationary Lights

whether to use area shadows for stationary light precomputed shadow maps. area shadows get softer the further they are from shadow casters, but require higher lightmap resolution to get the same quality where the shadow is sharp.

By default, Static Lights automatically use area shadows — crisp, hard shadowing near surface contacts with softer shadows the farther surfaces are apart from one another — when building lighting. For Stationary Lights, the property **Use Area Shadows for Stationary Lights** enables soft area shadowing for any Static geometry in the scene affected by this light.

This property is enabled on Stationary Lights under the **Lightmass** section in the Light's **Details** panel.

![Default Stationary Shadows | for Static Geometry](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c08da1f2-025a-42fe-99bb-541f5345fa34/uniformpenumbrasharp.png)

![Area Shadows Enabled | for Static Geometry](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e022445c-c46f-41eb-a5c6-1615eac7fbb0/areashadows.png)

**Use Area Shadows for Stationary Lights** is only available on Stationary Lights and require higher lightmap resolutions for good results.
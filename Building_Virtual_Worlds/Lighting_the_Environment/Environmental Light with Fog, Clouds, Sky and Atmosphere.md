# Environmental Light with Fog, Clouds, Sky and Atmosphere

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/environmental-light-with-fog-clouds-sky-and-atmosphere-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/environmental-light-with-fog-clouds-sky-and-atmosphere-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:22

---

Unreal Engine provides a set of components that allow for designers and artists to create immersive worlds with physically based lighting at large — or even small — scale while working efficiently to do so. These environment lighting components for atmosphere, clouds, fog, and lighting all work seamlessly together to create a unified experience that supports fully dynamically lit worlds.

The tools and features in this page will help you get started with creating your own worlds.

## Light Mixer

The **Light Mixer** is a dockable editor window where you can add, edit, and reference properties of Directional, Point, Spot, and Rect Lights in your Level.

For artists and designers, this window simplifies and can speed up your workflow by having them availabl and editable in one location. This includes lights that are components of scene Actors or of Blueprints. You can use Collections to organize them as well.

![Light Mixer Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/550aff9a-55a6-491f-b3d2-e12819d6cec2/light-mixer.png)

For more information, see [Light Mixer](/documentation/en-us/unreal-engine/using-the-light-mixer-in-unreal-engine).

## Environment Light Mixer

The **Environment Light Mixer** is a dockable editor window where you can add, edit, and reference properties of environment lighting components for sky, clouds, atmosphere lights, and a sky light.

For artists and designers, this window simplifies and can speed up your workflow by having them all available in one location.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/841425de-12be-4260-86af-5de3a8b8c6b7/1_envlightmixer.png)

For more information, see [Environment Light Mixer](/documentation/en-us/unreal-engine/environment-light-mixer-in-unreal-engine).

## Fog Effects

Fog effects are useful for adding ambiance to the world and setting the mood for environments. This includes creating multi-layered fog for high and low-lying areas, and volumetric effects for light shafts.

![volumetric fog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b601a1b-9615-44c6-ac55-1d6e9e96616b/volumetricfog.png)

The [Sky Atmosphere](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine) includes its own scattering and height fog simulation, but also works well with the Exponential Height Fog to support all types of lights in the scene.

![Sky Atmosphere's Height Fog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bd51de6-18a6-4d43-b297-b18db13f0eef/skyatmos_heightfog.png)

![Sky Atmosphere | with Exponential Height Fog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a5357b4-801b-41a8-90e0-ca3b018bb6ea/expoheightfog_2.png)

When the Project Setting **Support Sky Atmosphere Affecting Height Fog** is enabled, any contribution from Exponential Height Fog is additive. The Sky Atmosphere's height fog is applied on top of the Exponential Height Fog colors. However, should the **Fog Inscattering Color** and **Directional Inscattering Color** be set to black, the Sky Atmosphere will directly affect and influence the coloring of any Exponential Height Fog in the scene.

Additionally, you can used locally placed fog volumes to create fog effects in large or small areas of your scene. These local fog volumes support all platforms and volumetric fog effects when enabled.

![Placed Local Fog Volumes in a scene.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/330d7c67-0eed-4a51-bd52-7354b773bcfe/lfv-withfog.png)

### Fog Effects Topics

%building-virtual-worlds/lighting-and-shadows/environmental-lighting/volumetric-fog:Topic%

## Atmosphere, Cloud, and World Lighting Effects

The lighting components for Sky Atmosphere, Volumetric Clouds, Directional Lights, and Sky Light make up the majority of your enviornment lighting. These components all work seamlessly together dynamically lit large worlds possible.

![enviornment lighting components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef42c940-2d34-4ad3-9add-815eb398e3b0/vt_cloudexamples.png)

In your Levels, you can use the following components:

-   Up to two Directional Lights for the sun and moon, two suns, or any combination.
-   A single Sky Light with optional real-time capturing.
-   A Sky Atmosphere with its own height fog.
-   Volumetric Clouds with or without a sky dome mesh.

With **Real Time Capture** enabled on the Sky Light, use the keyboard shortcut **Right Ctrl + L** (first Directional Light) or **Right Ctrl + Right Shift + L** (second Directional Light) in combination with moving the mouse to change lighting dynamically and see the results instantly.

### Atmosphere, Clouds, and World Lighting Topics

%building-virtual-worlds/lighting-and-shadows/light-types-and-mobility/Directional:Topic%

### Atmosphere, Clouds, and World Lighting Properties Reference

## Material and Sparse Volume Texture Assets

%building-virtual-worlds/lighting-and-shadows/environmental-lighting/sparse-volume-texture:Topic%
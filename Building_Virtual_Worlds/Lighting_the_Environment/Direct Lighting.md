# Direct Lighting

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/features-and-properties-of-lights-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/features-and-properties-of-lights-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:35

---

Lights in Unreal Engine contain a large set of properties to work with, which are partly dependent on the [Light's mobility and type](/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine).

Light properties are found in the **Details** panel when a light is selected in the Level. Depending on the set **Mobility** of **Static**, **Stationary**, or **Movable** determines what features and properties of the light are supported for the selected light.

![directional light properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f7074f5-1c67-44c8-9e1a-cab962a4bac0/light-properties.png)

Light properties of a Directional Light.

## Things to Consider for Lights and their Properties

Before diving into the specific features and properties of Lights, you'll want to consider the following:

-   What types of lights does your scene require to light it?
-   What Mobility should your lights have?
-   Lights with different mobilities can be mixed and matched as needed to light a scene. However, considerations must be considered for what that means for the lighting, shadows, and assets it affects within the Level. Not all properties support every mobility or light type.
-   [Shadowing](/documentation/en-us/unreal-engine/shadowing-in-unreal-engine) is a broad subject with lighting. Mobilities, type of light, or even enabled lighting features in the Project Settings can affect how lighting works within the project.
-   Some types of lights complement other standalone features, such as one for [Environmental Lighting](/documentation/en-us/unreal-engine/environmental-light-with-fog-clouds-sky-and-atmosphere-in-unreal-engine).

## Setting Properties for Lights

The properties and features of lights can be found in the **Details** panel when a light is selected in the Level.

Each light must have its **Mobility** set to **Static**, **Stationary**, or **Movable**.

![light mobility selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b42ebff6-b79f-474f-9aca-36ec233b1510/il_mobility.png)

All properties of lights are listed no matter what selection is made, but the mobility affects some properties that are supported. For example, Lightmass settings only affect mobilities set to Static or Stationary.

Explore the topics below to learn about some of the features and properties you can use with the Lights in your scenes and projects.

### General Light Features and Properties Topics

A listing of general concepts and features related to all, or most, types of lights you can use. These can be individual features of lights you can use, or properties of lights that work with larger features, like Global Illumination.

%building-virtual-worlds/lighting-and-shadows/features-of-lights/light-functions:Topic%

## Directional Light Features and Properties Topics

The following features work with [Directional Lights](/documentation/en-us/unreal-engine/directional-lights-in-unreal-engine).

%building-virtual-worlds/lighting-and-shadows/features-of-lights/light-shafts:Topic%

## Sky Light Features and Properties Topics

The following features work with a [Sky Light](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine).
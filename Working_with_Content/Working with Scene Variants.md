# Working with Scene Variants

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-scene-variants-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-scene-variants-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:56

---

When you create realtime 3D experiences around design data, you often need to switch the objects in your scene from one state to another. This may mean swapping objects' positions and rotations in 3D space from one place to another, showing and hiding specific objects, changing Materials, turning lights on and off, and so on.

This is a particularly common need in mechanical and industrial design applications, where some industry-standard modeling and scene design tools allow you to set up multiple *variants* to represent different versions of your scene. This is sometimes referred to as *150% BOM* (Bill of Materials), meaning that the scene contains more than 100% of the visible options.

The classic example is a configurator that lets clients choose in advance between different possible options for an expensive vehicle such as a car, motorcycle, or aircraft, before the vehicle is actually assembled or manufactured. The simple example in the video below shows a car configurator that offers multiple options for items such as wheel trims, brake calipers, and body paint colors.

To help you handle these kinds of scenarios in your own visualization projects, Unreal Engine offers a helper called the **Variant Manager**. The Variant Manager makes it easier to set up multiple variants of your scene and to switch between these variants—both in the editor and at runtime. For example, in the sample application shown above, the Variant Manager is set up with each available option. A simple on-screen UMG UI calls Blueprint functions exposed by the Variant Manager to activate those options on demand.

The topics in this section describe what the Variant Manager is and how you can use it to produce similar effects.

## Getting Started

## Tutorials

## Credits

The car model used on this page is courtesy of [Allegorithmic](https://www.substance3d.com/).
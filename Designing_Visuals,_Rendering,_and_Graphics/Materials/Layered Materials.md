# Layered Materials

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/layering-materials-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/layering-materials-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:53

---

Unreal Engine provides two main ways to layer your Materials and create complex blends between unique surface types. These workflows give you a way to apply distinct Material properties to different regions of a single mesh. While you could achieve similar results in a regular Material using texture masks and other per-pixel logic, the two systems documented here produce easier to read Material graphs and a more artist-friendly editing workflow when changes to the Material are needed.

The two workflows for layering Materials are listed below.

-   **Layered Materials** as an extension of the Material Functions system.
-   **Material Layers** as implemented in the Material Instance Editor.

## Layering Materials with Material Functions

This approach to layering Materials works as an extension of the [Material Functions](/documentation/en-us/unreal-engine/unreal-engine-material-functions-overview) system. Each Material type you wish to use as a layer is fully defined within its own Material Function using the [Material Attributes](/documentation/en-us/unreal-engine/material-attributes-expressions-in-unreal-engine) expressions. You then create a base Material which contains all the logic needed to blend between your various layers. Read the two pages below to learn how to use this workflow.

## Material Layers

The [Material Layers](/documentation/en-us/unreal-engine/using-material-layers-in-unreal-engine) system makes it easier to edit layered Materials by providing a user-inteface tab in the [Material Instance Editor](/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui). This **Layer Parameters** tab allows artists intuitively swap layers in and out of a Material Instance, change the order of the layer stack, and modify the way layers are blended without ever editing the node graph in the base Material.

While the Layered Material Functions workflow documented above is still a valid approach, the **Material Layers** system typically provides a faster and more iterative user experience for artists and designers who may not have the technical background needed to edit the node graph. Learn how to use Material Layers below.
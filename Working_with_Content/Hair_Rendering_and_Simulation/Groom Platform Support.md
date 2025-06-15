# Groom Platform Support

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/groom-platform-support-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/groom-platform-support-in-unreal-engine)  
**Processed:** 2025-06-14 16:26:54

---

This page contains information on various platforms that support different features of grooms.

## Groom Geometry Types

Groom **Cards** and Groom **Meshes** geometry are supported on all platforms. However, Groom **Strands** rendering can only run on certain platforms due to its demanding rendering cost.

Strands rendering is only supported on the following platforms:

-   Microsoft Windows that uses either DirectX 11, DirectX 12, or Vulkan.
-   Apple macOS
-   Linux
-   Current generation console, such as PlayStation 5 and Xbox Series S/X.

For more general information about what hardware and software Unreal Engine supports, see Unreal Engine's [Hardware and Software Specifications](/documentation/404).

## Groom Binding

A Groom can be attached to skeletal mesh geometry with Groom Bindings. There are two types of binding attachments: rigid and skinned.

These bindings attachments support the following platforms:

-   **Rigid attachment** is supported on all platforms.
-   **Skinned attachment** is supported on all platforms except Nintendo Switch and mobile because the performance cost is too much and there is missing implementation to support it.

Similar to Skinned attachment, **Global Interpolation** (also called RBF) is supported on all platforms except Nintendo Switch and mobile.

To learn more about groom bindings and how they are used, see [Setting up Bindings for Grooms](/documentation/en-us/unreal-engine/setting-up-bindings-for-grooms-in-unreal-engine).

## Simulation

Groom simulation is supported on all platforms.

To learn more about using simulation with grooms, see [Enabling Physics Simulation on Grooms](/documentation/en-us/unreal-engine/enabling-physics-simulation-on-grooms-in-unreal-engine).

## Groom Cache

Using a Groom Cache allows for pre-computed simulation / animation. This is achieved at the Guide level or Strands level.

-   The **Strands Cache** is available only on platforms that support Strand rendering (see ["Groom Geometry Types"](/documentation/en-us/unreal-engine/groom-platform-support-in-unreal-engine#groomgeometrytypes) above).
-   The **Guides Cache** is supporte don all platforms.

To learn more about the grooms cache and its function, see [Groom Caches](/documentation/en-us/unreal-engine/using-groom-caches-with-hair-in-unreal-engine).

## Known Platform Limitations

-   Frame rate depends on several factors, such as the size of the groom, the resolution of the groom, and the hardware in which the groom is being run on.
    -   For example, you should expect a 30Hz or higher framerate with a NVIDIA RTX-2090Ti GPU for a human-like groom rendered at 1080p. Higher quality settings will result in a significant performance drop.
-   Depth of Field is supported but may produce some artifacts.
-   Grooms rendered with the [Path Tracer](/documentation/en-us/unreal-engine/path-tracer-in-unreal-engine) have a different appearance than the rasterizer's output.
-   Grooms do not yet support proper precomputed lighting (Static or Stationary).
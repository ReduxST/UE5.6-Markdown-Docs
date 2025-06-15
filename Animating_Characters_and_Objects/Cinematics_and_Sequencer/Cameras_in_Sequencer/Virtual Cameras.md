# Virtual Cameras

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-cameras-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-cameras-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:11

---

A **Virtual Camera** drives a **Cine Camera** in **Unreal Engine** by using a modular component system to manipulate camera data and output the final results to a variety of external output devices. In addition, the Virtual Camera system provides its functionality while in the **editor** and during **Play In Editor (PIE)** or **Standalone Game** mode.

The **Virtual Camera Component (VCamComponent)** is the base component that enables building custom virtual cameras in Unreal Engine. With the VCamComponent, a user can drive a Cine Camera inside Unreal Engine by adding custom **Modifiers** and **Output Providers**. The Modifiers manipulate the camera data with custom effects such as filtering, tracking, and auto focus. The Output Providers route the output of the virtual camera to **Composure**, **Media Framework**, editor viewports, or any devices running the **Unreal Remote** app.

In addition, this new architecture includes the following:

-   **[Multi-User editing](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine)** support for all features.
-   The ability to overlay custom UMG controls over the output and interact with them in the editor or on a device.
-   Built-in support for input hardware such as controllers and touchscreens.
-   Provides the functionality to switch to any custom tracking system with **Live Link**.
-   An updated Unreal Remote app with a new UI and improved streaming performance.

For further documentation regarding the virtual camera system, please see the page links below which include a Quick Start on how to use the Virtual Camera Component to build a custom camera, and an overview of a built-in virtual camera that comes with the engine.
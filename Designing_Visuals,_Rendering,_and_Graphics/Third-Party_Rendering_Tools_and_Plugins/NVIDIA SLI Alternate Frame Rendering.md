# NVIDIA SLI Alternate Frame Rendering

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/nvidia-sli-alternative-frame-rendering-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/nvidia-sli-alternative-frame-rendering-in-unreal-engine)  
**Processed:** 2025-06-14 16:39:14

---

Unreal Engine supports NVIDIA's **Alternate Frame Rendering** (AFR) for packaged games running on NVIDIA SLI configurations. Alternate Frame Rendering works by alternating frames between the linked GPUs. One frame is rendered by GPU 1 with the next frame rendered by GPU 2, before repeating the procress. Using this method, image quality and performance are improved by using multiple GPUs on a single monitor.

Projects that intend to ship with support for Alternate Frame Rendering will need to work directly with NVIDIA to test their games and have it automatically switch over to use this functionality where possible.

For additional details, see NVIDIA documentation on their [SLI modes, specifically Alternate Frame Rendering](https://docs.nvidia.com/gameworks/content/technologies/desktop/sli.htm) here.

## Forcefully Enabling Alternate Frame Rendering

NVIDIA Control Panel allows for some applications to be manually added which support AFR forcibly enabling the SLI rendering mode. Add applications to the NVIDIA Control Panel using the following steps.

1.  Open the **NVIDIA Control Panel** from your task tray, and navigate to **Manage 3D Settings**.
2.  Click on the **Program Settings** tab. Under **Select a program to cumstomize** use the dropdown to select the program you want to add.
3.  Next to **SLI Rendering Mode**, select **Force Alternate Frame Rendering**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9fa2579-26e5-43b3-9abb-9711f387272b/afrsetting.jpg)

This feature is not guaranteed to improve the quality or performance of your applications. It is not intended for use with the Unreal Engine Editor, specifically. Should to want this for your developed and released project, you will need to talk with NVIDIA directly to set up this functionality with their drivers.
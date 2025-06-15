# Hardware Ray Tracing and Path Tracing Features

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ray-tracing-and-path-tracing-features-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ray-tracing-and-path-tracing-features-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:44

---

Ray Tracing techniques have long been used in film, television, and visualization for rendering photo-realistic images, but often it required powerful computers and time to render individual images (or frames). For architectural visualization, this can often mean hours of rendering. For film and television, it can take many hours or even days to render high-quality image sequences.

Unreal Engine uses its own ray tracing code base that is shared with both its real-time and offline rendering paths. Real-Time Ray Tracing is an optimized path to work in real-time to render scenes, such as interactive experiences or in games. The offline path uses the built-in Path Tracer to generate uncompromised renderings of scenes. It works seamlessly with the [Movie Render Queue](/documentation/404) to output the highest quality frame renders.

Explore the topics below to learn more about these paths and how you can use them in your own projects.

## Ray Tracing in Unreal Engine

Ray Tracing in Unreal Engine supports two modes:

-   A hybrid **Ray Tracer** that couples ray tracing capabilities with traditional raster techniques for real-time rendering.
-   A **Path Tracer** for generating high quality, compromise-free rendered results.

## System Requirements

The following system requirements must be met to use Ray Tracing and Path Tracing features of Unreal Engine:

| System Requirements |   |
| --- | --- |
| **Operating System** | 
-   [Windows 10 RS5 (Build 1809) or later](https://support.microsoft.com/en-us/help/4028685/windows-10-get-the-update)
    
    Verify your Windows build by typing **winver** in the Windows search bar.
    
-   Vulkan Desktop on Linux and Windows
    
    -   For details on what operating system builds are needed, see [Hardware and Software Specifications](/documentation/404).



 |
| **GPU** | 

NVIDIA RTX and some GTX series cards with DXR support using the latest device drivers.

For more information, see NVIDIA's site [here](https://www.nvidia.com/en-us/geforce/news/geforce-gtx-dxr-ray-tracing-available-now).



 |
| **Unreal Engine Version** | 5.0 and Later |
| **Unreal Engine Rendering Path** | Deferred Path |

## Overviews

## Guides

## Reference
# Mesh Auto-Instancing on Mobile

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-mesh-auto-instancing-on-mobile-devices-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-mesh-auto-instancing-on-mobile-devices-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:59

---

The Unreal Engine [**Mesh Drawing Pipeline**](/documentation/en-us/unreal-engine/mesh-drawing-pipeline-in-unreal-engine) implements a mesh auto-instancing feature that merges draw calls, which can greatly improve graphics performance. This functionality is now available for mobile devices with some additional settings configuration.

## Steps

1.  Locate the **Config** folder for your project and open **DefaultEngine.ini.**
    
2.  Add the following lines:
    
    ```
             `r.Mobile.SupportGPUScene=1          r.Mobile.UseGPUSceneTexture=1`
    		
    Copy full snippet
    ```
    r.Mobile.SupportGPUScene=1 r.Mobile.UseGPUSceneTexture=1
    
    Save your changes and close the file.
    

Enabling this feature will cause shaders to be rebuilt for mobile platforms. If you have Unreal Editor set to Android Preview mode, the editor will recompile shaders accordingly. Large projects may have a long iteration time.

## Result

By enabling the above settings for your project, auto-instancing will be enabled for all devices. `r.Mobile.SupportGPUScene` enables auto-instancing on mobile devices. However, they will use the same buffer as a desktop build. Mali devices only support buffers of up to 64 kb and are unable to support this feature normally. `r.Mobile.UseGPUSceneTexture` will make the auto-instancing process use a texture instead of a buffer to store the required information, enabling Mali devices to use auto-instancing as well.

## Limitations

In addition to the limitations mentioned for draw call merging on the [Mesh-Drawing Pipeline](/documentation/en-us/unreal-engine/mesh-drawing-pipeline-in-unreal-engine) page, there are some limitations to auto-instancing that are specific to mobile devices:

-   Auto-instancing on mobile mainly benefits projects that are heavily CPU-bound rather than GPU-bound. While it is unlikely that enabling auto-instancing will harm a GPU-bound project, you are less likely to see significant performance improvements from using it.
    
-   If a game is heavily memory-bound, it may be more beneficial to turn off `r.Mobile.UseGPUSceneTexture` and use the buffer instead, with the understanding that it will not work on Mali devices.
    

The effectiveness of auto-instancing is highly dependent on the exact specifications of your project. Therefore, we recommend that you create a build with auto-instancing enabled and profile it in order to determine whether you will see substantial performance gains. For more information about profiling, refer to the [Performance and Profiling](/documentation/en-us/unreal-engine/testing-and-optimizing-your-content) section.
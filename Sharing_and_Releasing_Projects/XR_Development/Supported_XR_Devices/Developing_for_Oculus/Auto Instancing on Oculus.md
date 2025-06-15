# Auto Instancing on Oculus

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/auto-instancing-on-oculus-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/auto-instancing-on-oculus-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:16

---

A **draw call** is the RHI command to draw an object. **Auto-Instancing** is a feature that automatically combines multiple draw calls into one instanced draw call. An **instanced draw** **call** is a way for the graphics API to draw multiple instances of similar objects that have varying attributes. These can be any attributes that relate to the rendering of a mesh: position, orientation, color, and so on.

Combining multiple draw calls into one reduces the CPU overhead on submitted graphics API draw calls. It is possible to combine all of its draw calls into one, but doing so requires the vertex buffer, uniform buffer, shaders, rasterization modes and many other graphics API states to be compatible for all draw calls.

Compatibility requirements differ from engine to engine, depending on what constraints an engine imposes on its draw calls.

When auto-instancing fails to combine draw calls, it is usually because hidden compatibility requirements are violated. An understanding of how auto-instancing works in Unreal can help you debug and discover any future new requirements.

Make sure the following CVars are enabled:

-   **r.Mobile.SupportGPUScene=1** Must be manually set to 1 in an .ini file because not all Android devices support compute shaders.
    
-   **r.MeshDrawCommands.DynamicInstancing** Defaults to 1 so there is no need to manually set it.
    
-   **r.MeshDrawCommands.UseCachedCommands** Defaults to 1 so no need to manually set.
    

## Common Instancing Incompatibilities

For StaticMeshComponents that use lit materials, [make sure lightmaps are built](/documentation/en-us/unreal-engine/understanding-lightmapping-in-unreal-engine).

![Go to Build menu, then Build Lighting Only to update lighting.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4873175a-b3c0-45e2-822c-24019375c012/updatelighting.png)

When lightmaps are not built (or when they are outdated), UE4 replaces them with an [indirect lighting cache](/documentation/en-us/unreal-engine/indirect-lighting-cache-in-unreal-engine). An indirect lighting cache passes lighting data to a draw call through the use of a **uniform buffer** (referred to as a **constant buffer** in DirectX), which prevents draw calls from combining because the uniform buffer will be unique for every draw call.

Lightmaps do not have this issue because their data paths are deliberately designed to support instancing.

To test auto-instancing in the editor:

1.  Make sure **View Mode** is either **Lit**, **Detailed Lighting**, or **Reflections**. This is necessary because many debug view modes are not compatible with the lightmap data paths.
    
2.  Make sure the following modes are **enabled**:
    
    -   **Show > Advanced > LOD Parenting**
        
    -   **Show > Lighting Features > Volumetric Lightmap**
        
    -   **Show > Lighting Features > Indirect Lighting Cache**
        
3.  Make sure the following modes are **disabled**:
    
    -   **View Mode > Lightmap Density**
        
    -   **View Mode > Level of Detail Coloration > Mesh LOD Coloration**
        
    -   **View Mode > Level of Detail Coloration > Hierarchical LOD Coloration**
        
    -   **Show > Advanced > BSP Split**
        
    -   **Show > Advanced > Property Coloration**
        
    -   **Show > Advanced > Mesh Edges**
        
    -   **Show > Advanced > Light Influences**
        
    -   **Show > Advanced > Mass Properties**
        

When testing in-editor, if `IsRichVew` returns true, all `FStaticMeshSceneProxy` will lose `bStaticRelevance` and gain `bDynamicRelevance`. This indirectly leads to excluding a static mesh from auto-instancing.

Debug view modes above can cause `IsRichVew` to return true.

## Verification

Use CVar **r.MeshDrawCommands.LogDynamicInstancingStats 1** to view stats on auto-instancing. This console command will print out the draw call reduction factor which is the ratio of number of draw calls before and after the instancing merge.

If you are curious about what happens within the software, use [RenderDoc](/documentation/en-us/unreal-engine/using-renderdoc-with-unreal-engine) to make a capture. You should see multiple objects that are combined into one single instanced draw call:

Click to enlarge. RenderDoc reports the number of instances in its annotation. This annotation is emitted by Unreal Engine.

## How It Works

Because of the complexity of the system, it is not possible to list out all causes of instancing incompatibilities, but it is possible to show basic internal functions for a high-level understanding when you need to debug instancing incompatibilities.

Before looking at how auto-instancing works in native code, turn off the following CVars:

-   **r.ParallelInitViews=0**
    
-   **r.MeshDrawCommands.ParallelPassSetup=0**
    

### Cached Draw Calls

Each draw call has an associated `FCachedMeshDrawCommandInfo::StateBucketId` that is a 32-bit integer for sorting cached draw calls.

Unreal caches a `StaticMeshComponent` that does not change for performance. This behavior is controlled by `r.MeshDrawCommands.UseCachedCommands`, which defaults to **1**.

This means that the value of `FCachedMeshDrawCommandInfo::StateBucketId` is calculated when the draw call is cached. This happens in `FCachedPassMeshDrawListContext::FinalizeCommand`. The calculation of `FCachedMeshDrawCommandInfo::StateBucketId` depends on the evaluation of the hash value calculated by `FMeshDrawCommand::GetDynamicInstancingHash`. From within that function, you can see that the hash value depends on the following attributes:

-   `IndexBuffer`
    
-   `VertexBuffers`
    
-   `VertexStreams`
    
-   `PipelineId`
    
-   `DynamicInstancingHash`
    
-   `FirstIndex`
    
-   `NumPrimitives`
    
-   `NumInstances`
    
-   `IndirectArgsBufferOrBaseVertexIndex`
    
-   `NumVertices`
    
-   `StencilRefAndPrimitiveIdStreamIndex`
    

The `IndexBuffer`, `VertexBuffers`, `VertexStreams`, and `NumVertices` are determined by the Static Mesh; therefore, all of your objects need to reference the same Static Mesh. `PipelineId` is determined by the material and renderer. `DynamicInstancingHash` is also determined by the material. The rest of the attributes are irrelevant for the average use case in UE4.

### Uncached Draw Calls

The `FVisibleMeshDrawCommand` class in `MeshPassProcessor.h` represents uncached draw calls that are generated dynamically, such as SkeletalMeshComponent or other editor widgets. Unfortunately this is not functional yet, and uncached draw calls don't support auto-instancing as of UE4.25.

### Materials

The instancing compatibility of draw calls can depend on the materials because of `PipelineId` and `DynamicInstancingHash`. `PipelineId` is influenced by the choice of Blend Mode and Shading Model from the Material. Using different Blend Modes and Shading Models will result in different Pipeline State Objects. `DynamicInstancingHash` is calculated by the `FMeshDrawShaderBindings::GetDynamicInstancingHash` function. The following attributes determine the output hash value.

| Attribute | Description |
| --- | --- |
| `LooseParametersHash` | An accumulation of hash values calculated from the material's textures. |
| `UniformBufferHash` | Refers to the use of material parameters or [Material Parameter Collections](/documentation/en-us/unreal-engine/material-functions-in-unreal-engine). |
| Size, frequencies | Both are determined by the resulting shaders generated from the material. |

Two materials are compatible if both materials reference the same set of textures and uniform buffers. This uniform-buffer requirement is the reason why indirect lighting cache prevents instancing; the need to upload lighting data with a unique uniform buffer changes the `UniformBufferHash`.

The use of material parameters and parameter collection does not prevent instancing in Unreal Engine from version 4.25 forward. The Unreal material expression cache allows the combination of identical parameters into the same Uniform Buffer.

## CPU Cost

Auto-Instancing happens after frustum culling, this means if something is not visible on screen, then it will not participate in the merging of draw calls, which saves computing costs.

However, the work of sorting and combining draw calls still costs CPU cycles; this means the only time you should turn off auto-instancing is when you know your scene is composed of incompatible components that are not instanceable.

Checking the CPU cost of merging draw calls shows that the operations are very cheap (for mobile VR). They are also distributed across multiple cores.

`STAT_DynamicInstancingOfVisibleMeshDrawCommands` is a CPU trace event that represents the CPU cost of collecting compatible draw calls.

## GPU Cost

The GPU cost relates to how compute shaders put a primitive uniform buffer into an indexable data structure. This compute shader is only executed when per-instance data is changed and so needs to update.

To force UE4 to update the per-instance data every frame, use this command in command prompt or power shell with the device connected:

```
	`adb shell "am broadcast -a android.intent.action.RUN -e cmd 'r.GPUScene.UploadEveryFrame 1'"`

Copy full snippet
```
adb shell "am broadcast -a android.intent.action.RUN -e cmd 'r.GPUScene.UploadEveryFrame 1'"

With UploadEveryFrame turned on, the RenderDoc for Oculus RenderStage trace feature will measure the cost of the compute shader.

![RenderDoc for Oculus capture shows the cost.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b80c2482-a139-4e3d-9465-c47f7d025300/oculuscapture.png)

The RenderDoc for Oculus capture above shows the cost of the compute shader, arranging the instance data for 15 instances of a sphere using a basic material that is 27 microseconds. This is cheaper than the cost of rendering a single tile.
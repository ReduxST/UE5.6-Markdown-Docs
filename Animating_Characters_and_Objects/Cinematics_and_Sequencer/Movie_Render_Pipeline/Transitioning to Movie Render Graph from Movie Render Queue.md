# Transitioning to Movie Render Graph from Movie Render Queue

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/transitioning-to-the-movie-render-graph-from-movie-render-queue-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/transitioning-to-the-movie-render-graph-from-movie-render-queue-in-unreal-engine)  
**Processed:** 2025-06-14 16:54:59

---

## Introduction

Unreal Engine's Movie Render Graph is node-based tool for creating high-quality render output. It is designed to be powerful, flexible, and more accessible than Movie Render Queue. This guide provides an overview of how to transition to using MRG when you are already familiar with MRQ.

## Example Content

A simple example Movie Render Graph is available in the [Meerkat Sample project](/documentation/en-us/unreal-engine/meerkat-sample-project-for-unreal-engine).

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea1c03d1-fd23-4e1c-8250-508673714d55/image_0.png) ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d4172ed-b20c-4bd2-b181-d1ba790c1189/image_1.png)

## MRQ Config to Graph transition

The default Movie Render Graph is nearly identical to the default MRQ config. The main difference is that settings being placed in the graph are nodes that are more conducive to rendering in layers.

### Exports

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48e58e3c-cfa4-4f47-a42e-d36b288d5001/image_2.png)

#### File Name Format

File Name Format has been moved to the File Type Output node. This will allow the user to control file naming settings per render layer.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b10924c6-7579-4e66-bba5-d55c29e46dbf/image_3.png)

#### Command Line Encoding

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41aeb9ab-596b-4b0c-bc23-e140da3b8070/image_4.png)

### Settings

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b66a619d-16e5-4cb0-8c06-642b4ead4c7b/image_5.png)

#### Anti Aliasing

Temporal and Spatial sampling settings have been split apart in the graph due to Temporal Samples needing to be set on the Global level while Spatial Samples can be set per render layer.

Temporal Samples are set in the Sampling Method node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1aa9c8b7-930b-4b40-b2f0-e69ca2a63248/image_6.png)

And Spatial Samples are now set on the Renderer node. Anti Aliasing Method can be set per render layer and is now located on the Renderer node as well.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dcfc44a4-7136-44a3-b8ac-6a3184ca4394/image_7.png)

#### Warm Up Settings

Warm Up settings have been simplified and given their own node:

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0540ad8a-af0a-435a-b141-eb43007e6efb/image_8.png)

#### Burn In

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41424f89-3c51-4976-a924-e9a424ea1efc/image_9.png)

#### Camera Settings

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21945b02-b16f-4297-826f-d9e1c35cbb61/image_10.png)

#### Color Output

**OCIO** has been placed onto the **File Type Output** node as well for render layer level control rather than job level.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bdbbcdaa-27d9-419d-9d0b-f58d321cd5f7/image_11.png)

Tone Curve is now controlled on the Renderer node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10902bcc-6662-49b2-a337-df1c8ad80ca0/image_12.png)

#### Console Variables

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a09145a-87b1-4708-bd06-6353d076d65e/image_13.png)

#### Debug Options

Write All Samples has been moved to the Renderer node

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8db18ba-4ac4-424c-b42a-2ac113659b97/image_14.png)

The ability to an Insights Trace or Capture frames for Render Dock is in the Debug Settings node

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e481407-9469-4bc4-91de-3592cf3f356b/image_15.png)

#### Game Overrides

The Game Overrides node exists in the graph by default and will no longer have any control over the render if deleted or disconnected, as opposed to the behavior on the config file.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3719d51d-b798-40b4-b4d9-788899ff7b48/image_16.png)

### Rendering

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d45bf72-3e72-488b-a769-66894ae4b8f2/image_17.png)

#### Render Path

The user can choose between the Path Tracer and Deferred rendering path by connecting their respective nodes to the render chain. This can be chosen per render layer.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab3bfef9-3e04-4402-890c-1b2b51541a13/image_18.png)

#### View Mode Index

View Mode rendering is now on the Renderer node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ad34944-5a1d-471e-be21-726ce5043534/image_19.png)

#### Additional Post-Processing Materials

Additional Post Process materials are located on the Renderer node and can be set per render layer.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f2e6a2f-fe65-4d7d-bfed-7dd4717b667d/image_20.png)

#### UI Renderer

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f11f8b1-7fb7-4d01-a07f-a92d1d3c5ef3/image_21.png)

### Currently Unsupported in Movie Render Graph

The following are features supported with MRQ, that do not yet have support when using MRG:

-   **nDisplay Rendering**
    
-   **High Resolution Rendering**
    
-   **Apple Pro Res plugin**
    
-   **Final Cut Pro XML**
    
-   **Prestreaming Recorder**
    
-   **32 Bit Post Process Material Rendering**
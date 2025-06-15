# Interchange MaterialX Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/interchange-materialx-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/interchange-materialx-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:31:30

---

The **MaterialX** format is an open-source interchange method developed by Industrial Light & Magic in 2012. It is a software agnostic method for describing patterns, textures, shader networks, and their geometric assignments. **Unreal Engine (UE)** supports MaterialX in the [Interchange Framework](/documentation/en-us/unreal-engine/interchange-framework-in-unreal-engine) using the following standards:

-   Standard Surface Shading model developed by Autodesk.
-   [Universal Scene Description (USD)](/documentation/en-us/unreal-engine/universal-scene-description-usd-in-unreal-engine) workflows using the USD Preview Surface shading model developed by Pixar.
-   OpenPBR shading model specified by Adobe and Autodesk.

By default, OpenPBR materials use Standard Surface shaders. Using [Substrate Materials](/documentation/en-us/unreal-engine/substrate-materials-in-unreal-engine) can give better material fidelity due to support for both opaque and translucent materials. This feature is currently Experimental.

## Import a MaterialX File

To import MaterialX files into Unreal Engine, use the standard [Interchange](/documentation/en-us/unreal-engine/importing-assets-using-interchange-in-unreal-engine) import process.

Importing a MaterialX File into the level.

The interchange import process imports the image data and automatically creates the appropriate number of materials.

## Edit MaterialX Import Settings

You can customize MaterialX import settings:

-   Anytime in Unreal Engine's **Project Settings** editor.
-   At the time of import in the Interchange Pipeline Configuration window.

For more information on customizing settings using the Interchange Pipeline Configuration window, see the [Interchange Import Reference](/documentation/en-us/unreal-engine/interchange-import-reference-in-unreal-engine).

MaterialX import settings are found in **Project Settings > Interchange MaterialX**:

MaterialX Project Settings

| **Option** | **Description** |
| --- | --- |
| **Standard Surface** | Defines the material function to use when translating data for Autodesk's Standard Surface shader. |
| **Standard Surface Transmission** | Defines the material function to use when translating Standard Surface data for translucency. |
| **Surface Unlit** | Defines the material function to use when translating Standard Surface data for unlit surfaces. |
| **USD Preview Surface** | Defines the material function to use when translating data for USD's surface shader. |
| **OpenPBR Surface** | Defines the material function to use when translating data for OpenPBR Surface shader. |
| **OpenPBR Surface Transmission** | Defines the material function to use when translating OpenPBR Surface data for translucency. |

The import process translates MaterialX definitions into Unreal Shader nodes using the following Material Functions:

-   `MX_StandardSurface`
-   `MX_TransmissionSurface`
-   `MX_SurfaceUnlit`
-   `MX_USDPreviewSurface`
-   `MX_Surface`
-   `MX_OpenPBR_Opaque`
-   `MX_OpenPBR_Translucent`
-   `MX_Substrate-StandardSurface-Opaque`
-   `MX_Substrate-StandardSurface-Translucent`
-   `MX_Substrate_OpenPBR_Opaque`
-   `MX_Substrate_OpenPBR_Translucent`

When the imported data uses an unsupported shader model, Unreal attempts to generate a shader graph using the MX\_Surface and other supported Material Functions.

These Materials are found in the following Unreal Engine directories:

-   `Engine/Plugins/InterchangeFrameworkContent/Functions`
-   `Engine/Plugins/InterchangeFrameworkContent/Substrate`
-   `Engine/Content/Functions/Substrate`

Editing the default engine material functions is not recommended. If you need to customize these functions, follow these steps:

1.  Create a copy of the material function you want to edit and move this new function into your project's **Content** folder.
2.  Make changes to the material function and save.
3.  Select the new material function in **Project Settings > Interchange MaterialX**.
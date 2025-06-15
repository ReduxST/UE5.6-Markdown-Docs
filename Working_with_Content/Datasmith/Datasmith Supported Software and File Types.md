# Datasmith Supported Software and File Types

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-supported-software-and-file-types](https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-supported-software-and-file-types)  
**Processed:** 2025-06-14 16:19:06

---

Datasmith currently works with the software applications and file formats listed in the following table.

For each type of software or file format listed, the **Status** column uses the following icons to indicate the level of readiness you should expect:

| Icon | Meaning |
| --- | --- |
| ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f40dfe99-b3b8-4727-aa85-4d7f8c2809ab/checkpoint_checked.png "Production-ready") | Production-ready. |
| ![Beta or Experimental](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1e72c96-9323-42ab-8dc3-425532efa479/checkpoint.png "Beta or Experimental") | Beta or Experimental feature, shared with customers for testing and feedback. Expect changes, and we may deprecate functionality at our discretion. |

The **Workflow Type** indicates how you package the information from your design application:

-   **Direct** means that the Datasmith Importer Plugin in Unreal reads the application's file format directly.
    
-   **Export** means that you need to export the content from your application to a specific file format before Datasmith can import it into Unreal Engine. You export the content using functionality that is already built into your application.
    
-   **Export Plugin** means that you need to install a new plugin into your application in order to export your design data into the format that Datasmith imports into Unreal.
    

The **Importer Plugin** column below tells you which Datasmith importer plugin you need to enable in your Unreal Engine Project to be able to import files of each type. For more information about this process, see [Importing Datasmith Content into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine)

You can download all Datasmith exporter plugins from the [Datasmith exporter plugins](https://www.unrealengine.com/en-US/datasmith/plugins) page.

## Supported Applications

| Application | Support Level | Version | Workflow Type | Importer Plugin |
| --- | --- | --- | --- | --- |
| **3D ACIS** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/698fd481-0c8f-408f-90f5-d68544b63c45/checkpoint_checked.png "Production-ready") | Up to 2023 | Direct | **CAD** |
| **3DEXCITE DELTAGEN** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fd3c38f-3f9a-4a98-bf26-9ce4f3c8fa58/checkpoint_checked.png "Production-ready") | 2017–2024 | Export (FBX only) | **FBX** |
| **ArcGIS CityEngine** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdf3c611-7f22-4d85-b999-3a1f6d5c05a6/checkpoint_checked.png "Production-ready") | \-- | Export Plugin | **Datasmith** |
| **Autodesk 3ds Max** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a56cbd72-5aa8-4a47-9f1b-03c328466a89/checkpoint_checked.png "Production-ready") | 2016–2025 | Export Plugin | **Datasmith** |
| **Autodesk Alias** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4e4adbf-f00e-4f9c-9867-3e27f9f432a8/checkpoint_checked.png "Production-ready") | Up to 2023 | Direct | **CAD** |
| **Autodesk AutoCAD** | ![Beta or Experimental](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d564ad90-0c4a-44b0-9182-725aad484298/checkpoint.png "Beta or Experimental") | \-- | Direct | **CAD** |
| **Autodesk Inventor** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a894cd3-436b-4255-ad92-94325f8afe8d/checkpoint_checked.png "Production-ready") | Up to 2024 | Direct | **CAD** |
| **Autodesk Revit** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f20fbb45-0354-4fb3-891b-a3cc97b0c73e/checkpoint_checked.png "Production-ready") | 2016.3–2023\* | Export Plugin | **Datasmith** |
| **Autodesk Navisworks** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/725c4c08-3f12-417c-bce1-d733705621e6/checkpoint_checked.png "Production-ready") | 2019–2023 | Export Plugin | **Datasmith** |
| **Autodesk VRED** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee1ef030-9a91-4e46-8a94-4e7fbb0308f7/checkpoint_checked.png "Production-ready") | VRED Professional 2018–2023 | Export Plugin | **FBX** |
| **Dassault Systèmes CATIA V5** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5519e77b-8d5f-475b-b8ef-878642d4a726/checkpoint_checked.png "Production-ready") | Up to V5\_6 R2023 | Direct | **CAD** |
| **Dassault Systèmes SOLIDWORKS** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bcc0d762-02a1-439e-abbb-ec8f8588516d/checkpoint_checked.png "Production-ready") | Up to 2024 | Export Plugin | **CAD** |
| **Dassault Systèmes SOLIDWORKS** | ![Beta or Experimental](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b451538b-076a-4853-8602-68c3d35d593f/checkpoint.png "Beta or Experimental") | 2020–2023 | Direct | **Datasmith** |
| **Graphisoft Archicad** | ![Beta or Experimental](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cce13ad-60d9-492f-aab7-e067d437bb59/checkpoint.png "Beta or Experimental") | 23–26 | Export Plugin | **Datasmith** |
| **Maxon Cinema 4D** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97f3a211-a5fb-477c-b15f-044b5cb34485/checkpoint_checked.png "Production-ready") | \-- | Direct | **C4D** |
| **McNeel Rhinoceros** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8dddbce1-2419-4529-98ce-af3208294d6a/checkpoint_checked.png "Production-ready") | up to 8 | Export Plugin | **Datasmith** |
| **McNeel Rhinoceros** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06c51d5a-337a-46d6-9958-dd5bb32b66d7/checkpoint_checked.png "Production-ready") | up to 8 | Direct (`.3dm` files) | **Datasmith** |
| **PTC Creo (Pro/ENGINEER)** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/436baeae-f789-42ce-8bde-7da5351d9498/checkpoint_checked.png "Production-ready") | Pro/Engineer 19.0 to Creo 10.0 | Direct | **CAD** |
| **Siemens NX** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e81ac58-41d0-4d9f-aed2-1692e9ef99ee/checkpoint_checked.png "Production-ready") | V11–V18, NX–NX12, NX1847–NX2212 | Direct | **CAD** |
| **Trimble SketchUp Pro** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2030595-8ccb-4a0b-aa53-e33605901a5d/checkpoint_checked.png "Production-ready") | 2019–2024 | Export Plugin, DirectLink | **Datasmith** |

\* As of Unreal Engine 5.3, Autodesk now manages newer versions of the Revit exporter plugin and is shipped directly in Revit 2024+. UE still supports this plugin and you can get older versions of the plugin from the download page.

## Supported File Formats and Standards

| File Format or Standard Name | Support Level | Version | Workflow Type | Importer Plugin |
| --- | --- | --- | --- | --- |
| **3DXML** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/024aedce-51ae-4b81-a97e-a481f11365ed/checkpoint_checked.png "Production-ready") | Up to V5-6 R2019 (R29) | Direct | **CAD** |
| **Industry Foundation Classes (IFC)** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13340b33-7eaa-4ff3-8d75-adec374509ad/checkpoint_checked.png "Production-ready") | IFC2x Editions 2, 3 and 4 | Direct | **CAD** |
| **Initial Graphics Exchange Specification (IGES)** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b177e5ef-02cf-4e45-ba9f-dc40d45e2998/checkpoint_checked.png "Production-ready") | 5.1, 5.2, 5.3 | Direct | **CAD** |
| **JT Open** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e443fb2-baad-488c-839f-853b8161885a/checkpoint_checked.png "Production-ready") | Up to 10.6 | Direct | **CAD** |
| **Parasolid (x\_t)** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2345ef81-1f6e-43e7-8ca4-ca097787bee6/checkpoint_checked.png "Production-ready") | up to 35.1 | Direct | **CAD** |
| **Siemens PLM XML** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1dc25581-bd45-4043-a4f8-ac39f8bec872/checkpoint_checked.png "Production-ready") | 7.0.3 and later (Compatible with TeamCenter 11 or later) | Direct | **CAD** |
| **STEP** | ![Production-ready](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67786719-ff97-4531-9940-29f385ae8dee/checkpoint_checked.png "Production-ready") | AP203, AP214, AP242 | Direct | **CAD** |

### Export Plugins for macOS

Most **Export Plugins**, as well as all Datasmith importers in the Unreal Editor, are currently only available for Microsoft Windows platforms. As of Unreal Engine 4.27, we also support exporting from the following applications on macOS:

| Application | Supported Versions |
| --- | --- |
| Trimble SketchUp Pro | 2019–2024 |
| Graphisoft Archicad | 23–27 |
| McNeel Rhinoceros | 6, 7, 8 |

## Formats that Unreal Engine Supports Directly

Unreal Engine offers built-in support for importing and exporting FBX files.

These FBX-based workflows are optimized to support game requirements, which tend to be focused on working with individual objects. Datasmith, by contrast, brings in entire scenes, potentially containing thousands of objects, each with its materials, pivots, scale, hierarchy, and metadata, from a wide range of sources. However, you should feel free to use the FBX import pipeline if it suits your needs. For example, you might use it to import pieces of additional set dressing that you'll use to augment your Datasmith content in your Unreal Level.

For details, you can read about our [FBX Content Pipeline](/documentation/en-us/unreal-engine/fbx-content-pipeline).

## Backward Compatibility

Sometimes, we may need to change the Datasmith file format and the behavior of the importer plugins in order to add new features. We do not guarantee backward compatibility between all versions of Unreal and all versions of the Datasmith export plugins. Although you may be able to import a `.udatasmith` file generated with an older version of an export plugin into a newer version of Unreal Engine, we do not recommend depending on it.

Always use the version of an export plugin that matches the Unreal Engine and Datasmith plugin versions that you need to use the exported file with. To get the most out of Datasmith, and to make sure you benefit from the latest fixes and features, we recommend always using the latest available version of Unreal Engine and the export plugins.
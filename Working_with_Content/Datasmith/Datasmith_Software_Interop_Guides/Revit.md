# Revit

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-with-revit-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-with-revit-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:51

---

This page describes how Datasmith imports scenes from Autodesk Revit into Unreal Editor. It follows the basic process outlined in the [Datasmith Overview](/documentation/en-us/unreal-engine/datasmith-plugins-overview) and [About the Datasmith Import Process](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine), but adds some special behavior that is specific to Revit. If you're planning to use Datasmith to import scenes from Revit into Unreal Editor, reading this page can help you understand how your scene is translated, and how you can work with the results in Unreal Editor.

![Revit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69db2c76-7c81-401d-9bfe-3db1edd94686/datasmith-revit-compare-revit.png)

![Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a487e1d-e343-4f05-97be-df10f94ded34/datasmith-revit-compare-unreal.png)

## Revit Workflow

Datasmith uses an Export Plugin workflow for Revit. This means that to get your Revit content into the Unreal Engine using Datasmith, you need to:

1.  Install a plugin for Revit. See the **Installation Notes** section below.
    
2.  Export your Revit content to a `*.udatasmith` file. See [Exporting Datasmith Content from Revit](/documentation/en-us/unreal-engine/exporting-datasmith-content-from-revit-to-unreal-engine). Alternatively, you can [use Dynamo](/documentation/en-us/unreal-engine/batch-exporting-revit-views-with-dynamo-to-a-datasmith-scene) to batch export Revit views.
    
3.  Enable the **Importers > Datasmith Importer** Plugin for your Project, if it's not already enabled.
    
4.  Use the **Datasmith** importer in the Toolbar of the Unreal Editor to import your`.udatasmith` file. See [Importing Datasmith Content into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine).
    

## Installation Notes

Before you can export Revit content, you must download and install the **Datasmith Exporter for Revit** plugin from the [Datasmith Export Plugins](https://www.unrealengine.com/en-US/datasmith/plugins) page.

To see what versions of Revit the plugin supports, see [Datasmith Supported Software and File Types](/documentation/en-us/unreal-engine/datasmith-supported-software-and-file-types).

We encourage you to share the download link to the Datasmith Exporter plugins with any number of people, both inside and outside of your organization. Please note that you are not permitted to distribute the Datasmith Exporter plugins themselves.

Before you install the Datasmith Exporter for Revit plugin, make sure that:

-   Revit is not running.
    
-   You downloaded the installer for the exporter plugin that matches Unreal Engine version you intend to use.
    
-   You uninstalled all previous versions of the Datasmith Exporter for Revit plugin.
    

After you downloaded the installer, double-click it to open, then follow the instructions on-screen.

When you launch Revit after you installed the exporter plugin, you might see the following warning: "The publisher of this add-in could not be verified. What do you want to do?" Click **Always Load** to confirm that you want the Datasmith Exporter plugin to be available each time you launch Revit.

If you need to uninstall the Datasmith Exporter for Revit plugin, you can do this from the **Control Panel**, like any other Windows application.

## Controlling What Gets Exported

You always need to have a 3D View selected and active in Revit in order to export your scene using the Datasmith Exporter plugin. The visibility settings of that 3D View define what elements from the Revit file get included in the exported `.udatasmith` file.

You can use any 3D View that you already have in your Revit file. However, to take full control over the objects that you bring in to Unreal Engine, we recommend that you set up a new 3D View in Revit, and set up that view so that it shows only the objects that you need in your realtime visualization.

Revit offers many tools and techniques for controlling the visibility of objects inside a 3D View. For example:

-   You can use the **Graphics > Visibility/Graphics Overrides** to control the visibility of the different objects and object categories in your Level.
    
-   You can use a [Section Box](http://help.autodesk.com/view/RVT/2019/ENU/?guid=GUID-C9EA51CB-3214-4BD8-AD55-3BEB1CCD15B6) to cut the geometry you export. Only the objects inside your Section Box are exported to Unreal Engine. Note that when an object crosses the boundaries of the Section Box, such as the walls, floor and furniture in the images below, its geometry is truncated. Inside Unreal Engine, the Static Mesh Assets that represent the exported objects only contain the geometry that lies inside the Section Box.
    
-   **Temporary Hide and Isolate** settings in Revit are respected.
-   Only geometric objects visible in the current 3D View are exported. Non-geometric objects are ignored.

The Datasmith Exporter respects your choice of which objects are shown and which are hidden, but it does not take into account other settings that control the way the 3D View is drawn in the Revit viewport. For example, it does not take into account the **Graphics > Graphic Display Options** set for the 3D View (Realistic vs. Shaded Model Display, Cast Shadows, and so on) or the **Camera > Rendering Settings** (Draft vs. High Quality settings, Lighting schemes, and so on).

For more information about controlling visibility in a Revit 3D View, see also [Visibility and Graphic Display in Project Views](http://help.autodesk.com/view/RVT/2019/ENU/?guid=GUID-A2FC119B-51D7-4C2E-84ED-CD51983EC532) in the Revit Help.

## Geometry

In general, each element that you can select individually in the Revit scene is translated to Unreal as a separate Static Mesh Asset. Some elements, such as railings, may be broken down further into smaller Static Meshes when they are made up of smaller parts.

In all cases, the geometry of each Static Mesh Asset is set to match the dimensions of the Revit object at the time you export the file. Parametric settings and constraints are not carried over into Unreal Engine. So, for example, if you move a floor up or down in the Unreal Editor, the height of the walls will not stretch or shrink to match the new location as it would in Revit.

### Instancing

If two objects belong to the same family, and if they have exactly the same parameter values, then both objects are represented in the Datasmith Scene as instances of the same Static Mesh Asset.

### Tessellation

Datasmith relies on Revit's built-in tessellation services to create triangular meshes from your scene geometry. In most cases, this produces adequate geometry for use in Unreal Engine. However, if you find these surfaces to be a problem in your Projects, you can try tools offered by the Unreal Editor for reducing the complexity of these meshes, such as the [Proxy Geometry tool](/documentation/en-us/unreal-engine/proxy-geometry-tool-in-unreal-engine).

You can also manually specify the level of tessellation for meshes that Revit creates from the **Datasmith Export Settings** panel. These levels are defined by the [Revit API](https://www.revitapidocs.com/2019/d98987f3-27a6-1893-3b7d-fc28e8ed5322.htm).

![Level of Tessellation setting in the Datasmith Export Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0321d0b-f624-4336-b005-38e9b4c8e4bc/export-settings-tessellation.png)

Level 8 is the default level of tessellation. This produces the same mesh resolution than with the Revit FBX Exporter:

|   |   |
| --- | --- |
| 
 | 

 |
| Level 2 | Level 8 |

### Linked Models

If your Revit scene contains any [Linked Models](http://help.autodesk.com/view/RVT/2019/ENU/?guid=GUID-0FBC74D9-C739-4ED3-962E-20DC4526A678) — that is, references to other Revit files — Datasmith attempts to find the linked files on your computer using the paths saved in the Revit file. Datasmith includes the data from all linked files that it is able to find in the Datasmith Scene it creates in Unreal Engine.

## Materials and Textures

For each different type of surface in your Revit scene, Datasmith creates a new Material Asset in the Unreal Engine project, and places it in the `Materials` folder next to your Datasmith Scene Asset. The goal of these Materials is to respect the way you've set up the surfaces to look in Revit, while also exposing a set of properties that closely mirror the ones you are used to working with in Revit.

|   |   |
| --- | --- |
| 
 | 

 |
| Revit | Unreal |

Datasmith currently supports translating diffuse maps and colors, Transparency, Cutouts, and Bump settings from Revit into the Unreal Engine Materials it generates.

To modify a Material in the Unreal Editor:

1.  Double-click it in the **Content Browser**. Alternatively, select an Actor in your Level that uses the Material you want to modify, and double-click the Material in the Details panel.
2.  This opens the Material Editor shown above, where you can modify these parameters in the **Parameter Groups** section at the top of the Details panel. You can also modify other built-in parameters exposed by the Unreal renderer.
3.  To override the default value for any property, first check the box to the left of its name to activate the property in your Material. Then, set the value you want the property to use.

Each of these Assets is a Material Instance, whose parent is the **RevitMaster** Material built in to the Datasmith plugin. You can open up this parent Material to see how each of the properties exposed in the Material Instance are wired together in the Material graph.

### Textures and UV Wrapping

Datasmith imports the textures that you use in your Revit Materials into Assets, and places them in the `Textures` folder next to your Datasmith Scene Asset.

Each Material that uses a Texture Asset offers similar settings to the Revit Texture Editor to control the way the texture map is applied to the surface of the 3D object using the Material.

![Texture mapping and UV settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/942a9fa2-4a34-4912-bc58-f6e2b3cd3285/revit-uvs.png "Texture mapping and UV settings")

1.  The **Position > Offset** value in Revit is modeled by the **UVOffsetX** and **UVOffsetY** settings for each type of map.
2.  The **Position > Rotation** value in Revit is modeled by the **UVWAngle** setting for each type of map.
3.  The **Scale** values in Revit, which are based on real-world dimensions, are converted in the Unreal Engine Material to a scale multiplier. As you increase the absolute value of these scale values, the texture becomes smaller on the object.

Datasmith does not convert procedural textures, such as Checker, Noise, Tiles, and so on.

## Building the Datasmith Scene Hierarchy

The Datasmith Exporter plugin creates a hierarchy of parent and child Actors in the Datasmith Scene that is intended to reflect the overall organization of your scene in Revit. The intent is to organize the Actors in your Unreal Engine Level according to the concepts you're used to working with in Revit, to make it easier for you to find and work with objects. 

This scene hierarchy is constructed according to the following rules:

-   Each **Level** in Revit — the Ground Floor, Level 1, Level 2, and so on — is reflected by a separate Actor in the Datasmith Scene hierarchy.
    
-   Within each Level, any object that can **host** other scene elements in Revit becomes a parent for the objects it hosts. 
    
-   Under the parent Actors that represent the Revit Levels and Hosts, you'll find a Static Mesh Actor to represent each geometric object.
    
    For example, the Actor named Level 1 contains an Actor that represents each wall. Each of these Actors in turn is represented by another parent Actor that has a child for each geometric object hosted by the wall — that is, each door, window, or wall section.
    
    ![Example scene hierarchy in the Unreal Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2e07bef-d878-4f3e-985e-7df60bc7efa8/scene-hierarchy.png "Example scene hierarchy in the Unreal Editor")
-   For most "compound" Revit objects, such as curtain walls or railings, the scene hierarchy contains only one Actor to represent the compound object. That Actor contains a Static Mesh Component for each of the sub-objects that the compound element is composed of.
    
    For example, a curtain wall in Revit typically comes through to Unreal Engine as a single Actor. That Actor has a separate Static Mesh Component for each mullion and each panel that makes up the curtain wall.
    

## Lights

Datasmith imports the lights from your Revit scene into Unreal Engine, maintaining the physical units you've set for their intensity.

## Cameras

When you import a 3D View from Revit, Datasmith creates a single **CineCameraActor** in the Unreal Editor Level. It places this camera at the position and orientation of the camera in the Revit 3D View, with a similar field of view. If you select this CineCameraActor in the Level Viewport or the **World Outliner**, you'll see a preview of its viewpoint that should match very closely the Crop Region of the Revit 3D View at the time you exported your `.udatasmith` file.

Datasmith does not handle some camera concepts available in Revit, including orthographic projection mode and perspective corrections like tilted, shifted, and cropped regions.

For best results:

1.  Set the **Camera > Projection Mode** setting for your 3D View to **Perspective**.
2.  Set the Crop Region for your 3D View in Revit to focus on the view that you want your camera to have in Unreal Engine.
3.  Make sure your camera's target point in Revit is centered within the crop area. You can verify this by showing the camera in other plan and elevation views. If the perspective is shifted, your result in Unreal Engine will not look the way you're expecting.

For example, the 3D View below has a perspective camera with a centered crop region, which translates well:

|   |   |
| --- | --- |
|  |  |

However, the following 3D View has had its crop region adjusted by hand, shifting one edge of the perspective region unequally toward the target point. This will not translate well.

|   |   |
| --- | --- |
|  |  |

## Categories

Each Revit Category that contains at least one object in the scene carries over into the Unreal Editor as a separate Layer.

!\[Revit layers\](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2934ea25-501a-48cb-bf30-7c803b75ba64/revit\_layers.png "")

You can use these Layers within the Unreal Editor to show and hide categories, or inspect and select the objects assigned to them.

Note that the information provided to the exporter by the Revit SDK does not always link every scene object to a Category. Objects with no assigned Category in Revit are not assigned to any Layer in the Unreal Editor.

## Metadata

When you select an element in a Revit view, the **Properties** palette shows a list of all instance properties that are assigned to that element. You can change these values freely, and add your own custom properties.

For details on setting and using these properties, see [the Revit help](https://help.autodesk.com/view/RVT/2019/ENU/?guid=GUID-A764EA7A-FE26-469B-857C-F3A70812FC34).

When you use Datasmith to import a Revit scene into the Unreal Editor, Datasmith assigns all instance properties for each Revit element as metadata on the Static Mesh Actor that it creates for that element in the Unreal Engine Level. This metadata also includes any type properties for the object's Revit type that are not empty.

Because Datasmith metadata is always a flat list of key-value pairs, the category headings in the Properties palette (such as **Constraints**, **Structural**, **Dimensions** and **Identity Data** in the image above) are not included. Only the names and values of the actual properties are preserved.

Some other, more technical internal information is attached to each Actor using Component Tags. You might find this information useful for identifying the Actors, particularly if you use Blueprint or Python scripts to automate data preparation in the Unreal Editor. For example:

-   **Revit.Instance.Depth. -** The depth of the object's family instance or family symbol in the Revit scene hierarchy.
-   **Revit.Instance.Id. -** The ID of the object's family instance or family symbol in the Revit document.
-   **Revit.Host.Id. -** When the object's family instance is hosted, this value gives the ID of the family instance host in the Revit document.

![Metadata saved in Component Tags](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3ce5a9b-22ab-4a3e-a768-b7bd2a13d242/metadata-component-tags.png "Metadata saved in Component Tags")

You can filter the amount of metadata that gets exported with `.udatasmith` files or via Direct Link from the **Settings** menu on the Datasmith toolbar inside Revit. This can help reduce the amount of data to be exported, which affects both export performance and the size of the exported Datasmith scene.

![Settings for metadata export](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac7acfc5-c0c9-4e24-832e-ce6b97654b4b/export-settings-metadata.png)

Settings for metadata export.

Use the **Add Group** and **Remove Selected** buttons to add or remove metadata that you want to be included with the exported Datasmith scene.

Note the following:

-   The metadata categories are defined by Revit and cannot be changed.
    
-   This filter affects both regular export (as a `.udatasmnith` file) and Direct Link setups.
    
-   The list of categories you add to the export filter will be saved within the Revit file.
    
-   If the list is completely empty, **all** metadata will be exported.
    

## RPC Objects

Datasmith brings Rich Photorealistic Content (RPC) objects from Revit scenes into Unreal Engine. For each type of RPC object in your Revit scene, Datasmith imports the visible geometry that you see in Revit into a new Static Mesh Asset. For each of those RPC object types that you have placed in your Revit scene, Datasmith creates a new Static Mesh Actor in the Unreal Engine Level with the same position and orientation in 3D space.

![RPC Actors in the World Outliner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a004d93d-7542-4c1f-b99d-9b0cb1df732b/rpc-objects-in-outliner.png "RPC Actors in the World Outliner")

You can find these RPC objects in your Unreal Engine Level by looking for Actors that have been assigned the **Revit.RPC** Component Tag:

![Component Tag for an RPC Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fb46769-03fd-4f82-91f5-f5d08d3db0c7/rpc-objects-component-tags.png "Component Tag for an RPC Actor")

This can be useful if you want to automate a way to replace the placeholder entourage objects used in Revit with alternatives more suited to your 3D realtime visualization.

## Survey Points and Base Points

If your Revit scene contains a [Base Point or Survey Point](http://help.autodesk.com/view/RVT/2019/ENU/?guid=GUID-68611F67-ED48-4659-9C3B-59C5024CE5F2), Datasmith imports those points into the Unreal Engine Level, representing them with plain Actors that contain no visible geometry. It records the data about the survey point and base point in Datasmith Metadata on those Actors:

|   |   |
| --- | --- |
| ![Base Point metadata](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e364b6b-03e5-483d-b843-6e7d2c0e9975/revit-basepoint.png "Base Point metadata") | ![Survey Point metadata](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da12e74e-8e37-4b80-a9b2-1ed6af6e63fb/revit-surveypoint.png "Survey Point metadata") |
| Base Point | Survey Point |

When exporting a Datasmith scene, the orientation of the model will be based on the Project Base Point (Project / Plan North). To match the orientation of the exported Revit model with the Survey Point (True North), the Project Base Point needs to be have the same rotation as the Survey Point.

See also [Metadata](/documentation/en-us/unreal-engine/using-datasmith-with-revit-in-unreal-engine#metadata) above and [Using Datasmith Metadata](/documentation/en-us/unreal-engine/using-datasmith-metadata-in-unreal-engine).

All scenes and models used on this page are courtesy of [Turbosquid](https://www.turbosquid.com/).
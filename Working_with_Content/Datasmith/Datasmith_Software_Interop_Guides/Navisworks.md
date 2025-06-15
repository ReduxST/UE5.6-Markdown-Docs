# Navisworks

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-with-navisworks-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-with-navisworks-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:49

---

This page describes how **Datasmith** imports scenes from Autodesk **Navisworks** into **Unreal Engine**. It follows the basic process outlined in the [Datasmith Overview](/documentation/en-us/unreal-engine/datasmith-plugins-overview) and [About the Datasmith Import Process](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine), but adds some special translation behaviors specific to Navisworks. If you are planning to use Datasmith to import scenes from Navisworks into UE, reading this page can help you understand how your scene is translated, and how you can work with the results in Unreal Editor.

## Navisworks Workflow

Similar to the Revit or 3ds Max Datasmith Exporters, our Navisworks Exporter uses an export workflow. This means that to get your content into the editor using Datasmith, you need to:

1.  Install the Datasmith Exporter for Navisworks. See the **Installation Notes** section below.
    
2.  Export your Navisworks content using the **Datasmith Export** button added to the toolbar by the plugin. See [Exporting Datasmith Content from Navisworks](/documentation/en-us/unreal-engine/exporting-datasmith-content-from-navisworks-to-unreal-engine).
    
3.  Use the Datasmith importer available in the Toolbar of the Unreal Editor to import your `.udatasmith` file. See [Importing Datasmith Content into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine).
    

## Installation Notes

Before you can export Navisworks content, you must download and install the **Datasmith Exporter for Navisworks** plugin from the [Datasmith Export Plugins](https://www.unrealengine.com/en-US/datasmith/plugins) page.

To see what versions of Navisworks the plugin supports, see [Datasmith Supported Software and File Types](/documentation/en-us/unreal-engine/datasmith-supported-software-and-file-types).

We encourage you to share the download link to the Datasmith Exporter plugins with any number of people, both inside and outside of your organization. Please note that you are not permitted to distribute the Datasmith Exporter plugins themselves.

Before you install the Datasmith Exporter for Navisworks plugin, make sure that:

-   Navisworks is not running.
    
-   You downloaded the installer for the exporter plugin that matches the Unreal Engine version you intend to use.
    
-   You uninstalled all previous versions of the Datasmith Exporter for Navisworks plugin.
    

After you downloaded the installer, double-click it to open, then follow the instructions on-screen.

If you need to uninstall the Datasmith Exporter for Navisworks plugin, you can do this from the **Control Panel**, like any other Windows application.

## Converting Geometry to Static Meshes

The Datasmith Exporter for Navisworks works to preserve the geometry, materials, and metadata contained in your file by using a process similar to our Revit and 3ds Max exporters:

-   To maintain performance, Datasmith merges objects in the hierarchy at a user defined level to create larger meshes and maintain triangle counts of less than one million.
-   Once meshes have been merged, the exporter creates a new **Static Mesh** asset in your **Content Browser** for each of the remaining meshes. It preserves the **Name** of each mesh as set in the **Properties** panel in Navisworks and places them in a **Geometries** folder.
-   The Navisworks hierarchy is maintained in the World Outliner by using empty Actor objects.
-   Your scene is assembled around a user-defined origin point.

## Merging Objects in the Hierarchy

As a Navisworks scene contains a significant amount of data from multiple sources, it is necessary to consolidate the number of assets during the export process. Datasmith does this with a process that merges objects at a user-defined depth of the hierarchy:

![Navisworks Datasmith Export dialog box](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7ae7e9b-2a4a-4495-9ed8-0121128857a2/datasmithnavismerge.png "Navisworks Datasmith Export dialog box")

In the example below, we can see when the value is set to 2 how the objects are merged 2 levels from the bottom:

![How Datasmith merges the Navisworks hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe31b28e-221b-444e-b022-e1524ccac30c/datasmithnavishierarchy.png "How Datasmith merges the Navisworks hierarchy")

If the node subtree contains more than 1M triangles, Datasmith merges objects up to a level where the resulting meshes do not exceed 1M triangles.

## Setting the Origin

Autodesk Navisworks uses a double precision coordinate system that allows support for models that are very far away from the origin. This is not compatible with Unreal and can lead to imprecision on import. For this purpose, when using the Datasmith Exporter for Navisworks users can designate the origin point of the scene. This specific point becomes the origin point (0,0,0) inside of UE:

![Selecting the origin point in Navisworks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94438543-e777-4840-b911-a8e9115b717f/datasmithnavisorigin.gif "Selecting the origin point in Navisworks")

## Navisworks Metadata

Datasmith imports metadata stored on objects in Navisworks as **Tabs**:

![Navisworks Metadata stored as Tabs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89374007-4713-4fce-b670-dfa71e2f9bd2/datasmithnavismetadata.png "Navisworks Metadata stored as Tabs")

The data is prepended with tab names using the following format:

\_\[TabName\]\_\[PropertyName\] = \[Value\]\_

So in the image above, the resulting data would be:

\_MyTab\_MyStringProperty = "MyStringValue"

MyTab\_MyBooleanProperty = "Yes"

MyTab\_MyFloatProperty = "0.000"

MyTab\_MyIntegerProperty = "0"\_

## Navisworks Materials

For each surface material in your Navisworks scene, Datasmith will create a **Material** asset in Unreal with the same name. These assets are placed in the **Material** folder next to your Datasmith Scene Asset.

-   Each asset that is placed in the Materials folder is a Material Instance that exposes properties set in Navisworks. You can change these exposed parameters to modify the way the Material looks when applied to a surface. Datasmith assigns these Materials to the Static Mesh assets it creates during the import process.
-   Datasmith also creates a set of master Materials that can be found in the **Materials/Masters** folder, one for Translucent Materials and another for Opaque Materials. Each of these master Materials is the parent of at least one of the Material Instances found in the **Materials** folder. You can edit these Materials if you want greater control over the Material graph that defines how each surface appears in Unreal, exposing additional parameters to child Material Instances or chase the way these parameters are processed during rendering.

Changing a Master Material also changes all Material Instances that inherit from that parent automatically. It's usually a good idea to duplicate a Master Material before you modify it, then make your changes to the duplicate, then finally update specific Material Instances to use your new duplicate as their parent. For details, see [Modifying a Datasmith Master Material](/documentation/en-us/unreal-engine/modifying-a-datasmith-master-material-in-unreal-engine).
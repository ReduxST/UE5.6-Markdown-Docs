# IFC Files

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-ifc-files-into-unreal-engine-using-datasmith](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-ifc-files-into-unreal-engine-using-datasmith)  
**Processed:** 2025-06-14 16:30:23

---

This page describes how Datasmith imports scenes from Industry Foundation Classes (IFC) files into Unreal Editor. It follows the basic process outlined by the [Datasmith Overview](/documentation/en-us/unreal-engine/datasmith-plugins-overview) and [Datasmith Import Process](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine) pages, but adds some special translation behavior that is specific to IFC. If you're planning to use Datasmith to import scenes from IFC into Unreal Editor, reading this page can help you understand how your scene is translated, and how you can work with the results in Unreal Editor.

![IFC Viewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/847e9294-876d-4fbf-aeb1-b62141e9136b/ifc-comparison-ifc.png)

![Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ccf78cb-ec3a-4548-a864-58a1fef51303/ifc-comparison-ue4.png)

## IFC Workflow

Datasmith uses a direct workflow for IFC. This means that to get the content of an IFC file into Unreal using Datasmith, you need to:

1.  Save the `.ifc` file.
    
2.  Activate the **Importers > Datasmith CAD Importer** plugin for your project.
    
3.  Use the Datasmith **IFC** importer available in the Toolbar of the Unreal Editor to import your `.ifc` file. See [Importing Datasmith Content into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine).
    

To learn more about other types of Datasmith workflows, see [Datasmith Supported Software and File Types](/documentation/en-us/unreal-engine/datasmith-supported-software-and-file-types).

### Supported IFC versions

Datasmith currently supports the **IFC2x Editions 2, 3 and 4** format.

For details about IFC formats and specifications, see the [buildingSMART International technical site](https://technical.buildingsmart.org/standards/ifc).

## Scene Hierarchy

Datasmith creates an Actor for each object in your IFC scene and gives each Actor a name that matches its corresponding object, prefaced by the object's IFC type. The Datasmith scene arranges the Actors into a hierarchy of parent-child relationships that closely matches the way your IFC objects are organized: sites contain buildings, buildings contain storeys, storeys contain walls, doors, spaces, and so on.

Left: an IFC hierarchy shown in IFC Viewer. Center: an IFC hierarchy shown in Open IFC Viewer. Right: the same hierarchy in Unreal Engine. Click for full image.

You may notice a few differences:

-   In the Unreal Editor **Outliner**, shown above on the right, the Actors at each level of the hierarchy are always ordered alphabetically. This may cause visual differences in ordering siblings between Unreal Engine and other IFC viewing and editing applications, but the parent-child relationships remain unchanged.
    
-   An IFC file can have multiple objects with the same name, but each Actor in the Unreal Engine level needs to have a unique name. Datasmith appends a different numeric suffix to distinguish between objects that share the same name.
    
-   Datasmith only allows alphanumeric characters, underscores, and hyphens in Actor names. All other characters are changed to underscores.
    

These minor visual differences do not affect unique IDs or other data assigned to the IFC objects. These values are preserved by Datasmith in [metadata](/documentation/en-us/unreal-engine/importing-ifc-files-into-unreal-engine-using-datasmith#metadata) assigned to each Actor. You can create best-practice IFC workflows in Unreal Engine by leveraging these metadata values.

## Lights and Cameras

The IFC specification does not define light emitters or cameras in the same way as Unreal Engine or other 3D design and visualization tools.

-   Lights in IFC are treated as building elements. These objects do not have measurements of the properties required for realtime rendering, such as illumination radii, intensity, color, and so on. Datasmith imports each ifcLamp element as an Actor in the Datasmith Scene, the same way it imports all other types of objects from the IFC file. However, Datasmith does not create any light sources for them, like [Point Lights](/documentation/en-us/unreal-engine/point-lights-in-unreal-engine), [Spot Lights](/documentation/en-us/unreal-engine/spot-lights-in-unreal-engine), [Rectangular Area Lights](/documentation/en-us/unreal-engine/rectangular-area-lights-in-unreal-engine), and so on.
-   Cameras are not part of the IFC specification, nor can an IFC file save viewpoints on the scene. Therefore, Datasmith does not create any cameras in the Datasmith Scene.

## Materials

For each surface material that Datasmith finds in your IFC scene, it creates a [Material Asset](/documentation/en-us/unreal-engine/unreal-engine-materials) in Unreal with the same name, and places that Material in the **Materials** folder next to your Datasmith Scene Asset. Datasmith assigns these Material Assets to the Static Mesh Assets it creates in order to shade their surfaces.

-   Each Material in the **Materials** folder is a [Material Instance](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) that exposes properties set in the IFC file: color values, transparency values, specular colors, and so on. Double-click one of these Material Assets to open it in the Material Instance Editor:
    
    Click for full image.
    
    You can change the exposed properties in the **Details** panel to modify the way the Material looks when applied to a surface. For example, the Material shown above exposes properties for its base color and transparency.
    
    Unlike some other file formats and design applications Datasmith works with, IFC does not offer deep controls over the physical characteristics of surface properties. When Datasmith translates Materials from an IFC file, it preserves your original properties as faithfully as possible. However, the results are not typically lifelike or well-suited to the physically based rendering of the Unreal Engine. Typically, you'll want to replace the default Materials that Datasmith creates and assigns to your Static Mesh Assets. You can author your own physically based Materials in Unreal Engine, or import physically based Materials from other sources—for example, from the Marketplace tab of the Epic Games Launcher.
    
-   Datasmith also creates a set of parent Materials in the **Materials/Master** folder. Each of these is the parent of at least one of the Material Assets in the **Materials** folder. You can edit these parent Materials to have greater control over the Material graphs that defines how each surface appears, to expose additional parameters to child instances, or to change the way the exposed parameters are taken into account during rendering.
    
    Changing a parent Material also automatically changes all Material Instances that inherit from that parent. It is a good idea to duplicate a parent Material before you modify it, make your changes to the duplicate, then update specific Material Instances to use the new duplicate as their parent. For details, see [Modifying a Datasmith Master Material](/documentation/en-us/unreal-engine/modifying-a-datasmith-master-material-in-unreal-engine).
    

## Metadata

Datasmith records the properties of each object it imports from the IFC file, and saves those property values as Datasmith Metadata on the Actor it creates to represent that object. You can access this metadata in the Unreal Editor or at runtime in the Unreal Engine.

Left: properties in an IFC file. Right: Datasmith Metadata built from those properties. Click for full image.

### How Datasmith Converts Properties from IFC Files

IFC properties are organized into groups. For example, the image above shows several groups: **PSet\_Revit\_Mechanical**, **PSet\_Revit\_Dimensions**, **PSet\_Revit\_Identity Data**, and so on. However, Datasmith Metadata is always a flat list of keys and values. If your IFC properties contain any groups, as shown above, Datasmith flattens the hierarchy, putting all metadata keys from all groups into a single flat list. The group names themselves are discarded.

IFC Properties in Unreal Engine.

## Credits

-   IFC building courtesy of [https://github.com/buildingSMART/Sample-Test-Files/tree/master/IFC%202x3/Schependomlaan](https://github.com/buildingSMART/Sample-Test-Files/tree/master/IFC%202x3/Schependomlaan).
    
    © original owners.
    
    This work is licensed under the Creative Commons Attribution 4.0 International License. More info and a link to the full license text is available on [http://creativecommons.org/licenses/by/4.0/](http://creativecommons.org/licenses/by/4.0/).
    
-   Other IFC hierarchy images are from Project 3: Clinic, available from the [National Institute of Building Sciences](https://www.nibs.org/?page=bsa_commonbimfiles).
    
-   IFC screen captures taken in the [RDF IFC Viewer](http://rdf.bg/product-list/ifc-engine/) and [Open IFC Viewer](https://openifcviewer.com/) application.
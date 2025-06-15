# Archicad

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-with-archicad-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-with-archicad-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:45

---

This page describes how **Datasmith** imports scenes from **Graphisoft Archicad** into **Unreal Engine**. It follows the basic process outlined in the [Datasmith Overview](/documentation/en-us/unreal-engine/datasmith-plugins-overview) and [Datasmith Import Process](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine), but it provides additional details on the Direct Link workflow and translation behaviors specific to Archicad. If you are planning to use Datasmith to import scenes from Archicad to Unreal Engine, reading this page can help you understand how your scene is translated, and how you can work with the imported scene in Unreal Editor.

## Archicad Workflows

### Datasmith DirectLink

With the DirectLink workflow, you can set up a Datasmith DirectLink between Archicad and Unreal Engine or Twinmotion. This link updates your Unreal Engine level or Twinmotion model, removing the need to re-export a `*.udatasmith` file from your Archicad scene every time you make a change.

### Export Workflow

Using the Export workflow, a `.udatasmith` file can be exported from Archicad for use in Unreal Engine or Twinmotion. For more information on exporting Datasmith content from Archicad, see [Exporting Datasmith Content from Archicad](/documentation/en-us/unreal-engine/exporting-datasmith-content-from-archicad-to-unreal-engine).

For more information importing `.udatasmith` files into Unreal Engine, see [Importing Datasmith Content into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine).

## Using the Datasmith Toolbar

The Datasmith plugin adds the Datasmith toolbar option to the **Windows > Palettes** menu.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe0d39e7-ff23-48c6-9a2b-21b5949111e3/image_0.png)

Datasmith DirectLink toolbar.

| Action | Button | Description |
| --- | --- | --- |
| Synchronize with Direct Link | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5e25f19-5d2a-4c48-a2d8-62c0d9bdb405/sync-icon.png) | Pushes the selected models to Unreal Engine or Twinmotion through the Direct Link connection. |
| Manage Connections | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6caf88e-ddf8-4a94-a779-cd3d335ad3d6/connect-icon.png) | Launches the Connection Status dialog. |
| Export to Datasmith File | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85ad4726-cb4c-4410-933f-27265b6c59f8/export-icon.png) | Launches the existing `.udatasmith` exporter, used to save a `.udatasmith` file to disk. |
| Show Messages | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be9c75a3-4014-4a33-a0ae-154c46bfa10f/messages-icon.png) | Launches the messages and logging window. This is useful for reporting errors, missing textures, and other information. |

## Geometry, Layers, and Scene Hierarchy

Archicad objects are imported into Unreal Engine as a single Actor composed of several nested Static Mesh components.

![World Outliner showing the hierarchy of an imported Archicad file.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d978da5c-36e5-43d6-876d-68ab373b77f3/image_1.png)

World Outliner showing the hierarchy of an imported Archicad file.

Each Actor in the World Outliner represents a Layer in Archicad and is visible from the Layers panel in Unreal Editor.

![Layers represented by Actors in the World Outliner are also represented as layers in the Layer panel.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71918596-918c-412e-9423-170a5eb7b90f/image_2.png)

Layers represented by Actors in the World Outliner are also represented as layers in the Layer panel.

Object pivot points are imported into Unreal Engine and they retain their same locations from Archicad. However, in some cases due to Archicad SDK limitations, it is possible that pivot locations will not be correctly defined resulting in a mismatch like the one shown below.

![Notice that the pivot point for the chair is different in the Editor than in Archicad.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72b2042c-f9e0-46cc-a218-a695ab87601e/image_3.png)

Notice that the pivot point for the chair is different in the Editor than in Archicad.

## HotLinks Modules

Unreal Engine retains your Archicad HotLink external references that contain 3D elements by importing them as an extra Actor with nested Static Meshes into the Level.

## Materials

Unreal Engine builds Materials in the Datasmith scene using a Physically Based Rendering (PBR) graph, where the Master materials are built in realtime by the Datasmith Importer. This process retains the look of the Archicad materials when importing them into Unreal Engine.

![The export plugin retains the look of Materials from Archicad when importing into Unreal Engine.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f169a41d-0706-47fd-a8b9-32081ce07290/image_4.png)

The export plugin retains the look of Materials from Archicad when importing into Unreal Engine.

There are two types of materials in Archicad:

-   Standard materials derived from surface attributes.
    
-   Materials derived from GDL objects.
    

### Standard Archicad Materials

Materials from Archicad are exported as PBR materials and imported into Unreal Engine with the following attributes being retained:

-   Base color
    
-   Texture transparency
    
-   UV size and more
    

![Properties highlighted in green are considered by the Datasmith exporter.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42ae2805-53f5-4bba-bb05-4d57f9a2bcbb/image_5.png)

Properties highlighted in green are considered by the Datasmith exporter.

### GDL and Two-Sided Materials

All architectural objects within Archicad are considered closed objects and are exported with materials that are one-sided.

Objects that are thin, such as GDL and Morph objects, export with materials that are two-sided. When this happens, the material name will be appended with a `_DS` suffix to maintain separation in Unreal Engine from single-sided materials.

![The highlighted material is double sided and the name contains the _DS suffix.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07f4a3af-6aad-4caa-a2c0-1580ec1668c6/image_6.png)

The highlighted material is double sided and the name contains the \_DS suffix.

## Lights

The Datasmith exporter supports basic light types and their parameters. Area lights are imported into Unreal Engine as point lights. Environment and parallel lights are not supported.

![A variety of light types imported from Archicad into Unreal Engine.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/155cd8d6-1d1b-49e0-ae82-22ec782d7f55/image_7.png)

A variety of light types imported from Archicad into Unreal Engine.

| Archicad Light Type | Unreal Engine Light Class | Supported Parameters | Unsupported Parameters |
| --- | --- | --- | --- |
| **General Light** | Point Light | 
-   Intensity
-   Color
-   Falloff Distance
-   Absolute Light Intensity



 | 

-   Shadow casting parameters (Opacity and Quality)



 |
| **Spot Light** | Spot Light | 

-   Intensity
-   Color
-   Falloff Distance
-   Absolute Light Intensity
-   Fade out between inner and outer angles



 | 

-   Shadow casting parameters (Opacity and Quality)
-   Spot light geometry (limited to circle)



 |
| **IES Light** | Point Light with IES profile | 

-   Intensity
-   Color
-   Falloff Distance
-   Absolute Light Intensity
-   IES Shape
-   IES Intensity



 | 

-   Shadow casting parameters (Opacity and Quality)
-   Use Area Shape and Size given in Photometric file
-   IES Light Quality/Grainy Illumination



 |
| **Area Light** | Datasmith Area Light | 

-   Intensity
-   Color
-   Falloff Distance
-   Absolute Light Intensity
-   Size Length/Width



 | 

-   Shadow casting parameters (Opacity and Quality)
-   Use Area Shape and Size given in Photometric file
-   IES Light Quality/Grainy Illumination



 |
| **Parallel Light** | Not Supported | Not Supported | Not Supported |
| **Sun Object** | Not Supported | Not Supported | Not Supported |
| **Window Light** | Not Supported | Not Supported | Not Supported |

## Cameras

The current viewpoint in Archicad at the time of export is imported into Unreal Engine as a Camera Actor named "Current View." The following camera properties are supported:

-   Transform
    
-   Sensor Width and Height
    
-   Focal Length Min and Max
    
-   FStop Min and Max
    
-   Focus Distance
    
-   Current Focal Length
    
-   Current Aperture
    

![Archicad camera settings retained during the import into Unreal Engine.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0eb9f513-fc0b-416a-a703-e4921f2f0c2f/image_8.png)

Archicad camera settings retained during the import into Unreal Engine.

Unreal Engine also supports Path Cameras. They are imported as Camera Actors under a Scene Actor using the Path name in Archicad.

![Path Cameras in Archicad.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0873c71b-630e-489e-9c61-931bb3427eee/image_9.png) ![Camera Actors in the World Outliner.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ec1899b-0943-4b6d-9e95-ef37cd54174f/image_10.png)

Path Cameras are supported and are imported into the World Outliner as Camera Actors.

## Metadata and Classifications

Most properties within Archicad are exported to Unreal Engine as MetaData when:

-   The element name Key ID value is the same as the element's name. For example, the ID value for a door is "Wooden\_Door".
    
-   The key value uses a specific classifications, including:
    
    -   Key value uses the classification System suffixed with "\_ID".
        
    -   Key value uses the classification System suffixed with "\_Name". This is generally empty.
        
    -   Key value uses the classification System suffixed with "\_Description". This is generally empty.
        
-   Categories key values contain the prefix "CAT\_Xyz"
    
-   IFCProperties key values contain the prefix "IFC\_Xyz"
    
-   IFCAttributes key values contain the prefix "IFC\_Attribute\_Xyz"
    

Undefined metadata will not be exported.

For example, if you were to export a Door from Archicad:

![Properties of a wooden door in Archicad.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/727aa61b-3b16-4ede-9cfe-2867bf86c9f1/image_11.png)

Properties of a wooden door in Archicad.

It would export as:

```

`<MetaData name="MetaData_95D3E85A-69DE-4E5D-993D-74480D3FBDBA" reference="Actor.95D3E85A-69DE-4E5D-993D-74480D3FBDBA"> 	<KeyValueProperty name="ID" type="String" val="Porte_Bois"/> 	<KeyValueProperty name="ARCHICAD_Classification_ID" type="String" val="Door"/> 	<KeyValueProperty name="CAT_Position" type="String" val="Interior"/> 	<KeyValueProperty name="CAT_Renovation_Status" type="String" val="Existing"/> 	<KeyValueProperty name="CAT_Show_On_Renovation_Filter" type="String" val="All Relevant Filters"/> 	<KeyValueProperty name="CAT_Structural_Function" type="String" val="Non-Load-Bearing Element"/> 	<KeyValueProperty name="IFC_ProductionYear" type="String" val="2021"/> 	<KeyValueProperty name="IFC_AcousticRating" type="String" val="patate"/> 	<KeyValueProperty name="IFC_FireRating" type="String" val="radis"/> 	<KeyValueProperty name="IFC_IsExternal" type="String" val="False"/> 	<KeyValueProperty name="IFC_FireResistanceRating" type="String" val="pastop"/> 	<KeyValueProperty name="IFC_IsCombustible" type="String" val="False"/> 	<KeyValueProperty name="IFC_SerialNumber" type="String" val="serialnumber"/> 	<KeyValueProperty name="IFC_Renovation_Status" type="String" val="Existing"/> 	<KeyValueProperty name="IFC_Attribute_GlobalId" type="String" val="2Lq_XQQTvENPazT4WDFxsw"/> 	<KeyValueProperty name="IFC_Attribute_Name" type="String" val="TestCustomName"/> 	<KeyValueProperty name="IFC_Attribute_Tag" type="String" val="95D3E85A-69DE-4E5D-993D-74480D3FBDBA"/> 	<KeyValueProperty name="IFC_Attribute_OverallHeight" type="String" val="210.00"/> 	<KeyValueProperty name="IFC_Attribute_OverallWidth" type="String" val="90.00"/> </MetaData>`

Copy full snippet
```
<MetaData name="MetaData\_95D3E85A-69DE-4E5D-993D-74480D3FBDBA" reference="Actor.95D3E85A-69DE-4E5D-993D-74480D3FBDBA"> <KeyValueProperty name="ID" type="String" val="Porte\_Bois"/> <KeyValueProperty name="ARCHICAD\_Classification\_ID" type="String" val="Door"/> <KeyValueProperty name="CAT\_Position" type="String" val="Interior"/> <KeyValueProperty name="CAT\_Renovation\_Status" type="String" val="Existing"/> <KeyValueProperty name="CAT\_Show\_On\_Renovation\_Filter" type="String" val="All Relevant Filters"/> <KeyValueProperty name="CAT\_Structural\_Function" type="String" val="Non-Load-Bearing Element"/> <KeyValueProperty name="IFC\_ProductionYear" type="String" val="2021"/> <KeyValueProperty name="IFC\_AcousticRating" type="String" val="patate"/> <KeyValueProperty name="IFC\_FireRating" type="String" val="radis"/> <KeyValueProperty name="IFC\_IsExternal" type="String" val="False"/> <KeyValueProperty name="IFC\_FireResistanceRating" type="String" val="pastop"/> <KeyValueProperty name="IFC\_IsCombustible" type="String" val="False"/> <KeyValueProperty name="IFC\_SerialNumber" type="String" val="serialnumber"/> <KeyValueProperty name="IFC\_Renovation\_Status" type="String" val="Existing"/> <KeyValueProperty name="IFC\_Attribute\_GlobalId" type="String" val="2Lq\_XQQTvENPazT4WDFxsw"/> <KeyValueProperty name="IFC\_Attribute\_Name" type="String" val="TestCustomName"/> <KeyValueProperty name="IFC\_Attribute\_Tag" type="String" val="95D3E85A-69DE-4E5D-993D-74480D3FBDBA"/> <KeyValueProperty name="IFC\_Attribute\_OverallHeight" type="String" val="210.00"/> <KeyValueProperty name="IFC\_Attribute\_OverallWidth" type="String" val="90.00"/> </MetaData>

Classifications can be added and edited within Archicad using the Classification Manager:

![The Classification Manager within Archicad is used to add additional Classifications.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/289a16b6-de32-4d36-b2d1-65111f1cb607/image_12.png)

The Classification Manager within Archicad is used to add additional Classifications.

This menu can be found by clicking the **Classification Manager** option in the **Windows** menu.

## Actor Tags

Archicad technical data can be exported to Unreal Engine by leveraging Actor Tags within the editor. The data stored within Actor Tags can then be used to perform a variety of operations using Visual Dataprep, Python scripting, and more.

Currently the Datasmith plugin exports:

-   ID
    
-   Type
    
-   LibPart (Main, Rev, Name)
    

![Tag values are imported  into Unreal as Actor Tags.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74e2be11-4c6f-4ccb-a452-559396d446a9/image_13.png)

Tag values are imported into Unreal as Actor Tags.
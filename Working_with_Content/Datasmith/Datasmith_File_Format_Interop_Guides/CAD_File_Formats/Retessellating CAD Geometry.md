# Retessellating CAD Geometry

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/retessellating-cad-geometry-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/retessellating-cad-geometry-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:18

---

When you use the Datasmith importer to bring a scene into the Unreal Editor from a supported CAD file that contains surfaces defined by parametric curves, Datasmith tessellates the surfaces of those scene objects into triangular meshes. At the time you import your file, you provide settings that control the fidelity of the resulting triangular meshes to the original parametric surfaces. You can read more about these settings under [Using Datasmith with CAD File Formats](/documentation/en-us/unreal-engine/importing-cad-files-into-unreal-engine-using-datasmith#tessellation). Datasmith uses the import settings you provide at the time you import your CAD file to tessellate all geometry in the scene.

In addition, after your initial import, you can override the values of the tessellation quality settings for individual Static Mesh Assets that you select. This helps you to import your overall scene at one level of detail—typically a low level of detail that tessellates all the objects in the scene relatively quickly. Then, after importing, you can retessellate selected Assets with different quality settings—typically higher levels of detail that provide better visual results for important scene objects. This way, you can achieve a balance between import speed, model complexity, and visual quality that fits the unique needs of each Project's content.

The effect is very similar to the ability to reimport individual Static Mesh Assets in a Datasmith Scene, as described in [About the Datasmith Reimport Process](/documentation/en-us/unreal-engine/datasmith-reimport-workflow-in-unreal-engine). However, the difference is that when you *reimport* a scene element, Datasmith opens the original CAD scene file, re-reads the geometry data for the selected object from the file, then tessellates that newly imported geometry. When you *retessellate* the geometry instead, Datasmith does not reopen the original scene file at all. It applies the new tessellation settings to the last imported geometry for the selected Static Mesh Asset. Therefore, retessellating tends to be faster than reimporting, and you can do it even when the original CAD source file is unavailable.

To retessellate individual Static Mesh Assets:

1.  Select the Static Mesh Assets that you want to retessellate in the **Content Browser**, in the **Geometries** folder next to your Datasmith Scene Asset.
    
2.  Right-click any Asset that you have selected, and choose the **Datasmith > Retessellate** option from the context menu.
    
3.  Set new values for the tessellation settings described on the [Using Datasmith with CAD File Formats](/documentation/en-us/unreal-engine/importing-cad-files-into-unreal-engine-using-datasmith#tessellation) page.
    
    ![Retessellation options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbf243e2-439f-43ec-8806-e08d26be40b8/retessellate-options.png "Retessellation options")
    
    This window only contains the settings that control geometry tessellation, not any other settings that you usually set when you import a Datasmith file. If you need to change other import settings, use the **Reimport** option to reimport the selected Asset from its original CAD scene file.
    
4.  Click **Import**.
    

The retessellation process uses the new values to recompute the triangular mesh for the selected Static Mesh Asset or Assets, but leaves all other Assets in the Datasmith Scene unchanged.

![Before retessellation: high tolerance, fewer triangles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f457ddad-8d12-4cab-920c-594e7a038303/retessellation-before.png)

![After retessellation: low tolerance, more triangles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bd03260-70d7-4278-bd94-eb18260cea17/retessellation-after.png)

If you don't see the **Retessellate** option in the context menu, one or more of the Assets you selected were not tessellated at the time they were originally imported. This typically means that the CAD file already contained a triangular mesh for the Asset, rather than a parametric surface. The Datasmith importer simply brought in that existing triangular mesh, and has no original parametric surface data to use as a basis for retessellation.

If this is the case, and if you need to *simplify* the geometry of the Static Mesh, you can do so using other tools provided by the Unreal Editor: the [Proxy Geometry Tool](/documentation/en-us/unreal-engine/proxy-geometry-tool-in-unreal-engine), [Levels of Detail](/documentation/en-us/unreal-engine/creating-and-using-lods-in-unreal-engine), and so on. However, you won't be able to *increase* the detail of the Static Mesh geometry.

## Retessellation Rule

After modeling operations, a NURBS surface can be:

-   **Intact**, which means no triangles were removed from the surface after tessellation.
-   **Altered**, which means several triangles were removed.
-   **Deleted**, which means all triangles were removed.

With that in mind, you can use the **Retessellation Rule** option controls which surfaces need to be retessellated. You can select one of the following options:

-   **All** selects all surfaces for retessellation.
-   **Skip Deleted Surfaces** excludes surfaces that had all of their triangles removed.
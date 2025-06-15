# DMX MVR Import and Export

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-mvr-import-and-export-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-mvr-import-and-export-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:02

---

“In the entertainment industry, the MVR file format allows programs to share data and geometry for a scene. A scene is a set of parametric objects such as fixtures, trusses, video screens, and other objects that are used in the entertainment industry.” (Quote: MVR Standard)

You can import MVR Files into Unreal Engine to use with DMX. Manually importing an MVR file only includes DMX-related fixtures and patching information. To also import static and scene geometry, use [Datasmith](/documentation/en-us/unreal-engine/datasmith-plugins-for-unreal-engine) and the [Datasmith MVR plugin](/documentation/en-us/unreal-engine/dmx-mvr-import-and-export-in-unreal-engine#importanmvrfileusingthedatasmithmvrplugin).

## MVR Exporter

![A promotional graphic of two stylized file icons, an MVR file and a GDTF file.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d11e65f0-b2bb-4189-8fbf-323dfb26bd08/mvr-exporter.png)

You can use the **MVR Exporter** in Unreal Engine to share DMX Libraries with lighting desks and 3rd party software.

The exported MVR file includes the following information from the DMX Library:

-   Patching information
-   Fixture definitions
-   Fixture GDTF signatures

### MVR Export Process

To export a DMX Library as an MVR file, follow these steps:

1.  Open the DMX Library from the **Content Browser**.
2.  Click **Export**.
    
    ![A screenshot of the Export button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7dc045d4-7f13-497d-b2ea-39483f228b76/mvr-export-button.png)
3.  Set the following options:
    
    1.  **Consider Level**: If checked, uses data from the current level. Must be checked for the other options to be available.
    2.  **Export Patches not Present in the World**: If checked, exports patches that are not used in the current level.
    3.  **Use Transforms from Level**: If checked, uses the transforms of patches as used in the level. If unchecked, uses the default transforms of Fixture Patches.
    4.  **Create Multi Patch Fixtures (experimental)**: If the same Fixture Patch is used more than once in a level, creates an MVR multi patch.
    
    ![The MVR export options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57f94369-50be-4c89-ac38-05ff8a5217db/mvr-export-options.png)
4.  Click **Export**.

Unreal Engine relies on Datasmith to import scene elements. If the DMX Library was created from an MVR file, then it retains the scene elements when the DMX Library is exported as an MVR file.

## Import an MVR File Manually

To manually import an MVR file into Unreal Engine, follow these steps:

1.  Drag the MVR file from your device into the **Content Browser**. This creates a DMX Library Asset using the data from the MVR file.
2.  Drag the DMX Library Asset into the level to populate the **DMX MVR Scene Actor**. This spawns the DMX-enabled Blueprint Actors at the right location along with their transforms.

It is possible but not recommended to add the same DMX Library to a level more than once. Adding more than one may lead to ambiguous MVR Fixture IDs for the actors, which will cause limitations during MVR export.

### DMX MVR Scene Actor

The DMX MVR Scene Actor contains a list of DMX-enabled Blueprints, automatically chosen to match the attributes of the fixtures described in the MVR file.

![A screenshot of the DMX MVR Scene Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de9635d4-81c7-4bef-9f3e-cb4bc31d66c5/dmx-mvr-scene-actor.png)

The **Details** panel for the MVR Scene Actor include the following options:

![The Details panel for the MVR Scene Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b9683cb-02b8-44e3-8de4-7aa0afaca4ee/mvr-scene-actor-details.png)

-   **Write Transforms to DMX Library**: Writes the current transforms of the fixture to the DMX Library.
-   **Refresh Actors from DMX Library**: Refreshes the DMX Library, spawns new actors, and includes the following options:
    -   **Respawn Deleted Actors**: When enabled, respawns deleted Fixture actors that are defined in the DMX Library.
    -   **Update Transforms**: When enabled, Fixture actors adopt the transform of their related patch in the DMX Library.
-   **Fixture Type to Spawned Actor**: Shows a list of Fixture Types described in the DMX Library. Use the dropdown menu to match a different Blueprint to the fixture. This replaces all Actors that make use of a Fixture Patch with related Fixture Type. You can only select Blueprints that implement the MVR Fixture Actor Interface.

### DMX MVR Fixture Actor Interface

You can implement the MVR Fixture Actor Interface in any actor class in Blueprints or C++.

![A screenshot of the DMX MVR Fixture Actor Interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99e9ee9c-9aa3-4dd0-8549-862d46dd16ce/fixture-actor.png)

**On MVR Get Supported DMX Attributes** returns the attributes that the Blueprint's actor supports. When an MVR file is imported, each fixture is automatically matched with the Blueprint of the actor with the most matching attributes.

Actors that implement the DMX MVR Fixture Actor Interface need to have exactly one DMX component attached. The component is automatically patched when the actor is spawned in an MVR scene. The engine logs an error if no or many DMX components are used in an Actor that implements the DMX MVR Fixture Actor Interface.

## Import an MVR File Using The Datasmith MVR Plugin

### Export MVR and Datasmith Files from Vectorworks Datasmith

1.  In Datasmith, click **File** > **Export** > **Unreal Datasmith (3D Only)** to export your Vectorworks scene.
2.  Click **File** > **Export** > **MVR** to export the DMX-related data from fixtures, GDTF, and patching information.

Place your MVR file in the same directory and use the same filename as the `.udatasmith` file from step 1.

### Import MVR and Datasmith Files into Unreal Engine

1.  In Unreal Engine, go to the Main Toolbar and click Create > Datasmith > File Import…
    
    ![A screenshot of the File Import menu option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e1c7fd3-ba68-4ab1-8646-a3e3221ce07b/import-datasmith-file.png)
2.  In the dialog, enable **Import MVR** to import DMX-related fixtures and patching information. If you only require the 3D geometry from the Datasmith file, then you can uncheck this option.
    

Place the MVR file in the same directory location as the `*.datasmith` file.

![A screenshot of the Datasmith Import Options window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dce8fb53-6699-47dc-a338-7a6c63b5d94a/datasmith-import-options.png)

### Unreal Imported Scene

The following example shows a sample Vectorworks project in Unreal Engine once fully imported through this process.

![A screenshot of a sample Vectorworks project imported into Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64cd321f-bed0-4dca-98b8-e7fd55b3965d/unreal-imported-scene.png)

Note the following elements in the editor:

1.  Content Browser
    -   Datasmith Scene
    -   DMX Library
2.  Preview Window
    -   Instanced 3D scene, geometry with textures and materials
    -   Instanced DMX enabled fixture BPs
3.  Datasmith Scene Actor
    -   Actor Scene Geometry actor
    -   DMX MVR Scene Actor
4.  Datasmith settings

#### Datasmith Scene

This asset contains all the mesh, texture, and material references imported from Vectorworks through Datasmith.

![The Details panel for a Datasmith scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3930b301-7a93-4264-88c1-b9ab57594e0d/datasmith-scene.png)

#### DMX Library

The DMX Library asset contains the following information:

1.  Fixture Types
2.  GDTF signature
3.  Attribute definitions

![A screenshot of a DMX Library](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7cf68661-e6e4-4dd2-bf98-5cb0d3b93c5a/dmx-library.png)

It also includes the DMX patching data imported from Vectorworks using the MVR standard.

![A screenshot of the DMX patching data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0e34bb6-2891-40ba-827c-e9c8215134e5/dmx-patching-data.png)

#### Datasmith Scene Actor

The instantiated Datasmith Scene Actor in your level contains two actors:

-   Actor Scene Geometry actor: this contains all of the instantiated 3D geometry, materials and texture references. !A screenshot of the Actor Scene Geometry actor\](actor-scene-geometry.png)
-   DMX MVR Scene Actor: This contains all of the DMX-enabled fixture Blueprints. These Blueprints are automatically chosen when you import the MVR file. You can choose to assign different Blueprints in the **GDTF To Spawned Actor** section.
    
    ![A screenshot of the DMX MVR Scene Actor](dmx-mvr-scene-actor2.png)

Use the **Details** panel to access **Update actors from Scene** and **Respawn** options for the **DatasmithSceneActor**. For more information about respawning and updating actors, refer to [Reimporting Datasmith Content](/documentation/en-us/unreal-engine/datasmith-reimport-workflow-in-unreal-engine).

![A screenshot of the DatasmithSceneActor options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/177cc43f-9086-4415-80b1-1dd4e2ceff7d/update-actors.png)

MVR and Datasmith scene actors are mutually exclusive in ownership and control. A live sync from Datasmith will not work with an MVR scene actor.
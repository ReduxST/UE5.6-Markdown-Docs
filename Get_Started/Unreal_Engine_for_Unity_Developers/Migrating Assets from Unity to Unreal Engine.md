# Migrating Assets from Unity to Unreal Engine

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/migrating-assets-from-unity-to-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/migrating-assets-from-unity-to-unreal-engine)  
**Processed:** 2025-06-14 16:36:11

---

# Importing and Converting Assets

**Unreal Engine 5** projects contain a variety of assets that make up the final game. Some of those asset types are specific to Unreal Engine, such as Blueprint classes, while others are universal file formats that can be imported into the engine.

This document goes over the types of assets you can import into Unreal Engine, how to import them, and links to additional information.

## Common Asset Types

Unreal Engine 5 supports the following asset types:

| Unreal Asset Type | Unity Equivalent | Supported Formats |
| --- | --- | --- |
| [Static Mesh](/documentation/en-us/unreal-engine/importing-static-meshes-in-unreal-engine) | Mesh | .fbx, .obj |
| [Skeletal Mesh](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine) | Skinned Mesh | .fbx, .obj, .usd |
| [Animation Sequence](/documentation/en-us/unreal-engine/fbx-animation-pipeline-in-unreal-engine) | Animation, Mecanim | .fbx, .obj, .abc |
| [Texture](/documentation/en-us/unreal-engine/textures-in-unreal-engine) | Texture | .bmp, .float, .jpeg, .jpg, .pcx, .png, .psd, .tga, .dds (Cubemap or 2D), .exr (HDR), .tif (TIFF), .tiff (TIFF) |
| [Audio File](/documentation/en-us/unreal-engine/importing-audio-files) | Audio File | .wav, .ogg, .flac, .aif, .opus, .mp3 |
| [Video Files](/documentation/en-us/unreal-engine/media-framework-technical-reference-for-unreal-engine) | Video clip | .mov, .mp4, .wmv |
| [Fonts](/documentation/en-us/unreal-engine/importing-fonts-in-unreal-engine) | Font asset | .ttf, .otf |
| [glTF File](/documentation/en-us/unreal-engine/importing-gltf-files-into-unreal-engine) | glTF File | .gltf (JSON), .glb |
| [SpeedTree Model](https://docs.speedtree.com/doku.php?id=ue4_introduction) | SpeedTree | .srt |

## Asset Considerations Before Importing to Unreal Engine

### Unreal Engine’s Coordinate System

Unreal Engine uses the [Cartesian coordinate system](https://en.wikipedia.org/wiki/Cartesian_coordinate_system) to represent positions in three-dimensional [Euclidean space](https://en.wikipedia.org/wiki/Euclidean_space). The coordinate system in the Unreal Editor is left-handed and uses the **X axis** to represent the **forward / backwards** direction, the **Y axis** to represent the **right / left** directions, and **Z axis** to represent the **up / down** directions.

![Unreal Engine’s coordinate axes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d394634-a514-4e46-9765-1bb67b56f09b/coordinate-axes.gif)

Unity’s coordinate system is also left-handed. However, Unity uses the **X axis** to represent **right / left**, **Y Axis** to represent **up / down**, and the **Z Axis** to represent the **forward / backwards** direction.

This has implications when directly importing assets from Unity to Unreal Engine as the asset’s orientation may be incorrect. To solve this, you can change the asset’s orientation inside a digital content creation (DCC) package such as Maya or Blender, or directly in the **Import dialogue** of Unreal Engine.

You can learn more about Unreal Engine’s coordinate system by reading the [Coordinate System and Spaces](/documentation/en-us/unreal-engine/coordinate-system-and-spaces-in-unreal-engine) documentation.

### Units of Measurement in Unreal Engine

Unreal Engine uses the [Metric System](https://en.wikipedia.org/wiki/Metric_system) to measure object size and distance. Specifically, Unreal Engine uses the **Unreal unit (UU)** internally for measurements. **One Unreal Unit** is equivalent to **1 cm**.

Use this information to assign the correct scale when creating meshes in an external digital content creation (DCC) package.

Unity also uses the Metric System internally, with **one Unity unit** being equal to **1 meter (100 cm)**. This will affect the scale of objects imported directly from Unity into Unreal Engine.

You can learn more about Unreal Engine’s units of measurement by reading the [Units of Measurement](/documentation/en-us/unreal-engine/units-of-measurement-in-unreal-engine) documentation.

### FBX Content Pipeline

Unreal Engine supports a variety of file formats for importing content into your project. One of the most popular asset formats is **Autodesk FBX**.

The FBX format provides interoperability between many digital content creating (DCC) packages and offers the following advantages:

-   Using a single file format for static meshes, skeletal meshes, animations, and morph targets.
    
-   Importing multiple LODs and Morphs/Blendshapes in one import operation.
    
-   Importing material and texture assets, and automatically applying them to static meshes.
    

Unreal Engine’s FBX pipeline uses **FBX 2020.2**, so we recommend using that version to avoid possible incompatibilities when importing assets.

To learn more about the FBX pipeline, read the [FBX Content Pipeline](/documentation/en-us/unreal-engine/fbx-content-pipeline) documentation.

## Version Information

At the time of writing, the version of Unreal Engine and Unity engine used for screenshots and terminology are as follows:

-   Unreal Engine 5.4.3
    
-   Unity 6 (6000.0.2f1)
    

## Preparing to Export Assets from Unity

Before exporting assets from Unity, follow these steps to **enable** the **FBX Exporter** package:

1.  In Unity, click **Window > Package Manager** to open the **Package Manager** window.
    
    ![Click Window - Package Manager](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12a51451-15cd-460c-9194-58fb5c30926a/unity-import-1.png)
2.  Click the **Unity Registry** category on the left and search for **FBX Exporter**. Click **Install** to install the package.
    
    ![Search for FBX Exporter and install the package](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ffe12e6-e72d-4c3c-ac24-5b6c76418d13/unity-import-2.png)
3.  Once the package is installed, close the **Package Manager** window.
    

You can now **right-click** a prefab in the **Hierarchy** window and select **Export to FBX** to export it as an .fbx file.

Alternatively, you can open your Unity project’s **source folder** and directly copy certain files, such as textures directly.

## Meshes / Static Meshes

![A static mesh in Unity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0989036-216f-4f11-b1ca-afc64be90b9f/unity-import-5.png)

**Static meshes** are 3D meshes whose geometry does not change. You can import static meshes to Unreal Engine in .**fbx** or .**obj** formats, with .fbx as the preferred format. You can learn more about static meshes in Unreal Engine by reading the [Static Meshes](/documentation/en-us/unreal-engine/static-meshes) documentation.

This example shows you how to export the Unreal Engine **material ball** static mesh from Unity into Unreal.

This prefab has one mesh and three materials. However, your mesh prefab can contain multiple meshes in its hierarchy.

![The Unreal Engine material ball static mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3742af30-4a1b-4b1f-bcfa-78bc268af9ad/unity-import-6.png) ![This prefab has one mesh and three materials](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bcd47d33-81a6-444a-a8e3-e683c1675ffe/unity-import-7.png)

### Export a Static Mesh from Unity

To export a **static mesh** from Unity, follow these steps:

1.  Right-click the prefab in the **Hierarchy** window and select **Export FBX…** from the menu.
    
    ![Right click the prefab in the Hierarchy window and select Export FBX](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb7d320e-323e-4cc6-a1ee-d765b431c3bf/unity-import-8.png)
2.  In the **Export Options** window, enter the **Export Name** and **Export Path**.
    
    1.  Under the **Options** category, select the **ASCII Export Format**.
    2.  Click the **Include** dropdown and select **Model(s) Only**.
    3.  If your mesh has Levels of Detail (LODs) then select the appropriate level.
    4.  **Enable** the **Embed Textures** checkbox if you want to export the mesh materials with their corresponding textures.
    5.  Click **Export** to export your static mesh.
    
    ![Enter the correct export options for your static mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be282d36-c2e6-419a-a05a-8185ce3aa2c1/unity-import-9.png)
3.  Go to the **Export Path** folder to find the static mesh .fbx file. This is the file you will import to Unreal Engine.
    
    ![Go to the Export Path folder to find the static mesh .fbx file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ceaa475d-6d22-4ffd-934f-7a75607ec597/unity-import-10.png)

### Import a Static Mesh to Unreal Engine

To import a **static mesh** to Unreal Engine, follow these steps:

1.  Open **Unreal Engine** and click the **Import** button in the **Content Browser**.
    
    ![Click the Import button in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21a1ddf1-d527-42f7-bb4a-652c11c22090/unity-import-11.png)
2.  Navigate to the **Export Path folder** and **select the mesh** .fbx file, then click **Open**.
    
    Alternatively, after using the **Show in Explorer** setting in Unity, you can **drag** the file from the file explorer window directly into the Unreal Engine **Content Browser** to import it.
    
3.  The **FBX Import Options** window will open to show the **import settings** for the static mesh.
    1.  Scroll to the bottom of the window to the **Fbx File Information** section to see the asset details. Notice that the **Creator Application** appears as **Unity FBX Exporter 5.1.1** and the **File Axis Direction** is **Y-UP**.
        
        ![Scroll down to the Fbx File Information section to see the asset details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/defb6a29-e3d4-441f-b154-47d77675376f/unity-import-13.png)
    2.  Scroll up to the **Mesh** section and **enable** the **Generate Missing Collision checkbox**.
        
        ![Enable the Generate Missing Collision checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac70f72c-b3a5-4bdb-9285-862163b663f5/unity-import-14.png)
    3.  Expand the **Advanced** section and **enable** the **Combine Meshes** checkbox if you want to combine several meshes into one. You can also **enable** the **Import Mesh LODs** if your mesh has LODs.
        
        ![Enable the Combine Meshes and Import Mesh LODs checkboxes if desired](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30abf0fc-3011-481f-833c-ed93fc97e003/unity-import-15.png)
    4.  Scroll down to the **Miscellaneous** section and **enable** the **Convert Scene** and the **Force Front X Axis** checkboxes.
        
        ![Enable the Convert Scene and the Force Front X Axis checkboxes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01234e51-c0c5-4e22-9fab-1ecb81729f47/unity-import-16.png)
    5.  Scroll down to the **Material** section, click the **Material Import Method** dropdown, and select **Create New Materials**. This will automatically create new materials for the static mesh.
        
        ![Click the Material Import Method dropdown and select Create New Materials](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6f7f634-fa07-4303-8783-72a1cd353784/unity-import-17.png)
        
        For more information on the settings available in the FBX Importer, go to the FBX Import Options Reference page.
        
4.  Click **Import All** to import the static mesh to Unreal Engine.
    
    ![Click Import All](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0f3a012-70ed-499f-827a-34fb87dc38f1/unity-import-18.png)
5.  The **static mesh** asset along with the **materials** and **textures** are now imported to Unreal Engine.
    
    ![The static mesh asset is now imported to Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bc27b33-100d-41da-9f50-ef1f34975228/unity-import-19.png)
6.  **Drag** the **static mesh** asset from the **Content Browser** to the level to see the final result.
    
    ![Drag the static mesh asset to the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2acffdb-7ed3-47b1-a6a1-388b3a4a945b/unity-import-20.png)

Learn more about the static mesh FBX pipeline by reading the [FBX Static Mesh Pipeline in Unreal Engine](/documentation/en-us/unreal-engine/fbx-static-mesh-pipeline-in-unreal-engine) documentation.

## Skinned Meshes / Skeletal Meshes

![A skeletal mesh in Unity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35031a25-902a-4adb-b3ed-ac126bd53141/unity-import-21.png)

Characters in Unreal Engine are created using multiple unique assets that render the visual geometry, play animations, and construct logic that controls the character's behaviors in real time.

The foundational asset for characters in Unreal Engine is the **skeletal mesh** asset, which contains the character's **visual mesh**, or geometric model render of the character, and the character's **[skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine)** that contains bone data, which is used to animate the character.

Learn more about skeletal meshes in Unreal Engine by reading the [Skeletal Meshes](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) documentation.

This example shows you how to export Unreal Engine’s **Quinn** character from Unity to Unreal.

This prefab has a **root** component which holds several transforms for IK processing, and a **skeletal mesh** component which has the Skinned Mesh Renderer and two materials.

![Quinn character prefab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64b0216c-53f5-46bc-aed9-b487dfcc9e6c/unity-import-22.png) ![The skeletal mesh component which has the Skinned Mesh Renderer and 2 materials](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0fd8146-af47-4ff1-a8b5-a7781573f651/unity-import-23.png)

### Export a Skeletal Mesh from Unity

To export a **Skeletal Mesh** from Unity, follow these steps:

1.  Right-click the prefab in the **Hierarchy** window and select **Export FBX…** from the menu.
    
    ![Right click the prefab in the Hierarchy window and select Export FBX](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fe025e0-a38a-4673-90cc-5bb8e0514b51/unity-import-24.png)
2.  In the **Export Options** window, enter the **Export Name** and **Export Path**.
    
    1.  Under the **Options** category, select the **ASCII Export Format**, then click the **Include** dropdown and select **Model(s) + Animations**. This will include any animations assigned to the skeletal mesh.
    2.  If your mesh has Levels of Detail (LODs), select the appropriate level.
    3.  **Enable** the **Animated Skinned Mesh** checkbox.
    4.  **Enable** the **Embed Textures** checkbox if you want to export the mesh materials with their corresponding textures.
    5.  Click **Export** to export your static mesh.
    
    ![Enter the correct export options for your skeletal mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/336df526-aee5-4230-a101-3bd4cfcf8e95/unity-import-25.png)
3.  Go to the **Export Path** folder to find the skeletal mesh .fbx file. This is the file you will import to Unreal Engine.
    
    ![Go to the Export Path folder to find the skeletal mesh .fbx file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2dc470a-e76d-468a-8b12-ec5beb5d82bf/unity-import-26.png)

### Import a Skeletal Mesh to Unreal Engine

To import a **Skeletal Mesh** to Unreal Engine, follow these steps:

1.  Open **Unreal Engine** and click the **Import** button in the **Content Browser**.
    
    ![Click the Import button in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3297d81c-81e0-4774-b459-9f9070e64045/unity-import-27.png)
2.  Navigate to the **Export Path folder** and **select the skeletal mesh** .fbx file then click **Open**.
    
    Alternatively, after using the **Show in Explorer** setting in Unity, you can **drag** the file from the file explorer window directly into the Unreal Engine **Content Browser** to import the file.
    
3.  The **FBX Import Options** window will open to show the **import settings** for the static mesh.
    1.  Scroll to the bottom of the window to the **Fbx File Information** section to see the asset details. Notice that the **Creator Application** appears as **Unity FBX Exporter 5.1.1** and the **File Axis Direction** is **Y-UP**.
        
        ![Scroll down to the Fbx File Information section to see the asset details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/943c18dd-0c25-42e4-97b3-f619beb1c2a6/unity-import-29.png)
    2.  Scroll up to the **Mesh** section and **enable** the **Skeletal Mesh** and **Import Mesh checkboxes**. Click the **Import Content Type** dropdown and select **Geometry and Skinning Weights**.
        
        ![Enable the Skeletal Mesh and Import Mesh checkboxes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b912125-7121-486b-b630-615bbaa57336/unity-import-30.png)
        
        If your Unreal Engine project already contains a skeleton asset that is compatible with the character’s skeleton that you are importing, you can optionally select the compatible skeleton from the **Skeleton** drop-down. However, unless the skeleton assets are identical, you may choose to import the skeletons as their own assets and then define the different skeleton assets as compatible. For more information, see the [Compatible Skeletons](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine#compatibleskeletons) documentation.
        
    3.  If your skeletal mesh was exported with animations, scroll down to the **Animation** section and **enable** the **Import Animations** checkbox. For this example, the skeletal mesh does not contain any animations.
        
        ![If your skeletal mesh has animations, enable the Import Animations checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67f83f17-2635-41a7-9bcd-98a8eeb8cd07/unity-import-31.png)
    4.  Scroll down to the **Material** section, click the **Material Import Method** dropdown and select **Create New Materials**. This will automatically create new materials for the skeletal mesh.
        
        ![Click the Material Import Method dropdown and select Create New Materials](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c7c1ec1-240b-454b-8d53-e179e256d71e/unity-import-17.png)
        
        For more information on the settings available in the FBX Importer, go to the FBX Import Options Reference page. |
        
4.  Click **Import All** to import the skeletal mesh to Unreal Engine.
    
    ![Click Import All](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/165a4e7a-dc6c-4d6b-93d9-2b3d14b9dd1c/unity-import-32.png)
5.  The **skeletal mesh** asset along with the **materials** and **textures** are now imported to Unreal Engine. In addition, a **skeleton** and a **physics asset** are also created based on the skeletal mesh.
    
    ![The skeletal mesh asset is now imported to Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09b29266-8913-4d78-9494-b9afe252c9d5/unity-import-33.png)
6.  **Drag** the **skeletal mesh** asset from the **Content Browser** to the level to see the final result.
    
    ![Drag the skeletal mesh asset to the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0377cf15-74fa-4289-b06e-af53896c1305/unity-import-34.png)

Learn more about the skeletal mesh FBX pipeline by reading the [FBX Skeletal Mesh Pipeline](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine) documentation.

## Animations

![Character animations in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31806c3b-f4cd-47a8-ae7c-74f9d5fa989d/ue5-animation.gif)

You can use Unreal Engine's suite of powerful **animation tools** and **editors** to create **character** and **object runtime animation systems**, **rendered cinematic content**, and author **new animation content** directly in the engine.

Character **animations** in Unreal Engine are built using the [Skeletal Mesh Animation System](/documentation/en-us/unreal-engine/skeletal-mesh-animation-system-in-unreal-engine). Animations are applied to a **skeletal mesh** and are driven by **animation assets**, such as an [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine).

Unreal Engine provides a variety of animation tools to work with Skeletal Meshes to further enhance your animations.

For more information about the Skeletal Mesh Animation system and for information about the suite of Animation [Editors](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine), [Assets, and Features](/documentation/en-us/unreal-engine/animation-assets-and-features-in-unreal-engine) in Unreal Engine, see the [Animating Characters and Objects](/documentation/en-us/unreal-engine/skeletal-mesh-animation-system-in-unreal-engine) documentation.

### Export Animation Clips from Unity

**Animation Clips** from Unity can be exported as .fbx files using the **FBX Exporter** package. These exported files can then be imported into Unreal Engine as **Animation Sequences** to be used in your project.

![Skeletal mesh animation in unity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af2f5778-4190-457f-838f-8c3f40a1cfaf/unity-import-anim-02.gif)

To export an Animation Clip from Unity, follow these steps:

1.  Navigate in your Unity project to the **Hierarchy** panel, and select the character prefab that contains the Animation Clip you want to export.
    
2.  **Right-click** the prefab and select the **Export to FBX…** option.
    
    ![Export animation clips in unity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74a4bddc-6882-4468-a281-3f879955f07e/unity-import-anim-03.png)
3.  Set the **Export Name** and **Export Path** properties to define the name of your exported file and where it will be saved on your computer.
    
    ![Export Name and Export Path properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f719e0f-ddfb-426d-bdf6-953f1a877f5d/unity-import-anim-04.png)
4.  Set the **Export Format** property to **ASCII**, then set the **Include** property to **Model(s) + Animation**. You can optionally decide to include all of the character’s Level Of Detail models (LODs) using the **LOD Level** property and set the **Object(s) Position** property to set a custom transform value.
    
    ![Options settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e856190-1280-48a6-bcad-d0c849f81b55/unity-import-anim-05.png)
    
    Setting the Include property to **Model(s) + Animation** will export the Animation Clip and your characters Model and Skeleton Hierarchy, and store everything in one .fbx file. This can be helpful when importing your assets into Unreal Engine as all of your assets will be saved together.
    
5.  **Enable** the **Animated Skinned Mesh** checkbox, then export the assets using the **Export** button.
    
    ![Enable the Animated Skinned Mesh checkbox and click Export](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30f2af8c-1ad8-486e-9ece-8c43ef2fa95a/unity-import-anim-06.png)

### Import Animations to Unreal Engine

To import an animation from Unity to Unreal Engine, follow these steps:

1.  In the Unreal Engine **Content Browser**, click the **Import** button.
    
    ![unreal engine content browser import button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fa57f7e-0189-47dc-838b-f1dd1a042b5d/unity-import-anim-07.png)
2.  Navigate to the location on your computer that you saved your exported Unity Animation Clip to, select the file, and click the **Open** button.
    
    Alternatively, after using the **Show in Explorer** setting in Unity, you can **drag** the file from the file explorer window directly into the Unreal Engine **Content Browser** to import it.
    
3.  In the **FBX Import Options** window, set the following properties:
    
    1.  **Enable** the **Skeletal Mesh** property.
    2.  If you want to import the Animation Clip and generate a new Skeletal Mesh asset with the Animation Sequence asset, **enable** the **Import Mesh** property. If you only want to import the animation as an Animation Sequence, **disable** this property. For this example, we are only importing an animation and do not want to import the mesh as well, since the skeletal mesh has already been previously imported.
        
        ![Set the correct options in the FBX Import Options window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbf363a0-84d1-494d-bd10-e9fb6d4b2ccb/unity-import-anim-08.png)
        
        If you are importing the mesh, you will also need to **enable** the **Import Animations** checkbox.
        
        ![import animation property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36f07593-0081-49ef-9f9e-c1fe61522298/unity-import-anim-09.png)
    3.  If you are importing a new character, and want to generate a new skeleton asset during the import process, leave the **Skeleton** property **undefined**. If you are importing an animation that you want to use with an existing character skeleton in your project, select the skeleton asset from the asset selection drop-down menu. In this example, the animation is for the Quinn skeletal mesh so the property is defined to use the **SK\_Mannequin** asset.
        
        ![skeleton property unreal engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e591d13-4cb1-4ad1-ba0d-c70a69d5cf76/unity-import-anim-10.png)
        
        If your Unreal Engine project already contains a skeleton asset that is compatible with the character’s skeleton that you are importing, you can optionally define this **Skeleton** property using the compatible skeleton. However, unless the skeleton assets are identical, you may choose to import the skeletons as their own assets and then define the different skeleton assets as compatible. For more information see the [Compatible Skeletons](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine#compatibleskeletons) documentation.
        
    4.  After defining the properties for the FBX Import Option window, click **Import** to import the asset.
        
        When importing skeletal mesh and animation assets using the FBX Import Option window, you can select either the **Import All** or the **Import** button to initiate the import process. The **Import All** will import all associated mesh, skeleton, material and texture assets contained within the .fbx file. This option is best used when trying to import all elements of the character. If you are importing additional animations associated with a character you have already imported, select the **Import** option to only import the individual animation assets.
        

After the import process completes, you can now access your Animation Sequence in the Asset Editor, or by dragging the asset into a level and [playing the project in the editor](/documentation/en-us/unreal-engine/playing-and-simulating-in-unreal-engine).

![animation working in unreal engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aca140bd-5d9f-4828-867e-93892319309c/unity-import-anim-11.gif)

### Skeletal Mesh Import Troubleshooting

You may encounter some issues when importing skeletal mesh characters and objects into Unreal Engine from another digital content creation (DCC) package or game engine. For example, objects may be imported at the incorrect scale or rotation due to differences between the programs and their respective coordinate systems.

Unreal Engine's FBX Import Settings menu can correct some issues during the import process, but if your objects are not importing correctly please reference the following sections for information about how to correct your import errors.

#### Scale

Unreal Engine’s coordinate system is based on a set scale where 1 Unreal Unit is 1 centimeter. Other programs operate using different scales, which, when migrating a file between the two programs, can result in characters or objects that are larger or smaller than they are designed to be. When migrating a file from Unity, which uses 1-meter units, your characters and objects could appear smaller after importing the assets into Unreal Engine.

![scale import error](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d043f79-cb49-40ca-8733-e279a62fe89b/unity-import-anim-13.png)

To fix this issue, navigate in the skeletal mesh editor to the **Asset Details** panel, and use the **Import Uniform Scale** property to set a new value for the mesh. After setting this value, use the **Reimport Base Mesh** button in the editor’s toolbar.

![scale import error fix](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36aad192-a0a8-4f98-a72e-9443351fd468/unity-import-anim-14.png)

#### Rotation

If your character’s skeleton, skeletal mesh, or animation assets are not rotated properly in the viewport, you can fix this issue by opening the asset in its associated editor.

![rotation import error](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c95fa039-9d22-4e42-991f-c0e97f298c1f/unity-import-anim-15.png)

Use the **Asset Details** panel to set a value for the **Import Rotation** property, then use the **Reimport Base Mesh** button in the asset editor’s **toolbar**. After the process is complete, your asset should be correctly rotated in Unreal Engine.

![rotation import error fix](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80c11f1f-a8d7-4eca-958a-2bcd679fbcd9/unity-import-anim-16.png)

Due to the coordinate system differences between Unity and Unreal Engine, a value of **90.0** on the **X-Axis** should correct any rotation issues for your skeletal mesh or Animation Sequence assets.

#### Convert Scene Properties

In the **Asset Details** panel of your asset, you can **enable** the **Convert Scene**, **Force Front Axis**, and **Convert Scene Unity** properties to correct any broken or irregular meshes during playback. After enabling any of these properties, click the **Reimport Base Mesh** button in the asset editor’s toolbar to apply the changes.

![convert scene properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7621433c-cf84-44de-af1b-6644ea4c3007/unity-import-anim-17.png)

#### Simultaneously Editing Multiple Assets

When importing Assets into Unreal Engine, it is possible that multiple assets will need the same correction to a setting, such as the import rotation or import scale. Rather than editing each asset individually, you can use bulk editing to apply the same setting or property value to multiple assets at the same time.

To edit multiple assets at once, use the following steps:

1.  Select each asset you want to edit in the **Content Browser** using **Shift + Click**.
    
2.  **Right-click** the selected assets and select the **Asset Actions** > **Edit Selection in Property Matrix** option in the context menu.
    
    ![bulk edit setting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe320c1d-3187-4a47-8ece-ec89c809992b/unity-import-anim-12.png)
3.  Each asset’s property will now be accessible in the **Asset Details** panel, where you can search or navigate to a specific property to apply a setting to all assets at once.
    

### Animation Blueprints

After importing your skeletal mesh character and its Animation Sequence assets, you can use an **Animation Blueprint** to drive animation playback and logic at runtime. Use these graphs to select animations to be played, blend between animations, and layer animations. For more information about using Animation Blueprints to drive animations in your project, see the [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) documentation.

![animation blueprint graph overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12627361-5591-4aba-9dd9-9beaf27d444a/unity-import-anim-18.png)

## Textures

![A cube with a material that uses a brick texture in Unity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec0031ce-7847-4c34-9f7c-b79de145ac66/unity-import-35.png)

**Textures** are image assets primarily used in Materials and applied to objects. They can also be used directly for other purposes, such as a heads up display (HUD).

Unreal Engine renders textures using [texture streaming](/documentation/en-us/unreal-engine/texture-streaming-overview-for-unreal-engine) to optimize loading textures into the scene. The texture streaming system uses texture **mipmaps**. These are a pre-calculated sequence of images of the same texture at different resolutions.

You can learn more about textures in Unreal Engine by reading the [Textures](/documentation/en-us/unreal-engine/textures-in-unreal-engine) documentation.

### Export a Texture from Unity

Unity keeps texture files saved in their original format inside the project directory, so there is no need to export a texture from Unity. Instead, you can copy the files directly from the project directory.

To find a texture file in Unity’s project directory, follow these steps:

1.  **Right-click** on the texture file inside the **Project** window and click **Show in Explorer**.
    
2.  You can now see the files inside the project directory. You can copy the files directly from here, or use this folder location to find the files from Unreal Engine.
    
    ![You can now see the files inside the project directory](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba8185ff-8213-428f-b46f-93eb629aeb17/unity-import-37.png)

### Import a Texture to Unreal Engine

To import a **texture** to Unreal Engine, follow these steps:

1.  Open **Unreal Engine** and click the **Import** button in the **Content Browser**.
    
    ![Click the Import button in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4bdc595e-7a7b-40e8-af2a-8bb02dd9695e/unity-import-38.png)
2.  Navigate to the **Unity project folder** where the textures are located, **select the texture** files, and click **Open**.
    
    ![Select the texture files and click Open](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/527e2829-7228-4c3f-830e-00c473c47631/unity-import-39.png)
    
    Alternatively, after using the **Show in Explorer** setting in Unity, you can **drag** the files from the file explorer window directly into the Unreal Engine **Content Browser** to import them.
    
3.  The **textures** are now imported to Unreal Engine.
    
    ![The textures are now imported to Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d7204ba-a713-414a-96e5-36409eece7ed/unity-import-40.png)

To learn how to use the textures in a material, see the **Shaders / Materials** section below.

## Shaders / Materials

![A cube with a brick material in Unity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59840293-e43d-43d4-a3af-5b5c19334468/unity-import-41.png)

**Materials** in Unreal Engine define the surface properties of the objects in your scene. In the broadest sense, you can think of a Material as the "paint" that is applied to a mesh to control its visual appearance.

In more technical terms, Materials tell the render engine exactly how a surface should interact with the light in your scene. Materials define every aspect of the surface including color, reflectivity, bumpiness, transparency, and so on. These calculations are done using data that is input to the material from a variety of **images (textures)** and node-based **Material Expressions**, as well as from various [property settings](/documentation/en-us/unreal-engine/unreal-engine-material-properties) inherent to the material itself.

You can learn more about materials in Unreal Engine by reading the [Materials](/documentation/en-us/unreal-engine/unreal-engine-materials) documentation.

### Export a Material from Unity

Unity’s **Shader Graph** is used to build shaders visually. Unity also has **materials**, which can reference a Shader Graph asset and are applied to GameObjects directly.

Unreal Engine’s materials are converted to shaders internally and are built using the [Material Editor](/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide), which also uses a node-based approach to building materials.

A Shader Graph asset cannot be directly exported from Unity and converted to a Material graph in Unreal Engine. However, you can export all relevant **textures** from Unity into Unreal Engine and rebuild the Shader Graph node network inside Unreal Engine’s Material Editor.

This example shows a **Lit Shader Graph** that contains a texture applied to the **base color** and another texture applied as the **normal map**.

![Lit Shader Graph that uses 2 textures](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6cd720a-5549-4e05-91c1-05c7b6c103be/unity-import-42.png)

Export both of those textures from Unity by following the steps described in the **Textures** section of this document.

### Import a Material to Unreal Engine

Since you cannot directly import a material from Unity, you will rebuild the Shader Graph shown above in Unreal Engine’s Material Editor.

Follow these steps to build the material:

1.  Import the textures to Unreal by following the steps described in the **Textures** section of this guide.
    
    ![The textures are now imported to Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/283a7805-dc02-453c-977c-6ab17958fbf6/unity-import-40.png)
2.  Right click in the **Content Browser** and click **Material** to create a new material. Name the asset **M\_Bricks**.
    
    ![Create a new material and name it M_Bricks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1643d738-db9f-4b6d-b969-b428020e6433/unity-import-43.png) ![The material asset is now created](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f58e825-d391-479a-90ae-b6e881b1fa8d/unity-import-44.png)
3.  Double click **M\_Bricks** to open the Material Editor.
    
    ![Double click M_Bricks to open the Material Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65de7439-ea53-4664-aeef-b1676a621776/unity-import-45.png)
4.  Select the **textures** in the **Content Browser** and drag them inside the **Material Editor** to create two **Texture Sample nodes**.
    
    ![Select the textures and drag them inside the Material Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c22f0ece-5994-4f63-b7d8-d5c26b208e96/unity-import-46.png)
5.  Connect the **Texture Sample** node that references the **diffuse** texture to the **Base Color** pin of the material node. Then, connect the **Texture Sample** node that references the **normal map** texture to the **Normal** pin of the material node.
    
    ![Connect the Texture Sample nodes to the Base Color and Normal pins of the material node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5db0cb48-2da0-4d67-b6f0-b64fbf0495b6/unity-import-47.png)
6.  On the material node, enter the values **0.2** for **Specular** and **0.8** for **Roughness**. Click the **Save** button to compile and save the material.
    
    ![On the material node, enter the values 0.2 for Specular and 0.8 for Roughness](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e844b52-a38b-4b54-9542-dfdfcf17e46c/unity-import-48.png)
7.  In the viewport, click **Add + > Shapes > Cube** to add a Cube static mesh to the level.
    
    ![In the viewport click Add + - Shapes - Cube](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/916f30c3-3ba8-4bbf-8f39-2c335952a27e/unity-import-49.png) ![A cube is added to the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fbbb270-1f7c-4593-8706-87c614fbcb3b/unity-import-50.png)
8.  Select **M\_Bricks** in the **Content Browser** and **drag it** to the **cube** static mesh in the level to apply the material.
    
    ![Select M_Bricks and drag it to the cube static mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14919adf-0aba-4195-a63e-9ef17b5ca7a8/unity-import-51.png)

Learn more about the material FBX pipeline by reading the [FBX Material Pipeline](/documentation/en-us/unreal-engine/fbx-material-pipeline-in-unreal-engine) documentation.

## Particle Effects

![Niagara Visual Effects System in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfc0283c-1af5-4b5c-bfe7-33441ff5f4c0/ue-vfx.gif)

Unity’s Visual Effects Graph is used to create GPU particle simulations. The system uses a node-based interface to create the effects and can simulate a large number of particles during gameplay.

The **Niagara VFX System** is Unreal Engine's next-generation VFX system. Niagara offers full control to its users. It is programmable and customizable on every axis and provides advanced tools for debugging, visualization, and performance measurement.

Niagara **Systems** contain one or more **emitters** that can combine to create complex effects. Emitters can spawn **CPU** or **GPU particles** independently and can render their particles as **sprites**, **meshes**, **decals**, **lights**, and **ribbons**. In addition, Niagara Systems have **inheritance**, which means that you can create a master Niagara System and derive several child systems from it.

Advanced users can create **custom modules** directly in the system for complete control over the emitter’s behavior. Niagara also comes with **pre-built templates**, including a full suite of [fluid simulation](/documentation/en-us/unreal-engine/niagara-fluids-in-unreal-engine) examples for **2D** and **3D gasses**, **liquids**, and **shallow water**.

Niagara particles can interact with the environment by using mesh distance fields, collision, and the NeighborGrid3D module that allows for complex particle BOID behavior, such as flocking.

Niagara supports input data from other systems in Unreal Engine such as physics, animations, and Blueprint code. It also supports input data from external sources.

A Unity Visual Effects Graph cannot be directly exported out and imported to Unreal, so you will have to recreate your effects within Niagara. Many effects use materials and textures, which can be exported. To learn how to export textures from Unity, see the **Textures** section of this document.

Learn more about Niagara by reading the [Creating Visual Effects](/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine) documentation.

## Audio

Unity’s audio system can import and play a variety of audio file formats in 3D space. The system can also apply many optional effects at runtime, such as reverb.

The **Unreal Audio Engine** is a robust audio engine that supports a wide variety of features across all platforms supported by Unreal Engine.

The audio engine comes with a multi-platform [audio mixer](/documentation/en-us/unreal-engine/audio-mixer-overview-in-unreal-engine) that enables audio digital signal processing (DSP), procedural synthesis, a customizable submix graph, and a flexible C++ API.

Next-generation features, such as [MetaSounds](/documentation/en-us/unreal-engine/metasounds-in-unreal-engine), [audio modulation](/documentation/en-us/unreal-engine/audio-modulation-in-unreal-engine), [audio analysis](/documentation/en-us/unreal-engine/audio-analysis-and-visualization-in-unreal-engine) and the ability to support custom interactive and [procedural music systems](/documentation/en-us/unreal-engine/creating-procedural-music-with-metasounds) means that there is no need to use audio middleware such as FMOD or Wwise when creating rich, interactive audio for your games.

Learn more about audio in Unreal Engine by reading the [Audio in Unreal Engine 5](/documentation/en-us/unreal-engine/audio-in-unreal-engine-5) documentation.

### Export an Audio File from Unity

Unity keeps audio files saved in their original format inside the project directory, so there is no need to export audio files from Unity. Instead, you can copy the file directly from the project directory.

To find an audio file in Unity’s project directory, follow these steps:

1.  Right click your audio file in the **Project** window and click **Show in Explorer**.
    
2.  You can now see the audio file inside the project directory. You can copy the file directly from here, or use this folder location to find the file from Unreal Engine.
    
    ![You can now see the audio file inside the project directory](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2a4f561-dd92-4ab6-b596-269a7f56ed88/unity-import-53.png)

### Import an Audio file to Unreal Engine

To import an **audio file** to Unreal Engine, follow these steps:

1.  Open **Unreal Engine** and click the **Import** button in the **Content Browser**.
    
    ![Click the Import button in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd21536b-1d3b-4b2f-bb1e-aeba981d509f/unity-import-54.png)
2.  Navigate to the **Unity project folder** where the audio file is located, **select the audio** file and click **Open**.
    
    Alternatively, after using the **Show in Explorer** setting in Unity, you can **drag** the file from the file explorer window directly into the Unreal Engine **Content Browser** to import it.
    
3.  The **audio file** is now imported to Unreal Engine.
    
    ![The audio file** **is now imported to Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/075efd8a-02e5-42b6-8967-33386240cae7/unity-import-56.png)
4.  Right click the **audio file** in the **Content Browser** and click **Create Cue** to create a sound cue asset. This is the standard audio asset in the engine used to play sounds in-game.
    
    ![A Sound Cue is now created in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f15f41e-cb35-48fb-ace9-922b33e383c4/unity-import-58.png)

Learn more about sound cues by reading the [Sound Cues](/documentation/en-us/unreal-engine/sound-cues-in-unreal-engine) documentation. We also recommend you learn about [MetaSounds](/documentation/en-us/unreal-engine/metasounds-in-unreal-engine), as they provide more advanced features compared to Sound Cues.

## Video

![UE5 revealed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f74eb5dc-4a0a-4c00-b0ee-a07525e8cbd5/ue5-revealed.gif)

Unity’s Video Player component attaches video files to GameObjects and provides several options to play video files in the scene.

Unreal Engine comes with a fully-featured [Media Framework](/documentation/en-us/unreal-engine/media-framework-technical-reference-for-unreal-engine) that provides similar functionality. The framework supports a variety of video file formats, comes with playback optimization, and supports audio/video capture hardware on Windows and Android devices.

Learn more about playing a video file in Unreal Engine by reading the [Play a Video File](/documentation/en-us/unreal-engine/play-a-video-file-in-unreal-engine) documentation.

### Export a Video File from Unity

Unity keeps video files saved in their original format inside the project directory, so there is no need to export a video from Unity. Instead, you can copy the file directly from the project directory.

To find the video file in Unity’s project directory, follow these steps:

1.  **Right-click** on the video file inside the **Project** window and click **Show in Explorer**.
    
2.  You can now see the file inside the project directory. You can copy the file directly from here, or use this folder location to find the file from Unreal Engine.
    
    ![You can now see video file inside the project directory](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6db6c6ee-7a3b-4a7d-bed7-0627d3b9b8aa/unity-import-60.png)

### Import a Video File to Unreal Engine

To import a **video file** to Unreal Engine, follow these steps:

1.  Open **Unreal Engine** and click the **Import** button in the **Content Browser**.
    
    ![Click the Import button in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91cd8cb5-15c4-4566-a0c1-7f34e5b724b5/unity-import-61.png)
2.  Navigate to the **Unity project folder** where the video is located, **select the video** file and click **Open**.
    
    Alternatively, after using the **Show in Explorer** setting in Unity, you can **drag** the file from the file explorer window directly into the Unreal Engine **Content Browser** to import it.
    
3.  The **video file** is now imported to Unreal Engine. A **Media Plate actor** is automatically created in the **Content Browser** which can be dragged into the level to play the video file directly.
    
    ![The video file** **is now imported to Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/092a7837-b63d-4ab7-b3fc-515c12e31cfb/unity-import-63.png)
4.  Select the **video file** in the **Content Browser** and drag it into the level.
    
    ![Select the video file** **and drag it into the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa788c0f-1988-4dd7-a639-c74e0158d39e/unity-import-64.png)
5.  With the **Media Plate actor** selected, go to the **Details** panel and scroll down to the **Control** section.
    
    1.  **Enable** the **Play on Open**, **Auto Play**, and **Enable Audio** checkboxes.
    2.  If desired, **enable** the **Loop** checkbox to have the video loop indefinitely.
    
    ![With the Media Plate actor selected, go to the Details panel and set your desired options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12ea4c6a-6175-47ea-a4f8-dbf9298e8d65/unity-import-65.png)
6.  Optionally, you can scroll down to the **Geometry** section and adjust the **geometry** used to display the video (Plane, Sphere, or Custom), the **Aspect Ratio**, and **Letterbox Aspect Ratio**. For this example, we will leave the **Auto Aspect Ratio** checkbox **enabled** so the shape conforms to the video file’s native aspect ratio when playing.
    
    ![You can scroll down to the Geometry section to adjust the geometry used and aspect ratio](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b58dd04-8fd6-4f98-816a-132f52c68b9f/unity-import-66.png)
7.  Click **Simulate** to see the video play inside the level.
    
    ![Click Simulate to see the video play inside the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d718b30c-2906-46d5-898e-31ee5e2dac85/unity-import-67.png) ![The video is playing inside the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b04cfa3-efa0-4b86-b0c0-4359fa936bce/ue-echo.gif)

You can learn more about the **Media Plate actor** by reading the [Media Plate Actor](/documentation/en-us/unreal-engine/the-media-plate-actor-in-unreal-engine) documentation.

## Camera Control and Cinematic Sequences

![A cinematic sequence created in Sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8aa357bc-b763-41fa-8aea-09b6469c15e0/ue-sequencer.gif)

Unity comes with several tools to create cinematic content. The Timeline tool is used to create cinematic sequences in the editor and Cinemachine is a set of tools for controlling the camera.

When used together, these tools provide developers the ability to create dynamic cinematic sequences at runtime.

**Sequencer** is Unreal Engine's multi-track editor used for creating and previewing cinematic sequences in real time.

The editor contains robust cinematic tools that you can use to create animated and cinematic sequences. You can pilot cameras to create level fly-throughs, animate lights, move objects, animate characters, render output sequences, and more.

Camera animations and behaviors created in Timeline and Cinemachine cannot be directly exported from Unity and into Unreal Engine. For this use case, you will have to recreate that behavior by using Sequencer.

Learn more about Sequencer by reading the [Cinematics and Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine) documentation.

## Code and Visual Scripting

![Code comparison between Unity and Unreal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c737f129-c4da-4b22-95fb-1abefc2d3aec/ue-coding.png)

Unity’s default programming language is C#, while Unreal uses [C++](/documentation/en-us/unreal-engine/programming-with-cplusplus-in-unreal-engine) as its native programming language. Unity also has Bolt Visual Scripting, which is similar to Unreal Engine’s [Blueprint Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) language.

Unity C# scripts and Bolt scripting files cannot be directly exported from Unity and imported to Unreal Engine. You will have to build your functionality using C++ or Blueprints.

To learn about common Unreal Engine programming patterns and best practices, read the [Creating Gameplay in Unreal Engine](https://stage.edc-dev.net/documentation/en-us/unreal-engine/creating-gameplay-in-unreal-engine-for-unity-developers) documentation.

## 2D Assets

![sprite paper 2d asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c38d7aec-3542-4554-8419-0143fb489128/unity-import-paper2d-01.gif)

**Paper 2D** is a sprite-based system for creating 2D and 2D/3D hybrid games in Unreal Engine. The Paper 2D system uses texture files mapped to planer game objects to represent 2D characters, objects and backgrounds in your Unreal Engine project.

For more information about Paper 2D, and creating 2D projects in Unreal Engine, see the [Paper 2D](/documentation/en-us/unreal-engine/paper-2d-overview-in-unreal-engine) documentation.

### Export 2D Assets from Unity

To export 2D assets from Unity, following these steps:

1.  **Right-click** the asset in your **Project** window, and select the **Show In Explorer** option to open the asset’s location on your computer.
    
    ![Export a sprite from Unity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81acb4b6-8932-4509-b26d-3c915a8718b3/unity-import-paper2d-02.png)
2.  You can now see the file inside the project directory. You can copy the file directly from here, or use this folder location to find the file from Unreal Engine.
    
    ![unity asset in file explorer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f9af235-ad74-43aa-bebb-45cd8941ff6a/unity-import-paper2d-05.png)

### Import 2D Assets to Unreal Engine

To import a **2D asset** to Unreal Engine, follow these steps:

1.  Open **Unreal Engine** and click the **Import** button in the **Content Browser**.
    
    ![import button unreal engine content browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0599ccb-6061-4956-b23d-cb5039382400/unity-import-paper2d-06.png)
2.  Navigate to the **Unity project folder** where the 2D file is located, select the 2D file and click **Open** to import the asset.
    
    Alternatively, after using the **Show in Explorer** setting in Unity, you can **drag** the file from the file explorer window directly into the Unreal Engine **Content Browser**, to import the file.
    
    ![import sprite to unreal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/655d7d45-fa8f-4860-8d8c-d709365ff6d2/unity-import-paper2d-03.png)
3.  The 2D asset is now imported to Unreal Engine
    
    ![sprite imported in unreal engine content browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/524cf0eb-e023-467d-92aa-d9b9208c8a22/unity-import-paper2d-07.png)
4.  Now that your file is imported, you can use it to create 2D assets or animations using Paper 2D.
    

For information about importing assets, creating Sprites, and Flipbook Animations, see the [Paper 2D](/documentation/en-us/unreal-engine/how-to-import-and-use-paper-2d-sprites-in-unreal-engine#importingsprites) documentation.

## SpeedTree Assets

![SpeedTree foliage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a4f656c-2b15-4f99-bab5-1b56f6afa33b/unity-speedtree.png)

SpeedTree is a suite of products focused on creating foliage for real time and linear content. The product includes a tree modeler and prebuilt assets you can purchase and import directly into Unreal Engine.

Learn more about using SpeedTree in Unreal Engine by reading [Introduction to SpeedTree for Unreal Engine](https://docs.speedtree.com/doku.php?id=ue4_introduction) in the SpeedTree documentation.
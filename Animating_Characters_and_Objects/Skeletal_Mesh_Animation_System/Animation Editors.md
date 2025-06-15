# Animation Editors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:10

---

The **Skeletal Mesh Animation System** in **Unreal Engine** is comprised of specialized animation asset editors that feature robust animation tools that you can use when working with Skeletal Meshes and other **Animation Assets**. With these animation editors, you can create character animations, interactions within the levels, and other procedural behaviors.

This document provides an overview of the specialized animation editors in Unreal.

## Overview

A character's skeletal mesh has many associated assets that can be opened through the **Content Browser**. These assets include a **Skeleton**, **Skeletal Mesh**, **Animation Sequences**, and **Animation Blueprints**. Depending on which asset is opened, the corresponding **Editor Mode** will open.

Here you will find an overview of an Animation Editor window with highlighted features, common across all of the Animation Editor Modes.

![animation editor overview window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4224f282-7e05-4055-97ce-9e8c81aa6c6e/animationeditoroverview.png)

1.  [Toolbar](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine#toolbar)
    
2.  [Viewport](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine#viewport)
    
3.  [Editor Modes](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine#editor%20modes)
    
4.  [Preview Scene Settings](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine#preview%20scene%20settings)
    

## Toolbar

The **Toolbar**, which is found in all of the Animation Editor modes, is similar to the **Toolbar** found across Unreal Engine's many editors and windows. For general Toolbar functions refer to the [Main Toolbar](/documentation/en-us/unreal-engine/unreal-editor-interface#main%20toolbar), and for specific animation editor toolbar features, reference their respective pages for more information.

![animation editor toolbar buttons](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e9e19ad-889d-484d-a9ed-ec672fe407ea/toolbar.png)

The following unique features are common across all of the Animation Editors:

| Name | Icon | Description |
| --- | --- | --- |
| **Preview Mesh** | ![preview mesh icon button toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/165e5407-e7c7-4b9a-9d07-66e06ad43414/previewmeshicon.png) | Set a new preview Skeletal Mesh for the current asset (Stored per-animation or per-skeleton). |
| **Preview Animation** | ![preview animation icon button toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/495e96a0-dd16-4cef-bf8a-adc2c607bc82/previewanimationicon.png) | Select a preview animation for playback with the current asset. |
| **Create Asset** | ![create asset icon button toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6cfd33f2-841d-4a85-875c-624ef84c1916/createasseticon.png) | 
From this drop down menu, the following Animation Assets can be created:

-   [Create Animation](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) creates a new Animation Sequence from either the current default **Reference Pose**, or from the displayed meshes **Current Pose**.
-   [Create Pose Asset](/documentation/en-us/unreal-engine/animation-pose-assets-in-unreal-engine) creates a new Pose Asset from either the **Current Pose** displayed on the mesh, the **Current Animation** description, or the **Insert Pose** Description.
-   [Anim Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) creates a new **Animation Blueprint** for the current Skeletal Mesh.
-   [Anim Composite](/documentation/en-us/unreal-engine/animation-composites-in-unreal-engine) created a new **AnimComposite** using the selected Skeleton.
-   [Anim Montage](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine) creates a new **AnimMontage** using the selected skeleton.
-   [Blend Space](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine) creates a new **Blend Space** used for smoothly blending transitions between animations.
-   [Blend Space 1D](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine#blend%20space%201d) creates a new **1D Blend Space** using the selected Skeleton.
-   [Aim Offset](/documentation/en-us/unreal-engine/aim-offset-in-unreal-engine) creates a new **Aim Offset Blend Space** using the selected skeleton.
-   [Aim Offset 1D](/documentation/en-us/unreal-engine/aim-offset-in-unreal-engine#aim%20offsets%201d) creates a new **Aim Offset 1D Blend Space** using the selected skeleton.



 |

## Viewport

The [Viewport](/documentation/en-us/unreal-engine/editor-viewports-in-unreal-engine) window allows you to preview playback of animation assets on your selected Skeletal Mesh and provides information about your assets. Below you will find highlighted features relevant to the Animation Editors.

![animation viewport window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ab1b186-edd3-446f-9dfc-2b65eaff9c1a/viewportwindow.png)

1.  Viewport Property Settings
    
    Listed below are the viewport properties relevant to the Animation Sequence Editor Viewport.
    
    | Name | Description |
    | --- | --- |
    | **Preview Animation** | Lists the current selected animation sequence. |
    | **LOD (Level of Detail)** | The current displayed LOD or Level of Detail assigned value of the character. |
    | **Current Screen Size** | This is a value that represents how much of the viewport is occupied by the character's bounding box (By default, the bounding box is derived from the Physics Asset, if one is present, and Skeleton Asset if not.). Factors that affect this number are how large the animation's bounding box is (or the displacement in 3D space), how close the character is to the camera, and the amount of zoom applied to the camera. Based on this value you can assign when your LOD should switch between levels. |
    | **Triangles** | Lists the number of triangles rendered that comprise the previewed mesh. |
    | **Vertices** | Lists the number of vertices, or individual coordinate points, that comprise the previewed mesh. |
    | **UV Channels** | Lists the current mesh's [UV Channel](/documentation/en-us/unreal-engine/using-uv-channels-with-static-meshes-in-unreal-engine). |
    | **Approximate Size** | Dimensions of a bounding box containing the current animations displaced space, calculated by one of the animations assets. By default the physics asset will be used, and if no physics asset is present then the Skeleton asset will be referenced. Listed in Unreal Units (Centimeters). |
    | **Frame Rate** | Lists the preview animations frame rate of playback. |
    
2.  Debug Text
    
    Here you the Animation Editor Debug Text can also be seen in the top right of the Viewport. Here you can find important reference information about the animation asset currently being used such as the name of the animation asset, the LOD mode, Current screen Size and display output of mesh properties such as displayed triangles and vertices.
    

## Editor Modes

Each Animation Editor Mode, can be opened with their respective buttons in the top right of your project window:

![animation editor modes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a41d0143-7592-461b-8c55-18c4d382e5eb/animationeditormodes.png)

1.  [Skeleton Editor](/documentation/en-us/unreal-engine/skeleton-editor-in-unreal-engine): This editor is used for working with Skeleton Rigs and provides visual control of bone and joint hierarchy associated with a Skeletal Mesh.
    
2.  [Skeletal Mesh Editor](/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine): The Skeletal Mesh Editor is where you can make edits to meshes, assign **Materials**, adjust **Level of Detail** (LOD), and test [Morph Target](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine#morphtargetpreviewer) functionality.
    
3.  [Animation Sequence Editor](/documentation/en-us/unreal-engine/paper-2d-setting-up-an-animation-state-machine-in-unreal-engine): If the Skeletal Mesh has associated Animation Sequences, you can edit and preview them, including augmentation tools such as, **Blendspaces**, Morph Targets and **Animation Notifies** here.
    
4.  [Animation Blueprint Editor](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine): Similar to Unreal's [Blueprint Editor](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine), The Animation Blueprint editor is a visual scripting environment for directing animation functionality and behaviors within the level. You can access this Mode after an Animation Blueprint asset has been created for your mesh.
    
5.  [Physics Asset Editor](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine): The Physics Asset Editor is a dedicated animation editor you can use to manipulate the Physics Asset assigned to your Skeletal Mesh.
    

After opening a Skeletal Mesh asset for the first time, the Skeletal Mesh Editor will be the default Editor Mode open. By clicking any of the other Editor Modes, a new window tab will open in your current editor window.

### Skeleton Editor

In the Skeleton Editor Mode you will find a hierarchy outline and visual preview of the Bone data found within your Skeleton Mesh. Here you can adjust bone placement, create [Skeleton Sockets](/documentation/en-us/unreal-engine/skeletal-mesh-sockets-in-unreal-engine), and preview [Animation Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine).

### Skeletal Mesh Editor

The Skeletal Mesh Editor Mode is where you can edit visual attributes of Skeletal Meshes. For instance, manipulating the polygonal structures of meshes, editing the associated Materials, and even assigning LODs.

### Animation Sequence Editor

With the Animation Sequencer Editor mode, you can perform animation focused editing, specific to any of your project's animation asset types. Examples include creating and managing **Animation Sequences**, **Animation Notifies**, **Animation Montages**, and more.

## Preview Scene Settings

The **Preview Scene** is the visual preview found in all of Unreal Engine's many project windows. With this window you can quickly see what your asset and animations will look like in different lighting environments and playback scenarios.

![animation editor preview scene settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0805707-d76c-4d77-9ffc-85aff0d2a744/animationeditorpreviewscenesettings.png)

Below are a few features of the Preview Scene Settings window that are unique to the animation editors modes:

| Name | Description |
| --- | --- |
| **Preview Controller** | 
Here you have control over which animation is previewed in the viewport.

-   **Default** will use the Animation tool's default settings. In most cases, this will cause the character to use the reference pose, except when an animation sequence is being viewed.
    
-   **Reference Pose** will use the Skeletal Mesh's Reference Pose.
    
-   **Use Specific Animation** will open an option to select a specific Animation Sequence associated with your skeletal mesh to preview.
    
-   **Live Link Preview Controller** will use preview using Live Link settings.
    

The selected mode will also be displayed on the first line of the **Debug Text** in the viewport.

![viewport debug text window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c22741a-c322-48ff-a1b3-b9a2e33966b0/viewportdebugtextcallout.png)

 |
| **Preview Mesh (Skeleton)** | This property enables you to change the Skeletal Mesh used for previewing purposes. Only found in Skeleton Editor and Animation Editor. |
| **Allow Different Skeletons** | When this property is enabled you can select an additional mesh, even ones not associated with the current skeleton, to preview in the viewport. Only found in Skeleton Editor and Animation Editor. |
| **Allow Custom AnimBP Override** | If using a Preview Collection, you can enable this property to allow an override of custom Animation Blueprints. Only found in Skeleton Editor and Animation Editor |
| **Additional Meshes** | For use in instances of Mesh Collection implementation. View other meshes included in the current Mesh Collection for previewing purposes. Only found in Skeleton Editor and Animation Editor. |
| **Skeletal Meshes** | The Skeletal Mesh assets that are included in the specified **Preview Mesh Collection**. Only found in Skeleton Editor and Animation Editor. |
| **Settings** | General scene lighting and rendering settings. |
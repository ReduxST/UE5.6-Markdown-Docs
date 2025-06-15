# USD Stage Editor Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/usd-stage-editor-quick-start-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/usd-stage-editor-quick-start-in-unreal-engine)  
**Processed:** 2025-06-14 16:57:49

---

Unreal Engine provides support for USD through the USD Stage Actor and the USD Stage workflow. In this Quick Start guide, you will:

-   Creating the USD Stage Actor.
-   Editing properties using the USD Stage Window.
-   Adding new Prims to your USD Stage Actor.
-   Writing data back to your USD file.
-   Accessing USD animations using Sequencer.
-   Importing assets into an Unreal Engine project.

Before you begin, you will need the **USD Importer** plugin enabled in your project. For more information, see [Working with Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine).

### Prerequisite Topics

In order to understand and use the content on this page, make sure you are familiar with the following topic:

-   [Universal Scene Description in Unreal Engine](/documentation/en-us/unreal-engine/universal-scene-description-in-unreal-engine)

This tutorial uses the Kitchen Set USD file from Pixar. Pixar maintains a small library of USD sample files for learning and demonstration. Download the Kitchen Set and other samples [here](https://graphics.pixar.com/usd/release/dl_downloads.html).

## 1\. Creating the USD Stage Actor

Start working with USD content by opening the USD Stage panel.

Click image for full size.

1.  In the Level Editor, from the Top Menu, select **Window > Virtual Production > USD Stage**.
    
2.  From the menu in the **USD Stage Editor** panel, select **File > Open** and navigate to your USD file.
    

The Hierarchy section will populate with the scene hierarchy from your USD file.

The Hierarchy section of the USD Stage window populated with the contents of the Kitchen Set. Click image for full size.

Each USD file you open in Unreal Engine requires its own **USD Stage** Actor that serves as an anchor for your USD data. The process outlined above will automatically add a USD Stage Actor to your Level.

It is also possible to add a USD Stage Actor using the **Place Actors** panel and select an associated USD file for it using the **Root Layer** option in the **Details** panel.

## 2\. Editing Properties Using the USD Stage Window

You can edit the properties of your USD Stage Actor and prims using the Properties section of the USD Stage Editor window.

### Changing the UpAxis of the USD Stage Actor

1.  Select **Stage** at the top of the hierarchy in the USD Stage window. In the Properties section, locate the **upAxis** property and click the dropdown menu. Select the new axis to represent up for your USD data.
    
    Select the axis the best fits your USD data. Click image for full size.
    

### Changing the Variant of a Prim

1.  In the USD Stage Editor, select **Options > Selection** and enable **Synchronize with Editor**. This synchronizes your selection between the Unreal Engine Level and the USD Stage Editor window.
    
    Enable Synchronize with Editor to synchronize your selection between the USD Stage and the Unreal Engine viewport. Click image for full size.
    
2.  In the Hierarchy section, click the dropdown arrow next to **Kitchen\_Set** to expand the group. Expand **Props\_grp** to display the props in the scene.
    
3.  Expand **West\_grp** to display individual prims. Props highlighted in orange indicate that they are **composition arcs**, and you can right-click any of their prims to add references to them (or clear references from them). Other right-click actions include the ability to add or remove prims, and the ability to toggle, load, or unload payloads.
    
    Click image for full size.
    
4.  Expand **DiningTable\_grp** and select **ChairB\_1**. In the Properties section you can edit the following:
    
    | Property | Description |
    | --- | --- |
    | **name** | Displays the name of the selected asset. |
    | **path** | Displays the path of the selected asset. |
    | **kind** | 
    Defines the type of the selected asset.
    
    -   **assembly**: Collection of models.
    -   **component**: Type of model that contains subcomponents.
    -   **group**: Collection of models within an assembly.
    -   **model**: Base type of kind. Assets should not have their kind set to model since it is an abstract commonality used to differentiate components and groups. For more information, see [Model Hierarchy](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-model) in the Pixar USD documentation.
    -   **subcomponent**: Prims inside a component. Not a type of model.
    
    
    
     |
    | **purpose** | 
    
    Sets the initial Purpose to load. Uses a USD Stage Actor and an integer as input.
    
    Options include:
    
    -   default
    -   proxy
    -   render
    -   guide
    
    
    
     |
    | **visibility** | 
    
    Sets the initial Purpose to load. Uses a USD Stage Actor and an integer as input.
    
    Options include:
    
    -   **inherited**: Inherits visibility from its parent
    -   **invisibile**: Prim and any prims included in its subtree are not rendered.
    
    
    
     |
    | **xformOp:rotateZ** | Defines the Z rotation of the selected asset. |
    | **xformOp:translate** | Defines the X, Y, and Z location of the asset. |
    | **xformOpOrder** | Displays the order in which transform operations are applied to the asset. |
    | **modelingVariant** | Defines the current variant being displayed in the scene. It will only be visible if the asset has one or more variants. |
    | **References** | Displays all references attached to this prim. |
    
5.  The chairs in this scene have two variants, **ChairA** and **ChairB**. With **ChairB\_1** selected, locate the **Variants** section of the Properties. Change **modelingVariant** to **ChairA**. This will swap the chair mesh used in the scene with the new variant.
    

## 3\. Adding New Prims to Your USD Stage Actor

Prims are added or removed from the hierarchy using the right-click menu. Once added, their properties can be edited in the Properties section.

### Adding a new chair to the Kitchen Set

1.  Right-click the **DiningTable\_grp** entry in the hierarchy and select **Add Prim** from the menu. Name this new prim **ChairB\_3**.
    
    Adding a new prim to the USD Stage. Click image for full size.
    
2.  Select your new prim in the hierarchy. In the **Details** section, change its **kind** to **component**.
    
    Changing the properties of the new prim. Click image for full size.
    
3.  Reference the chair USD file to bring it into the stage. Right-click **ChairB\_3** in the hierarchy and select **Add Reference**. Navigate to the location of your Kitchen Set files. Open the **assets > Chair** folder and select **Chair.usd**. Click **Open**.
    
4.  Your new prim now references the Chair USD data and displays the **ChairA** variant. It should be located at the Level's origin. Select **ChairB\_3** in the hierarchy and change the modelingVariant to **ChairB**.
    
5.  Click the new chair in the viewport and use the transform tools to place the chair near the table.
    

## 4\. Writing Data Back to Your USD File

Changes made using the USD Stage Actor can be written back to your USD file. From the USD Stage panel, select **File > Save**.

## 5\. Accessing USD Animations Using Sequencer

### Accessing USD Animations

Animations stored within a USD file are accessible from a specifically-generated Level Sequence spawned by the USD Stage Actor.

1.  In the **Outliner**, select **UsdStageActor**. In the **USD** section of the **Details** panel, locate the **Level Sequence**. Double-click the asset to open it in **Sequencer**.
    
    Double click the Level Sequence in the Details panel. Click image for full size.
    

For more information on using Sequencer, see [Cinematics and Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine).

### Animating the Chair

To add animation to the new prim **ChairB\_3** that you created in step three, you will create a new USD file and add it as a layer to the USD Stage Actor.

1.  In the **Layers** section of the USD Stage window, right-click the **kitchen\_set.usd** layer and select **Add New**. Save this new file as **myanim.usda**.
    
    Add a new Layer to your USD data for the animation. Click image for full size.
    
2.  USD layers use a [LIVRPS structure](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-livrpsstrengthordering) to determine how layers affect the final composition of the scene. For animation to affect the kitchen set, the layer containing that animation must be higher in the layer structure than the scene containing the prims. From the Top Menu in the Level Editor, select **Window > Place Actors** to open the panel. Search for **Usd Stage Actor** in the **Place Actors** panel and drag a new copy into your Level.
    
    New USD Actors in the Place Actors panel. Click image for full size.
    
3.  Select the **UsdStageActor** in the **Outliner**. From the USD Stage panel, select **File > Open** and browse to your **myanim.usda** file.
    
4.  Add the kitchen set back into the layer stack by right-clicking the **myanim.usda** layer and selecting the **Add Existing** option. In the File window, navigate to your **kitchen\_set.usd** file and click **Open**.
    
5.  Before adding the animation, the USD Stage needs to know how long the animation will be. Click the **Stage** prim in the hierarchy. In the Properties section, change the **endTimeCode** and **endFrame** values to **48**.
    
    Change the endTimeCode and endFrame properties. Click image for full size.
    
6.  Select your new USD Stage Actor in the **Outliner**. From the **Details** panel, scroll down to the USD section and locate **Level Sequence**. Double-click the asset to open it in **Sequencer**.
    
7.  In the Sequencer panel, click the **\+ Track** button and select the Actor you want to animate from the **Actor to Sequencer** submenu.
    
    Add a new Track group for the selected Actor. Click image for full size.
    
8.  Click the **Add (+)** button on the new track and create a new **Transform** track.
    
    Add a new Transform track. Click image for full size.
    
9.  Animate the chair rotating in place. For more information on using Tracks in Sequencer, see [Tracks](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine).
    
10.  Write the data back to USD using **File > Save** in the USD Stage window.
    

## 6\. Importing Assets into an Unreal Engine Project

Actors displayed on the USD Stage Actor can be imported into the Unreal Editor's Content Browser through any of the following import options.

-   Using **File > Import Into Level**. This process will import both assets (static mesh, skeletal mesh, materials, textures, and so on) and Actors.
-   Using the **Add/Import** button in the **Content Browser**. This process will only import assets.
-   Dragging and dropping the file into the **Content Browser**. This process will only import assets.
-   Using the **Action > Import** option in the USD Stage Editor window. This process will import everything on the USD Stage Actor and works with both assets and Actors. After the import process is complete, assets on the USD Stage are replaced with new Actors from the **Content Browser**.

### Importing the Kitchen Set into Unreal Engine

1.  With the Kitchen Set open in the USD Stage window, open the **Actions** menu and select **Import**.
    
2.  Select the location to store the imported assets. In this example, importing the Kitchen Set will create a folder named **Kitchen\_set** in the selected location. Materials and static meshes are saved into separate subfolders.
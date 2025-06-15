# Groom Simulation and Rendering Quick Start Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hair-simulation-and-rendering-quick-start-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/hair-simulation-and-rendering-quick-start-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:27:08

---

The focus of this quick start guide is to walk you through the basics of working with your hair grooms on skinned meshes in Unreal Engine.

After going through this tutorial, you will know how to:

-   Set up a project for hair rendering and simulation.
-   Set up a groom for use with an animated skeletal mesh.
-   Set up a basic *Hair* material.
-   Enable and control physics for hair.

## Required Setup

1.  Create a new project using using the [Third Person template](/documentation/en-us/unreal-engine/working-with-projects-and-templates-in-unreal-engine).
2.  In the editor, go to the **Main Menu** and select **Edit > Project Settings** to open the Project Settings window. Under the **Rendering > Optimization** category, enable the **Support Compute Skin Cache** option.
    
    ![Enable Support Compute Skin Cache in Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69729734-8c19-4802-ae48-d58f3cf50990/01-hair-project-settings.png)
    
    You can ignore the **Restart Now** popup that appears in the bottom right of the editor window since the next steps also require you to restart the editor.
    
3.  Go to the Main Menu again and this time select **Edit > Plugins** to open the Plugins browser window.
    
    ![Enabling Groom Plugins](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09c99b8b-8a9f-4fff-8749-2f418cb3e510/02-enabling-groom-plugins.png)
    
    In the search bar start typing `groom` and enable the following plugins:
    
    -   **Alembic Groom Importer**
    -   **Groom**
4.  Restart the editor for changes to the Project Settings and Plugins to take effect.
    
    ![Restarting the Unreal Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8407ef39-87dd-4485-b28c-1a7210a32f39/03-restarting-the-editor.png)

## Creating and Importing your Groom

Grooms for a character — even a simple one — can contain different types of hair, such as that for heads, beards, brows, and more. Each of these types of hair could have its own Material and physics settings. There are also types of hair within each group, such as hairs that are to be used during simulation. This information can be defined during grooming in your DCC application, and Unreal Engine looks at this information to define guides.

1.  In your preferred DCC application, create your Groom and then export it to Alembic `.abc` file format.
    
    Use the [Alembic for Grooms Specification](/documentation/en-us/unreal-engine/using-alembic-for-grooms-in-unreal-engine) to prepare your groom for Unreal Engine with proper naming conventions.
    
2.  In the Content Drawer, click the **Import** button to import your Alembic file with your groom, or drag and drop your Alembic file into the Content Browser.
    
    ![From your Content Drawer, click Import](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8253320-48a8-4f92-897d-91948141786d/04-click-the-import-button.png)
3.  In the **Groom Import Options** window, consider the following options:
    
    ![The Groom Import Options Window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd2bff02-fdc3-47a0-9631-39e1172bc0c5/05-groom-import-options-window.png)
    -   Modify the initial Rotation that is baked into the groom, which avoids some extra runtime cost.
    -   Use the Override Guides check box to replace the imported guides with a set of strands selected from the imported strands. The amount of guides depends on the Hair to Guide Density value.
    -   Use the Interpolation Quality and Interpolation Distance to modify how the pairing between guides and the strands is handled for transferring the guide motion.
    -   The Randomize Guide and Unique Guide checkboxes affect how a guide influences a strand is handled; whether only a single or multiple guides should influence a strand.
4.  Click **Import**.
    

During the import process, the Groom system looks for attributes and groups that follow the Alembic naming conventions outlined in the [Alembic for Grooms](/documentation/en-us/unreal-engine/using-alembic-for-grooms-in-unreal-engine) specifications page, and imports them to a new Groom Asset. Among these attributes, the RootUV attribute fetches the UV of the underlying surface, such as a skin surface, which allows for the creation of some spatial variation across the groom.

## Attaching a Groom to a Skeletal Mesh

The Groom component enables you to attach a Groom Asset and bind a groom to a Skeletal Mesh's surface. An optional Binding Asset caches the projected data of the groom onto the Skeletal Mesh, which saves GPU costs of doing this at startup when one is not created and assigned.

### Setting up the Groom Component

For this part of the guide, we'll use the `SKM_Manny` found in the **Third Person** template. If you do not have this, you can add it to your project from the Content Browser by clicking **Add New** > **Add Feature or Content Pack**, and selecting the **Third Person** template.

Also, note that this same setup can be applied inside of a character Blueprint.

1.  In the **Content Browser**, locate the **SKM\_Manny** Skeletal Mesh found in the **Characters > Mannequins > Meshes** folder and drag it into the scene.  
    ![Drag the SKM_Manny into the Scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff4397a5-d4cd-4cf2-aa89-f0a8b7bf7a9e/06-dragging-the-mannequin-into-the-scene.png)
    
2.  With the Skeletal Mesh selected, use the **Details** panel to click the **Add Component** button and add a **Groom** Component.  
    ![Adding the Groom Component to the Skeletal Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67372a4f-4203-4278-8a49-7da1076eb1fc/07-adding-the-groom-component.png)
    
3.  Select the **Groom** component and use the **Groom Asset** slot to assign your imported groom to this Skeletal Mesh.
    
    ![Assigning a Groom Asset to the Skeletal Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ece6085-d320-407e-942d-a45da35951ae/08-assigning-groom-asset.png)

### Creating a Binding Asset

1.  In your Content Drawer, locate your Groom Asset. Right-click it and select **Create Binding**.
    
    ![Create a Binding Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dcd93955-ad6d-464a-8bd1-b94007e11f0b/09-creating-binding-asset.png)
2.  The **Groom Binding Options** window will open. To create the asset, it's required that you assign a **Target Skeletal Mesh** and you can optionally specify a **Source Skeletal Mesh** that shares similar topology as the Target Skeletal Mesh. With these slots assigned, click **Create**.
    
    ![Assigning a Target Skeletal Mesh for the Groom Binding Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2f7f45f-0005-4cc7-a2c6-1737772a1f0a/10-assigning-target-skeletal-mesh.png)
3.  This will open your Groom Binding Asset. Save it and close the window.
    
    ![Groom Binding Asset Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d02f87f2-3082-4ee5-8ec9-0f9474c2f7c8/11-groom-binding-asset-details.png)
4.  Select the Skeletal Mesh in your level. Use the **Details** panel to select the **Groom** Component in the Components panel. Under the **Groom** section, use the **Binding Asset** slot to assign the Binding Asset you created.
    
    ![Assigning a Binding Asset to the Skeletal Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5cdf9ec1-d149-460c-9a33-3da64d9e317d/12-assigning-binding-asset.png)

## Setting Up Your Hair Material

By Default, Unreal Engine contains a simple Hair Material with `HairDefaultMaterial`.

The steps below are optional for this guide since Unreal Engine includes a default hair material. However, if you've not set one up before, the steps below will guide you through the properties and setting required to do so.

1.  In the Content Drawer, click the **Add** button and select **Material**.
    
    ![Create new Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec103300-ebfa-4d62-b34e-7ae4a3fec147/13-add-new-material.png)
2.  Give your Material Asset a name and open it.
    
3.  In the Material Editor, use the **Details** panel to set the following:
    
    ![Select Hair for the Shading Model Property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ebc7c896-7ced-43a4-b6b1-7560ddad4e0e/14-set-shading-model-to-hair.png)
    -   Shading Model: **Hair**
        
        You also need to enable **Use with Hair Strands**. When the material is applied to a groom component, this checkbox should automatically enable itself and recompile the material. If it doesn't, you can enable it from the **Usage** category of the Details panel in the Material Editor.
        
4.  In the Material Graph, use the following node setup for a basic *hair* material:
    
    ![Basic Hair Material Node Setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54fbda79-9410-4fb7-af77-84ff48801c45/15-basic-hair-material-setup.png)
    
    Use a **Constant4Vector** for the Base Color and a **Constant** to control the Roughness.
    
    If you're setting up more complex hair materials, use the **HairAttribute** expression in the Material Graph to access the hair attributes such as UV, Dimensions, RootUV, and Seed.
    
5.  **Save and close** the Material Editor.
6.  You can apply your hair material in one of two ways; directly on the Groom Asset component through its Details panel in the Level or Blueprint, or by opening the Groom Asset from the Content Browser. Assign your hair material to the **Material** element slot.  
    ![Applying the hair Material through the Details Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4062cea-42c3-45ac-a797-a0509a5f5f06/16-apply-material-in-details-panel.png)
    
    Groom Asset Actor (Details panel)
    
      
    ![Applying the hair Material in the Groom Asset Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abcfab6e-a938-4a36-8101-695d02c932b1/17-apply-material-in-groom-asset-editor.png)
    
    Groom Asset (Groom Asset Editor)
    

## Setting Up Hair Physics

In this step, you'll enable physics simulation for your Groom Asset.

1.  In your Conent Drawer, locate your Groom Asset and open it in the **Groom Asset Editor**.
    
2.  Go to the **Physics** tab and check the box next to the **Enable Simulation** option.
    
    ![Enabling Simulation from the Physics window in the Groom Asset Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84854879-8d6b-41ea-a25e-fdecc06d1455/18-enabling-groom-simulation.png)

Once enabled, the properties in the **Physics** tab can be used to control the physics properties of the hair.

See the [Enabling Physics Simulation on Grooms](/documentation/en-us/unreal-engine/enabling-physics-simulation-on-grooms-in-unreal-engine) page for more information on these Groom Asset properties.

Once enabled, you should see physics applied to the hair while working in the editor and when using play-in-editor (PIE) or simulate-in-editor modes.
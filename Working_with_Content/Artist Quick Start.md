# Artist Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/artist-quick-start-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/artist-quick-start-in-unreal-engine)  
**Processed:** 2025-06-14 16:08:04

---

Operating System

×Windows

3D Art Tool

×Autodesk Maya

Select an option from the dropdown to see content relevant to it.

[![Materials Header](https://dev.epicgames.com/community/api/documentation/image/713a4888-70a7-4d53-98cb-c06fb6539dfa?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/713a4888-70a7-4d53-98cb-c06fb6539dfa?resizing_type=fit)

Click image for full size.

This quick start guide shows you how to add assets to your **Unreal Engine (UE5)** games. By the end of this guide, you'll know how to use the **Project Browser** to create new projects and navigate the **Content Browser** to find and add content. You'll also know where to find information on the **FBX Content Pipeline** while learning how to use the **Material Editor** to modify **Materials** before applying them to a **Static Mesh Actor**.

## 1\. Required Project Setup

1.  Open **Unreal Engine** from the Launcher.
    
2.  Create a new Project using the **Games > Blank** template using the following settings:
    
    -   **C++** enabled
        
    -   **With Starter Content** enabled
        
3.  You'll need to enter a project name, so use **Artist\_QuickStart**.
    
4.  You can now click **Create Project** and get started.
    

The **Unreal Editor** now opens your new project. **Visual Studio** also opens and loads the solution file your project created.

## 2\. Creating Folders

It's always good practice to keep your project's content organized. The first thing you're going to learn is how to create a folder that will store your imported content.

  

Before you get started: Download Quick Start Assets from the following link.

-   [Sample Assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/7ba2327f-a20d-4f14-af5a-23617888fb2e/quickstartsampleassets.zip)
    

1.  Extract the downloaded assets to a location on your computer.  
    
    [![](https://dev.epicgames.com/community/api/documentation/image/46c21a9e-691c-4591-97e0-d86396d2fb79?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/46c21a9e-691c-4591-97e0-d86396d2fb79?resizing_type=fit)
    
    Click image for full size.
    
2.  From the **Content Browser** inside the Editor, click the **Add New** button.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/6e470953-a5fb-4326-9167-a033dde0aa5f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6e470953-a5fb-4326-9167-a033dde0aa5f?resizing_type=fit)
    
    Click image for full size.
    
3.  Select **New Folder** to create a new folder.  
    
    [![](https://dev.epicgames.com/community/api/documentation/image/f6f6ac45-c7f7-4d46-9928-266e7e29aedb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f6f6ac45-c7f7-4d46-9928-266e7e29aedb?resizing_type=fit)
    
    Click image for full size.
    
4.  Name the folder **QuickStartContent.**
    
    [![](https://dev.epicgames.com/community/api/documentation/image/5c11c0ac-1d97-4719-98fc-836c605fb26c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5c11c0ac-1d97-4719-98fc-836c605fb26c?resizing_type=fit)
    
    Click image for full size.
    
5.  Double-click the **QuickStartContent** folder.
    

*Naming conventions matter! Be consistent when naming folders and files.*

## 3\. Importing Meshes

There are a few ways to add content to your UE5 project; however, we'll focus on the Content Browser's **Import** functionality.

1.  Now that you're inside the **QuickStartContent** folder, click the Content Browser's **Import** button to open a file dialog box.  
    
    [![](https://dev.epicgames.com/community/api/documentation/image/f3bc1a11-a06e-43c8-8578-700e44bcf139?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f3bc1a11-a06e-43c8-8578-700e44bcf139?resizing_type=fit)
    
    Click image for full size.
    
2.  Locate and select the **Basic\_Asset1** and **Basic\_Asset2** FBX mesh files.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/3d3accfb-efae-4fc0-b294-bbfc975781c4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3d3accfb-efae-4fc0-b294-bbfc975781c4?resizing_type=fit)
    
    Click image for full size.
    
3.  Click **Open** to begin importing the FBX mesh files to your project.
    
4.  Inside the editor, the **FBX Import Options** dialog box appears. Clicking **Import** or **Import All** adds your meshes to the Project.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/cf8472cf-1246-439b-a05c-09b0c84e1032?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cf8472cf-1246-439b-a05c-09b0c84e1032?resizing_type=fit)
    
    Click image for full size.
    
5.  Click **Save All** to save your imported meshes.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/4de352cc-d520-41a5-b6ac-928d87f88f81?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4de352cc-d520-41a5-b6ac-928d87f88f81?resizing_type=fit)
    
    Click image for full size.
    
6.  A **Save Content** dialog box appears. Click **Save Selected** to save your imported assets.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/79a030d5-f179-409a-b926-df588077abf1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/79a030d5-f179-409a-b926-df588077abf1?resizing_type=fit)
    
    Click image for full size.
    
7.  Navigate to the **QuickStartContent** folder, then verify UE5 created the corresponding **.uasset files**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/e9e2a86d-f562-4dc3-9434-47f568381e5c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e9e2a86d-f562-4dc3-9434-47f568381e5c?resizing_type=fit)
    
    Click image for full size.
    

*Organize your assets so that you can easily find them.*

## 4\. Importing Textures

1.  Navigate to the **QuickStartContent** folder in the Editor, then click the Content Browser's **Import** button to open a file dialog box.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/68a6f950-1cd3-4be7-841b-94bc61567ffe?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/68a6f950-1cd3-4be7-841b-94bc61567ffe?resizing_type=fit)
    
    Click image for full size.
    
2.  Locate and select the **T\_Rock\_04\_D** and **T\_Rock\_04\_n** Targa (TGA) image files.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/ad478237-5bc8-458b-ba65-8755c3224300?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ad478237-5bc8-458b-ba65-8755c3224300?resizing_type=fit)
    
    Click image for full size.
    
3.  Click **Open** to begin importing the TGA image files to your project.
    
4.  A confirmation box appears in the lower right corner of the Unreal Editor.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/0819795e-1751-413f-8fb9-d9290d88fbd1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0819795e-1751-413f-8fb9-d9290d88fbd1?resizing_type=fit)
    
    Click image for full size.
    
5.  Click **OK** to accept the **T\_Rock\_04\_n.TGA** normal map's settings.
    
6.  Click **Save All** to save your imported images.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/18c788b2-944b-4e48-8a12-883df1de645d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/18c788b2-944b-4e48-8a12-883df1de645d?resizing_type=fit)
    
    Click image for full size.
    
7.  A **Save Content** dialog box appears.
    
8.  Click **Save Selected** to save your imported assets.
    
9.  Navigate to the **QuickStartContent** folder, then verify UE5 created the corresponding **.uasset files**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/e540856e-7398-4af0-8692-1f86079f8884?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e540856e-7398-4af0-8692-1f86079f8884?resizing_type=fit)
    
    Click image for full size.
    

[Fab](https://www.fab.com/) *(also accessible from the **Epic Launcher**) is a great place to find and share content.*

## 5\. Preparing Meshes for Import

If you have your own meshes to import, this section is for you.

The UE5 FBX import pipeline uses **FBX 2018**. Using a different version during export may result in incompatibilities.

1.  Select the mesh(es) to be exported in the viewport.
    
    [![Maya Export](https://dev.epicgames.com/community/api/documentation/image/687ebb46-af4d-4f3e-b373-0df667b10bbf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/687ebb46-af4d-4f3e-b373-0df667b10bbf?resizing_type=fit)
    
    Click image for full size.
    
2.  In the **File** menu, choose **Export Selection** (or **Export All** if you want to export everything in the scene regardless of selection).
    
    [![Maya Export](https://dev.epicgames.com/community/api/documentation/image/d9668f1a-3fee-4ae9-b48f-754b58714282?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d9668f1a-3fee-4ae9-b48f-754b58714282?resizing_type=fit)
    
    Click image for full size.
    
3.  In the **Export** dialog box:
    
    -   Choose the **Content** folder inside your UE5 Project (1)
        
    -   Enter a name for the file and set it to FBX Export (2)
        
    -   Set your Export Options (3)
        
    -   Click **Export All** (4)
        
        [![Maya Export](https://dev.epicgames.com/community/api/documentation/image/db7b6d6e-51a1-4297-8973-05dd824d9591?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/db7b6d6e-51a1-4297-8973-05dd824d9591?resizing_type=fit)
        
        Click image for full size.
        
    
    *The settings in the Geometry category above are the most basic requirements for exporting **Static Meshes** to Unreal Engine 5.*
    
    *You can use the default options for importing. Refer to [FBX Import Options Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) for more information on each option.*
    
4.  Your asset has now been imported and you can drag-and-drop it from the **Content Browser** into your level.
    
    [![Asset into your Level](https://dev.epicgames.com/community/api/documentation/image/3d8ab278-b9eb-4e4b-aa02-3921e33b6849?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3d8ab278-b9eb-4e4b-aa02-3921e33b6849?resizing_type=fit)
    
    Click image for full size.
    
    *In the example above (as part of our Import Options), we imported **Materials** and **Textures**.*
    

Well done! You've learned how to prepare meshes for import into UE5.

✓ [Click here if you want to learn more about the FBX content pipeline.](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-content-pipeline).

*Clean modeling improves a game's performance.*

## 6\. Creating Materials

**Materials** are assets applied to meshes, contributing to a scene's visual aesthetic. There are a few ways to create and edit materials for your UE5 project; however, we'll focus on using the **Material Editor**.

1.  Navigating to your **Content Browser**, click **Add New** and select **Material**.
    
    [![New Create Material](https://dev.epicgames.com/community/api/documentation/image/635f6975-697f-468d-bb72-a8b1d8ae189d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/635f6975-697f-468d-bb72-a8b1d8ae189d?resizing_type=fit)
    
    Click image for full size.
    
2.  Name your material **Rock**.
    
    [![Material Naming](https://dev.epicgames.com/community/api/documentation/image/c48d76c6-102a-400b-b220-39223dd8b4d6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c48d76c6-102a-400b-b220-39223dd8b4d6?resizing_type=fit)
    
    Click image for full size.
    
3.  Your **Rock Material** is now ready to be used.
    
    [![New Rock Material](https://dev.epicgames.com/community/api/documentation/image/6900c1b1-5dd2-4f46-83c5-2ebe589a2f61?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6900c1b1-5dd2-4f46-83c5-2ebe589a2f61?resizing_type=fit)
    
    Click image for full size.
    
4.  Double-clicking the **Rock Material** will open the [Material Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide).
    
    [![Material Editor](https://dev.epicgames.com/community/api/documentation/image/f4d7596e-e48b-4a52-a0ee-1978d0c3d07b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f4d7596e-e48b-4a52-a0ee-1978d0c3d07b?resizing_type=fit)
    
    Click image for full size.
    
    Read our [Material - How-to](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials-tutorials) documentation if you want to learn more about working with material nodes.
    

*Size your textures using powers of two.*

## 7\. Editing Materials

At this point, you should have created a new material and opened the **Material Editor**.

[![Material Editor](https://dev.epicgames.com/community/api/documentation/image/e14abe35-e001-4065-a699-ef70a39a11d1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e14abe35-e001-4065-a699-ef70a39a11d1?resizing_type=fit)

Click image for full size.

You can define a material's color, shininess, transparency, and much more in the [Material Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide). You're now ready to edit the **Rock Material** you created.

1.  Select the **Main Material Node** in the center of the **Material Graph**. The **Material Editor** will highlight the node for you when you select it.
    
    [![Main Material Node](https://dev.epicgames.com/community/api/documentation/image/03495866-43be-4869-b429-e748263b4931?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/03495866-43be-4869-b429-e748263b4931?resizing_type=fit)
    
    Click image for full size.
    
    *It is the only node in the graph (named after your material).*
    
2.  Inside the **Details** panel, change the **Shading Model** from **Default Lit** to **Subsurface**.
    
    [![Select Subsurface](https://dev.epicgames.com/community/api/documentation/image/926a3397-e4f0-47ac-989a-67395540aec3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/926a3397-e4f0-47ac-989a-67395540aec3?resizing_type=fit)
    
    Click image for full size.
    
3.  The **Subsurface Shading Model** enables two more pins in the **Main Material Node**: **Opacity** and **Subsurface Color**.
    
    [![New More Pins](https://dev.epicgames.com/community/api/documentation/image/5e847a59-8b95-422f-b3c5-d2660f50f871?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5e847a59-8b95-422f-b3c5-d2660f50f871?resizing_type=fit)
    
    Click image for full size.
    
4.  Get your textures into the Graph. Hold the **T** key and left-click inside the Editor's Graph area. A **Texture Sample Node** should appear inside the graph.
    
    [![Texture Sample](https://dev.epicgames.com/community/api/documentation/image/7d17a80e-44de-437d-b89a-a4a5df07125d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7d17a80e-44de-437d-b89a-a4a5df07125d?resizing_type=fit)
    
    Click image for full size.
    
5.  You'll want at least 2 textures. Repeat Step 4 until your graph looks like the image below.
    
    [![New Texture Sample Nodes](https://dev.epicgames.com/community/api/documentation/image/a8bb136a-0e3e-4131-99ed-c31df0386389?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a8bb136a-0e3e-4131-99ed-c31df0386389?resizing_type=fit)
    
    Click image for full size.
    
6.  Select one of the **Texture Sample Nodes** and locate the **Details Panel** under the **Material Expression Texture Base** category.
    
    [![Material Expression Texture Base](https://dev.epicgames.com/community/api/documentation/image/499e66b7-4d5e-41bf-a90f-b4ec5f4f43e3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/499e66b7-4d5e-41bf-a90f-b4ec5f4f43e3?resizing_type=fit)
    
    Click image for full size.
    
    Under the texture property, left-click the pull down menu labeled **None** and select the color texture named **T\_Rock\_04\_D**.
    
    *You can also use the search field to locate the texture asset by entering **T\_Rock\_04\_D** in the search field.*
    
7.  Repeat Step 6 for the other **Texture Sample Node**, making sure to select the normal map texture named **T\_Rock\_04\_n**.
    
    [![New Both Textures Selected](https://dev.epicgames.com/community/api/documentation/image/88eb915c-a750-466b-b08c-7de06d0328d6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/88eb915c-a750-466b-b08c-7de06d0328d6?resizing_type=fit)
    
    Click image for full size.
    
    *The Material Graph should resemble the image pictured above.*
    
8.  Connect the **T\_Rock\_04\_D** Texture Sample's **Color pin (white)** to the Rock Material's **Base Color pin**.
    
    [![New Connect Color Pin](https://dev.epicgames.com/community/api/documentation/image/4416f60b-ccad-404a-a8ee-ea587c0e4c21?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4416f60b-ccad-404a-a8ee-ea587c0e4c21?resizing_type=fit)
    
    Click image for full size.
    
    *The newly connected **white pin** contains the texture's color channels.*
    
9.  Connect the **T\_Rock\_04\_n** Texture Sample's **Normal pin (white)** to the Rock Material's **Normal pin**.
    
    [![New Connect Normal Pin](https://dev.epicgames.com/community/api/documentation/image/5bd3f0bb-77d0-4e4c-9c34-2da051386b5e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5bd3f0bb-77d0-4e4c-9c34-2da051386b5e?resizing_type=fit)
    
    Click image for full size.
    
    *The newly connected **white pin** contains information for the texture's normal map*.
    
10.  The **Preview** should look similar to the image pictured below.
    
    [![New Preview DN](https://dev.epicgames.com/community/api/documentation/image/368eaa44-5863-4fe3-8941-0a55eb5bd971?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/368eaa44-5863-4fe3-8941-0a55eb5bd971?resizing_type=fit)
    
    Click image for full size.
    
11.  Hold the **1** key and left-click in the **Graph Panel** to create three (**3**) **Constant** nodes.
    
    [![Constants](https://dev.epicgames.com/community/api/documentation/image/1e37744a-92fe-4e7c-b272-e67150549521?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1e37744a-92fe-4e7c-b272-e67150549521?resizing_type=fit)
    
    Click image for full size.
    
    *The **Constant Node** is a modifiable scalar float variable.*
    
12.  Hold the **3** key and left-click in the Graph Panel to create one (**1**) **Constant3Vector**.
    
    [![Constant 3](https://dev.epicgames.com/community/api/documentation/image/5a77b930-72fd-4f1c-a07d-22bc40da76d9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5a77b930-72fd-4f1c-a07d-22bc40da76d9?resizing_type=fit)
    
    Click image for full size.
    
    *The **Constant3Vector** node is a modifiable vector corresponding to color without an alpha channel.*
    
    Read our [Constant Expression](https://dev.epicgames.com/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine) documentation if you want to learn more about working with constant expressions.
    
13.  Your nodes should be arranged so that connections can be easily made without wires crossing or sliding beneath each other.
    
    [![New Mat Constants Added](https://dev.epicgames.com/community/api/documentation/image/88df501c-b06c-413e-9ced-5d71dbc30c93?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/88df501c-b06c-413e-9ced-5d71dbc30c93?resizing_type=fit)
    
    Click image for full size.
    
14.  Connect all of the **Constant** and **Constant3Vector** nodes to corresponding pins in the **Rock Material Main Node**.
    
    [![New All Nodes Connected NoVal](https://dev.epicgames.com/community/api/documentation/image/fcab4173-51a2-4189-bfa2-b04cdb13bac3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fcab4173-51a2-4189-bfa2-b04cdb13bac3?resizing_type=fit)
    
    Click image for full size.
    
15.  Change the values of each **Constant** and **Constant3Vector** by updating their **Value** parameter in the **Details** panel.
    
    -   **Specular Value** = 0.0
        
    -   **Roughness Value** = 0.8
        
    -   **Opacity Value** = 0.95
        
    -   **Subsurface Color** = Red(1,0,0)
        
        [![New All Connected All Adjusted](https://dev.epicgames.com/community/api/documentation/image/a314aa40-235e-4791-9ae5-773abd2da678?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a314aa40-235e-4791-9ae5-773abd2da678?resizing_type=fit)
        
        Click image for full size.
        
16.  The **Preview** should look similar to the image pictured below.
    
    [![New Preview All](https://dev.epicgames.com/community/api/documentation/image/0c79e864-a609-46d6-a7de-3beb84304743?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0c79e864-a609-46d6-a7de-3beb84304743?resizing_type=fit)
    
    Click image for full size.
    
    Make sure to save your material before exiting the **Material Editor**.
    

You're almost done! You've just used the **Material Editor** to edit your **Rock Material**.

*A list of all Material Editor Keyboard Shortcuts can be found by going to **Edit Menu > Editor Preferences > Keyboard Shortcuts > "Material Editor" and "Material Editor-Spawn Nodes"** categories.*

## 8\. Applying Materials to Static Mesh Actors

You're now ready to bring things together!

The objective of this step is to apply our **Material** to the Static Mesh we imported. Specifically, you'll learn how to:

-   [Set an Actor's default Material](https://dev.epicgames.com/documentation/en-us/unreal-engine/artist-quick-start-in-unreal-engine)
    
-   [Change Materials used by an Actor](https://dev.epicgames.com/documentation/en-us/unreal-engine/artist-quick-start-in-unreal-engine)
    

### Setting an Actor's Default Material

This section will show you how to set a **Static Mesh Actor's** default material. The default material will be used whenever an **Actor** is placed in the level.

1.  Inside the **Content Browser**, double-click the asset you imported earlier in this guide.
    
    [![New Browser Conten Asset](https://dev.epicgames.com/community/api/documentation/image/a121fc28-e076-4234-b531-f710c781fccf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a121fc28-e076-4234-b531-f710c781fccf?resizing_type=fit)
    
    Click image for full size.
    
    The [Static Mesh Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/static-mesh-editor-ui-in-unreal-engine) will load your asset for editing.
    
    [![Static Mesh Editor](https://dev.epicgames.com/community/api/documentation/image/f73f7417-786b-41e1-b1d5-e2823eb4f8a3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f73f7417-786b-41e1-b1d5-e2823eb4f8a3?resizing_type=fit)
    
    Click image for full size.
    
2.  Inside the **Details** panel under **LOD0**, left-click the material's drop-down menu.
    
    [![LOD 0](https://dev.epicgames.com/community/api/documentation/image/59ad046d-d8fe-43f5-8e95-864e5ae461b5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/59ad046d-d8fe-43f5-8e95-864e5ae461b5?resizing_type=fit)
    
    Click image for full size.0
    
3.  Select the **Rock Material** you created earlier. The material should be available in the selection window.
    
    [![Select Rock Material](https://dev.epicgames.com/community/api/documentation/image/d306ef10-2e48-4b8d-bc57-65b0248ab660?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d306ef10-2e48-4b8d-bc57-65b0248ab660?resizing_type=fit)
    
    Click image for full size.
    
    Your **Preview Pane** will update to reflect the newly applied material.
    
    [![New Default Material](https://dev.epicgames.com/community/api/documentation/image/c06aa877-b853-4af3-b627-5a26d9df7fbf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c06aa877-b853-4af3-b627-5a26d9df7fbf?resizing_type=fit)
    
    Click image for full size.
    
4.  Clicking the **Save** button first, close the **Material Editor**.
    
5.  Inside the **Content Browser**, drag-and-drop the newly textured **Static Mesh Actor** into your level.
    
    [![New Material In Level](https://dev.epicgames.com/community/api/documentation/image/5e1176b9-2090-4a16-a548-0b11b017381a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5e1176b9-2090-4a16-a548-0b11b017381a?resizing_type=fit)
    
    Click image for full size.
    
    *The specified **Material** will be used anytime you place this asset in the level.*
    

### Changing Material Used by an Actor

When we placed a **Static Mesh** object in our level, we created an instance of our object (an [Actor](https://dev.epicgames.com/documentation/en-us/unreal-engine/actors-and-geometry-in-unreal-engine)). For every instance of that **Actor**, we're able to specify its **Material**.

Here's how you change a **Static Mesh Actor's** Material.

1.  Select your **Static Mesh Actor**.
    
    [![New Statis Mesh Selected](https://dev.epicgames.com/community/api/documentation/image/39750ad4-98a2-4e47-915f-6d5bba387c06?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/39750ad4-98a2-4e47-915f-6d5bba387c06?resizing_type=fit)
    
    Click image for full size.
    
2.  Inside the **Details** panel, locate the **Materials** section and click the **Materials** dropdown menu.
    
    [![Material DropDown](https://dev.epicgames.com/community/api/documentation/image/52cc5e33-f351-423e-b760-195bdc2c1e6c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/52cc5e33-f351-423e-b760-195bdc2c1e6c?resizing_type=fit)
    
    Click image for full size.
    
3.  Inside the pop-up menu, select a different Material.
    
    [![Select Tutorial Asset Material](https://dev.epicgames.com/community/api/documentation/image/ccc54d06-d3d9-45e8-8cb1-d8137c1ee9e0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ccc54d06-d3d9-45e8-8cb1-d8137c1ee9e0?resizing_type=fit)
    
    Click image for full size.
    
4.  Alternatively, drag-and-drop a new Material onto the **Static Mesh Actor**.
    
    [![New Material Drop](https://dev.epicgames.com/community/api/documentation/image/c399522a-37d1-4b6d-a636-77caaa68d2bf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c399522a-37d1-4b6d-a636-77caaa68d2bf?resizing_type=fit)
    
    Click image for full size.
    

You've just applied materials to your Static Mesh Actors by:

-   Setting your Actor's Default Material
    
-   Changing Material used by your Actor
    

We've now reached the end of the Artist Quick Start Guide. By now, you should have the skills needed to:

✓ Set-up a Project  
✓ Create Materials  
✓ Edit Materials  
✓ Apply Materials to a Static Mesh Actor

Are you ready to do some exercises on your own?

## 9\. On your own!

Using what you know, create a new **Material** similar to this graph:

[![Plastic Material Network](https://dev.epicgames.com/community/api/documentation/image/299118da-c3ac-4719-a3f4-1ae1b11a99ad?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/299118da-c3ac-4719-a3f4-1ae1b11a99ad?resizing_type=fit)

Click image for full size.

The Main Material node settings simulate a plastic material.

Add **Basic\_Asset1** to the level, apply the Material to it, and update the Material to apply a "Brick" Normal Map Texture.

[![Normal Map Added](https://dev.epicgames.com/community/api/documentation/image/595a4282-8538-4dc8-8e01-3267979bef40?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/595a4282-8538-4dc8-8e01-3267979bef40?resizing_type=fit)

Click image for full size.

For information on importing different types of content, refer to:

-   Information on the FBX pipeline (in general): [FBX Content Pipeline](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-content-pipeline).
    
-   Information on the FBX Skeletal Mesh pipeline: [FBX Skeletal Mesh Pipeline](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine).
    
-   Information on the FBX Animation pipeline: [FBX Animation Pipeline](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-animation-pipeline-in-unreal-engine).
    
-   Information on the FBX Morph Target pipeline: [FBX Morph Target Pipeline](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-morph-target-pipeline-in-unreal-engine).
    
-   Information on the FBX Material pipeline: [FBX Material Pipeline](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-material-pipeline-in-unreal-engine).
    
-   Information on Importing Audio: [Audio Files](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-audio-files).
    

For specifics covered in this Quick Start Guide, refer to:

-   Information on Supported Image Types: [Texture Import Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/textures-in-unreal-engine).
    
-   Information on Materials: [Materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials).
    
-   Information on the Content Browser: [Content Browser](https://dev.epicgames.com/documentation/en-us/unreal-engine/content-browser-in-unreal-engine).
    
-   Information on the Static Mesh Editor: [Static Mesh Editor UI](https://dev.epicgames.com/documentation/en-us/unreal-engine/static-mesh-editor-ui-in-unreal-engine).
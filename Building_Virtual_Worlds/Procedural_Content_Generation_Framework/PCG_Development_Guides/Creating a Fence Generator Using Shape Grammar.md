# Creating a Fence Generator Using Shape Grammar

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-fence-generator-using-shape-grammar-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-fence-generator-using-shape-grammar-in-unreal-engine)  
**Processed:** 2025-06-14 16:16:50

---

A common use case for [Shape Grammar](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-shape-grammar-with-pcg-in-unreal-engine) in Unreal Engine's [Procedural Content Generation Framework](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-overview) is building systems. In this example, you will create a fence generator that spawns several static meshes along a spline using grammar and changes the meshes when the spline control points are altered.

This sample uses the [Privacy Fence Pack (with damaged sections)](https://www.fab.com/listings/71f4143b-a429-4c8b-9ae6-8e03609cbaf4) pack available for free on the Fab store. However, this example could be made using any static meshes of your choice.

## Prerequisites

This how to guide uses terms and concepts discussed in the following documentation:

-   [Procedural Content Generation Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-overview)
    
-   [Using Shape Grammar With PCG](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-shape-grammar-with-pcg-in-unreal-engine)
    

## Project Setup

1.  [Create a new Project](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine) in Unreal Engine.
    
2.  [Create a new Level](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-levels-in-unreal-engine) using the Basic level template. Save your Level.
    
3.  Open **Edit > Plugins** and confirm the following plugins are active:
    
    1.  **Procedural Content Generation Framework (PCG)**
        
    2.  **Procedural Content Generation Framework (PCG) Geometry Script Interop**
        

[![Activate the Plugins](https://dev.epicgames.com/community/api/documentation/image/e81eb8fc-6c0a-4bda-ac0a-8750884c5762?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e81eb8fc-6c0a-4bda-ac0a-8750884c5762?resizing_type=fit)

## Create the Spline

The PCG graph connects to a PCG component and a spline which are contained with a new blueprint class. Create the blueprint class by following the steps below:

1.  Create a new blueprint class by right clicking in the **Content Drawer** or **Content Browser** and selecting **Blueprint Class**.
    
2.  Name your new blueprint class **FenceSpline**.
    
3.  In the **Components** tab, add a utility **Spline** and a **PCG** component.
    
4.  Save your blueprint class.
    

[![Create the FenceSpline Blueprint Class](https://dev.epicgames.com/community/api/documentation/image/e30fb9e2-726c-4807-96fe-df06c744e99e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e30fb9e2-726c-4807-96fe-df06c744e99e?resizing_type=fit)

## PCG Graph Asset

The **PCG Graph** is the foundation of the fence generator and contains the instructions that are used to generate the fence sections along the spline. Create a new PCG graph asset by following the steps below:

1.  Right click in the **Content Drawer** or **Content Browser**, navigate to **PCG**, and select **PCG Graph**.
    
    [![Create a New PCG Graph](https://dev.epicgames.com/community/api/documentation/image/947965aa-d283-4b56-bf20-7102e8a80588?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/947965aa-d283-4b56-bf20-7102e8a80588?resizing_type=fit)
    
2.  Name the new asset **PCG\_FenceGen** and press **Enter**.
    
3.  Double-click **PCG\_FenceGen** to open the PCG Graph Editor.
    

## Create the PCG Grammar

The grammar is stored in a graph parameter as a string. Storing the value in a parameter makes it possible to use **Parameter Overrides** to customize each instance of the fence generator in the level. The **Grammar** attribute is then added to the spline data and passed to a **Subdivide Spline** node to assigned points along the spline.

1.  In the **PCG Graph Editor** window, add a **Get Spline Data** node to the graph.
    
2.  Open the **Graph Settings** by clicking the button at the top of the screen and create a new **Parameter**. Name the new parameter **Grammar** and change its type to **String**.
    
    [![Set Grammar to String](https://dev.epicgames.com/community/api/documentation/image/ec30c0fc-3a00-458b-971d-a730bc3e7199?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ec30c0fc-3a00-458b-971d-a730bc3e7199?resizing_type=fit)
    
3.  Set the initial value of **Grammar** to `A*`. This will tell the graph to place an initial static mesh and then fill the rest of the spline in with static meshes as long as there is room.
    
4.  Drag from the output of **Get Spline Data** and create an **Add Attribute** node. In the Details panel, change the **Output Target** to `Grammar`.
    
5.  Create a Get node for the **Grammar** parameter and connect it to the **Attributes** input on **Add Attribute**.
    
    [![Add the Add Attribute node](https://dev.epicgames.com/community/api/documentation/image/d8648254-43db-434a-84dc-1db40c1b2cff?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d8648254-43db-434a-84dc-1db40c1b2cff?resizing_type=fit)
    
6.  Click the checkbox for **Accept Incomplete Subdivision**.
    
7.  Click the checkbox for **Grammar as Attribute** and set **Grammar Attribute** to `Grammar`.
    
    [![Add Subdivide Spline node](https://dev.epicgames.com/community/api/documentation/image/30e68aa4-7c15-4c9c-a46b-182ad7eef49a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/30e68aa4-7c15-4c9c-a46b-182ad7eef49a?resizing_type=fit)
    

## Assign Meshes to the Grammar

Each symbol in the grammar needs to be assigned a static mesh to spawn. This is done by using two parameters: **Module Info** and **Mesh Info**. Module Info contains an array of symbols. Mesh Info contains an array of static meshes. This information is passed to the **Subdivide Spline** node later as an attribute set.

1.  Select the **Subdivide Spline** node and click the checkbox for **Module Info as Input**. This adds an input for an attribute that can be used to assign module information to your grammar symbols.
    
2.  Create a new parameter in the Graph Settings and name it Module Info. Change the type to **PCG Subdivision Submodule** and click the dropdown menu next to the type and select **Array**. This will hold our symbol information.
    
    [![Set Module Info to an Array](https://dev.epicgames.com/community/api/documentation/image/56ee07af-5893-47fb-bb8c-df170babfd54?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/56ee07af-5893-47fb-bb8c-df170babfd54?resizing_type=fit)
    
3.  Click the **+** button to add a new array element and click the arrow next to **Index \[0\]** to open the entry.
    
4.  Set the value of **Symbol** to `A` and click the checkbox next to the **Scalable** option.
    
5.  Create a new parameter in the Graph Settings and name it **Mesh Info**. Change the type to **Static Mesh** and click the dropdown menu next to the type and select **Array**. This will hold our static mesh information.
    
    [![Create Mesh Info](https://dev.epicgames.com/community/api/documentation/image/0c03220a-3e56-4fb6-8651-0065ac4eea64?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0c03220a-3e56-4fb6-8651-0065ac4eea64?resizing_type=fit)
    
6.  Click the **+** button to add a new array element to Mesh Info.
    
7.  Open the dropdown menu next to **Index \[0\]** and select the **Fence\_17\_DE** static mesh.
    

## Create the Extract Info Subgraph

The subdivision process assigns each module a size and places a pivot point in the middle of the bounds. This creates a problem if the mesh changes later or does not have its pivot in the middle of the mesh. This subgraph extracts the size information directly from the selected mesh’s bounds and adjusts its pivot point to be at the center.

### Setup the Input Node

1.  In the **Content Drawer** or **Content Browser**, create a new **PCG Graph** and name it **PCG\_ExtractInfo**.
    
2.  Click on the **Input** node and open the **Pins** option in the Details panel. **Open Index \[0\]** and change the **Label** to `Mesh Info`.
    
3.  Change the **Allowed Types** option to **Point or Param**.
    
4.  Change the **Pin Status** option to **Normal**.
    
5.  Set the **Tooltip** to `List of meshes to extract info from`.
    
    [![Input Node Settings](https://dev.epicgames.com/community/api/documentation/image/98a88a8c-320c-4abc-8eb7-5c3f6bf788f3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/98a88a8c-320c-4abc-8eb7-5c3f6bf788f3?resizing_type=fit)
    

### Extract the Mesh Bounds

1.  Open the **Graph Settings** and create a new parameter. Name it **Mesh Attribute Name** and set the type to **Name**. Set the initial value to `Mesh`.
    
2.  Drag from the output of the **Input** node and create an **Attribute Rename** node.
    
3.  In the Details panel, set the **New Attribute Name** to `Mesh`.
    
4.  Create a **Get Mesh Attribute Name** node and connect it to the **Attribute to Rename** input on the **Attribute Rename** node.
    
5.  Drag from the **Attribute Rename** node and create a new **Bounds From Mesh** node.
    
6.  Click the new node and set the Mesh Attribute value to `Mesh`.
    
    [![Add Attribute Rename node and settings](https://dev.epicgames.com/community/api/documentation/image/5cfcdfc8-a325-4702-b10e-41b91f96f846?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5cfcdfc8-a325-4702-b10e-41b91f96f846?resizing_type=fit)
    
7.  Drag from the output of **Attribute Rename** and connect it to the **Attribute** input on the **Bounds From Mesh** node. The graph will automatically create a filter to create the appropriate input.
    
8.  Hold the **ALT** key and click the output of the new filter node to break its connection.
    
9.  Drag off the disconnected filter node and create an **Attribute Set To Point** node. Connect the output of that node to the input on **Bounds From Mesh**. Doing this gives the graph the ability to support both point and attribute set data types.
    
10.  Click the Bounds From Mesh node and set the value of the **Mesh Attribute** option to `Mesh`.
    
    [![Graph structure processes both point and attribute set data](https://dev.epicgames.com/community/api/documentation/image/bbcc04f8-de23-4938-9fa1-7efca270cad6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bbcc04f8-de23-4938-9fa1-7efca270cad6?resizing_type=fit)
    

### Adjust the Pivot Point

1.  The pivot point on the static mesh needs to be adjusted to display correctly on the spline, drag from **Bounds From Mesh** and create a **Multiply** node.
    
2.  Click on the new node and set the value of **Input Source 1** to `$Extents.X` This will extract the X extents from the bounds data.
    
3.  Drag off from the **In B** input and create a **Create Attribute** node. Change the **Double Value** to `2.0`.
    
4.  Click back on the **Multiply** node and change the **Output Target** value to `Size`. This will output the full X value multiplied by two and store it in an attribute called Size.
    
    [![Add Multiply node and settings](https://dev.epicgames.com/community/api/documentation/image/11d9ff99-610f-4329-9517-3af0efc41c4c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/11d9ff99-610f-4329-9517-3af0efc41c4c?resizing_type=fit)
    
5.  Drag off from the **Multiply** node and create a **Copy Attributes** node. Drag off the **Multiply** output again and connect it to the **Source** input on the new node. This node extracts the Z extents from the bounds data and saves it to an attribute to help with future scaling, if needed.
    
6.  Click on **Copy Attributes** and set the **Input Source** to `$Extents.Z`.
    
7.  Set the **Output Target** to `ExtentsZ`.
    
    [![The Copy Attributes node](https://dev.epicgames.com/community/api/documentation/image/d32d77ba-9049-4564-a2a1-44bba9794a68?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d32d77ba-9049-4564-a2a1-44bba9794a68?resizing_type=fit)
    
8.  Drag from the output on **Copy Attributes** and create another **Multiply** node. This node will help move the pivot of the mesh to the center.
    
9.  Drag off from the **In B** input and create a **Create Attribute** node. Change the **Double Value** to `-1.0`.
    
10.  Click back to the **Multiply** node. In the Details panel, set the value of **Input Source 1** to `$LocalCenter`.
    
11.  Set the value of **Output Target** to `PivotOffset`.
    
    [![Add a second Multiply node](https://dev.epicgames.com/community/api/documentation/image/c02b2ed4-965f-4fd4-bc66-f963bab010f7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c02b2ed4-965f-4fd4-bc66-f963bab010f7?resizing_type=fit)
    

### Setup the Output Node

1.  Click on the **Output** node and position it at the end of the graph.
    
2.  Open the **Pins** option in the Details panel. **Open Index \[0\]** and change the **Allowed Types** to **Attribute Set**.
    
3.  Change the **Pin Status** option to **Normal**.
    
    [![Output node settings](https://dev.epicgames.com/community/api/documentation/image/5fbe197d-6f26-40a8-8666-b1a38e2426af?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5fbe197d-6f26-40a8-8666-b1a38e2426af?resizing_type=fit)
    
4.  Drag from the output on the **Multiply** node and create a new **Point to Attribute** Set node.
    
5.  Connect the output of the new node to the **Out** pin on the **Output** node.
    
    [![Convert the point data to an attribute set](https://dev.epicgames.com/community/api/documentation/image/5fa2c64b-e40e-4174-b853-dffcd0268609?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5fa2c64b-e40e-4174-b853-dffcd0268609?resizing_type=fit)
    
6.  Save the completed graph.
    
    [![The complete subgraph](https://dev.epicgames.com/community/api/documentation/image/0435eda5-59ce-47e0-a5ba-522160de9ea6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0435eda5-59ce-47e0-a5ba-522160de9ea6?resizing_type=fit)
    
7.  Return to the **PCG\_FenceGen** graph editor window. Drag and drop your **PCG\_ExtractInfo** graph asset from the **Content Drawer** or **Content Browser** into the viewport and select **Create PCG\_ExtractInfo Subgraph Node**.
    
    [![Create the Subgraph node](https://dev.epicgames.com/community/api/documentation/image/463677bd-b7c0-4d93-90df-8e30190ddc7e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/463677bd-b7c0-4d93-90df-8e30190ddc7e?resizing_type=fit)
    

## Apply the Module and Mesh Information

1.  Back in the **PCG\_FenceGen** graph, create an **Add Attribute** node and position it near the **Subdivide Spline** node.
    
2.  Create a **Get Module Info** node and connect it to the **In** on **Add Attribute**.
    
3.  Create a **Get Mesh Info** node and connect it to the **Attributes** input on **Add Attribute**.
    
4.  Connect the **Out** from **Add Attribute** to the **Mesh Info** input on your **PCG\_ExtractInfo** subgraph node.
    
5.  Connect the output from the subgraph node to the **Modules Info** input on the **Subdivide Spline** node.
    
    [![Connect the Module and Mesh data](https://dev.epicgames.com/community/api/documentation/image/5b2c847c-74ce-4fc5-b878-d0c2c6f2b3f2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5b2c847c-74ce-4fc5-b878-d0c2c6f2b3f2?resizing_type=fit)
    
6.  Drag from the output of the **Subdivide Spline** node and create a **Match and Set Attributes** node. Connect the output of the subgraph node to its **Match Data** input. This node takes in the point data and grammar from the **Subdivide Spline** and matches it with the **Module Info** and **Mesh Info** from those parameters.
    
7.  Click on the Match and Set Attributes node and set the following options:
    
    1.  Click the checkbox next to **Match Attributes**.
        
    2.  Set the value of the **Input Attribute** and the **Match Attribute** to `Symbol`.
        
    
    [![The Match And Set Attributes node](https://dev.epicgames.com/community/api/documentation/image/fbf79549-7239-4cc4-94a8-1868ef5e2ed5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fbf79549-7239-4cc4-94a8-1868ef5e2ed5?resizing_type=fit)
    

## Apply the Pivot Offset Transform

1.  Drag from the output of **Match and Set Attribute** to create a **Multiply** node.This node scales the pivot of each mesh using data from the **PCG\_ExtractInfo** subgraph.
    
2.  Drag from the output of **Match and Set Attribute** and connect it to the **In B** input on the **Multiply** node.
    
3.  Click on the **Multiply** node. Set the **Input Source 1** value to `PivotOffset` and the **Input Source 2** value to `$Scale`.
    
    [![Scale the Pivot with the Multiply node](https://dev.epicgames.com/community/api/documentation/image/b38e82e4-226a-4350-99ed-c86dae244e12?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b38e82e4-226a-4350-99ed-c86dae244e12?resizing_type=fit)
    
4.  Drag from the **Multiply** and create a **Vector: Transform Direction** node. This node will rotate the pivot to match the points on the spline.
    
5.  Drag from the output of **Multiply** and connect it to the **Transform** input on the **Vector: Transform Direction** node.
    
6.  Click on the new node and set the **Operation** to **Transform Direction**.
    
7.  Set the **Input Source 1** value to `PivotOffset` and the **Input Source 2** value to `$Transform`.
    
    [![Rotate the pivot with Tranform Direction](https://dev.epicgames.com/community/api/documentation/image/cb5dcda7-b08c-4bda-aab2-3804eb970bcb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cb5dcda7-b08c-4bda-aab2-3804eb970bcb?resizing_type=fit)
    
8.  Drag from **Vector: Transform Direction** and create a new **Add** node. This node adds the final pivot offset to the position of the pivot on the mesh.
    
9.  Drag from the output of **Vector: Transform Direction** and connect it to the **In B** input on the **Add** node.
    
10.  Set the **Input Source 1** value to `$Position` and the **Input Source 2** value to `PivotOffset`.
    
    [![Apply the offset with the Add node](https://dev.epicgames.com/community/api/documentation/image/764d6080-754e-4dc4-bfde-f348627a0be1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/764d6080-754e-4dc4-bfde-f348627a0be1?resizing_type=fit)
    

## Spawn The Static Meshes

1.  Drag from the output of the **Add** node and create a new **Static Mesh Spawner**. This node spawns the static meshes along the spline.
    
2.  In the Details panel, set the **Mesh Selector Type** to **PCGMeshSelectorByAttribute**.
    
3.  Set the **Attribute Name** value to `Mesh`.
    
4.  Save the graph.
    
    [![Connect the Static Mesh Spawner](https://dev.epicgames.com/community/api/documentation/image/79fa5659-1b54-4a28-aac5-01cc342224fb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/79fa5659-1b54-4a28-aac5-01cc342224fb?resizing_type=fit)
    
5.  Click the **FenceSpline** actor in the level. In the Details panel, select the **PCG** component and use the dropdown menu to set the **Graph** option to **PCG\_FenceGen**.
    
    [![Connect the PCG Graph to the PCG component](https://dev.epicgames.com/community/api/documentation/image/1fd242a2-07cd-4f31-a86d-aed2ed573c92?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1fd242a2-07cd-4f31-a86d-aed2ed573c92?resizing_type=fit)
    

## Result

You should see a line of fence static meshes spawning along the length of the spline.

[![The complete Fence Generator](https://dev.epicgames.com/community/api/documentation/image/bfe4ef4e-0afa-4294-8ff7-e4901cd521c7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bfe4ef4e-0afa-4294-8ff7-e4901cd521c7?resizing_type=fit)

You can add additional variety to the static meshes by adding symbols to your grammar, defining them in your Modules Info, and assigning them static meshes in your Meshes Info. You can do this in the graph itself or on a per-instance basis using **Parameter Overrides**.

[![Parameter Overrides work on a per instance basis](https://dev.epicgames.com/community/api/documentation/image/a1373e3c-af42-4165-8096-9d85514c4913?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a1373e3c-af42-4165-8096-9d85514c4913?resizing_type=fit)

In the example below, the fence line has the following extra features:

-   Posts using the symbol `P`.
    
-   A gate using the symbol `G`.
    
-   Large broken sections using the symbol `BL`.
    
-   Small broken sections using the symbol `BS`.
    

The grammar has been updated to `{[A,P]:2,[BL,P]:1,[BS,P]:1}*,[G,P], {[A,P]:2,[BL,P]:1,[BS,P]:1}*`.

[![The updated grammar generates a more interesting result](https://dev.epicgames.com/community/api/documentation/image/d8913ffe-8403-43ca-a7b0-c6980fc06ccd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d8913ffe-8403-43ca-a7b0-c6980fc06ccd?resizing_type=fit)
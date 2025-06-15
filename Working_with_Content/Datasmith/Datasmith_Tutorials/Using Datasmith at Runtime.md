# Using Datasmith at Runtime

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-at-runtime-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-at-runtime-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:39

---

## What is Datasmith Runtime?

**Datasmith Runtime** is a collection of Datasmith features that are available at runtime (as opposed to an in-editor workflow) in an Unreal Engine-based application. You can use these features to create applications that can import `.udatasmith` files and manipulate them using Blueprints.

![Collab Viewer Direct Link](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7eaa5f5c-b05b-44fa-bf3e-fdb12a05611c/collabviewer_directlink.png "Direct Link in the Collab Viewer Template")

Datasmith Direct Link is accessible in a cooked Unreal Engine-based application using Datasmith Runtime and Blueprints.

With Datasmith Runtime, you can create custom applications that take advantage of [Datasmith Direct Link](/documentation/en-us/unreal-engine/using-datasmith-direct-link-in-unreal-engine) or visualize Datasmith data on demand as part of an iterative 3D workflow.

Enable the following plugins in your project to work with Datasmith Runtime:

-   Datasmith Content
-   Datasmith Importer
-   Datasmith Runtime

Datasmith Runtime is officially supported in Unreal Engine 4 and Unreal Engine 5 using Windows and MacOS. While Datasmith Runtime will work with Linux, this is experimental and you may experience instability and performance issues.

## Using Datasmith Runtime with Blueprints

Datasmith Runtime exposes a variety of Datasmith features and import options using several Blueprint nodes. Listed below are the most common:

![Runtime Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b82b1d1-7589-4490-83cf-9ab01dfcb423/5-0-010-datasmith-nodes.png "The most common Datasmith Runtime Blueprint nodes")

The most common Datasmith Runtime Blueprint nodes.

### Make Datasmith Runtime Import Options

Exposes several import parameters and converts them to a data structure:

![Make Datasmith Runtime Import Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f25f68a6-b0d8-492e-b4d4-b624cdbfc048/5-0-020-datasmith-runtime-options-node.png "The Make Datasmith Runtime Import Options node")

| **Inputs** | **Description** |
| --- | --- |
| **Build Hierarchy** | 
Determines whether the hierarchy of Actors is built. Choosing a more detailed hierarchy increases loading and rendering time.

-   **None**: Imports the source content with the hierarchy stored in the Datasmith Runtime Actor. Your content will not be represented in the World Outliner.
-   **Simplified**: Imports the source content while minimizing the number of Actors created. Allows exposing objects so the application can modify their properties, while limiting the number of draw calls due to the high number of Actors in the scene.
-   **Unfiltered**: Imports the source content with full hierarchy.



 |
| **Build Collision** | 

Determines the type of collision used for components.

-   **No Collision**: Does not have any representation in the physics engine. Provides the best possible performance.
-   **Query Only (No Physical Collision)**: Uses only spatial queries. Useful for objects that do not need physical simulation such as pawn navigation. Improves performance.
-   **Physics Only (No Query Collision)**: Uses only physics simulation. Useful for objects that do not need spatial queries. Improves performance.
-   **Collision Enabled (Query and Physics)**: Uses both spatial queries and physics simulation.



 |
| **Collision Type** | 

Determines the type of collision used for Static Meshes.

-   **Project Default**: Uses the project's physics settings.
-   **Simple and Complex**: Uses both simple and complex shapes. Simple shapes are used for regular scene queries and collisions. Complex (per-poly) shapes are used for complex scene queries.
-   **Use Simple Collision as Complex**: Uses only simple shapes for all scene queries and collision tests.
-   **Use Complex Collision as Simple**: Uses complex (per-poly) shapes for all scene queries and collision tests. Can be used for simulation in static shapes only. Might be necessary if precise collision is needed while navigating a scene.



 |
| **Import Metadata** | Reads and imports metadata for Actors. Increases load time. |

The **Tesselation Options** input is currently not used.

### Set Import Options

Sets the value of the selected import options for Datasmith content using a **Datasmith Runtime Actor**. Uses a Datasmith Runtime Actor as the **Target** and **Datasmith Runtime Import Options** as its value.

![Set Import Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80f604b3-a2fa-4226-b415-9446630335a1/5-0-030-datasmith-import-options-node.png "The Set Import Options node")

### Load File

Loads the `.udatasmith` file located at the specified file path. Requires a **File Path** and **Datasmith Runtime Actor** as inputs.

![Load File](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c9e2331-5602-4fa1-a490-33d52d596bda/5-0-040-datasmith-load-file-node.png "The Load File node")

### Load File from Explorer

Opens a File Browser window so you can browse to a location and select a `.udatasmith` file. Requires a **Datasmith Runtime Actor** as input. A **Default File Path** is optional.

![Load File from Explorer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a4b30b2-b2c0-4d0b-bf10-cab1590f47be/5-0-050-datasmith-load-file-from-explorer-node.png "The Load File from Explorer")

Though it works with both Windows and Mac operating systems in Play In Editor (PIE), Load File from Explorer works only with Windows at runtime.

### Get Direct Link Proxy

Returns an interface to a **Direct Link** connection called a Direct Link Proxy. This is the first step in creating a **Datasmith Direct Link** connection.

![Get Direct Link Proxy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23a8a360-073c-4b78-b493-d737a1e5f0b1/5-0-060-datasmith-get-direct-link-proxy-node.png "The Get Direct Link Proxy node")

### Get List of Sources

Gets a list of Datasmith Direct Link Sources. Requires a **Direct Link Proxy** as input.

![Direct Link Get List of Sources](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b4cf727-866b-496e-a12a-6ff765922542/5-0-070-datasmith-get-list-of-sources-node.png "The Get List of Sources node")

### Open Connection with Index

Opens a Direct Link connection with the source located at the specified index value. Requires a **Datasmith Runtime Actor** and a **Source Index** as input.

![Open Connection with Index](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a624389d-e3c7-42c4-adc6-4078ad20cf2b/5-0-080-datasmith-open-connection-with-index-node.png "The Open Connection with Index node")

### Close Connection

Closes an open Direct Link connection associated with a specified **Datasmith Runtime Actor**.

![Close Connection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ac7d500-5979-4687-aa84-7b0b844dc321/5-0-090-datasmith-close-connection-node.png "The Close Connection node")

## Loading Datasmith Content at Runtime

Using Datasmith Runtime, you can load Datasmith content inside a cooked application while having access to the hierarchy and Actor properties.

Click for full image.

To load Datasmith content using Blueprints:

1.  Create a new **Actor Blueprint** to contain the anchor point for the Datasmith content. You can do this by right-clicking in the **Content Browser** and selecting **Blueprint Class** from the context menu. In the **Pick Parent Class** window, select **Actor** and name the new Blueprint class **DatasmithActor**. Double-click the new Blueprint to open the editor.
    
    ![Pick Parent Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/422083f5-4eb2-4c55-8631-83efca6becb3/5-0-110-create-actor.png "Pick Parent Class menu")
    
    This anchor will serve as the origin point for the imported Datasmith content. If your content is offset from the origin in your source application, then Unreal Engine will maintain that offset from the anchor when the content is imported.
    
2.  Select the **Event Graph** tab and remove every event except Event **BeginPlay**. Drag a connection from Event BeginPlay and add the **Spawn Actor From Class** node. Open the **Class** dropdown menu and select **DatasmithRuntimeActor**. Promote the **Return Value** to a variable and name it **Anchor**.
    
    ![Runtime Spawn Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f659e99-4184-43a3-ae85-977e59f23554/5-0-120-spawn-datasmith-actor.png "Using Spawn Actor From Class to spawn the Anchor at Runtime")
3.  **Spawn Actor** requires a Transform to spawn the Anchor. Right-click to the left of Spawn Actor and add a **Make Transform** node. Connect the output from Make Transform to the **Spawn Transform** pin on Spawn Actor.
    
    ![Make Transform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f15099c-ca5f-4562-a78f-e2716690348c/5-0-130-add-make-transform-node.png "Adding the Make Transform node")
4.  To finish the Blueprint, click and drag from the execute pin of the **Set** node and add a **Load File from Explorer** node. Connect a reference to the **Anchor** variable to the **Datasmith Runtime Actor** input.
    
    ![Runtime Load Datasmith](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15cf87b3-c9e7-4653-8a12-000dd5c62555/5-0-140-add-load-file-from-explorer.png "Finishing the Blueprint with the Load File From Explorer node.")
5.  **Save** and **Compile** the Blueprint. Add a copy of your Anchor Blueprint to the level and press **Play** to test.
    

Unreal Engine will open a File Explorer window and ask you to select a file.

## Creating a Datasmith Direct Link with Blueprints

You can also open a Datasmith Direct Link between one or more source applications and your Unreal Engine project at runtime using Datasmith Runtime.

1.  Start by creating a new **Actor** Blueprint to contain the anchor point for your Datasmith content. Double-click the new Blueprint to open the editor.
2.  Similar to the previous example, select the tab for the **Event Graph** and remove every event except for **Event BeginPlay**. Drag a connection off Event BeginPlay and add the **Spawn Actor From Class** node. Open the **Class** dropdown menu and select **DatasmithRuntimeActor**.
3.  A Transform is required to spawn the Anchor. Right-click to the left of Spawn Actor and add a **Make Transform** node. Connect the output from Make Transform to the **Spawn Transform** pin on Spawn Actor.
    
    ![Make Transform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4baa82b8-3fe5-40b6-8bab-4c2d3bda8ae8/5-0-150-spawn-datasmith-actor-and-attach-transform.png "Adding the Make Transform node")
4.  Next, you need a **Direct Link Proxy** to act as a connection point between your application and your source application. Drag a connection from the **Set** node and create a **Get Direct Link Proxy**. Promote the output to a variable and name it **Direct Link Sources Proxy**. Set it to be Public.
    
    ![Load Direct Link Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e21fb48-3bf8-4ab0-8c40-90c36083e6b2/5-0-160-get-direct-link-proxy-blueprint.png "Adding the Direct Link Proxy node.")
5.  Click the plus **(+)** button in the **Functions** section of the **My Blueprints** panel to create a new function. Name it **DirectLinkUpdate**. You will use this new function to trigger the Direct Link connection during runtime.
    
    ![Creating a new Blueprint Function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98557c67-6ebb-42a3-bbc5-7e9e51073c20/5-0-170-create-direct-link-update-function.png "Creating a new Blueprint Function")
6.  Start by getting a copy of your **Direct Link Proxy** variable. Drag a line from the variable and create a **Get List of Sources** node. Promote the output to a variable to hold the list of Direct Link sources and make this variable public.
    
    ![Get List of Sources](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f10cdeb-402d-4d91-985c-0db7319e2b64/5-0-180-direct-link-get-sources.png "Adding Get List of Sources node.")
7.  Drag the Anchor variable you created earlier from the **My Blueprint** tab into the Direct Link Update function. Drag the a line from the output, then type in **Set Import Options** to select and insert that node.
    
    ![Set Import Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1434f13-feff-4de1-adac-099d183bc2ab/5-0-190-direct-link-set-import-options.png "Adding the Set Import Options node.")
8.  Right-click and create a **Make Datasmith Runtime Import Options** node, and then drag a connection from the output to the **Import Options** input.
    
    ![Make Import Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/720d7480-c059-424d-a09a-eab3e4eb119e/5-0-200-direct-link-make-datasmith-runtime-import-options.png "Making the import options used by the Direct Link connection.")
9.  Finish the function by dragging a line from Set Import Options and creating an **Open Connection with Index** node. This takes in an anchor and a **Source Index** as input. Connect the reference to the Anchor to the Target input.
    
    ![Open Connection with Index](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1df00e4-8c80-4b18-856d-54e98835250d/5-0-210-direct-link-open-connection-with-index.png "Using the Open Connection with Index node.")
10.  Click the plus **(+)** next to Variables to create a new variable. Name it **SourceIndex**, and make it of type Integer.
    
    ![Adding a Source Index](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/772505b0-3409-4f85-ae37-ad40dc1d35f9/5-0-215-add-source-index-variable.png "Adding a Source Index")
11.  Connect the new variable to the **Source Index** input on the **Open Connection with Index** node. An index value of 0 will connect to the first source in the list.
    
    ![Connecting the Source Index](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3616d15d-04de-4933-9bcc-1110c31e9632/5-0-220-direct-link-set-source-index.png "Connecting the Source Index")
12.  Finally, click on the **DirectLinkUpdate** function in My Blueprints and enable **Call In Editor** in the **Details** panel. This option makes the function available at runtime in the Details of the Anchor object.
    
    Click for full image.
    
13.  **Save** and **Compile**. The finished Blueprint should look like the example below:

Click for full image.

Start your source application and run the project by clicking the **Play** button. Select your Anchor in the **World Outliner** and click the **Direct Link Update** button in the **Details** panel. Then, click the **Synchronize with Direct Link** button in your source application. You will see your Datasmith content appear in your Level using the import options specified in the Blueprint.

Disabling the **Use Less CPU when in Background** option enables the engine to update the 3D viewport when the Unreal Engine window is not focused and when a Pawn in the level is not possessed. This option is found in the **Editor Preferences** under **General > Performance**.
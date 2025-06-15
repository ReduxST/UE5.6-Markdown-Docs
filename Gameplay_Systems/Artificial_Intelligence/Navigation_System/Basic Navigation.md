# Basic Navigation

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/basic-navigation-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/basic-navigation-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:40

---

## Overview

The **Unreal Engine Navigation System** provides pathfinding capabilities to Artificial Intelligence Agents.

To make it possible to find a path between a start location and a destination, a Navigation Mesh is generated from the world's collision geometry. This simplified polygon mesh represents the navigable space in the Level. Default settings subdivide the Navigation Mesh into tiles to allow rebuilding localized parts of the Navigation Mesh.

The resulting mesh is made of polygons and a cost is associated with each polygon. While searching for a path, the pathfinding algorithm will attempt to find an optimal path with the lowest cost to the destination.

The system includes a variety of features that you can use to customize the Agent's navigation behavior based on your specific needs.

## Goals

In this Quick Start guide, you will learn how to create a simple Agent that will use the Navigation System to roam around the Level.

## Objectives

-   Use a Navigation Mesh Actor in your Level to build the navigation.
    
-   Learn to visualize the navigation mesh in your Level and adjust it to cover your needs.
    
-   Modify the ThirdPersonCharacter Blueprint to roam around the Level using the Navigation System.
    

## 1 - Required Setup

1.  In the **New Project Categories** section of the Unreal Project Browser, select **Games** and the **Third Person** template.
    
    ![Select the Games category and click Next](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bd96e7a-bd59-40e0-a7de-b9520d7dae39/create-project-a.png)
2.  Select the **Blueprint** and **No Starter Content** options and click **Create**.
    
    ![Select Blueprint and No Starter Content and click Create Project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d17601fc-9e28-4d78-afe9-868a6966cce6/basic-create-settings-a.png)

### Section Results

You have created a new Third Person project and are now ready to learn about the Navigation System.

## 2 - Building the Navigation Mesh

In this section, you will use a **Navigation Mesh Bounds Volume** to specify the area in your Level where navigation needs to be generated. This information is used by Agents to navigate the Level and get to their destinations.

1.  On the default **ThirdPersonExampleMap** of your project, go to the **Place Actors** panel, search for **NavMeshBoundsVolume,** and drag it into your Level.
    
    ![Drag a Nav Mesh Bounds Volume actor to the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1ad172b-0e6c-431d-ac24-642f9d7f1577/basic-drag-navmesh-bounds.png)
2.  With the **NavMeshBoundsVolume** selected, go to the **Details** panel and scale the volume to X = 20, Y= 20, and Z = 5. Move the volume so it covers the entire play area, as seen below.
    
    ![Scale the volume to X = 20, Y= 20, and Z = 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3cecfd8-3de2-4c1c-8b48-08450babd089/basic-navmesh-scale-a.png) ![The volume now covers the entire play area](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6796f3b1-192f-4e58-b52a-c7d2f6d2a2ff/basic-navmesh-scale-2.png)
3.  Select the **BP\_ThirdPersonCharacter** Blueprint in the **Outliner** window and remove it from the Level.
    
    ![Remove the Third Person Character from the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce3a25ad-3331-4189-bf42-702b1f40759f/basic-remove-char.png)
4.  Press the **P key** on your keyboard to visualize the Navigation Mesh in your Level. As you can see from the image below, the Navigation Mesh is visualized with the color green by default.
    
    Unreal Engine automatically generates the Navigation Mesh as soon as a Nav Mesh Bounds Volume Actor is added to the Level or is resized.
    
    ![Press P to visualize the Navigation Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69bc24a6-f990-4cfe-b45a-f1d1d899ea8f/basic-navmesh-visualize-a.png)
5.  Notice how the Navigation Mesh contains visual artifacts on the stairs. This can happen because the Navigation Mesh is a simplified representation of the collision in the Level. Select the **RecastNavMesh-Default** Actor in the **Outliner** window and go to the **Details** panel. Go to the **Display** section and set the **Draw Offset** value to **50**. This adjusts the height offset where the Navigation Mesh is drawn for better readability.
    
    ![Set the Draw Offset to 50 for better readibility](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e02376d5-0431-4ca0-93bc-db98d6df37f7/basic-navmesh-offset-a.png)

### Section Results

In this section, you added a Nav Mesh Bounds Volume Actor to your Level and scaled it to fit the play area. You also learned how to visualize the final Navigation Mesh by pressing the P key.

## 3 - Visualizing the Navigation Mesh

In this section, you will learn how to modify various Navigation Mesh settings, as well as how to change the way you can visualize the mesh in the Level.

1.  Go to the **Outliner** and select the **RecastNavMesh-Default** Actor.
    
    ![Select the Recast Nav Mesh Actor Default from the World Outliner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc9063d7-17fe-43fb-8067-eeebe09a16c2/basic-navmesh-select-recast-actor.png)
2.  With the Actor selected, go to the **Details** panel and scroll down to the **Display** section. Here you will find a variety of options to better visualize the generated Navigation Mesh. In the example below, I selected the **Draw Poly Edges** to see the polygons that make up the mesh.
    
    ![Select Draw Poly Edges to see the polygons that make up the mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/824620ce-1487-4a2b-966c-38c76c29df8b/basic-navmesh-recast-triangles-a.png)
3.  You can also visualize the individual Navigation Tiles by enabling the **Draw Tile Bounds** checkbox.
    
    ![Enable Draw Tile Bounds to visualize the Navigation Tiles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0935794-8da6-424a-8ad6-e931569feb47/basic-navmesh-vsualize-2.png)
4.  You can modify the way the Navigation Mesh is generated by going to the **Generation** section and changing its options.
    

### Section Results

In this section, you learned how to change the Display settings of your Navigation Mesh and how you can influence its generation by adjusting a variety of options.

## 4 - Creating your First Agent

In this section, you will create a simple Agent that will roam around your Level by selecting a random location nearby and navigating to it. The Agent will wait a few seconds when it arrives at its destination before repeating the process.

1.  In the **Content Drawer**, right-click and select **New Folder** to create a new folder. Name the folder **NavigationSystem**.
    
2.  In the **Content Drawer**, go to **ThirdPerson > Blueprints** and select the **BP\_ThirdPersonCharacter** Blueprint. Drag it to the **NavigationSystem** folder and select the option **Copy Here**.
    
    ![Drag the Third Person Character Blueprint into the Navigation System folder and select Copy Here](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01a45622-a8cf-4896-8517-e8765a7509ff/basic-npc-copy-a.png)
3.  Go to the **NavigationSystem** folder and rename the Blueprint to **BP\_NPC\_NavMesh**. Double-click the Blueprint to open it and go to the **Event Graph**. Select all input nodes and delete them.
    
4.  Right-click the **Event Graph**, then search for and select **Add Custom Event**. Name the event **MoveNPC**.
    
    ![Right click in the Event Graph and search for Add Custom Event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ab40b5a-a74d-4d4b-8d75-ad7cb10b67b0/basic-npc-add-custom-event.png)
5.  Right-click the **Event Graph**, then search for and select **Get Actor Location**.
    
    ![Right click the Event Graph then search for and select Get Actor Location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/747a7765-1e53-4c6a-89f4-68727c4af336/basic-npc-get-location.png)
6.  Drag from the **GetActorLocation** node and search for and select **Get Random Reachable Point In Radius**. Set the **Radius** to 1000 units.
    
    ![Drag from the Get Actor Location node and search for and select Get Random Reachable Point In Radius](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/582531b2-7c47-472e-96f5-e347ab7d1356/basic-npc-random-point.png)
7.  Drag from the **Random Location** pin of the **GetRandomReachablePointInRadius** node and select **Promote to variable**.
    
    ![Drag from the Random Location pin of the Get Random Reachable Point In Radius node and select Promote to variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80ba506a-31cb-4059-ac42-f39ece4c4729/basic-npc-create-target-loc.png)
8.  Connect the **MoveNPC** node to the **RandomLocation** node you just created.
    
    ![Connect the Move NPC node to the Random Location node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28ffede0-71a2-4a51-b2fd-a08e303395ff/basic-npc-create-target-loc-2.png)
9.  Right-click the **Event Graph**, then search for and select **AI Move To**. Connect the **RandomLocation** node to the **AI Move To** node.
    
    ![Right click the Event Graph, then search for and select AI Move To](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fccc3f17-4a64-4262-989e-dddb80d139e2/basic-npc-ai-moveto.png)
10.  Right-click the **Event Graph** and search for and select **Get a reference to self**.
    
    ![Right click the Event Graph and search for and select Get a reference to self](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4126d8bd-745e-4b6d-80b0-4e6e7ab58fa8/basic-npc-self-a.png)
11.  Connect the **Self** node to the **Pawn** pin of the **AI Move To** node. Connect the **yellow** pin of the **Random Location** node to the **Destination** pin of the **AI Move To** node, as seen below.
    
    ![Connect the Self node to the Pawn pin of the AI Move To node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53333ed5-be51-4872-a487-0aa74cf30925/basic-npc-ai-move-connected.png)
12.  Drag from the **On Success** pin of the **AI Move To** node, then search for and select **Delay**. Set the **Duration** of the node to 4. Drag from the **Completed** pin of the **Delay** node, then search for and select **MoveNPC**, as seen below.
    
    ![Drag from the On Success pin of the AI Move To node and add a Delay node. Set Duration to 0.4. Drag from the Delay node and add a Move NPC node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb8bf540-c1e0-408a-af21-700a6c33c79c/basic-npc-success.png)
13.  Repeat the steps above to add the nodes to the **On Fail** pin of the **AI Move To** node. Set the **Duration** of the **Delay** node to 0.1.
    
    ![Repeat the steps above to add nodes to the  On Fail pin of the AI Move To node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef53282c-c3b9-4bad-9bd5-e03ec82fcbd6/basic-npc-on-fail.png)
14.  Right-click the **Event Graph**, then search for and select **Event Begin Play**. Drag from the **Event Begin Play** node, then search for and select **MoveNPC**.
    
    ![Right-click the Event Graph, then search for and select Event Begin Play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61e27dc1-27f4-46e1-af20-738aaee9f703/basic-npc-begin-play-1.png) ![Drag from the Event Begin Play node, then search for and select Move NPC](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23468243-4519-4a87-954d-1d7f1cf883c8/basic-npc-begin-play-2.png)
15.  **Compile** and **Save** the Blueprint.
    
16.  Drag your **BP\_NPC\_NavMesh** Blueprint to your Level and click **Simulate**. You should see your Agent roam around the Level.
    
    ![Your Agent is now moving in the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d406213-2a57-488c-acd8-301ce79edc7b/basic-npc-final-1.gif) ![Multiple Agents are moving in the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51c3012f-322d-48ee-b1b6-9d781d078442/basic-npc-final-2.gif)

### Section Results

In this section, you learned how to create a simple Agent that roams around the Level using the **Navigation Mesh**.
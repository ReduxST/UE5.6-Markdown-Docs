# Using Navigation Invokers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-navigation-invokers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-navigation-invokers-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:21

---

## Overview

Unreal Engine's **Navigation System** allows Agents to navigate the Level using a **Navigation Mesh** for pathfinding. In addition to the various **Runtime Generation** methods for the Navigation Mesh, the system also includes a way to only build the navigation locally around specific targets.

**Navigation Invokers** are Blueprint Actor components that generate the Navigation Mesh around the Agent at runtime. Using Navigation Invokers removes the need to build the Navigation Mesh in the editor and can also limit the number of tiles generated at runtime.

Navigation Invokers are ideal for big Levels where building the Navigation Mesh in the editor is impractical.

## Goals

In this guide, you will learn to use Navigation Invokers with your Agents to generate the Navigation Mesh during gameplay.

## Objectives

-   Create a new Level and configure the Navigation System to use Navigation Invokers.
    
-   Modify the ThirdPersonCharacter Blueprint to roam around the Level using Navigation Invokers.
    

## 1 - Required Setup

1.  In the **Unreal Project Browser** window, select the **Games** category and **Third Person** template.
    
    ![Select the Games and ThirdPerson category and click Next](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6aecd2b0-0f38-4c5c-b16e-b2c2acfcad72/create-project-a.png)
2.  Enter a **Project Name** and click **Create**.
    
    ![Select Blueprint and No Starter Content and click Create Project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ec0d55d-4020-444b-8ac0-1361846f604f/basic-create-settings-a.png)

### Section Results

You created a new Third Person project and are now ready to learn about Navigation Invokers.

## 2 - Creating Your Test Level

1.  Click **File > New Level** from the Menu Bar.
    
    ![Click New Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7778eaa9-e047-431a-a9d3-2156d9d36ea0/new-level-a.png)
2.  Select the **Basic** Level.
    
    ![Select the Basic Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ae88140-4986-4689-9b44-a9c52f2e2737/select-level-template-a.png)
3.  Select the **Floor** Static Mesh Actor in the **Outliner** and go to the **Details** panel. Set the **Scale** to X = 100, Y = 100, Z = 1.
    
    ![Select the Floor Static Mesh Actor in the Outliner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1807f8cd-cdd5-4337-863b-1b6425354f42/create-floor-1.png) ![Set the Scale to X = 100, Y = 100, Z = 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed0e9b2b-f7b8-4b82-9f98-c52db19c57f0/invokers-floor-scale-a.png)
4.  Click **Settings > Project Settings** and go to the **Navigation System** category. Enable the **Generate Navigation Only Around Navigation Invokers** checkbox.
    
    ![Click Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/621a5e90-6911-461f-9abe-74becaf5ce10/project-settings-a.png) ![Enable the Generate Navigation Only Around Navigation Invokers checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b400a51-9c25-4bab-9ffd-d2490c768956/invokers-settings-1.png)
5.  (Optional) The **Invokers Maximum Distance from Seed** property sets the maximum distance between players (seeds by default) and Invokers that will be considered to regenerate tiles around those Invokers.
    
    In the example below, we set the maximum distance to 30,000 units (300 meters). Any Invokers farther from the player will not trigger navigation regeneration.
    
    ![Set the Invokers Maximum Distance from Seed to 30,000](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34b34f25-1a47-48a9-8b54-6bb979c924fb/invokers-max-distance.png)
6.  Go to the **Navigation Mesh** category and scroll down to the **Runtime** section. Click the **Runtime Generation** dropdown and select **Dynamic**.
    
    ![Click the Runtime Generation dropdown and select Dynamic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fcb35e02-3479-4b76-bbe8-899c37f5ca6c/invokers-settings-2.png)
7.  Go to the **Place Actors** panel and search for **NavMeshBoundsVolume**. Drag it into the Level and place it on the floor mesh. Scale the **NavMeshBoundsVolume** to X = 500, Y=500, Z = 10.
    
    ![Drag the Nav Mesh Bounds Volume to the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef5320f6-3b74-46fd-9be9-67594c1167da/invokers-nav-mesh-drag.png) ![Set the Scale to X = 500, Y=500, Z = 10](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/686fdac9-6cbd-4122-a065-e9e1a26691d5/invokers-nav-mesh-scale.png)

### Section Results

In this section, you created a new Level and configured the Navigation System to use Navigation Invokers.

## 3 - Creating your Agent

1.  In the **Content Drawer**, right-click and select **New Folder** to create a new folder. Name the folder **NavigationSystem**.
    
2.  In the **Content Drawer**, go to **ThirdPerson> Blueprints** and select the **BP\_ThirdPersonCharacter** Blueprint. Drag it into the **NavigationSystem** folder and select the option **Copy Here**.
    
    ![Drag the Third Person Character Blueprint to the Navigation System folder and select Copy Here](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66246496-7e91-4c49-b107-733fa2e0241d/move-blueprint-a.png)
3.  Navigate to the **NavigationSystem** folder and rename the Blueprint to **BP\_NPC\_Invoker**. Double-click the Blueprint to open it and go to the **Event Graph**. Select all input nodes and delete them.
    
4.  Right-click the **Event Graph**, then search for and select **Add Custom Event**. Name the event **MoveNPC**.
    
    ![Right-click the Event Graph, then search for and select Add Custom Event. Name the event Move NPC](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c972ce4c-fc8a-4d45-a0cf-69e3b1d49276/custom-event-a.png)
5.  Right-click the **Event Graph**, then search for and select **Get Actor Location**.
    
    ![Right-click the Event Graph, then search for and select Get Actor Location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb32bad7-92b3-4881-9460-02780a121977/get-actor-location-a.png)
6.  Drag from the **GetActorLocation** node and search for and select **Get Random Reachable Point In Radius**. Set the **Radius** to 1000.
    
    ![Drag from the Get Actor Location node and search for and select Get Random Reachable Point In Radius](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b111c9b-ab03-4997-803b-54579f218391/get-random-a.png)
7.  Drag from the **Random Location** pin of the **GetRandomReachablePointInRadius** node and select **Promote to variable**.
    
    ![Drag from the Random Location pin of the Get Random Reachable Point In Radius node and select Promote to variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13d78acf-3149-46ce-8069-255f10c9bdaf/promote-variable-a.png)
8.  Connect the **MoveNPC** node to the **RandomLocation** node you just created.
    
    ![Connect the Move NPC node to the Random Location node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4e8d44c-d252-4893-852d-8f2bedc50987/move-npc-a.png)
9.  Right-click the **Event Graph**, then search for and select **AI Move To**. Connect the **RandomLocation** node to the **AI Move To** node.
    
    ![Right-click the Event Graph, then search for and select AI Move To](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56a24289-ec7e-408b-a8b2-324a3b107e70/ai-move-to.png)
10.  Right-click the **Event Graph**, then search for and select **Get a reference to self**.
    
    ![Right-click the Event Graph, then search for and select Get a reference to self](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36f183fa-e0c9-4194-9368-7dff01e6618f/reference-self-a.png)
11.  Connect the **Self** node to the **Pawn** pin of the **AI Move To** node. Connect the **yellow** pin of the **Random Location** node to the **Destination** pin of the **AI Move To** node, as seen below.
    
    ![Connect the Self node to the Pawn pin of the AI Move To node. Connect the yellow pin of the Random Location node to the Destination pin of the AI Move To node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be764628-dab5-4762-acc8-5917bd595a34/blueprints-1.png)
12.  Drag from the **On Success** pin of the **AI Move To** node, then search for and select **Delay**. Set the **Duration** of the node to 4. Drag from the **Completed** pin of the **Delay** node, then search for and select **MoveNPC**, as seen below.
    
    ![Drag from the On Success pin of the AI Move To node and add a Delay node. Set the Duration to 4. Drag from the Duration node and add a Move NPC node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2dfee8ca-5bdf-4469-9d5a-670be175678a/blueprints-2.png)
13.  Repeat the steps above to add these nodes to the **On Fail** pin of the **AI Move To** node. Set the **Duration** of the **Delay** node to 0.1.
    
    ![Repeat the steps above to add these nodes to the On Fail pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9dab2f44-6f5e-4ba9-a289-6d58b4cffeec/blueprints-3.png)
14.  Right-click the **Event Graph**, then search for and select **Event Begin Play**. Drag from the **Event Begin Play** node, then search for and select **MoveNPC**.
    
    ![Right-click the Event Graph, then search for and select Event Begin Play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af0e29de-cb22-4b5f-a8c8-5331e913dd9a/begin-play-a.png) ![Drag from the Event Begin Play node, then search for and select Move NPC](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed787828-3c94-4f3c-b963-1e68e4ad8721/begin-play-b.png)
15.  Go to the **Components** tab, click the **+Add** dropdown, then search for and select **Navigation Invoker**.
    
    ![Go to the Components tab, click the Add Component dropdown, then search for and select Navigation Invoker](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11fdfbb6-ecd4-4e2d-bb61-5f8d0cc600a9/invokers-npc-nav-invoker.png)
16.  With the **Navigation Invoker** component selected, go to the **Details** panel and find the **Navigation** section. Here you can change the **Tile Generation Radius** (radius around the actor used to generate Navigation Mesh tiles) and **Tile Removal Radius** (radius from the actor used to remove Navigation Mesh tiles). For this example, set these values to **3000** and **5000**, respectively.
    
    ![Set the Tile Generation Radius to 3000 and the Tile Removal Radius to 5000](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7708a30-3e8f-43a6-bf62-03169373a151/invokers-npc-nav-ivoker-2.png)
17.  **Compile** and **Save** the Blueprint.
    
18.  Drag several **BP\_NPC\_Invoker** Blueprints to your Level and click **Simulate** to see the navigation generating around each Agent.
    
    ![Drag several BP_NPC_Invoker Blueprints to your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/561ce11b-6aab-4aa5-ade9-03d3f5f30a39/invokers-npc-drag-a.png)
    
    If you don't see the navigation, press P on your keyboard to visualize the Navigation Mesh.
    
    ![Your Agents are now moving in the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e3117d2-95db-41f6-b734-cbf128585cb0/invokers-agents-walking-a.gif)

### Section Results

In this section, you created an Agent that roams around the Level and uses the Navigation Invoker component to build the Navigation Mesh around itself.
# Modifying the Navigation Mesh Preparation Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/modifying-the-navigation-mesh-preparation-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/modifying-the-navigation-mesh-preparation-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:36:43

---

## Overview

This document will guide you through the preliminary steps of creating a Level and AI Agent to demonstrate the different ways you can modify the Navigation Mesh.

Alternatively, you can download the [full sample project](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/aa1121fe-094e-4665-9dd9-2737c6d7e125/navsystemsample.zip), which includes all the material covered in this guide.

## Objectives

-   Create a simple Level and add navigation by placing a Nav Mesh Bounds Volume Actor in the Level.
    
-   Modify the ThirdPersonCharacter Blueprint to roam around the Level using the Navigation System.
    

## 1 - Required Setup

1.  In the **New Project Categories** section of the menu, select **Games > Third Person** template.
    
    ![Select the Games category and select Games and the Third Person template](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acc99caf-787b-477f-8073-85ac6b7cbe89/create-project.png)
2.  Select the **Blueprint** and **No Starter Content** options and click **Create**.
    
    ![Select Blueprint and No Starter Content and click Create ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/396fe80e-844b-434b-b074-7521c4f9cc30/basic-create-settings.png)

### Section Results

You have created a new Third Person project and are now ready to build a basic Level with a Navigation Mesh.

## 2 - Creating Your Test Level

1.  Click **File > New Level** on the Menu Bar.
    
    ![Create a new Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f007e946-b5c9-4bc4-815d-25fbeb19d217/mod-new-level.png)
2.  Select the **Basic** Level and click **Create**.
    
    ![Select the Basic Level and click Create](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f14c987-6117-415c-8f56-87223449bb5f/mod-new-level-2.png)
3.  Select the **Floor** Static Mesh Actor in the **Outliner** and from the **Details** panel, set the **Scale** to X = 10, Y = 10, Z = 1.
    
    ![Select the Floor Static Mesh Actor in the World Outliner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82e4d22c-ccc3-443f-99df-dc7cef9c5dc9/mod-level-floor-selected.png) ![Set the Scale to X = 10, Y = 10, Z = 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33330a44-6c93-449c-9ba9-e03ad6bee48f/mod-level-floor-selected-2.png)
4.  Inside the **Content Drawer**, go to **LevelPrototyping > Meshes** and drag the **TemplateFloor** Static Mesh into the Level.
    
    ![Drag the Template Floor Static Mesh into the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f922df6-3335-41d2-8935-e74507586915/mod-level-drag-template-floor.png)
5.  Go to the **Place Actors** panel and search for **Nav Mesh Bounds Volume**. Drag it into the Level and place it above the floor mesh.
    
    ![Drag the Nav Mesh Bounds Volume to the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df695cd9-0a70-4ffc-8697-a08664691ae6/mod-level-nav-bounds-drag.png)
6.  With the **NavMeshBoundsVolume** selected, go to the **Details Panel** and set the **Scale** to X = 20, Y = 20, Z = 5 to cover the entire floor area. Unreal Engine will automatically generate navigation inside the navigation bounds by default. A Navmesh Actor **RecastNavMesh-Default** should have also been added to the Level. Press the **P** key to visualize the Navigation Mesh in the Level.
    
    If no navigation is generated, go to Project Settings > Navigation System and enable the Auto Create Navigation Data checkbox.
    
    ![Set the Scale to X = 20, Y = 20, Z = 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08b85a46-3ea6-425a-bc9a-2e5fbd3dbeca/mod-level-nav-bounds-scale.png) ![The Navigation Mesh now covers the entire floor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06d14fbc-0f4f-4811-a0c0-9cb3cb2e89a5/mod-level-nav-bounds-p.png)
7.  Go to the **Place Actors** panel and under the **Shapes** category drag the **Cube** Static MeshActor into your Level.
    
    ![Drag the Cube Static Mesh Actor into your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70b22511-9e3c-472a-b099-c7043e7b7342/mod-level-cube-drag.png)
8.  With the **Cube** selected, go to the **Details Panel** and set the **Scale** to X = 1, Y = 1, Z = 5.
    
    ![Set the Scale to X = 1, Y = 1, Z = 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7cac95a9-f859-486e-acc0-7833cf9f1179/mod-level-cube-scale.png) ![The Cube is now rescaled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0ede969-8cb9-40d6-90f1-d615d44d3455/mod-level-cube-scale-2.png)
9.  Drag three more **Cubes** into the level and scale them like the one above. Place them around your floor to create four pillars as seen below.
    
    ![Drag three more Cubes into the level and scale them like the one above](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/090eb3d8-3693-44d9-8c93-b785a707597d/mod-level-pillars.png)
10.  Next, add a stair and a platform in the middle. Inside the **Content Drawer**, go to **ThirdPerson > Meshes** and drag the **Linear\_Stair\_StaticMesh** into the Level.
    
    ![Add a stair and a platform in the middle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3177afd-cdad-4d2f-9b63-41f7082b0beb/mod-level-stairs-drag.png)
11.  With the stairs selected, go to the **Details Panel** and set the **Scale** to X = 1.5, Y = 1, Z = 1.3.
    
    ![Set the Scale to X = 1.5, Y = 1, Z = 1.3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a69727a-8c86-4e24-ac3d-0a43c9678f84/mod-level-stairs-scale.png)
12.  With the stairs selected, drag the mesh while holding the **Alt** key to duplicate it.
    
    ![Duplicate the stairs mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06d1dd86-a258-4981-9fc6-a35b57ad50fb/mod-level-stairs-duplicate.png)
13.  Go to the **Place Actors** panel and under the **Shapes** category drag the **Cube** Static Mesh Actor into your Level. Go to the **Details Panel** and set the **Scale** to X = 14, Y = 4, Z = 0.1. Place the Actor on the edge of the stairs to create a platform, as seen below.
    
    ![Drag a Cube Static Mesh Actor into your Level and set the scale to X = 14, Y = 4, Z = 0.1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce15967d-9f66-43bb-8db3-1c6a2ae71d9d/mod-level-bridge.png)
14.  Go to the **Place Actors** panel and under the **Basic** category drag the **Sphere** Static Mesh Actor into your Level.
    
    ![Drag a Sphere Static Mesh Actor into your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/589de925-7131-481d-a399-8450472c7b5c/mod-level-goal-drag.png)
15.  With the **Sphere** selected, go to the **Details** Panel and from the **Collision** section, set the **Collision Presets** to **No Collision**.
    
    ![Set the Collision Presets to No Collision](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cadfad48-5af7-4178-8bcc-58a1fcad3149/mod-level-goal-collision.png)
16.  Finally, duplicate the spheres and place them around your Level as shown below.
    
    ![Duplicate the spheres and place them around your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/013639e9-f7ca-4357-b61d-3b94a363c363/mod-level-goal-duplicate.png)

### Section Results

In this section, you created a simple Level and added a Nav Mesh Bounds Volume. You also added five spheres that will serve as target Actors for the Agent.

## 3 - Creating Your Agent

In this section, you will create an AI Agent that will move between a list of target Actors.

1.  In the **Content Drawer**, right-click and select **New Folder** to create a new folder. Name the folder **NavigationSystem**.
    
2.  In the **Content Drawer**, go to **ThirdPerson > Blueprints** and select the **BP\_ThirdPersonCharacter** Blueprint. Drag it into the **NavigationSystem** folder and select the option **Copy Here**.
    
    ![Copy the Third Person Character Blueprint to the Navigation System folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/362e416a-5e46-4a2e-b6de-b3c3b7f56a4a/drag-blueprint.png)
3.  Go to the **NavigationSystem** folder and rename the Blueprint to **BP\_NPC\_ModNavMesh**. Double-click the Blueprint to open it in the Blueprint Editor and go to the **Event Graph**. Select all input nodes and delete them.
    
4.  Right-click the **Event Graph**, then search for and select **Add Custom Event**. Name the event **MoveNPC**.
    
    ![Right click the Event Graph, then search for and select Add Custom Event. Name it Move NPC](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6128637-3693-4410-8a2d-490268732643/add-custom-event.png)
5.  Go to the **My Blueprint** panel and click the **Add (+)** button next to **Variables** to create a new variable. Name the variable **TargetList**.
    
    ![Create a new variable and name it Target List](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb061cb3-5fa9-4658-9aa0-752586ff6bdf/mod-npc-target-list-create.png)
6.  Go to the **Details** panel and click the dropdown next to **Variable Type**. Search for and select **Actor > Object Reference**.
    
    ![Set the variable type to Actor Object Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68af15c3-6caa-4cb0-bb7d-8996773f058f/mod-npc-target-list-actor.png)
7.  Click the **blue sphere** icon next to the Actor selection and click the **Array** option, as shown below. Click the **Instance Editable** checkbox to enable it.
    
    ![Click the blue sphere icon next to Actor selection and click the Array option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6ddc683-f9b1-44e8-ab24-a9dcfa0a08db/mod-npc-target-list-array.png) ![Click the Instance Editable checkbox to enable it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21449942-8b2e-48a5-bc6b-308ab4cb7d92/mod-npc-target-list-public.png)
8.  Drag the **TargetList** variable to the **Event Graph** and select the option **Get TargetList**.
    
9.  Drag from the **TargetList** node, then search for and select **Last Index**.
    
    ![Drag from the TargetList node, then search for and select Last Index](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b265bc9d-94cd-4882-8b9e-a21d358dfc24/mod-npc-target-list-last-index.png)
10.  Drag from the **TargetList** node and search for and select **Get (a copy)**.
    
    ![Drag from the TargetList node and search for and select Get a copy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de8b4d5d-144e-4b11-afba-c14887ec44dc/mod-npc-target-list-get-copy.png)
11.  Drag from the **green** pin of the **Get** node, then search for and select **Random Integer in Range**. Connect the **green** pin of the **Last Index** node to the **Max** pin of the **Random Integer in Range** node, as seen below.
    
    ![Drag from the green pin of the Get node, then search for and select Random Integer in Range](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e9dc1a9-686d-4768-86bd-140a809bce87/mod-npc-random-int.png) ![Connect the green pin of the Last Index node to the Max pin of the Random Integer in Range node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66801224-674d-4350-95dd-4fe63c7f487d/mod-npc-random-int-2.png)
12.  Drag from the **Get** node, then search for and select **Promote to variable**. Name the variable **CurrentTarget** and connect it to the **MoveNPC** node.
    
    ![Drag from the Get node, then search for and select Promote to variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fdfa810-0fc2-4b37-945a-38f477b0a985/mod-npc-curr-target.png) ![Name the variable Current Target and connect it to the Move NPC node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4572454-92a7-422d-9b26-115354519a61/mod-npc-curr-target-2.png)
13.  Drag from the **CurrentTarget** node, then search for and select **Is Valid**. Connect the **IsValid** macro node to the **Set CurrentTarget** node.
    
    ![Drag from the CurrentTarget node, then search for and select Is Valid](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b6c82fa-9a20-450e-8983-0487431c2d53/mod-npc-is-valid.png) ![Connect the IsValid macro node to the Set CurrentTarget node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/017a2c0a-ba4b-488d-8f11-b5a7dad8dad8/mod-npc-is-valid-2.png)
14.  Drag the **CurrentTarget** variable to the **Event Graph**, then select **Get Current Target**. Drag from the **CurrentTarget** node, then search for and select **Get Actor Location**.
    
    ![Drag from the CurrentTarget node, then search for and select Get Actor Location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30d3956e-127e-4068-8bda-f41de8e2d19b/mod-npc-get-location.png)
15.  Drag from the **Return Value** of the **GetActorLocation** node, then search for and select **Get Random Reachable Point In Radius**. Set the **Radius** value to **100**.
    
    ![Drag from the Return Value of the GetActorLocation node, then search for and select Get Random Reachable Point In Radius](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/665ea14f-6c0c-40b2-b5f5-9180924092b3/mod-npc-get-random-point.png) ![Set the Radius value to 100](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b03b9d9b-0355-4450-b414-2e92678052e7/mod-npc-get-random-point-2.png)
16.  Drag from the **Random Location** pin of the **GetRandomReachablePointInRadius** node and select **Promote to variable**. Name the variable **RandomLocation**. Connect the **RandomLocation** node to the **IsValid** node as shown below.
    
    ![Drag from the Random Location pin of the GetRandomReachablePointInRadius node and select Promote to variable. Name the variable Random Location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/862fa71f-7d5f-4022-8394-57991d74967c/mod-npc-random-location.png) ![Connect the RandomLocation node to the IsValid node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa841bfa-dd91-495b-87a5-68f0db6fc2b6/mod-npc-random-location-2.png)
17.  Drag from the **RandomLocation** node, then search for and select **AI MoveTo**.
    
    ![Drag from the Random Location node, then search for and select AI MoveTo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69be0fb3-96ab-4e7d-9611-a28c63081abb/mod-npc-ai-move.png)
18.  Drag from the **Pawn** pin of the **AI MoveTo** node, then search for and select **Get a reference to self**. Connect the **yellow** pin of the **RandomLocation** node to the **Destination** pin of the **AI MoveTo** node. Finally, set the **Acceptance Radius** of the **AI MoveTo** node to 50, as seen below.
    
    ![Drag from the Pawn pin of the AI MoveTo node, then search for and select Get a reference to self](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9250e0e2-1db3-4deb-8a5b-987d10e0ccf1/get-reference.png) ![Connect the yellow pin of the Random Location node to the Destination pin of the AI MoveTo node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2b5d0f9-ee33-43f8-b6f8-c8887884d4d4/mod-npc-ai-move-connected.png)
19.  Drag from the **On Success** pin of the **AI Move To** node, then search for and select **Delay**. Set the **Duration** of the node to 4. Drag from the **Completed** pin of the **Delay** node, then search for and select **MoveNPC**, as seen below.
    
    ![Drag from the On Success pin of the AI Move To node, then search for and select Delay. Set the Duration to 4. Drag from the Delay node and add a Move NPC node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8d668db-63d6-4426-867f-c450ff5a8b7f/mod-npc-delay-1.png)
20.  Repeat the steps above to add the nodes to the **On Fail** pin of the **AI Move To** node. Set the **Duration** of the **Delay** node to 0.1.
    
    ![Repeat the steps above to add the nodes to the On Fail pin of the AI Move To node. Set the Duration of the Delay node to 0.1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2cae2148-de64-4ce4-bd84-753571d8be60/mod-npc-delay-2.png)
21.  Right-click the **Event Graph**, then search for and select **Event Begin Play**. Drag from the **Event Begin Play** node, then search for and select **MoveNPC**.
    
    ![Right-click the Event Graph, then search for and select Event Begin Play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0101ac5-9646-4a03-a62e-2a5754a33139/mod-moving-begin-1.png) ![Drag from the Event Begin Play node, then search for and select Move NPC](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73c18708-7855-4743-a9cb-be0355d40866/mod-moving-begin-2.png)
22.  **Compile** and **Save** the Blueprint.
    
23.  Drag your **BP\_NPC\_ModNavMesh** Blueprint into your Level and under the **Details** panel find the **Target List** and click the **Add (+)** button to add a new target Actor.
    
    ![Drag your BP_NPC_ModNavMesh Blueprint into your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4424b199-b126-477f-ac30-29519bc8c4b1/mod-npc-drag.png) ![In the Details panel find the Target List and click the Add button to add a new target Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/558ff45d-b77b-4aa5-9a93-8dc4446a5b24/mod-npc-targets-1.png)
24.  Click the dropdown, then search for and select the **Sphere** Actor you created earlier.
    
    ![Click the dropdown, then search for and select the Sphere Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2791d287-2363-49d5-b17e-e0956ee14193/mod-npc-targets-2.png)
25.  Repeat the step above to add the remaining four **Sphere** Actors.
    
    ![Repeat the step above to add the remaining four Sphere Actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd349adf-a9b7-429f-a38c-cd19c1fdd9f3/mod-npc-targets-3.png)
26.  Click **Simulate** to see your Agent roam between goals in your Level.
    
    ![Click Simulate to see your Agent roam between goals in your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/620236f1-a2d3-4a6d-b16f-96bcd748b1c1/mod-prep-demo.gif)

### Section Results

In this section, you created an Agent that roams between a list of target Actors. You can now move on to learning about [Modifying the Navigation System](/documentation/en-us/unreal-engine/overview-of-how-to-modify-the-navigation-mesh-in-unreal-engine).
# Custom Navigation Areas and Query Filters Preparation Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/custom-navigation-areas-and-query-filters-preparation-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/custom-navigation-areas-and-query-filters-preparation-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:10

---

## Overview

This document will guide you through the preliminary steps of creating a Level and AI Agent to learn about the Custom Areas and Query Filters in the Navigation System.

You can also download the [full sample project](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/bd70b8c8-4740-43e9-af93-f2b4d3e5bc34/navsystemsample.zip), which includes all the material covered in this guide.

## Objectives

-   Create a new Level and set up navigation by placing a Navigation Mesh Actor in the Level.
    
-   Modify the ThirdPersonCharacter Blueprint to navigate toward its target by using specific Query Filters.
    

## 1 - Required Setup

1.  In the **New Project Categories** section of the Unreal Project Browser, select **Games > Third Person** template.
    
    ![Select the Games category and click Third Person](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50bfc04f-df2f-48fe-b71a-061a8a75e477/create-project-a.png)
2.  Select the **Blueprint** and **No Starter Content** options and click **Create**.
    
    ![Select Blueprint and No Starter Content and click Create](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76503cfe-18f4-4b36-8d19-2167a7eea603/basic-create-settings-a.png)

### Section Results

You have created a new Third Person project and are now ready to learn about creating Area Classes and Navigation Query Filters.

## 2 - Creating Your Test Level

1.  Click **File > New Level** on the Menu Bar.
    
    ![Click New Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/875bf185-463a-4e3a-b21e-fbbf459ddd75/new-level-a.png)
2.  Select the **Basic** Level and click **Create**.
    
    ![Select the Basic Level and click Create](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60724785-1c65-4fc0-b543-1fd22a5ba225/select-level-template-a.png)
3.  Select the **Floor** Static Mesh Actor in the **Outliner** and on the **Details** panel, set the **Scale** to X = 10, Y = 10, Z = 1.
    
    ![Select the Floor Static Mesh Actor in the World Outliner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f59f0a47-1549-4ace-af05-6577c120be52/create-floor-1.png) ![Set the Scale to X = 10, Y = 10, Z = 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e534028-a2d1-41ba-9aa3-e685851e1a72/create-floor-2.png)
4.  Go to the **Place Actors** panel and search for **NavMeshBoundsVolume**. Drag it into the Level and place it on the floor mesh.
    
    ![Drag a Nav Mesh Bounds Volume Actor to the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0de4cf3-6658-4cc1-a777-79f24a5ebb76/custom-navmesh-drag-a.png)
5.  With the **NavMeshBoundsVolume** selected, go to the **Details** panel and set the **Scale** to X = 5, Y = 10, Z = 1.
    
    ![Set the Scale to X = 5, Y = 10, Z = 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9e7ebe3-ce23-472f-a237-b9698fcd7740/custom-navmesh-scale-a.png)
6.  Go to the **Place Actors** panel and go to the **Shapes** category. Drag a **Sphere** Actor into the Level.
    
    ![Drag a Sphere Actor into the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07d3c262-ae11-4c03-8b7f-b738bcdd321e/custom-sphere-drag-a.png)

### Section Results

In this section, you created a new Level and added a Navigation Mesh and a Sphere Actor. You are now ready to create an Agent that will walk toward the sphere goal.

## 3 - Creating Your Agent

In this section, you will create an Agent that navigates to its target Actor.

1.  In the **Content Drawer**, right-click and select **New Folder** to create a new folder. Name the folder **NavigationSystem**.
    
2.  In the **Content Drawer**, go to **ThirdPersonBP > Blueprints** and select the **BP\_ThirdPersonCharacter** Blueprint. Drag it to the **NavigationSystem** folder and select the option **Copy Here**.
    
    ![Drag the Third Person Character Blueprint to the Navigation System folder and select Copy Here](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a65cc213-a515-4d8f-8e61-d1bdb79fc1c9/move-blueprint-a.png)
3.  Navigate to the **NavigationSystem** folder and rename the Blueprint to **BP\_NPC\_CustomZone**. Double-click the Blueprint to open it and go to the **Event Graph**. Select all input nodes and delete them.
    
4.  Right-click the **Event Graph,** then search for and select **Add Custom Event**. Name the event **MoveNPC**.
    
    ![Right-click the Event Graph, then search for and select Add Custom Event. Name the event Move NPC](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a3cc6a6-3caa-4a3d-be0b-1f795e286690/custom-event-a.png)
5.  Go to the **My Blueprint** panel and click the **Add (+) button** next to **Variables** to create a new variable. Name the variable **Target**.
    
    ![Click the Add next to Variables to create a new variable and name it Target](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c28403a-f555-414c-a2c5-4d338fde6528/custom-npc-target-1.png)
6.  Go to the **Details** panel and click the **Variable Type** dropdown. Search for **Actor** and select the **Object Reference**. Enable the **Instance Editable** checkbox.
    
    ![Click the Variable Type dropdown and  select the Actor Object Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e86e539e-a9c6-4d9c-b07d-3f7e75fd7303/custom-npc-target-2.png) ![Enable the Instance Editable checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2364825e-40ba-4735-940c-87e834fdff4c/custom-npc-target-3.png)
7.  Drag the **Target** variable to the **Event Graph** and select the option **Get Target**. Drag from the **Target** node, then search for and select the **Is Valid** macro, as shown below.
    
    ![Drag from the Target node, then search for and select the Is Valid macro](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16e6c381-0100-46e8-b4e7-20d7bd023059/custom-npc-is-valid.png)
8.  Right-click the **Event Graph**, then search for and select **Get reference to self**.
    
    ![Right-click the Event Graph, then search for and select Get reference to self](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0331cf8a-d16b-4108-b5fd-10eb839e8d24/custom-npc-self-a.png)
9.  Drag from the **Self** node, then search for and select **Get AIController**.
    
    ![Drag from the Self node, then search for and select Get AI Controller](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d0799cb-dbcc-4e53-9eb4-0ed5f3983dfb/custom-npc-ai-controller.png)
10.  Drag from the **AI Controller** node, then search for and select **Move to Actor**.
    
    ![Drag from the AI Controller node, then search for and select Move to Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3ce3799-a2ae-4ec1-8d79-253cce43a7e6/custom-npc-move-to-actor.png)
11.  Connect the **Is Valid** pin of the **Is Valid** node to the **Move to Actor** node. Set the **Acceptance Radius** of the **Move to Actor** node to 50. Drag the **Target** variable and connect it to the **Goal** pin of the **Move to Actor** node.
    
    ![Connect the Is Valid pin of the Is Valid node to the Move to Actor node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4da0c12-0b32-4584-9990-0f1dde4e05f2/custom-npc-move-to-actor-2.png)
12.  Right-click the **Filter** Class pin of the **Move to Actor** node and select **Promote to Variable**. Go to the **Details** panel and enable the **Instance Editable** checkbox.
    
    ![Right-click the Filter Class pin of the Move to Actor node and select Promote to Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f033b20-46c7-423d-8b50-8be7ebdb5863/custom-npc-filter-1.png) ![Enable the Instance Editable checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3bb0001d-8d41-4fa7-af87-464aa11ade50/custom-npc-filter-2.png)
13.  Right-click the **Event Graph**, then search for and select **Event Begin Play**. Drag from the **Event Begin Play** node and search for and select **MoveNPC**.
    
    ![Right-click the Event Graph, then search for and select Event Begin Play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63be4aef-a0a4-48dd-a8e7-1e98196f4f5a/custom-npc-begin-play.png) ![Drag from the Event Begin Play node and search for and select MoveNPC](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e2926ce-f25a-44d8-83d1-8c3e1116b8b1/custom-npc-begin-play-2.png)
14.  **Compile** and **Save** the Blueprint. The final Blueprint should look like the image below.
    
    ![This is the final Blueprint Setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e43701e-6b71-4f20-8974-e56cb85a3700/custom-npc-completed-a.png)
15.  Drag the **BP\_NPC\_CustomZone** Blueprint into your Level. Navigate to the **Details** panel and click the dropdown next to **Target**. Search for and select **Sphere**, as seen below.
    
    ![Drag the BP_NPC_CustomZone Blueprint into your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a39d1c77-bf3a-4fe3-afe8-f14b2beb9e14/custom-npc-drag-1.png) ![Navigate to the Details panel and click the dropdown next to Target. Search for and select Sphere](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e61e934-d34e-421a-9341-60bcc93e6208/custom-npc-drag-2.png)
16.  Press **Simulate** and watch as your Agent moves toward the Sphere.
    
    ![Your Agent is now moving towards the Sphere](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bf12c12-004e-417d-b889-f647b059ef22/custom-npc-walk-1.gif)

### Section Results

In this section, you created an Agent that navigates toward its goal and can use a Navigation Query Filter. You are now ready to learn about adding [Custom Navigation Areas and Query Filters](/documentation/en-us/unreal-engine/custom-navigation-areas-and-query-filters-quick-start-in-unreal-engine).
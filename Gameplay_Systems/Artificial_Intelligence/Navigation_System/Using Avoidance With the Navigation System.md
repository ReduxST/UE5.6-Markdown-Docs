# Using Avoidance With the Navigation System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-avoidance-with-the-navigation-system-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-avoidance-with-the-navigation-system-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:18

---

## Overview

**Unreal Engine's** **Navigation System** allows Agents to traverse the Level using a **Navigation Mesh** for pathfinding.

While pathfinding can determine a path around objects that don't move, avoidance algorithms are better suited to handle moving obstacles. There are two methods of avoidance the Agents can use to navigate around dynamic obstacles and each other, **Reciprocal Velocity Obstacles (RVO)** and **Detour Crowd Manager**.

The **Reciprocal Velocity Obstacles (RVO)** system calculates the velocity vectors for each Agent to avoid a collision with nearby Agents. This system looks at the nearby Agents and assumes they are traveling with a constant velocity within each time step of the calculation. The optimal velocity vector chosen is the closest match to the Agent's preferred velocity in the direction of its target.

Unreal Engine's implementation of RVO includes optimizations to reduce frame rate dependencies. It also includes improvements to avoid constant path recalculation and a priority system to help resolve potential collisions. RVO does not use the Navigation Mesh for avoidance, so it can be used separately from the Navigation System for any Character. The system is included in the **Character Movement** component of the Character class.

The **Detour Crowd Manager** system handles avoidance between Agents by using an adaptive RVO sampling calculation. It does this by calculating a coarse sample of velocities with a bias toward the Agent's direction that allows for a significant improvement in the quality of the avoidance over the traditional RVO method. This system also uses visibility and topology path corridor optimizations to further improve collision avoidance.

The Detour Crowd Manager system is highly configurable with options to specify sampling patterns, the maximum number of Agents, and Agent Radius. The system is included in the **DetourCrowd AI Controller** class and can be used with any Pawn class.

Both systems work independently and should be used exclusively in your project.

### High-Level Comparison of Avoidance Methods

| Method | Description | Limitations |
| --- | --- | --- |
| Reciprocal Velocity Obstacles | 
-   Agents avoid obstacles by using velocity vectors within a specified radius.
-   Included in the Character Movement component of the Character class.



 | 

-   Less configurable compared to the Detour Crowd Manager.
-   Limited to the Character class.
-   Does not use the Navigation Mesh for avoidance so Agents can potentially go "out of bounds".



 |
| Detour Crowd Manager | 

-   Agents avoid obstacles by using path optimizations along with velocity vectors within a specified radius.
-   Included in the DetourCrowd AI Controller class. | Has a fixed maximum number of Agents defined in the project settings.



 | 

-   Has a fixed maximum number of Agents defined in the project settings.



 |

## Goals

In this guide, you will learn how to use the Reciprocal Velocity Obstacles and Detour Crowd avoidance methods by comparing the behavior of several Agents interacting with each other.

## Objectives

-   Modify the ThirdPersonCharacter Blueprint so it navigates toward a target.
    
-   Modify the Agent Blueprint to use RVO avoidance.
    
-   Modify the Agent Blueprint to use Crowd Detour avoidance.
    

## 1 - Required Setup

1.  In the **New Project Categories** section of the Unreal Project Browser, select **Games > Third Person** template.
    
    ![Select the Games category and click Next](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b7b6677-7670-44c4-ae22-42087616b6ff/create-project-a.png)
2.  Select the **Blueprint** and **No Starter Content** options and click **Create**.
    
    ![Select Blueprint and No Starter Content and click Create Project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ee20e00-1579-4410-a7ca-4b87b49d531a/basic-create-settings-a.png)

### Section Results

You created a new Third Person project and are now ready to learn about the avoidance methods available in Unreal Engine.

## 2 - Creating Your Test Level

1.  Click **File > New Level** on the Menu Bar.
    
    ![Click New Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee3f97c0-4e35-419b-b795-92bca9014113/new-level-a.png)
2.  Select the **Default** Level.
    
    ![Select the Default Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34d73c66-e497-41fa-9fda-3b12f15a9da4/select-level-template-a.png)
3.  Select the **Floor** Static Mesh Actor in the **Outliner** and under the **Details** panel, set the **Scale** to X = 10, Y = 10, Z = 1.
    
    ![Select the Floor Static Mesh Actor in the World Outliner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa939b2c-e475-418d-827e-95be94673b4d/create-floor-1.png) ![Set the Scale to X = 10, Y = 10, Z = 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc9ea97a-7dde-44c6-ac0d-48eb4595ec47/create-floor-2.png)
4.  Go to the **Place Actors** panel and search for **NavMeshBoundsVolume**. Drag it into the Level and place it on the floor mesh. Scale the **NavMeshBoundsVolume** to X = 7, Y=10, Z = 1.
    
    ![Drag a Nav Mesh Bounds Volume Actor to the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9aa8a3b9-7459-4b47-ba5b-414002738d03/custom-nav-mesh-drag.png) ![Scale the Nav Mesh Bounds Volume to X = 7, Y=10, Z = 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7754abd1-476c-4268-89a6-afad59622299/avoid-nav-mesh-scale.png)
5.  Go to the **Place Actors** panel and from the **Shapes** category, drag two **Sphere** Actors into the Level.
    
    ![Drag two Sphere Actors into the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aeb20e07-1052-4333-8a62-14f444b5e39d/avoid-sphere-drag-a.png)

### Section Results

In this section, you created a new Level and added a Navigation Mesh. You also added two Sphere Actors that will serve as targets for your Agents.

## 3 - Creating Your Agent

1.  In the **Content Drawer**, right-click and select **New Folder** to create a new folder. Name the folder **NavigationSystem**.
    
2.  In the **Content Drawer**, go to **ThirdPerson > Blueprints** and select the **BP\_ThirdPersonCharacter** Blueprint. Drag it into the **NavigationSystem** folder and select the option **Copy Here**.
    
    ![Drag the Third Person Character Blueprint to the Avoidance folder and select Copy Here](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a701377-6fe6-4431-a632-2a238f088681/move-blueprint-a.png)
3.  Navigate to the **NavigationSystem** folder and rename the Blueprint to **BP\_NPC\_NoAvoidance**. Double-click the Blueprint to open it and go to the **Event Graph**. Select all input nodes and delete them.
    
4.  Right-click the **Event Graph**, then search for and select **Add Custom Event**. Name the event **MoveNPC**.
    
    ![Right-click the Event Graph, then search for and select Add Custom Event. Name the event Move NPC](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7773c4b-2b6d-4056-8063-6d9e7d396e40/custom-event-a.png)
5.  Go to the **My Blueprint** panel and click the **Add (+)** button next to **Variables** to create a new variable. Name the variable **Target**.
    
    ![Click the Add button next to Variables to create a new variable. Name the variable Target](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/641faf90-f6cf-4d51-977c-1e087c7e2c74/custom-npc-target-1.png)
6.  Go to the **Details** panel and click the **Variable Type** dropdown. Search for **Actor** and select the **Object Reference**. Enable the **Instance Editable** checkbox.
    
    ![Set the Variable Type to Actor Object Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b0c3d1b-76c2-4d8d-b80e-5b4cdaba57c6/custom-npc-target-2.png) ![Enable the Instance Editable checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdd626b0-c998-4ffe-867a-32951f664c10/custom-npc-target-3.png)
7.  Drag the **Target** variable into the **Event Graph** and select **Get Target**. Drag from the **Target** node, then search for and select the **Is Valid** macro, as shown below.
    
    ![Drag from the Target node, then search for and select the Is Valid macro](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c16e73d-ef1e-497a-87d0-84f8e6077a29/custom-npc-is-valid.png)
8.  Right-click the **Event Graph**, then search for and select **Get reference to self**.
    
    ![Right-click the Event Graph, then search for and select Get reference to self](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/736f872e-9512-4bf4-9245-aba24badf750/custom-npc-self-a.png)
9.  Right-click the **Event Graph**, then search for and select **AI Move To**.
    
    ![Right-click the Event Graph, then search for and select AI Move To](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c08f114a-91af-4a79-8af6-85f682dd0c3d/avoid-npc-ai-move-to.png)
10.  Connect the **Is Valid** pin of the **Is Valid** node to the **AIMoveTo** node. Connect the **Self** node to the **Pawn** pin of the **AIMoveTo** node. Drag the **Target** variable and connect it to the **Target Actor** pin of the **AIMoveTo** node.
    
    ![Connect the Is Valid node to the AI Move To node. Connect the Target variable to the AI Move To node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09f24b03-7f09-44c2-b8a9-c1c7c606ab18/avoid-npc-ai-move-to-2.png)
11.  Right-click the **Event Graph**, then search for and select **Event Begin Play**. Drag from the **Event Begin Play** node, then search for and select **MoveNPC**.
    
    ![Right click the Event Graph, then search for and select Event Begin Play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c04aaffc-20bd-4ddc-beb2-8827064340f7/custom-npc-begin-play.png) ![Drag from the Event Begin Play node, then search for and select Move NPC](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e1b297d-9aaa-4ab4-ae43-2da24fbfac01/custom-npc-begin-play-2.png)
12.  **Compile** and **Save** the Blueprint. The final Blueprint should look like the image below.
    
    ![This is the final Blueprint setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6524948f-9363-405b-960e-29cf5649f8ec/custom-npc-completed-a.png)
13.  Drag the **BP\_NPC\_NoAvoidance** Blueprint into your Level and from the **Details** panel, click the dropdown next to **Target,** then search for and select the **Sphere** Actor in front of the Agent.
    
    ![Drag the BP_NPC_NoAvoidance Blueprint into your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc64a39e-539a-4919-98b2-1a85519a9377/avoid-npc-drag-1.png) ![Click the dropdown next to Target, then search for and select the Sphere Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f92be6a2-f8ba-42ad-ab0f-14d3096e70b7/avoid-npc-drag-2.png)
14.  Duplicate the **BP\_NPC\_NoAvoidance** Blueprint as seen below.
    
    ![Duplicate the BP_NPC_NoAvoidance Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/673b8f1b-40c5-41ac-bf46-d33dc241fbcc/avoid-npc-drag-3.png)
15.  Repeat the last two steps to create another group of Agents on the opposite side of the Level with the **Sphere** placed in front of them as their target.
    
16.  Click **Simulate** and watch as the Agents navigate toward their goals. Notice how the lack of avoidance creates collisions in the center of the Level.
    
    ![Click Simulate and watch as the Agents navigate toward their goals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/615e8232-59ec-4055-aaec-5d2e65aabd33/avoid-npc-walk-no-avoidance.gif)

### Section Results

In this section, you created an Agent that navigates toward its goal without using avoidance.

## 4 - Adding Reciprocal Velocity Obstacles Avoidance to Your Agent

1.  In the **Content Drawer**, right-click the **BP\_NPC\_NoAvoidance** Blueprint and select **Duplicate**. Name the new Blueprint **BP\_NPC\_RVO**.
    
    ![Duplicate the BP_NPC_NoAvoidance Blueprint and name it BP_NPC_RVO](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7492ba36-c5c7-4502-879a-12cbfb3b312c/avoid-npc-rvo-duplicate-a.png)
2.  Double-click the **BP\_NPC\_RVO** Blueprint to open it in the Blueprint editor. Select the **Character Movement** component and in the **Details** panel, navigate to the **Character Movement: Avoidance** section.
    
    ![Select the Character Movement component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7b6b162-6bd0-48b2-abeb-e0576d046a11/avoid-npc-rvo-select-component.png) ![Go to the Avoidance section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/112be2aa-3f83-48d1-9433-2a236bd86028/avoid-npc-rvo-settings-1.png)
3.  Enable the **Use RVOAvoidance** checkbox and set **Avoidance Consideration Radius** to **100**.
    
    ![Enable the Use RVOAvoidance checkbox and set Avoidance Consideration Radius to 100](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c7157ac-c0aa-41b2-b4d8-b73dca038ac7/avoid-npc-rvo-settings-2.png)
4.  **Compile** and **Save** the **Blueprint**. Reciprocal Velocity Obstacles avoidance is now enabled in your Agent.
    
5.  Drag several **BP\_NPC\_RVO** Blueprints to your Level and follow the same configuration as before. Click **Simulate** to see the results.
    
    ![Drag several BP_NPC_RVO Blueprints to your Level and follow the same configuration as before](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5021f905-08dc-4f60-bc61-e2192a2123f2/avoid-npc-walk-rvo-a.gif)

### Section Results

In this section, you learned how to add Reciprocal Velocity Obstacles avoidance to your Agent.

## 5 - Adding Detour Crowd Avoidance to Your Agent

1.  In the **Content Drawer**, right-click the **BP\_NPC\_NoAvoidance** Blueprint and select **Duplicate**. Name the new Blueprint **BP\_NPC\_DetourCrowd**.
    
    ![Duplicate the BP_NPC_NoAvoidance Blueprint and name it BP_NPC_DetourCrowd](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0c29b87-f588-417e-8cf2-b20014ecef57/avoid-npc-rvo-duplicate-a.png)
2.  Double-click the **BP\_NPC\_DetourCrowd** Blueprint to open it. Go to the **Details** panel and search for **AI Controller**.
    
    ![Go to the Details panel and search for AI Controller](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3378578-9db1-43ae-872a-1c68d14a6c09/avoid-npc-detour-controller-1.png)
3.  Click the dropdown next to **AI Controller Class** and select **DetourCrowdAIController**.
    
    ![Click the dropdown next to AI Controller Class and select Detour Crowd AI Controller](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fa10aef-da5e-4275-8024-84cd621463a8/avoid-npc-detour-controller-2.png)
4.  **Compile** and **Save** your Blueprint. Detour Crowd avoidance is now enabled in your Agent.
    
5.  Drag several **BP\_NPC\_DetourCrowd** Blueprints to your Level and follow the same configuration as before. Click **Simulate** to see the results.
    
    ![Drag several BP_NPC_DetourCrowd Blueprints to your Level and follow the same configuration as before](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e916572-864a-4a5c-82a9-31158fe620ee/avoid-npc-walk-detour-a.gif)
6.  You can adjust the **Detour Crowd Manager** settings by going to **Settings > Project Settings** and navigating to the **Crowd Manager** section.
    
    ![Click Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98134686-da08-45fa-ac23-f293a17894d9/avoid-project-settings-1.png)
7.  In this section, you can adjust several settings for the **Detour Crowd Manager** system, such as the **Max Agents** used by the system and the **Max Agent Radius** used for the avoidance calculation.
    
    ![In this section you can adjust several settings for the Detour Crowd Manager system](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7c9a8c1-a6a8-4716-bd19-29fa58cefa8a/avoid-project-settings-2.png)

## Section Results

In this section, you learned how to add Detour Crowd avoidance to your Agent.
# Modifying the Navigation Mesh

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-how-to-modify-the-navigation-mesh-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-how-to-modify-the-navigation-mesh-in-unreal-engine)  
**Processed:** 2025-06-14 16:40:55

---

## Overview

Unreal Engine's **Navigation System** provides pathfinding capabilities to Artificial Intelligence Agents. To make it possible to find a path between a start location and a destination, a Navigation Mesh is generated from the world's collision geometry.

Default settings subdivide the Navigation Mesh into tiles to allow localized parts of the Navigation Mesh to be rebuilt. The resulting mesh is made of polygons with a cost assigned to each polygon. While determining the optimal path, the pathfinding algorithm will attempt to determine the path with the lowest cost to the destination.

The Navigation System includes a variety of components and settings that modify the way the Navigation Mesh is generated, including the cost of polygons. This, in turn, affects the way Agents navigate through your Level.

## Goals

In this Quick Start guide, you will learn how to modify the Navigation Mesh using **Navigation Modifier Volumes**, **Navigation Proxy Links**, and Blueprint Actors that affect navigation at runtime.

## Objectives

-   Use Navigation Modifier Volumes to alter the Navigation Mesh cost in specific areas
    
-   Use Navigation Proxy Links to create connections between two areas that are otherwise inaccessible
    
-   Use Smart Proxy Links to allow your Agents to jump between platforms toward their goal
    
-   Create moving Blueprint Actors to learn how the Navigation Mesh can be regenerated dynamically at runtime
    

## 1 - Required Setup

Follow the **Modifying the Navigation System preparation guide** or download the [full sample project](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/651c6d3d-bc90-4fe5-b9fa-66e7379b71fe/navsystemsample.zip) and open the **LevelModNavigation\_0** Level before proceeding to the next section.

## 2 - Using Navigation Modifier Volumes

A **Navigation Modifier Volume** applies a Navigation Area Class to the Navigation Mesh using a volume shape. This can be used to change the properties of the polygons within the volume space to modify their traversal cost.

The polygon properties are defined by the appropriate **Area Class** of the Navigation Modifier Volume. This class determines the effect on the Navigation Mesh. You can use the built-in classes to modify the mesh or create your custom implementations.

You will now start by using the built-in classes to modify the Navigation Mesh in your Level.

1.  Go to the **Place Actors** panel and search for **Nav Modifier Volume**. Drag the Nav Modifier Volume Actor into your Level. Notice that by default, no Navigation Mesh is generated inside the volume.
    
    ![Drag the Nav Modifier Volume Actor into your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9107fe31-ccd9-42f4-8921-faf0521429f7/mod-nav-mod-drag.png)
2.  **Move** and **scale** the volume to cover the area shown below. Notice how you are now forcing the Agent to reach the bottom **sphere** by moving around the volume on the left side of the Level. This area could represent any obstacle the Agent is not allowed to cross in your game.
    
    ![Move and scale the volume to cover the area as shown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70dd71e4-0163-4732-b673-6e350f4250ce/mod-nav-mod-null-1.png)
3.  Repeat the step above and create another area on the opposite side of the map. When you scale the volume, leave space on both sides for the Agent to navigate.
    
    ![Repeat the step above and create another area on the opposite side of the map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/949c9f20-dd23-48a7-bc44-41d96b5bfe17/mod-nav-mod-null-2.png)
4.  Drag another **Nav Modifier Volume** into your Level. Navigate to the **Details** panel and click the **dropdown** next to **Area Class**. Select the **NavArea\_Obstacle** class from the list. This built-in class assigns the area inside the volume a higher cost of navigation compared to the default value (**NavArea\_Default** in green). This will cause your Agent to avoid the area unless it cannot find a cheaper path to its destination.
    
    ![Select the NavArea_Obstacle class from the list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61ce3e67-24ef-4ad1-a901-a02d92952248/mod-nav-mod-obs-1.png) ![The area inside the volume has a higher navigation cost compared to the default navigation mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0a2dfbd-f29b-4797-9c0c-3c815eb9ce87/mod-nav-mod-obs-2.png)
5.  Duplicate the volume twice to form the following shape around the sphere. This will force the Agent to navigate around the volumes to reach the sphere.
    
    ![Duplicate the volume twice](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/131110ea-41aa-42ef-bc09-c5b588271ef4/mod-nav-mod-obs-3.png)
    
    If you completely block the area around the sphere with another volume, the Agent will still reach its destination because the volumes represent a valid path. In contrast, if you were to change the Area Class of the volumes to NavArea\_Null, the Agent will not be able to reach its destination as it will not be able to find a suitable path to its target. This is because the NavArea\_Null applies an infinite cost which causes the Navigation Mesh to not be generated in the affected area.
    
6.  Click **Simulate** and notice how your Agent moves between the spheres. This illustrates how your changes have affected the way the Navigation Mesh was generated.
    
    ![Click Simulate and notice how your Agent moves between the spheres](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/617c15d9-357f-44ce-aa1d-1d32751e95b2/mod-nav-mod-demo.gif)

### Section Results

In this section, you learned how to use **Nav Modifier Volumes** to change the way the Navigation Mesh is generated. You also learned about some of the built-in Area Classes available in Unreal Engine.

### Available Nav Modifier Volume Area Classes

| Area Class | Description |
| --- | --- |
| NavArea\_Default | Assigns the same navigation cost to the area inside the volume and the Navigation Mesh by default. |
| NavArea\_LowHeight | Represents an area that matches the conditions for traversal with a low height that prevents an Agent from traversing it. The Navigation Mesh will not generate navigation data inside this volume. |
| NavArea\_Null | Represents an empty area inside the volume. The Navigation Mesh will not generate navigation data inside this volume. |
| NavArea\_Obstacle | Assigns a high navigation cost to the area inside the volume. |

## 3 - Using Navigation Link Proxies

**Navigation Link Proxies** connect two areas of the Navigation Mesh that don't have a direct navigation path. While a path is being searched, Navigation Link Proxies are used as extra connections that Agents can use to reach their destination.

Navigation Link Proxies are commonly used to build bridges between areas with separate Navigation Meshes and to instruct Agents that they can fall or jump from a platform towards their goal when there is no continuous navigation path available.

**Creating Bridges to Connect Two Areas**

1.  Select the first **Nav Modifier Volume** and resize it so it covers the entire length of the floor, as seen below. This blocks the Agent from reaching the bottom sphere in the Level.
    
    ![Select the first Nav Modifier Volume and resize it so it covers the entire length of the floor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42295d4f-b81c-486e-9d77-4e685c934717/mod-nav-link-nav-mod-resize.png)
2.  Go to the **Place Actors** panel and drag a **Cube** Actor into the Level. Scale it to X = 4, Y = 1, Z =0.2 and place it as shown below.
    
    ![Drag a Cube Actor into the Level. Scale it to X = 4, Y = 1, Z =0.2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9b04ba0-0a62-44f7-9158-3e9c5de7bf64/mod-nav-link-cube-1.png)
3.  Duplicate the **cube** and move it to the other side of the Level, as shown below.
    
    ![Duplicate the cube and move it to the other side of the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5180149-8f55-4e6f-a4b2-407ec81846a7/mod-nav-link-cube-2.png)
    
    These Cube Actors serve as a visual representation of the Navigation Link Proxies in the Level. You are not required to use them in conjunction with Navigation Link Proxies.
    
4.  Go to the **Place Actors** panel and search for **Nav Link Proxy**. Drag the **Nav Link Proxy** Actor into your Level.
    
    ![Drag the Nav Link Proxy Actor into your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/958bff43-e713-497d-a9f5-08ee0cdf540e/mod-nav-link-drag.png)
5.  With the **Nav Link Proxy** selected, click the **PointLinks\[0\].Left** handle and move it so it's placed on one side of the mesh. Click the **PointLinks\[0\].Right** handle and move it so it's placed on the opposite side of the mesh, as shown below.
    
    The green arrow will disappear if the Nav Link Proxy doesn't connect with the surface of the Navigation Mesh.
    
    ![Click the PointLinks[0].Left handle and move it so it's placed on one side of the mesh and the PointLinks[0].Right handle on the opposite side](mod-nav-link-bridge-1.png)(convert:false)
    
    Now that you have created a connection, the Agent will be able to navigate through the **Nav Link Proxy**, even though there is no navigation data in between.
    
6.  With the **Nav Link Proxy** selected, go to the **Details** panel and expand the section labeled **0** under **Point Links** to find the **Direction** dropdown. You can choose to have the **Direction** be **Both Ways**, **Left to Right**, or **Right to Left**. For this example, select **Left to Right**.
    
    ![Click the Direction dropdown and select Left to Right](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0a2ceb4-8b8b-49a6-896f-9093fa965b4a/mod-nav-link-direction.png)
7.  Duplicate the **Nav Link Proxy** and move it to the other side of the level. For this example, set the **Direction** to **Right to Left**.
    
    ![Duplicate the Nav Link Proxy and move it to the other side of the level. Set the Direction to Right to Left](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/454327b0-fe10-4386-949e-eda72c043088/mod-nav-link-bridge-2.png)
8.  Click **Simulate** and notice how your Agent can now reach the **sphere** by entering from the left side and exiting from the right side.
    
    ![Click Simulate and notice how your Agent can now reach the sphere by entering from the left side and exiting from the right side](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbd94e7e-b3ab-4db8-baff-59acacf8ab16/mod-nav-link-demo.gif)

### Section Results

You used **Nav Link Proxies** to connect two areas of the **Navigation Mesh** that did not have a viable path. You also learned that you could configure the **Nav Link Proxies** to have different directions, such as **Both Ways**, **Left to Right**, or **Right to Left**.

### Using a Nav Link Proxy to Allow Your Agent to Fall from a Platform

1.  Drag another **Nav Link Proxy** into your Level and place it at the end of the raised platform, as seen below.
    
    ![Drag another Nav Link Proxy into your Level and place it at the end of the raised platform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3fae8d5-9206-4bdc-9e2b-b0d4091e6366/mod-nav-link-fall-1.png)
2.  Select the **PointLinks\[0\].Left** and place it at the platform's edge and select the **PointLinks\[0\].Right** and place it at the bottom overlapping the floor.
    
    ![Select the PointLinks[0].Left and place it at the edge of the platform and select the PointLinks[0].Right and place it at the bottom](mod-nav-link-fall-2.png)(convert:false)
    
3.  Navigate to the **Details** panel, expand the section labeled **0** under **Point Links** and select **Left to Right** as the **Direction**.
    
    ![Set the Direction Left to Right](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b7c31ae-50c3-4012-b71c-1bb2e616981f/mod-nav-link-fall-3.png)
4.  Click **Simulate** and notice how your Agent is now able to fall from the platform to reach its goal.
    
    ![The Agent is now able to fall from the platform to reach its goal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94793ea8-0c6f-4656-9f49-eeee8ca50291/mod-nav-link-demo-2.gif)

#### Section Results

In this section, you used a **Nav Link Proxy** to allow your Agent to fall from a platform to reach its goal.

### Using a Nav Link Proxy to Allow Your Agent to Jump to Its Goal

In this section, you will learn how to use a **Smart Link** on a **Nav Link Proxy** to allow your Agent to jump from one platform to another.

1.  Select the platform mesh and drag it while holding the **Alt** key to the side to duplicate it.
    
    ![Select the platform mesh and drag it while holding the Alt key to the side to duplicate it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce72aff0-0527-4871-ac17-6fdd7ef52b2f/mod-smart-link-platform-1.png)
2.  Resize the new platform and move it higher, as shown below.
    
    ![Resize the new platform and move it higher](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/685f9624-425f-4f0a-ab3f-6d34b949bde8/mod-smart-link-platform-2.png)
3.  Duplicate a **Sphere** Actor and place it on top of the platform.
    
    ![Duplicate a Sphere Actor and place it on top of the platform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecdf7466-a1e8-428b-af25-67688057722c/mod-smart-link-platform-3.png)
4.  Inside the **Content Drawer**, right-click and select **Blueprint Class** from the **Create Basic Asset** section.
    
    ![Select Blueprint Class from the Create Basic Asset section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/006c0f2d-6ee9-46e5-be89-25a3f7b51459/mod-smart-link-create-1.png)
5.  Inside the **Pick Parent Class** window, go to the **All Classes** section and expand the arrow. Search for and select **Nav Link Proxy** and click **Select**. Name the Blueprint **BP\_NavProxyLink**.
    
    ![ Search for and select Nav Link Proxy and click Select](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b2ed2ba-acc3-492f-ac9f-171b74a9ac20/mod-smart-link-create-2.png) ![Name the Blueprint BP_NavProxyLink](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61e7529a-f7b3-4a0d-a5e7-c60938ecfaf1/mod-smart-link-create-3.png)
6.  Open **BP\_NavProxyLink** by double-clicking it. Inside the **Event Graph**, right-click then search for and select **Event Receive Smart Link Reached**.
    
    ![Inside the Event Graph, right-click then search for and select Event Receive Smart Link Reached](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81843b25-97e3-4bd4-b569-8d155e224365/mod-smart-link-blueprint-event.png)
7.  Drag from the **Agent** pin of the **Event Receive Smart Link Reached** node then search for and select **Cast to Character**.
    
    ![Drag from the Agent pin of the Event Receive Smart Link Reached node then search for and select Cast to Character](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0568a058-9d78-4e88-a413-06aa0710734e/mod-smart-link-blueprint-cast.png)
8.  Drag from the **As Character** pin of the **Cast to Character** node and select **Promote to variable**.
    
    ![Drag from the As Character pin of the Cast to Character node and select Promote to variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/972d0052-2e5a-4f3d-911d-556c05674836/mod-smart-link-blueprint-character.png)
9.  Drag from the **execution** pin of the **As Character** node then search for and select **Suggest Projectile Velocity Custom Arc**.
    
    ![Drag from the As Character node then search for and select Suggest Projectile Velocity Custom Arc](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38ba3919-c559-4ab9-8dd4-be5c11d71ca2/mod-smart-link-blueprint-custom-arc.png)
10.  Drag from the **blue** pin of the **As Character** node then search for and select **Get Actor Location**. Connect the **Return Value** pin of the **Get Actor Location** node to the **Start Pos** pin of the **SuggestProjectileVelocityCustomArc** node.
    
    ![Drag from the As Character node then search for and select Get Actor Location. Connect the node to the Start Pos pin of the Suggest Projectile Velocity Custom Arc node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbce22f6-76a9-4b96-9998-2163896276dc/mod-smart-link-blueprint-start-pos.png)
11.  Drag from the **Destination** pin of the **Event Receive Smart Link Reached** node and connect it to the **End Pos** pin of the **SuggestProjectileVelocityCustomArc** node.
    
    ![Drag from the Destination pin of the Event Receive Smart Link Reached node and connect it to the End Pos pin of the Suggest Projectile Velocity Custom Arc node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56ed17e2-5dbf-4627-a083-0ac8a2dbf588/mod-smart-link-blueprint-end-pos.png)
12.  Drag the **As Character** variable into the **Event Graph** and select **Get As Character**. Drag from the node then search for and select **Launch Character**. Enable the **XYOverride** and **ZOverride** checkboxes.
    
    ![Drag from the As Character node then search for and select Launch Character](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c29a9a3f-0559-4618-818e-e2886d3ba992/mod-smart-link-blueprint-launch-character-1.png)
13.  Drag from the **SuggestProjectileVelocityCustomArc** node then search for and select **Delay**. Set the **Duration** to 0.1. Connect the **Completed** pin of the **Delay** node to the **Launch Character** node.
    
    ![Add a Delay node and set the Duration to 0.1. Connect the Delay node to the Launch Character node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b05b938-1a78-4c34-8d6c-c01743fa52b6/mod-smart-link-blueprint-delay.png)
14.  Drag from the **Out Launch Velocity** pin of the **SuggestProjectileVelocityCustomArc** node then search for and select **vector \* float**.
    
    ![Drag from the Out Launch Velocity pin of the Suggest Projectile Velocity Custom Arc node then search for and select vector * float](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f6c566e-d44b-47a1-99ee-5a1ef6bec250/mod-smart-link-blueprint-jump-boost-1.png)
15.  Connect the **yellow** pin of the **Multiplication** node to the **Launch Velocity** pin of the **Launch Character** node. Right-click the **green** pin of the **Multiplication** node and select **Promote to variable**.
    
    ![Right click the green pin of the Multiplication node and select Promote to variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3860c4f9-80b5-4012-9cfa-d8dacb54b88d/mod-smart-link-blueprint-jump-boost-2.png)
16.  With the **New Var 0** node selected, go to the **Details** panel and rename the variable to **JumpBoost**. Set the default value to **1**. Enable the **Instance Editable** checkbox, as shown below.
    
    ![Name the Variable Jump Boost and set the default value to 1. Enable the Instance Editable checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6da73d55-db54-484e-9c92-b5865752e757/mod-smart-link-blueprint-jump-boost-3.png)
17.  **Compile** and **Save** your Blueprint.
    
    ![This is the complete Blueprint set up](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea9c6fca-aae5-4a51-84fa-ec70a091dfea/mod-smart-link-blueprint-final.png)
18.  Select the **BP\_NPC\_ModNavMesh** character in your Level and under the **Details** panel, click on the **Add (+)** button next to **Target List** to add a new entry. Search for and select the last **Sphere** Actor you added to the platform.
    
    ![Search for and select the last Sphere Actor you added to the platform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fffd3767-249a-4d71-b539-0cf458fb3b21/mod-npc-targets-2.png)
19.  Drag the **BP\_NavProxyLink** Blueprint Actor onto the platform and adjust the connections, as seen below.
    
    ![Drag the BP_NavProxyLink Blueprint Actor onto the platform and adjust the connections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c0bf79e-6a0d-49a0-a0ad-0ace4a3cf566/mod-smart-link-blueprint-drag.png)
20.  With the **BP\_NavProxyLink** Blueprint Actor selected, go to the **Details** panel and click the **Copy End Points from Simple Link to Smart Link** button. Enable the **Smart Link Is Relevant** checkbox.
    
    ![click the Copy End Points from Simple Link to Smart Link button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1123bca-76ef-4ab4-b179-42bf79c78a67/mod-smart-link-blueprint-drag-2.png)
21.  Click **Simulate** and watch as your Agent can now jump to reach the last sphere.
    
    ![Click Simulate and watch as your Agent can now jump to reach the last sphere](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb585471-5878-4bfb-958f-578cfbaa8587/mod-nav-link-demo-3.gif)
    
    Nav Link Proxies can only connect adjacent Navigation Mesh tiles. You can visualize the tiles by selecting the RecastNavMesh-Default Actor and enabling the Draw Tile Bounds checkbox.
    

### Section Results

In this section you learned how to create a custom **Nav Proxy Link** Blueprint and how it can be used to get your Agent to jump to a platform.

## 4 - Generating the Navigation Mesh at Runtime

Unreal Engine comes with three Navigation Mesh generation modes:

| Generation Mode | Description |
| --- | --- |
| Static | The Navigation Mesh is generated offline and is saved with the Level. The Navigation Mesh is loaded at runtime and cannot change. |
| Dynamic | The Navigation Mesh is generated offline and is saved with the Level or built at runtime. At runtime, the navigation-relevant data used by the Navigation Mesh can be updated and the generation is performed on the tiles affected by the change in the data. |
| Dynamic Modifiers Only | 
The Navigation Mesh is generated offline and is saved with the Level. At runtime, only Navigation Modifiers such as Navigation Areas, Navigation Links, and dynamic objects, can modify the existing Navigation Mesh by changing the cost or block areas. No new Navigation Mesh surfaces are generated at runtime.

This method allows the Navigation Mesh to cache collision data and can result in up to 50% cheaper processing of the affected tiles.

Advanced users should use this mode after careful consideration of its benefits and limitations.



 |

By default, the Navigation Mesh is configured to be **Static**. However, you can set your Navigation Mesh generation to one of the dynamic modes so it can change at runtime.

### Using the Runtime Generation (Dynamic Modifiers Only)

1.  To change the **Runtime Generation** settings, go to **Settings > Project Settings** on the menu bar.
    
    ![Click Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c4cb5cd-1fac-4d49-8ede-4d58c255fb29/mod-dyn-project-settings-1.png)
2.  Go to the **Navigation Mesh** settings and under the **Runtime** section, click the **Runtime Generation** dropdown. Select **Dynamic Modifiers Only** for this example.
    
    ![Click the Runtime Generation dropdown and select Dynamic Modifiers Only](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d13cc8b-ce8f-4242-b305-ce54851ed943/mod-dyn-project-settings-2.png)
3.  Inside the **Content Drawer**, right-click and select **Blueprint Class** under the **Create Basic Asset** section.
    
    ![Select Blueprint Class under the Create Basic Asset section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8070077f-be53-4775-adad-5cbf25b9137d/mod-smart-link-create-1.png)
4.  Select the **Actor** class under the **Common** section. Name the Blueprint **BP\_RotatingActor**.
    
    ![Select the Actor class under the Common Classes section](mod-rot-create.png)(convert:false)
    
    ![Name the Blueprint BP_RotatingActor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/865d1292-e7cd-4b11-8ef2-dfb6c3c1633d/mod-rot-create-2.png)
5.  Double-click the **BP\_RotatingActor** Blueprint to open it. Click the **+Add** dropdown, then search for and select **Cube**. Scale the Cube to X = 4, Y = 1.5, Z = 1.
    
    ![Click the Add Component dropdown, then search for and select Cube](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94f352a8-f8c5-4f28-be68-e4ce20c6678f/mod-rot-add-cube.png) ![Scale the Cube to X = 4, Y = 1.5, Z = 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e9750f2-b066-48b4-9c9d-d4d2e2a62e58/mod-rot-add-cube-2.png)
6.  Click the **+Add** dropdown, then search for and select **Rotating Movement**.
    
    ![Click the **Add Component** dropdown, then search for and select Rotating Movement](mod-rot-rotate.png)(convert:false)
    
7.  **Compile** and **Save** the Blueprint.
    
8.  Drag the **BP\_RotatingActor** Blueprint Actor into your Level and click **Simulate**. Notice how the Navigation Mesh does not update with the rotating mesh. This is because the **Dynamic Modifier Only** Runtime Generation mode will only work if the Actor has a **NavModifier** component.
    
    ![Drag the BP_RotatingActor Blueprint Actor into your Level and click Simulate](mod-rot-demo.gif)(convert:false)
    
9.  Go back to the **BP\_RotatingActor** Blueprint and click the **+Add** dropdown. Search for and select **Nav Modifier**.
    
    ![Click the Add Component dropdown and search for and select Nav Modifier](nav-modifier.png)(convert:false)
    
10.  **Compile** and **Save** the Blueprint. Click **Simulate** to see the difference. You should now see the Navigation Mesh correctly updating as the mesh rotates in the Level.
    
    Notice how no new Navigation Mesh is being generated in the Level (the tiles being generated are displayed in red). The Navigation Modifier is simply changing the existing Navigation Mesh.
    
    ![You should now see the Navigation Mesh correctly updating as the mesh rotates in the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7dea215-4bac-4201-8415-df5de8770775/mod-rot-demo-2.gif)

### Section Results

In this section, you learned how to make the Navigation Mesh regenerate during gameplay by using the Runtime Generation **Dynamic Modifiers Only**. You also tested the results using a simple rotating Blueprint Actor with the NavModifier component.

### Using the Runtime Generation (Dynamic)

1.  Inside the **Content Drawer**, right-click and select **Blueprint Class** from the **Create Basic Asset** section.
    
    ![Select Blueprint Class from the Create Basic Asset section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b8a9b1b-d63b-44a9-970a-2460804cbbec/mod-smart-link-create-1.png)
2.  Select the **Actor** class under the **Common** section. Name the Blueprint **BP\_MovingActor**.
    
    ![Select the Actor class under the Common Classes section](mod-rot-create.png)(convert:false)
    
    ![Name the Blueprint BP_MovingActor](mod-moving-create.png)(convert:false)
    
3.  Double-click the **BP\_MovingActor** Blueprint to open it. Click the **+Add** dropdown, then search for and select **Sphere**. Scale the Sphere to X = 2, Y = 2, Z = 2.
    
    ![Click the Add Component dropdown, then search for and select Sphere](mod-moving-sphere.png)(convert:false)
    
4.  In the **Event Graph**, right-click, then search for and select **Add Custom Event**. Name the event **MoveForward**. Repeat these steps and create another event named **MoveBackwards**.
    
    ![In the Event Graph, right click, then search for and select Add Custom Event. Name the event Move Forward](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77928e47-2595-4e95-845e-0d5ee8b8a6e7/mod-moving-custom-event-1.png) ![Repeat these steps and create another event named Move Backwards](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c147a74-c75c-4e20-926b-bfd9b907a89f/mod-moving-custom-event-2.png)
5.  Drag from the **MoveForward** node then search for and select **Add Timeline**. Name the Timeline **TM\_MoveObject**. Connect the **MoveBackwards** node to the **Reverse** pin of the **TM\_MoveObject** node.
    
    ![Drag from the Move Forward node then search for and select Add Timeline](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8ec1be7-64a3-4636-9420-33ba8cefa923/mod-moving-add-tm.png) ![Connect the Move Backwards node to the Reverse pin of the Timeline](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca706053-59b0-4219-afc1-4b584f807cdc/mod-moving-add-tm-2.png)
6.  Double-click the **TM\_MoveObject** node to open it. Click the **+Track** button to create a new Float Track. Name the track **Alpha**.
    
    ![Click the Add Float Track button to create a new Float Track.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a5e21c5-2709-486c-8fad-864cb2cf2225/add-float-track-button.png)
    
    ![Name the track Alpha](mod-moving-tm-alpha.png)(convert:false)
    
7.  Right-click inside the graph and select **Add key to CurveFloat\_1**. Enter Time = **0** and Value = **0**.
    
    ![Right click inside the graph and select Add key to CurveFloat_1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4badeede-ba3d-44e6-81d9-26979a81038f/mod-moving-tm-point-1.png) ![Enter Time = 0 and Value = 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5273c02b-a2a9-4f9d-9af2-8e7578e5a302/mod-moving-tm-point-2.png)
8.  Repeat the previous step and enter Time = **5**, Value = **1**.
    
9.  Drag the **Sphere** component into the **Event Graph** to create a node. Drag from the **Sphere** node, then search for and select **Set Relative Location**.
    
    ![Drag from the Sphere node, then search for and select Set Relative Location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92418bad-c37a-466b-8e32-dd57a9422634/mod-moving-relative-location.png)
10.  Connect the **Update** pin of the **TM\_MoveObject** node to the **SetRelativeLocation** node. Right-click the **New Location** pin of the **SetRelativeLocation** node and select **Split Struct Pin**.
    
    ![Right click the New Location pin of the Set Relative Location node and select Split Struct Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbae97fb-2e17-4ea6-bb1a-267f4bfc1d6a/mod-moving-set-location.png)
11.  Drag from the **New Location X** pin of the **SetRelativeLocation** node, then search for and select **Lerp**. Connect the **Alpha** pin of the **TM\_MoveObject** node to the **Alpha** pin of the **Lerp** node.
    
    ![Drag from the New Location X pin of the Set Relative Location node, then search for and select Lerp](mod-moving-lerp.png)(convert:false)
    
    ![Connect the Alpha pin of the TM_MoveObject node to the Alpha pin of the Lerp node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dd49105-b0e8-4590-af1d-f78b4a8b69d4/mod-moving-lerp-2.png)
12.  Right-click the **B** pin of the **Lerp** node and select **Promote to Variable**. Go to the **Details** panel and name the variable **Distance**. Select the **Instance Editable** checkbox.
    
    ![Right click the B pin of the Lerp node and select Promote to Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83de4e52-ee22-42cf-a34f-4c6546a249d3/mod-moving-distance-1.png) ![Name the variable Distance. Select the Instance Editable checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fea2f23-a662-4316-8496-03363ed7be2e/mod-moving-distance-2.png)
13.  **Compile** and **Save** the Blueprint. Set the default value for **Distance** to **1000**.
    
14.  Drag from the **Finished** pin of the **TM\_MoveObject** Timeline, then search for and select **Delay**. Set the **Duration** to **1**.
    
    ![Drag from the Finished pin of the Timeline, then search for and select Delay. Set the Duration to 1](mod-moving-delay.png)(convert:false)
    
15.  Drag from the **Completed** pin of the **Delay** node and search for and select **Branch**.
    
    ![Drag from the Delay node and search for and select Branch](mod-moving-branch.png)(convert:false)
    
16.  Right-click the **Condition** pin of the **Branch** node and select **Promote to Variable**. Go to the **Details** panel and rename the variable to **Forward**.
    
    ![Right click the Condition pin of the Branch node and select Promote to Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1caf78a-794c-4659-b713-f194d7b54a49/mod-moving-branch-2.png) ![Rename the variable to Forward](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2a4e96a-ecba-45cf-ac9a-a79cfbb0da52/mod-moving-branch-3.png)
17.  Drag the **Forward** variable to the **Event Graph** and select **Set Forward**. Connect the **True** pin of the **Branch** to the **Set Forward** node. Drag from the **Set Forward** node, then search for and select **Move Backwards**.
    
    ![Connect the True pin of the Branch to the Set Forward node. Drag from the Set Forward node, then search for and select Move Backwards](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe56d865-2917-45b2-baa5-edf4fb158ddd/mod-moving-branch-4.png)
18.  Drag the **Forward** variable to the **Event Graph** and select **Set Forward**. Connect the **False** pin of the **Branch** to the **Set Forward** node. **Enable** the **Forward** checkbox of the **Set Forward** node. Drag from the **Set Forward** node, then search for and select **Move Forward**.
    
    ![Connect the False pin of the Branch to the Set Forward node. Enable the Forward checkbox. Drag from the Set Forward node, then search for and select Move Forward](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da32156a-4822-4968-a384-ec61025ec7e6/mod-moving-branch-5.png)
19.  Right-click in the **Event Graph**, then search for and select **Event Begin Play**. Drag from the **Event Begin Play** node, then search for and select **Move Forward**.
    
    ![Right click in the Event Graph, then search for and select Event Begin Play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0cdcbe51-46ba-4ddd-852b-67e48209796c/mod-moving-begin-1.png) ![Drag from the Event Begin Play node, then search for and select Move Forward](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b30ea64-ffdc-4351-a9db-f4c04b19dfcd/mod-moving-begin-2.png)
20.  **Compile** and **Save** your Blueprint. You can see the completed Blueprint below.
    
    ![This is the complete Blueprint set up](mod-moving-completed.png)(convert:false)
    
21.  Drag the **BP\_MovingActor** Blueprint Actor into your Level and click **Simulate**. Notice how the Navigation Mesh does not update with the Actor's movement.
    
    ![Drag the BP_MovingActor Blueprint Actor into your Level and click Simulate](mod-moving-demo.gif)(convert:false)
    
22.  Click **Settings > Project Settings** and go to the **Navigation Mesh** settings.
    
    ![Click Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/daf782e2-33f0-4be2-b9ad-e32c57205041/mod-dyn-project-settings-1.png)
23.  Under the **Runtime** section, click the **Runtime Generation** dropdown and select **Dynamic.**
    
    ![Click the Runtime Generation dropdown and select Dynamic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a9d6c6d-67fd-4297-9fd0-57f294639dfc/mod-dyn-project-settings-3.png)
24.  Go back to the Level and click **Simulate**. You should now see the Navigation Mesh update correctly.
    
    The examples used in this section force the constant runtime generation of the Navigation Mesh which has a high computational cost. These examples do not represent best practices and are used for demonstration purposes only.
    
    ![The Navigation Mesh updates correctly with the moving Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acbc95cd-e45b-47f7-bc43-365b5af25c1e/mod-moving-demo-2.gif) ![The Navigation Mesh updates correctly with the rotating Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79f5cc3e-bede-4c51-8334-2cac7323ebf5/mod-moving-demo-3.gif) ![Final set up for the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08f6980e-9794-423a-bc45-7035b66c66c3/mod-moving-demo-4.gif)

### Section Results

In this section, you learned that you can make the Navigation Mesh regenerate during gameplay using the **Dynamic** Runtime Generation setting. You also tested the results by creating a Blueprint that moves a Sphere mesh in the Level and forces constant Navigation Mesh regeneration.
# Custom Navigation Areas and Query Filters Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/custom-navigation-areas-and-query-filters-quick-start-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/custom-navigation-areas-and-query-filters-quick-start-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:12

---

## Overview

Unreal Engine's **Navigation System** allows Agents to traverse the Level using a **Navigation Mesh** for pathfinding.

The Agent determines the most optimal route to its destination by comparing the cost of each navigation polygon within the Navigation Mesh. If all polygons along the route are of equal cost, then the Agent will choose the shortest path to its target (usually a straight line).

You can influence the cost of the navigation polygons using **Navigation Modifier Volumes** and **Navigation Query Filters**.

Navigation Modifier Volumes use **Area Classes** to determine the **Default Cost** multiplier of navigation within the volume. Area Classes also define the **Fixed Area Entering Cost**, which is the initial cost applied when the Agent enters the area. You can create as many Area Classes as needed to influence how your Agents navigate your Level.

**Navigation Query Filters** contains information about one or more Area Classes and can override the cost values if needed. You can create as many Query Filters as needed to further customize how your Agents navigate your Level.

## Goals

In this Quick Start Guide, you will learn to create and use your Navigation Areas and Query Filters to influence how different Agents traverse the same Navigation Mesh toward their targets.

## Objectives

-   Create three custom Area Classes to use with Navigation Modifier Volumes.
    
-   Create two Navigation Query Filters to be used by Agents.
    

## 1 - Creating Custom Area Classes

1.  Go to the **Place Actors** panel and search for **Nav Modifier Volume**. Drag the **Nav Modifier Volume** Actor into your Level and place it on the Floor mesh. Go to the **Details** panel and set the **Scale** to X = 2, Y = 6, Z = 1.
    
    ![Drag the Nav Modifier Volume Actor into your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e9ac5b1-aba1-4be4-8dba-f7ce367c6bd0/custom-nav-mod-drag-1.png) ![Set the Scale to X = 2, Y = 6, Z = 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09b0ae33-6946-44ae-bf23-eaa2d945bbcd/custom-nav-mod-drag-2.png)
2.  Inside the **Content Drawer**, right-click and select **Blueprint Class** under the **Create Basic Asset** section.
    
    ![Select Blueprint Class under the Create Basic Asset section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0aa9396e-da02-416f-ad46-7ef571a1a7b9/blueprint-class-a.png)
3.  Inside the **Pick Parent Class** window, go to the **All Classes** section and expand the arrow. Search for and select **Nav Area.** Click **Select** and name the Blueprint **BP\_Area\_Neutral**.
    
    ![Go to the All Classes section and expand the arrow. Select Nav Area](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2ec0fd6-df37-469d-90a7-1e7665a5991a/custom-nav-area-create-1.png) ![Name the Blueprint BP_Area_Neutral](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a6da4be-92e2-49a4-baf5-574bd55400c3/custom-nav-area-create-2.png)
4.  Repeat the previous two steps twice and name these Blueprints **BP\_Area\_Lane1** and **BP\_Area\_Lane2.**
    
5.  Double-click the **BP\_Area\_Lane1** Blueprint to open it. You can modify the **Default Cost** multiplier when navigating inside the volume and the **Fixed Area Entering Cost**. For this example, leave the settings at their default values.
    
6.  Click the **Draw Color** bar and select a **blue** color. **Compile** and **Save**.
    
    ![Click the Draw Color bar and select a blue color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47801714-69c8-400d-9a47-e35184403c61/custom-nav-area-blue.png)
7.  Repeat the step above for the **BP\_Area\_Lane2** Blueprint and change its **Draw Color** to **red**.
    
8.  Select the **Nav Modifier Volume** in your Level, and on the **Details** panel, click the **Area Class** dropdown and select **BP\_Area\_Neutral**.
    
    ![Select BP_Area_Neutral from the dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e144795-abec-45d2-83ef-8e22f160bffa/custom-nav-mod-neutral.png) ![Notice how the area changes color in the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40365efc-b792-4254-a390-4b80d7212c7a/custom-nav-mod-neutral-2.png)
9.  Duplicate the **Nav Modifier Volume** and follow the steps above to change the **Area Class** to **BP\_Area\_Lane1**. Move the volume to the side to create a lane as seen below.
    
    ![Duplicate the Nav Modifier Volume and follow the steps above to change the Area Class to BP_Area_Lane 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d502242b-42ba-4493-89c0-78d8c450f15c/custom-nav-mod-lane-1.png)
10.  Repeat the previous step to duplicate the **Nav Modifier Volume** and set the **Area Class** to **BP\_Area\_Lane2**. Move the volume to the side to create a lane as seen below.
    
    ![Duplicate the Nav Modifier Volume and follow the steps above to change the Area Class to BP_Area_Lane 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3b9016f-2fad-4f5c-aaae-4a02a203b8b4/custom-nav-mod-lane-2.png)
11.  You can now experiment by changing the values of each **Area Class** to influence the Agent's path to its target. In the example below, the **Default Cost** of **BP\_Area\_Neutral** and **BP\_Area\_Lane1** are both set to 4.
    
    ![In this example the Default Cost of BP_Area_Neutral and BP_Area_Lane 1 are both set to 4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c70f8956-e544-4cbf-b2c1-da68d4bc9dd0/custom-npc-walk-2.gif)
12.  In this example, the **Default Cost** of **BP\_Area\_Neutral** and **BP\_Area\_Lane2** are both set to 4.
    
    ![In this example the Default Cost of BP_Area_Neutral and BP_Area_Lane 2 are both set to 4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b07fc886-285e-4429-b35b-ce01885d56bb/custom-npc-walk-3.gif)

### Section Results

In this section, you created three custom **Area Classes** and placed them in your Level. You also changed the **Default Cost** values of these **Area Classes** to influence the Agent's navigation towards its target.

## 2 - Creating Navigation Query Filters

1.  Inside the **Content Drawer**, right-click and select **Blueprint Class** under the **Create Basic Asset** section.
    
    ![Select Blueprint Class under the Create Basic Asset section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b8e3594-0979-49f4-af5f-8cbdcdf7234f/blueprint-class-a.png)
2.  Inside the **Pick Parent Class** window, go to the **All Classes** section and expand the arrow. Search for and select **Navigation Query Filter.** Click **Select** and name the Blueprint **BP\_QueryFilter1**.
    
    ![Search for and select Navigation Query Filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01822efb-a98b-4f1b-baac-51c42a113318/custom-filter-create-1.png) ![Name the Blueprint BP_QueryFilter 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/966dd139-7a38-47de-9d3b-24f4a51d3ab7/custom-filter-create-2.png)
3.  Double-click the **BP\_QueryFilter1** Blueprint to open it. Click on the **Add (+) button** next to the **Areas** section to expand it.
    
    ![Click on the Add button next to the Areas section to expand it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bb66ceb-c449-4495-a7a4-9da12449612e/custom-filter-filter-1a.png)
4.  Click the dropdown next to **Area Class** and search for and select **BP\_Area\_Neutral**. Enable the **Travel Cost Override** checkbox and enter **100**.
    
    ![Click the dropdown next to Area Class and search for and select BP_Area_Neutral](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/571a15e9-0055-42e7-a35c-f2961191c013/custom-filter-filter-1b.png) ![Enable the Travel Cost Override checkbox and enter 100](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91ee0074-4341-46b7-a628-89e16bb2918b/custom-filter-filter-1c.png)
5.  Repeat the previous step to add **BP\_Area\_Lane1** and **BP\_Area\_Lane2** to the list. For **BP\_Area\_Lane2**, enable the **Travel Cost Override** checkbox and enter 100.
    
    ![Repeat the previous step to add BP_Area_Lane 1 and BP_Area_Lane 2 to the list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3689197b-56d2-48e8-b7ba-f96cb2357139/custom-filter-filter-1d.png)
6.  In the **Content Drawer**, right-click the **BP\_QueryFilter1** Blueprint and select **Duplicate**.
    
7.  Double-click the **BP\_QueryFilter2** Blueprint to open it. For the Area Class **BP\_Area\_Lane1**, enable the **Travel Cost Override** checkbox and set its value to 100. For the Area Class **BP\_Area\_Lane2**, disable the **Travel Cost Override** checkbox.
    
    ![Enable Travel Cost Override for BP_Area_Lane 1 and disable Travel Cost Override for BP_Area_Lane2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33ebf02c-59c2-4e2b-af54-e5e22afc199f/custom-filter-filter-2.png)
8.  **Compile** and **Save** the Blueprint.
    
9.  Select the **BP\_NPC** Blueprint in your Level and on the **Details** panel, click the **Filter Class** dropdown, then search for and select **BP\_QueryFilter1**.
    
    ![Click the Filter Class dropdown, then search for and select BP_QueryFilter 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a59ecd43-0844-4e90-a852-030b247f8b7f/custom-npc-add-filter-1.png)
10.  Click **Simulate** and observe how the Agent is now using the **Navigation Query Filter** to determine the best route to its destination. Since **BP\_QueryFilter1** has the **BP\_Area\_Lane1** as the cheapest route, the Agent uses it to reach the Sphere.
    
    ![Since BP_QueryFilter 1 has the BP_Area_Lane 1 as the cheapest route, the Agent uses it to reach the Sphere](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60c90f92-b2af-4e2e-bc4a-2a3c8dab8f03/custom-npc-walk-3.gif)
11.  Select the **BP\_NPC** Blueprint and change the **Filter Class** to **BP\_QueryFilter2**. Click **Simulate** and observe how the Agent now uses **BP\_Area\_Lane2** area to reach its destination.
    
    ![The Agent now uses BP_Area_Lane 2  area to reach its destination](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03a84307-e93c-4317-88d4-609b77d37477/custom-npc-walk-2.gif)

### Section Results

In this section, you created two **Navigation Query Filters** and added the three previous **Area Classes**. You also changed the cost values associated with the **Area Classes** to modify the Agent's navigation when using different **Navigation Query Filters**.
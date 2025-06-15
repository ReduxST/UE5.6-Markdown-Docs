# External StateTree Quickstart Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/external-statetree-quickstart-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/external-statetree-quickstart-guide)  
**Processed:** 2025-06-14 16:23:03

---

## Introduction

Unreal Engine 5.4 introduces the ability to link a StateTree asset within another StateTree. This enables a more modular approach when building and reusing StateTrees in your project.

You can now create State Trees with specific functionality and reuse them when needed.

This guide will go through the steps of creating a simple State Tree and linking it to the State Tree created in the [StateTree Quickstart Guide](/documentation/en-us/unreal-engine/statetree-quick-start-guide).

## Goals

In this guide you will create a State Tree that rotates a moving target when it is hit. You will add this State Tree as an external asset to another StateTree that handles the movement of the target.

## Objectives

-   Create a new Hit Reaction StateTree and StateTree Task that rotate the moving target when hit
-   Add the Hit Reaction StateTree to the ShootingTarget StateStree as an external asset and configure it
-   Modify BP\_ShootingTarget and STT\_MoveAlongSpline to accommodate this new functionality

## 1- Prerequisites

This guide will use the StateTree created in the [StateTree Quickstart Guide](/documentation/en-us/unreal-engine/statetree-quick-start-guide) to demonstrate how to use an external StateTree. Please complete the Quickstart Guide to follow along the examples in this document.

Once you complete the Quickstart guide, press **Play** to verify the behavior.

![Moving target](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abd3605c-16df-451c-8375-3f1e5a1bf2e0/state-tree-pre-req.gif)

## 2 - Create a StateTree Task to rotate the target

In this section you will create a StateTree Task that rotates the moving target.

1.  Right click in the **Content Browser** and click **Blueprint Class** from the **Create Basic Asset** section.
    
    -   In the **Pick Parent Class** window, expand **All Classes** and search for **StateTree Task Blueprint Base**. Select it and click **Select**.
    -   Name the asset **STT\_RotateTarget**.
    
    ![Create a new Blueprint class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f364682-acb5-427f-8632-1910122dfa65/state-tree-external-3.png) ![Select the StateTree Task Blueprint Base class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31267683-2a00-439a-a35c-ca225b2ac4bf/state-tree-external-4.png)
2.  Double click **STT\_RotateTarget** to open it. Create a new variable and call it **ContextActor**.
    
    ![Create a new variable and call it ContextActor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ccf72a4-3e9c-4225-ac91-d55a006e8139/state-tree-external-5.png)
3.  Go to the **Details** panel, click the **Variable Type** dropdown and select **Actor Object Reference**.
    
    -   Click the **Category** textbox and enter **Context**. This will automatically bind the variable to the Context Actor in the StateTree.
    -   **Compile** and **Save** the Blueprint.
    
    ![Set the Variable Type to Actor Object Reference and the Category to Context](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f673d28-df97-4165-aa8c-377dbdf17e4c/state-tree-external-6.png)
4.  Go to the **Functions** section and click the **Override** dropdown. Click **EnterState** to create the **EventEnterState** node in the **Event Graph**. Repeat this process and click on **ExitState**.
    
    ![Override the Enter State and Exit State events](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35f349e8-4cbe-42af-b22a-9ca7768d26b5/state-tree-external-7.png) ![Two nodes are created in the Event Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdec1fce-11aa-4475-942e-abed79621501/state-tree-external-8.png)
5.  Drag the **Context Actor** into the Event Graph and select **Get ContextActor**.
    
    -   Drag from **ContextActor** and search for then select **Add Actor Component By Class**.
    -   Click the **Class** dropdown and search for then select **Rotating Movement Component**.
    
    ![Add a Rotating Movement Component to the Context Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b3b13c0-d441-40e7-a049-27577315ff8e/state-tree-external-9.png)
6.  Right click the **Return Value** pin of the **Add Rotating Movement Component** node and click **Promote to Variable**.
    
    -   Name the variable **RotatingMovementComp**.
    -   Drag from the **RotatingMovementComp** pin and search for then select **Set Rotation Rate** and enter **720** as the **Z** value.
    
    ![Create a variable for the rotating component and name it Rotating Movement Comp. Set the Rotation Rate to have a Z value of 720](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1062f837-fdf8-429c-aeb0-be3fc2f9f3ef/state-tree-external-10.png)
7.  Drag **RotatingMovementComp** to the **Event Graph** and select **Get RotatingMovementComp**.
    
    -   Drag from **RotatingMovementComp** and search for then select **Is Valid**.
    -   Connect the **EventEnterState** node to the **Is Valid** node.
    -   Connect the **Is Not Valid** pin of the **Is Valid** node to the **Add Rotating Movement Component** node.
    
    ![Check if the Rotating Movement Component is valid. If not, connect to the previous nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdc23c8f-782f-480d-94ce-68c87321d82b/state-tree-external-11.png)
8.  Drag **RotatingMovementComp** to the **Event Graph** and select **Get RotatingMovementComp**.
    
    -   Drag from **RotatingMovementComp** and search for then select **Set Component Tick Enabled**.
    -   Check the **Enabled** pin to set it to **True**.
    
    ![Enable Tick on the Rotating Movement Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a349bb68-1fb1-44db-9129-17e0854bc9be/state-tree-external-12.png)
9.  Drag **RotatingMovementComp** to the **Event Graph** and select **Get RotatingMovementComp**.
    
    -   Drag from **RotatingMovementComp** and search for then select **Set Component Tick Enabled.**
    -   Make sure the **Enabled** pin is set to **False** (unchecked).
    -   Connect the **EventExitState** node to the **SetComponentTickEnabled** node.
    
    ![Disable Tick on the Rotating Movement Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47137b44-3832-4ee9-be00-8eae424f42d9/state-tree-external-13.png)
10.  Verify your Blueprint graph looks like the example below.
    
    ![Verify your Blueprint code looks like this](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/269dc895-d6d1-4f06-8605-46651dea16e1/state-tree-external-14.png)

### Section Results

In this section you created a StateTree Task that adds a **Rotating Actor component** to the target actor and rotates it.

## 3 - Create a StateTree to rotate the target

In this section you will create a StateTree that rotates the moving target when it is hit. This StateTree will be linked to the **ST\_ShootingTarget** StateTree from the StateTree Quickstart Guide.

1.  Right click in the Content Browser and click Artificial Intelligence > StateTree. Click StateTree Component and name the asset ST\_Reaction.
    
    ![Create a new State Tree](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94472846-56ca-4e4d-a14d-aeb50dff07e6/state-tree-external-1.png) ![Click State Tree Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c97ebf2-b52c-4adb-9b7f-e77455893c7c/state-tree-external-2.png)
2.  Double click **ST\_Reaction** to open it. Expand the **Schema** section and click the **Context Actor Class** dropdown. Search for and select **BP\_ShootingTarget**.
    
    ![Set the Context Actor Class to BP_ShootingTarget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38eefddd-8183-4376-9225-4b524bf7b0ff/state-tree-external-15.png)
3.  Click **+Add State** to create a new State. Name the State **Reaction**.
    
    ![Add a new State and name it Reaction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/198c519b-b45a-4764-80d5-5448feb9f58d/state-tree-external-16.png)
4.  Add a **Delay Task** and enter **0.5** for its **Duration**. Then add a new Task and select **STT Rotate Target** from the dropdown.
    
    ![Add a Delay and a STT Rotate Target tasks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dedf2dca-9806-46e1-bd70-224fb3903e8e/state-tree-external-17.png)
5.  Create a **Transition** and set the **Trigger** to **On State Completed** and **Transition To** to **Tree Succeeded**.
    
    ![Set Transition to Tree Succeeded](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74aa17f5-ebf5-4623-b0c6-386f2183144f/state-tree-external-18.png)
6.  **Compile** and **Save** the StateTree.
    

### Section Results

In this section you created the **ST\_Reaction** StateTree which runs the **STT\_RotateTarget** task. This task rotates the target when the StateTree is executed.

## 4 - Add the External StateTree

In this section you will add **ST\_Reaction** as an external (linked) StateTree to **ST\_ShootingTarget**.

1.  Open **ST\_ShootingTarget** and click **+Add State** to create a new State. Name the State **Hit Reaction**.
    
    ![Add a new State and called it Hit Reaction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cacfe354-b82a-45ff-af28-7a695ae6807f/state-tree-external-19.png)
2.  Select the **Hit Reaction** State and go to the **Details** panel. Click the **Type** dropdown and select **Linked Asset**. Click the **Linked Asset** dropdown and select **ST\_Reaction**.
    
    ![Add ST_Reaction as a linked asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/546a2351-ce92-4be7-a2d7-50c3d3ec6a19/state-tree-external-20.png)
3.  Add an **Enter Condition**, click the **If** dropdown and select **Integer Compare**.
    
    -   Click the **Operator** dropdown and select **Less**.
    -   Set the **Right** value to **5**.
    -   Click the **Left** dropdown and select **Actor > Hit Count**.
    
    ![Add an enter condition that compares whether the Hit Count is less than 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05abd7ad-41f9-40fa-94d0-d58957aca0c2/state-tree-external-21.png)
4.  Add a new **Transition** and set the **Trigger** to **On State Completed**. Set **Transition To** to **Idle**.
    
    ![Add a transition that triggers when the State completes and it transitions to the Idle State](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d97283d-e02f-4778-8ccc-9109098be0b0/state-tree-external-22.png)
5.  Select the **MoveAlongSpline** State and create a new **Transition**.
    
    -   Click the **Trigger** dropdown and select **On Event**.
    -   Click the **Event Tag** dropdown and select **Manage Gameplay Tags**.
    
    ![Add a new Transition that triggers on an event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb760b39-5662-4897-8ea6-be1af8ebc5e4/state-tree-external-23.png)
6.  Click the **+** button to add a new entry called **StateTree**. Add another entry below it and call it **HitReaction**, as seen below.
    
    ![Add the Gameplay Tags State Tree - Hit Reaction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d085364-5aec-40f9-a945-7c517220b7cb/state-tree-external-24.png)
7.  Click the **Event Tag** dropdown and select **StateTree > Hit Reaction**. Set **Transition To** to **Hit Reaction**.
    
    ![Set the Event Tag to StateTree.HitReaction and transition to the Hit Reaction State](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e9ef1ae-d224-4057-bd8f-e809221df450/state-tree-external-25.png)

### Section Results

In this section you modified **ST\_ShootingTarget** by adding **ST\_Reaction** as an external StateTree in the **Hit Reaction** State. You also modified the **MoveAlongSpline** State to transition to **Hit Reaction** when a gameplay event is called.

## 5 - Modify BP\_ShootingTarget

In this section you will modify the **ShootingTarget** Blueprint so it sends a Hit Reaction event to the StateTree and causes the target to rotate.

1.  In the **Content Browser**, double click **BP\_ShootingTarget** to open it. Create a new Float variable and name it **DistanceTraveled**.
    
    ![Create a new Float variable and name it DistanceTraveled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f35c1d21-dd1a-49c0-a1ac-6080e4373dab/state-tree-external-30.png)
2.  Drag the **StateTree** component to the **Event Graph**.
    
    -   Drag from the **StateTree** reference and search for then select **Send State Tree Event**.
    -   Connect the **++** node to the **Send State Tree Event** node.
    
    ![Add a Send State Tree Event node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3755940-7998-481b-ba51-d8829c88acec/state-tree-external-26.png)
3.  Drag from the **Event** pin in the **Send State Tree Event** node and search for then select **Make StateTree Event**.
    
    ![Drag from the Event pin and search for then select Make StateTree Event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d14b704-d684-4140-946d-d4f7ad77701f/state-tree-external-27.png)
4.  Click the **Tag** dropdown and select **StateTree > Hit Reaction**.
    
    ![Click the Tag dropdown and select StateTree > Hit Reaction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b51a8dc-de8b-46bd-9319-da285d0d580a/state-tree-external-28.png)
5.  Drag from the **Hit Component** pin of the **OnComponentHit** node and search for then select **Get Display Name**.
    
    -   Drag from the **Return Value** pin of the **Get Display Name** node and connect it to the **Origin** pin of the **Make StateTree Event** node.
    
    ![Connect the Hit Component to the Origin pin of the Make StateTree Event node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d2b4b5b-19bf-44ed-b18d-dc047f2c0481/state-tree-external-29.png)
6.  **Compile** and **Save** the Blueprint.

### Section Results

In this section you modified the **ShootingTarget** Blueprint so it sends a StateTree **Hit Reaction** event when it is hit.

## 6 - Modify STT\_MoveAlongSpline

In this section you will modify **STT\_MoveAlongSpline** to use the **DistanceTraveled** variable from **BP\_ShootingTarget** instead of a local distance variable to calculate its position along the spline.

1.  In the **Content Browser**, double click **STT\_MoveAlongSpline** to open it. Click the **Override** dropdown next to Functions and select **EnterState** to create the **Event EnterState** node in the **Event Graph**.
    
    ![Override the Enter State event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8df01aa2-164b-439b-b4ea-8b9472e1f1db/state-tree-external-31.png)
2.  Drag the **Actor** variable to the **Event Graph** and select **Get Actor**.
    
    -   Drag from **Actor** and search for then select **Cast to BP\_ShootingTarget**.
    -   Right click the **As BP\_ShootingTarget** pin in the **Cast to BP\_ShootingTarget** node and select **Promote to Variable**.
    -   Connect the **Event EnterState** node to the **Cast to BP\_ShootingTarget** node.
    
    ![Drag from Actor and search for then select Cast to BP_ShootingTarget. Save this as a variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d4134b5-7543-40c6-9bf1-c8322c12f5a8/state-tree-external-32.png)
3.  Drag **AsBPShootingTarget** to the **Event Graph** and select **Get AsBPShootingTarget**.
    
    -   Drag from **AsBPShootingTarget** and search for then select **Get Distance Traveled**.
    -   Connect **DistanceTraveled** to the **Distance** pin of the **Get Location at Distance Along Spline** node. This replaces the current connection to Distance.
    
    ![Connect DistanceTraveled to the Distance pin of the Get Location at Distance Along Spline node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee071b4e-17a9-4401-a9bc-704a915769cc/state-tree-external-33.png)
4.  Drag **AsBPShootingTarget** to the **Event Graph** and select **Get AsBPShootingTarget**.
    
    -   Drag from **AsBPShootingTarget** and search for then select **Get Distance Traveled**.
    -   Connect **DistanceTraveled** to the **Less Than** node, replacing the connection with Distance.
    
    ![Connect DistanceTraveled to the Less Than node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/453c88b1-17c6-4db9-89c8-10f5c1fb07ef/state-tree-external-34.png)
5.  Drag **AsBPShootingTarget** to the **Event Graph** and select **Get AsBPShootingTarget**.
    
    -   Drag from **AsBPShootingTarget** and search for then select **Get Distance Traveled**.
    -   Connect **DistanceTraveled** to the **+** node, replacing the connection with Distance.
    -   Drag **AsBPShootingTarget** to the **Event Graph** and select **Get AsBPShootingTarget**. Drag from the node and search for then select **Set DistanceTraveled**.
    -   Replace the **Set Distance** node connected to the **True** pin of the **Branch** node.
    
    ![Connect DistanceTraveled to the + node and replace the Set Distance node with the Set Distance Traveled node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d390304-43e8-4dac-8371-b21f9aa2e702/state-tree-external-35.png)
6.  Drag **AsBPShootingTarget** to the **Event Graph** and select **Get AsBPShootingTarget**.
    
    -   Drag from the node and search for then select **Set DistanceTraveled**.
    -   Replace the **Set Distance** node connected to the **True** pin of the **Branch** node.
    
    ![Replace the Set Distance node with the Set Distance Traveled node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf31c2a0-7e3c-45d7-a0d2-3aa3db4c5a60/state-tree-external-36.png)
7.  **Compile** and **Save** the Blueprint.

### Section Results

In this section you modified **STT\_MoveAlongSpline** to use the **DistanceTraveled** variable from **BP\_ShootingTarget**, instead of a local Distance variable.

## 7 - Test your Results

Press **Play** and shoot at the target. You should see the target spin when it's hit and resume moving after 0.5 seconds.

![The target now rotates when hit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1efd3979-36d5-451b-a279-307b4608fe49/state-tree-external-final.gif)
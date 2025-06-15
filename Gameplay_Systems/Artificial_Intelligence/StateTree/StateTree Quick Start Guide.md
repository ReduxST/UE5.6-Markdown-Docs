# StateTree Quick Start Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/statetree-quick-start-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/statetree-quick-start-guide)  
**Processed:** 2025-06-14 16:52:12

---

## Overview

**StateTree** is a general-purpose hierarchical state machine that combines the **Selectors** from behavior trees with **States** and **Transitions** from state machines. Users can create highly performant logic that stays flexible and organized.

You can learn more about State Trees by reading the [State Tree Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-state-tree-in-unreal-engine) documentation.

## Goals

In this guide you will use a State Tree to create a moving target the player can shoot and destroy.

## Objectives

-   Create a **Blueprint** for a target Actor the player can shoot and destroy.
    
-   Create the State Tree that contains the logic to move and destroy the target actor.
    
-   Create State Tree Tasks and use them in the State Tree.
    
-   Create a State Tree Evaluator and use it in the State Tree.
    

## Required Setup

1.  Create a new project then select the **Games** category and the **First Person** template. Enter your project's location and name. Click **Create**.
    
    [![Create a new First Person project](https://dev.epicgames.com/community/api/documentation/image/4ea8d7dc-9399-4784-9c9e-9082b1db8273?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4ea8d7dc-9399-4784-9c9e-9082b1db8273?resizing_type=fit)
    
    *Click image for full size.*
    
2.  Click **Settings > Plugins** to open the **Plugins** window.
    
    [![Open the Plugins window](https://dev.epicgames.com/community/api/documentation/image/166db7a0-a235-4ed3-bfa3-3120f485bdb2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/166db7a0-a235-4ed3-bfa3-3120f485bdb2?resizing_type=fit)
    
3.  Search for and **enable** the **GameplayStateTree** and **StateTree** plugins. Restart the Unreal Engine editor.
    
    [![Open the Plugins window](https://dev.epicgames.com/community/api/documentation/image/376772ba-66c3-48f7-9acc-09bf44a20517?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/376772ba-66c3-48f7-9acc-09bf44a20517?resizing_type=fit)
    

### Section Results

In this section, you created a new project and enabled the State Tree plugins. You are now ready to create the State Tree you will use in the target Actor.

## Create the State Tree

In this section, you will create a State Tree that will be used by the target Actor. This State Tree is intended to be used as a component of the target Actor, so you will use the **State Tree Component Schema** for this example.

1.  In the **Content Browser**, right click and select **Artificial Intelligence > StateTree**.
    
    [![In the Content Browser, right click and select Artificial Intelligence > StateTree](https://dev.epicgames.com/community/api/documentation/image/540e642b-16a3-4f48-82a5-af42a37e8f50?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/540e642b-16a3-4f48-82a5-af42a37e8f50?resizing_type=fit)
    
2.  Select the **StateTreeComponentSchema** class and click **Select**.
    
    [![Select the StateTreeComponentSchema class and click Select](https://dev.epicgames.com/community/api/documentation/image/65face20-1c8a-4738-bbc8-d48759fc1143?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/65face20-1c8a-4738-bbc8-d48759fc1143?resizing_type=fit)
    
3.  Name the State **Tree ST\_ShootingTarget**.
    
    [![Name the State Tree ST ShootingTarget](https://dev.epicgames.com/community/api/documentation/image/8ecb7579-807a-45c6-b8ec-821fc9eef8e2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8ecb7579-807a-45c6-b8ec-821fc9eef8e2?resizing_type=fit)
    

### Section Results

In this section, you created a State Tree with the Component Schema that will be used by a target Actor.

## Create the Shooting Target Blueprint

In this section, you will create the Blueprint for the target Actor that will move and receive damage from the player.

1.  In the **Content Browser**, right click and select **Blueprint Class** from the **Create Basic Asset** section.
    
    1.  In the **Pick Parent Class** window, click the **Actor** button to create a new Actor Blueprint.
        
    2.  Name the Blueprint **BP\_ShootingTarget**.
        
    
    [![Select Blueprint Class from the Create Basic Asset section](https://dev.epicgames.com/community/api/documentation/image/7e4e1199-74ce-4640-8537-ee482019e9ec?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7e4e1199-74ce-4640-8537-ee482019e9ec?resizing_type=fit)
    
    [![Click the Actor button to create a new Actor Blueprint](https://dev.epicgames.com/community/api/documentation/image/d177df7a-c992-4070-9d5d-a2ed59df5f61?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d177df7a-c992-4070-9d5d-a2ed59df5f61?resizing_type=fit)
    
    [![Name the Blueprint BP_ShootingTarget](https://dev.epicgames.com/community/api/documentation/image/f24b8b4e-a65d-42c8-9fb1-2e1c930562bd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f24b8b4e-a65d-42c8-9fb1-2e1c930562bd?resizing_type=fit)
    
2.  Open **BP\_ShootingTarget** and go to the **Components** window. Click **+Add** and select **Static Mesh**.
    
    1.  Go to the **Details** panel and scroll down to the **Static Mesh** section.
        
    2.  Click the **Static Mesh** dropdown and select **1M\_Cube**.
        
    
    [![Click +Add and select Static Mesh](https://dev.epicgames.com/community/api/documentation/image/18645769-a973-4747-b7a0-55e1d950ea36?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/18645769-a973-4747-b7a0-55e1d950ea36?resizing_type=fit)
    
    [![Click the Static Mesh dropdown and select 1M_Cube](https://dev.epicgames.com/community/api/documentation/image/4aee00c6-fd92-472b-aca5-ab7a5fd82071?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4aee00c6-fd92-472b-aca5-ab7a5fd82071?resizing_type=fit)
    
3.  Set the **Scale** of the **Static Mesh** to **X = 0.2**, **Y = 2.0**, **Z = 2.0**.
    
    [![Set the Scale of the Static Mesh to X = 0.2, Y = 2.0, Z = 2.0](https://dev.epicgames.com/community/api/documentation/image/42986b50-93df-4217-9576-0ef85f45725a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/42986b50-93df-4217-9576-0ef85f45725a?resizing_type=fit)
    
4.  In the **Components** window, click **+Add** and select **StateTree**.
    
    1.  Go to the **Details** panel and scroll down to the **AI** section.
        
    2.  Click the **State Tree** dropdown and select **ST\_ShootingTarget**.
        
    
    [![Click +Add and select StateTree](https://dev.epicgames.com/community/api/documentation/image/93b92e68-4edf-4bb2-918e-f481d36a3a94?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/93b92e68-4edf-4bb2-918e-f481d36a3a94?resizing_type=fit)
    
    [![Click the State Tree dropdown and select ST Shooting Target](https://dev.epicgames.com/community/api/documentation/image/403b413d-58a2-4ff3-a5a5-85e88bd0ff8d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/403b413d-58a2-4ff3-a5a5-85e88bd0ff8d?resizing_type=fit)
    
    If the State Tree does not appear in the dropdown, it means that the incorrect schema was selected. Make sure to select the **StateTreeComponentSchema** to use in the State Tree component.
    
5.  Right-click the **Static Mesh** component and select **Add Event > Add OnComponentHit**.
    
    [![Right click the Static Mesh component and select Add Event then Add OnComponentHit](https://dev.epicgames.com/community/api/documentation/image/8d4534e9-a869-48e0-89d2-a9b5662e1283?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8d4534e9-a869-48e0-89d2-a9b5662e1283?resizing_type=fit)
    
6.  Create a new variable and name it **HitCount**.
    
    1.  Go to the **Details** panel and set the **Variable Type** to **Integer**.
        
    
    [![Create a new variable and name it HitCount](https://dev.epicgames.com/community/api/documentation/image/21d79083-12ea-4f09-be29-d31ff4abdc5a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/21d79083-12ea-4f09-be29-d31ff4abdc5a?resizing_type=fit)
    
    [![Set the Variable Type to Integer](https://dev.epicgames.com/community/api/documentation/image/b49719fa-fcbd-4188-a26a-0067031281a6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b49719fa-fcbd-4188-a26a-0067031281a6?resizing_type=fit)
    
7.  Drag the **HitCount** variable to the **Event Graph** and select **Get HitCount**.
    
    1.  Drag from the **HitCount** node and search for and select **Increment Int**.
        
    2.  Connect the **On Component Hit** node to the **Increment Int** node.
        
    
    [![Connect the On Component Hit node to the Increment Int node](https://dev.epicgames.com/community/api/documentation/image/d4199f2b-94c2-4895-9625-7d44808bcae4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d4199f2b-94c2-4895-9625-7d44808bcae4?resizing_type=fit)
    
8.  In the **Event Graph**, right click and search for then select **Add Custom Event**. Name the event **DelayedDestroy**.
    
    [![Add a Custom Event and name it DelayedDestroy](https://dev.epicgames.com/community/api/documentation/image/cacec730-7d8b-419e-88eb-7c868abce4fb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cacec730-7d8b-419e-88eb-7c868abce4fb?resizing_type=fit)
    
9.  Drag from the **DelayedDestroy** node and search for then select **Delay**.
    
    [![Add a Delay node](https://dev.epicgames.com/community/api/documentation/image/43bad0eb-491b-4baa-b2a9-836fb7fcd157?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/43bad0eb-491b-4baa-b2a9-836fb7fcd157?resizing_type=fit)
    
10.  Drag from the **Delay** node and search for then select **Destroy Actor**.
    
    [![Add a Destroy Actor node](https://dev.epicgames.com/community/api/documentation/image/9f40e43d-c8c5-4f22-a731-dc31f38d863f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9f40e43d-c8c5-4f22-a731-dc31f38d863f?resizing_type=fit)
    

### Section Results

In this section, you created the Shooting Actor Blueprint the player will shoot during gameplay. You are now ready to create the Idle and Dead States of the State Tree.

## Create the Idle and Dead States

1.  Go back to **ST\_ShootingTarget** and under the **Schema** section, click the **Context Actor Class** dropdown. Select **BP\_ShootingTarget**.
    
    [![Click the Context Actor Class dropdown and select BP_ShootingTarget](https://dev.epicgames.com/community/api/documentation/image/9c2da622-0d8b-4b01-bcba-9f3af429c117?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9c2da622-0d8b-4b01-bcba-9f3af429c117?resizing_type=fit)
    
2.  Click **\+ Add State** to create a new State and name it **Idle**.
    
    [![Click + Add State to create a new State and name it Idle](https://dev.epicgames.com/community/api/documentation/image/380d823b-d29e-4db7-abd2-6e769ed40dfb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/380d823b-d29e-4db7-abd2-6e769ed40dfb?resizing_type=fit)
    
3.  Go to the **Details** panel and scroll down to the **Transitions** section.
    
    1.  Expand the **Go to State** section and click the **Transition To** dropdown. Select **Root**. This will set the State Tree to transition back to the Root State once this State is completed.
        
    2.  Click the **Trigger** dropdown and select **On State Completed**.
        
    
    [![Click the Transition To dropdown and select Root](https://dev.epicgames.com/community/api/documentation/image/d24115e2-5b39-414e-8466-793f1b3a6c2b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d24115e2-5b39-414e-8466-793f1b3a6c2b?resizing_type=fit)
    
    [![The Idle State now shows the Transition to Root](https://dev.epicgames.com/community/api/documentation/image/ae3e6ba4-c27e-4557-96b5-e265ffc93ebe?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ae3e6ba4-c27e-4557-96b5-e265ffc93ebe?resizing_type=fit)
    
4.  Create another State and name it **Dead**.
    
    [![Create another State and name it Dead](https://dev.epicgames.com/community/api/documentation/image/6b4f07e6-8427-44ed-88d3-49d007514a87?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6b4f07e6-8427-44ed-88d3-49d007514a87?resizing_type=fit)
    
5.  Select the **Idle** State and add another **Transition**.
    
    1.  Click the **Trigger** dropdown and select **On Tick**.
        
    2.  Click the **Transition To** dropdown and select **Dead**.
        
    
    [![Click the Trigger dropdown and select On Tick. Click the Transition To dropdown and select Dead](https://dev.epicgames.com/community/api/documentation/image/5cf35ff3-1688-4972-b845-db1a0a174a46?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5cf35ff3-1688-4972-b845-db1a0a174a46?resizing_type=fit)
    
6.  Add a new **Condition** by clicking on the **plus sign**. Click the dropdown and select **Integer Compare**.
    
    1.  Expand the structure and click on the **Left Bind** dropdown and select **Actor > Hit Count**. This binds the value of **Hit Count** inside **BP\_ShootingTarget** to the StateTree Condition.
        
    2.  Enter **5** as the value of the **Right** integer.
        
    
    [![Expand the structure and click on the Left Bind dropdown and select Actor > Hit Count](https://dev.epicgames.com/community/api/documentation/image/651fbfce-3d04-47d4-b862-ac7e1ec7641e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/651fbfce-3d04-47d4-b862-ac7e1ec7641e?resizing_type=fit)
    
    [![Expand the structure and click on the Left Bind dropdown and select Actor > Hit Count](https://dev.epicgames.com/community/api/documentation/image/256cfd6c-8b6c-4ebf-9624-8e5310515377?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/256cfd6c-8b6c-4ebf-9624-8e5310515377?resizing_type=fit)
    
    [![Enter 5 as the value of the Right integer](https://dev.epicgames.com/community/api/documentation/image/6a30e411-38f9-4239-9279-5eee2338c5a9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6a30e411-38f9-4239-9279-5eee2338c5a9?resizing_type=fit)
    

### Section Results

In this section, you added the Idle and Dead States to the State Tree. You are now ready to create a State Tree Task that will handle the Dead State.

## Create a New State Tree Task

In this section, you will create a new **State Tree Task** that will destroy the Actor when the **Dead** State is executed.

1.  In the **Content Browser**, right click and select **Blueprint Class**.
    
    1.  In the **Pick Parent Class** window, expand the **All Classes** dropdown and search for and select **StateTreeTaskBlueprintBase**.
        
    2.  Click **Select** to create the asset.
        
    3.  Name the Blueprint class **STT\_Destroy**.
        
    
    [![Select Blueprint Class from the Create Basic Asset section](https://dev.epicgames.com/community/api/documentation/image/90a65aa2-5c6a-49f4-97bd-7d1326df4f43?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/90a65aa2-5c6a-49f4-97bd-7d1326df4f43?resizing_type=fit)
    
    [![Expand the All Classes dropdown and search for and select  StateTreeTaskBlueprintBase](https://dev.epicgames.com/community/api/documentation/image/8c7cb939-3f62-41bf-8938-9f545bb9bf66?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8c7cb939-3f62-41bf-8938-9f545bb9bf66?resizing_type=fit)
    
    [![Name the Blueprint class STT Destroy](https://dev.epicgames.com/community/api/documentation/image/8308a705-24ca-4473-a9c6-c773667a4be8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8308a705-24ca-4473-a9c6-c773667a4be8?resizing_type=fit)
    
2.  Open **STT\_Destroy** by double-clicking it in the **Content Browser**. Go to the **Functions** section and click the **Override** dropdown. Select **ExitState**.
    
    [![Go to the Functions section and click the Override dropdown. Select ExitState](https://dev.epicgames.com/community/api/documentation/image/83e2f91d-7640-4739-9d82-5959dd30451d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/83e2f91d-7640-4739-9d82-5959dd30451d?resizing_type=fit)
    
3.  Create a new variable and name it **Actor**. Set its type to **Actor Object Reference**.
    
    1.  Go to the **Details** panel, and click in the **Category** field. Enter **Context**.
        
    2.  Drag the **Actor** variable to the **Event Graph** and select **Get Actor**.
        
    3.  Drag from the **Actor** node and search for and select **Cast to BP\_ShootingTarget**.
        
    4.  Drag from the **As BP Shooting Target** pin of the **Cast to BP\_ShootingTarget** node and search for then select **Delayed Destroy**.
        
    5.  Connect the **Event ExitState** node to the **Cast to BP\_ShootingTarget** node.
        
    
    [![Create a new variable and name it Actor. Set its type to Actor Object Reference](https://dev.epicgames.com/community/api/documentation/image/722da9e8-4ac0-4410-afe0-b8521abe5b29?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/722da9e8-4ac0-4410-afe0-b8521abe5b29?resizing_type=fit)
    
    [![Go to the Details panel, and set its Category to Context](https://dev.epicgames.com/community/api/documentation/image/4d147993-ab33-4a6a-91b2-ccc2637dd973?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4d147993-ab33-4a6a-91b2-ccc2637dd973?resizing_type=fit)
    
    [![Connect the Event ExitState node to the Cast to BP_ShootingTarget node](https://dev.epicgames.com/community/api/documentation/image/085282ca-13ee-414b-b4f3-90e9250b3af5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/085282ca-13ee-414b-b4f3-90e9250b3af5?resizing_type=fit)
    

### Section Results

In this section, you created a new State Tree Task that runs once the Dead State is executed. This Task destroys the Actor.

## Finish the Dead State

1.  Go back to **ST\_ShootingTarget** and select the **Dead** State. Add a new **Task** and select **Debug Text Task** from the dropdown.
    
    1.  Enter **'Actor Destroyed'** in the **Text** field.
        
    2.  Enter a **Text Color** and a **Font Scale**.
        
    
    [![Add a new Task and select Debug Text Task from the dropdown](https://dev.epicgames.com/community/api/documentation/image/125d5e22-c2ee-47e9-badb-29e058233fd7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/125d5e22-c2ee-47e9-badb-29e058233fd7?resizing_type=fit)
    
2.  Add another **Task** and select **Delay Task** from the dropdown.
    
    1.  Enter **2.0** for the **Duration**.
        
    
    [![Add another Task and select Delay Task from the dropdown](https://dev.epicgames.com/community/api/documentation/image/262ce13b-c696-48c4-8d00-f96916d2975e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/262ce13b-c696-48c4-8d00-f96916d2975e?resizing_type=fit)
    
3.  Add a third **Task** and select **STT\_Destroy** from the dropdown. This will destroy the Actor.
    
    [![Add a third Task and select STT_Destroy from the dropdown](https://dev.epicgames.com/community/api/documentation/image/9bc56b0e-3da7-4ffd-9e9b-6b76d3267161?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9bc56b0e-3da7-4ffd-9e9b-6b76d3267161?resizing_type=fit)
    
4.  Create a new **Transition** and set the **Trigger** to **On State Completed**.
    
    1.  Set the **Transition To** dropdown to **Tree Succeeded**.
        
    
    [![Create a new Transition and set the Trigger to On State Completed. Set the Transition To dropdown to Tree Succeeded](https://dev.epicgames.com/community/api/documentation/image/1ea5cff8-3646-45aa-98cf-60f7ab32645c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1ea5cff8-3646-45aa-98cf-60f7ab32645c?resizing_type=fit)
    
5.  Drag **BP\_ShootingTarget** to your Level and press **Play**. Shoot the Blueprint and confirm the State Tree is working.
    
    [![Drag BP_ShootingTarget to your Level and press Play](https://dev.epicgames.com/community/api/documentation/image/32f951d8-b84e-456d-8c84-7df286df0bba?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/32f951d8-b84e-456d-8c84-7df286df0bba?resizing_type=fit)
    
    [![The player shoots and destroys the Shooting Target](https://dev.epicgames.com/community/api/documentation/image/813fd07b-b247-4cdc-a370-1294924a7c1e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/813fd07b-b247-4cdc-a370-1294924a7c1e?resizing_type=fit)
    

### Section Results

In this section, you completed the Dead State and tested that the Shooting Actor Blueprint can receive damage and be destroyed.

## Add a Spline Path

In this section, you will create an Actor with a Spline component. This spline will be used by the Shooting Target Blueprint to move in the Level.

1.  In the **Content Browser**, right click and select **Blueprint Class** from the **Create Basic Asset** section.
    
    1.  In the **Pick Parent Class** window, click the **Actor** button to create a new Actor Blueprint.
        
    2.  Name the Blueprint **BP\_SplineActor**.
        
    
    [![Select Blueprint Class from the Create Basic Asset section](https://dev.epicgames.com/community/api/documentation/image/d0ebae8c-7514-49d1-ae39-c3c5d8440950?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d0ebae8c-7514-49d1-ae39-c3c5d8440950?resizing_type=fit)
    
    [![Click the Actor button to create a new Actor Blueprint](https://dev.epicgames.com/community/api/documentation/image/430d9e28-184f-4861-b7a5-1281a09654cc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/430d9e28-184f-4861-b7a5-1281a09654cc?resizing_type=fit)
    
    [![Name the Blueprint BP_ShootingTarget](https://dev.epicgames.com/community/api/documentation/image/aee8571a-1ff5-41f0-9348-6d159777e78c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/aee8571a-1ff5-41f0-9348-6d159777e78c?resizing_type=fit)
    
2.  Open **BP\_SplineActor** and go to the **Components** window. Click **+Add** and select **Spline**.
    
    1.  **Compile** and **Save** the Blueprint.
        
    
    [![Click the +Add button and select Spline](https://dev.epicgames.com/community/api/documentation/image/af502188-3bdc-4e9c-9c47-3763df48ceca?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/af502188-3bdc-4e9c-9c47-3763df48ceca?resizing_type=fit)
    

### Section Results

In this section, you created a generic Blueprint Actor that has a Spline component. This Spline will be used to create a moving path for the Shooting Actor in the Level.

## Add a State Tree Evaluator

Now you will create a **State Tree Evaluator** that will search for all Spline Actors in the Level and return the closest one to the State Tree.

1.  In the **Content Browser**, right click and select **Blueprint Class** from the **Create Basic Asset** section.
    
    1.  In the **Pick Parent Class** window, expand the **All Classes** dropdown and search for and select **StateTreeEvaluatorBlueprintBase**.
        
    2.  Click **Select** to create the asset.
        
    3.  Name the Blueprint class **STE\_GetSpline**.
        
    
    [![Select Blueprint Class from the Create Basic Asset section](https://dev.epicgames.com/community/api/documentation/image/e2c65d8d-ae2e-4eca-a27b-6ce1fafa9b40?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e2c65d8d-ae2e-4eca-a27b-6ce1fafa9b40?resizing_type=fit)
    
    [![In the Pick Parent Class window, expand the All Classes dropdown and search for and select StateTreeEvaluatorBlueprintBase](https://dev.epicgames.com/community/api/documentation/image/89ec9e9d-cdd5-4cfb-8c01-0f92e3584136?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/89ec9e9d-cdd5-4cfb-8c01-0f92e3584136?resizing_type=fit)
    
    [![Name the Blueprint class STE_GetSpline](https://dev.epicgames.com/community/api/documentation/image/c397bc2a-a1ae-427d-9d75-bad045a5c455?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c397bc2a-a1ae-427d-9d75-bad045a5c455?resizing_type=fit)
    
2.  Open **STE\_GetSpline** and go to the **Functions** section of the **My Blueprint** panel.
    
    1.  Click the **Override** dropdown and select **TreeStart**.
        
    
    [![Click the Override dropdown and select TreeStart](https://dev.epicgames.com/community/api/documentation/image/a399780d-b45b-4258-993f-6a8f6666e04d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a399780d-b45b-4258-993f-6a8f6666e04d?resizing_type=fit)
    
3.  Drag from the **Event TreeStart** node and search for and select **Get All Actors of Class**.
    
    1.  Click the **Actor Class** dropdown and select **BP\_SplineActor**.
        
    
    [![Drag from the Event TreeStart node and search for and select Get All Actors of Class](https://dev.epicgames.com/community/api/documentation/image/6960b3ee-963f-4603-8695-e2e55adf30ec?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6960b3ee-963f-4603-8695-e2e55adf30ec?resizing_type=fit)
    
4.  Create a new variable and name it **Actor**.
    
    1.  Go to the **Details** panel and set the **Variable Type** to **Actor Object Reference**.
        
    2.  Click the **Category** dropdown and enter '**Context**'.
        
    
    [![Create a new variable and name it Actor](https://dev.epicgames.com/community/api/documentation/image/2bc337bf-5212-4310-9820-5ccc70e2788d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2bc337bf-5212-4310-9820-5ccc70e2788d?resizing_type=fit)
    
    [![Set the Variable Type to Actor Object Reference and click the Category dropdown and enter 'Context'](https://dev.epicgames.com/community/api/documentation/image/67470e14-bc5e-42d9-b2f3-d7c85c267aa5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/67470e14-bc5e-42d9-b2f3-d7c85c267aa5?resizing_type=fit)
    
5.  Drag from the **Out Actors** pin of the **Get All Actors from Class** node and search for and select **Find Nearest Actor**.
    
    1.  Drag the **Actor** variable to the **Event Graph** and select **Get Actor**.
        
    2.  Drag from the **Actor** node and search for and select **Get Actor Location**.
        
    3.  Connect the **Return Value** of the **Get Actor Location** node to the **Origin** pin of the **Find Nearest Actor** node.
        
    
    [![Drag from the Out Actors pin of the Get All Actors from Class node and search for and select Find Nearest Actor](https://dev.epicgames.com/community/api/documentation/image/7ab7a24f-7bdc-430a-a030-3fb80fe9ac01?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7ab7a24f-7bdc-430a-a030-3fb80fe9ac01?resizing_type=fit)
    
6.  Drag from the **Return Value** pin of the **Find Nearest Actor** node and search for and select **Cast to BP\_SplineActor**.
    
    1.  Right click on the **As BP Spline Actor** pin of the **Cast to BP\_SplineActor** node and select **Promote to Variable**.
        
    2.  Name this variable to **SplineActor** and enter '**Output**' for its **Category**.
        
    3.  **Compile** and **Save** the Blueprint.
        
    
    [![Drag from the Return Value pin of the Find Nearest Actor node and search for and select Cast to BP_SplineActor](https://dev.epicgames.com/community/api/documentation/image/568f92d6-10d6-4eb1-8e49-a3d14d39f72f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/568f92d6-10d6-4eb1-8e49-a3d14d39f72f?resizing_type=fit)
    
    [![Name this variable to SplineActor and enter 'Output' for its Category](https://dev.epicgames.com/community/api/documentation/image/793b35ad-f67d-4eb7-a56a-2bdb95e2c2c5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/793b35ad-f67d-4eb7-a56a-2bdb95e2c2c5?resizing_type=fit)
    
7.  Go back to **ST\_ShootingTarget** and under the **StateTree** window, click the **plus sign** next to **Evaluators**.
    
    1.  Click the dropdown and select **STE\_GetSpline**.
        
    
    [![Click the dropdown and select STE_GetSpline](https://dev.epicgames.com/community/api/documentation/image/3bba7ee3-409e-49a0-8328-b0d75b42174b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3bba7ee3-409e-49a0-8328-b0d75b42174b?resizing_type=fit)
    

### Section Results

In this section, you created a State Tree Evaluator that will execute when the State Tree begins execution. This Evaluator checks for all Spline Actors in the Level and returns the closest one to the Shooting Actor.

## Add a State Tree Task to Move Along Spline

In this section, you will create a new **State Tree Task** that will move the Actor along the **BP\_SplineActor**'s spline.

1.  In the **Content Browser**, right click and select **Blueprint Class**.
    
    1.  In the **Pick Parent Class** window, expand the **All Classes** dropdown and search for and select **StateTreeTaskBlueprintBase**.
        
    2.  Click **Select** to create the asset.
        
    3.  Name the Blueprint class **STT\_MoveAlongSpline**.
        
    
    [![Select Blueprint Class from the Create Basic Asset section](https://dev.epicgames.com/community/api/documentation/image/54d04753-50fe-4f44-857f-4028adc1daef?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/54d04753-50fe-4f44-857f-4028adc1daef?resizing_type=fit)
    
    [![In the Pick Parent Class window, expand the All Classes dropdown and search for and select  StateTreeTaskBlueprintBase](https://dev.epicgames.com/community/api/documentation/image/3bccdc6f-4ac5-4e2c-ad25-8d7e222f585e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3bccdc6f-4ac5-4e2c-ad25-8d7e222f585e?resizing_type=fit)
    
    [![Name the Blueprint class STT_MoveAlongSpline](https://dev.epicgames.com/community/api/documentation/image/15d1a0b6-89ce-4f6a-b5e8-6b47a1c6808a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/15d1a0b6-89ce-4f6a-b5e8-6b47a1c6808a?resizing_type=fit)
    
2.  Open **STT\_MoveAlongSpline** and go to the **Functions** section of the **My Blueprint** panel. Click the **Override** dropdown and select **Tick**.
    
    [![Click the Override dropdown and select Tick](https://dev.epicgames.com/community/api/documentation/image/ca317507-cff8-4a36-aa64-2891062184c6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ca317507-cff8-4a36-aa64-2891062184c6?resizing_type=fit)
    
3.  Create a new variable and name it **Actor**.
    
    1.  Go to the **Details** panel and set the **Variable Type** to **Actor Object Reference**.
        
    2.  Click the Category dropdown and enter '**Context**'.
        
    
    [![Create a new variable and name it Actor](https://dev.epicgames.com/community/api/documentation/image/3ef8c836-7932-4705-9d95-5d58394d5a12?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3ef8c836-7932-4705-9d95-5d58394d5a12?resizing_type=fit)
    
    [![Set the Variable Type to Actor Object Reference and click the Category dropdown and enter 'Context'](https://dev.epicgames.com/community/api/documentation/image/8a851941-b08f-4cb0-b71e-b86eb2a6fbfd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8a851941-b08f-4cb0-b71e-b86eb2a6fbfd?resizing_type=fit)
    
4.  Create a new variable and name it **SplineActor**.
    
    1.  Go to the **Details** panel and set the **Variable Type** to **BP\_SplineActor**.
        
    2.  Enter '**Input**' as the **Category**.
        
    
    [![Create a new variable and name it SplineActor](https://dev.epicgames.com/community/api/documentation/image/8465240e-6842-4322-8f78-f0d97d51401b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8465240e-6842-4322-8f78-f0d97d51401b?resizing_type=fit)
    
    [![Set the Variable Type to B SplineActor and enter 'Input' as the Category](https://dev.epicgames.com/community/api/documentation/image/c5afaa3f-4f7e-453c-8c0e-9f95271eab09?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c5afaa3f-4f7e-453c-8c0e-9f95271eab09?resizing_type=fit)
    
5.  Drag the **Actor** variable to the **Event Graph** and select **Get Actor**.
    
    1.  Drag from the **Actor** node and search for and select **Set Actor Location**.
        
    2.  Connect the **Tick** node to the **Set Actor Location** node.
        
    
    [![Drag from the Actor node and search for and select Set Actor Location](https://dev.epicgames.com/community/api/documentation/image/b35a09b4-5643-45a7-9fa9-c7bc266080c9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b35a09b4-5643-45a7-9fa9-c7bc266080c9?resizing_type=fit)
    
6.  Drag the **SplineActor** to the **Event Graph** and select **Get Spline Actor**.
    
    1.  Drag from the **SplineActor** node and search for and select **Spline**.
        
    2.  Drag from the **Spline** node and search for and select **Get Location at Distance Along Spline**.
        
    3.  Connect the **Return Value** of the **Get Location** at **Distance Along Spline** node and connect it to the **New Location** pin of the **Set Actor Location** node.
        
    4.  Right click the **Distance** pin of the **Get Location at Distance Along Spline** node and select **Promote to Variable**.
        
    
    [![Connect the Return Value of the Get Location at Distance Along Spline node and connect it to the New Location pin of the Set Actor Location node](https://dev.epicgames.com/community/api/documentation/image/0e8da996-e54d-47b4-aa36-9252295108b2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0e8da996-e54d-47b4-aa36-9252295108b2?resizing_type=fit)
    
7.  Drag from the **Set Actor Location** node and search for and select **Branch**.
    
    1.  Drag the **Distance** variable to the **Event Graph** and select **Get Distance**.
        
    2.  Drag from the **Distance** node and search for and select **Less**.
        
    3.  Connect the **Less** node to the **Condition** pin of the **Branch** node.
        
    
    [![Connect the Less node to the Condition pin of the Branch node](https://dev.epicgames.com/community/api/documentation/image/505d3348-8088-4155-b82c-2b035a5a6ebf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/505d3348-8088-4155-b82c-2b035a5a6ebf?resizing_type=fit)
    
8.  Drag the **SplineActor** to the **Event Graph** and select **Get Spline Actor**.
    
    1.  Drag from the **SplineActor** node and search for and select **Spline**.
        
    2.  Drag from the **Spline** node and search for and select **Get Spline Length**.
        
    3.  Connect the **Return Value** from the **Get Spline Length** node and connect it to the lower pin of the **Less** node.
        
    
    [![Connect the Return Value from the Get Spline Length node and connect it to the lower pin of the Less node](https://dev.epicgames.com/community/api/documentation/image/6a8301ea-4add-463c-9b18-ba68a9bf4757?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6a8301ea-4add-463c-9b18-ba68a9bf4757?resizing_type=fit)
    
9.  Drag the **Distance** variable to the **Event Graph** and select **Get Distance**.
    
    1.  Drag from the **Distance** node and search for and select **Add**.
        
    2.  Create a new variable of type **Float** and name it **MovementSpeed**.
        
    3.  Connect **MovementSpeed** to the lower pin of the **Add** node.
        
    4.  Drag the **Distance** variable to the **Event Graph** and select **Set Distance**.
        
    5.  Connect the **Add** node to the **Set Distance** node.
        
    6.  Connect the **True** pin of the **Branch** node to the **Set Distance** node, as seen below.
        
    
    [![Connect the True pin of the Branch node to the Set Distance node, as seen below](https://dev.epicgames.com/community/api/documentation/image/84251042-cb0c-4181-8408-ef53daad6d8e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/84251042-cb0c-4181-8408-ef53daad6d8e?resizing_type=fit)
    
10.  Select the **MovementSpeed** variable and set its **Default** value to **5.0**.
    
    [![Select the MovementSpeed variable and set its Default value to 5.0](https://dev.epicgames.com/community/api/documentation/image/631d940d-6516-4900-815c-131a8df59c80?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/631d940d-6516-4900-815c-131a8df59c80?resizing_type=fit)
    
11.  Drag the **Distance** variable to the **Event Graph** and select **Set Distance**.
    
    1.  Connect the **False** pin of the **Branch** node to the **Set Distance** node.
        
    2.  Drag from the **Set Distance** node and search for then select the **Finish Task** function.
        
    
    [![Connect the False pin of the Branch node to the Set Distance node](https://dev.epicgames.com/community/api/documentation/image/fc0e9e75-d18f-462f-b257-0f9fc9e948b4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fc0e9e75-d18f-462f-b257-0f9fc9e948b4?resizing_type=fit)
    
    [![Connect both Set Distance nodes to the Return Node with a Return Value of Running](https://dev.epicgames.com/community/api/documentation/image/91e8250d-ec69-4240-a29a-458c176414d6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/91e8250d-ec69-4240-a29a-458c176414d6?resizing_type=fit)
    

### Section Results

In this section, you create a State Tree Task that moves the Shooting Actor Blueprint along the spline path created with the Spline Actor Blueprint.

## Finalize the State Tree

1.  Go back to **ST\_ShootingTarget** and click **+Add State**. Name the new State **MoveAlongSpline**.
    
    1.  Click and drag the **MoveAlongSpline** State into the **Idle** State to parent it.
        
    
    [![Click and drag the MoveAlongSpline State into the Idle State to parent it](https://dev.epicgames.com/community/api/documentation/image/4137ebf2-1e52-444b-8538-188c7f04afd2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4137ebf2-1e52-444b-8538-188c7f04afd2?resizing_type=fit)
    
2.  Go to the **Details** panel and add a new **Task** by clicking the **+** button.
    
    1.  Click the **dropdown** and select **STT\_MoveAlongSpline**.
        
    2.  Click the **Bind** dropdown next to **Spline Actor** and select **STE Get Spline > Spline Actor**.
        
    
    [![Click the dropdown and select STT_MoveAlongSpline](https://dev.epicgames.com/community/api/documentation/image/859bcbea-269d-4d6d-a675-69b7fcee157f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/859bcbea-269d-4d6d-a675-69b7fcee157f?resizing_type=fit)
    
    [![Click the Bind dropdown next to Spline Actor and select STE Get Spline > Spline Actor](https://dev.epicgames.com/community/api/documentation/image/bebb5d51-3d1f-477a-8460-73911357de5d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bebb5d51-3d1f-477a-8460-73911357de5d?resizing_type=fit)
    
    [![The Spline Actor is now bound to the Spline Actor variable in STE Get Spline](https://dev.epicgames.com/community/api/documentation/image/7f129c0c-c00a-4f37-8913-8d5046f491e8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7f129c0c-c00a-4f37-8913-8d5046f491e8?resizing_type=fit)
    
3.  Drag **BP\_SplineActor** to the Level.
    
    [![Drag B SplineActor to the Level](https://dev.epicgames.com/community/api/documentation/image/5da1cf12-ad6d-459e-96bb-7c82ee221591?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5da1cf12-ad6d-459e-96bb-7c82ee221591?resizing_type=fit)
    
4.  Select the **Spline** component of **BP\_SplineActor**. **Alt-drag** to create new spline points and create a closed shape.
    
    1.  Select the **Spline** component of the **Spline Actor** Blueprint and scroll down to the **Spline** section. **Enable** the **Closed Loop** checkbox to make the spline a closed shape.
        
    
    [![Enable the Closed Loop checkbox to make the spline a closed shape](https://dev.epicgames.com/community/api/documentation/image/9b7d41e0-6ece-43bb-8c7b-b205daed7210?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9b7d41e0-6ece-43bb-8c7b-b205daed7210?resizing_type=fit)
    
5.  Press **Play** and shoot at the target.
    
    [![Press Play and shoot at the target](https://dev.epicgames.com/community/api/documentation/image/ebd1a5de-2986-4a6d-844c-224f1cf107b9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ebd1a5de-2986-4a6d-844c-224f1cf107b9?resizing_type=fit)
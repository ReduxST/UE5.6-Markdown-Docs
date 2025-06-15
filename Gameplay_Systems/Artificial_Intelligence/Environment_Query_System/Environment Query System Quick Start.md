# Environment Query System Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-system-quick-start-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-query-system-quick-start-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:17

---

It is recommended that you proceed through the [Behavior Tree Quick Start Guide](/documentation/en-us/unreal-engine/behavior-tree-in-unreal-engine---quick-start-guide) or have some prior knowledge of Blueprints and Behavior Trees in Unreal Engine 5 before proceeding with this guide.

The **Environment Query System (EQS)** can be used within [Behavior Trees](/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine) to poll the environment through a variety of [Tests](/documentation/en-us/unreal-engine/eqs-node-reference-tests-in-unreal-engine), then based on the results of those Tests, can make decisions on how to proceed. Some example use cases for EQS could be to have an AI character find a cover location away from the Player or to find the nearest health or ammo in the Level.

An Environment Query is made up of several different pieces. You can call an Environment Query from a Behavior Tree, and then the actual Environment Query will use its [Generator](/documentation/en-us/unreal-engine/eqs-node-reference-generators-in-unreal-engine), reference its [Contexts](/documentation/en-us/unreal-engine/eqs-node-reference-contexts-in-unreal-engine), and use its Tests to give the Behavior Tree the highest weighted result.

In this guide, we create an AI that randomly moves around the environment until seeing the player. When seeing the player, the AI uses the EQS system to find a location in the environment that provides the best vantage point while maintaining its distance. This can be useful in situations where you have an AI character that performs some form of ranged attack, as the AI will keep its distance from the player and try to retain a line of sight as seen in the example below.

By the end of this guide, you will have a basic understanding of the following systems:

1.  Blueprint Visual Scripting
    
2.  AI Controllers
    
3.  Blackboards
    
4.  Behavior Trees
    
5.  Environmental Query System (EQS)
    
6.  EQS Contexts
    
7.  AI Debugging Tools
    

## 1 - Required Project Setup

In this step, we'll set up our project with some of the assets we'll need for our AI as well as enable the EQS system.

For this guide, we are using a new **Blueprint Third Person Template** project.

1.  Inside your project, in the **Settings > Plugins** section, enable the **Environment Query Editor** option if necessary.
    
    ![In the Project Settings,enable the Environment Query Editor option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de90b34a-a3b4-470c-b0aa-c501ca3d815b/environment-query-system-quick-start-01.png)
    
    Enabling the EQS system will allow you to create and access EQS-related assets.
    
2.  In the **Content > ThirdPerson > Blueprints** folder, copy the **BP\_ThirdPersonCharacter** over to a new folder called **AI**.
    
    ![Copy the BPThirdPersonCharacter over to a new folder called AI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a40e3592-8601-403f-86aa-7e958bc7bcde/environment-query-system-quick-start-02.png)
3.  In the **AI** folder, create the following three AI assets from the **+Add > Create Advanced Asset > Artificial Intelligence** option:
    
    ![In the AI folder create the following three AI assets from the Add option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7825d75-f91d-485b-8f82-fb89272a253f/environment-query-system-quick-start-03.png)
    -   **Blackboard** named **BB\_Enemy**
    -   **Behavior Tree** named **BT\_Enemy**
    -   **Environment Query** named **EQS\_FindPlayer**
4.  Create a new **Blueprint Class** of the **AIController** type and call it **AIC\_Enemy**.
    
    ![Create a new Blueprint Class of the AIController type and call it AIC_Enemy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3943317-84f7-4536-a832-740146ce7d6b/environment-query-system-quick-start-04.png)
5.  Create a new **Blueprint Class** of the **EnvQueryContext\_BlueprintBase** type and call it **EQC\_PlayerContext**.
    
    ![Create a new Blueprint Class of the EnvQueryContextBlueprintBase type and call it EQCPlayerContext](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e821a221-90d0-467f-aea1-836caaa74d38/environment-query-system-quick-start-05.png)
    
    **Contexts** can be used in the EQS system for reference when applying various Tests, for example, "EQS, how close am I to the specified Context" is a Test we could run. This asset will be used to provide the Player Character as a Context when we perform Tests a little later in this guide.
    

## 2 - Environment Query Context

In this step, we establish a Context for the EQS system of the Player Character that will be used in Tests later in the guide.

1.  Open the **EQC\_PlayerContext** asset, then in the **My Blueprint** panel, override the **Provide Single Actor** function.
    
    ![In the My Blueprint panel override the Provide Single Actor function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a53a7328-e71e-40c1-9c70-bdcb6d480365/environment-query-system-quick-start-06.png)
    
    You can provide individual **Actors** or **Locations** as a Context as well as a set of **Actors** or **Locations**.
    
2.  In the **Provide Single Actor** function, use a **Get Player Character** call as the **Resulting Actor**.
    
    ![Use a Get Player Character call as the Resulting Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/610528ff-a79b-4b6f-ae97-5b7d60ee12eb/environment-query-system-quick-start-06b.png)
    
    This will retrieve the Player Character at run-time as the Context.
    
    While we are focusing on Blueprint, in this case, a more optimized approach would be to create the Context through C++.
    

## 3 - EQS Setup

In this step, we jump into the EQS editor and set up the Tests for finding a location that has a line of sight to the Player Character.

1.  Inside **EQS\_FindPlayer**, drag off the **Root** node in the graph and add a **Points: Grid** node.
    
    ![Drag off the Root node in the graph and add a Points: Grid node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c700a1fa-00f5-4a45-b74d-f3e612b24b69/environment-query-system-quick-start-07.png)
    
    Several different types of **Generators** are used to create **Items** about a Context. Those items are then used in Tests (for example, how far is Item X from Context Y). From the results of the Tests, Items are culled or scored and can be used to determine what is the "best" (highest or lowest scoring) option.
    
    In this example, we will generate a series of points on a grid around the AI that will put it into a position where it can see the Player Character.
    
2.  In the **Details** panel, change the **GridHalfSize** to **800** and the **Space Between** to **150.0**.
    
    ![Change the GridHalfSize to 800 and the Space Between to 150.0 in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd0a7896-5f09-426a-a0af-45b6c72472ab/environment-query-system-quick-start-08.png)
    
    These settings are used to define the possible number of points to test against and the distance between those points. For performance reasons, you will want to keep this to a manageable size, as having a grid too large may start to impact your game's performance.
    
    Using the **Generate Around** field, you can determine where the grid should be placed (in this case, around the querier or AI character). While it will also work if we set **Generate Around** to use the Player Context we created, we don't want the AI to move up to a point on the grid near the Player if it already has a line of sight to the Player.
    
    The **Projection Data** option provides additional fields for determining how the grid is generated, for this example, we can leave these as default but you can come back and adjust these settings if you desire.
    
3.  Right-click on the **SimpleGrid** node and under **Add Test** select **Trace**.
    
    ![Right-click on the SimpleGrid node and under Add Test select Trace](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7eac337e-bb24-44bf-84d2-80b2b9f28812/environment-query-system-quick-start-09.png)
    
    The **Trace** Test will be used to determine if a point on the grid can see the Player Character.
    
    The order in which you add Tests to a Generator is irrelevant. Tests get sorted by putting the Filters first (so that subsequent Tests deal with as small of an Item collection as possible) and also filter by cost (so the distance filter will be executed before the Line of Sight filter).
    
4.  Right-click and add another Test, of the **Distance** type**.**
    
    ![Right-click and add another Test of the Distance type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccce2de8-cb3b-46a5-8d73-996d03f74286/environment-query-system-quick-start-10.png)
    
    After the **Trace** Test returns points that can see the Player Character, the **Distance** Test will be used to score those points based on their proximity to the Player Character.
    
5.  Select the **Trace** Test, then in the **Details** panel set the following options:
    
    ![Select the Trace Test and in the Details panel set the following options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbdacc7f-c9e8-4b26-a33e-f7710ad0a883/environment-query-system-trace-details.png)
    
    -   **Test Purpose** = **Filter Only**
    -   **Context** = **EQC\_PlayerContext**
    -   **Bool Match** = **Disabled**
    
    Here we are providing the Player Character as the point of reference (Context) in the **Trace** Test for visibility. By disabling the **Bool Match** option, we are stating that we want to filter out any points that cannot see the Player Character.
    
6.  Select the **Distance** Test, then in the **Details** panel, change the **Test Purpose** to **Score Only** and the **Scoring Factor** to **\-1.0**.
    
    ![Change the Test Purpose to Score Only and the Scoring Factor to -1.0 in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f48916fc-96a3-4e4b-9ed9-6973e2735816/environment-query-system-quick-start-12.png)
    
    The **Distance** Test Purpose is to score the Items returned and the Scoring Factor of -1.0 scores points that are closer to the Player's Character. If we leave this as 1.0, it will return points that are furthest away from the player which may cause the AI to run right past the Player Character in an attempt to reach the furthest point.
    
    There are additional scoring options such as clamping the scores to a minimum or maximum value, changing the **Scoring Equation** which changes the curve equation applied to the normalized score before being multiplied by the **Scoring Factor**, defining the **Normalization Type** or assigning a **Reference Value** used to normalize scores. For this example, we can leave these all at their default settings.
    

## 4 - Blackboard and Behavior Tree Setup

In this step, we set up the Blackboard Keys and lay out the branches of our Behavior Tree.

1.  In the **BB\_Enemy** Blackboard asset, create the following three Keys:
    
    ![Create the following three Keys in the BB_Enemy Blackboard asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e3ff46e-6df3-4c6a-81ab-d6fd2ca15a03/environment-query-system-quick-start-13-1.png)
    
    -   **Bool** named **HasLineOfSight**
    -   **Vector** named **MoveToLocation**
    -   **Object** with **Base Class** set to **Actor** named **TargetActor**
    
    These Keys will be used to update and move between branches in our Behavior Tree.
    
2.  Open the **BT\_Enemy** Behavior Tree and create the graph below using **Selectors**, **Sequences**, and a **Wait Task** node:
    
    Click image for full view.
    
    Above, we have three main branches. The left most branch uses a **Selector** node (which we have named **In Combat**) to switch between two **Sequence** nodes (one called **Attack** and another called **Move into Position**). When the AI is not executing the "In Combat" branch, it will execute the next branch which we have named **Patrolling**. In the event for some reason, the AI is not in either combat or patrolling, we have a fail-safe task to wait (which we have set to 1 second) before trying to move to another branch.
    

## 5 - Behavior Tree: Patrol Setup

In this step, we set up the patrolling branch of the Behavior Tree.

1.  Off the **Patrolling** Sequence node, add a **Move To** Task (set to **MoveToLocation**) and a **Wait** Task (set to **5** +/- **1** second).
    
    ![Add a Move To Task and a Wait Task oiff the Patrolling Sequence node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0532b5d-08a9-40df-ac2c-7d4238d43462/environment-query-system-quick-start-15.png)
    
    This will instruct the AI to move to the Blackboard Key **MoveToLocation** and then wait the specified time, however, we still need to define the vector value for **MoveToLocation.**
    
2.  From the Toolbar create a **New Task**, then in the **Content Drawer**, call it **BTT\_RandomLocation.**
    
    ![From the Toolbar create a New Task then in the Content Drawer call it BTT_RandomLocation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62ccaff5-2452-45b3-ac0a-30a42ccf53e3/environment-query-system-quick-start-16.png)
3.  In **BTT\_RandomLocation**, recreate the Blueprint Graph below:
    
    Using an **Event Receive Execute AI** node, off the **Controlled Pawn** you can **Get Actor Location** and use that as the **Origin** for the **Get Random Reachable Point in Radius** function (which we've set to **1000** as the **Radius**).
    
    Use the **Return Value** from the **GetRandomReachablePointInRadius** node as a **Branch** condition. Off the **True** pin, use the **Random Location** value and **Set Blackboard Value as Vector** with the Key being a **Blackboard Key Selector** variable called **MoveToLocation**.
    
    Off the **False** pin, **Set Blackboard Value as Vector** with **Get Actor Location** as the **Value**. This is if a random point is not found, we take the character's existing location before trying to find a new location. End the Task with both execution wires feeding into a **Finish Execute** node with **Success** enabled.
    
    Before adding this as a Task in the Behavior Tree, we'll want to be able to set the value of **MoveToLocation** so we need to make sure that it is set to **Instance Editable** by clicking the eye icon in the **My Blueprint** panel.
    
    ![Click the eye icon in the My Blueprint panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7152ac84-7384-4be7-943d-d85e9c0a2647/environment-query-system-quick-start-17b.png)
4.  In the Behavior Tree, add the **BTT\_RandomLocation** Task (setting **MoveToLocation** in the **Details** panel) as the first node under **Patrolling**.
    
    ![Add the BTT_RandomLocation Task in the Behavior Tree](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eca96ef0-08a0-453d-80a0-722b26d2f0fa/environment-query-system-quick-start-18.png)

## 6 - Behavior Tree: In Combat Setup

In this step, we set up the tasks associated with the In Combat branch including our EQS\_FindPlayer query used to find a location that has a line of sight to the Player Character.

1.  Right-click on the **In Combat** Selector and add a **Decorator** of the **Blackboard** type with the following settings:
    
    ![Right-click on the In Combat Selector and add a Decorator of the Blackboard type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c369925-fb7d-40de-897d-240c7d448fe5/environment-query-system-quick-start-19-1.png)
    
    -   **Observer aborts** set to **Lower Priority**
    -   **Blackboard Key** set to **TargetActor**
    
    Here we are stating that once TargetActor becomes set, execute the In Combat branch aborting any lower priority tasks.
    
2.  Right-click on the **Attack** Sequence and add a **Decorator** of the **Blackboard** type with the following settings:
    
    ![Right-click on the Attack Sequence and add a Decorator of the Blackboard type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bcc3be9-411e-4b23-bc7d-01c9d8619bfa/environment-query-system-quick-start-20-1.png)
    
    -   **Notify Observer** set to **On Value Change**
    -   **Observer aborts** set to **Lower Priority**
    -   **Blackboard Key** set to **HasLineOfSight**
    
    Here we are stating that if **HasLineOfSight** is Set, then execute the Attack branch. If **HasLineOfSight** is not set, execute a different branch until **HasLineOfSight** is set again.
    
3.  Off the **Attack** node add a **Rotate to face BB entry** (set to **TargetActor**).
    
    ![Off the Attack node, add a Rotate to face BB entry](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc811959-a7d5-416c-94ee-42f2c02fdd17/environment-query-system-quick-start-20b-2.png)
    
    This will cause the AI to rotate towards the TargetActor while in the "attack" branch. For this example, we do not have an attack to give our AI however this is something you can add later on if you desire.
    
4.  Off the **Move Into Position** node, use the **Run EQSQuery** node.
    
    ![Off the Move Into Position node use the Run EQSQuery node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68e16b25-9bda-413c-81df-5f7a7e48024c/environment-query-system-quick-start-20c-1.png)
    
    The Run EQSQuery node can be used to execute an EQS Query that will update the assigned Blackboard Key.
    
5.  In the **Details** panel for the **Run EQSQuery** node, set the **Blackboard Key** to **MoveToLocation** and the **Query Template** to **EQS\_FindPlayer**.
    
    ![Set the Blackboard Key to MoveToLocation and the Query Template to EQSFindPlayer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a72081b5-b961-4478-822d-e9e88603a486/environment-query-system-quick-start-21.png)
6.  Add a **MoveTo** (set to **MoveToLocation)** and **Rotate to face BB entry** (set to **TargetActor**) following the **Run EQS Query.**
    
    ![Add a MoveTo and Rotate to face BB entry following the Run EQS Query](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a14db7bc-cec1-496e-b8b9-ee357d227552/environment-query-system-quick-start-22.png)
    
    The Behavior Tree will run the EQS Query to update the Blackboard Key **MoveToLocation** and the AI will then move to that location and rotate to face the **TargetActor** (Player Character).
    
    The full Behavior Tree should look like the following:
    
    Click image for full view.
    

## 7 - AI Controller Setup

In this step, we set up our AI Controller to run our Behavior Tree as well as provide a way for the AI to see the Player Character using AI Perception.

1.  In the **AIC\_Enemy** Blueprint, add an **Event On Possess** and connect to a **Run Behavior Tree** (set to **BT\_Enemy)**.

![IAdd an Event On Possess and connect to a Run Behavior Tree](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a0749f4-03a1-4508-a9ca-67832860ead8/environment-query-system-quick-start-23.png)

1.  Add an **AIPerception** component with the following **AI Sight config** settings:
    
    ![Add an AIPerception component with the following AI Sight config settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa354bc7-7bbd-445b-925a-8e7ca5c83282/environment-query-system-quick-start-24.png)
    
    -   **Senses Config** add an **AI Sight config**
    -   **Detect Neutrals** set to **enabled**
    
    This will enable the AI to sense other Actors and fire an event when an Actor has been perceived by the Perception system. Currently, by default, Players do not get assigned an affiliation and can only be assigned one through C++ code. To circumvent this, we are enabling neutrals to be detected by the Perception system and will use Actor tagging to only perceive Actors tagged as "Player".
    
2.  For the **AIPerception** component, under **Events**, add an **On Target Perception Updated** then promote the **Actor** pin to a variable called **Perceived Actor.**
    
    Click image for full view.
    
    When the AI perceives something, that Actor will be stored as a variable which we will use later to update our Blackboard.
    
3.  Add two **Branch** nodes with the following conditions:
    
    Click image for full view.
    
    -   1st Branch **Condition** set to **Actor Has Tag** with the **Tag** of **Player** and the **Target** beingthe **Actor** from **Perception Updated**.
    -   2nd Branch **Condition** set to **Successfully Sensed** from the **Stimulus** pin of **Perception Updated** Event.
    
    Above, if the perceived Actor has the Tag of Player, the Branch continues to check if that Actor was successfully sensed or not. If it doesn't have the Tag of Actor (another enemy perhaps) it does not proceed on.
    
4.  Off the **False** pin of the 2nd Branch, add the 3 nodes shown below:
    
    ![Off the False pin of the 2nd Branch, add the 3 nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a26f8e8-eaf8-4aa5-a251-a4f6ff2e5037/environment-query-system-quick-start-27-1.png)
    
    Above we have a **Set Timer by Event** node (set to **8.0**) and promoted the **Return Value** to a variable called **LostSightTimer**. We then assign a Custom Event we created and called **LostSight** as the **Event Delegate.**
    
5.  Create 2 Functions in the **My Blueprint** panel called: **UpdateSightKey** and **UpdateTargetKey**.
    
    ![Create UpdateSightKey and UpdateTargetKey Functions in the My Blueprint panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff7940e3-40b8-4df3-8407-90c5a460f53a/environment-query-system-quick-start-28.png)
    
    We will use these two functions to update our Blackboard Keys that are used to make decisions in our Behavior Tree.
    
6.  For **UpdateSightKey**, add a **Bool** input called **HasLineOfSight**.
    
    ![Add a Bool input called HasLineOfSight](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a027f2c3-9fd6-4a48-b29d-4c91226b2e77/environment-query-system-quick-start-29.png)
7.  In **UpdateSightKey** right-click and get the **Blackboard** variable, then **Set Value as Bool** with **Key Name** using **HasLineOfSight**.
    
    ![In UpdateSightKey right-click and get the Blackboard variable and Set Value as Bool with Key Name using HasLineOfSight](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8b9a2d4-b65a-4918-be20-a5f6f22ce6c0/environment-query-system-quick-start-30.png)
    
    This enables us to use this function to pass through a bool value to our Blackboard Key, updating the **HasLineOfSIght** key.
    
8.  For **UpdateTargetKey**, add an **Actor** input called **TargetActor**.
    
    ![Add an Actor input called TargetActor for UpdateTargetKey](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0333a7c0-b77b-4247-9baf-f907a7145aa7/environment-query-system-quick-start-31.png)
9.  In **UpdateTargetKey** right-click and get the **Blackboard** variable, then **Set Value as Object** with **Key Name** using **TargetActor**.
    
    ![In UpdateTargetKey right-click and get the Blackboard variable and Set Value as Object with Key Name using TargetActor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef64132e-cda4-471d-bf8f-5bc5d16b115a/environment-query-system-quick-start-32.png)
    
    Similar to the UpdateSightKey function, this is used to update the Blackboard Key **TargetActor** with whatever Actor we pass through.
    
10.  Add **UpdateSightKey** and **UpdateTargetActor** functions to the **False** condition as shown:
    
    ![Add UpdateSightKey and UpdateTargetActor functions to the False condition](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e43b52ca-63ea-493b-9509-664ab3375762/environment-query-system-quick-start-33.png)
    
    When the AI Perception does not successfully sense the Actor who has the tag of Player, the false condition will start a timer (storing it in a handle for later) and will update the Blackboard Key **HasLineOfSight** to false. After the time specified (8.0 seconds), the Custom Event **LostSight** will execute, clearing the **TargetActor** Blackboard Key (meaning we no longer are targeting the Player and have lost sight of them).
    
    You can tune and tweak the amount of time before the AI "gives up" chasing the Player Character by adjusting the **Time** value on the Timer.
    
11.  Off the **True** pin of the 2nd Branch, use **LostSIghtTimer** and **Clear and Invalidate Timer by Handle**.
    
    ![Off the True pin of the 2nd Branch use LostSIghtTimer and Clear and Invalidate Timer by Handle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d05f2061-55d9-4f68-ae65-73b7378e0ad2/environment-query-system-quick-start-34-1.png)
    
    This will stop and reset the Timer used when losing sight of the Player Character.
    
12.  Add the **UpdateSightKey** (set to **enabled)** and **UpdateTargetKey** (set to **Perceived Actor**).
    
    ![Add the UpdateSightKey and UpdateTargetKey](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2e1632a-0593-4abf-b0ef-fc90d1421927/environment-query-system-quick-start-35.png)
    
    The full graph should look similar to below:
    
    Click image for full view.
    
    Our AI Controller is now set up, runs our Behavior Tree, and updates our Blackboard Keys based on when we perceive an Actor with the tag Player through the AI Perception system.
    

## 8 - Final Setup

In this step, we set up the enemy AI Character Blueprint, add the Tag Player to the Player Character Blueprint so it can be perceived by the AI, and add a NavMeshBoundsVolume and some meshes so the AI knows how to move around the environment and we can break line of sight easier.

1.  Open **BP\_Enemy**, in the **Details** panel, enable **Use Controller Rotation Yaw** and set **AI Controller Class** to **AIC\_Enemy**.
    
    Click image for full view.
    
    For the AI to execute the rotate task inside the Behavior Tree, we need to enable Controller Rotation Yaw. We also assign the custom AI Controller class that has our logic in it and runs the Behavior Tree. Optionally, we deleted all the script that was copied over from the Player Character (as well as the Camera Component) as we will not need it for the AI Character.
    
2.  From the **Modes** panel, add a **NavMeshBoundsVolume** to the Level and scale it so it encapsulates the Level.
    
    ![Add a Nav Mesh Bounds Volume to the Level and scale it so it encapsulates the Level from the Modes panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0eb375dd-8d9b-47cd-be1b-3c6d9891add5/environment-query-system-quick-start-37.png)
    
    You can press the **P** key to toggle on/off the debug grid which shows navigatable paths in green. Or during gameplay with the console command **show Navigation** **true** (to display) or **false** (to hide).
    
3.  Right-click on the **BP\_ThirdPersonCharacter** in the Level, then select **Edit BP\_hirdPersonCharacter**.
    
    ![Right-click on the BPThirdPersonCharacter in the Level, then select Edit BPThirdPersonCharacter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a34da034-53ec-4fa9-8e7d-47cd5bcbd5d3/environment-query-system-quick-start-38.png)
4.  In the **Details** panel, search for **Tag**, then add a **Tag** called **Player**.
    
    ![Search for Tag, then add a Tag called Player in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98186f9c-740b-4b91-a6c6-00e3a9f0c37f/environment-query-system-quick-start-39.png)
    
    Inside our **AIC\_Enemy** Blueprint when the AI Perception system perceives an Actor, this Actor has the tag of Player so our Branch will be evaluated as True.
    
5.  Inside the Level, scale up and add multiple versions of the **Cube Mesh** to provide additional cover points to break the line of sight.
    
    ![Scale up and add multiple versions of the Cube Mesh to provide additional cover points to break line of sight](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/024c2de7-6453-4ae9-bc5a-60119eecb784/environment-query-system-quick-start-40-1.png)
6.  Click the **Play** button from the Toolbar to play in the Level.
    

## 9 - End Result

While playing in the Editor, the AI will patrol around randomly until seeing the Player. After seeing the Player, it will rotate and face the Player and attempt to move to a new location when losing sight of the Player. Using EQS, it will find a location that will provide a line of sight to the Player but remain a distance away. If it does not see the Player again while moving to a new location, after some time the AI will give up chasing and go back to patrolling as portrayed in the video below.

You can use the [AI Debugging Tools](/documentation/en-us/unreal-engine/ai-debugging-in-unreal-engine) to view any active EQS queries (in addition to Behavior Trees or Perception info). To activate AI Debugging at runtime, press the **'** (apostrophe) key, then select 1 (for general AI debugging), 2 (for Behavior Trees), 3 (for EQS), or 4 (for AI Perception). Below, we activate AI Debugging and bring up the EQS Debugging tools.

While the EQS Debugging tools are running, you can see the points from our Grid test along with their score values. You will also see which point was selected, denoted with the text **Winner**. These tools are useful to see which points are being evaluated and why one point may have been selected over another point based on the score values.

In addition to using the EQS Debugging tools, there is a special type of Pawn called the **EQS Testing Pawn** that can be used to debug EQS queries while in the Editor. You can create this Pawn, by creating a new Blueprint Class of the **EQS Testing Pawn** Class.

![You can create  EQS Testing Pawn by creating a new Blueprint Class of the EQS Testing Pawn Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ccee25d-65ab-47cd-9fde-179702d2ddd5/environment-query-system-quick-start-end-01.png)

Our current setup uses the Player Character as a Context for evaluation in our EQS Test. To test while the game is not running, we would need to make a slight modification to the **EQS\_PlayerContext** Blueprint and override the **Provide Actors Set** function.

![We need to make a slight modification to the EQS_PlayerContext Blueprint and override the Provide Actors Set function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/012abd2d-da85-4d56-b38f-337270777724/environment-query-system-quick-start-end-02.png)

We can use **Get All Actors of Class** set to **BP\_ThirdPersonCharacter** which provides the **Resulting Actors Set**:

![We can use Get All Actors of Class set to BP_ThirdPersonCharacter which provides the Resulting Actors Set](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/678de407-b211-4588-94fd-040fdf6cba57/environment-query-system-quick-start-end-03.png)

When adding the EQS Testing Pawn to the Level, in the **Details** panel, you can assign the **Query Template** (which we've set to our **EQS\_FindPlayer** query).

![You can assign the Query Template in the Details panel,](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d6a4914-096d-4ff2-9768-7cb31fa405d1/environment-query-system-quick-start-end-04.png)

This enables you to see the results of your test while in you are in the Editor as seen below:

EQS Data is also being recorded through VisLog which you can reference. Please see **Visual Logger** for more information.
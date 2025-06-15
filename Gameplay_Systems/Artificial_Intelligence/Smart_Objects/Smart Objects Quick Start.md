# Smart Objects Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/smart-objects-in-unreal-engine---quick-start](https://dev.epicgames.com/documentation/en-us/unreal-engine/smart-objects-in-unreal-engine---quick-start)  
**Processed:** 2025-06-14 16:51:15

---

## Overview

**Smart Objects** are objects placed in a Level that AI Agents and players can interact with. These objects contain all the information needed for those interactions.

At a high level, Smart Objects represent a set of activities in the Level that can be used through a reservation system. This system keeps track of all the Smart Objects in the Level and allows an AI Agent to "reserve" a Smart Object so no other Agent can use it until the Smart Object becomes available again.

## Goals

In this Quick Start guide, you will learn how to create and use Smart Objects with an AI Agent.

## Objectives

-   Create the AI Gameplay Behavior and Behavior Definition that the AI Agent can use when it reaches a Smart Object.
    
-   Create a Smart Object that holds the Behavior Definition to play an animation montage.
    
-   Create simple AI behavior with a Behavior Tree and Behavior Tree Tasks.
    
-   Create the AI Agent that can search for and use Smart Objects in the level.
    

## 1 - Required Setup

1.  Create a new **Blueprint** project based on the **Third Person** template.
    
2.  From the main menu, go to **Settings > Plugins** to open the **Plugins** window.
    
    ![Open the Plugins window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8be4418a-28c4-4a3e-8c73-7ef6e0a6fe86/so-qs-plugins-1.png)
3.  Go to the **Gameplay** section and enable the **Smart Objects**, **AI Behaviors**, and **Gameplay Behavior Smart Objects** plugins. Restart the editor if prompted.
    
    ![Enable the Smart Objects plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5df8930b-1b21-4cf1-bda1-107b61fa04aa/so-qs-plugins-2.png) ![Enable the AI Behaviors plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8efba39e-d212-4d58-b173-063d951155e3/so-qs-plugins-3.png) ![Enable the Gameplay Behavior Smart Objects plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/435d8057-2920-4cb9-a09c-1c1bfabbbbbc/so-qs-plugins-4.png)

### Section Results

In this section, you created a new project and enabled the Smart Objects and AI Behaviors plugins. You are now ready to create the AI Gameplay Behavior for your AI Agent.

## 2 - Create the AI Gameplay Behavior

In this section, you will create the Gameplay Behavior and Gameplay Config Blueprints that define what your Agent will do when it reaches a Smart Object Slot.

1.  In the **Content Browser**, right-click and select **Blueprint Class** from the **Create Basic Asset** section.
    
    ![Create a new Blueprint Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a7b90e4-d866-49de-93db-ba931b52a378/so-qs-createbp.png)
2.  In the **Pick Parent Class** window, expand the **All Classes** section, then search for and select **Gameplay Behavior**. Click **Select** and name the new Asset **BP\_SO\_Behavior\_PlayMontage**.
    
    ![Select the Gameplay Behavior class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6aa33f52-9b55-4ff8-8c37-f10d60c30740/so-qs-createbehavior-1.png)
3.  Create a new Blueprint class, then search for and select **Gameplay Behavior Config**. Click **Select** and name the new Asset **BP\_SO\_BehaviorConfig**.
    
    ![Select the Gameplay Behavior Config class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e94543df-e7b9-4afd-8385-ebebd198a18a/so-qs-createbehavior-2.png)
4.  In the **Content Browser**, double-click **BP\_SO\_BehaviorConfig** to open it. Go to the **Details** panel and click the **Behavior Class** dropdown. Select **BP\_SO\_Behavior\_PlayMontage**. Compile and save the Blueprint.
    
    ![Add the BP_SO_Behavior_PlayMontage to the Behavior Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e7bc031-1dce-4c04-81ae-71dc2cac36a6/so-qs-createbehavior-3.png)
5.  In the **Content Browser**, double-click **BP\_SO\_Behavior\_PlayMontage** to open it. Click the **Override** dropdown next to **Functions** and select **OnTriggeredCharacter**.
    
    ![Override the OnTriggeredCharacter function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b93342c-90a3-416c-808f-6bf712241fd0/so-qs-createbehavior-4.png)
6.  Right-click the **Avatar** pin of the **Event OnTriggeredCharacter** node and select **Promote to Variable**.
    
    ![Right-click the Avatar pin of the Event OnTriggeredCharacter node and select Promote to Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ee94c74-ce82-4f52-a480-5cb5e8e439b2/so-qs-createbehavior-5.png)
7.  Drag the **Avatar** variable to the **Event Graph** and select **Get Avatar**. Drag from the **Avatar** node, then search for and select **Get Component by Class**.
    
    ![Search for and select Get Component by Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1cfecb48-4aeb-4cc7-92d1-f54fc5e94cd4/so-qs-createbehavior-6.png)
8.  Click the **Component Class** dropdown, then search for and select **Skeletal Mesh Component**.
    
    ![Add the Skeletal Mesh component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37b0e671-1522-4890-9ed8-eebf411bfd59/so-qs-createbehavior-7.png)
9.  Right-click in the **Event Graph,** then search for and select **Play Montage**.
    
    1.  Connect the **Return Value** pin of the **Get Component by Class** node to the **In Skeletal Mesh Component** pin of the **Play Montage** node.
        
    2.  Connect the **Set Avatar** node to the **Play Montage** node.
        
    
    ![Add a Play Montage node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8176d784-0f69-4967-9f9a-1293fdf42fff/so-qs-createbehavior-8.png) ![Connect the Play Montage node to the Set Avatar node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75ef8886-5433-499a-8199-749fc02f38ad/so-qs-createbehavior-9.png)
10.  Click the **Montage to Play** dropdown on the **Play Montage** node. Select an animation montage from the list.
    
    ![Select an animation montage to play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3dab7eb-b233-4b95-9978-f3a7b3665958/so-qs-createbehavior-10.png)
    
    If you don't have animations available, you can get free animation asset packs from [Fab](https://www.fab.com/), such as the [Animation Starter pack](https://www.fab.com/listings/98ff449d-79db-4f54-9303-75486c4fb9d9). You can also convert any Animation Sequence to an Animation Montage by right-clicking it and selecting **Create > Create AnimMontage**.
    
11.  Drag the **Avatar** variable to the **Event Graph** and select **Get Avatar**. Drag from the **Avatar** node, then search for and select **End Behavior**.
    
    ![Add the End Behavior node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/232f8428-6da0-4f58-94d9-22244391a7db/so-qs-createbehavior-11.png)
12.  Connect the **On Completed** and **On Interrupted** pins from the **Play Montage** node to the **End Behavior** node.
    
    ![Connect On Completed and On Interrupted to the End Behavior node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab1c3d7c-8785-4386-b317-3931d42ea8aa/so-qs-createbehavior-12.png)
13.  Compile and save the Blueprint.
    
    This example uses the **Play Montage** node, as opposed to the **Play Anim Montage** node to use the **On Completed** and **On Interrupted** pins to end the behavior. This ensures the Smart Object remains occupied until the animation finishes playing.
    

### Section Results

In this section, you created the Gameplay Behavior and Gameplay Config Blueprints that the Agent will use to play an animation montage once it reaches a Smart Object Slot. You can now create the Behavior Definition that will be used by the Smart Object.

## 3 - Create the Smart Object Definition Data Asset

In this section, you will create the SmartObject Definition Data Asset that will define the behavior for each Slot of the Smart Object.

1.  In the **Content Browser**, right-click and select **Miscellaneous > Data Asset**.
    
    1.  In the **Pick Class for Data Asset Instance** window, search for and select **Smart Object Definition**.
        
    2.  Click **Select** to create the Asset and name it **SO\_Definition\_PlayMontage**.
        
    
    ![Select Miscellaneous - Data Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/193aa911-2357-4a9a-ad7e-0e67f3f19cbb/so-qs-createdefinition-1.png) ![Select the Smart Object Definition](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e65b6d5f-ed66-4261-8ed3-0fb438c5e6c0/so-qs-createdefinition-2.png)
2.  In the **Content Browser**, double-click **SO\_Definition\_PlayMontage** to open it. Scroll down to the **Smart Object** section and click the **Add (+)** button next to **Slots** to add a new Slot. This is the Slot that will be used by the AI Agent when performing the behavior.
    
    ![Click the Add (+) button next to Slots** **to add a new Slot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2455aa3c-a968-4393-919b-897b02f6b303/so-qs-createdefinition-3.png)
3.  Click the **Add (+)** button next to **Default Behavior Definitions** and select **Gameplay Behavior Smart Object Behavior Definition** for **Index 0**. Click the **Gameplay Behavior Config** dropdown and select **BP\_SO\_BehaviorConfig**.
    
    ![Add a new Default Behavior Definition](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/229702db-52c0-4d7c-8f26-7b795ef46787/so-qs-createdefinition-4.png)
4.  Save and close the Blueprint.
    

### Section Results

In this section, you created the SmartObject Definition Data Asset that defines each Slot of the Smart Object and its default behavior definition.

## 4 - Create a Smart Object

In this section, you will create a Smart Object that can be found and used by an Agent in the level.

1.  In the **Content Browser**, right-click and select **Blueprint Class** from the **Create Basic Asset** section.
    
    ![Create a new Blueprint Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02bbf74e-2c95-4a05-9272-386b66884ff7/so-qs-createbp.png)
2.  In the **Pick Parent Class** window, click the **Actor** class button to create the asset. Name the new Asset **BP\_SO\_RunBT**.
    
    ![Select the Actor class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/042612e7-f2b2-4b77-997a-4f507dd21893/so-qs-createobject-1.png)
3.  In the **Content Browser**, double-click **BP\_SO\_RunBT** to open it. Go to the **Components** window and click the + **Add** button. Search for and select **Smart Object**.
    
    ![Select the SOComponent component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cee78e4e-38a2-42b3-bca7-a72f89f6f786/so-qs-createobject-2.png)
4.  With the **SmartObject** component selected, go to the **Details** panel and scroll down to the **Smart Object** section. Click the **Definition Asset** dropdown and select **SO\_Definition\_PlayMontage**.
    
    ![Add the Definition Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db479a4c-9f1b-4dee-bd89-618aa67bfe24/so-qs-createobject-3.png)
5.  Compile and save the Blueprint.
    

### Section Results

In this section, you created a Smart Object and added the Behavior Definition that defines the default behavior of its Slot.

## 5 - Create the Behavior Tree for the AI Agent

In this section, you will create the necessary behavior for the AI Agent to search for and use Smart Objects in the Level. You will use a simple Behavior Tree and two custom Behavior Tree Tasks to accomplish this.

### Create the Behavior Tree and Blackboard

1.  In the **Content Browser**, right-click and select **AI > Blackboard**. Name the Blackboard **BB\_SO\_Agent**.
    
    ![Create a Blackboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a9c9922-4335-42fb-ad98-20d3bf4b6b94/so-qs-createbt-1.png)
2.  Double-click **BB\_SO\_Agent** to open it. Click the **New Key** dropdown and select **SO Claim Handle**. Name the key **ClaimHandle**. Save and close the Blackboard.
    
    ![Add a SmartObject Claim Handle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e904337e-2bcb-4f29-8b6e-da924cb105d1/so-qs-createbt-2.png)
3.  In the **Content Browser**, right-click and select **AI > Behavior Tree**. Name the Behavior Tree **BT\_SO\_Agent**.
    
    ![Create a Behavior Tree](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/831282c5-2235-4f71-8e88-cbbe8e83fd5e/so-qs-createbt-3.png)

### Create the Behavior Tree Tasks

**Finding Smart Objects**

1.  In the **Content Browser**, right-click and select **Blueprint Class** from the **Create Basic Asset** section.
    
    ![Create a new Blueprint Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b237e1fd-2df6-4d64-a27e-5e071c9d46ca/so-qs-createbp.png)
2.  In the **All Classes** section, search for and select **BT Task Blueprint Base**, then click **Select**. Name the Blueprint **BTT\_FindSmartObject**.
    
    ![Search for and select BT Task Blueprint Base, then click Select](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ab6ee19-a0b0-4439-97e8-fefeaea7cfdc/so-qs-createbt-4.png)
3.  In the **Content Browser**, right-click **BTT\_FindSmartObject** and select **Duplicate**. Name the new Blueprint **BTT\_UseSmartObject**.
    
    ![Duplicate BTT_FindSmartObject](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bfb052ba-4136-4abe-b2c6-cd99e79fc7f6/so-qs-createbt-5.png)
4.  In the **Content Browser**, double-click **BTT\_FindSmartObject** to open it. In the **Event Graph**, right-click, then search for and select **Event Receive Execute AI**.
    
    ![Add the Event Receive Execute AI node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac7779da-3e67-4966-8486-05fbe686bed0/so-qs-createbt-6.png)
5.  Drag from the **Owner Controller** pin of the **Event Receive Execute AI** node, then search for and select **Get Blackboard**.
    
    1.  Right-click the **Return Value** pin of the **Get Blackboard** node and select **Promote to Variable**. Name the variable **Blackboard**.
        
    2.  Connect the **Event Receive Execute AI** node to the **Set Blackboard** node.
        
    
    ![Add the Get Blackboard node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca989462-930c-4247-9ba3-63b243c9131b/so-qs-createbt-7.png) ![Connect the Set Blackboard node to the Event Receive Execute AI node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/973423da-9dd5-4867-ba44-d776ffd20720/so-qs-createbt-8.png)
6.  Drag from the **Controlled Pawn** pin of the **Event Receive Execute AI** node, then search for and select **Get Actor Location**.
    
    1.  Drag from the **Return Value** of the **Get Actor Location** node, then search for and select **Subtract**.
        
    2.  Drag from the **Return Value** of the **Get Actor Location** node, then search for and select **Add**.
        
    3.  Set the **X**, **Y**, and **Z** values of both nodes to **2000**. This creates a search box of 4000 x 4000 units, or 40 x 40 meters around the Agent.
        
    
    ![Add the Get Actor Location node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe28c0c2-bfb7-4abd-8a0e-2a34cfc924c6/so-qs-createbt-9.png) ![Add Subtract and Add nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2906d038-066e-4a69-b186-314b411d105a/so-qs-createbt-10.png)
7.  In the **Event Graph**, right-click then search for and select **Make Box**.
    
    1.  Connect the **Subtract** node to the **Min** pin of the **Make Box** node.
        
    2.  Connect the **Add** node to the **Max** pin of the **Make Box** node.
        
    
    ![Add a Make Box node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ba090da-454d-438d-83de-518d126f62f6/so-qs-createbt-11.png) ![Connect the Make Box node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec123b5d-4d85-49dd-bc80-a099a6e99346/so-qs-createbt-12.png)
8.  In the **Event Graph**, right-click then search for and select **Get Smart Object Subsystem**.
    
    1.  Drag from the **Smart Object Subsystem** node, then search for and select **Find Smart Objects**.
        
    2.  Drag from the **Request** pin of the **Find Smart Objects** node and select **Make SmartObjectRequest**.
        
    
    ![Add a Get Smart Object Subsystem node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c268d10-ccf5-4e06-a43d-1025160faf44/so-qs-createbt-13.png) ![Add a Find Smart Objects node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51098a5d-c54f-4eaa-a14b-1379987ae060/so-qs-createbt-14.png) ![Select Make SmartObjectRequest](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e7e0e7d-1187-4bb9-8d9c-0137861af306/so-qs-createbt-15.png)
9.  Connect the **Return Value** pin of the **Make Box** node to the **Query Box** pin of the **Make SmartObjectRequest** node.
    
    1.  Drag from the **Filter** pin of the **Make SmartObjectRequest** node and select **Make SmartObjectRequestFilter**.
        
    2.  Drag from the **Behavior Definition Classes** pin and search for then select **Make Array**.
        
    3.  Click the dropdown of the **Make Array** node and select **GameplayBehaviorSmartObjectBehaviorDefinition**.
        
    4.  Connect the **Set Blackboard** node to the **Find Smart Objects** node.
        
    
    ![Connect the Return Value pin of the Make Box node to the Query Box pin of the Make SmartObjectRequest node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bc4748e-ae23-43e3-a7b0-d326753f18e3/so-qs-createbt-16.png) ![Select GameplayBehaviorSmartObjectBehaviorDefinition from the dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26d12d47-2ec5-4f87-9313-fc0fc97a552e/so-qs-createbt-17.png)
10.  This is what the Blueprint looks like so far.
    
    ![The Blueprint so far](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a35109be-b628-4ddd-b23f-9544d2485289/so-qs-createbt-18.png)
11.  Right-click the **Out Results** pin of the **Find Smart Objects** node and select **Promote to Variable**. Connect the **Out Results** node to the **Blackboard** node.
    
    1.  Drag from the pin of the **Out Results** node, then search for and select **Is Valid Index**.
        
    2.  Drag from the **Is Valid Index** node, then search for and select **Branch**. Connect the **Out Results** node to the **Branch** node.
        
    
    ![Right-click the Out Results pin of the Find Smart Objects node and select Promote to Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/338c1151-8658-44f9-a5dc-da1ed1b66c76/so-qs-createbt-19.png) ![Select Is Valid Index](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/533e0ea4-0c95-48e7-9b03-da73e46d7aa6/so-qs-createbt-20.png) ![Select Is Valid Index](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45967916-d895-431f-8547-59b68e3dcb18/so-qs-createbt-21.png)
12.  Drag from the **False** pin of the **Branch** node, then search for and select **Finish Execute**. The **Out Results** will be invalid if no nearby Smart Objects match the search criteria.
    
    ![Drag from the False pin of the Branch node, then search for and select Finish Execute](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5782b86-90f9-4412-9cfd-897c98b42da7/so-qs-createbt-22.png)
13.  Create a **Smart Object Subsystem** node in the **Event Graph**. Drag from the node, then search for and select **Claim**.
    
    1.  Connect the **True** pin of the **Branch** node to the **Claim** node.
        
    2.  Drag the **Out Results** variable to the **Event Graph** and select **Get Out Results**. Drag from the node, then search for and select **Random Array Item**.
        
    3.  Drag from the **Random** node and connect it to the **Request Results** pin of the **Claim** node.
        
    
    ![Add a Claim node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4471704d-e727-42be-b7bf-a6b6fcf3aed2/so-qs-createbt-23.png) ![Drag from the node, then search for and select Random Array Item](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cefaf2e8-1d84-426c-96cd-5b08bcdb8956/so-qs-createbt-24.png) ![Drag from the Random node and connect it to the Request Results pin of the Claim node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d281fa0-7e35-41ee-abfa-84e33e12313c/so-qs-createbt-25.png)
14.  Right-click the **Return Value** pin of the **Claim** node and select **Promote to Variable**. Name the variable **ClaimHandle**.
    
    1.  Drag from the **Claim Handle** node pin, then search for and select **Is Valid Smart Object Claim Handle**.
        
    2.  Drag from the **Return Value** of the **Is Valid Smart Object Claim Handle** node, then search for and select **Branch**.
        
    
    ![Right-click the Return Value pin of the Claim node and select Promote to Variable. Name the variable ClaimHandle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4ed8914-23cd-41dd-b52f-6bf946ce1e4f/so-qs-createbt-26.png) ![Drag from the Claim Handle node pin, then search for and select Is Valid Smart Object Claim Handle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b50d4b1-56e0-4046-8ca7-a5a31c5a74f0/so-qs-createbt-27.png) ![Drag from the Return Value of the Is Valid Smart Object Claim Handle node, then search for and select Branch](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7f48330-3d3f-4fc1-8e0c-21b3e9192853/so-qs-createbt-28.png)
15.  Drag from the **False** pin of the **Branch** node, then search for and select **Finish Execute**.
    
    ![Drag from the False pin of the Branch node, then search for and select Finish Execute](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a056c02-4f0f-4278-a0f8-03927c90c0fe/so-qs-createbt-22.png)
16.  Drag the **Blackboard** variable to the **Event Graph** and select **Get Blackboard**.
    
    1.  Drag from the **Blackboard** node, then search for and select **Set Value as SOClaim Handle**.
        
    2.  Connect the **True** pin of the **Branch** node to the **Set Value as SOClaim Handle** node.
        
    3.  Right-click the **Key Name** pin of the **Set Value as SOClaim Handle** node and select **Promote to Variable**.
        
    4.  With the **Key Name** variable selected, go to the **Details** panel and enable the **Instance Editable** checkbox. Set the **Default Value** to **ClaimHandle**.
        
    
    ![Drag from the Blackboard node, then search for and select Set Value as SOClaim Handle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d77a81d8-aff1-4346-ab8c-b437822f8ddd/so-qs-createbt-29.png) ![Right-click the Key Name pin of the Set Value as SOClaim Handle node and select Promote to Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b726f29-82f3-48ab-8ee3-354fdb4c86db/so-qs-createbt-30.png) ![Enable the Instance Editable checkbox. Set the Default Value to ClaimHandle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0cd5869-9054-4446-873a-fac4d34cd821/so-qs-createbt-31.png)
17.  Drag the **ClaimHandle** variable and connect it to the **Value** pin of the **Set Value as SOClaim Handle** node.
    
    ![Drag the ClaimHandle variable and connect it to the Value pin of the Set Value as SOClaim Handle node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c78d931-9bcd-43a8-b9e5-0364e9fa602c/so-qs-createbt-32.png)
18.  Drag from the **Set Value as SOClaim Handle** node, then search for and select **Finish Execute**. Enable the **Success** checkbox on the node.
    
    ![Add a Finish Execute node and enable the Success checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d899ff65-e307-438e-a302-beae6353c1be/so-qs-createbt-33.png)
19.  Compile and save the Blueprint.
    

**Use the Smart Object**

1.  In the **Content Browser**, double-click **BTT\_UseSmartObject** to open it. In the **Event Graph**, right-click and search for then select **Event Receive Execute AI**.
    
    ![Add the Event Receive Execute AI node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d7bed4a-c49b-4c87-94c5-f9586922e326/so-qs-createbt-6.png)
2.  Drag from the **Owner Controller** pin of the **Event Receive Execute AI** node, then search for and select **Get Blackboard**.
    
    ![Drag from the Owner Controller pin of the Event Receive Execute AI node, then search for and select Get Blackboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd50f868-f840-4811-a6f0-219992fccc40/so-qs-createbt-34.png)
3.  Drag from the **Return Value** pin of the **Get Blackboard** node, then search for and select **Get Value as SOClaim Handle**.
    
    ![Drag from the Return Value pin of the Get Blackboard node, then search for and select Get Value as SOClaim Handle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/129ef402-cf21-4288-85c4-13c0e2a7d0dc/so-qs-createbt-35.png)
4.  Right-click the **Key Name** pin of the **Get Value as SOClaim Handle** node and select **Promote to Variable**.
    
    1.  With the **Key Name** variable selected, go to the **Details** panel and enable the **Instance Editable** checkbox. Set the **Default Value** to **ClaimHandle**.
    
    ![Enable the Instance Editable checkbox. Set the Default Value to ClaimHandle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41c0aab7-e6e3-44fe-9aff-b626f0b477c3/so-qs-createbt-31.png)
5.  Drag from the **Return Value** pin of the **Get Value as SOClaim Handle** node, then search for and select **Use Claimed Gameplay Behavior Smart Object**.
    
    1.  Connect the **Get Value as SOClaim Handle** node to the **Use Claimed Smart Object** node.
        
    2.  Drag from the **Owner Controller** pin of the **Event Receive Execute AI** node and connect it to the **Controller** pin of the **Use Claimed Smart Object** node.
        
    
    ![Drag from the Return Value pin of the Get Value as SOClaim Handle node, then search for and select Use Claimed Smart Object](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/904189ed-99ee-4c05-b28d-5edc90402869/so-qs-createbt-36.png) ![Drag from the Owner Controller pin of the Event Receive Execute AI node and connect it to the Controller pin of the Use Claimed Smart Object node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3583991d-3c1e-4abc-add0-fb3012573d4c/so-qs-createbt-37.png)
6.  Drag from the **On Succeeded** pin of the **Use Claimed Smart Object** node, then search for and select **Finish Execute**. Enable the **Success** checkbox on the node.
    
    ![Drag from the On Finished pin of the Use Claimed Smart Object node, then search for and select Finish Execute](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9be6c01-8c24-46bb-82d3-1c83855da0ca/so-qs-createbt-38.png)
7.  Compile and save the Blueprint.
    

**Create the Behavior Tree**

1.  In the **Content Browser**, double-click **BT\_SO\_Agent** to open it. Drag from the **Root** node and select **Selector**.
    
    ![Drag from the Root node and select Selector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14424046-1f50-48d1-b02f-1127f1fb7a52/so-qs-createbt-39.png)
2.  Drag from the **Selector** node and select **Sequence**.
    
    1.  Drag from the Selector node and select **Wait**. This node will have the Agent wait for 5 seconds before searching for a new Smart Object, if the initial search was unsuccessful.
        
    2.  Make sure the **Sequence** node is to the left of the **Wait** node. This ensures the Sequence will be executed first in the Behavior Tree.
        
    
    ![Drag from the Selector node and select Sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3d84373-e054-4983-9044-5c286ac0633e/so-qs-createbt-40.png)
3.  Drag from the **Sequence** node and select **BTT\_FindSmartObjects**.
    
    ![Drag from the Sequence node and select BTT_FindSmartObjects](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/363bd090-b4df-4e7d-991c-22d8f2fed3ea/so-qs-createbt-41.png)
4.  Drag from the **Sequence** node and select **BTT\_UseSmartObjects**.
    
    ![Drag from the Sequence node and select BTT_UseSmartObjects](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4854914-57e9-41e7-bfb4-b89a940c52f3/so-qs-createbt-42.png)
5.  Drag from the **Sequence** node and select **Wait**. With the node selected, set the **Wait Time** to **2.0** and **Random Deviation** to **0.5**. This node will have the Agent wait between 1.5 and 2.5 seconds before searching for a new Smart Object.
    
    ![Drag from the Sequence node and select Wait](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e26ee2f-614b-4254-966a-aa7bcc99fd26/so-qs-createbt-43.png) ![Final Behavior Tree](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10b3f414-d8f5-4564-a8e7-345842379869/so-qs-createbt-44.png)
6.  Save and close the Behavior Tree.
    

**Section Results**

In this section, you created the Behavior Tree and Behavior Tree Tasks that allow the Agent to find and use Smart Objects in the Level.

## 6 - Create the AI Agent

In this section, you will create the AI Agent that will search for Smart Objects in the level.

1.  In the **Content Browser**, double-click the **BP\_ThirdPersonCharacter** Blueprint to open it.
    
    ![Double-click the ThirdPersonCharacter Blueprint to open it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8699918b-a38a-4d85-9d0c-1d21a557117e/so-qs-createagent-1.png)
2.  Select all the nodes in the **Event Graph** and delete them. Right-click in the **Event Graph**, then search for and select **Event Possessed**.
    
    ![Right-click in the Event Graph and search for then select Event Possessed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d405012-5fa8-4a6a-88b5-f9b5c410861e/so-qs-createagent-2.png)
3.  Drag from the **New Controller** pin of the **Event Possessed** node, then search for and select **Cast to AI Controller**. Connect the **Event Possessed** node to the **Cast to AIController** node.
    
    ![Drag from the New Controller pin of the Event Possessed node, then search for and select Cast to AI Controller](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dad029c3-7555-49d6-8b31-71d88f256cc3/so-qs-createagent-3.png)
4.  Drag from the **As AIController** pin of the **Cast to AIController** node, then search for and select **Run Behavior Tree**. Click the **BTAsset** dropdown and select **BT\_SO\_Agent**.
    
    ![Drag from the As AIController pin of the Cast to AIController node, then search for and select Run Behavior Tree](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7480a8b-450a-4b29-b3d6-158af7ea3ba2/so-qs-createagent-4.png)
5.  Compile and save the Blueprint.
    

**Section Results**

In this section, you created the AI Agent Blueprint that will search for Smart Objects in the Level. You also modified the animation Blueprint to make sure the animation montage can play correctly.

## 7 - Test the Smart Objects

You will now test the Agent to make sure it can find and use the Smart Objects in the Level.

1.  From the Main Toolbar, click **Add Content (****+****) > Volumes > NavMeshBoundsVolume** to add a new **Navigation Mesh** actor to your Level. Scale the Mesh to cover your Level so the Agent can navigate to its destination.
    
    ![Add a NavMeshBoundsVolume to your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48ddbc27-4f00-4aa4-a157-8da83182b86c/so-qs-testsos-0.png)
2.  Drag several **BP\_SO\_RunBT** Blueprints to your level.
    
    ![Drag several BP_SO_RunBT** **Blueprints to your level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9af74092-5ebc-459d-9032-61a1dec56571/so-qs-testsos-1.png)
3.  Drag the **ThirdPersonCharacter** Blueprint to your Level.
    
    ![Drag the ThirdPersonCharacter** **Blueprint to your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33d4422b-23c3-4f43-8932-eca024db361b/so-qs-testsos-2.png)
4.  Press **Simulate** to see the Agent find and use Smart Objects in the Level.
    
    ![Press Simulate to see the Agent find and use Smart Objects in the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cffebda1-7eb5-4b4b-95c0-d6dd3d1940a1/so-qs-testsos-demo.gif)

**Section Results**

In this section, you confirmed that the Agent can find and use Smart Objects in the Level.
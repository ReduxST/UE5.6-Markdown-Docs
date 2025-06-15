# Behavior Tree Quick Start Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/behavior-tree-in-unreal-engine---quick-start-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/behavior-tree-in-unreal-engine---quick-start-guide)  
**Processed:** 2025-06-14 16:09:50

---

In the **Behavior Tree Quick Start Guide**, you will learn how to create an enemy AI that responds to seeing the Player and proceeds to chase them. When losing sight of the Player, after a few seconds (which can be adjusted based on your preference), the AI will give up chasing and randomly move around the environment until seeing the Player again as seen in the example video below.

By the end of this guide, you will have an understanding of the following systems: 

1.  Blueprint Visual Scripting
    
2.  AI Controllers
    
3.  Blackboards
    
4.  Behavior Trees
    
5.  Behavior Tree Services
    
6.  Behavior Tree Decorators
    
7.  Behavior Tree Tasks
    

## 1 - Required Project Setup

In this first step, we set up our project with the assets we'll need for our AI character to get around the environment. 

For this guide, we are using a new **Blueprint Third Person Template** project.

1.  Open the **Content Drawer**, then right-click on the **ThirdPerson** folder and create a **New Folder** called **AI**.
    
    ![Open the Content Drawer then right-click on the ThirdPerson folder and create a New Folder called AI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c35a40a3-473e-4022-84f6-fee629bb9977/1-create-folder.png)
2.  In the **ThirdPerson > Blueprints** folder, drag the **BP\_ThirdPersonCharacter** onto the **AI** folder and select **Copy Here**.
    
    ![In the ThirdPerson Blueprints folder drag the BP_ThirdPersonCharacter onto the AI folder and select Copy Here](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1ee0a6d-2682-41ef-a08f-a2c9b12da39e/2-copy-character.png)
3.  In the **AI** folder, create a new **Blueprint Class** based on the **AIController** class.
    
    ![In the AI folder create a new Blueprint Class based on the AIController class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37a44c01-57df-43fb-be56-2927cfb3095e/3-create-ai-controller.png)
4.  Name the **AIController** Blueprint **Enemy\_Controller** and the **BP\_ThirdPersonCharacter** Blueprint **Enemy\_Character**.
    
    ![Name the AIController Blueprint Enemy_Controller and the BP_ThirdPersonCharacter Blueprint  Enemy_Character](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2fe1b9c8-9c67-410e-a8a3-896a16bc2476/4-rename-and-save.png)
5.  Open **Enemy\_Character**, then delete all the script from the graph.
    
6.  Select the **Character Movement** component then set **Max Walk Speed** in the **Details** panel to **120.0**.
    
    *Click image for full view.*
    
    This reduces the speed of our AI Character's movement around the environment when patrolling and not chasing the Player. 
    
7.  Select **Class Defaults** from the Toolbar, then in the **Details** panel, assign the **Enemy\_Controller** as the **AI Controller Class**.
    
    *Click image for full view.*
    
    We are going to place our AI in the world. If you spawn the AI after the world is loaded, change the **Auto Possess AI** setting to **Spawned**.
    
8.  From the **Content Drawer**, drag the **Enemy\_Character** into the Level. 
    
9.  From the **Place Actors** panel, drag a **NavMeshBoundsVolume** into the Level.
    
    ![From the Place Actors panel drag a NavMeshBoundsVolume into the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f60cae85-029b-4b65-bba0-f24099568210/7-nav-mesh.png)
10.  With the **NavMeshBoundsVolume** selected, press **R** and scale the volume to encapsulate the entire Level.
    
    ![With the NavMeshBoundsVolume selected, press R and scale the volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fb38724-3cbf-4356-a7ad-42fb175f7027/8-scale-nav-mesh.png)
    
    This will generate a Navigation Mesh that enables our AI character to move around the environment. You can press the **P** key to toggle the display of the NavMesh in the Viewport (green areas indicate possible navigation locations).
    
    During gameplay, you can use the **Show Navigation** console command to toggle the display of the NavMesh on/off.
    

Our project setup is complete, in the next step we will set up our **Blackboard** asset.

## 2 - Blackboard Setup

In this step, we create our **Blackboard** asset, which is essentially the brain of our AI. Anything we want our AI to know about will have a **Blackboard Key** that we can reference. We'll create keys for keeping track of the Player, whether or not the AI has a line of sight to the Player, and a location where the AI can move to when it is not chasing the Player.

1.  In the **Content Drawer**, click **+Add** and under **Artificial Intelligence**, select **Blackboard** and call it **BB\_Enemy**.
    
    ![In the Content Drawer click  Add and under Artificial Intelligence select  Blackboard and call it  BB_Enemy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b7289e7-89d5-4001-9c53-f71d56fb8b49/1-create-blackboard.png)
2.  Inside the **BB\_Enemy** Blackboard, click the **New Key** button and select **Object**.
    
    ![Inside the BB_Enemy Blackboard click the New Key button and select Object](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f903292b-51cc-4ea2-a79f-f93537b42544/step-2-2.png)
    
    The **Blackboard** asset consists of two panels: the **Blackboard**, which enables you to add and keep track of your **Blackboard Keys** (variables to monitor), and **Blackboard Details**, which enables you to name and specify the type of Keys.
    
3.  For the **Object** key, enter **EnemyActor** as the **Entry Name** and **Actor** as the **Base Class**.
    
    ![For the Object key enter EnemyActor as the Entry Name and Actor as the Base Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3345a699-1008-4f0f-99e4-e3c1a2197a19/step-2-3.png)
4.  Add another **Key** with the **Key Type** set to **Bool** called **HasLineOfSight**.
    
    ![Add another Key with the Key Type set to Bool called HasLineOfSight](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/448e1b22-0eb5-4408-84d8-4b248a88db68/step-2-4.png)
    
    This will be used to keep track of whether or not the AI has a line of sight to the Player.
    
5.  Add another **Key**, with the **Key Type** set to **Vector** called **PatrolLocation**.
    
    ![Add another Key with the Key Type set to Vector called PatrolLocation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f28a8960-8612-44d6-8e81-cc987a3fcf3f/step-2-5.png)
    
    This will be used to keep track of a location in the Level where the AI can move when it is not chasing the Player.
    

Our **Blackboard** is set up with the things we need to track. In the next step, we will lay out our **Behavior Tree**.

## 3 - Behavior Tree Layout

In this step, we will lay out the flow of our **Behavior Tree** and the states that we want our AI to enter. Laying out your **Behavior Tree** with the states you anticipate your AI could be in as a visual flow will give you an idea of what type of logic and rules you will need to create to enter those states.

1.  In the **Content Drawer**, click **+Add** and under **Artificial Intelligence**, select **Behavior Tree** and call it **BT\_Enemy**.
    
    ![In the Content Drawer click  Add and under Artificial Intelligence select  Behavior Tree and call it BT_Enemy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/727fe68e-8480-4958-a73d-50ee2681e61e/create-behavior-tree.png)
    
    Naming conventions may vary, but it's generally good practice to add an acronym of the asset type to the name.
    
2.  Open the **BT\_Enemy** and assign the **BB\_Enemy** as the **Blackboard Asset**.
    
    ![Open the BT_Enemy assign the BB_Enemy as the Blackboard Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36e650bb-2685-4ecf-9877-524646826700/behavior-tree-quick-start-step-3-2-1.png)
    
    If you do not see the **Blackboard Keys** we created, clear the **Blackboard Asset** by clicking the yellow arrow, then re-assign the **Enemy\_BB** to refresh the keys.
    
    The **Behavior Tree** consists of three panels: the **Behavior Tree** graph, where you visually layout the branches and nodes that define your behaviors, the **Details** panel, where properties of your nodes can be defined, and the **Blackboard**, which shows your **Blackboard Keys** and their current values when the game is running and is useful for debugging.
    
3.  In the graph, left-click and drag off the **Root** and add a **Selector** node.
    
    ![In the graph left-click and drag off the Root and add a Selector node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a30a097f-f800-4240-8663-dd2e4d97e674/behavior-tree-quick-start-step-3-3.png)
    
    **Composites** are a form of flow control and determine how the child branches that are connected to them execute.
    
    | Composites | Description |
    | --- | --- |
    | **Selector** | Executes branches from left-to-right and is typically used to select between subtrees. Selectors stop moving between subtrees when they find a subtree they successfully execute. For example, if the AI is successfully chasing the Player, it will stay in that branch until its execution is finished, then go up to the selector's parent composite to continue the decision flow.  |
    | **Sequence** | Executes branches from left-to-right and is more commonly used to execute a series of children in order. Unlike Selectors, the Sequence continues to execute its children until it reaches a node that fails. For example, if we had a Sequence to move to the Player, check if they are in range, then rotate and attack. If the check if they are in range portion failed, the rotate and attack actions would not be performed |
    | **Simple Parallel** | Simple Parallel has two "connections". The first one is the Main Task, and it can only be assigned a Task node (meaning no Composites). The second connection (the Background Branch) is the activity that's supposed to be executed while the main Task is still running. Depending on the properties, the Simple Parallel may finish as soon as the Main Task finishes, or wait for the Background Branch to finish as well. |
    
4.  For the **Selector** node, in the **Details** panel, change the **Node Name** to **AI Root**. 
    
    ![For the Selector node in the Details panel change the Node Name to AI Root](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14327e2d-076f-43ad-b4e2-02e6f1d0c3c8/behavior-tree-quick-start-step-3-4.png)
    
    Renaming nodes in the graph is a good way to easily identify, from a high-level, what the node accomplishes. In this example, we name it **AI Root** as this is the real "Root" of our Behavior Tree which will switch between our child branches. The default Root node that is automatically added when creating a Behavior Tree is used to configure properties of the Behavior Tree as well as assign the Blackboard asset it's using. 
    
5.  Left-click and drag off **AI Root** and add a **Sequence** node named **Chase Player**.
    
    Click image for full view.
    
    We use a Sequence node here as we plan to tell the AI to do a sequence of actions: rotate towards the player, change their movement speed, then move to and chase the Player. 
    
6.  Left-click and drag off the **AI Root** node and add a **Sequence** node called **Patrol**.
    
    Click image for full view.
    
    For our AI, we will use the **Sequence** node to find a random location on the map, move to that location, then wait there for a while before repeating the process of finding a new location to move to. 
    
    You may also notice the numbers in the upper-right corner of the nodes:
    
    ![The numbers in the upper-right corner of the nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a3cf0ee-009a-44b0-9ff8-a507540d7bca/behavior-tree-quick-start-step-3-6b.png)
    
    This indicates the order of operation. **Behavior Trees** execute from left-to-right and top-down, so the arrangement of your nodes is important. The most important actions for the AI should usually be placed to the left, while the less important actions (or fallback behaviors) are placed to the right. Child branches execute in the same fashion and should any child branch fail, the entire branch will stop executing and will fail back up the tree. For example, if **Chase Player** failed, it would return up to **AI Root** before moving on to **Patrol**.
    
7.  Drag off **AI Root** then add a **Wait** Task to the right of **Patrol** with **Wait Time** set to **1.0**. 
    
    Click image for full view.
    
    You will notice that this node is purple, indicating that it is a **Task** node. Task nodes are the actions that you want the **Behavior Tree** to perform. The **Wait** Task acts as a catch-all if the **Behavior Tree** fails both Chase Player and Patrol. 
    
8.  Drag off the **Chase Player** and add a **Rotate to Face BBEntry** node.
    
    Click image for full view.
    
    This particular **Task** enables you to designate a **Blackboard Entry** that you want to rotate and face, in our case the **Enemy Actor** (Player). Once you add the node, if you look in the **Details** panel, the **Blackboard Key** will automatically be set to **EnemyActor** because it filters for the Actor blackboard variable and it is the first one in the list. You can adjust the **Precision** option if you want to tune the success condition range as well as change the **Node Name**.
    
9.  From the **Toolbar**, click the **New Task** button.
    
    ![From the Toolbar click the New Task button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b8d65ae-ab95-4741-a1ed-d64546f9cd26/behavior-tree-quick-start-step-3-9.png)
    
    In addition to using the built-in Tasks, you can create and assign your custom Tasks that have additional logic that you can customize and define. This Task will be used to change the movement speed of the AI so that it runs after the Player. When you create a new Task, a new **Blueprint** will automatically be created and opened.
    
    Click image for full view.
    
10.  In the **Content Drawer**, rename the new asset as **BTT \_ChasePlayer**.
    
    ![In the Content Browser rename the new asset as BTT _ChasePlayer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f42f936-8859-4408-a23a-74bcb69a872a/behavior-tree-quick-start-step-3-10.png)
    
    It's a good practice to immediately rename any newly created **Tasks**, **Decorators** or **Services** when you create them. Proper naming conventions would be to prefix the name of the asset with the type of asset you create such as **BTT** for Behavior Tree Tasks, **BTD** for Behavior Tree Decorators, or **BTS** for Behavior Tree Services. 
    
11.  Inside the **BT\_Enemy**, add the **BTT\_ChasePlayer** Task followed by a **Move To**. 
    
    Click image for full view.
    
    Our new Task has no logic in it yet, but we will come back and add the logic for changing the movement speed of our AI character after which, the AI will Move To the EnemyActor (Player).
    
12.  Create a new **Task** and rename it **BTT\_FindRandomPatrol**, then connect it to **Patrol**. 
    
    Click image for full view.
    
13.  Add a **Move To** Task and set the **Blackboard Key** to **PatrolLocation**. 
    
    Click image for full view.
    
    This will instruct the AI to Move To the PatrolLocation which will be set inside the BTT\_FindRandomPatrol Task. 
    
14.  Add a **Wait** Task following **Move To** with **Wait Time** to **4.0** and **Random Deviation** to **1.0**. 
    
    Click image for full view.
    
    This instructs the AI to wait at PatrolLocation for 3-5 seconds (Random Deviation adds + or - a second to Wait Time). 
    

The framework for our **Behavior Tree** is complete. In the next step, we will add the logic for changing the movement speed of the AI, finding a random location to navigate to when the AI is patrolling, and the logic for determining when the AI should be chasing the player or patrolling.

## 4 - Task Setup - Chase Player

In this step, we set up our **Chase Player Task** to change the movement speed when chasing the Player.

1.  Inside **BTT\_ChasePlayer**, right-click and add an **Event Receive Execute AI** node. 
    
    ![Inside BTT_ChasePlayer right-click and add an Event Receive Execute AI node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76b5eab0-a579-4778-902c-8edab759502a/behavior-tree-quick-start-step-4-1.png)
    
    The Event Receive Execute AI node is fired when this Task is activated inside the **Behavior Tree**. 
    
    You should always select the AI version of **Event Receive Execute**, **Event Receive Abort**, and **Event Receive Tick** if the Agent is an AI Controller. If both generic and AI event versions are implemented, only the more suitable one will be called, meaning the AI version is called for AI, and the generic one otherwise.
    
2.  Off the **Controlled Pawn** pin, use a **Cast to Enemy\_Character** node.
    
    ![Off the Controlled Pawn pin use a Cast to Enemy_Character node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2632f93-6bcc-4c77-b0df-5478fe498830/2-event-receive-ai.png)
    
    Here, we are accessing the **Character Blueprint** for our AI called **Enemy\_Character** by using a Cast node.
    
3.  Inside the **Content Drawer**, open the **Enemy\_Character** Blueprint and add a **Function** called **Update Walk Speed**. 
    
    ![Inside the Content Drawer open the Enemy_Character Blueprint and add a Function called Update Walk Speed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a880339-05b4-4e05-820d-74f11b64e009/behavior-tree-add-new-function.png)
    
    This function will be called from our Behavior Tree and will be used to change the AI's movement speed. 
    
    Technically we could access the **Character Movement** Component off the Cast node in our Chase Player Task and adjust the movement speed from within the Task, however having the Behavior Tree directly change properties of sub-objects is not a recommended best practice. Instead, we will have the Behavior Tree call a function inside the Character which will then make the modifications we need.�
    
4.  In the **Details** panel for the **Update Walk Speed** function, add a **Float** input called **NewWalkSpeed**. 
    
    ![In the Details panel for the Update Walk Speed function add a Float input called NewWalkSpeed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b69cbead-d355-43df-b29c-08e70560336a/behavior-tree-new-walk-speed.png)
5.  Drag the **CharacterMovement** Component off the Components tab. 
    
    ![Drag the **CharacterMovement** Component off the Components tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5353c335-3154-4917-bec8-1d66a7f05005/behavior-tree-function-1.png)
6.  Click and drag off the pin of **Character Movement** and from the actions menu type in **Set Max Walk Speed**, then click **Set Max Walk Speed** from the menu. 
    
    ![Click and drag off the pin of Character Movement and from the actions menu type in Set Max Walk Speed then click that function from the menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/514e1f01-c1d3-4eff-a526-324935da2f30/behavior-tree-function-2.png)  
    
7.  Use **Set Max Walk Speed** and connect as shown below. 
    

![Use Set Max Walk Speed and connect as shown below](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df0f9c97-7aad-416b-b9db-8a34d6cfd10d/behavior-tree-function-complete.png)  

When we call this function from the Behavior Tree, we can pass through a value to be used as the new speed.

1.  Back inside the **BTT\_ChasePlayer** Task, from the **As Enemy Character** node, call **Update Walk Speed** set to **500.0** and connect as shown.
    
    ![Back inside the BTT_ChasePlayer Task from the As Enemy Character node call Update Walk Speed set to 500.0 and connect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f627e647-c7cb-4e4f-aa26-34c8316a9fd2/behavior-tree-chase-player-function-call.png)
    
    Don't see the **Update Walk Speed** function you created? You may need to **Compile** the **Enemy\_Character** Blueprint before trying to add it to the **Chase Player Task**.
    
2.  Following **Update Walk Speed**, add two **Finish Execute** nodes and connect as shown below.
    
    ![Following Update Walk Speed, add two Finish Execute nodes and connect ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0da3a8b-363c-4783-a45e-98a0ab0681f7/behavior-tree-finish-execute.png)
    
    Here we mark the Task as successfully finishing when we successfully cast to the Enemy\_Character. If the controlled Pawn is not Enemy\_Character, we need to handle this case so we mark the Task as unsuccessful which will abort the Task.
    
3.  Right-click the **New Walk Speed** pin, then promote it to a variable and call it **ChaseSpeed**.
    
    ![Right-click the New Walk Speed pin then promote it to a variable and call it ChaseSpeed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94ad94db-b45c-40b7-b026-1c071a441160/behavior-tree-chase-speed-variable-promoted.png)
4.  For **ChaseSpeed**, make sure to enable **Instance Editable**.
    
    ![For ChaseSpeed make sure to enable Instance Editable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/446bde4e-5cd7-44df-b509-f4688cb937f9/behavior-tree-chase-speed-variable.png)
    
    By promoting this to an **Instance Editable** variable, the value of **Max Walk Speed** can be set from outside of this Blueprint and will be available as a property inside our **Behavior Tree**. 
    
    ![The value of Max Walk Speed can be set from outside of this Blueprint and will be available as a property inside our Behavior Tree](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9dcabb0f-ed11-4092-b213-656b55cd0ab9/behavior-tree-quick-start-step-4-7b.png)
    
    We can now easily change the value of **Chase Speed** that is being sent to the **Enemy\_Character** Blueprint enabling us to tune and tweak how fast our AI chases the Player.
    

Our **Chase Player Task** is complete, in the next step, we will set up the **Find Random Patrol Task** logic to get a random location for the AI to move to.

## 5 - Task Setup - Find Random Patrol

In this step, we set up our **Find Random Patrol Task** so our AI moves to a random location when it is not chasing the Player. 

Implementing a Blueprint Behavior Tree Task is a clever way to quickly iterate, but, if performance is a concern, you may decide to move to a native Behavior Tree Task.

1.  Inside **BTT\_FindRandomPatrol**, use **Event Receive Execute AI** and **Cast to Enemy\_Character** and connect them.
    
    ![nside BTT_FindRandomPatrol use Event Receive Execute AI and Cast to Enemy_Character](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8749d685-28ba-4e66-978e-31fe4ba27d8b/behavior-tree-find-random-patrol.png)
2.  Off **As Enemy Character**, call **Update Walk Speed** and promote **New Walk Speed** to a variable called **Patrol Speed** with the following settings:
    
    Click image for full view.
    
    **\- Variable Name** to **PatrolSpeed**  
    **\- Instance Editable** to **Enabled**  
    **\- Patrol Speed (Default Value)** to **125.0**
    
    Here we are lowering the enemy movement speed while patrolling.
    
3.  Off **Controlled Pawn**, **Get Actor Location** then **GetRandomReachablePointInRadius** with the **Return Value** connected to a **Branch**.
    
4.  Promote the **Radius** on **GetRandomReachablePointInRadius** to a variable with the following settings:
    
    Click image for full view.
    
    **\- Variable Name** to **PatrolRadius**  
    **\- Instance Editable** to **Enabled**  
    **\- Patrol Radius (Default Value)** to **1000.0**
    
    Here we are finding a random location within 1000 units of the enemy character's current location. We are also using a Branch node to handle the edge case that a random point to move to is not found.
    
5.  Off the **Random Location** pin, use **Set Blackboard Value as Vector** with the **Key** promoted to a variable called **PatrolLocation**.
    
6.  Use another **Set Blackboard Value as Vector** node with the **Value** coming from **Get Actor Location**.
    
7.  Continuing from the previous step, connect as shown below with both nodes resulting in **Finish Execute** marked **Success**.
    
    Click image for full view.
    
    If the enemy finds a random position to move to, it will be stored in the Blackboard as the location to move to. If a location is not found, it will use its current location and stay put before trying a new location. We still need to handle the edge case that the Controlled Pawn is not Enemy\_Character.
    
8.  Off the **Cast Failed** pin of the **Cast** node, use **Finish Execute** with **Success** disabled.
    
    Click image for full view.
    
    If the Controlled Pawn is not Enemy\_Character, this Task will be marked as unsuccessful and will be aborted.
    

Our **Find Random Patrol Task** is complete. In the next step, we will learn more about **Decorators** and how they can be used as conditionals as well as set up our AI Controller.

## 6 - AI Controller Setup

In this step, we do a little bit of work inside the AI Controller in preparation for the final step, setting up a **Decorator** to determine which branch of our **Behavior Tree** to enter. 

1.  In the **Content Drawer**, open the **Enemy\_Controller** Blueprint and add an **Event On Possess** node. 
    
2.  Off **Event On Possess**, add a **Run Behavior Tree** node with **BTAsset** set to **BT\_Enemy**. 
    
    ![Off Event On Possess and add a Run Behavior Tree node with BTAsset set to BT_Enemy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4374474c-2d5b-40d2-933f-c9ea952fca4f/step-6-3.png)
    
    **Run Behavior Tree** is a contextual functional call that targets AI Controller Class Blueprints and enables you to execute the assigned **Behavior Tree** asset.
    
3.  In the **Components** window, click **\+ Add** and search for and add an **AIPerception Component**.
    
    ![In the Components window click Add Component and search for and add an AIPerception Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85ffe041-af2e-4bea-a81d-e0355a1d89f2/2-ai-perception.png)
    
    The **AI Perception Component** is used to create a stimuli listener within the **AI Perception System** and gathers registered stimuli (in our case, we can use Sight) that you can respond to. This will give us the ability to determine when the AI actually sees the Player and can react accordingly.
    
4.  In the **Details** panel for the **AIPerception Component**, add an **AI Sight config** and enable **Detect Neutrals**.
    
    ![In the Details panel for the AIPerception Component add an AI Sight config and enable Detect Neutrals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/762379df-8ac3-4f2a-8492-f39f9fa1e63c/3-perception-setup.png)
    
    The **Detection by Affiliation** properties enable you to set up team-based AI that fights alongside teammates of the same affiliation and attack members of the opposing affiliation.  **Actors** by default are not assigned an affiliation and are considered neutral.
    
    Currently, you cannot assign affiliation through Blueprint, therefore we are enabling the **Detect Neutral** flag to detect the Player. As an alternative, we are going to use **Actor Tagging** to determine which Character is the Player and force AI Character(s) to only chase Actors tagged as Player.
    
5.  In the **Events** section for **AIPerception**, click the **+** sign next to **On Target Perception Updated**.
    
    ![In the Events section for AIPerception click the plus sign next to On Target Perception Updated](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c69b6a0-618d-4acb-895b-260513693f3c/3b-click-add-event.png)
6.  Off **On Target Perception Updated** in the graph, add an **Actor Has Tag** node with **Tag** set to **Player**.  
    
    ![Off On Target Perception Updated in the graph and add an Actor Has Tag node with Tag set to Player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1662305b-7d59-4887-b9bf-62e6369fec63/behavior-tree-quick-start-step-6-7.png)
7.  Off the **Stimulus** pin, add a **Break AIStimulus** node.
    
8.  Add a **Branch** node with the **Condition** shown below. 
    
    ![Add a Branch node with the Condition](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/823adff0-b037-40ca-95ad-2f9decad9738/behavior-tree-quick-start-step-6-8.png)
    
    Here we are checking if the Actor was successfully Sensed and if that Actor has the Tag of the Player. 
    
    You can select the **Break AIStimulus** node and in the **Details** panel use **Hide Unconnected Pins** to hide all pins that are not connected so your graph looks similar to the one above.
    
9.  Off the **False** of the **Branch**, use **Set Timer by Event** with **Time** set to **4.0**. 
    
10.  Right-click and promote **Time** to a variable and call it **Line Of Sight Timer**. 
    
    *Click image for full view.*
    
    This Variable and the value assigned will determine how long before the AI gives up chasing the Player at which point, the attached Event will execute. 
    
11.  Right-click on the **Return Value** of **Set Timer by Event** and promote it to a Variable called **EnemyTimer**. 
    
    *Click image for full view.*
    
    This stores a reference to the Timer by way of a **Handle**. This Handle can be called upon through script to invalidate itself and clear any associated Events (preventing the associated Event from being executed). We can use this later in the event the AI sees the player again before the Line of Sight Timer runs out, which stops the AI from losing sight of the player and giving up the chase. 
    
12.  Create a **Custom Event** and call it **StartEnemyTimer** and connect it to the **Event** pin of **Set Timer by Event**. 
    
    *Click image for full view.*
    
13.  Right-click, then under **Variables > AI**, add a **Get Blackboard** node.
    
    ![Add a Get Blackboard node under Variables  AI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0283c48a-5ad8-46f1-80af-76b41737bca7/behavior-tree-quick-start-step-6-12.png)
14.  Off **Blackboard**, use **Set Value as Bool** and **Set Value as Object** and connect as shown below. 
    
    ![Off Blackboard and use Set Value as Bool and Set Value as Object and connect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6953df1-c9fc-4716-83fd-7a18fd635340/behavior-tree-quick-start-step-6-13.png)
    
    This enables us to update the **Blackboard Keys** defined with new Values. 
    
15.  Right-click and promote both **Key Names** to **Variables** called **HasLineOfSight** and **EnemyActor** respectively. 
    
16.  **Compile** the Blueprint and set the **Default Values** for both **Key Names** to **HasLineOfSight** and **EnemyActor** respectively. 
    
    *Click image for full view.*
    
17.  Off the **True** of the **Branch**, use **Get EnemyTimer** then **Clear and Invalidate Timer by Handle**. 
    
    *Click image for full view.*
    
    When the AI sees the Player, it will clear the Line Of Sight Timer until it loses sight of the Player again (where a new Line Of Sight Timer will start). 
    
18.  Copy and Paste the **Blackboard** node, **Set Value as**, and **Key Name** nodes as shown. 
    
    *Click image for full view.*
    
19.  On the **Set Value as Bool** node, enable the **Bool Value** and drag the **Actor** pin to the **Object Value** as shown. 
    
    *Click image for full view.*
    
    This sets the **Blackboard Key Values** for **Has Line Of Sight** to **True** and **EnemyActor** to the **Actor** we perceived (which we have set up to only trigger if it is the Player). 
    
20.  Click **Compile** to compile then close the Blueprint.
    
    *Click image for full view.*
    
    The final graph should look similar to the above. 
    

## 7 - Decorator and Final Setup

In this final section, we adjust a few settings on the Player Character and Enemy Character Blueprints. We also set up our **Decorator** in our **Behavior Tree** which will determine what branch we can enter based on a specified condition. 

1.  Inside the **Content Drawer** under **Content > ThirdPersonBP > Blueprints**, open the **ThirdPersonCharacter** Blueprint. 
    
2.  In the **Details** panel, search for and add a **Tag** set to **Player**. 
    
    !\[ In the Details panel search for and add a Tag set to Playerbtqs-step-6-18.png)
    
    By setting adding this Tag of Player, the AI can now perceive and react to the Player. 
    
3.  Open up the **Enemy\_Character** Blueprint inside your **AI** folder. 
    
4.  In the **Details** panel, search for **Rotation** and enable **Use Controller Rotation Yaw**. 
    
    ![n the Details panel, search for Rotation and enable Use Controller Rotation Yaw](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2bc5af8-1c2e-4f76-a71b-c519d222a41f/behavior-tree-quick-start-step-6-19.png)
    
    This will cause the AI to rotate properly when the **Rotate to Face BB Entry** is called from our **Behavior Tree**. 
    
    Don't see the Pawn options? You may need to click the **Class Defaults** button from the Toolbar first.
    
5.  Open up the **BT\_Enemy** and right-click on **Chase Player**, then under **Add Decorator..**, select **Blackboard**. 
    
    *Click image for full view.*
    
    When you right-click on a node in a **Behavior Tree**, you can add subnodes that provide additional functionality: 
    
    | Subnode | Description |
    | --- | --- |
    | **Decorator** | Also known as conditionals. These attach to another node and make decisions on whether or not a branch in the tree, or even a single node, can be executed. |
    | **Service** | These attach to both **Task** and **Composite** nodes, and will execute at their defined frequency as long as their branch is being executed. These are often used to make checks and to update the **Blackboard**. These take the place of traditional Parallel nodes in other Behavior Tree systems. |
    
    We are going to use the **Blackboard Decorator** to determine the value of a **Blackboard Key**, which when valid, is going to allow this branch to execute. 
    
6.  Select the **Blackboard Based Condition** that was added and set the following settings in the **Details** panel. 
    
    *Click image for full view.*
    
    -   **Observer aborts** to **Both**
    -   **Blackboard Key** to **HasLineOfSIght**
    -   **Node Name** to **Has Line of Sight?**
    
    Here we are stating that when the **HasLineOfSight** value **Is Set** (or is true), execute this **Chase Player** branch. The **Observer aborts** setting of **Both** states that when the **Blackboard Key** we assigned changes, abort our self (**Chase Player**) and any lower priority Tasks. This means that when the value of **HasLineOfSight** changes and is not set, abort self (**Chase Player**), at which point the next branch (**Patrol**) will execute. When the **HasLineOfSight** value becomes **Is Set** , the observer will abort lower priority Tasks as well enabling the **Chase Player** branch to be executed. 
    
7.  **Compile** and close the **Behavior Tree** then **Play** in the Editor. 
    

### End Result

You should now be able to test your AI and it will follow you when it sees you.

When the AI loses sight of you, it will still attempt to track you down and regain line of sight. After the time you have entered the **Line Of Sight Timer** value, it will give up chasing you and return to patrolling.

You can watch the **Behavior Tree** in action as you are playing to see how it switches between the different branches. The variables can also be watched inside the **Behavior Tree** as you are playing to get an idea of what values the AI current has.

## 8 - On Your Own!

Now that your AI Character will chase the Player and return to patrolling after losing sight of the Player for a specified duration of time, try to add some of the following elements to your **Behavior Tree** on your own!

-   In the **Behavior Tree**, for both **Move To** Tasks, add a new **Service** that incorporates the functionality from the **Task** that precedes it.
    -   Our original **Behavior Tree** uses a separate **Task** for adjusting the movement speed (in the case of chasing the Player) and finding a random location to patrol to and decreasing movement speed (in the case of patrolling). Convert these to **Services** that are attached to the **Move To Task**.
        
    -   **Hint:** The script in the **Services** will be similar to the script in each **Task**, however instead of **Event Receive Execute AI**, you want to use **Event Receive Activation AI**. Because they are a **Service**, you will also not need a **Finish Execute** node.
        
-   Instead of using a random patrol point to move to, create a **Patrol Path Blueprint** that contains an array variable of vector values that AI can move between.
    -   **Hint:** Cycle through and get the next entry in the array to move the AI between the locations, then update the **Blackboard Key** value **PatrolLocation** based on the current entry in your array.
-   When losing line of sight to the Player, move the AI to the last known location of the Player rather than getting the current location of the Player.
    -   **Hint:** On the **Move To** command for **Turning and Chasing the Player**, you will need to specify a location instead of **EnemyActor** as it is currently set to get the location of **EnemyActor** (which retrieves the Player's current location).
-   Add attacking functionality to the AI once they reach the Player.
    -   **Hint:** Add a new **Composite** node as the **Background Task** for **Turning and Chasing the Player**. Once the AI reaches the Player, add a **Task** node for an Attack animation.
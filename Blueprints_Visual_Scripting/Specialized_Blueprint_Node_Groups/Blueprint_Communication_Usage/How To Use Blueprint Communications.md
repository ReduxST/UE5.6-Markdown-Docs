# How To Use Blueprint Communications

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-communications-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-communications-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:29

---

On this page you will learn step-by-step how to set up and use different methods of **Blueprint Communication**.

### Direct Blueprint Communications

Below we have two **Blueprints** in our level that we want to have communicate with one another. Suppose we wanted the Cube Blueprint to communicate to the Sparks Blueprint to turn itself off when a player character enters the cube. This can easily be achieved with **Direct Blueprint Communications**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d4c05da-c967-40a2-b20d-cd79c7b1aabd/2_1.png)

-   The cube above is a Blueprint created using the **Shape\_Cube** mesh and its collision has been set to **OverlapOnlyPawn** so it acts as a trigger. Also enable **Generate Overlap Events**
-   The sparks above are the **Blueprint\_Effect\_Sparks** asset (included with starter content).

Using Direct Blueprint Communication, we would do the following:

1.  In the **Shape\_Cube** Blueprint, under **My Blueprint** click the ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7565128-a7e2-495d-aa3b-3ab8add59d8c/plus_button.png) button on the Variables category: ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d39d630-bc22-4071-bf4e-66d8e23fae1d/myblueprint_variable.png)
    
2.  In the **Details** panel, under **Variable Type** select the type of Blueprint you wish to access.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99893ae9-c40e-47fd-8dae-eb77c037b638/2_3.png)
    
    Hover over the **Blueprint\_Effects\_Sparks** Variable Type and select **Reference** from the list.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80f72d21-2876-44f4-84de-a2010f387827/2_3_1.png)
    
    Here we are stating that we want to access a **Blueprint\_Effect\_Sparks** Blueprint.
    
3.  In the **Details** panel, update the sections outlined below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93b19a08-fb1c-460e-9070-ca343885f776/2_4.png)
    1.  **Variable Name** - give the variable a descriptive name such as **TargetBlueprint**.
    2.  **Variable Type** - this should be the type of Blueprint that you want to access.
    3.  **Editable** - make sure this is checked to expose the variable and make it public which will allow you to access it in the Level Editor.
    4.  **Tool Tip** - add a short description of what the variable does or what it will reference.
4.  With the **Shape\_Cube** Blueprint selected in the level, in the Level Editor under **Details** you should see the exposed variable created in the previous step.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34737c7e-d025-406b-b935-614679d3364b/2_6.png)
    
    1.  Click the **None** drop-down box to assign a Target Blueprint.
    2.  All instances of the Blueprint placed in the level are displayed here, allowing you to specify which instance is the **Target Blueprint**.
    
    Here we are stating which **Blueprint\_Effect\_Sparks** Blueprint Actor we want to affect that is placed in our level; this is considered the Instance Actor. If we had multiple sparks in our level and we only wanted to turn off one of them, we could choose which instance of the Blueprint we want to affect here by setting it as the **Target Blueprint**.
    
5.  Instead of using the drop-down, you can click the ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb3008a6-a7f5-49c0-82b3-53e22814a672/2_7.png) icon, then click on the object you want to reference that is placed in your level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18d625b0-79b2-43ba-89bc-7f8750353c17/2_8.png)
    
    You can only set the **Target Blueprint** to target the specified Variable Type (in our case **Blueprint\_Effect\_Sparks**).
    
6.  In the **Shape\_Cube** Blueprint, while holding down the **Ctrl** key, drag the variable into the graph.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41a8f2a2-6198-403d-b476-ba38f3edde77/2_9.png)
    
    1.  This creates a Getter node which allows you to access Events, Variables, Functions, etc. from the **Target Blueprint**.
    2.  Drag off the out pin to view the context menu.
    
    Here we are searching for the spark effect and spark audio components from our **Target Blueprint** as we want to access those components.
    
7.  The sample script below states that when the player enters the cube, deactivate the spark effect and spark audio.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ea78dea-a249-4e8a-9c56-0ee4016d23a6/2_10.png)

#### Direct Blueprint Communication for Spawned Actors

There may be an instance when you want to communicate between two Blueprints, however one (or more) of your Blueprints is not placed in the level yet (for example, a magic effect that is spawned when the player presses a button). In this case neither the player character nor the magic effect has spawned in the level, so setting a **Target Blueprint** and instance like above cannot be performed.

When using the **Spawn Actor from Class** node, you can drag off its **Return Value** and assign it as a variable.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9dd4665-e3c4-4cd1-93d5-1ea50efee444/spawn1.png)

In the example below, inside our **MyCharacter** Blueprint, we have stated that when **F** is pressed we want to spawn an instance of the **Blueprint\_Effect\_Smoke** Blueprint at the player's location and assign it to a variable called **Target Blueprint**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/249df462-9f3b-4c14-8284-9f84cb1cca50/spawn2.png)

We can then access the **Blueprint\_Effect\_Smoke** Blueprint (contained in the yellow boxes above) and get the Smoke Effect and Smoke Audio components from our **Target Blueprint** and **Deactivate** them when **F** is pressed a second time (which is what the **Flip/Flop** node does). Therefore we are accessing one Blueprint from inside another Blueprint through **Direct Blueprint Communication**.

Refer to the [Blueprint Communication Usage](/documentation/en-us/unreal-engine/blueprint-communication-usage-in-unreal-engine) documentation for more information.

### Blueprint Casting

For this example, we have a fire effect Blueprint in our level (which is an Actor) and we want it to communicate with the playable Character Blueprint the player is using. When the player enters the fire, we want to send a signal to the Character Blueprint that the player has entered the fire and that they should now take damage. By using the Return Value of an OverlapEvent, we can Cast To our Character Blueprint and access the Events, Functions, or Variables within it.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e594c4e1-716a-40ff-8bf6-3192ec8f2f3c/3_0a.png)

-   The fire effect above is the **Blueprint\_Effect\_Fire** asset (included with starter content).
-   A sphere component named **Trigger** was added to the Blueprint and was set to **OverlapOnlyPawn** for its collision.

Using Blueprint Casting, we would do the following:

1.  The Character Blueprint assigned to the **Default Pawn Class** (the playable character) is our Target Blueprint we want to access.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d39f669-4485-417b-ba6e-83c934529189/3_0b.png)
    
    You can view the **Default Pawn Class** from the **Edit** menu under **Project Settings** in the **Maps & Modes** section.
    
2.  Now that we know our target is the **MyCharacter** Blueprint, inside it we create a **Bool** variable that states if the player **Is on Fire**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0aa9b7df-12c9-499a-b0aa-bb393b234aff/3_0c.png)
    
    Above the **Event Tick** feeds a **Branch** where if **True**, we print **Apply Damage** to the screen (off True is where you would have your apply damage script).
    
3.  Inside the **Blueprint\_Effect\_Fire** Blueprint, we add two events for the **Trigger**: **OnComponentBeginOverlap** and **OnComponentEndOverlap**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65a8bce3-e8ce-43d3-adee-9d3d21cc8fd1/3_1.png)
4.  With the Events added, we drag off the **Other Actor** pin and enter **Cast To My** in the search field.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe5fe968-0fb7-4e45-83fc-b76afca4a15b/3_2.png)
    
    Here we check/assign the Actor (MyCharacter Blueprint) we want to trigger the event and **Cast To** it so that we may access it within the fire Blueprint.
    
5.  Select the **Cast To MyCharacter** option.
    
6.  With the node added, we can drag off the **As My Character C** pin and access the Events, Variables, Functions, etc. within it (in this case **Set Is on Fire**).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba194533-c6f3-4eff-874a-8b5d58d3d57c/3_3.png)
7.  Both Events in the **Blueprint\_Effect\_Fire** Blueprint would then look like this.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01ac80b8-517c-451a-b881-57d53b875d7b/3_4.png)
    
    When overlapping the fire, we are setting the **IsOnFire** variable in the **MyCharacter** Blueprint to **True** and setting it to **False** when not overlapping it. Inside the **MyCharacter** Blueprint, when **IsOnFire** is set to **True** via the fire Blueprint, we print to the screen **Apply Damage** (or if you have created a Health/Damage system, you could apply damage and reduce player's health here).
    

#### Other Types of Casting

There are some special functions that can be used to **Cast To** different classifications of **Blueprints**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aeac57a9-b724-400c-a843-c790a2fe9d08/othercasting.png)

In the example graph above, the following examples are given:

| Blueprint | Description |
| --- | --- |
| **Character** (1) | Here the **Get Player Character** node is used and we are casting to a Character Blueprint called **MyCharacter**. |
| **PlayerController** (2) | Here the **Get Player Controller** node is used and we are casting to a Player Controller Blueprint called **MyController**. |
| **Game Mode** (3) | Here the **Get Game Mode** node is used and we are casting to a Game Mode Blueprint called **MyGame**. |
| **Pawn** (4) | Here the **Get Controlled Pawn** and **Get Player Controller** nodes are used to cast to a Pawn Blueprint called **MyPawn**. |
| **HUD** (5) | Here the **Get HUD** and **Get Player Controller** nodes are used to cast to a HUD Blueprint called **MyHUD**. |

In each of the examples above, dragging off the **As My X** (where X is the type of Blueprint) node will allow you to access the Events, Variables, Functions, etc. from their respective Blueprints.

Also of note, the **Player Index** value in the **Get Player Character** and **Get Player Controller** nodes can be used to specify different players in a multiplayer scenario. For a single player scenario, leaving these as 0 is fine.

#### Target Blueprint Casting

There are also instances where you can use a variable to **Cast To** a specific type of Blueprint in order to access it.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bb47f43-ba2f-49b6-b7b8-8c94f70de19a/createcasting.png)

In the image above for number 1, a **Save Game Object** is created and assigned to a **SaveGameObject** variable. That variable is then used to **Cast To** a Save Game Blueprint called **MySaveGame** - which could be used to pass off or retrieve save game information such as a high score, best lap time, etc.

In the image above for number 2, a **Widget Blueprint** is created and assigned to a **UserWidget** variable. That variable is then used to **Cast To** a Widget Blueprint called **MyWidgetBlueprint** - which could be used to update or retrieve information from the Widget Blueprint (which could be a HUD or other UI element you want to access).

### Event Dispatchers

Below we have a bush **Actor Blueprint** in our level that we want to receive communication from the **Character Blueprint** when the player presses a button to set the bush on fire, then destroy the fire and the bush after a few seconds. We are wanting to communicate from the **Character Blueprint** to the **Level Blueprint** which can be done through using an **Event Dispatcher**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75948b12-180e-472c-a99e-aedeae585594/event1.png)

-   The bush above is the **SM\_Bush** asset (included with starter content).

Using an **Event Dispatcher** we would do the following:

1.  Inside the **MyCharacter** Blueprint, click the **Event Dispatcher** icon or the >> arrows if the icon is hidden and name the Event Dispatcher **StartFire**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55daf595-089f-46df-8335-f28f5d7a147e/event2.png)
2.  **Right-click** in the graph and add the **F** key event, then off the **Pressed** search for and add the **Call StartFire** Event Dispatcher.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f147b495-ce9c-4e17-9ce6-faa4a06d8d0f/event3.png)
3.  **Compile** and **Save** then close the **MyBlueprint**.
    
4.  Click on the bush in the level to select it, then open the **Level Blueprint**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8d10f8a-a800-47fd-8ef3-a0a7d9834c20/event4.png)
5.  **Right-click** in the graph and add the reference to the bush from the level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4bda507c-9746-4877-aaf3-708943854142/event5.png)
6.  **Right-click** and add an **Event Begin Play** node and a **Get Player Character** node, then off the **Get Player Character**, **Cast To MyCharacter**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69e0609e-5e0b-47fe-815b-1112af02a90b/event6.png)
7.  Off the **As My Character C**, add the **Assign Start Fire** Event Dispatcher (a new Binded Event will be created).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ff64b05-8f8f-46d2-a574-a0646b951fff/event7.png)
8.  Off the **StartFire\_Event**, add a **SpawnActorFromClass** node (class set to **Blueprint\_Effect\_Fire**) and for the **Transform**, get the **SM\_Bush** Transform.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eafe6901-b237-4d2e-9399-e5ad417d25f4/event8.png)
9.  Off the **Return Value** of the Spawn Actor node, add the **Assign On Destroyed** node.
    
10.  Off the **OnDestroyed\_Event**, add a **Destroy Actor** node with target being **SM\_Bush**.
    
11.  Off the **Bind Event to OnDestroyed**, add a **Delay** (3 seconds) then add a **Destroy Actor** with the target the **Return Value** from the Spawn Actor node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de30d652-526a-4654-b6b7-120bba87abfa/event9.png)
    
    The last few steps should result in the graph above.
    

If you compile and save then play in the editor, you should see that when you press the **F** key a fire effect is spawned inside the bush. After 3 seconds both the fire and bush should then be removed from the level.

This is of course a simple example and you would probably want more checking to occur (if the player is near the bush allow them to set it on fire) as well only allowing the player to start the fire once, but it illustrates how you can execute events inside the **Level Blueprint** by way of a **Character Blueprint** using an **Event Dispatcher**. The example above also shows how you can assign an **Event Dispatcher** to a Spawned Actor and execute Events when something occurs to that Actor (in this case, when it is destroyed).

Refer to the **[Event Dispatchers](/documentation/en-us/unreal-engine/event-dispatchers-in-unreal-engine)** documentation for more information.

### Blueprint Interfaces

Below we have four **Blueprints** in our level: a cube which acts as a trigger, a fire effect, a spark effect and a hanging light. We want the fire, light and sparks to each do something differently when the player enters the cube. We also want to increase the movement speed of the character each time they enter the cube.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/939bd761-39a5-4208-9f2a-357340920f44/interface1.png)

-   The cube above is a **Blueprint** created using the **Shape\_Cube** mesh and its collision has been set to **OverlapOnlyPawn** so it acts as a trigger.
-   The sparks above are the **Blueprint\_Effect\_Sparks** asset (included with starter content).
-   The fire above is the **Blueprint\_Effect\_Fire** asset (included with starter content).
-   The light above is the **Blueprint\_CeilingLight** asset (included with starter content).

Using a **Blueprint Interface** would allow us to communicate with the three different Blueprints as well as the player character Blueprint.

To communicate with each of them, we would do the following:

1.  In the **Content Browser**, in an empty space, **Right-click** and select **Blueprints** then **Blueprint Interface**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa958780-9a08-4867-83de-448b22b9f5d9/interface2.png)
2.  Name the Interface, **CubeInterface** (or some other name) then **Double-click** on it to open it up and click the **Add Function** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9fe6fe5-c689-40aa-bbd4-460ad8c5e576/interface3.png)
3.  Name the new function **MagicCube** or any name you want, then **Compile**, **Save**, and close the Interface.
    
4.  Open the Cube Blueprint, then **Right-click** on the **StaticMesh** and add a **OnComponentBeginOverlap** Event.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0005545-768d-4035-8542-d1179869ff83/interface4.png)
5.  Create a new **Actor** variable called **Targets** and click the box next to Variable Type to make it an **Array**, then check the **Editable** box.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db8a74b9-c08e-4473-b017-ec59d3994a60/interface5.png)
    
    This will store the Actors that are affected by the **Blueprint Interface**.
    
6.  **Right-click** in the graph and under **Interface Messages**, click the **MagicCube** (or whatever you called it) function.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e12bfb2-7b3e-43bc-ad16-28b87c6b522d/interface6.png)
7.  Set up your graph as seen below, **Compile** and **Save** then close the Blueprint.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59447da9-f285-4f3e-bd85-f56655ac39f2/interface7.png)
    
    Drag in the **Targets** variable then drag off it to get the **Add** node.
    
    Plug **Targets** into the **MagicCube** node and plug a **Get Player Character** node into the **Add** node.
    
8.  Select the cube in the level, then in the **Details** panel, click the + sign under targets and add the fire, light and sparks from the level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20c07484-5469-4e2d-af1c-f334ba9c8bc2/interface8.png)
9.  Open the **Blueprint\_Effect\_Fire** Blueprint, then click the **Blueprint Props** button from the toolbar.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/971941e4-1cdf-430b-9fdb-b6a4f27114c7/interface9.png)
10.  In the **Details** panel under **Interfaces**, click the **Add** button then select your Interface (**CubeInterface\_C** in our example).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3cdc26c5-62dd-4441-8e89-d7b8accd8f00/interface10.png)
11.  **Right-click** in the graph and under **Add Event**, select the **Event Magic Cube** Event.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bebf4aa5-c6da-4835-afd8-e3cadef003e2/interface11.png)
12.  Anything following the **Event Magic Cube** will now be executed when the player enters the cube.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c9b1ac3-6a42-4dac-af32-a4566c541955/interface12.png)
    
    Here we are increasing the size of the fire when the player enters the cube, then resetting it when they enter it a second time.
    
13.  Open the **Blueprint\_CeilingLight** Blueprint, click **Blueprint Props** then add the Interface from the **Details** panel as before.
    
14.  **Right-click** in the graph and add the **Event Magic Cube** Event so that anything following the Event is executed when the player enters the cube.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b8f0c90-03d8-4972-8200-efa26dd9bda0/interface15.png)
    
    Here we are turning the light off by setting its Brightness to 0, then turning it on by setting the Brightness to 1500.
    
15.  Repeat the process of adding **Blueprint Props** to the **Blueprint\_Effect\_Sparks** Blueprint, then add the **CubeInterface\_C**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa2bac97-c2e6-46f1-9738-1204c88e1486/interface13.png)
    
    Here we are moving the spark effect up when entering the cube, then down when entering the cube a second time.
    
16.  Repeat the process of adding **Blueprint Props** to the **MyCharacter** Blueprint, then add the **CubeInterface\_C**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82cab188-d4af-4783-8da2-2b824a92e5bf/interface14.png)
    
    Here we increase the character's movement speed each time they enter the cube by 100.
    

As you can see from the examples above, by using a **Blueprint Interface** you can communicate with several different types of **Blueprints** at once where each can perform a different function all stemming from the same singular source (in this case a trigger).

This example is good for having an Event execute functionality in multiple Blueprints, however it is not the only manner in which **Blueprint Interfaces** can be used. The next section discusses how Variables can be passed between Blueprints using **Blueprint Interfaces**.

#### Passing Variables through Blueprint Interfaces

Below we have the **Blueprint\_Effect\_Fire** Blueprint which will represent the player character's life force.

This Blueprint will check what the player's health is and once it is 0, will dissolve and disappear.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b759b01a-35e9-41d0-a967-70076777afae/interfaceexample2_1.png)

-   The fire above is the **Blueprint\_Effect\_Fire** asset (included with starter content).

Using a **Blueprint Interface** and passing two variables through (the player's health and whether the player is dead or not) we can tell the fire when to disappear.

Here is how we would set up passing through those variables:

1.  In the **Content Browser**, in an empty space, **Right-click** and select **Blueprints** then **Blueprint Interface**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48a13010-ac19-4e1b-a1b4-d39333203dad/interface2.png)
2.  Name the Interface, **BP\_Interface** (or some other name) then **Double-click** on it to open it up and click the **Add Function** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce8c7b06-92f8-470c-b1b1-d83271c71d4b/interface3.png)
3.  Name the new function **GetHealth**, then in the **Details** panel, add two **Outputs** by clicking the **New** button.
    
4.  Make one of the new outputs a **Bool** called **playerIsDead** and the other a **Float** called **playerHealth**, then **Compile** and **Save** and close the Interface.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4f26e4e-0810-40cd-a6dc-354aab6aa401/interfaceexample2_2.png)
5.  Open the **MyCharacter** Blueprint, then click the **Blueprint Props** button from the toolbar.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/986e0f18-a336-4b52-89c0-e60dbf7f643e/interface9.png)
6.  In the **Details** panel under **Interfaces**, click the **Add** button then select your Interface (**BP\_Interface\_C** in our example).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3eb155ff-95b6-40b4-97b9-26f04ee91074/interfaceexample2_3.png)
7.  Create a **Bool** variable called **OutOfHealth** and a **Float** variable called **PlayerHealthValue**, **Compile** then set the **PlayerHealthValue** to **100**.
    
8.  Under the **Interfaces** section of **MyBlueprint**, **Double-click** on the **GetHealth** function to open it up.
    
9.  In the graph, drag in the **OutOfHealth** and **PlayerHealthValues** and plug them in to the **ReturnNode** as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94369f42-816b-4caf-afc7-19d08281150f/interfaceexample2_5.png)
    
    This will pass the values that are stored in the **MyCharacter** Blueprint to the Interface.
    
10.  Return to the **EventGraph** of the **MyCharacter** Blueprint and re-create the setup below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f336ff1-7929-4271-9521-4d8f8e4ac5a9/interfaceexample2_6.png)
    
    Here we are saying when the player's health is greater than 0 and the player presses **F**, subtract 25 from the current health value and call an **Event Dispatcher** called **TakeDamage**. When health is less than or equal to 0, set a Bool variable called OutOfHealth to *true* and call the **Event Dispatcher** called **TakeDamage**. We use an **Event Dispatcher** here to signal another Blueprint that the player has taken damage, rather than the other Blueprint checking the player's health each tick using an Event Tick.
    
11.  Open the Blueprint you want to pass the variables to (**Blueprint\_Effect\_Fire**), and click the **Blueprint Props** button, then **Add** the interface via the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40cad1b3-8edb-4b84-8359-733c51bb90ab/interfaceexample2_3.png)
12.  In the **EventGraph**, bind an Event to the **TakeDamage** event from the **MyCharacter** Blueprint.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4ce901c-c070-41c0-836c-726bc7251f1c/interfaceexample2_7.png)
    
    Drag off the **Get Player Character** node and **Cast To MyCharacter**, then off the **As My Character C**, **Assign Take Damage** to create a Binded Event.
    
13.  Off the Binded Event **TakeDamage\_Event**, add the **GetHealth** Interface Message.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7324594d-e898-4f88-becc-ab84f4efa37b/interfaceexample2_8.png)
    
    Be sure to implement the **Interface Message** and not the **Call Function**.
    
14.  Re-create the setup below.
    
    *Click image for full view.*
    
    Here, the **GetHealth** Interface is connected to a series of **Branch** nodes where the first checks if the **PlayerIsDead** (defined in the **MyCharacter** Blueprint) and if so, text is printed to the screen and the fire effect/audio is deactivated.
    
    The second **Branch** node checks if the **PlayerHealth** value is 0 and if it is, text is printed to the screen that states "1 More Hit" before the character is "dead". This is by no means a perfect Health/Damage setup, but it illustrates how you can pass two variables through an Interface and how you could then use those variables in another Blueprint. The "PlayerHealth" value in this example could be passed to a HUD and updated to reflect current Health for example.
    

Refer to the **[Blueprint Interface](/documentation/en-us/unreal-engine/blueprint-interface-in-unreal-engine)** documentation for more information.
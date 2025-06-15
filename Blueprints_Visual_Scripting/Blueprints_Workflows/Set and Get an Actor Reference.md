# Set and Get an Actor Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/set-and-get-an-actor-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/set-and-get-an-actor-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:33

---

In object-oriented programming, there are two key types of variables:

-   **Primitives**, such as integers, text characters, floats, and booleans.
    
-   **Objects**, such as actors and actor components.
    

Each of these behave differently when you get and set their values.

When you create a primitive-type variable, it creates a new instance of that primitive and initializes its value to 0 (or its equivalent for that primitive) automatically. For instance, if you create an Integer-type variable called MyInt, that variable immediately exists with a value of 0, and you can start doing mathematical operations on it. Every new integer-type variable you create in the variables panel creates a brand new integer with its own unique value right out of the box, and **setting** its value changes the value of that integer.

When you create an object-type variable, it does NOT create a new instance of that object. Instead, that variable acts as a **reference** to an object. You can think of the variable as a placeholder that *could* point to any object that matches its definition, giving you a shortcut in your code so that you can quickly access it. When you set or assign a value for an object variable, it does not replace the previous object or change it. Instead, it changes which object the reference points at, while the previous object continues to exist until it's explicitly deleted. To instantiate a new object, you must *construct* one, and to access it, you must assign it to a reference.

This guide provides a walkthrough of all these ways of interacting with object references, using a teleporter as an example. After you complete the tutorials below, you will be able to:

-   Create object references and assign objects to them.
    
-   Use object references to access objects' functions and run code on them.
    
-   Assign object references in the Details panel.
    
-   Reassign object references.
    

## Required Setup

This tutorial uses a new project with the following settings:

-   Third-person template.
    
-   Blueprint-only.
    

## Create an Actor that References Another Actor

To demonstrate how object references work, you will create an actor that references two other actors:

-   A **Teleport Location**, which acts as the location to teleport an actor to.
    
-   A **Target Actor**, which acts as the actor being teleported.
    

To set up an actor with these references:

1.  Create a new **Blueprint Class** using **TriggerBox** as the parent class. Name it **BP\_TeleporterActor**.
    
2.  Open the Blueprint for BP\_TeleporterActor and click the **EventGraph** tab.
    
3.  Click the **+** button in the **Variables** panel to add a new variable. Name it **TargetActor** and set its **type** to **Actor**.
    
4.  Create another actor variable called **TeleportLocation**. This is the location that you will teleport your target actor to.
    
5.  Click the **eye icon** for **TeleportLocation** to ensure it is visible in the Details panel.
    

[![The variables panel in BP_TeleporterActor shows an actor-type variable called TargetActor and another actor-type variable called TeleportLocation. TeleportLocation is marked "public" with an open eye icon](https://dev.epicgames.com/community/api/documentation/image/0cc2d633-5fe9-480c-8a12-28a6ea87ef97?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0cc2d633-5fe9-480c-8a12-28a6ea87ef97?resizing_type=fit)

Each of these variables is a placeholder that can reference an actor in the world. Neither of them actually points at an actor yet, but you can use them to create logic for what you want the teleporter to do.

## Get an Actor Reference in Blueprint and Teleport It to Another Location

Now that you have your actor variables set up, create the logic for handling teleportation. To do this, you need to perform a Get operation to get a reference to your actors.

1.  In BP\_TeleporterActor, click and drag **TargetActor** into the Event Graph. In the drop-down menu that appears, click **Get TargetActor**. This creates a **Get** node.
    

[![The user clicks and drags TargetActor into the EventGraph, then chooses "Get TargetActor" to place a Get node.](https://dev.epicgames.com/community/api/documentation/image/cd035c7a-18ff-4747-b124-4861bb0ebc9e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cd035c7a-18ff-4747-b124-4861bb0ebc9e?resizing_type=fit)

You can access that actor's functions by clicking and dragging from the pin on the Get node.

1.  Click and drag from the Get Target Actor node, then, in the search box that appears, find **Set Actor Location** and click it to create a new Set Actor Location node. Check the **Teleport** box.
    
2.  Connect **Event ActorBeginOverlap** to the Set Actor Location node.
    
3.  Click and drag **TeleportLocation** into the Event Graph and create a **Get** node.
    
4.  Click and drag from **Get TeleportLocation** in the Event Graph, then create a new **Get Actor Location** node.
    
5.  Hook the Get Actor Location node up to the **New Location** pin of the Set Actor Location node.
    

If you try to run this code, it will fail and throw an error, as the TargetActor and TeleportLocation references are both currently empty. In other words, they don't point at anything yet -- they're just placeholders. The next sections will show you how to set these values.

## Set an Actor Reference in Blueprint

Next, use a Set operation to set the Target Actor to be any actor that enters the trigger box.

1.  Click and drag **TargetActor** from the variables panel into the Event Graph. This time, create a **Set TargetActor** node.
    
2.  Connect the Set TargetActor node in-between **Event ActorBeginOverlap** and **Set Actor Location**.
    
3.  Click and drag the **Other Actor** variable from ActorBeginOverlap to the input pin on **Set TargetActor**.
    

[![The user creates a Set Target Actor node and connects it to the Actor Begin Overlap event.](https://dev.epicgames.com/community/api/documentation/image/3d7b47d1-2607-4050-a820-d4818c056bb2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3d7b47d1-2607-4050-a820-d4818c056bb2?resizing_type=fit)

This sets TargetActor to point at any actor that moves into the trigger box. You can think of this as a way to keep a record of the last thing that entered the teleporter. The final graph should appear as follows:

[![The final graph for this Blueprint.](https://dev.epicgames.com/community/api/documentation/image/7d745882-55ef-45a2-8a94-ab333c75cd04?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7d745882-55ef-45a2-8a94-ab333c75cd04?resizing_type=fit)

## Set an Actor Reference in the Details Panel

Finally, set the location that you want to teleport your actor to.

1.  Click and drag an instance of **BP\_TeleporterActor** into the world. Rename it **Teleporter1**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/2573008c-5faa-43d0-9eb5-f54e8127c67f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2573008c-5faa-43d0-9eb5-f54e8127c67f?resizing_type=fit)
    
2.  Click and drag an instance of an empty **actor** into the world. Rename it **TeleportLocation1**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/c20d7710-50d9-4bd8-93bb-9414a39b2312?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c20d7710-50d9-4bd8-93bb-9414a39b2312?resizing_type=fit)
    
3.  Click Teleporter1. In the **Details Panel**, click the drop-down for **Teleport Location**, then set it to **TeleportLocation1**. You can also use the **eye dropper** to select it from the world itself.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/aa2626c4-b230-4f57-84fe-043b7ae6d57f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/aa2626c4-b230-4f57-84fe-043b7ae6d57f?resizing_type=fit)
    
4.  Move Teleporter1 so that the trigger box is fully above ground. In the Details Panel, find the **Actor Hidden in Game** setting, then disable it. This will make it possible for you to see the teleporter when you run your game, then walk directly into the trigger box for your teleporter.
    

If you create multiple teleporters, each one could have a different Teleport Location set, as these references are tracked for each individual instance of the teleporter.

## Test Your Teleporter

Now that you have assigned actors to the object references in your teleporter, it is ready to function. Hit the **Play** button to run your game in-editor, then run directly into the trigger box for Teleporter1.

[![The user steps into the teleporter and it transports their character to TeleportLocation1](https://dev.epicgames.com/community/api/documentation/image/ba382d23-9444-47f0-aff6-78327e04d4a5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ba382d23-9444-47f0-aff6-78327e04d4a5?resizing_type=fit)

Here's what's happening:

1.  Teleporter1 gets your character in the BeginOverlap event, then assigns it to TargetActor.
    
2.  It then gets a reference to TargetActor and sets its location to the location of TeleportLocation1. The reference to TeleportLocation1 is assigned in the Details Panel for Teleporter1, so there is no need to set the reference in code.
    
3.  If a different actor steps into Teleporter1's trigger box, it will set TargetActor to be that actor instead and teleport it to TeleportLocation1 as well.
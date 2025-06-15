# Placing Nodes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/placing-nodes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/placing-nodes-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:23

---

On this page, you will learn how you can place nodes on your graphs in Blueprints.

## Drag-and-Drop

The first method uses a **Drag-and-drop** procedure where you add nodes to your graph by dragging and dropping nodes from the **MyBlueprint** window onto your graph. For example, below we have several variables where we drag the **PlayerHealth** variable into and drop it in our graph so that we can use it in our script.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ffc3390-fbe8-4ee1-aac2-2a5c1ff67af1/addingnodes1.png)

By **Left-clicking** on and dragging a variable into the Graph window, we are presented with two options, **Get** or **Set**. Selecting Get will create a **Getter** node which will get the variable or value of the variable while selecting Set will create a **Setter** node which will allow you to set the value of the variable. Depending upon the type of node, there may be instances where Get is the only option available.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa72b031-e533-415d-af4e-0abeb5210e15/addingnodes2.png)

In the image above, the top node is a Getter while the bottom node is a Setter. The Getter, for example, could be used as a condition for elements in your games (such as getting the Player Health and checking if that value is above a specified range and if not, killing the player). The Setter on the other hand, using the previous example, could be used to increase the Player's Health as you are telling the Player Health variable what its value should be by setting it.

You can also drag in any **Functions** or **Macros** you have created into your graph in the same manner.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/398a3a84-242f-4727-8736-851c8f72df19/addingnodes7.png)

-   See [Functions](/documentation/en-us/unreal-engine/functions-in-unreal-engine) or [Macros](/documentation/en-us/unreal-engine/macros-in-unreal-engine) for more information.

There are some special context actions that become available when dragging in an **Event Dispatcher** as illustrated below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29ba4f45-0392-4a02-abf4-ef390e15249e/addingnodes6.png)

You can select the action you wish to perform from the context menu that appears when dragging in an Event Dispatcher.

-   See [Event Dispatchers](/documentation/en-us/unreal-engine/event-dispatchers-in-unreal-engine) for more information.

## Context Menu Search

Most of the time when placing nodes, you will use the **Context Menu** which can be accessed by **Right-clicking** inside a Blueprint graph.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4debfce5-be72-4330-9fcf-29b927cf6aee/rightclick1.png)

From the menu above, you can expand any category (or sub category) and select the node you wish to add to the graph.

There is also an option in the upper right corner of the window called **Context Sensitive** that is enabled by default but can be disabled which automatically filters the options presented in the menu based on the current context.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f10fe35d-c71d-4680-b2d4-1ecb95e07567/rightclick2.png)

As you can see below, when **Right-clicking** and searching for **Animation** with **Context Sensitive** on, you are presented with a filtered list.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/678ef694-6802-4c40-ae65-0ce8d21b2515/rightclick3.png)

However, if you un-check **Context Sensitive** and search for **Animation**, you are presented with everything related to animation.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59c711e6-bc3e-4552-92ba-28b2e96b98fd/rightclick4.png)

While **Right-clicking** in the graph brings up the Context Menu, you can drag off an existing node to access the Context Menu as well.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f632da1-65a9-4382-bdf3-65f5c9b55656/rightclick5.png)

Above, we have a **Character Movement** Component Reference and by dragging off its out pin, we can add nodes that contextually make sense and are relevant to the node we are dragging off of as seen in the example below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83ca5463-8264-41b5-b10c-6ded8e21aee6/rightclick6.png)

Above we can set the character's Max Walk Speed by searching for **Set Max Walk** then choosing **Set Max Walk Speed** from the menu.

## Keyboard Shortcuts

You can also use **Keyboard Shortcuts** to place (and work with) nodes, increasing your productivity.

-   See [Blueprint Editor Cheat Sheet](/documentation/en-us/unreal-engine/blueprint-editor-cheat-sheet-in-unreal-engine) for more information.
# Binding and Unbinding Events

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/binding-and-unbinding-events-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/binding-and-unbinding-events-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:59

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e26bd094-b429-4c21-bdbf-00e617f2dfa4/bind_node.png)

Calling the Event Dispatcher will have no effect if there are no events bound to it. Consider that each Event Dispatcher has a list of events associated with it. The way to add an event to this list is by using a **Bind Event** node, and the way to remove an event from this list is by using an **Unbind Event** node. It is also possible to unbind all of the events currently bound to an Event Dispatcher with an **Unbind All Events** node.

Each event can be bound only once, even if the **Bind Event** node is executed multiple times. Also, events in the Blueprint Class and the Level Blueprint are both added to the same event list, so an **Unbind All Events** node will unbind events in both the Blueprint Class and the Level Blueprint.

-   An **Unbind All Events** node executed in the Blueprint Class will unbind events in both the Blueprint Class and the Level Blueprint for all instances of the class.
-   An **Unbind All Events** node executed in the Level Blueprint will unbind events in both the Blueprint Class and the Level Blueprint, but just for the **Target** supplied.

## Creating Bind, Unbind, and Unbind All Nodes

The processes for creating **Bind Event**, **Unbind Event**, and **Unbind All Events** nodes are very similar. The steps below explain how to create a **Bind Event** node, but **Unbind Event** and **Unbind All Events** nodes can be created by choosing the respective menu items at the appropriate steps.

### In Blueprint Classes

1.  Drag off of the Event Dispatcher's name in the **My Blueprint** tab, and drop into the graph you are working in.
    
2.  Select **Bind** in the menu that appears.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96bda394-bc8b-4735-95b4-a38e0232b282/dispatcher_bind_menu.png)

**Alternatively:**

1.  **Right-click** in the graph.
    
2.  Search for **Bind Event to \[EventDispatcherName\]** and select the entry from the context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/941665a3-175e-4237-86bc-e93aa121a968/event_dispatcher_context_search.png)

### In Level Blueprints

1.  [Add a reference](/documentation/en-us/unreal-engine/level-blueprint-in-unreal-engine#referencingactors) to the Actor in your level you would like to call the Event Dispatcher for.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/121b1446-4b71-4c74-8e29-9850768b084b/target_step1.png)
2.  Drag off of the output pin of the reference node and release to show the context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e21a36d-f91a-4bbb-af61-54aa905ed87c/empty_context_menu.png)
3.  Navigate to **Event Dispatcher > Bind Event to \[EventDispatcherName\]** in the context menu. Searching for "Bind \[EventName\]" should quickly bring up the correct entry.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccaadd42-b711-4c84-b4e5-1ebd5e43ac2c/bind_node_level.png)
    
    The **Call** node will appear, with the Actor reference already wired to the **Target** pin.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86ef5de8-1afe-4f10-b3f4-a07053052070/bind_dispatcher_wired_level.png)
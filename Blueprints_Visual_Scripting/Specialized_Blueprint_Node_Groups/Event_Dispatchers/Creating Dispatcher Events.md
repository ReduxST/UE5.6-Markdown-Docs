# Creating Dispatcher Events

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-dispatcher-events-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-dispatcher-events-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:26

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a529244d-0c1e-4915-8893-4eedf393fcc7/dispatcher_event.png)

Using the **Event** option on the Event Dispatcher's menu creates a custom event with the correct signature so that it can be bound to the Event Dispatcher. While the event node appears similar to a [Custom Event node](/documentation/en-us/unreal-engine/custom-events-in-unreal-engine), without being connected to a **Bind** node, this event will never be triggered when the **Call \[EventDispatcherName\]** node is executed.

## Creating Event Dispatcher Event Nodes

Event Dispatcher **Event** nodes are connected to **Bind Event** nodes by wiring the red square pin on their upper right corner to the red square **Event** input pin on the **Bind Event** node. So, if you already have a **Bind Event** node for a particular Event Dispatcher and would like to create the event node for it:

1.  Drag off of the **Event** input pin and release to show the context menu.
    
2.  Select **Add Custom Event for Dispatcher** in the context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f3e5c42-9298-4fc9-8794-bbcf7a29634b/add_custom_event_for_dispatcher.png)
3.  An event node will be created and automatically wired correctly to the **Bind Event** node. Enter a name for your event.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a4fcd5f-0e8d-4007-a9df-6bdef366528b/delegate_pin_enter_name.png)

Selecting **Assign** from either the Event Dispatcher menu or the context menu will also create a **Bind Event** node and a corresponding **Event** node, already wired together.

### In Blueprint Classes

1.  Drag off of the Event Dispatcher's name in the **My Blueprint** tab, and drop into the graph you are working in.
    
2.  Select **Event** in the menu that appears.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fbd21f5-cb2e-48f1-9ee2-c609741f6142/dispatcher_event_menu.png)
3.  Enter a name for your event.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bec9f0a-44c3-4580-8c53-b26b599eb5b7/dispatcher_event_enter_name.png)

### In Level Blueprints

A special type of Event Dispatcher event can be set up in the Level Blueprint, and it is the one case where an event is automatically bound to the Event Dispatcher. These events are created with the same steps as the default events such as **OnClicked** or **OnOverlap** events. The [Level Blueprint documentation](/documentation/en-us/unreal-engine/level-blueprint-in-unreal-engine#addingevents) provides a walkthrough for this process.

These particular events are unique, and are automatically bound at the start of gameplay. As a result, an **Unbind All** node executed at any point will unbind these events as well. It is possible to rebind them, however, by wiring their delegate pins to **Bind Event** nodes that are executed at other points in gameplay.
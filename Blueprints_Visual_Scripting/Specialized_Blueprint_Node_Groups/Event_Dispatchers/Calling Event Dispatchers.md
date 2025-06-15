# Calling Event Dispatchers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/calling-event-dispatchers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/calling-event-dispatchers-in-unreal-engine)  
**Processed:** 2025-06-14 16:11:48

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e622ac7-36e9-42c9-97b3-d85493c9c53b/event_dispatcher_call_node.png)

Calling an Event Dispatcher with a **Call** node causes all of the events bound to the Event Dispatcher to fire. You can have more than one **Call** node for each Event Dispatcher, and you can also call the Event Dispatcher in both Blueprint Classes and Level Blueprints.

## Calling in Blueprint Classes

1.  Drag off of the Event Dispatcher's name in the **My Blueprint** tab, and drop into the graph you are working in.
    
2.  Select **Call** in the menu that appears.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/900da6dc-7cf4-4486-ad99-b2689350cd90/dispatcher_call_menu.png)

**Alternatively:**

1.  **Right-click** in the graph.
    
2.  Expand **Event Dispatcher** in the context menu that appears.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ac35c2e-a6d2-4489-82a8-fce9363957cd/event_dispatcher_context.png)
3.  Select **Call \[EventDispatcherName\]** under **Event Dispatcher**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42ddd18c-238f-4e28-9ae3-ef9d2c774abf/event_dispatcher_context_name.png)

## Calling in Level Blueprints

1.  [Add a reference](/documentation/en-us/unreal-engine/level-blueprint-in-unreal-engine#referencingactors) to the Actor in your level you would like to call the Event Dispatcher for.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/650738cb-fef5-4cb1-b728-70006287d461/target_step1.png)
2.  Drag off of the output pin of the reference node and release to show the context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24e85d48-137e-4ee0-b2d1-7e5909792a81/empty_context_menu.png)
3.  Navigate to **Event Dispatcher > Call \[EventDispatcherName\]** in the context menu. Searching for "Event Call" should quickly bring up the correct entry.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e915a778-b13b-43d2-ba7b-966dcff3776e/call_node_level.png)
    
    The **Call** node will appear, with the Actor reference already wired to the **Target** pin.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b547732-9883-460e-a41b-919cada5c0f0/call_dispatcher_wired_level.png)
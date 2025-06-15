# Using Cluster Events with nDisplay

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-cluster-events-with-ndisplay-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-cluster-events-with-ndisplay-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:29

---

Cluster Events are a way for you to make all the nodes in your nDisplay cluster respond to events simultaneously.

1.  You generate a Cluster Event either from a node in the cluster or by sending it to the primary node from an external application. See [Emitting Cluster Events from Blueprints](/documentation/en-us/unreal-engine/using-cluster-events-with-ndisplay-in-unreal-engine#emittingclustereventsfromblueprints) or [Emitting Cluster Events from External Applications](/documentation/en-us/unreal-engine/using-cluster-events-with-ndisplay-in-unreal-engine#emittingclustereventsfromexternalapplications).
2.  When the primary node of your cluster receives a Cluster Event, it propagates that event to each node in the cluster so that the event happens on each node in exactly the same frame.
3.  Within the Blueprint or C++ logic of your Unreal Engine application, you set up listeners to detect these Cluster Events and respond to them with whatever gameplay logic you need for your Project. See [Responding to Cluster Events in Blueprints](/documentation/en-us/unreal-engine/using-cluster-events-with-ndisplay-in-unreal-engine#respondingtoclustereventsinblueprints).

## Cluster Event Format

There are two types of formats supported by nDisplay for Cluster Events: JSON and binary. The JSON format is human-readable; it uses ASCII, with some characters forbidden by the JSON standard, and requires a specific schema for structuring data. With the binary format, you can use any kind of binary data, and serialization and deserialization is up to you. Using the binary format for Cluster Events has better performance than the JSON format for data throughput and latency.

### JSON Cluster Event Structure

Each JSON nDisplay Cluster Event can contain several properties:

| Setting | Type |
| --- | --- |
| **Name** | string |
| **Type** | string |
| **Category** | string |
| **SystemEvent** | Boolean to specify whether this is a system or user event. You do not need to set this flag yourself. |
| **ShouldDiscardOnRepeat** | Boolean to specify whether events with the same **Name**, **Type**, and **Category** that have already been received within the current frame should be discarded. |
| **Parameters** | An optional map of key-value pairs, where the keys and values are both strings. |

It's up to you to decide in your Project what data you want to send in each of these properties, and how you want your listeners to interpret that data.

When you interact with a JSON Cluster Event in Blueprint, you'll use the **Make DisplayClusterClusterEventJson** and **Break DisplayClusterClusterEventJson** nodes to construct and deconstruct JSON Cluster Events. For example:

![A JSON Cluster Event in Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33bd05f3-a5a9-44ec-bdfd-36110ae4d479/01-make-cluster-event-json_ue5.png)

In C++, or when emitting JSON Cluster Events from your own applications, you'll use the [`FDisplayClusterClusterEventJson`](/documentation/en-us/unreal-engine/API/Plugins/DisplayCluster/Cluster/FDisplayClusterClusterEventJson) struct to express the same structure.

### Binary Cluster Event Structure

Each Binary Cluster Event can contain several properties.

| Setting | Type |
| --- | --- |
| **Event Id** | 32-bit integer |
| **System Event** | Boolean to specify whether this is a system or user event. You do not need to set this flag yourself. |
| **ShouldDiscardOnRepeat** | Boolean to specify whether events with the same **Event Id** that have already been received within the current frame should be discarded. |
| **Event Data** | Array of bytes |

It's up to you to decide in your Project what data you want to send in each of these properties, and how you want your listeners to interpret that data.

When you interact with a Binary Cluster Event in Blueprint, you'll use the **Make DisplayClusterClusterEventBinary** and **Break DisplayClusterClusterEventBinary** nodes to construct and deconstruct Binary Cluster Events. For example:

![A Binary Cluster Event in Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8aca7da8-adbd-4c4d-92d1-9fb93f1e66f0/02-make-cluster-event-binary_ue5.png "A Binary Cluster Event in Blueprint")

In C++, or when emitting Binary Cluster Events from your own applications, you'll use the [`FDisplayClusterClusterEventBinary`](/documentation/en-us/unreal-engine/API/Plugins/DisplayCluster/Cluster/FDisplayClusterClusterEventBinar-) struct to express the same structure.

## Emitting Cluster Events from Blueprints

The following example shows how to emit JSON Cluster Events from a Blueprint class. You can use these same steps, with some modification, for emitting Binary Cluster Events from a Blueprint class.

To emit a JSON Cluster Event from a Blueprint class in your Project:

1.  Get the **DisplayCluster Module API** (see [Blueprint API](/documentation/en-us/unreal-engine/ndisplay-overview-for-unreal-engine#blueprintapi)), and call its **Cluster >** **Emit JSON cluster event** function. This node fires the Cluster Event out to the primary node, labeled the master node in the API, which propagates it back to all the nodes in the cluster.
    
    Click image to expand.
    
2.  By default, every instance of your Unreal Engine application that evaluates this Blueprint node in its gameplay logic will fire this Cluster Event. If this Blueprint graph gets evaluated on many different nodes in your cluster, this can cause multiple copies of the event to happen. To avoid triggering multiple copies of the Cluster Event, you can set the **Primary Only** Boolean value on the **Emit JSON cluster event** node. If you check this box, only the primary node will emit this Cluster Event. If any other non-primary cluster node evaluates the same Blueprint graph, those nodes will not emit the event.
    
    ![Primary Only](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/accf0cab-20e3-4c79-8b29-b2fd52f75702/04-emit-json-event-primary_ue5.png "Primary Only")
3.  Drag left from the **Event** port on the **Emit JSON cluster event** node, and choose **Make DisplayClusterClusterEventJson**.
    
    Click image to expand.
    
4.  Use the settings in the **Make DisplayClusterClusterEventJson** node to set set up your Cluster Event with string values for its **Name**, **Type**, and **Category**. If you need to pass arbitrary key-value data along with your cluster event, you can also pass a map of those keys and values to the **Parameters** input.
    
    Click image to expand.
    
5.  **Compile** and **Save** your Blueprint.
    

The next time you repackage your Project and relaunch your nDisplay cluster, this Blueprint code will fire the JSON Cluster Event you've set up. To respond to this event elsewhere in your Blueprint code, see [Responding to Cluster Events in Blueprints](/documentation/en-us/unreal-engine/using-cluster-events-with-ndisplay-in-unreal-engine#respondingtoclustereventsinblueprints).

## Emitting Cluster Events from External Applications

When you start up your nDisplay cluster, the primary node begins listening for incoming Cluster Events on a specific local port. You can emit new Cluster Events to your nDisplay system from another application running on any other computer in your network by connecting to that port and sending messages. Both JSON and Binary port listeners use TCP, so you can keep the connection open until the cluster session has ended.

For each Cluster Node you want to emit, your message must follow this convention:

-   The first four bytes must give the total length of the rest of the message.
-   The rest of the message should be the content of your Cluster Event, expressed as either a JSON object or binary data.
    -   For JSON event messages:
        -   JSON object with the mandatory fields **Name**, **Type**, **Category**, **SystemEvent**, and **ShouldDiscardOnRepeat**, and the optional field **Parameters**.
    -   For binary event messages:
        -   4 bytes for the event ID.
        -   1 byte for the System Event boolean.
        -   1 byte for the Should Discard on Repeat boolean.
        -   N bytes for the binary data, where there is no limit for N.

For example, to emit a JSON Cluster Event with the name "quit" and the type "command", you would need to:

1.  Construct a JSON string that contains the values for your Cluster Node. In this case:
    
    ```
            `{"Name":"quit","Type":"command","Category":"","Parameters":{}}`
    		
    Copy full snippet
    ```
    {"Name":"quit","Type":"command","Category":"","Parameters":{}}
    
    The **Name**, **Type**, and **Category** fields are mandatory, but you may omit the Parameters field. Although some of the fields are mandatory, you can assign empty values to any of the fields because the events with empty fields will be grouped together. It's recommended to provide names and IDs for readability.
    
2.  Get the length of the JSON string — in this case, 62 characters — and send that length to the nDisplay primary node in binary format with 4 bytes. In this example, it would be `0x00111110`.
3.  Send the JSON string itself to the nDisplay primary node.

By default, the primary node listens for Cluster Events on port 41003 and Binary Cluster Events on port 41004. You can change this default in your nDisplay configuration file. See [Changing nDisplay Communication Ports](/documentation/en-us/unreal-engine/changing-ndisplay-communication-ports-in-unreal-engine).

To respond to these Cluster Events in your Project's Blueprint code, see [Responding to Cluster Events in Blueprints](/documentation/en-us/unreal-engine/using-cluster-events-with-ndisplay-in-unreal-engine#respondingtoclustereventsinblueprints).

## Responding to Cluster Events in Blueprints

Once you've set up one of the methods described above to emit Cluster Events into your nDisplay network, you'll want to set up your Blueprint (or C++) gameplay logic to detect those Cluster Events and respond to them in some way. To do this, you need to create and register a listener: a class that implements the **DisplayClusterClusterEventListener** interface. You register the listener by calling the **Add Cluster Event Listener** function from the nDisplay API, then use the **Event On Cluster Event** node to detect Cluster Events and respond to them.

For example, to create a new Blueprint class and register it as a listener:

1.  In the **Content Browser**, right-click and choose **Create Basic Asset > Blueprint Class**.
    
    Click image to expand.
    
2.  Choose **Actor** as the parent class. ![Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5510e471-1bbf-4e3a-a258-7e24237d904f/08-actor-parent-class_ue5.png "Actor")
    
3.  Type a name for your new listener class in the **Content Browser**.
    
    ![Rename the class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba7b18ff-07d2-47d2-a48e-aa4716f69b63/09-name-blueprint-class_ue5.png "Rename the class")
4.  Drag your class into the Level Viewport and drop it into your Level.
    
    Click image to expand.
    
5.  Double-click your new Blueprint class to edit it.
    
6.  In the Toolbar, click **Class Settings**. ![Class Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d366773-5bed-49c4-ab33-19db4fe68163/11-class-settings_ue5.png "Class Settings")
    
7.  In the **Details** panel, find the **Interfaces > Implemented Interfaces** setting and click **Add**.
    
    ![Add interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02f034f9-b902-4309-828b-87ccc046ac74/12-add-interfaces_ue5.png "Add interface")
8.  Find and select the **DisplayClusterClusterEventListener** interface in the list. ![DisplayClusterClusterEventListener](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6f19c67-a47f-4131-be93-b79ecaf0727d/13-display-cluster-event-listener_ue5.png "DisplayClusterClusterEventListener")
    
9.  Click **Compile** in the Toolbar to compile your class.
    
10.  On the **Event Graph** tab, set up the following graph to register your listener:
    
    Click image to expand.
    
    To set this up:
    
    1.  Drag right from the output of the **Begin Play** Event node and choose **N Display > DisplayCluster Module API**.
    2.  Drag right from the **Out API** port of that node and choose **Display Cluster > Cluster > Add cluster event listener**.
    3.  Finally, drag left from the **Listener** port of the **Add cluster event listener** node, and choose **Variables > Get a reference to self**.
11.  It's a good idea to also destroy each listener you create when you know you won't need it anymore. For example, you can do it when your Blueprint Actor is destroyed:
    
    Click image to expand.
    
    To set this up:
    
    1.  Right-click in the Event Graph and choose the **Add Event > Event Destroyed** node.
    2.  Drag right from the output of the **Event Destroyed** node and choose **N Display > DisplayCluster Module API**.
    3.  Drag right from the **Out API** port of that node and choose **Display Cluster > Cluster > Remove cluster event listener (Interface Call)**.
    4.  Finally, drag left from the **Listener** port of the **Remove cluster event listener** node, and choose **Variables > Get a reference to self**.
12.  In another area of the **Event Graph**, add the **Add Event > N Display > Event On Cluster Event Json** node. Every time a JSON Cluster Event happens in your nDisplay cluster, this event will trigger. You will probably want to read the settings and parameters assigned to this event, so that you can use them to determine what action your Blueprint needs to take. To do this, drag right from the **Event** port of the Event **On Cluster Event Json** node, and choose **Break DisplayClusterClusterEventJson**. For example, this graph simply prints out the Name value of each JSON Cluster Event to the screen:
    
    Click image to expand.
    
13.  **Compile** and **Save** your Blueprint class.
    

The next time any JSON Cluster Event is emitted in the cluster, from any source, the name of that JSON Cluster Event gets printed to the screen.
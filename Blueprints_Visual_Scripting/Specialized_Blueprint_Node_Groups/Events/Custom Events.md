# Custom Events

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/custom-events-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/custom-events-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:05

---

Just like **Events**, **Custom Events** have an output pin for execution and optional output data pins. However, they are created by the user, and can be called multiple times throughout a graph. They define an entry point for execution of an individual network, but are not executed based on being called from code. Instead, they rely on some other part of the **EventGraph** to explicitly execute them using a **Custom Event** call or via the `CE` or `KE` console commands.

## Custom Events

Custom Events provide you with a way to create your own events that can be called at any point in your Blueprint's sequence. In cases where you are connecting multiple output execution wires to the input execution pin of one particular node, Custom Events can simplify the wire network of your graph. Custom Events can even be set up in one graph of a Blueprint and called in another graph.

They have a fairly straightforward workflow:

-   Create and name the Custom Event.
-   Establish any input parameters the event should have, along with any default values.
-   Create a special function node that calls the custom event.
-   Feed in any input parameters required.

### Creating Custom Events

1.  Create a Custom Event node by right-clicking and choosing **Add Custom Event...** from the context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9e8b398-da6e-4b58-87ac-b5c5d8c41ac2/add_custom_event.png)
2.  Give your new event a name.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2631cb2d-1305-4088-82c7-ae63a06eb9fa/name_custom_event.png)
3.  In the **Details** pane for your new event, you can set whether or not the event should be replicated on all clients when called on the server and add input parameters.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d9e5651-f69d-49a5-83c6-9b07a6c4b371/new_details_custom_event.png)

To add input parameters:

1.  Click on the **New** button in the **Inputs** section of the **Details** pane.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6f27614-ed4c-450e-bbc3-66d277d26514/new_input_custom_event.png)
2.  Name the new input and set its type using the dropdown menu. In this example, there is a String input parameter named **MyStringParam**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78da784c-0386-40db-8976-7ac3297a7998/named_new_variable.png)
3.  You can also set a default value by expanding the entry for the parameter.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3adb3977-b1e3-4ce5-b182-52fb5f9a30a5/set_default_parameter.png)

To change the location of the pin for this parameter on the edge of the node, use the up and down arrows in the expanded **Details** pane entry.

Now, just like any other Event or execution node, you can attach other nodes to the output execution pin of your Custom Event, and execution of that network will begin when your Custom Event is triggered. This Custom Event example prints a String to the screen.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0eeeebb6-f091-4e06-ae83-0612b9e311ae/small_custom_event.png)

### Calling Custom Events

Your Custom Event and its associated network have been created, but unlike regular Events, there are no preset conditions for the Custom Event to fire. To call your Custom Event, **Right-click** and choose **Call Function > \[Custom Event Name\]** from the context menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c87fc432-3a1b-458a-9e5b-0c94f552c531/call_ce_context_menu.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/022fb718-d043-4efc-a7c7-8e9e6c9b00f7/call_custom_event_node.png)

Any input parameters that were set up on the Custom Event will appear as input data pins in the new node so that they can be passed into the Custom Event. Connect any input data pins with data wires to variables or other data pins as needed.

Unlike regular Events, which can only be called once per graph per Event type, you can call a Custom Event multiple times throughout a graph. In this way, Custom Events allow branching of multiple execution outputs to a single execution input without needing to directly connect wires.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7644d307-aec7-48ca-a912-ca1921de0e2e/connected_custom_event.png)

In this example, if the **IsSuccess** boolean variable is false, an error message will be printed. This graph has the same function as wiring the **Print String** node in sequence after the **Branch** node, but with the added functionality that other sections of the graph can utilize the **Print String** node, and the two network sections do not have to be located near each other in the graph.

### Troubleshooting Custom Events

If you get a **Warning!** bar on your Custom Event node with an **"Unable to find function with name \[CustomEvent\]"** message, **Compile** your Blueprint.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed4cde2f-d753-4610-b852-c93f36e31fe5/custom_event_warning.png)

If you change the number of input parameters on your Custom Event, all nodes that call the Custom Event will have an error when you compile your Blueprint.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38f0983c-d625-4f64-8415-aec5394ce917/parameter_change_error.png)

You must refresh all the nodes that call your Custom Event. To refresh an individual node or a selected group of nodes, right-click on the node(s) and select **Refresh Nodes**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e87f0ceb-146b-42dd-9422-b325acd2a2f9/refresh_nodes.png)

To refresh all nodes in your graph, in the **File** menu, select **Refresh All Nodes**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b5a1833-3311-406d-8338-8da985e6ce05/refresh_all_nodes.png)
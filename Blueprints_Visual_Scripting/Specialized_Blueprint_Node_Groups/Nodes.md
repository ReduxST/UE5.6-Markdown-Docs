# Nodes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/nodes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/nodes-in-unreal-engine)  
**Processed:** 2025-06-14 16:39:09

---

**Nodes** are objects such as events, function calls, flow control operations, variables, and so on that can be used in graphs to define the functionality of the particular graph and Blueprint that contains it.

## Working with Nodes

Each type of node performs a unique function; however, the way in which nodes are created and used is common to all nodes. This helps to make for an intuitive experience when creating node graphs.

### Placing Nodes

New nodes are added to a graph by selecting the type of node from the **Context menu**. The node types listed in the context menu depend on the manner in which the list is accessed and what is currently selected.

-   **Right-clicking** on an empty space in the **Graph Editor** tab brings up a list of all nodes that can be added to the graph. If an Actor is selected, events supported by that type of Actor are also listed.
    
    ![Blueprint Context Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e763751-ed1f-4082-84b2-bb1272ab950b/k2_context.png)
-   Dragging a connection from a pin on a node and releasing in empty space brings up a list of nodes compatible with the type of pin the connection originated from.
    
    ![Blueprint New Connection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94666e30-61bf-4ab6-8787-2601f47f5b39/k2_connection_new.png)![Blueprint Context Menu - Pin Specific](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f97975a-7e1c-429f-84f4-63b28c1087e5/k2_context_compat.png)
    

### Selecting Nodes

Nodes are selected by clicking on the node in the **Graph Editor** tab.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4ed180e-4c13-4fe4-88f1-b60751b73759/selectnode.jpg)

A node can be added to, or removed from, the current selection by holding **Ctrl** and clicking on the node.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abc8c637-65f6-4b75-bd72-d08663aa678e/varmessage.jpg)

Multiple nodes can be selected at once by clicking and dragging to create a marquee selection. Holding **Ctrl** + clicking and dragging creates a marquee selection that toggles selection. Holding **Shift** + clicking and dragging creates a marquee selection that adds to the current selection.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62fd2f8f-fda2-426c-ae92-edf983ef7ddd/dotboxspawnemitter.jpg)

To deselect all nodes, simply click in an empty space of the **Graph Editor** tab.

### Moving Nodes

A node is moved by clicking on the node and dragging. If multiple nodes are selected, clicking on any node in the selection and dragging will move all of the nodes.

![Blueprint Moving Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bd1b5f5-0071-4553-8ea0-b0363f331cf0/k2_move.png)

### Pins

Nodes can have pins on either side. Pins on the left are input pins, while those on the right of the node are outputs.

![Blueprint Input and Output Pins](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16b664e9-447f-4525-ac64-fbdc991f51ae/k2_pins.png)

There are two main types of pins: execution pins and data pins.

#### Execution Pins

![Blueprint Exec Pins](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a73129f-ddc3-4f7f-9129-f0c8745dfd7f/k2_pins_exec.png)

**Execution pins** are used to connect nodes together to create a flow of execution. When an input execution pin is activated, the node is executed. Once execution of the node completes, it activates an output execution pin to continue the flow of execution. Execution pins are displayed as an outline when not wired, and solid when wired to another execution pin. Function Call nodes always have only a single input execution pin and a single output execution pin as functions only have one entry point and one exit point. Other types of nodes can have multiple input and output execution pins, allowing for different behavior dependent on which pin is activated.

#### Data Pins

![Blueprint Data Pin Types](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/344eb741-1c42-47ca-a70b-ce50b461f556/k2_pins_data_types.png)

**Data pins** are used for taking data into a node or outputting data from a node. Data pins are type-specific and can be wired to variables of the same type (which have data pins of their own) or a data pin of the same type on another node. Like execution pins, data pins are displayed as an outline when not wired to anything, and solid when wired.

![Blueprint Data Pins](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0be1b31f-1e55-4353-ab2b-e76bd67d9317/k2_pins_data.png)

Nodes can have any number of input or output data pins. The data pins of a Function Call node correspond to the parameters and return value of the corresponding function.

#### Auto-Casting

Connections can be made between certain pins of different data types by way of the auto-casting feature in Blueprints. Compatible types can be identified by the tooltip displayed when attempting to create a connection between two pins.

![Blueprint - Compatible Types Message](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84b7b5a3-51c0-40de-a46f-0e4c52217ef3/k2_autocast_message.png)

Dragging a wire from a pin of one type to a pin of a different, but compatible, type will cause an **autocast** node to be created with wires to both pins.

![Blueprint - Autocast Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a10810f5-efb4-4742-89d5-8db3726e57b0/k2_autocast_node.png)

#### Promote to Variable

The value represented by a data pin can be converted to a variable within the Blueprint using the **Promote to Variable** command. This command creates a new variable in the Blueprint and wires it to the data pin being promoted. In the case of an output data pin, a Set node is used to set the value of the new variable. Essentially, this is just a shortcut to manually adding a new variable, adding it to the graph and wiring it to the data pin.

You can also create variables by using **Promote to Variable**.

Right-click any input or output data pins on a Blueprint node and select **Promote to Variable**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0522186-18ed-4c7b-9684-78127ca71b3c/ht38.png)

By right-clicking the **New Light Color** pin and selecting **Promote to Variable**, we can assign a variable as the **New Light Color** value.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8ebdce8-c600-4194-921d-fc234400a347/ht40.png)

Alternatively, you can drag off an input or output pin and select **Promote to Variable**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/152ef092-0115-4120-b10f-0c4b212ed3bb/ht39.png)

### Wires

Connections between pins are called **Wires**. Wires can represent either the flow of execution or the flow of data.

#### Execution Wires

Wires between exec pins represent the flow of execution. Exec wires are displayed as white arrows spanning from an output exec pin to an input exec pin. The direction of the arrow indicates the flow of execution.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15b74246-1f6b-4d1b-989d-47140dbe2032/selectnode.jpg)

Exec wires produce a visual indicator when being executed. During play, as one node completes execution and the next is activated, the wire between their execution pins highlights the fact that execution is being transferred from one node to another.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90248d73-dbfd-4b58-9c1c-8d153c2cdaf9/k2_flow_exec.jpg)

The visual indicator for an exec wire fades away over time.

#### Data Wires

Data wires connect one data pin to another data pin of the same type. They are displayed as colored arrows and are used to visualize the transfer of data, with the direction of the arrow representing the direction the data is traveling. The color of a data wire is dependent upon the type of data, just as the color of the data pins.

![Blueprint Data Wire](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c583d5a-8afb-4033-93ba-6a7530e6e3bd/k2_flow_data.png)

#### Working with Wires

Wires are created in the **Graph Editor** tab using one of the methods below:

-   Click on one pin and drag and release on another pin of the same type to create a direct connection.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65f56836-1c5c-412a-b528-54f81cac7d4e/hovercheck.jpg)
    
    The connection can only be made between two compatible types of pins. If you drag a connection on to a pin that is not compatible, an error will be displayed informing you the connection cannot be made.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e889331-fb84-4d16-9478-47a45454518e/hovercheckno.jpg)
-   Drag a connection from a pin and release in an empty space to summon a context-sensitive menu that lists all the nodes that are compatible with the type of pin the connection originated from. Selecting a node from this list creates a new instance of that node and makes a connection to a compatible pin on the new node.
    
    ![Blueprint Wire Creation - New Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e199fc6-d13c-40f1-b85d-77dc52d131c7/k2_connection_new.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a71a6ab-1f17-45fe-8a51-11ed92ac10a2/connectednodes.jpg)
    
    A wire between two pins can be broken using one of the methods below:
    
-   **Alt + Click** on one of the connected pins.
    
-   **Right-click** on one of the connected pins and choose Break Link(s).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0a85b22-446c-4cbb-bd4d-d2c8a18b031a/breaklinknode.jpg)

### Collapsed Graphs

Collections of nodes in the graph can be collapsed into sub-graphs for organizational purposes. This creates a hierarchy of graphs and allows large or complex portions of a graph to be viewed as a single node in the parent graph, with inputs and outputs, while still being able to edit the contents of the collapsed graph.

Unlike macros, a set of collapsed nodes is not shared, even within a single Level Blueprint or Blueprint Class. If you copy the collapsed node, it duplicates the internal graph. This can be handy if you want to make several variants of the same approximate behavior, but it also means that any bug fixes would have to be applied to each copy. The feature is really more intended to 'tidy up' a graph, hiding complexity inside, rather than any sort of sharing or reuse.

#### Tunnels

The collapsed graph uses tunnel nodes to communicate and interact externally with the graph that contains it.

The **Inputs** tunnel node acts as the entry point into the collapsed graph. It contains the execution and data pins that correspond to the input pins on the collapsed graph node in the parent graph.

![Blueprint Tunnel Entrance Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/396d71eb-6f34-4432-92d6-f34e3d9d9e12/k2_tunnel_entrance.png)

The **Outputs** tunnel node acts as the exit point of the collapsed graph. It contains the execution and data pins corresponding to the output pins of the collapsed graph node in the parent sequence.

![Blueprint Tunnel Exit Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44c32b28-59f1-406e-b574-5055f7d41733/k2_tunnel_exit.png)

These pins are automatically generated when the nodes are collapsed. Any execution or data wires connected to pins on the first node in the sequence causes a corresponding pin to be created on the **Inputs** tunnel node which appear on the collapsed graph node in the parent sequence as input pins. Similarly, any execution or data wires connected to the last node in the sequence cause corresponding pins to be generated on the **Outputs** tunnel node, and thus as pins on the collapsed graph node in the parent sequence.

#### To Collapse a Collection of Nodes

1.  Select the nodes to be collapsed in the graph by clicking and dragging a marquee selection box around them or **Ctrl + Clicking** on each node.
    
2.  **Right-click** on one of the nodes and choose **Collapse Nodes**.
    
    ![Blueprint Collapse Nodes - Menu Option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc07c358-6a70-49d7-b4f3-60827028df5e/k2_collapse_menu.png)
3.  Enter a name for the collapsed graph in the text field of the new node that appears and press **Enter**.
    
    ![Blueprint Collapse Nodes - Graph Name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/773ba9c7-f03e-4c9d-b7cf-d3eede63e404/k2_collapse_name.png)
4.  The collapsed graph is now displayed as a single node, and a reference to the collapsed graph appears in the **My Blueprint** tab.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25adbe03-1b1c-45c5-82fb-188ea4e6a197/collapsed_graph_myblueprint.png)
5.  To edit the collapsed nodes, **Double-click** the collapsed graph node or select the sub-graph in the **My Blueprint** tab.
    

#### To Expand a Collapsed Graph:

1.  **Right-click** on a collapsed graph node and choose **Expand Node**.
    
    ![Blueprint Expand Node - Menu Option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b092e024-76ff-43c8-8269-28251a5a7b04/k2_expand_menu.png)
2.  The collapsed graph node is replaced by the nodes it contained and is no longer present in the **My Blueprint** tab graph hierarchy.
    
    ![Blueprint Expand Node - Resulting Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72d5e072-c581-4c13-9b9c-7c03e002cbca/k2_expand_graph.png)
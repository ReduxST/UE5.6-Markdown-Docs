# Connecting Nodes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/connecting-nodes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/connecting-nodes-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:53

---

This page covers the various methods in which you can connect nodes together on your graphs in Blueprints.

## Pin to Pin Connection

The most common method of connecting nodes together is through **Pin to Pin** connection.

Using the **Left Mouse Button**, drag from one pin onto another compatible pin.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbcd4e0e-984a-4a8c-980d-c2bb5bc97c88/connectingnodes1.png)

A green check mark will appear when hovering over a compatible pin.

When attempting to connect two non-compatible pins, an icon will appear along with the reason why you cannot connect the nodes.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a6eea9c-2619-4de0-b3f7-cefb73cdd28e/noncompatible.png)

Typically pins are color coded to reflect the type of connection they take in.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc86006c-1fe3-4508-b211-827ed7242eeb/colorcoded.png)

There are instances where you can connect two different pin types together, in which case a **Conversion Node** is created.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07db3670-195a-43ce-9fa4-ce411925d2d0/conversionnode1.png)

Above we have taken a Integer output and connected it to a String input. You can see it will convert via the tooltip.

After connecting, a new conversion node is added between the two pins.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e2710ef-8f5a-40ef-8f4c-ae833fafc8a3/conversionnode2.png)

If you drag off a pin into an empty space in the graph, you can place a new node.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20d7f69b-1ee7-43c6-8cdb-da892ecee476/placenodenode.png)

When releasing the **Left Mouse Button**, the context menu will appear.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51100c4d-aba8-4a76-8e97-a15bf5f85724/dragoffnode.png)

-   See [Placing Nodes](/documentation/en-us/unreal-engine/placing-nodes-in-unreal-engine) for more information on the Context Menu.

After selecting a node to place, the nodes will automatically become connected.

You can also take an existing connection and connect it to another compatible pin.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9782d50-9fe2-48eb-9445-6b65681e2aa7/movingwires1.png)

In the example image above, holding **Control** and clicking on a pin and dragging to another input...

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a5e49b8-f683-4ab7-9d95-775351b9ce67/movingwires2.png)

This will allow you to move the connection from one pin to another without having to re-wire it.

### Pin Actions

There are some additional pin related actions that can be taken for nodes as outlined in the table below.

![Pin Actions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52fcab4d-8442-4578-bf1f-0741c98076ef/pinactions.png)

| Action | Command |
| --- | --- |
| Pin-specific Context Menu | **Right-Click** on Pin |
| Emphasize Connected Wires | **Mouse** Hover over Pin |
| Connect to Another Pin | **Left-Click** + Drag to Pin |
| Filtered Action Menu for Pin | **Left-Click** + Drag to graph |
| Break All Connections | **Alt + Left-Click** on Pin |
| Move All Connections | **Ctrl + LMB** Drag to Pin |

## Node to Node Connection

There are some **Node to Node** connections that are available when working with variables, which can save you a bit of time.

Say for example you have a **Set** variable node (in which you are setting the value of the variable to something) which is connected in your script somewhere and you want to swap it out for another variable without rewiring your script. You can drag another variable on top of the variable you wish to change and it will automatically swap it out and keep everything connected.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12502345-41e4-4809-b71d-c000609d9983/nodetonode1.png)

Above, we have an **Event Begin Play** which then sets the **Boolean Variable** to false and we want to change it out to set a **Float Variable** we have created instead. We can drag the Float variable onto the Set variable and you can see that the tooltip will inform you of the action you are taking which is to change the node to write Float Variable or Set it.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/279dd10c-31b1-4a46-a296-6d2133ada0b2/nodetonode2.png)

After confirming as indicated above, your node will be swapped with the new node and the connections will remain.

You can do the same for **Get** nodes which are connected already (below we are swapping one Bool variable out for another).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78b5078b-3fd9-4470-8b43-8aace628197a/nodetonode3.png)

## Drag-and-Drop Connection

Another shortcut you can take when working with variables is performing **Drag-and-Drop** (or Node to Pin) connections.

In the example below, upon **Event Begin Play** we want to set the light color of a Point Light. The **Set Light Color** node itself asks for the **New Light Color** which we have created a **Linear Color Variable** for. In the **MyBlueprint** window, we can drag-and-drop that variable directly onto the pin in the graph.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fad2d6a7-f6db-4c7e-85e7-0df4686d03c4/nodetonode5.png)

When doing so, the variable is automatically connected to the node.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c63d360-3aba-4905-a6f6-8d100ac2be28/nodetonode6.png)

Doing so this way eliminates the process of adding the node to the graph, then performing a pin to pin connection.

## Reroute Connections

When working with complex or large Blueprints, you may run into situations where your wires are all over the place and you want to change the way they appear in the graph for visual clarity. There is an option to add a **Reroute** node, which will allow you to move the wires around by adding an "extension cord" of sorts to your out pin.

Here we have an out pin's wire that is hidden behind another node which is outlined in the box.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/daf2cd38-106b-4e8d-846c-48655276d971/reroute1.png)

By dragging off the out pin that we want to reroute, we can select the **Add Reroute Node** option.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f4dcbf4-e936-426f-aa67-ee59af152946/reroute2.png)

This will create a new pin in your graph that your original pin is connected to.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdc63dfc-148c-48b0-a4b7-393193a27a9e/reroute3.png)

You can then drag off the new pin and connect it to your target as shown below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a231162-4119-44c4-b9f6-494034ff1668/reroute4.png)

The Reroute node acts as the original pin and can be dragged off of and new nodes can be connected to it.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88bc087e-e60b-425c-bc5a-d2b097ce3861/reroute5.png)

Using Reroute nodes will help keep your Blueprints clean, allowing anyone who accesses them the ability to see the connections clearly.
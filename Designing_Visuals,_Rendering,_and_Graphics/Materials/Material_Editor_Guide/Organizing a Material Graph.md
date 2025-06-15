# Organizing a Material Graph

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/organizing-a-material-graph-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/organizing-a-material-graph-in-unreal-engine)  
**Processed:** 2025-06-14 16:40:43

---

As Materials increase in complexity, the node graph can quickly become difficult to read and interact with. Complicated, unorganized graphs can be slow to edit, and difficult to comprehend when a Material is handed off from the primary author to another artist or developer.

## Material Editor Organization Tools

Unreal Engine includes several tools to improve the organization of your Material graphs.

1.  [Commenting](/documentation/en-us/unreal-engine/organizing-a-material-graph-in-unreal-engine#commenting)
2.  [Reroute Nodes](/documentation/en-us/unreal-engine/organizing-a-material-graph-in-unreal-engine#reroutenodes)
3.  [Named Reroutes](/documentation/en-us/unreal-engine/organizing-a-material-graph-in-unreal-engine#namedreroutes)
4.  [Align and Distribute](/documentation/en-us/unreal-engine/organizing-a-material-graph-in-unreal-engine#alignanddistribute)
5.  [Collapse Nodes](/documentation/en-us/unreal-engine/organizing-a-material-graph-in-unreal-engine#collapsenodes)

## Commenting

Comments are the easiest way to improve the readability of a Material graph. This Material isn't overwhelmingly complicated, but without annotations it would take a moment or two to interpret if it was passed off to a second artist.

 ![Uncommented Material Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2aa51cda-564b-4dfb-bb66-6e732957f15c/messy-graph.png) ![Material Graph with comment boxes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1368eba5-87a4-4db2-a77a-cbfce92bd1c7/commented-graph.png)

**A Material Graph network with and without comments.**

Drag the slider to see the same Material annotated with comments. It is immediately apparent from the labels what each group of nodes is doing.

There are two ways to add comments to Materials.

### Node Description

You can add a comment or description to any individual Material Expression or Function in the node graph.

1.  Hover the mouse pointer over a node in the Material graph.
2.  **Left-click** the **Toggle Comment Bubble** icon.
    
    ![Toggle comment bubble](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fc70fe7-78b0-45bb-9c5d-0777502f67f2/toggle-comment.png)
3.  Enter a comment in the field.
    
    ![Enter comment](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68ce0550-85ed-450e-9c85-1e33f5cc56a5/add-comment.png)
4.  Click the pin icon if you want the comment to remain visible as you zoom in and out of the Material Graph. This keeps the comment at a readable scale, even when zoomed out. You can click the **Toggle Comment Bubble** icon again to hide the comment.
    
    ![Pin Comment](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/965337e9-b178-4678-85fc-486831188fff/pin-comment-sm.png)

Anything you type in the Comment Bubble will also appear in the **Desc** field in the **Details** panel for that node. This description remains visible even when the Comment Bubble is hidden.

![Node description box](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/199bcd7c-5d08-4c3d-b82a-1379dd670025/node-description.png)

### Comment Box

You can use a comment box to group a selection of related nodes.

![UV Tiling comment box](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c010b209-dfc9-4eef-b6a8-88ef2455630b/global-tiling-comment.png)

1.  Select all the nodes you want to place in a comment box.
2.  Press the **C key** to create a comment box around the selected nodes.
3.  Type a name in the header field.

Comment boxes let you move all the nodes within the box as a single group. **Left-click and drag** the header bar to move a comment box.

-   You can add and remove nodes by dragging them in or out of the comment box.
-   Resize a comment box by dragging the corners or edges.
-   You can nest comment boxes within one another.

### Comment color

Comment boxes have a color property in the **Details** panel.

1.  Click the **header bar** of a comment box to access its Details properties.
    
    ![Comment header bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1b8d692-379b-40e0-8964-d5b4ff741794/comment-header.png)
2.  Click the **Comment Color** swatch and choose a new color in the **Color Picker** dialog.
    
    ![Comment color picker](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/337479ac-9237-4099-b31a-94e347660ff9/comment-color-sm.png)

## Reroute Nodes

Reroute nodes provide a way to modify the path of the wire between two Material expression nodes. You can also use a reroute node to split a wire in order to connect it to multiple inputs.

Double-click anywhere along the length of a wire to add a Reroute node.

![Add wire reroute pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/100b1720-e532-4551-9aa5-e772ad95b4d4/cable-reroute-add.png)

To modify the path of the wire, hover over the Reroute node until the mouse displays a move icon.

![Move cable reroute pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79204a6f-f6e7-4f6c-b48c-3c572b6e2038/cable-reroute-hover.png)

Left-click and drag the node to a new location. Reroutes allow you to redirect wires around nodes that are in the way of the original path.

![New cable path](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6fb4ed0-62fb-4fef-8ade-0f866c61266f/cable-reroute-example.png)

In this video a Reroute node is used to split a wire in order to feed it into three downstream inputs.

## Named Reroutes

**Named Reroutes** let you simplify a Material graph by eliminating wire connections and routing information through input and output nodes instead. A Named Reroute is like a tunnel or portal from one region of the Material graph to another.

For example, this small cluster of nodes related to the Roughness map creates a relatively long wire across the middle of the Material graph. Using a Named Reroute you can eliminate the wire without affecting the flow of data.

![Unnecessary cable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbed7a2b-2579-48b2-be20-e7b10c478b67/unnecessary-cable.png)

### Creating Named Reroutes

1.  Double-click along a wire to add a Reroute node.
    
    ![Named reroute pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed3a44ad-6d4b-4402-ba41-f75db3f789e2/named-reroute-pin.png)
2.  Right-click the node and choose **Convert to Named Reroute** from the context menu.
    
    ![Convert to named reroute](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78e70c05-ddf6-47ab-9738-2569de7f182f/convert-to-named.png)
3.  The wire connection disappears and two **Named Reroute** nodes are created at the beginning and end of the connection. Shown side by side you can see how a Named Reroute resembles a tunnel. Data flows into the first node, and exits through the second, which is called a **Named Reroute Usage node.**
    
    ![Named reroute nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1cdb25b9-8a34-4246-9ed7-eb3d30d9cd35/named-reroute-nodes.png)

The first node in a reroute is called the **Named Reroute Declaration.** It is extremely important to give this node a unique, descriptive name in the **Details** panel.

![Reroute declaration description](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6170bc45-a661-4890-a1c8-b9bde50428ef/reroute-declaration.png)

Select the Named Reroute Declaration node and enter a description in the **Name** field. You can also change the **Node Color** property if you want to color-code your reroutes.

Named Reroute **output nodes** can be passed into multiple inputs further downstream, or can be duplicated and used multiple times.

For example, earlier we used a Reroute node to pass the Global UV Controls into three downstream inputs.

![Triple reroute pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20ed6e4d-8473-4da6-8ba4-5ca73998e1e0/triple-reroute.png)

If this pin is converted to a Named Reroute, three **Usage** nodes spawn instead of one.

![Three usage nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b5b1179-d0a5-41ad-aadb-fda005eb8809/triple-output.png)

Everything within the **Global UV Controls** comment box is now physically detached from the rest of the node network. You can move it anywhere in the graph and the data will still flow through the Named Reroute into the **Albedo**, **Roughness**, and **Base Normal** UVs.

![Named reroute data flow](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/701c203a-74dc-4e7b-a022-52ca0050148d/named-reroutes-zoomedout.png)

Or if you prefer you could use a single Named Reroute output node and feed it into all three UV inputs.

![Single usage three inputs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccc7e39d-4abb-4bd0-a633-d30060c09271/named-reroute-output-alt.png)

### Adding Named Reroute Usage Nodes

You can add additional Named Reroute Usage nodes from the **right-click** menu or the **Palette.**

Any Named Reroutes in your Material appear at the very top of the menu. You can also duplicate existing reroute nodes by selecting them and pressing **Ctrl+D.**

![Named Reroutes in palette](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6fea6167-5ad0-401d-8595-da2e1a4fc709/call-reroutes.png)

### Convert Back to Traditional Reroute

You can convert any Named Reroute back to an unnamed Reroute pin if you decide it is beneficial to see the wire connection.

 ![Named reroute](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82a3eb9d-8387-462b-b458-cbbfb3c9a358/restore-connection.png) ![Named reroute converted to pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06a6ebad-554d-4c07-918f-f819bd0b5537/reroute-pin-restored.png)

The Roughness Named Reroute is converted back to a traditional Reroute pin.

1.  **Right-click** a Named Reroute Declaration or Usage Node (either one works).
2.  Choose **Convert to Reroute** from the menu.
    
    ![Convert back to reroute](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eadde072-830a-48f1-ae32-241e5a7afbbd/convert-to-reroute-cleaner.png)
3.  The wire is restored and an unnamed Reroute pin is left behind. You can select the pin and press **delete** if it is no longer needed.
    
    ![Delete reroute pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/439996f2-1ebd-40d8-b95c-d1e3615874ff/delete-pin.png)

### Reroute Selection Options

There are selection options for Named Reroute nodes that let you **find and select** corresponding Reroute nodes in the Material Graph.

Right-click a **Named Reroute Declaration** node and click **Select Named Reroute Usages** to select all the downstream output nodes for that reroute.

![Select reroute usages](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e668174-4d25-4462-a724-29471dfe6999/select-usages.png)

Right-click a **Named Reroute Usage** node and click **Select Named Reroute Declaration** to select the upstream origin node of the reroute.

![Select reroute declarations](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7cddd153-923b-4149-b575-c362bb0eea9a/select-declaration.png)

## Align and Distribute

The Material Editor has several options in the right-click menu to align and distribute nodes in your Material graph.

1.  Select two or more nodes that you want to align.
    
    ![Select multiple nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04c9172d-3b75-4fa6-9368-00a064473787/select-multiple.png)
2.  **Right-click** one of the nodes and open the **Alignment** sub-menu.
    
    ![Alignment options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/874d7565-3a2a-4ae2-83fd-3d4859eb95b4/alignment-options.png)
3.  Select one of the options to align or distribute the selected nodes.
    
    ![Nodes left-aligned](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08ed4ff8-2e85-417f-93cf-b21590d9cec2/aligned-and-distributed.png)

In this example, **Align Left** was used to line up the left edge of the selected nodes. **Distribute Vertically** was then used to create equal spacing between them on the vertical axis.

### Align

The options in the Align menu let you align nodes along six different axes. You can also straighten the connection wire between two nodes.

| Option | Result | Shortcut |
| --- | --- | --- |
| Align Top | Align the top edge of selected nodes. | Shift+W |
| Align Middle | Align selected nodes at their vertical middles. | Alt+Shift+W |
| Align Bottom | Align the bottom edge of selected nodes. | Shift+S |
| Align Left | Align the left edge of selected nodes. | Shift+A |
| Align Center | Align selected nodes at horizontal centers. | Alt+Shift+S |
| Align Right | Align the right edge of selected nodes. | Shift+D |
| Straighten Connection | Straightens the wire between two nodes so that it is perfectly horizontal. | Q |

### Distribution

The **Distribution** options allow you to create equal spacing between the selected nodes on either the horizontal or vertical axis.

| Option | Result |
| --- | --- |
| Distribute Horizontally | Create equal horizontal spacing between selected nodes. |
| Distribute Vertically | Create equal vertical spacing between selected nodes. |

## Collapse Nodes

You can use the **Collapse Nodes** option to condense multiple Material Expressions or Functions into a single node.

There are a few reasons you might want to do this.

-   If a large group of related nodes is getting too complicated, collapsing them can free up space in the graph and make the Material easier to read.
-   A second use case is if a set of nodes is so commonplace or repetitive that you don't need to see the full node network to understand its purpose.

For example, the **Detail Normal Tiling** nodes shown below use a familiar method for controlling the scale of a texture.

![Detail normal tiling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b86f6a2f-f845-41bc-909c-c236cd92cd78/detail-normal-tiling.png)

To simplify the graph, you could collapse everything within the Detail Normal Tiling box .

### How to Collapse Nodes

1.  Select all the Material nodes you want to collapse.
    
    ![Select node group](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9dbdc544-50da-4049-a9e6-9c136bfc52e0/select-detail-normals.png)
2.  . **Right-click** one of the nodes and choose **Collapse Nodes** from the context menu.
    
    ![Collapse nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf52fc36-f065-4b65-868f-2bf7200afc2a/collapse-nodes.png)
3.  The selected Material Expressions are replaced by a single node with the default name **Collapsed Nodes**.
    
    ![Nodes collapsed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5594bdbe-03e8-4e10-996e-a294d3a91f64/collapsed-nodes-unnamed.png)
4.  **Left-click** the name at the top of the node, and enter a descriptive name in the field.
    
    ![Rename nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49e3baad-8fee-4bf4-8d41-a0513ad50c42/rename-collapsed-node.png)
5.  The Detail Normals section of the graph is greatly simplified.
    
    ![Detail normal simplified](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ccf3e20-e517-4006-a710-b47147ade0a8/detail-normals-condensed.png)

### Editing Collapsed Nodes

Nothing has changed about the Material Graph. The Collapsed Node simply acts as a container for the node network within it.

If you mouse over a Collapsed Node you will see a preview of the Material graph stored inside.

![Hover preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dadca7ea-e0a9-4aaa-a42f-5ea37fada9ba/collapsed-node-preview.png)

**Double-click** a Collapsed Node to view and edit the contents. This opens a sub-graph within the same Material Editor tab.

Click **Material Graph** in the breadcrumb navigation at the top of the Material Editor to stop viewing the collapsed nodes and return to the main graph.

![Return to graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d492f29-2b6c-4d6f-8e36-4d7e35a7134b/return-to-main-graph.png)

### Expanding Collapsed Nodes

You can expand collapsed nodes back to their previous configuration in the Material Graph.

1.  Right-click a collapsed node.
2.  Click **Expand Node** in the context menu.
    
    ![Expand node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ed4a66a-0e9e-4176-a05f-db1a1956e63e/expand-node.png)
3.  The collapsed nodes are restored to their original position.
    
    ![Nodes restored](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c61773a6-256a-4df8-a0f1-aa0f2a69c34d/nodes-restored.png)
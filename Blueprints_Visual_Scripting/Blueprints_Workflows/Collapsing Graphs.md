# Collapsing Graphs

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/collapsing-graphs-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/collapsing-graphs-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:56

---

This page covers several ways in which you can collapse your **Blueprint** graphs into a single node, into a **Function** or into a **Macro** which can help clean up any large graphs you may have by consolidating them into a linked graph.

## Collapsing Nodes

The easiest method of collapsing which is illustrated below is through **Collapsing Nodes** into a linked graph. These are primarily used for organization and keeping things nice and neat inside your Event Graph.

1.  On the **Graph** of a **Blueprint**, locate the nodes that you want to collapse.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53be7b8e-bf89-48f0-914f-2f09392435db/collapse1.png)
    
    Here we have some nodes that reduce the player's energy after they jump.
    
2.  Select all the nodes that you want to collapse by **Left-clicking** and dragging over the nodes.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9494c016-90bb-4d24-9cc1-e897d129769e/collapse2.png)
    
    You can also **Control + Left-click** to add/subtract nodes to your selection.
    
3.  Once you have the nodes you wish to collapse, **Right-click** on any node in the selection and choose **Collapse Nodes**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d2f19e5-f441-4807-8814-da75ff3b240b/collapse3.png)
4.  The nodes will be collapsed into a single **Collapsed Graph** node, which you can then assign a name.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e5aa194-5a5a-4655-8a7a-2920c77c1fcb/collapse4.png)
5.  If you mouse over the **Collapsed Graph** node, you will see a preview window of the node network.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9569a43-7af3-497a-8240-fff7d79282e3/collapse5.png)
6.  **Double-clicking** on the **Collapsed Graph** will open up a new graph with your selected nodes.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7a6ba9a-eb5f-4bf9-a71a-d8b42069c988/collapse6.png)
7.  Inside the **Collapsed Graph**, you can add pins to the **Inputs** or **Outputs** nodes from the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea791afe-1740-46e0-b0f0-3f063eab44af/collapse10.png)
    
    **Execute** is added by default when collapsing, here we have added two Execute Out Pins: **OutOfEnergy** and **CanJump**.
    
    We also modified the graph to check if the player is out of energy before subtracting from the overall energy the player has.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77e0f1f4-41e8-45e9-b93a-b9ae2ab1c68d/collapse8.png)
    
    And our **Event Graph** with the collapsed node would look something like below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5b55dd0-a08f-499b-8aa9-11c7a17d8f8a/collapse9.png)
8.  By **Right-clicking** on the collapsed node, you can select **Expand Node** to revert the nodes to their original state.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96b401ca-66e9-4e05-a687-1f2fa6e6f414/collapse7.png)

## Collapsing to Function

Another method that can be used to collapse your nodes is to collapse them to a **Function**. The benefit of collapsing your nodes to a Function versus to a Collapsed Graph is that not only can you can call the Function in another area of script based on whatever parameters you wish to specify, but you can also call the Function from inside a different Blueprint (as long as you provide a reference to the Blueprint that contains the Function you wish to call).

Below are the steps you can take to collapse your nodes to a Function.

1.  With the nodes you want to collapse selected, **Right-click** on a node and select **Collapse to Function**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9eafc946-0a22-4618-9877-b77555d026e1/collapsefunction1.png)
2.  A new **Function** will be created, which you can re-name from the **MyBlueprint** window by pressing **F2** on it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7dbcc7b9-4f1b-4eed-8d50-429f6e37b918/collapsefunction2.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1dba3d0c-79ca-4a74-974e-7fbe3be29d3e/collapsefunction3.png)
    
    Here you can re-name your Function.
    
3.  **Double-clicking** on the Function will open it up in a new graph window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a42b6c0-4ca2-4322-8003-80bc0acba1d7/collapsefunction4.png)
    
    Similar to Collapsed Graphs, you can click on the **Inputs** or **Outputs** nodes and add pins to them via the **Details** panel.
    
4.  You can call the Function by its name off any condition you wish to specify.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8937990b-8a73-40e1-a130-a49e0fb443f4/collapsefunction5.png)
    
    Here we are calling the **Remove Energy** Function whenever F is pressed.
    
5.  You can revert this collapsing by **Right-clicking** on the Function and selecting the **Expand Node** option.
    

For more information about Using or Calling Functions, see the [Functions](/documentation/en-us/unreal-engine/functions-in-unreal-engine) documentation.

## Collapsing to Macro

In addition to collapsing to a Collapsed Graph or Function, you can also collapse nodes to a **Macro**. The best way to think of a Macro is that it allows you to take several nodes that are connected and consolidate them into a single node that does everything you need it to do all in one. It is particularly useful for anything that you do frequently, like a complex math equation.

See below for steps on collapsing nodes to a Macro.

1.  With the nodes you wish to collapse selected, **Right-click** on a node and select **Collapse to Macro**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/850db7bc-5fd4-447c-95ba-92752b033002/collapsemacro1.png)
2.  A new Macro node will be created, which you can rename via the **MyBlueprint** window by pressing **F2** on it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b2595b7-83f6-482c-8baf-c860d493f5f4/collapsemacro2.png)
3.  You can open the Macro by **Double-clicking** on it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f5c8868-3794-4e47-88d4-0778c1d15cbe/collapsemacro4.png)
    
    As with the other method of collapsing nodes, you can add **Input** or **Output** pins as needed.
    
    Here is our Event Graph which implements the Macro with the additional pins.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6d0c6cd-5a76-41e6-91bd-ffdaa80d731e/collapsemacro5.png)
4.  By **Right-clicking** on your Macro, you can select **Expand Node** to revert the collapsing of the nodes.
    

For more information about Macros, see the [Macros](/documentation/en-us/unreal-engine/macros-in-unreal-engine) documentation.
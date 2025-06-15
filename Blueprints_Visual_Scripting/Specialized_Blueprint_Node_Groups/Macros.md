# Macros

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/macros-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/macros-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:43

---

**Blueprint Macros**, or **Macros**, are essentially the same as collapsed graphs of nodes. They have an entry point and exit point designated by tunnel nodes. Each tunnel can have any number of execution or data pins which are visible on the macro node when used in other Blueprints and graphs.

## Creating a Blueprint Macro

Blueprint Macros can be created within a Blueprint Class or Level Blueprint, just like Blueprint Functions. They can also be organized into Blueprint Macro Libraries.

To create a Blueprint Macro inside a Blueprint Class, Level Blueprint, or Blueprint Macro Library:

1.  In the **My Blueprint** tab create a new macro, by clicking on the **Add Button** ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e304ce5-e31b-4846-91d2-b785a0250521/plus_button.png) on the macros list header ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aad4cf5a-6a57-48a2-b175-8f4cf75656e5/myblueprint_macro.png).
    
2.  Enter a name for your Blueprint Macro.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f4a3f45-d34d-4762-b770-dca6166c0af3/name_macro_blueprint.png)

Your Blueprint Macro will open in a new tab in the **Graph** tab of the Blueprint Editor.

You can also create a Blueprint Macro by **Right-clicking** in the **My Blueprint** tab and selecting **Macro**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50a6fe74-75cc-4e56-9bfd-4054ece51c41/add_macro_rtclick.png)

## Building a Blueprint Macro

When you first create a Blueprint Macro, a new graph will open containing an **Inputs** tunnel node and an **Outputs** tunnel node.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99df6452-fb8c-4b49-8b87-c43e7dfa8b14/input_output_macro.png)

In the **Details** pane for your Blueprint Macro, you can add input and output execution and data pins. You can also set the **Description**, **Category**, and **Instance Color** of your Blueprint Macro.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dace9cd9-5faa-43c2-8a7c-4c4e197c377f/new_macro_details.png)

To add input or output parameters:

1.  Click on the **New** button in either the **Inputs** or **Outputs** section of the **Details** pane.
    
2.  Name the new parameter and set its type using the dropdown menu. In this example, there is an Integer data input parameter named **Score**, an input execution pin named **Test**, and two output execution pins named **Win** and **Lose**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0994dc39-b9a4-44e5-9a49-4e78cc260240/macro_details.png)
    
    The tunnel nodes in the Blueprint Macro graph will automatically update with the correct pins.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12254580-aa96-4414-ba79-0ea1ee51e314/macro_tunnels_with_pins.png)
3.  You can also set a default value by expanding the entry for the parameter.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d075dbf-20d7-4d39-a604-94d8c919dbf5/macro_details_expanded.png)

To change the location of the pin for this parameter on the edge of the node, use the up and down arrows in the expanded **Details** pane entry.

To give your Blueprint Macro some functionality, connect data and execution wires to the pins of your **Inputs** and **Outputs** tunnel nodes and create a network between them.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d67b5586-d878-440f-8869-61a16858d389/score_comparison_example_macro.png)

This example Blueprint Macro checks if the score that is input into the Macro is greater than the necessary score for winning, and then triggers different output execution flows depending on the result of the comparison. Note here that the **Test** and **Score** pins were flipped using the up and down arrows in the **Details** pane, to avoid wires crossing in the Blueprint Macro graph.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f29e35d-7740-42ef-b889-890fd62fd612/move_pin_arrows.png)

Unlike Functions, Macros can have more than one output execution pin, so you can have execution flow like this where different output execution pins are activated depending on the results of graph logic. Also, you could have a Macro with no execution pins that only manipulates data, as long as the nodes within the Macro are not execution nodes.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d805efc0-4e34-4cf5-b87a-1c5bcdbbe27a/data_macro.png)

### Implementing Macros

There are several ways to add a Macro node to another Blueprint graph. Like Function nodes and Custom Event Call nodes, it is possible to add multiple copies of Macro nodes throughout the graphs in your Blueprint.

To add a Macro, **Right-click** in the graph and select the Macro in the context menu that appears.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2efee6e1-d178-4c92-bc7a-be5e2fc4af1d/right_click_add_macro.png)

You can also drag and drop off the pin of another node, and the Macro will appear in the context menu if it has a parameter pin of the corresponding variable type and flow direction.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9690d749-5c29-4688-8132-892dad377fa3/pin_macro_summon.png)

Alternatively, you can drag the Macro from the **My Blueprint** tab and drop it in the graph.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc86af00-0ad9-4838-9b4e-de6e1c3e1656/macro_drag_1.png)

Once the Macro node has been added to the graph, it behaves like any other node and the input and output pins can be wired accordingly. **Double-clicking** on a Macro node will open the Macro's graph.
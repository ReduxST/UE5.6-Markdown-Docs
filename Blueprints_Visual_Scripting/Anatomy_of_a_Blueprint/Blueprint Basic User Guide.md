# Blueprint Basic User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-basic-user-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-basic-user-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:23

---

This page aims to quickly get you started using **Blueprints** by covering the most basic use cases and commonly used actions.

For more detailed information on Blueprints, refer to the [Blueprints Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) documentation.

## Creating Blueprints

There are several methods in which you can create Blueprints, the first is through the **Content Browser** using the **Add New** button:

1.  In the **Content Browser**, click the **Add New** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7469bfc5-6533-4cb2-a646-552215db8906/contentbrowseraddnew.png)
2.  Select **Blueprint Class** from the **Create Basic Asset** section of the dropdown menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/846ba685-3440-4abb-b515-7fc74402a95a/contentbrowserdropdown.png)
    
    You can create several different [types of Blueprint Assets](/documentation/en-us/unreal-engine/types-of-blueprints-in-unreal-engine) from the **Blueprints** option under **Create Advanced Asset**.
    
3.  Choose a **Parent Class** for your Blueprint Asset. See [Parent Classes](/documentation/en-us/unreal-engine/blueprint-class-assets-in-unreal-engine#parentclasses) for more information.
    
    ![Choose a Parent Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4cc035a-4fad-4b19-90d2-39d538604814/new_asset_parent_class.png)

After you select your class, a new Blueprint asset will be added to the **Content Browser** which you can then assign a name.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59589841-a1e6-47b4-98d1-70d03ba9d0ef/basic4.png)

### Create Blueprint Using Assets

You can also create a Blueprint by **Right-clicking** on an asset in the **Content Browser**, then under *Asset Actions*, selecting the **Create Blueprint Using This...** option.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a774673-5fd6-4fb6-b65e-68eb5ce1504f/basic8.png)

This option is only available for assets that support it - Static Meshes, Skeletal Meshes, Particle Effects, Sound Cues or Sound Waves, etc. If the option is not available for the selected asset, it will appear grayed out.

After selecting the **Create Blueprint Using This...** option, you will be prompted on where you want to save the Blueprint. After confirming your save location, the Blueprint will automatically open in the Blueprint Editor.

## Placing Blueprints in Levels

To place a Blueprint in your level, you can either...

**Drag-and-drop** it from the **Content Browser** into your level.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32c0d35b-3d57-480c-adaf-f6f9c9109ef4/draganddropbp.png)

Or with the Blueprint selected in the **Content Browser**, you can **Right-click** in the level and select **Place Actor** from the context menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f17064d-0cde-4778-afb4-a6ff8b9abc59/rightclickmethod.png)

## Placing Blueprint Nodes

There are several methods in which you can place nodes while using the **Graph** (see [Placing Nodes](/documentation/en-us/unreal-engine/placing-nodes-in-unreal-engine) for more information), this section will show you the most common method as well as how to connect nodes together.

Most of the time when placing nodes, you will use the **Context Menu** which can be accessed by **Right-clicking** inside a Blueprint graph.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4debfce5-be72-4330-9fcf-29b927cf6aee/rightclick1.png)

From the menu above, you can expand any category (or sub category) and select the node you wish to add to the graph.

There is also an option in the upper right corner of the window called **Context Sensitive** that is enabled by default but can be disabled which automatically filters the options presented in the menu based on the current context.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f10fe35d-c71d-4680-b2d4-1ecb95e07567/rightclick2.png)

As you can see below, when **Right-clicking** and searching for **Animation** with **Context Sensitive** on, you are presented with a filtered list.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/678ef694-6802-4c40-ae65-0ce8d21b2515/rightclick3.png)

However, if you un-check **Context Sensitive** and search for **Animation**, you are presented with everything related to animation.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59c711e6-bc3e-4552-92ba-28b2e96b98fd/rightclick4.png)

While **Right-clicking** in the graph brings up the Context Menu, you can drag off an existing node to access the Context Menu as well.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f632da1-65a9-4382-bdf3-65f5c9b55656/rightclick5.png)

Above, we have a **Character Movement** Component Reference and by dragging off its out pin, we can add nodes that contextually make sense and are relevant to the node we are dragging off of as seen in the example below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83ca5463-8264-41b5-b10c-6ded8e21aee6/rightclick6.png)

Above we can set the character's Max Walk Speed by searching for **Set Max Walk** then choosing **Set Max Walk Speed** from the menu.

## Connecting Blueprint Nodes

To connect nodes, drag off one pin and connect it to another pin of the same type (there are some instances where a conversion node will be created, for example, connecting a Float output to a Text input will create a conversion node between the two and automatically convert and connect the two nodes).

Here is a basic connection between two nodes where the input/output pins are of the same type.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e704a89-2e8a-4755-ade2-7f76a96aeb90/basicconnect.png)

And here is an example of a conversion in progress.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7447f5f4-eea6-4c8a-801a-7c3b8cbc446a/conversionnode.png)

-   See [Blueprint Editor Cheat Sheet](/documentation/en-us/unreal-engine/blueprint-editor-cheat-sheet-in-unreal-engine) for additional node based actions and shortcuts.

## Creating Variables

**Variables** are properties that hold a value or reference an Object or Actor in the world. These properties can be accessible internally to the **Blueprint** containing them, or they can be made accessible externally so that their values can be modified by designers working with instances of the Blueprint placed in a level.

You can create variables for your Blueprints from the **MyBlueprint** window, by clicking on the **Add Button (+)** on the variable list header.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e984b7d9-6b40-4d9c-bf0c-f4ac40c0fc4b/myblueprint_variable.png)

Once you have created a variable, you will need to be able to define the properties of the variable.

-   See [Blueprint Variables](/documentation/en-us/unreal-engine/blueprint-variables-in-unreal-engine) for more information on variable types and more on working with them.
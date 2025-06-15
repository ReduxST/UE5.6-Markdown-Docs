# Working With Dataprep Instances

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-dataprep-instances-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-dataprep-instances-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:43

---

In the Visual Dataprep system, your Dataprep Assets provide reusable recipes that help you be consistent about how you import and modify 3D data. The Dataprep graph provides a high level of flexibility and power; you can use it to manipulate your data in whatever way you need to make your imported scenes work well at runtime in Unreal Engine.

Sometimes, depending on what tasks you need your Dataprep graph to carry out, you may need to make adjustments in order to work with different input scenes or assets. For example, a new set of input data may use a different naming convention for objects or surfaces, and you may need to change settings in your graph to match. You can always modify your Dataprep Asset graph to handle these new situations. However, Dataprep graphs can be large and complex, and in larger organizations the person who needs to import content might not be the same person who created the graph. In cases like this, it may not always be clear what settings need to be changed.

To make these kinds of situations easier, you can select important settings in your Dataprep graph and expose them as *parameters*, with descriptive names that you choose. When anyone edits the Dataprep Asset, these exposed parameters show up in a special **Parameterization** area within the **Settings** panel at the upper right of the Dataprep Editor. This effectively highlights selected settings that other users might need to customize most often.

In addition, you can create a Dataprep *Instance* that allows users to *only* modify the parameters you have chosen to expose, but that prevents them from touching the rest of the Dataprep graph. By judiciously exposing the right settings in your Dataprep Assets and creating Dataprep Instances from them, you can give users in your organization the freedom they need to modify pre-selected settings, without requiring them to modify or even see the actual logic of the Dataprep graph itself.

If you're familiar with the way you work with Materials and Material Instances in the Unreal Engine, the concept of the Dataprep Asset and the Dataprep Instance is exactly analogous.

## Exposing Parameters in a Parent Dataprep Asset

To expose settings in a Dataprep Asset so that they can be customized as parameters and overridden in Dataprep Instances:

1.  Set up your Dataprep graph the way you want it.
    
2.  Right-click the setting you want to expose. In the context menu, under the **Parameterization** section, click **Link to Parameter**.
    
    Click image for full size.
    
    You can expose any setting in any type of Dataprep blocks: filter blocks, operator blocks, and transform blocks.
    
3.  In the text box provided, enter a descriptive name you want to use to refer to the parameter. When the name is the way you want it, click **Create New Parameter** under the text box.
    
    Click image for full size.
    
4.  The setting you chose is marked in the Dataprep graph with a link icon, to mark that it has been exposed for customization. You can hover over this icon to see the name of the parameter that corresponds to this setting.
    
    Click image for full size.
    
    The new parameter you created also shows up in the **Parameterization** section of the **Settings panel** at the top right of the Dataprep Editor.
    
    Click image for full size.
    
    Modifying the value of the setting in either the block or the **Settings** panel modifies it in both places.
    

Your setting is now editable in any Dataprep Instance you create from this Dataprep Asset, under the parameter name you set. See the following sections for details.

If you want to remove the parameterization on a setting so that it can no longer be changed in any Instances of this Dataprep Asset, right-click the setting again and choose **Remove Link to Parameter**.

You can link multiple settings on different Dataprep blocks to a single named parameter. If different parts of your Dataprep graph rely on the same threshold values or string names, reusing a parameter to drive multiple different block settings can help reduce the number of parameters you expose to your Dataprep Instances.

## Creating a Dataprep Instance Asset

You can create a Dataprep Instance Asset from any Dataprep Asset. Right-click the Dataprep Asset in the **Content Browser**, and in the context menu click **Create Instance**.

Click image for full size.

Your new Dataprep Instance Asset is created in the same folder as its parent. You can assign it a name and double-click it to open it up in the Dataprep Instance Editor to configure the values of its exposed parameters.

## Setting Up the Dataprep Instance Asset

When you edit a Dataprep Instance Asset, it opens in an editor that contains most of the same panels visible in the main Dataprep Editor.

Click image for full size.

The main difference is that the graph editor is completely missing. In a Dataprep Instance, you can't modify or even see the recipe that the Dataprep Instance will use to modify the scenes you import. Instead, you only have access to the settings that have been exposed in the parent Dataprep Asset, in the **Parameterization** section of the **Settings** panel at the top right of the editor.

Otherwise, working in the Dataprep Instance Editor is very similar to working in the Dataprep Editor:

-   Use the **Settings** panel to customize input files and output locations.
-   Use the buttons in the Toolbar to **Import** the input files, **Execute** the Dataprep graph, and **Commit** the results to your Unreal Engine Project.
-   Use the preview panels to interact with your imported data and make sure that it looks the way you are expecting before you commit the results.
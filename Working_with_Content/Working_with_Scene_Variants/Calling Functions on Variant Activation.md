# Calling Functions on Variant Activation

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/calling-functions-on-variant-activation](https://dev.epicgames.com/documentation/en-us/unreal-engine/calling-functions-on-variant-activation)  
**Processed:** 2025-06-14 16:11:49

---

Whenever you bind an Actor to a Variant, the Variant Manager prompts you to choose the properties of that Actor that you want to change when the current Variant is switched on. However, in addition to or instead of changing a bound Actor's property values, you can also specify one or more functions that you want the Variant Manager to invoke on that Actor.

You can set up the Variant Manager to call any function that is already exposed by the Actor you've bound. You can also create your own new Blueprint function from scratch that accepts the bound Actor as an input. The steps on this page show how to do both.

## Steps

To call a Blueprint function when a Variant is activated:

1.  Double-click your **Level Variant Sets** Asset in the **Content Browser** to open it in the Variant Manager UI.
    
    Click image for full size.
    
2.  Select the Variant you want to set up in the left-hand column of the Variant Manager UI.
    
    Click image for full size.
    
3.  If you haven't already bound the Actor whose function you want to call to the Variant, drag it from the **World Outliner** panel into the **Actors** column of the Variant Manager.
    
    Click image for full size.
    
    When the Variant Manager prompts you to select which properties you want to capture, you can leave all the properties unchecked. Click **Select** to continue.
    
4.  Right-click your Actor in the list of bound Actors on the Variant, and select **Add function caller** from the context menu.
    
    Click image for full size.
    
5.  Find the new **Function caller** item at the bottom of the **Properties** column, and use the dropdown list in the **Values** column to choose the function you want to call.
    
    Click image for full size.
    
    Choose **Create New Function** to create a totally new Blueprint function, or choose an existing function from the **Create Quick Binding** list if your Actor is already set up with the function you want to call.
    
6.  The Variant Manager opens a special Blueprint class for you to edit, called the **LevelVariantSetDirector**. This Blueprint is owned by the Level Variant Sets Asset. Its role to store all logic that you need to run in respose to your Variants being activated.
    
    The Variant Manager automatically creates a new function for you in the **LevelVariantSetDirector** Blueprint. Whenever your Variant is activated, the Variant Manager automatically calls this function. If you need to further customize the Blueprint logic that gets triggered when the Variant is activated, you can do it in this graph.
    
    If you chose to create a new function in the previous step, you get a new empty function with a default name. You can fill out this function with any Blueprint logic you need to carry out.
    
    Click image for full size.
    
    The Variant Manager passes your new function some information that you might find useful in creating your Blueprint graph:
    
    | Parameter | Description |
    | --- | --- |
    | **Target** | A reference to the bound Actor that you set up with the Function Caller in the previous step. |
    | **Level Variant Sets** | A reference to the Level Variant Sets Asset that this **LevelVariantSetDirector** Blueprint controls. You can use this to retrieve information about all the other Variants and Variant Sets that you've configured for the same Asset. |
    | **Variant Set** | A reference to the Variant Set that contains the current Variant: that is, the Variant that has just been activated. |
    | **Variant** | A reference to the Variant that has just been activated: that is, the Variant that contains the bound Actor that you set up with the Function Caller. |
    
    If you chose to create a quick binding to an existing function exposed by the Actor, the Variant Manager automatically adds a call to that function and hooks it up to the new function it creates in the **LevelVariantSetDirector** Blueprint. If the function being called on the Actor requires any other input values, such as the **New Actor Enable Collision** option in the image below, you can set them up in this graph.
    
    Click image for full size.
    
    Click image for full size.
    
    By default, the Variant Manager only calls your function when the Variant is activated at runtime. If you want your function to also run when the Variant is switched on in the editor, select your function node in the **LevelVariantSetDirector** Blueprint and enable the **Call in Editor** setting in the **Details** panel.
    
    Click image for full size.
    
7.  When you are done setting up your new function or quick binding in the **LevelVariantSetDirector** Blueprint, **Compile** and **Save** the Blueprint. You can then close the Blueprint Editor and the Variant Manager window.
    

## End Result

Whenever you switch on the Variant that you set up with a function caller at runtime, the Variant Manager automatically invokes the function you defined in the **LevelVariantSetDirector** Blueprint.

If you've enabled the **Call in Editor** option for the function in the **LevelVariantSetDirector** Blueprint, the Variant Manager will also automatically invoke your function when you switch on that Variant in the Unreal Editor.

You can add multiple function callers to a single bound Actor if you need to call multiple functions on that Actor when a Variant is activated.
# Widget Designer (Team)

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/widget-designer-team-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/widget-designer-team-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 17:04:20

---

## Widget Designer (Team)

Widgets are classes that represent individual menus or on-screen elements. You can define them in the Content Browser and build them in UMG, which has both a WYSIWYG (What You See Is What You Get) designer and a Blueprint graph.

### Compiler

| **Section** | **Description** |
| --- | --- |
| **Allow Blueprint Tick** | If disabled, widgets that these compiler options apply to will not be allowed to respond to the **Event Tick** event. |
| **Allow Blueprint Paint** | If disabled, widgets that these compiler options apply to will not be allowed to override the **On Paint** function. |
| **Property Binding Rule** | 
This setting controls whether to let the engine use property bindings in widgets.

Using property bindings can have a large performance impact.

You can choose from the following options:

-   **Allow:** Allows the free use of property binding.
-   **Prevent:** Prevents any new property bindings, but you can still edit widgets with property bindings. The buttons will be missing on all existing widgets that don't have bindings.
-   **Prevent and Warn:** Prevents any new property bindings and gives a warning when the engine compiles any existing binding.
-   **Prevent and Error:** Prevents any new property bindings and gives an error when the engine compiles any existing binding.



 |
| **Rules** | 

Custom widget compiler rule classes that you can write in C++. You can make these by extending the `UWidgetCompilerRule` class, which is in `WidgetCompilerRule.h`. These classes will have an `ExecuteRule` function that runs when you compile a widget blueprint.

You can use this rules list to execute some custom code before the widget is finalized and compiled.



 |
| **Directory Compiler Options** | Allow Blueprint Tick, Allow Blueprint Paint, Property Binding Rule, and custom Rules, which you can set in specific project directories in a selective way. |
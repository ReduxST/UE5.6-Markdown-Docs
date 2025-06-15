# Blueprint Editor Defaults Tab

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-editor-defaults-tab](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-editor-defaults-tab)  
**Processed:** 2025-06-14 16:10:36

---

The **Class Defaults** tab contains information about the Blueprint's default settings and properties, and about any variables the Blueprint contains. You can modify these settings to suit your needs.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6973643d-d3cd-4568-8cfa-2c9b36c7f3be/bp_defaultstab.png)

The **Class Defaults** tab contains the following sections:

| Item | Description |
| --- | --- |
| **Default** | Lists any variables and their values if you do not specify a different category than **Default** when you create them. Note that you must compile the Blueprint in order to display its variables on the **Class Defaults** tab. |
| **Rendering** | Contains information about properties related to how (and whether) an Actor based on the Blueprint is rendered in the game. |
| **Replication** | Contains information about properties that dictate how your Actor behaves in a networked game, such as its network priority and relevancy to other clients. |
| **Input** | Contains information about how Actors based on this Blueprint respond to input. |
| **Actor** | Contains information about Actors based on this Blueprint, such as whether they can be damaged. Note that for Level Blueprints, only the **Tags** properties are relevant in this section. |

If you create custom categories for variables, the **Class Defaults** tab will display those categories too, after the Blueprint is compiled.

## Get Class Defaults

The properties defined inside the Class Defaults can also be accessed at runtime through the use of the **Get Class Defaults** Blueprint node. Targeted use case is for data-only Blueprint Class types and other cases where you may not necessarily need/want to create an instance in order to access default property values.

**To Access the Get Class Defaults Node**

1.  **Right-click** inside your Blueprint Class or Function Graph and enter **GetClassDefaults** from the context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c177ab8-f2da-47bb-9a4e-b948e3672bb2/getclassdefaults.png)
2.  Choose the class to access via the class picker drop-down menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f9ce7d5-751e-4b99-b53a-261e17050ead/selectclass.png)
    
    You can also wire in a class type result from a function call or variable instead as shown in the example below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4ca2c31-af2c-4554-9cd4-8a406effdf31/fromvariable.png)
3.  With the node selected, you can show/hide pins via the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0cf111d4-8dfd-472d-a4a6-20daefa616b3/detailspanel.png)

**Usage Notes**

-   Output pins (accessible class properties) are shown by default and can be optionally hidden (similar to Struct Break/Set Nodes).
    -   Parent class properties are currently hidden by default to reduce the number of output pins.
    -   Properties tagged as *Advanced View* are also hidden by default in the **Advanced** node section.
-   Object reference property default values are **not** currently exposed.
    -   This means you currently cannot, for instance, access the default property values of component templates or other archetypes within a Blueprint Class.
    -   This is because we do not currently enforce read-only reference types in a Blueprint, and we'd need to do that in order to ensure that the internal state of the referenced object cannot be changed.\\
-   Only **BlueprintVisible** or **BlueprintReadOnly** properties are currently exposed for defaults access.
    -   This matches the behavior of "normal" variable Get nodes exposed through the context menu.
-   Currently the *Class* input drop-down lists **all** UOBject-derived class types (including engine classes).
    -   This may be limited in the future to exclude engine-specific class types.
-   Adding a **GetClassDefaults** node to an Actor-based Blueprint class (for example) will currently default the input class pin's value to match the current Blueprint Class type when placed.
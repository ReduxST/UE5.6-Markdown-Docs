# Blueprints Only

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprints-only-example](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprints-only-example)  
**Processed:** 2025-06-14 16:10:58

---

A [Blueprints Class](/documentation/en-us/unreal-engine/blueprint-class-assets-in-unreal-engine) allows you to set up new classes using the [Blueprints Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) system. After you [create a new Blueprint Class](/documentation/en-us/unreal-engine/creating-blueprint-classes-in-unreal-engine), you can add components, set up functions and other gameplay or design behavior with visual scripting, and set default values for class variables. The LightSwitch class set up using only Blueprints is named **LightSwitch\_BPOnly**, and is explained below.

## Class Setup

The LightSwitch\_BPOnly class was created in the **Content Browser**, and **Actor** was selected as the parent class.

Components are added to the Blueprint either statically in the **Blueprint Editor**'s [Components](/documentation/en-us/unreal-engine/components-window-in-unreal-engine) tab, or dynamically through visual scripting in the [Graph Editor](/documentation/en-us/unreal-engine/graph-editor-for-the-blueprints-visual-scripting-editor-in-unreal-engine). Because the LightSwitch class will always have the PointLightComponent and the SphereComponent, in this case the components have been added statically in **Components** tab.

The **Components** tab was used to add the PointLightComponent, named PointLight1, as the root component, and the SphereComponent, named Sphere1, attached to the PointLightComponent. Components added to the class in the **Blueprint Editor** have light blue icons, while components inherited from the parent class have dark blue icons.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b96bd5db-4767-4745-b14d-1c5e3cf39b6f/bp_only_componentlist.png)

In the **Blueprint Editor**, you can add new [variables](/documentation/en-us/unreal-engine/blueprint-variables-in-unreal-engine), [functions](/documentation/en-us/unreal-engine/functions-in-unreal-engine), and [macros](/documentation/en-us/unreal-engine/macros-in-unreal-engine) in the [Blueprint Editor My Blueprint Panel](/documentation/en-us/unreal-engine/my-blueprint-panel-in-the-blueprints-visual-scripting-editor-for-unreal-engine) tab. You also have access to all the [graphs](/documentation/en-us/unreal-engine/graphs-in-unreal-engine) contained within the Blueprint Class. In graphs, [nodes](/documentation/en-us/unreal-engine/nodes-in-unreal-engine) are wired together to create design-time and gameplay functionality that can be driven by class variables, gameplay events, and even an Actor's surroundings.

The float variable **DesiredIntensity** was added to the LightSwitch\_BPOnly class using the **My Blueprint** tab. The **My Blueprint** tab also displays the components added in **Components Window**, so they can be accessed in graphs if desired.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72a0f620-20f7-4f48-b34c-7d5122b66c0c/bp_only_myblueprint.png)

There are two graphs used to set up the LightSwitch\_BPOnly class behavior. The first is the [Construction Script](/documentation/en-us/unreal-engine/construction-script-in-unreal-engine) function graph, which contains the **Construction Script** function entry node. This event executes when an Actor is added to the level, or when an existing Actor is moved within the level. In the LightSwitch\_BPOnly class, the **Construction Script** event is connected to a **Set Intensity** node, so that the intensity of **Point Light 1** (the PointLightComponent) is set to the value of **DesiredIntensity** when the Actor is added to or moved within the level.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f983417a-949a-4b8c-a5a2-34c8c904d054/bp_only_constructionscript.png)

The other graph set up in the LightSwitch\_BPOnly class is the [EventGraph](/documentation/en-us/unreal-engine/event-graph-in-unreal-engine). Execution in the EventGraph begins from events, such as the **OnComponentBeginOverlap** and **OnComponentEndOverlap** events. These events execute when some other Actor within the level overlaps or leaves the SphereComponent. Both events are connected to the **Toggle Visibility** node, so the visibility of the PointLightComponent is toggled when those events execute. For more on events and working with graphs, see the [Events](/documentation/en-us/unreal-engine/events-in-unreal-engine), [EventGraph](/documentation/en-us/unreal-engine/event-graph-in-unreal-engine), and [Graph Editor](/documentation/en-us/unreal-engine/graph-editor-for-the-blueprints-visual-scripting-editor-in-unreal-engine) documentation.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa4ed11b-5fe0-41ac-bdc2-9b823c18a76f/bp_only_eventgraph.png)

If you cannot find the Toggle Visibility from **Right-click** menu un-check context sensitive or try searching for it in the Find a Node Menu. You can also get the same results by simply dragging out a line from the Point light variable node and then searching for Toggle Visibility.

If you cannot find the OnComponentEndOverlap for Sphere1 make sure that you have the Sphere variable selected and then use the add event from the Event->Add Event or from the **Right-click** menu Add Event->Collision->View **OnComponentBeginOverlap / OnComponentEndOverlap**.

The **DesiredIntensity** variable is set to **Editable** in the variable's settings, so it is visible in the **Blueprint Editor**'s **Class Defaults** and can be edited. This also means that the variable can be changed for each instance of the class, so each Actor can have its own **DesiredIntensity**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9fae146-3c71-417e-967f-046c7adcc8cc/bp_only_defaults.png)

Blueprinted classes can be extended with other Blueprint Classes, either using the dropdown button next to the class in the **Class Viewer** to create a new Blueprint, or by **Right-clicking** on the Blueprint and selecting **Create New Blueprint Based on This**.

The Blueprint Class LightSwitch\_BPOnly is in the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine), and can be dragged into the level from there. It is also in the [Class Viewer](/documentation/en-us/unreal-engine/class-viewer-in-unreal-engine). For more information on placing Actors in a level using the **Content Browser** or **Class Viewer**, see the [Placing Actors](/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine) documentation.
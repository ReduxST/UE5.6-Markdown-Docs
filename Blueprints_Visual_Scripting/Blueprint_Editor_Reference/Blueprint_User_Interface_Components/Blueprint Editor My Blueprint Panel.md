# Blueprint Editor My Blueprint Panel

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/my-blueprint-panel-in-the-blueprints-visual-scripting-editor-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/my-blueprint-panel-in-the-blueprints-visual-scripting-editor-for-unreal-engine)  
**Processed:** 2025-06-14 16:37:59

---

The **My Blueprint** tab displays a tree list of the graphs, scripts, functions, macros, etc. contained within the Blueprint. This is essentially an outline of the Blueprint that lets you easily view existing elements of the Blueprint, as well as create new ones.

Different types of Blueprints will have different types of items shown in the **My Blueprint** tab tree list.

![My Blueprint Pane](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/671e9734-93a1-4af0-9e47-fd06ffdb9cb0/myblueprintpane.png)

For example, a normal Blueprint will always have a **ConstructionScript** and an **EventGraph**. In addition, any functions created within the Blueprint will be displayed. A Level Blueprint will only have an **EventGraph** and any functions created within it. An Interface will only display the functions created within it. A Macro Blueprint will display the macro functions created within it.

## Creation Buttons

The **My Blueprint** tab has shortcut buttons (the ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41e3428e-8be3-4444-8b21-a7808b4e5760/plus_button.png) at the end of each heading) for creating new variables, functions, macros, event graphs, and event dispatchers.

| **Button** | **Name** | **Description** |
| --- | --- | --- |
| ![New Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23631b5d-0179-4c6d-8456-ea62d5ee9355/myblueprint_variable.png) | **New Variable** | Creates a new variable when clicked. The properties of that variable immediately appear in the **Details** tab. There, you can change the name, type, and other properties. |
| ![New Function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a809429-6a30-4aa4-aadf-5b4ddb480b2f/myblueprint_function.png) | **New Function** | Creates a new function, then immediately puts focus on the Name field of the **Details** tab so that it can be named. A new graph view will also be opened where you can define the node network for the function. |
| ![New Macro](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbbe9a3c-c076-451e-bc48-3c9068718a04/myblueprint_macro.png) | **New Macro** | Creates a new macro, then immediately puts focus on the Name field of the **Details** tab so that it can be named. A new graph view will also be opened where you can define the node network for the macro. |
| ![New Event Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eaf61ccd-b8d1-4e98-9d05-d48cc0a1fe0b/myblueprint_eventgraph.png) | **New Event Graph** | Creates a new function, then immediately puts focus on the Name field of the **Details** tab so that it can be named. The new graph appears and is ready to have a node network defined within it. |
| ![New Event Dispatcher](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37c79b68-acb7-47be-a71d-8e19d4523e9b/myblueprint_eventdispatcher.png) | **New Event Dispatcher** | Creates a new event dispatcher, then immediately puts focus on the Name field of the **Details** tab so that it can be named. |

These same buttons can also be accessed by **Right-clicking** in the **My Blueprint** tab. The **Right-click** menu also includes an option for creating a new enum asset.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93c1e737-7141-42a7-909c-e552f48c7b4f/myblueprint_rightclick.png)

Finally, you can use the **Add New** button at the top of the **My Blueprint** Panel

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03ce2368-df24-48d3-8ed7-12ca87e16e46/addnew.png)

## My Blueprint Sections

The **My Blueprint** tab is divided up into 6 sections: The **Add New**, Graphs, Functions, Macros, Variables, and Event Dispatchers sections.

![My Blueprint Pane](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3570ecfe-1ea7-425a-8f17-e080307c1e73/myblueprintpane.png)

The 5 lower sections will organize elements of your Blueprint into their respective groups. While the top section gives you quick access to create new Graphs, Variables, etc... and search the entire **My Blueprint** panel.

## Searching in My Blueprint

The **My Blueprint** tab contains a text box used for searching the graphs belonging to the Blueprint. This works the same way as the contextual action menu that you use for adding new nodes, but is limited to searching items found within **My Blueprint**. You can search based on name, comment, and other data. So, if you know you have a node that is **SetActorHidden**, you can type that in the box, and the explorer will show you all the **SetActorHidden** nodes in your graph.
# Level Blueprint

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/level-blueprint-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/level-blueprint-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:57

---

A **Level Blueprint** is a specialized type of **Blueprint** that acts as a level-wide global event graph. Each level in your project has its own Level Blueprint created by default that can be edited within the Unreal Editor, however new Level Blueprints cannot be created through the editor interface.

Events pertaining to the level as a whole, or specific instances of Actors within the level, are used to fire off sequences of actions in the form of Function Calls or Flow Control operations. Those familiar with Unreal Engine 3 should be very familiar with this concept as this is very similar to how Kismet worked in Unreal Engine 3.

Level Blueprints also provide a control mechanism for level streaming and [Sequencer](/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine) as well as for binding events to Actors placed within the level.

For more information about the Level Blueprint UI, see [Blueprint Editor Level Blueprint UI](/documentation/en-us/unreal-engine/blueprints-visual-scripting-editor-user-interface-for-level-blueprints-in-unreal-engine).

## Default Level Blueprint

Each game can specify the default Level Blueprint class in the DefaultGame.ini config file. The Level Blueprints for all new maps will be created using this class allowing for game-specific additions and functionality.

## Opening a Level Blueprint

To open a Level Blueprint for editing, click the **Blueprints** button in the **Level Editor Toolbar** and select **Open Level Blueprint**.

![Level Blueprint Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05a4e608-e086-44fd-a6ce-12d048f6e94b/toolbar_level_editor.png)

This opens the Level Blueprint in the **Blueprint Editor**:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/612ebe5e-2932-4ad6-9394-71ab613e32a7/level_blueprint_editor.png)

The **Blueprint Editor** only uses [Graph Editor](/documentation/en-us/unreal-engine/graph-editor-for-the-blueprints-visual-scripting-editor-in-unreal-engine), **My Blueprints** panel, and **Details** panel. The **Class Defaults** panel using the **Class Defaults** ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d985b97-2934-4abe-b60d-721ca9fee647/classdefaults_button.png) button on the menu bar.

## Referencing Actors

Often, you will need to connect a reference to an Actor to a **Target** pin on a node in your Level Blueprint. To get a node that contains an Actor reference:

1.  Select the Actor in the **Level Viewport** or in the **World Outliner**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/374f083a-c258-495a-bfa1-fe2ba114e4fd/selected_actor.png)
2.  Open the Level Blueprint.
    
    ![Level Blueprint Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b2471e5-d6bd-4020-95d8-cb7026815c80/toolbar_level_editor.png)
3.  Right-click in the graph where you would like to add the node.
4.  Select **Create a reference to \[SelectedActor\]** in the context menu that appears.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a473e9da-ceb8-49d5-b301-dc66dfcb7e2e/add_reference_to.png)

Alternatively:

1.  Drag and drop an Actor from the **World Outliner** tab into a graph in the Level Blueprint.
    
    Click image for full view.
    

The Actor reference node that appears can be connected to any compatible **Target** pin.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aad104b4-0d48-43e4-8456-942252e75d75/actor_reference.png)

In some cases, you will not need a reference node, as you can connect an output pin with the correct type to the **Target** input pin.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f185b0d8-fc6d-43bd-876a-5c6251bb6a5b/target_pin_noref.png)

## Adding Events

There are two ways that [Events](/documentation/en-us/unreal-engine/events-in-unreal-engine) for a specific Actor can be added to a Level Blueprint.

1.  Right-click an Actor in the Level, then in the context menu under **Level Blueprint**, select the Event you wish to add.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef5cf5c6-f7e6-4de3-bb07-2c080b75bbe8/add_event_details_tab.png)

Alternatively, once you have your Actor selected:

1.  Open the Level Blueprint.
    
    ![Level Blueprint Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f140563-45d4-4b82-925a-e123d2bc4f55/toolbar_level_editor.png)
2.  Right-click in the graph where you would like to add the node.
    
3.  In the context menu that appears, expand **Add Event for \[ActorName\]** and select your desired Event type.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/496dbe2f-bb5d-4cf5-a5b3-5e5a6b325a43/add_event_for_actor.png)
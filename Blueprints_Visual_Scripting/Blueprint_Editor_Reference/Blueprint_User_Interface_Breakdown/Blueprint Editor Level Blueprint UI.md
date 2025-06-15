# Blueprint Editor Level Blueprint UI

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprints-visual-scripting-editor-user-interface-for-level-blueprints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprints-visual-scripting-editor-user-interface-for-level-blueprints-in-unreal-engine)  
**Processed:** 2025-06-14 16:11:02

---

A **Level Blueprint** is a specialized type of **Blueprint** that acts as a level-wide global event graph. Each level in your project has its own Level Blueprint created by default that can be edited within the Unreal Editor, however new Level Blueprints cannot be created through the editor interface.

Events pertaining to the level as a whole, or specific instances of Actors within the level, are used to fire off sequences of actions in the form of Function Calls or Flow Control operations. Those familiar with Unreal Engine 3 should be very familiar with this concept as this is very similar to how Kismet worked in Unreal Engine 3.

Level Blueprints also provide a control mechanism for level streaming and [Sequencer](/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine) as well as for binding events to Actors placed within the level.

## Interface

The Blueprint Editor contains the following sections when editing Level Blueprints:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05ab4748-e1b1-4497-8e5b-e4a42feb8528/levelblueprintui.png)

| Default Visible UI Components | Available in the Window Menu |
| --- | --- |
| 
1.  [Menu](/documentation/en-us/unreal-engine/menu-for-the-blueprints-visual-scripting-editor-in-unreal-engine)
2.  [Toolbar](/documentation/en-us/unreal-engine/toolbar-in-the-blueprints-visual-scripting-editor-for-unreal-engine)
3.  [My Blueprint](/documentation/en-us/unreal-engine/my-blueprint-panel-in-the-blueprints-visual-scripting-editor-for-unreal-engine)
4.  [Details](/documentation/en-us/unreal-engine/details-panel-in-the-blueprints-visual-scriting-editor-for-unreal-engine)
5.  [Graph Editor](/documentation/en-us/unreal-engine/graph-editor-for-the-blueprints-visual-scripting-editor-in-unreal-engine)



 | 

-   [Compiler Results](/documentation/en-us/unreal-engine/compiler-results-in-the-blueprints-visual-scripting-editor-for-unreal-engine)
-   [Debug](/documentation/en-us/unreal-engine/debug-panel-in-the-blueprints-visual-scripting-editor-for-unreal-engine)
-   [Find Results](/documentation/en-us/unreal-engine/find-result-panel-in-the-blueprints-visual-scripting-editor-for-unreal-engine)
-   [Palette](/documentation/en-us/unreal-engine/palette-in-the-bleprints-visual-scripting-editor-for-unreal-engine)
-   [Viewport](/documentation/en-us/unreal-engine/components-mode-viewport-in-the-blueprints-visual-scripting-editor-for-unreal-engine)



 |
# Widget Components

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/widget-components-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/widget-components-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:18

---

Widget Components allow you to manifest 3D UI elements created through [Unreal Motion Graphics](/documentation/en-us/unreal-engine/specialized-blueprint-visual-scripting-node-groups-in-unreal-engine) in your game world. The **Widget** Component itself is a 3D instance of a Widget Blueprint that you can interact with in your game world. Once you place the Actor that contains the WidgetComponent in your level, the Widget Class Blueprint is displayed in the world.

![Add the Widget Component to the Actor Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec495227-97a2-412b-b483-4cbedf296837/ue5_1-add-widget-component.png "Add the Widget Component to the Actor Blueprint")

## Widget Component Property Reference

Here are the properties that can be adjusted via the **Details** panel for the Widget Component.

| Option | Description |
| --- | --- |
| **Space** | The coordinate space in which to render the widget (World or Screen). With World the widget is rendered in the world as a mesh while and can be occluded while Screen renders the widget on the screen completely outside of the world and is never occluded. |
| **Widget Class** | The class of User Widget to create and display an instance of. |
| **Draw Size** | The size of the displayed quad. |
| **Manually Redraw** | Should the Widget wait to be told to redraw to actually draw or not. |
| **Redraw Time** | The time in between draws, if 0 - redraw every frame. If 1, we would redraw every second. This will work with the Manually Redraw as well. So you can say, manually redraw, but only redraw at this maximum rate. |
| **Window Focusable** | Is the virtual window created to host the widget focusable? Should this take focus from the user. |
| **Draw at Desired Size** | Causes the render target to automatically match the desired size specified by the Widget Class. Expensive if is done every frame. |
| **Pivot** | The Alignment/Pivot point that the widget is placed at relative to the position. |
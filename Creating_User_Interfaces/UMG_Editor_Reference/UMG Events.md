# UMG Events

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-events-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-events-in-unreal-engine)  
**Processed:** 2025-06-14 16:55:30

---

This page details the methods you can use to call and bind **Events** in UMG.

### Bindable Events

**Bindable Events** are a way for UMG to mimic the behavior currently used by Slate which needs a single handler to tell it if the Event was handled. You can bind a function in your **Widget Blueprint** to the event from the **Details** panel under the **Events** section (shown below indicated by the yellow arrows).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4977bc39-ccf7-442c-863b-7564133c24a4/eventbinding.png)

Indicated above by the yellow box, some Widgets supplement **Events** through the handling of **Interaction**. For the example above, in addition to the **OnClicked** Event for a Button Widget, you are able to specify the handling of click events through setting the **Click Method** or **Touch Method**. You can also specify through the **IsFocusable** option if a button should only be mouse-clickable and never keyboard focusable.

### Multicast Events

**Multicast Events** are the standard way Events are handled in **Blueprints**.

To use a Multicast Event:

1.  click the **Widget** in the **My Blueprint** tab (1).
    
2.  Scroll down to the **Events** section in the **Details** panel, then click the **+** button for the Event you want to use (2).
    
3.  The Event appears in the Blueprint graph, where you can connect other nodes to it (3).
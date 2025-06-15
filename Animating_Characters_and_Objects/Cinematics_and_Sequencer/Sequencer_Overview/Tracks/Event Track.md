# Event Track

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:07

---

In Sequencer, you can define frames in your sequence where you want to execute [Blueprint Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) functionality. This is accomplished using the **Event Track**.

This guide provides an overview of the Event Track, including how to create it, access the Director Blueprint, and the types of events you can create.

#### Prerequisites

-   You have an understanding of [Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine), and its [Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine).
-   You have an understanding of [Blueprints Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine).

## Creation

To create an Event Track, click **Add Track (+)** in Sequencer, navigate to **Event Track**, and select either the [Trigger](/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine#triggerevents) or [Repeater](/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine#repeaterevents) event type.

![create event track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0258fa8a-56ed-43ad-9582-4f2c56407e33/createevent1.png)

Event Tracks can also be created under an [Object Binding Track](/documentation/en-us/unreal-engine/cinematic-actor-tracks-in-unreal-engine), which will [bind the event to that object](/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine#objectbinding).

![create event track actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36d73258-3f1e-4753-81fd-a93455a87b4c/createevent2.png)

Once an Event Track is created, you can create additional event [Sections](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#sections) by clicking **Add Section (+)** on the Event Track and selecting an event type.

![add more event tracks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/197fde22-e49a-4e88-b8ae-19e74859571b/createevent3.png)

When adding events, you can choose to add either **Trigger** or **Repeater** type events. Trigger Events cause an event to evaluate on the same frame as the keyframe, whereas Repeater Events will evaluate for each frame for the duration of the event section.

### Trigger Events

Trigger events are events that evaluate once per keyframe. When this track is created, you can then **[Keyframe](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine)** it to create event keyframes.

![trigger event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/047574c9-34b0-404e-8b6b-104142405486/trigger1.png)

### Repeater Events

Repeater events are events that will fire or evaluate for each frame of the sequence continuously for the duration of the event section. Adjusting the [Frames Per Second](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#framespersecond) of the sequence will also adjust the evaluation rate of the repeater to match. When this track is created, it will contain a finite [Section](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#sections) range, controlling its evaluation time.

![repeater event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61552c43-1458-4d1a-b23b-06c0ffe1ae03/repeater.png)

You can [edit, move, and trim](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#interactionanddisplay) this event section just like any other section in Sequencer.

## Director Blueprint

The Director Blueprint is the logic center for the Event Track from which you will perform [Blueprint Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) from your event endpoints. **Parameters** and **Object Bindings** can also be specified in the Blueprint in order to pass variable and object information throughout the script. Each **Level Sequence** has its own Director Blueprint, containing all the logic for the events in that sequence.

There are several ways you can open the Director Blueprint:

1.  Double clicking an event keyframe or section. This method will also bind the event to a new [**endpoint**](/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine#eventendpoint) if it is currently unbound.
    
    ![double click event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39419881-7700-4366-bcf5-86ea88eaff61/directorbp1.gif)
    
2.  Clicking the [Director Blueprint Toolbar button](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#directorblueprint).
    
    ![director blueprint toolbar button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ed1af54-8eaf-4330-809a-5079b6e095b6/opendp2.png)
    
3.  Clicking the [Actions Toolbar button](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#actions) and then selecting **Open Director Blueprint**.
    
    ![open director blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2c66314-be22-45c9-8068-d3e7e06c2ce4/opendp.png)
    

### Event Endpoint

Regardless of whether a Trigger or Repeater event is created, you must bind it to an **Event Endpoint** in order to add logic to it. To do this, right-click the keyframe (if using trigger) or section (if using repeater) and select **Properties > Unbound > Create New Endpoint**. Doing this will bind the event keyframe or section to a new endpoint node and open the **Director Blueprint**.

![create new endpoint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abd8a5d9-e29d-45c1-a5be-a8a50bddb83b/bind1.png)

The Event Endpoint can be renamed in the Blueprint's Details panel from the **Name** property.

![rename event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e52a742d-31e7-4676-9d02-e0d32d1fd95c/rename.png)

You can create as many event keyframes or sections as you need. Event nodes can also be shared between multiple event sources by using the **Quick Bind** or **Rebind To** menus.

![event track link](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f44da817-b452-459e-8569-0e7f5f75a179/eventlink.png)

### Parameters and Event Payloads

Similar to Blueprint [Custom Events](/documentation/en-us/unreal-engine/custom-events-in-unreal-engine), the Event Track can have input parameters associated with it. Using event parameters and payloads, you can send property values to targets when the event fires.

To add a parameter to your event, select the event endpoint and click **Add Parameter (+)** in the Details panel. Doing this will create a new parameter in the details and on the node for scripting

![event track parameter property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/726419ef-e067-4387-8b99-5dde7337dd21/newparam.png)

When you right-click the event keyframe or section, additional properties for your parameters will be displayed under the **Payload** category. Here you can define the values on the parameters, which will be sent when the event executes.

![payload](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be30b64b-f4ef-4f7e-9e8b-28d78bc41e56/payload.png)

### Object Binding

When creating an Event Track under a bound object in Sequencer, it will create an **Object Binding** for the Event Track where the target object of the event node becomes bound to the object the Event Track has been added to. This makes it easier to script functions on specific Actors in your sequence, as functions can now be called on the object directly.

![event track actor binding](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2f81992-8c57-453a-9503-e8ca83168a81/binding1.png)

An additional property will also be exposed on the keyframe or section properties context menu. **Pass Bound Object To** controls which object parameter this event should be bound to. If you have added additional **Object** or [Blueprint Interface](/documentation/en-us/unreal-engine/blueprint-interface-in-unreal-engine) parameters to your endpoint node, then they will be selectable here.

![pass bound object to](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d8ff94f-47e1-4e82-aecd-0b67087f06ea/binding2.png)

If an endpoint node is not yet designated for your object bound event, you can use the **Quick Bind** command to add script functions directly related to the bound object, similar to calling functions from an object reference in Blueprints.

![quick bind event actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9808c533-2065-499c-8efe-0c5e1a243ef2/binding3.png)

## Event Properties

When right-clicking either a Trigger keyframe or Repeater section, you can view the following properties in the **Properties** context menu.

![event properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66b592af-1557-407a-bedf-afe4772e8a7e/eventproperties.png)

| Name | Description |
| --- | --- |
| **Event** | 
The **Event Endpoint** this keyframe or section is bound to in the [Director Blueprint](/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine#directorblueprint).

By default this is unbound and can be bound by clicking the dropdown menu and selecting **Create New Endpoint** or any other existing endpoint node.

![unbound create new endpoint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fed1d0b-ba03-47e0-816d-096d329011a2/newendpoint.png)

**Quick Bind** contains a list of compatible functions for this event, including the object binding if the Event Track is bound to an object.

![quick bind](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0536c192-591d-482a-a1c6-8a5690d5e938/quickbind.png)

 |
| **Call In Editor** | Enabling this will cause the event logic to evaluate in the editor session without requiring you to [Play or Simulate in Editor](/documentation/en-us/unreal-engine/in-editor-testing-play-and-simulate-in-unreal-engine). This property appears once the event is bound to an endpoint node. |

You can also right-click the Event Track to view the following properties in the **Properties** context menu.

![event track properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82a0bd1c-65b5-47ab-9e7f-0c552770403c/eventproperties2.png)

| Name | Description |
| --- | --- |
| Fire Event when Forwards | Enabling this will cause the Event to fire when the sequence is playing forward normally. |
| Fire Event when Backwards | 
Enabling this will cause the Event to fire when the sequence is playing in reverse.

Using the **Forwards** and **Backwards** properties can be useful if you need to reset an event chain back to normal when previewing your sequence multiple times. You can set one Event Track to fire forward only and another to fire backward only. Afterward, you can hook up the forward event to the normal event chain, and the backward event to the reset chain.



 |
| Event Position | 

Defines where in the evaluation the event should trigger.

-   **At Start Of Evaluation** will cause the event to fire first, before anything else is evaluated in the sequence.
-   **At End Of Evaluation** will cause the event to fire last, after everything else has been evaluated in the sequence.
-   **After Spawn** will cause the event to fire after [Spawnables](/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics) have spawned and evaluated.



 |
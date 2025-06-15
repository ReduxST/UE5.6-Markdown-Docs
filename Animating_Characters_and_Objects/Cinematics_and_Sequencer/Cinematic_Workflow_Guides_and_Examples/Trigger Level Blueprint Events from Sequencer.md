# Trigger Level Blueprint Events from Sequencer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/trigger-level-blueprint-events-from-sequencer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/trigger-level-blueprint-events-from-sequencer-in-unreal-engine)  
**Processed:** 2025-06-14 16:55:01

---

[Event Tracks](/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine) are mainly used to trigger [Blueprint Scripts](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) within Sequencer's **Director Blueprint**. In your project, there may be cases where you instead want events from Sequencer to trigger in other Blueprints, such as the **Level Blueprint**. You can do this using [Blueprint Interfaces](/documentation/en-us/unreal-engine/blueprint-interface-in-unreal-engine) and additional set-up steps in the Director Blueprint.

This document provides instructions on how to trigger Level Blueprint events from Sequencer's Event Track.

#### Prerequisites

-   You have a basic understanding of how to create and open a [Level Sequence](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview).
-   You have an understanding of how to create and use the [Event Track](/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine).
-   You have a basic understanding of [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine).

## Create Blueprint Interface

First, create a Blueprint Interface. In the **Content Browser**, click **Add (+)** and select **Blueprints > Blueprint Interface**. Name your asset and open it.

![create blueprint interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16bc6715-55e0-4210-ba14-b8caecf60e01/createbpi1.png)

In the **Blueprint Interface Editor**, give a unique name to the default Function, to help you locate it later in this guide.

![name blueprint interface function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12336119-2de3-452c-859e-bea6b6908679/createbpi2.png)

The purpose of the Blueprint Interface is to provide communication between the Sequencer Director Blueprint and the Level Blueprint.

## Implement the Interface in your Level

Next, open your Level Blueprint by clicking **Level Blueprint** in the **Level Toolbar** and selecting **Open Level Blueprint**.

![open level blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24649ab9-0fc1-4ccf-8103-3980229cadce/level1.png)

Enable **Class Settings**, and in the **Details** panel click the **Add** dropdown menu for **Inherited Interfaces**. Locate and select your Blueprint Interface to add it to the Level Blueprint.

![implement blueprint interface in level blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13d061aa-72aa-4077-ac71-853e305e5ac4/level2.png)

Right-click in the **Event Graph** and add the **Event** from your Blueprint Interface. The event name matches the name of the Function you named earlier in this guide. Add the Event and connect it to the Level Blueprint logic you want to trigger. Due to the arbitrary nature of Blueprints, this guide will assume your Level Blueprint logic is already created. In this example, the logic is activating a [Niagara System](/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine).

![reference blueprint interface event in level blueprint logic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a92dd068-17f0-4b88-90b2-50241377f10c/level3.png)

## Set Up Event Track

Now that the Level Blueprint side of the logic is set up, you can implement the rest of the logic in Sequencer's Event Track.

Open your **Level Sequence**, then create an **Event Track** by clicking **Add Track (+) > Event Track > Trigger**.

![create event track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e7555df-cc98-4e81-a5b9-30851a123a57/eventtrack1.png)

Select the **Event Track** and press **Enter** to create an **Event keyframe** at the Playhead. Double-click this keyframe to open the **Director Blueprint** and bind the keyframe to a new **Event**.

![create event keyframe](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a3e74bc-0afd-496d-863a-0d385057126c/eventtrack2.gif)

### Implement Interface

Like you did in the Level Blueprint earlier, enable **Class Settings** in the **Director Blueprint**, and in the **Details** panel click the **Add** dropdown menu for **Inherited Interfaces**. Locate and select your **Blueprint Interface** to add it to the Level Blueprint.

![implement blueprint interface in director blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9500ee1-b84b-4cbf-a920-2e4db410d5cd/level2.png)

### Create Logic

Right-click in the **Director Blueprint Graph** and add the **Function** from your Blueprint Interface under the **Call Function** category. The Function name matches the name of the Function you named earlier in this guide.

![reference blueprint interface function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ad42057-8845-4f08-b7e4-664d9a778be5/eventtrack3.png)

Make sure you are using the Blueprint Interface Function that targets your Sequence Director BP. Other function targets will not work.

![ensure function targets sequence director](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3628b164-6c34-4191-9785-854de7638dfe/eventtrack4.png)

Connect the **execution** and **target** pins to the **Event**.

![connect function to event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88772997-8171-48b1-930d-8c3574c8f6d4/eventtrack5.gif)

### Bind Keyframe to Target

Lastly, return to the **Event Track** and right-click the **keyframe**. Under the **Properties** menu, set **Pass Bound Object To** to **Target**.

![set pass bound object to target](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73bfac59-cfc0-4379-a370-48bf1ea750fb/eventtrack6.png)

Connecting and binding the **Target** is a necessary step, despite there being no actual target. This is because when no target is specified, the Blueprint Interface system will fallback to the Level Blueprint, and then correctly link to the interface there.

## Results

Once the preceding steps are finished, you can now play or simulate your level. Upon playing your sequence, the level event should trigger.

![sequencer event triggers level event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/766942e5-22c4-4db7-8469-0fa77b0f6fb5/final.gif)
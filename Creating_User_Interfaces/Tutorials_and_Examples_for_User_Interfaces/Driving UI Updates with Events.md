# Driving UI Updates with Events

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/driving-ui-updates-with-events-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/driving-ui-updates-with-events-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:18

---

When crafting your UI elements, it's best practice to think of ways you can optimize your content to increase performance and minimize inefficiencies. For example, based on the scope of your project, [Property Binding](/documentation/en-us/unreal-engine/property-binding-for-umg-in-unreal-engine) may be fine for communicating information to your UI. However, if you have a more complex UI setup, or need to optimize your project, you may want to consider updating your UI on a need-to-know basis.

In this reference guide, we will examine three ways of communicating information to a HUD. While all three approaches accomplish the task, the third example presents the most cost effective way by moving the update process away from tick events, and instead manually updates information through the use of [Event Dispatchers](/documentation/en-us/unreal-engine/event-dispatchers-in-unreal-engine).

## Example 1. Function Binding

For this example, we will take a look at updating Health/Energy for a player using **Function Binding**.

Here we have a basic Health/Energy setup.

![Hierarchy structure of the HUD widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/223372f0-76b1-43ba-bb38-0e0d173f3571/ue5_1-01-hierarchy.png "Hierarchy structure of the HUD widget")

With display in place, we **Create Bindings** for our progress bars called **GetHealth** and **GetEnergy**. The function bindings cast to the Player Character Blueprint and assign the variables we defined for Health and Energy.

Below is the binding for GetHealth. For debugging purposes, we also added a **Print String** node to print to the screen the value of our Health variable.

Click image for full view.

In the image below, you can see the Health and Energy values from the player character that are passed through and reflected in the HUD. However, you can also see that even when we are not updating the Health Value, the blue debug text illustrates that we are still checking the Health Value every frame.

![Gameplay Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f5d200d-f267-46f4-8076-84d97619b925/ue5_1-03-gameplay-example.png)

Essentially, this approach is asking "What is the player character blueprint? And when I know what it is, "give me the values for health and energy" each frame. For smaller, less complex systems, this approach works well; however, if you are using a more complex system with multiple properties checking for updates every frame, this setup can lead to poor performance.

## Example 2. Property Binding

The second approach is **Property Binding**, which is a bit more cost effective than Function Binding.

Using the same Health/Energy setup, let's examine how Property Bindings work.

![Hierarchy structure of the HUD widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6d1b955-f9c6-424b-9dc6-0aac210d39ed/ue5_1-01-hierarchy.png "Hierarchy structure of the HUD widget")

In the **Event Graph** of our [Widget Blueprint](/documentation/en-us/unreal-engine/widget-blueprints-in-umg-for-unreal-engine), we use the **Event Construct** to get a reference to the Player Character Blueprint.

By using Event Construct, we are casting to the Character Blueprint once and storing the information as a reference so the script does not have to call that information every frame.

![BP script of the HUD Widget Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f27e0414-f391-4b91-8f5c-c14612f945a8/ue5_1-04-hud-widget-bp-script-1.png "BP script of the HUD Widget Blueprint")

Then, we can bind the values for the progress bars directly to the variables inside the Character Blueprint.

![Set bind for percent value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9166ab9-7be8-47c4-8684-c6379c7d42f3/ue5_1-05-set-percent-bind.png "Set bind for percent value")

With this approach, we are no longer casting every frame and checking "what is the player character blueprint?" Instead, we are only querying the values for health and energy each frame.

Based on the scope of your project, this is approach can be efficient; however, if your system is more complex, then an Event Driven approach may be better.

## Example 3. Event Driven

Here we take a look at using Events to update the HUD only when it changes, and we will continue with the same Health/Energy setup.

![Hierarchy structure of the HUD widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8e30643-e600-4819-b46e-5ebbc0b9a067/ue5_1-01-hierarchy.png "Hierarchy structure of the HUD widget")

Inside the Character Blueprint, add an **Event Dispatcher** node to the end of the script that decrements our Health. In this example, the Event Dispatcher node is **Call Update Health**.

For testing purposes, Health is set to decrease whenever the **F** key is pressed.

![BP Script for causing damage of the Character](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c900d09c-b450-436d-b0db-98f3c50ae7f6/ue5_1-06-set-causing-damage.png "BP Script for causing damage of the Character")

Now, whenever we decrease our Health, we also call this Event Dispatcher. In the Event Graph of the HUD Widget Blueprint, we can use the Event Construct again to get and store a reference to the Player Character Blueprint. We can also Bind a Custom Event to the Event Dispatcher inside that Character Blueprint so that the Custom Event is called when the Event Dispatcher is called.

Click image for full view.

The Custom Event inside the HUD Widget Blueprint now only checks and updates the display of player's Health when it changes, rather than always checking the value regardless of whether or not it changed.

The image below shows how you can incorporate Health and Energy into the same Event Construct script.

The Custom Events **UpdateHealth** and **UpdateEnergy** are bound to Event Dispatchers from the Character Blueprint, which are only called when the character's Health/Energy value changes. We can also initialize the display by calling those two Custom Events when the HUD is constructed following the binding process.

Click image for full view.
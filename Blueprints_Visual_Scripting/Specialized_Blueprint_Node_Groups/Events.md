# Events

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/events-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/events-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:41

---

**Events** are nodes that are called from gameplay code to begin execution of an individual network within the **EventGraph**. They enable Blueprints to perform a series of actions in response to certain events that occur within the game, such as when the game starts, when a level resets, or when a player takes damage.

Events can be accessed within Blueprints to implement new functionality or to override or augment the default functionality. Any number of **Events** can be used within a single **EventGraph**; though only one of each type may be used.

An event can only execute a single object. If you want to trigger multiple actions from one event, you will need to string them together linearly.

![Blueprint Class Events Expanded](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32f026d3-36b4-4f37-bc35-9fe82d87bce6/eventsexpanded.png) ![Level Blueprint Events Expanded](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8824642f-87ed-453b-b799-f881cdcf17a7/levelbpeventsexpanded.png)

## Event Level Reset

This Blueprint Event node is only available in the Level Blueprint.

![LevelReset.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d66b5831-3660-46f2-8c53-b608f163dcdc/levelreset.png)

The **Level Reset** event sends out an execution signal when the level restarts. This is useful when you need something to be triggered once a level has reloaded, such as in a gaming situation when the player has died but the level does not need to reload.

![LevelReset_Example.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0362580b-8a55-47cb-94fc-52426014a2e6/levelreset_example.png)

## Event Actor Begin Overlap

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c8fbaad-8f3c-4849-829b-0ece960f436f/beginoverlap.png)

This event will execute when a number of conditions are met at the same time:

-   Collision response between the actors must allow Overlaps.
-   Both Actors that are to execute the event have **Generate Overlap Events** set to true.
-   And finally, both Actors' collision starts overlapping; moving together or one is created overlapping the other.

For more information on collision, see: [Collision Responses](/documentation/en-us/unreal-engine/collision-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6592c8e-b5d3-42cc-a025-96ee00c2a12c/beginoverlapex.png)

When this Blueprint Actor overlaps the Actor stored in the Player Actor variable, it will increment the Counter integer variable.

| Item | Description |
| --- | --- |
| Output Pins |   |
| **Other Actor** | Actor - This is the Actor that is overlapping this Blueprint. |

## Event Actor End Overlap

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cad1a8a4-78b6-4d30-8211-03b2a2dd2976/endoverlap.png)

This event will execute when a number of conditions are met at the same time:

-   Collision response between the actors must allow Overlaps.
-   Both Actors that are to execute the event have **Generate Overlap Events** set to true.
-   And finally, both Actors' collision stop overlapping; moving apart or if one is destroyed.

For more information on collision, see: [Collision Responses](/documentation/en-us/unreal-engine/collision-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a379f070-3b68-4b99-978a-fd945df45665/endoverlapex.png)

When this Blueprint Actor stops overlapping any other Actor except the Actor stored in the Player Actor variable, it will destroy the Actor that overlapped it.

| Item | Description |
| --- | --- |
| Output Pins |   |
| **Other Actor** | Actor - This is the Actor that is overlapping this Blueprint. |

## Event Hit

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad37ae47-521b-49e8-9f3b-7f268766eda0/eventhit.png)

This event will execute as long as the collision settings on one of the Actors involved have **Simulation Generates Hit Events** set to true.

If you are creating movement using Sweeps, you will get this event even if you don't have the flag selected. This occurs as long as the Sweep stops you from moving past the blocking object.

| Item | Description |
| --- | --- |
| Output Pins |   |
| **My Comp** | PrimitiveComponent - The Component on the executing Actor that was hit. |
| **Other** | Actor - The other Actor involved in the collision. |
| **Other Comp** | PrimitiveComponent - The component on the other Actor involved in the collision that was hit. |
| **Self Moved** | Boolean - Used when receiving a hit from another object's movement (if false), the directions of Hit Normal and Hit Impact Normal will be adjusted to indicate force from the other object against the object being hit. |
| **Hit Location** | Vector - The location of contact between the two colliding Actors. |
| **Hit Normal** | Vector - The direction of the collision. |
| **Normal Impulse** | Vector - The force that the Actors collided with. |
| **Hit** | Struct HitResult - All the data collected in a Hit, you can pull off and "break" this result to gain access to the individual bits of data. |

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb050347-4699-4d32-b77f-683abdf24560/eventhitex.png)

In this example, when this Blueprint executes Hit it will spawn an explosion effect at the point of impact.

## Event Any Damage

This Blueprint Event node executes only on the server. For single player games, the local client is considered the server.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c656a0f5-2fad-4106-a67e-673a5dc8019d/anydamage.png)

This event is passed along when general damage is to be dealt. Like drowning or environmental damage, not specifically point damage or radial damage.

| Item | Description |
| --- | --- |
| Output Pins |   |
| **Damage** | Float - The amount of damage being passed into the Actor. |
| **Damage Type** | Object DamageType - This is the object that contains additional data on the Damage being dealt. |
| **Instigated By** | Controller - The Controller of the Object that is responsible for the damage. This could be the Player Controller that fired a gun or an AIController that threw the grenade to deal the damage. |
| **Damage Causer** | Actor - The Actor that caused the damage. This would be like a bullet or explosion. |

Here if the damage being dealt to the Actor is coming from Water, it will subtract health and print a warning to the screen.

## Event Point Damage

This Blueprint Event node executes only on the server. For single player games, the local client is considered the server.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e6564aa-a957-4206-b027-bea7981c54db/pointdamage.png)

**Point Damage** is meant to represent damage dealt by projectiles, hit scan weapons, or even melee weaponry.

| Item | Description |
| --- | --- |
| Output Pins |   |
| **Damage** | Float - The amount of damage being passed into the Actor. |
| **Damage Type** | Object DamageType - This is the object that contains additional data on the Damage being dealt. |
| **Hit Location** | Vector - The location of where the damage is being applied. |
| **Hit Normal** | Vector - The direction of the collision. |
| **Hit Component** | PrimitiveComponent - The Component on the executing Actor that was hit. |
| **Bone Name** | Name - The name of the bone that was hit. |
| **Shot from Direction** | Vector - The direction the damage came from. |
| **Instigated By** | Actor - The Actor that is responsible for the damage. This would be the Actor that fired a gun or threw the grenade to deal the damage. |
| **Damage Causer** | Actor - The Actor that caused the damage. This would be like a bullet or explosion. |

In this example, when any damage is received, the damage dealt is subtracted from the Actor's health, but if the Head of the Actor is hit then the Actor's health is set to -1.

## Event Radial Damage

This Blueprint Event node executes only on the server. For single player games, the local client is considered the server.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb086931-039a-44ba-a228-20b56d2deaa9/radialdamage.png)

The **Radial Damage** Event is called whenever the parent Actor for this sequence receives radial damage. This is useful for handling events based on explosion damage, or damage caused indirectly.

| Item | Description |
| --- | --- |
| Output Pins |   |
| **Damage Received** | Float - The amount of damage received from the event. |
| **Damage Type** | Object DamageType - This is the object that contains additional data on the Damage being dealt. |
| **Origin** | Vector - This gives the location in 3D space where the damage originated. |
| **Hit Info** | Struct HitResult - All the data collected in a Hit, you can pull off and "break" this result to gain access to the individual bits of data. |
| **Instigated By** | Controller - The Controller (AI or Player) that instigated the damage. |
| **Damage Causer** | Actor - The Actor that caused the damage. Could be a bullet, rocket, laser, or a character punching another. |

## Event Actor Begin Cursor Over

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7b22faf-fdbb-4387-9f85-ddf5bacc24b6/begincursorover.png)

When using the mouse interface, when the mouse cursor is moved over an Actor, this event will execute.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5517e442-30ec-4d60-8ead-20de578d84a2/begincursoroverex.png)

Once the mouse passes over this Actor it sets the scalar Parameter named Highlight on the Dynamic Material Instance to 1.0.

## Event Actor End Cursor Over

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0947be5-758d-41e5-b5bb-dbed3ea30ed0/endcursorover.png)

When using the mouse interface, when the mouse cursor is moved off an Actor, this event will execute.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1fe05933-7abd-4725-9961-997bcb956720/endcursoroverex.png)

This will set the Actor stored in Target Notification to hidden in game.

## Event Begin Play

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09c2041a-fb9f-436f-98c0-04f322863de6/beginplay.png)

This event is triggered for all Actors when the game is started, any Actors spawned after the game is started will have this called immediately.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d11b75d4-de43-4ef6-97e0-b80f850bc2aa/beginplayex.png)

When beginning play, this Actor will set its Health to 1000 and Score to 0.

## Event End Play

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa1941ff-e5bc-4c01-9c9e-f2b64c1108e8/endplay.png)

This event is executed when the Actor ceases to be in the World.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ec52727-cd35-4960-ab62-310f0ae49468/endplayex.png)

Once this Actor is no longer in the World, a String will output to indicate the reason for the Event being called.

| Item | Description |
| --- | --- |
| Output Pins |   |
| **End Play Reason** | enum EEndPlayReason - An enum indicating the reason for why Event End Play is being called. |

## Event Destroyed

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51cb33cd-85cd-4d03-a0dc-961b07c0e722/destroyed.png)

This event is executed when the Actor is Destroyed.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/131515f1-9291-4b9b-b566-bc2c105a3dec/destroyedex.png)

In this example, the variable of Score is being set to Value plus Score.

The Destroyed Event will be deprecated in a future release! The functionality of the Destroyed function has been incorporated into the EndPlay function.

## Event Tick

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32b3cd9e-f0a7-4572-87a3-851eea7d8fc7/tick.png)

This is a simple event that is called on every frame of gameplay.

| Item | Description |
| --- | --- |
| Output Pins |   |
| **Delta Seconds** | Float - This outputs the amount of time between frames. |

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af645007-8b07-4777-abec-abedea7fe56a/tickex.png)

This example uses Delta Seconds to form a countdown timer that displays in the log with the final tick being "Blast Off!"

## Event Receive Draw HUD

This Event is only available to Blueprint Classes that inherit from the HUD class.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/412e4728-40ba-4b79-b309-d9f0aa3a7fce/drawhud.png)

This is a specialized event that enables Blueprints to draw to the HUD. The HUD draw nodes require this event to be the one that creates them.

| Item | Description |
| --- | --- |
| Output Pins |   |
| **Size X** | Int - The width of the render window in pixels. |
| **Size Y** | Int - The height of the render window in pixels. |

This will create a clickable Hit Box in the center of the render window, with a red box behind it so you can see it.

## Custom Event

![Custom Event Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fd45cea-8165-4924-930c-4866c801f4b1/name_custom_event.png)

The Custom Event node is a specialized node with its own workflow.

To learn more:

-   [Custom Events](/documentation/en-us/unreal-engine/custom-events-in-unreal-engine): Create your own events that can be called at any point in your Blueprint's sequence.
-   [Calling Events through Sequencer](/documentation/en-us/unreal-engine/fire-blueprint-events-during-cinematics-in-unreal-engine): Create events to be triggered at specific times during the playback of a cinematic sequence.
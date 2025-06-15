# Add Event Handler Group

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/add-event-handler-group-reference-for-niagara-effects-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/add-event-handler-group-reference-for-niagara-effects-in-unreal-engine)  
**Processed:** 2025-06-14 16:04:51

---

An **Event Handler** determines how an emitter responds to incoming events. For each event, you create an **Event Handler Properties** item and a **Receive Event** item. There can be multiple events in each emitter.

Events currently do not work with GPU simulation. They can only be used with CPU simulations.

In order to use an Event Handler, you need to first place an [**Event Module**](/documentation/en-us/unreal-engine/particle-update-group-reference-for-niagara-effects-in-unreal-engine#eventsmodules) in the Particle Update group of the emitter that is generating the event. For example, if you want the particles in Emitter B to follow the particles in Emitter A, you would place a **Generate Location Event** module in the Particle Update group of Emitter A. Then you would add an **Event Handler** to Emitter B, along with a **Receive Location Event** item, to listen for that location event.

In order to use events properly, make sure to enable **Requires Persistent IDs** in the **Emitter Properties** item of any emitter that is generating events.

## Event Handler Properties

| Parameter | Description |
| --- | --- |
| **Source** | Click the dropdown to select the source emitter and event. |
| **Execution Mode** | 
This controls which particles have the event script run on them. Available options are:

-   **Spawned Particles**: The event script is run only on particles that were spawned in response to the current event in the emitter.
-   **Every Particle**: The event script is run on every existing particle in the emitter. Be careful with this mode, as it can lead to a large amount of runtime work.



 |
| **Max Events Per Frame** | This sets the number of events that are consumed by this event handler. If the number of events generated is greater than this value, those additional events will be ignored. |
| **Spawn Number** | This controls whether or not particles are spawned as a result of handling this event. If **Random Spawn Number** is checked, this indicates the maximum number of particles spawned. |
| **Min Spawn Number** | If **Random Spawn Number** is checked, this indicates the minimum number of particles spawned. |
| **Random Spawn Number** | Check this box to randomly generate the number of particles that spawn as a result of handling this event. |

## Receive Event Modules

| Module Name | Description |
| --- | --- |
| **Receive Collision Event** | This is required to listen for a generated collision event (created by the **Generate Collision Event** module in the Particle Update group). Optionally, you can enable Inherited Collision Velocity Scale to determine how much of the parent velocity particles will inherit. |
| **Receive Death Event** | This is required to listen for a generated death event (created by the **Generate Death Event** module in the Particle Update group). Optionally, you can enable Inherited Velocity Scale to determine how much of the parent velocity particles will inherit. |
| Receive Location Event | 
This is required to listen for a generated location event (created by the **Generate Location Event** module in the Particle Update group). The Receive Location Event has the following settings: ***Inherited Velocity**: This determines how much of the parent velocity the particles inherit.* **Use Acceleration**: Extrapolate from the incoming event's acceleration to determine the new position. ***Inherit Parent Normalized Age**: This sends the maximum of either the receiving particle lifetime or the parent particle lifetime.* **Spawn Count**: This indicates how many particles are spawning as a result of this event.



 |
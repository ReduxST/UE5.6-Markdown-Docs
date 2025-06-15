# Events and Event Handlers Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/events-and-event-handlers-in-niagara-effects-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/events-and-event-handlers-in-niagara-effects-for-unreal-engine)  
**Processed:** 2025-06-14 16:22:39

---

In many cases, you will want several emitters in one system to interact with each other to create the effect you want. This usually means that one emitter generates some data, and then other emitters listen for that data, and perform some behavior in reaction to that data. In Niagara, this is done using **Events** and **Event Handlers**. **Events** are the modules that generate specific events that occur in the lifetime of a particle. **Event Handlers** are modules that listen for those generated events, and then initiate a behavior in response to that event.

Currently, events with GPU simulations will not work. Events only work with CPU simulation.

## Events

In order to use events, make sure to enable Requires Persistent IDs in the Emitter Properties of your emitters.

Because events happen dynamically as the particle ages, events are added to the Particle Update group. If you click on the **Plus (+)** next to Particle Update, you will see a section called **Events** in which you can add event modules to the stack.

There are several types of event modules available:

-   Location
-   Death
-   Collision

### Location Events

When you place a **Generate Location Event** module into the Particle Update group of your emitter, each particle spawned in that emitter will generate location data during its lifecycle. You can then set an Event Handler to receive that location data and trigger another behavior.

For example, if you want to create a trail effect for a fireworks rocket, you can place a **Generate Location Event** module into the Particle Update group of your rocket emitter. Then the trail emitter can spawn particles that follow the rocket by using the location data.

Click image for full size.

### Death Events

When you place a **Generate Death Event** module into the Particle Update group of your emitter, each particle spawned in that emitter will generate an event at the end of its lifetime. There are many ways to use this data. You can trigger another emitter's particle effect when the first emitter's particles die, or you can create chain reactions where each emitter spawns their effect when the previous emitter's particles die. You can also combine Location and Death events to create intricate interactions.

To use our fireworks example, you can generate an explosion effect to spawn at the end of the rocket particle's life. The Location event determines where the rocket particle is, which is where the explosion occurs. The Death event determines when the particle's lifetime ends, which is when the explosion effect is spawned.

Click image for full size.

### Collision Events

When you place a **Generate Collision Event** module into the Particle Update group of your emitter, particles will generate an event when they collide with an Actor, such as a static mesh or skeletal mesh. For example, if you want to change the firework effect into a weapon effect, you could have the explosion spawn when the rocket particles collide with a static or skeletal mesh.

Click image for full size.

You need to add a **Collision** module to an emitter before you can add a **Generate Collision Event** to that emitter. This enables the emitter's particles to collide with objects in the world.

## Event Handlers

Event Handlers consist of two parts: **Event Handler Properties**, and a **Receive Event**. For each event you want the emitter to respond to, you will add an **Event Handler Properties** item, and a **Receive Event** module.

If you click the **Plus (+)** next to Emitter Properties, you will be able to add an **Event Handler** stage to your emitter.

Click image for full size.

In **Event Handler Properties**, set the **Source** of the event with a dropdown that lists all of the Generate Event modules that are available. Then you can choose what particles are affected by the event, how many times the event occurs per frame, and if the event spawns particles you can select how many are spawned.

Click image for full size.

After you set the properties for the Event Handler, click the **Plus (+)** next to **Event Handler** to add a **Receive Event** module. It must match the generated event module you placed in the Particle Update group of the emitter that generates the event.

Click image for full size.

For example, if you placed a **Generate Location Event** in an emitter, you would select the **Receive Location Event** module for your Event Handler.

Click image for full size.
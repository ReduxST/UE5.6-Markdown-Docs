# Niagara System and Emitter Module Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/system-and-emitter-module-reference-for-niagara-effects-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/system-and-emitter-module-reference-for-niagara-effects-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:21

---

This page contains some basic reference information about how modules work in Niagara. Below this reference information, there are links to pages describing each group of items and modules that are included with the Niagara plugin.

## Niagara Selection Stack Model

Particle simulation in Niagara operates as a *stack* simulation flows from the top of the stack to the bottom, executing programmable code blocks called *modules* in order. Crucially, every module is assigned to a *group* that describes when the module is executed.

Modules that are part of the **System** groups execute first, handling behavior that is shared with every emitter. Then, modules and items in the **Emitter** groups execute for each unique emitter. Following this, parameters in the **Particle** groups execute for each unique particle in an individual emitter. Finally, **Render** group items describe how to render each emitter's simulated particle data to the screen.

For more information on the Stack, see the **Niagara Selection Stack and Stack Groups** section in [Niagara Key Concepts](/documentation/en-us/unreal-engine/key-concepts-in-niagara-effects-for-unreal-engine).

**A module is an item, but an item is not a module**. *Modules* are editable assets a user can create. *Items* refer to parts of a system or emitter that the user cannot create. Examples of items are system properties, emitter properties, and renderers.

## Execution State Management

Niagara systems and emitters have a distinct Execution State that defines how their simulation is run. Emitters that are part of a system each have a unique Execution State independent of the owning system, so they can change how they are being executed independent of that owning System. The possible Execution States are:

-   **Active**: The System or Emitter simulates and allows spawning.
-   **Inactive**: The System or Emitter simulates but does not allow any new spawning.
-   **InactiveClear**: The System or Emitter destroys all Particles it owns, and then moves to the Inactive Execution State.
-   **Complete**: The System or Emitter does not simulate and does not render.

## Settings, Groups, and Renderers
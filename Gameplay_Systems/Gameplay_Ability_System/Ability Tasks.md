# Ability Tasks

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-ability-tasks-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-ability-tasks-in-unreal-engine)  
**Processed:** 2025-06-14 16:24:47

---

Ability Tasks (C++ class `UAbilityTask`) are a specialized form of the more general Gameplay Task class intended to work with Gameplay Abilities. Games that use the Gameplay Ability System usually include a variety of custom Ability Tasks which implement their unique gameplay features. They perform asynchronous work during a Gameplay Ability's execution, and have the capability to affect execution flow by calling [Delegates](/documentation/en-us/unreal-engine/delegates-and-lambda-functions-in-unreal-engine) (in native C++ code) or moving through one or more output execution pins (in Blueprints). This enables Abilities to execute across multiple frames, and to perform several distinct functions in the same frame. Most Ability Tasks have an execution pin that fires immediately, enabling Blueprint execution to continue after starting a Task. In addition, there are often task-specific pins that will fire after a delay, or following a certain event that may or may not happen.

Ability Tasks can self-terminate by calling the `EndTask` function, or it can wait to be terminated automatically when the Gameplay Ability that ran it ends. This prevents phantom Ability Tasks from running, effectively leaking CPU cycles and memory. For example, one Ability Task might play a spell-casting animation while another places a targeting reticule at the player's aim point. The Gameplay Ability could end if the player either hits the Confirm input to cast the spell, or waits for the animation to finish without confirming the spell. Although they can self-terminate at any time, the Ability Tasks are guaranteed to end, at latest, when the main Ability ends.

Ability Tasks are designed to be used in both networked and non-networked environments, although they do not directly update themselves across the network. They generally stay in sync indirectly, since they are created by Gameplay Abilities (which do replicate), and use replicated information, such as player input or networked variables, to determine their execution flow.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5d35850-116e-4538-b621-3e6288ef4d6d/sampleabilitytaskbp.png "SampleAbilityTaskBP.png")

*A melee attack Gameplay Ability, implemented in Blueprints. The "Play Montage and Wait for Event" Ability Task at the center is part of the ActionRPG sample.*

To see how this could be setup in a UE4 project, check out the [Melee Abilities In ARPG](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine) documents.
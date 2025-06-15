# Abilities in Lyra

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/abilities-in-lyra-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/abilities-in-lyra-in-unreal-engine)  
**Processed:** 2025-06-14 16:04:13

---

Lyra uses the [Gameplay Ability System](/documentation/en-us/unreal-engine/gameplay-ability-system-for-unreal-engine) (**GAS**) to orchestrate most of its gameplay. Abilities can be innate to hero data like jump, granted from an action like a Game feature, gained through Experience, or granted from Equipment.

## What is the Gameplay Ability System and Why Use It?

The Gameplay Ability System is a plugin that provides a framework for quickly implementing and iterating on gameplay mechanics. When writing code for complex gameplay mechanics that can include multiplayer, you may write a lot of common boilerplate functionality that applies over many different game types.

GAS attempts to abstract mechanics into common game design patterns, and provides a framework that solves common gameplay implementation problems while letting context vary from project to project.

Writing boilerplate code is often error-prone and time consuming, especially for multiplayer games. For example, you don't want to spend a significant amount of time ensuring your Health values are replicating correctly, or copying the same lines of code over when you decide to have an Energy value that behaves identically.

The GAS addresses these issues by providing a foundation that fulfills common gameplay functionality as much as possible, while staying mechanic-neutral. Instead of forcing concepts such as Health, Ammo, Melee Attack, or Poison Debuff, GAS provides tools to define, replicate, and work with **Attributes**, **Abilities**, and **Effects**, which can then be specialized to fulfill the needs of the given gameplay mechanic.

Lyra implements abilities for common actions such as using weapons, movement-related actions like jumping and dashing, and passive listening actions such as triggering respawn after death. Abilities are also used for less obvious purposes such as summoning match information UI or managing gameplay phases. These are detailed in sections below.

GAS is structured around the following core classes. Lyra extends many of these to provide additional functionality:

| Core Class | Description |
| --- | --- |
| UAbilitySystemComponent | An **Ability System Component** (**ASC**) can be added to any Actor to provide it with GAS functionality. This keeps track of the state for that specific Actor, and handles replication. |
| UAttributeSet | A collection of Attributes, or numeric values with a specific meaning within your game mechanics. Attributes can represent game resources such as 'Health', reference values that can affect other game rules, such as 'Base Attack Power', or even stateless quantities such as 'Applied Damage'. Attribute Sets are responsible for defining, managing and replicating one or more Attribute properties. |
| FGameplayTag | An arbitrary hierarchical identifier that can be applied to a game object. These can be used to identify, categorize, and filter game entities. They can be granted or revoked by Gameplay Effects and Abilities, and can affect their behavior. One example is a 'Gameplay.DamageImmunity' tag that prevents damage on an owner's avatar/pawn. |
| UGameplayAbility | A game action that can be granted to, and performed by, a GAS-enabled Actor, along with information to determine its requirements, costs, and other behaviors. Examples range from basic melee attacks to a self-contained game menu flow to a triggered behavior caused by another game action. |
| UGameplayEffect | The consequences of a game action. Effects can temporarily or permanently modify attributes, grant or revoke tags, enable access to other abilities, and much more. Gameplay Effects are the most common way in which GAS-enabled Actors interact with each other. |

The main benefits of GAS are:

-   **Network Replication:** You don't need to worry about ensuring your attributes or debuffs are applying or replicating properly. GAS takes care of the inner logic for you.
    
-   **Modularity:** Adding or changing game mechanics is often as easy as implementing and granting a new ability. By breaking down gameplay functionality into separate assets, the ability system can provide a common communication layer between radically different game objects or mechanics. For example, Health can be compartmentalized into its own Attribute Set and interacted with through Gameplay Effects from a variety of systems.
    
-   **Fast iteration:** GAS makes it easy to change individual game rules without the need to modify the entire system. Data sources for game calculations can be easily swapped, and changing the consequences of an action can be modified from the corresponding Gameplay Effect.
    

## ULyraAbilitySystemComponent

The **Lyra Ability System Component** (**ULyraAbilitySystemComponent**) extends the **Ability System Component** (**UAbilitySystemComponent**) functionality to interface with the Lyra framework. It is added to all **LyraPlayerState** instances and can be found in your c:Lyra\\Source\\LyraGame\\AbilitySystem\\LyraAbilitySystemComponent.h file directory.

### ALyraPlayerState

**Lyra Player States**(**ALyraPlayerState**) own the Ability System Components used for all player-specific abilities and behaviors. Human players and AI bots will each have one. You can access this class in your c:\\Lyra\\Source\\LyraGame\\Player\\LyraPlayerState.h file directory. The main benefit of adding an Ability System Component to the Player State class is that it helps separate the GAS state logic from the underlying **Pawn** data.

Separating this logic is useful in games where the player's Pawn will need to often be respawned, or if a Player is switching control between multiple Pawns, or in instances of gameplay where they may not currently be in possession of a Pawn.

This guarantees that some of its Abilities, Attributes, and Effects persist between possessing Pawns. This logic provides an easier process to retain the GAS state between the game phase changes. However, special care is required when initializing and de-initializing the Pawn-specific GAS state every time you **Possess** or **Unpossess** a Pawn.

Lyra accommodates this through the **ULyraHeroComponent** and the **ULyraPawnExtensionComponent**. These Components are responsible for granting a specific set of Abilities, Attributes, and Gameplay Effects to the PlayerState's AbilitySystemComponent when it's possessed by a valid Controller. These are revoked automatically when the Pawn is eliminated, unpossessed, or otherwise removed from play.

You can navigate to the ULyraHeroComponent from the `c:\ReleaseWorkspace\Samples\Games\Lyra\Source\LyraGame\Hero\LyraHeroComponent.h` directory and the ULyraPawnExtensionComponent from the `c:\Lyra\Source\LyraGame\Pawn\LyraPawnExtensionComponent.h` file directory.

### ALyraGameState

High-level game phase logic is managed server-side by the **Lyra Game State** (**ALyraGameState**) class, located in your `C:\Lyra\Source\LyraGame\LyraGameState.h file`. Game States exist on both the client and server, and use an Ability System Component with Game Phases that are implemented as abilities. These Game Phases are activated and deactivated to affect how gameplay events are handled. As an example, ShooterCore implements three phases:

| Phase | Description |
| --- | --- |
| Warmup | During this phase, a damage immunity Gameplay Effect is applied to all players, then starts a replicated countdown, removes the immunity, and transitions to Playing state. |
| Playing | In this phase, the Game has begun and is currently in play. Scoring and time limits are tracked, and will transition to PostGame when appropriate. |
| PostGame | This phase reapplies damage immunity and disables controls on all players, then transitions to the next match round. |

While **Game States** exist on both the Client and Server, **Game Mode** is server-only

### Game Phase Abilities

Game Phase abilities extend from the **ULyraGamePhaseAbility** class, with each ability encapsulating an individual state. The Game State logic assumes ability activation is phase start, and ability end is phase end. This provides you with the capability to listen for the start or end of specific phases, using the **Gameplay Tag** `GamePhaseTag`.

```
	`| */ Defines the game phase this game phase ability is part of.  For example, if your game phase is GamePhase.RoundStart, then it will cancel all sibling phases.  	So, if you had a phase such as GamePhase.WaitingToStart that was active, starting the ability part of RoundStart would end WaitingToStart. However, to get nested behaviors you can also nest the phases. For example, GamePhase.Playing.NormalPlay, is a sub-phase of the parent GamePhase.Playing, so changing the sub-phase to GamePhase.Playing.SuddenDeath, would stop any ability tied to GamePhase.Playing.*, but wouldn't end any ability tied to the GamePhase.Playing phase.  		UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = "Lyra|Game Phase") 		FGameplayTag GamePhaseTag; 	 |`

Copy full snippet
```
| \*/ Defines the game phase this game phase ability is part of. For example, if your game phase is GamePhase.RoundStart, then it will cancel all sibling phases. So, if you had a phase such as GamePhase.WaitingToStart that was active, starting the ability part of RoundStart would end WaitingToStart. However, to get nested behaviors you can also nest the phases. For example, GamePhase.Playing.NormalPlay, is a sub-phase of the parent GamePhase.Playing, so changing the sub-phase to GamePhase.Playing.SuddenDeath, would stop any ability tied to GamePhase.Playing.\*, but wouldn't end any ability tied to the GamePhase.Playing phase. UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = "Lyra|Game Phase") FGameplayTag GamePhaseTag; |

You can switch phases from Blueprint using the **Lyra Game Phase Subsystem** (**ULyraGamePhaseSubsytem**), which ends the previous phase ability (if it's running) and activates a new one.

### Input Tag Activation Support

Abilities granted through the **Gameplay Ability Set** (**UGameplayAbilitySet**) will automatically check for activation if a matching **Input Tag** is received from[Lyra's Input system](/documentation/en-us/unreal-engine/lyra-input-settings-in-unreal-engine). This streamlines ability activation without having to rely on opaque numeric **Input ID** numbers or manually handling **Input Action** events. Examples include jumping (GA\_Hero\_Jump) and weapon firing (GA\_Weapon\_Fire), described below.

### Expanded Tag Relationship System

GAS Abilities and Effects provide the functionality to block or cancel specific Abilities based on which Gameplay Tags have been granted to their owner, typically by other Abilities or Gameplay Effects.

This information is held by each specific Ability and Effect, which may be inconvenient when you need to make overarching changes to these relationships. For example, as your game grows and its rules become more complex, it can lead to errors and inconsistencies when updating your game rules.

Lyra provides an improvement to this workflow by introducing the **Lyra Ability Tag Relationship Mapping** (**ULyraAbilityTagRelationshipMapping**) data assets. These hold a list of blocking, canceling, and required tag relationships. They can be created through the **Content Browser** > **Add** > **Miscellaneous** > **Data Asset**.

You can specify an **Ability Tag Relationship Mapping** asset as part of an **ULyraPawnData** asset, and it will be assigned to the corresponding Lyra Ability System Component when the Pawn is possessed. When the Ability System Component holds a reference to a valid tag relationship mapping, it will apply these as an additional layer of activation and cancellation conditions for ability activation.

## ULyraGlobalAbilitySystem

The **Lyra Global Ability System** (**ULyraGlobalAbilitySystem**) provides a quick means of keeping track of and interacting with all Lyra Ability System Components in a level.

A Lyra Ability System Component will automatically register with the subsystem during initialization. Currently, the subsystem provides Blueprint-callable functions to grant or remove Abilities and Gameplay effects from all registered Ability System Components.

For example, Lyra's Elimination mode applies a Gameplay Effect (GE\_PregameLobby) globally during the warm-up phase of a match. It grants a damage immunity tag to all players and triggers a Gameplay Cue that enables a UI element indicating that the match hasn't started yet.

## ULyraAbilitySet

The **Lyra Ability Set** (**ULyraAbilitySet**) is a **Data Asset** type that can be created from the Content Browser. It holds a list of Gameplay Abilities, Gameplay Effects, and Attribute Sets which will be granted to a Lyra Character when the Ability Set is applied.

Parties that grant Lyra Ability Sets, such as Game Features or Equipment, are responsible for tracking which Actors they are granted to. A helper struct, FLyraAbilitySet\_GrantedHandles, is used for bookkeeping and removal.

| Method | Description |
| --- | --- |
| Granted Gameplay Abilities | A list of Lyra Gameplay Abilities to grant, along with the default level to grant the ability at and an optional Input Tag to associate with the ability. |
| Granted Gameplay Effects | A list of Gameplay Effects to grant, along with the default level to grant the effect at. |
| Granted Attributes | A list of Attribute Sets to grant. |

Ability Sets can be granted in a variety of ways:

| Method To Grant Ability Set | Description |
| --- | --- |
| ULyraExperienceDefinition ULyraPawnData | 
A list of Ability Sets is defined in the **ULyraPawnData** asset. These assets can be referenced from the **ULyraExperience Definition**, and its Ability Sets will be granted to the player's Pawn automatically upon initialization. This is mediated by ULyraPlayerState when the Experience is loaded.

These abilities are granted to the Player State, not the Pawn it possesses. They may be granted before a Pawn is possessed and persist even if the possessed Pawn changes. They won't be Activated until the Pawn itself is possessed, even if their Activation Policy is set to On Spawn. Plan accordingly.



 |
| Game Feature Actions | **UGameFeatureAction\_AddAbilities** can grant Ability Sets to an Actor upon activation. These Actions can be added to Game Feature plugins or the Experience Definition itself. |
| Equipment | 

**ULyraEquipmentDefinitions** can also grant AbilitySets to the Actor they're added to. This is mediated by the **ULyraPlayerState** when the Experience is loaded.

These abilities are granted to the Player State, not the Pawn it possesses. They may be granted before a Pawn is possessed and persist even if the possessed Pawn changes. They won't be Activated until the Pawn itself is possessed, even if their Activation Policy is set to On Spawn. Plan accordingly.



 |

## ULyraGameplayAbility

The **Lyra Gameplay Ability** (**ULyraGameplayAbility**) is extended from the UGameplayAbility class to provide extra utility and interface with the Lyra framework.

### Activation Group

The Activation Group determines if an ability can be freely activated, or if the ability blocks or interrupts other exclusive abilities. You can achieve additional complex blocking behaviors using the following Tag Relationship assets:

| Activation Group | Description |
| --- | --- |
| Independent | The ability doesn't block or replace other abilities. Most abilities should be set to this tag by default. |
| Exclusive Replaceable | The ability doesn't block other exclusive abilities but will be canceled if another Exclusive ability is activated. |
| Exclusive Blocking | While the ability is running, no other exclusive abilities may be activated. |

Most game actions, such as shooting, switching weapons, and melee attacks are set to Independent and Blocking. Concurrency and Cancellation are mediated by Tag Relationships. Leaderboards and other in-game menus are set to Exclusive Blocking to ensure that only one menu is visible at a time.

### Activation Policy

Allows ability activation to be automatically handled by the Lyra framework.

| Activation Policy | Description |
| --- | --- |
| None | Activation is done manually by game code or Blueprint. |
| On Spawn | The ability is activated as soon as a valid Avatar is assigned to the PlayerState. The Weapon Reload Gameplay Ability (**GA\_Weapon\_AutoReload**) is set to On Spawn. It activates immediately and runs passively, checking at periodic intervals if the current magazine is empty. The ability does not end until the Pawn is unpossessed. |
| On Input Triggered | The ability is activated once as soon as the associated Input Tag is triggered. **Aim Down Sights** (**ADS**), Grenade, and other similar abilities are set to On Input Triggered. They are activated once and do not reactivate automatically if the button is held. |
| While Input Active | 
The ability is activated continuously for as long as the associated Input Tag is triggered. Weapon Fire abilities like **GA\_Weapon\_Fire\_Shotgun** are set to While Input Active. They play a firing Animation Montage, then wait until the refire time has elapsed, and then will end the ability. This is because the Retrigger Instanced Ability is set to false, redundant activation messages are ignored until the ability is finished.

We recommend caution using this activation if the Retrigger Instanced Ability is set, otherwise you could spam activation and get undesired effects.



 |

### K2\_CanActivateAbility

Some Lyra Abilities use the **K2\_CanActivateAbility** function to implement activation checks in Blueprints instead of C++. The function returns true or false to allow activation and provides you with context gameplay tags to determine what may have prevented an activation. This is exposed to all Gameplay Abilities, not just Lyra's.

### Additional Costs

Normal Gameplay Abilities only allow for a single Cost and Cooldown Gameplay Effect. The **Additional Costs** list provides you additional costs you can specify without setting them to Gameplay Effects, which enables more complex activation conditions.

Additional costs are integrated into the standard cost flow and can be checked and committed manually with the corresponding **Check Cost** and **Commit Cost** nodes, or **Commit Ability** (if you also want to commit the cooldown).

Actual costs are implemented as **ULyraAbilityCost** objects. You can create custom costs by extending this class in C++ and overriding the **CheckCost** and **ApplyCost** virtual functions.

Lyra implements several additional costs using **ULyraAbilityCost\_PlayerTagStack**, which consumes a number of stacks from the specified Gameplay Tag on the Player State. These assume they are being called from an Ability deriving from **ULyraGameplayAbility\_FromEquipment**.

| Lyra Ability Cost | Description |
| --- | --- |
| ULyraAbilityCost\_InventoryItem | Consumes a given quantity of the associated item in the character's inventory. This is used for consumable inventory items. |
| ULyraAbilityCost\_ItemTagStack | Consumes a number of stacks from the specified item in the character's inventory. If the cost cannot be paid, this reports a Gameplay Tag back to other abilities to handle the cost. This is used in Lyra for Ammo consumption and reload tracking. GA\_Weapon\_Fire\_Shotgun and similar abilities use an Item Tag Stack additional cost set to `Lyra.ShooterGame.Weapon.MagazineAmmo`. Every time the weapon fires, the MagazineAmmo stack is decreased by the consumed amount. This prevents them from activating if the player runs out of ammo in the current weapon's magazine. |

### Added and Removed Events

Lyra Abilities provide additional Blueprint Events that enable the ability to handle being added to or removed from a character without the need to rely on activation. These are useful for initial setup and cleanup.

| Blueprint Event | Description |
| --- | --- |
| On Ability Added | The Event is called as soon as the ability is granted. The Avatar or Input Component may not yet be valid, so be careful what you access. |
| On Pawn Avatar Set | Called when the pawn is fully initialized, and both its Avatar and Input Component are valid. |
| On Ability Removed | This Event is called when the ability is about to be removed from the ASC, usually due to the Pawn being Unpossessed or Destroyed |

### Camera Modes

Lyra Abilities can override the Camera Mode through the Set Camera Mode and Clear Camera Mode Blueprint nodes. One example is the use of a death camera mode while a pawn is dying, triggered by the **GA\_Hero\_Death** ability.

### Type Tags

Lyra's abilities commonly include a type Gameplay Tag in their 'Ability Tags' property to classify them hierarchically. This type tag is widely used to manage blocking, canceling, and required tag settings on other abilities, or through the Tag Relationship system.

As examples, the character-centric action abilities include type tags such as 'Ability.Type.Action.Dash' and 'Ability.Type.Action.Jump'. But there are also passive abilities that outlive the characters with tags such as 'Ability.Type.Passive.AutoRespawn'. Character death will cancel all other character action abilities, without affecting some others.

### Native Ability Subclasses

Some Lyra Abilities have C++ implementations, to either enforce specific activation conditions, perform complex math logic(that would be cumbersome to implement in a Blueprint), or interact with sensitive low-level gameplay systems. See the table below for some example Abilities.

| Gameplay Ability | Description |
| --- | --- |
| ULyraGameplayAbility\_Death | Automatically configured to trigger off of a Death Gameplay Event. Cancels all other abilities, and signals the Pawn's Health Component to begin the Death process (which in turn triggers the rest of the game notifications and state changes). The visual effects are performed by a BP ability extension of this class (GA\_Hero\_Death). |
| ULyraGameplayAbility\_Jump | Provides functionality to trigger Jump and StopJumping inputs on the pawn's Character Movement Component while checking that the ability owner is a valid, locally controlled Pawn. |
| ULyraGameplayAbility\_Reset | When activated, this ability instantly resets the owning player with a new pawn in its initial spawned state and cancels all other abilities. |
| ULyraGameplayAbility\_FromEquipment | Provides functionality to interact with Lyra's Equipment system and retrieve the item associated with the ability. |
| ULyraGameplayAbility\_RangedWeapon | Native implementation of weapon firing. Interacts with the associated weapon to determine ammo count, hit accuracy, and others. Provides ray casting functionality to calculate bullet trajectories within a firing cone, find and validate hit targets. |

### Blueprint Ability Subclasses

These are some examples of how the Blueprint subclasses make use of the extended ability functionality in Lyra.

| Blueprint Subclass | Gameplay AbilityDescription |
| --- | --- |
| GA\_AbilityWithWidget | The base class for any ability that provides additional UI features. This manages the widget state for the ability, so it can display status, cooldown, and other ability information. One example is Lyra's Melee ability, with a custom touch input widget for mobile platforms. The **OnAbilityAdded** event registers the widget extensions with the UI Extension Subsystem, this saves the extension handles. The **OnAbilityRemoved** event unregisters and clears the extension handles. |
| GA\_Melee | 
Contains an Asset Tag of `Ability.Type.Action.Melee` that grants the Event.Movement.Melee tag while active. This ability is Triggered by the tag `InputTag.Ability.Melee`, when this tag becomes activated the On Activation event will Commit ability costs in the following order:

1.  Find the currently equipped weapon, and play its associated animation montage.
2.  Check for authority (server only), then perform a capsule trace in front of the player.
3.  If the trace hits a Pawn, additional checks are run, like a team comparison to avoid friendly fire and a secondary check to make sure the target is not occluded by level geometry.
4.  If a valid hit is registered, the character is moved towards the target through a RootMotion force.
5.  Next, a melee damage gameplay effect is applied on the target, and a melee hit gameplay cue is triggered on the owner.
6.  Finally, a Melee Impact sound is played on all clients through a multicast RPC.



 |
| GA\_Weapon\_Fire | 

Fire and Reload abilities are granted through an Ability Set inside the **Lyra Equipment Definition** (**ULyraEquipmentDefinition**) class when the associated weapon is picked up. The activation requirements are handled by the ULyraGameplayAbility\_RangedWeapon class, and the targeting logic is done in C++ by the same class. The Weapon Fire Gameplay Ability is activated by the tag `InputTag.Weapon.FireAuto` (input binding) and the `Input.Weapon.Fire` tag (gameplay event). It is Inhibited by the `Ability.Weapon.NoFiring` tag that is set from the reload ability, if the magazine is empty. The Asset Tag of `Ability.Type.Action.WeaponFire` grants the `Event.Movement.WeaponFire` tag. While the tag is active the On Ability Added event will set up a listener for the `Ability.PlayMontageOnActivateFail.Message` tag. This event is triggered when the player attempts to fire the weapon while no ammo is left. When the message is received, it plays a failed to fire montage (dry fire). This montage is only played if the player is still alive, and the animation will only be retriggered if a set amount of time has elapsed to prevent animation spamming. When **On Activation** is called, If the character is locally controlled, it will perform native targeting traces and builds the targeting data in the following order:

1.  Ability costs (ammo consumption) are committed natively.
2.  The targeting data is network predicted and sent to the server, where it's validated and confirmed by the **ULyraWeaponStateComponent**.
3.  If the targeting data is confirmed by the server, then the BP event **OnRangedWeaponTargetDataReady** is called, passing all found targets. This allows the ability to apply damage, play hit effects.
4.  Plays the firing Animation montage.
5.  Sets a timer to Fire Delay, which is the effective delay between shots.
6.  When Fire Delay or the timer finishes, ends the ability. Additional firing attempts are handled by the activation logic.

**On Ranged Weapon Target Data Ready** Is Called from C++ when all targets hit by the weapon are validated. This triggers the Firing gameplay cue on the weapon's owner, which then passes the first hit as a parameter. The cue Iterates through all targets hit, playing impact gameplay cues on each target location. If the ability has authority (is executed on the server), it applies the damage Gameplay Effect on each target hit.



 |
| GA\_Weapon\_ReloadMagazine | 

This Gameplay Ability is activated by the `InputTag.Weapon.Reload`, which is an Asset of the `Ability.Type.Action.Reload` tag. This grants the `Event.Movement.Reload` tag. While active, it will limit movement options. The reload logic revolves around three gameplay tag stacks on the associated weapon. The `Lyra.ShooterGame.Weapon.MagazineSize` is the maximum amount of ammo allowed per magazine for the current weapon. `Lyra.ShooterGame.Weapon.MagazineAmmo` is the remaining amount of ammo in the current magazine. When the amount reaches zero, the weapon must be reloaded to continue firing. `Lyra.ShooterGame.Weapon.SpareAmmo` is the remaining amount of ammo not in the current magazine. It overrides the `K2_CanActivateAbility` function, which is a Blueprint implementation of the following activation check logic:

-   Checks if `MagazineAmmo` is less than `MagazineSize`. If false, the magazine is full, and reloading should not continue.
-   Checks if `SpareAmmo` is greater than zero. If false, the player is out of ammo for this weapon.

On Activation of the ability:

-   Check for the `MagazineAmmo` stack count of the associated item. If there's no ammo remaining in the current magazine, it applies a tag to inhibit activation of weapon firing abilities.
-   Plays the weapon reload animation montage, then listens for the `GameplayEvent.ReloadDone` event. This event is sent through an Animation Notify on the mannequin's montage.
-   When the event is received, checks for authority (server), then performs the reload logic, which is simply changing values for the `Lyra.ShooterGame.Weapon.MagazineAmmo` and `Lyra.ShooterGame.Weapon.SpareAmmo` in the associated weapon on the character's inventory. Then ends the ability.
-   If for any reason the event was not processed, the ability ends locally once the montage is stopped or interrupted. On End Ability is called to remove the shooting inhibition tag set on activation if it was set earlier.



 |
| GA\_Grenade | 

This ability is activated by the `InputTag.Weapon.Grenade` Asset tag of the `Ability.Type.Action.Grenade`. This uses **GE\_Grenade\_Cooldown** as a cooldown effect. On Pawn Avatar Set registers the widget with the UI Extension Subsystem on the local client, ensuring that only one widget is added per ability instance. On Activation checks for ability costs and cooldowns and commits them. It ends the ability if either check fails. It will then execute in the following process:

1.  Commits the ability cost and cooldown.
2.  Calculates the grenade spawn location and rotation.
3.  Checks for authority. If the authority is on the server, then it spawns the grenade Actor at the calculated values and sets the owning Lyra Character as the instigator.
4.  The spawned B\_Grenade Actor is responsible for doing the detonation checks and applying relevant Gameplay Effects.
5.  B\_Grenade detonates automatically on collision with an enemy pawn. It applies friendly fire to the instigating character (the one who threw the grenade), but not to their teammates.
6.  Plays the grenade throw montage, then broadcasts the remaining cooldown time through the Gameplay Message Subsystem, so the associated widget can sync up its cooldown display.
7.  Ends the ability immediately, without waiting for the montage to complete.

On Ability Removed unregisters and clears the UI Extension.



 |
| GA\_ADS (Aim Down Sights) | 

Inherits from **GA\_AbilityWithWidget** to handle the HUD display buttons. This ability is Activated by the `InputTag.Weapon.ADS` tag, an Asset Tag of `Ability.Type.Action.ADS` that grants the `Event.Movement.ADS` tag. While active it is Local predicted, meaning it runs on the client immediately, then the server syncs to catch up. On Activation:

1.  Applies a custom camera mode to narrow the Field of View(FOV).
2.  Caches and overrides the character's walk speed. Because the ability is locally predicted, this will run on the owning client and server, then replicate to non-local clients.
3.  Applies a temporary input mapping context, overriding the movement inputs to one with a lower multiplier. By decreasing the input magnitude, any further movement inputs produce a lower acceleration and are replicated to the server with the lower acceleration value, forcing the character to walk while aiming.
4.  For the local player, updates the UI and plays the 'aim started' sound.
5.  Waits until the input button is released, and ends the ability once it does.

On End Ability:

1.  Clears the custom camera mode.
2.  If locally controlled, the UI updates and plays the 'aim ended' sound.
3.  Restores the controlled character's walk speed and removes the input mapping context to restore normal movement speed.



 |
| GA\_Hero\_Dash | 

Inherits from the GA\_AbilityWithWidget. This ability is activated by the `InputTag.Ability.Dash`, an Asset tag of the `Ability.Type.Action.Dash`. This grants the `Event.Movement.Dash`. while active it uses a cooldown effect: **GE\_HeroDash\_Cooldown**: On Activation the cooldown:

1.  Checks the ability costs. If the costs can be paid, commits them, otherwise ends the ability.
2.  Checks for local control, and ends the ability on the server.
3.  In the local client, the dash direction is chosen based on input and look direction. If there's no movement input, then the ability ends on the client (dash will only happen if there's a dash direction input).
4.  Selects an animation montage to play based on the movement direction and the character's orientation.
5.  The character stops crouching if it's crouched.
6.  If the ability doesn't have authority (local client), replicates the dash direction and chosen montage through a server RPC.
7.  On both the owning client and the server, plays the chosen montage, then applies a root motion force in the dash direction.
8.  Sends a message through the messaging subsystem, so the client-side UI can synchronize its cooldown time.
9.  On the server, triggers the dash effect gameplay cue, so it is replicated to all clients
10.  When the root motion force is completed, delays for a few additional moments then ends the ability. This keeps the granted ability tags for a few extra moments and inhibits other actions such as shooting or jumping.



 |
| GE\_InstantHeal | Granted by the **B\_AbilitySpawner**, which has a ALyraWeaponSpawner class that overrides the **GiveWeapon** function to apply a gameplay effect to the receiving Pawn and applies an instant heal gameplay effect. |

## FLyraGameplayEffectContext

The **Lyra Gameplay Effect Context** extends from the default **Gameplay Effect Context** (**FGameplayEffectContext**) struct provided by the GAS to define additional data members and functions to be sent to **Gameplay Cue Notifies**. Because FGameplayEffectContext is a struct type, it needs a replacement type that can be correctly recognized by Unreal and the Gameplay Ability System. The Lyra Gameplay Effect Context overrides multiple functions:

| Function | Description |
| --- | --- |
| Duplicate() | Performs a deep copy of HitResults and the other members that can't be memory-copied. |
| GetScriptStruct() | Returns a `FLyraGameplayEffectContext::StaticStruct()` to provide the correct reflection data to Blueprint. |
| NetSerialize() | Adds replication for any extra members defined. |

A struct template (`TStructOpsTypeTraits<>`) is defined for the Lyra Gameplay Effect Context. This helper struct will bind both the duplication and serialization functionality and make them available to the replication system.

The **Lyra Ability System Globals** (**ULyraAbilitySystemGlobals**) class extends the **Ability System Globals** (**UAbilitySystemGlobals**) class and overrides the `AllocGameplayEffectContext()` function to construct and return a Lyra Gameplay Effect Context struct.

This ensures the Gameplay Ability System allocates the extended structure whenever a new Gameplay Effect Context object is created.

#### What extra data is included?

Currently, the Gameplay Effect Context struct provides the unique Cartridge ID associated with Shooter Core's ranged weapon hits and provides extra utility to access the Physical Material and Ability Source Object.

#### How is the extra data accessed?

Because it is a type of struct, the Lyra Gameplay Effect Context struct can't directly include a Blueprint-exposed function to access its data.

A method to work around this limitation is to implement accessors as static functions in a Blueprint Function Library, pass the Context Handle as an input parameter, then cast it to the derived struct type internally.

The helper function `FLyraGameplayEffectContext::ExtractEffectContext` takes care of casting context pointers to the specialized types. Currently, this is used in the `FLyraGameplayAbilityTargetData_SingleTargetHit` structure.

Similar methods can be used to cast the Effect Context Handle passed to the Gameplay Cue through `FGameplayCueParameters`, allowing access to the extra functionality.

## ULyraAttributeSet

The **Lyra Attribute Set** (**ULyraAttributeSet**) is extended from the default Attribute Set class. This Lyra-specific base class provides a convenient `ATTRIBUTE_ACCESSORS` macro to automate the Gameplay Attribute property and value for Get, Set, and Initialize functionality.

`FLyraAttributeEvent` is used to streamline attribute changed events at the Attribute Set level.

| Function | Description |
| --- | --- |
| GetWorld() | Convenience getter that gets a reference to the world. |
| GetLyraAbilitySystemComponent() | Convenience getter that gets a reference to the lyra ability system component. |

Lyra provides two specialized Attribute Set classes:

### ULyraHealthSet

The **Lyra Health Set** (**ULyraHealthSet**) Include the following attributes that manage the character's current and maximum health:

| Attribute | Description |
| --- | --- |
| Health | The current health value, capped at MaxHealth. |
| MaxHealth | Determines the maximum allowed health value. |
| Healing | Accumulates the amount of healing applied to the character. Affects the Health value, then gets automatically reset to zero. |
| Damage | Accumulates the amount of damage applied to the character. Affects the Health value. |

This attribute set is also responsible for clamping the current Health value to MaxHealth, and for keeping track of when Health has run out. It implements a `FLyraAttributeEvent` delegate, which is fired when health runs out.

Other classes bind to this delegate to receive out of health notifications, like the `ULyraHealthComponent`, which is responsible for handling death and exposing the Health value to the game.

### ULyraCombatSet

The **Lyra Combat Set** (**ULyraCombatSet**) provides support for damage and healing. Gameplay Effects deal with modifying either one of these attributes or relying on Lyra's custom executions to adjust the Health total.

| Attribute | Description |
| --- | --- |
| BaseDamage: | The base amount of damage to be dealt in a damage execution. It is fed as an input to the damage execution calculation to determine actual damage dealt. |
| BaseHeal: | The amount of health to restore when the execution runs. |

### How Healing and Damage Work

By default, the Health attribute is hidden from modifiers, so it cannot be changed directly by Gameplay Effects like regular attributes. Instead, its value is set indirectly through the Healing attribute, and through the Custom Executions **ULyraHealExecution** and **ULyraDamageExecution**.

Treating damage and healing as attributes has the benefit of decoupling individual damage instances from the modified attribute, and makes working with damage values easier. It helps prevent accidental modification of important attributes. Because the Health value is hidden from Gameplay Effect modifiers, there's no risk of applying timed or infinite effects on top of its base value, which could cause issues in the long run.

#### Heal Execution

ULyraHealExecution snapshots the **BaseHeal** attribute on the source, then it clamps to zero to prevent negative healing. Finally, it modifies the Health attribute on the **Target**. Because this is done in source, the Health value can be modified without issue.

#### Damage Execution

ULyraDamageExecution tallies the **BaseDamage** and **Health** attribute values. BaseDamage is captured on the Source and snapshotted, while Health is captured on the Target. Then it checks for the impact location (so it knows where to spawn the damage numbers effect).

It checks with the target's Team for friendly fire and applies attenuations based on distance and Physical Material. Finally, it modifies the Health attribute on the Target. Because this is done in source code, the Health value can be modified without issue.

The damage numbers Gameplay Cue is set to receive the change in the Health attribute as its magnitude and derives the display from its raw (not normalized) value.

## Additional Information

### How do Damage Numbers Work?

When a damaging Ability is activated, it runs a test to determine what it has hit, then the Ability applies a damage Gameplay Effect to the target Actor.

The **GameplayEffectParent\_Damage\_Basic**(or any children that inherit from it), are applied by weapon casts and grenades. Damage is then applied through Execution which converts BaseDamage to Health and filters friendly fire, then the Gameplay Cue `GameplayCue.Character.DamageTaken` is applied on magnitude to the `LyraHealthSet.Health` cue.

**GCN\_Character\_DamageTaken** is invoked on clients. It is only displayed if the effect instigator is a local player. Damage is determined by the Gameplay Cue's raw magnitude. Location is determined by the hit result's location values, which are passed to the local Controller's ULyraNumberPopComponent. This component handles the display and the pooling, and spawns and configures a Niagara Emitter at the hit location to display the actual damage.

### How are Lyra Characters initialized?

Because of the interaction between the Pawn's possession flow, Game Feature registration, and the various replicated game framework values, a playable character's initialization flow is not always predictable: events can happen out of order, while the client is still waiting for server data.

Lyra solves this by implementing a **UPawnExtensionComponent**. Its main job is to ensure all relevant initialization conditions for the pawn are met before granting the pawn's AbilitySets and activating any On Spawn Lyra Abilities.

The Pawn Extension Component also keeps track of any abilities granted due to the Pawn and removes them from the possessor's Player State when the character is destroyed or unpossessed.

You can assign Ability Sets to a Pawn through the **ULyraPawnData** asset. These can be created from the Content Browser, and the default Pawn Data is determined by the [Experience Definition](https://docs.google.com/document/u/0/d/1GmJTjn6aeoXnn-eszLfWH25ysW_ps574bB2e64kgtl8/edit).

To initialize the Pawn and assign its abilities, the following conditions must be met:

-   The default Pawn Data is valid.
    
-   The Pawn is possessed by a valid local Controller or has server authority.
    
-   The associated Player State and Input Component have been replicated to the Pawn, and are valid.
    

## Blueprint Asset Naming Conventions

| Abbreviation | Meaning |
| --- | --- |
| GA\_ | Gameplay Abilities |
| GE\_ | Gameplay Effects |
| GCN\_ | Gameplay Cue Notifies (UGameplayCueNotify) |
| GCNL\_ | Latent Gameplay Cue Notifies (Inherits from AGameplayCueNotify\_Actor and subclasses.) |
| Phase\_ | Game Phase Abilities |
| AbilitySet\_ | Ability Set |
| IA\_ | Input Action |
| InputData\_ | Lyra Input Config |
| W\_ | Widget UI |
| B\_ | All other blueprints such as pawn types, item spawners, etc. |
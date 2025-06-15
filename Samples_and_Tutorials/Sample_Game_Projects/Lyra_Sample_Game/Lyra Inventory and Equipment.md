# Lyra Inventory and Equipment

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/lyra-inventory-and-equipment-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/lyra-inventory-and-equipment-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:33

---

## Lyra Inventory and Equipment

An **Inventory** is a collection of items that are in your possession, but they may also be stowed away, perhaps hidden inside a container such as a backpack.

**Equipment** is an item pulled out of that container or backpack that is being held, worn, or used.

For example, consider a Rifle item given to a Player Character. It initially only exists virtually in the player's inventory, including its ammunition. By pressing a weapon-swapping button, the Rifle becomes equipped. This appears as a 3D mesh in the character's hands, with the rifle's firing and reloading abilities added.

Below are some key distinctions between Inventory and Equipment:

| **Category** | **Inventory Items** | **Equipment Items** |
| --- | --- | --- |
| Visualization | Icons are used in the User Interface (UI) or for in-game pickups. | Visible Actors that are spawned while in use and often attached to the owner. |
| Lifetime | Instances exist as long as the owner holds onto them, then they are destroyed when dropped. | Instances are created when the item is equipped, then destroyed when unequipped. |
| Gameplay | The state is maintained using Gameplay Tag stacks. | No state is maintained between equip/unequip cycles.Can grant ability sets while equipped. |
| Ownership | Owned by the Controller from the InventoryManagerComponent. | Owned by the Pawn from the EquipmentManagerComponent. |
| Network Replication | Server and Autonomous Proxy only. | Server, Autonomous Proxy, and Simulated Proxies. |
| Data Definition | Composed from extensible inventory fragments. | Limited to data properties. |
| Association | The item definition usually specifies the associated equipment definition. | The equipment definition does not reference the inventory definition. |
| Naming Convention | Prefixed with 'ID\_' (ID\_Rifle) | Prefixed with 'WID\_' (WID\_Rifle) |

## Inventory

An Inventory item is an object that can be acquired or picked up. It affects gameplay and presentation through its array of **Inventory Fragments**. Fragments can alter the owner's stats through [Gameplay tags](/documentation/en-us/unreal-engine/using-gameplay-tags-in-unreal-engine), appear in the inventory UI, or let the item become equipped.

### Inventory Item Fragments

Lyra has a variety of fragments you can be apply to inventory items:

| **Inventory Fragment** | **Description** |
| --- | --- |
| InventoryFragment\_PickupIcon | Determines in-world representation of an item ready to be picked up. |
| InventoryFragment\_EquippableItem | Pairs this inventory item with an equipment definition used when the owner equips the item |
| InventoryFragment\_SetStats | Grants a set of gameplay tag-based stacks upon pickup, such as ammunition. |
| InventoryFragment\_QuickbarIcon | Determines HUD icons used for items that occupy a slot in the player's quick bar UI. |
| InventoryFragment\_ReticleConfig | Specifies alternative HUD reticle classes to instantiate when this inventory item is equipped. |

You can customize Lyra's Inventory Fragment Item effects by implementing new fragment types.

## Item Pickups

The `ALyraWeaponSpawner` class contains an example of how pickups function together with inventory items. These items are used in Lyra shooter maps as `B_WeaponSpawner` (for weapon pickups) and `B_AbilitySpawner` instances (for health pickups).

## Equipment

**Equipment** is an item that can be equipped to a player, potentially changing their gameplay visuals, UI, or granting passive or active [Abilities](/documentation/en-us/unreal-engine/abilities-in-lyra-in-unreal-engine). Typically an equipped item is instantiated based on an inventory item.

Unlike inventory items, equipment items only exist when equipped.

## Relationship with UI

### Quick Bar

The **Quick Bar** is a player HUD area where equipable inventory items are shown, such as weapons. It uses information from the item's inventory fragments for display and the inventory instance's stat tags for the ammunition status.

As you choose different quick bar slots, weapons in the player's inventory are equipped, and unequipped.

See the **W\_QuickBar** and **W\_QuickBarSlot** widget Blueprints for implementation details.

### Custom Reticles

Different items, when equipped, may cause a player's HUD to change. For example, the Pistol's reticle is designed for focused shooting, while the Shotgun's reticle is designed for a widespread visualization of multiple hit locations.

Reticles are specified from a fragment in the item's inventory item definition. Refer to the **W\_ShooterHUDLayout** and **W\_WeaponReticleHost** Widget Blueprints.

## Key Inventory Types

| Type | Notes |
| --- | --- |
| InventoryManagerComponent | 
-   Manages a collection of inventory items.
    
-   Converts shared InventoryItemDefinitions into InventoryItemInstances.
    
-   Duplicate items can be represented from multiple InventoryItemInstances or from a single one with a StackCount.
    
-   Owned by a LyraPlayerController.
    



 |
| InventoryItemDefinition (asset) | 

-   Asset Example: ID\_Pistol.
    
-   Holds the array of InventoryFragments that provides more information about different aspects of the item.
    
-   For equipable items, the InventoryItem has a fragment that specifies the EquipmentDefinition asset
    



 |
| InventoryFragment | An optional chunk of data describing an aspect of the item. An item will typically have more than one of these. |
| InventoryItemInstance | 

-   Created when an item is added to an inventory
    
-   References its original InventoryItemDefinition
    
-   Represents a single item, such as a Rifle, along with 'stacks' of stat tags. These stacks represent features of the item, such as remaining ammo and capacity.
    
-   Does not have subclasses.
    



 |
| PickupDefinition (asset) | 

-   A data asset type that holds information about a pickup item's inventory item definition, its presentation, and respawning behavior.
    
-   Example: WeaponPickupData\_Heal\_Small.
    



 |

## Key Equipment Types

| Type | Notes |
| --- | --- |
| EquipmentManagerComponent | 
-   Manages items equipped on a specific Pawn.
    
-   Only one weapon can be equipped on a character at a time.
    
-   Holds bookkeeping of equipped instances. (array of AppliedEquipmentEntry)
    
-   Owned by a Pawn.
    



 |
| EquipmentDefinition (asset) | 

-   Defines things to do to the pawn on which it is equipped.
    
-   List of Actors to spawn at equip time.
    
-   List of Abilities to grant.
    



 |
| EquipmentInstance | 

-   Created when equipped on a Pawn.
    
-   Has OnEquipped / OnUnequipped virtual and Bluerint-implementable functions.
    
-   Holds tag stacks in an FGameplayTagStackContainer.
    
-   Holds the Instigator. (The object responsible for equipping. For the quickbar, this is an InventoryItemInstance.)
    
-   Can access the owning Pawn.
    
-   Subclassing EquipmentInstances exist. (WeaponInstance, RangedWeaponInstance)
    
-   Does not have access to which EquipmentDefinition it was created from.
    



 |
| AppliedEquipmentEntry | 

-   Bookkeeping entry, one per equipped item.
    
-   Pairs the EquipmentInstance with its source EquipmentDefinition.
    
-   Holds items applied to the owning Pawn (granted abilities, spawned Actors.)
    



 |
| RangedWeaponInstance / WeaponInstance | Specializations of EquipmentInstance that do some type-specific internal bookkeeping. |

## Beyond Lyra

Although items in Lyra have both inventory and equipment representations, the systems can function independently.

For example, consider an item the player is given that grants a defensive bonus, such as a magical luck charm. This item may have an inventory definition that specifies a HUD icon and a new fragment type that applies a shielding Gameplay Effect to its owner. Since it's a passive effect that does not need to be equipped, there would be no need for an equipment item definition.
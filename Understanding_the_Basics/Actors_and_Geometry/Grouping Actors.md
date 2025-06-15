# Grouping Actors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/grouping-actors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/grouping-actors-in-unreal-engine)  
**Processed:** 2025-06-14 16:27:00

---

Group Actors together so you can manage multiple Actors at the same time. With Actor groups, you can:

-   Transform grouped Actors as a single unit through rotation, translation, and scaling. Individual Actor transformation is locked while Actors are part of a Group.
    
-   Temporarily unlock a group to transform individual Actors, then lock it again to freeze the Actors inside the group and prevent changes to an individual Actor's transforms.
    
-   Add and remove Actors from a group.
    

An Actor can only belong to one group at a time.

Before you can group Actors together, you need to make sure that the **Allow Group Selection** option is enabled. This option is located in the **Settings** menu on the **Main Toolbar**. You can also toggle this option using the **Ctrl + Shift + G** keyboard shortcut.

![Allow Group Selection option in the Settings menu.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1110ac6-45e6-41d8-a79e-d5c5d48403f0/allowgroupselection.png)

Allow Group Selection option in the Settings menu.

## Grouping Actors

To group two or more Actors together, select the Actors, then do either of the following:

-   Right-click one of the selected Actors to bring up the **context menu**, then select **Group**.
    
-   Use the **Ctrl + G** keyboard shortcut.
    

Actor groups are delineated with green brackets in the **Viewport**.

![An Actor group consisting of four Static Mesh Actors.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bed2434-5e40-4e8f-98c3-14cddb17cf3d/lockedgroup.png)

An Actor group consisting of four Static Mesh Actors. Any transformations will affect all Actors in this group simultaneously.

It is not possible to group Actors that are in different Levels. Moving an Actor that is currently in a group from one Level to another will remove it from the existing group. However, you can move entire groups across Levels.

When you group Actors together, you create a **Group Actor** in the **World Outliner**. To select all Actors in that group, you can select either the Group Actor or any member of the group.

![A Group Actor in the World Outliner.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8301dff-08af-4a26-b793-429beeec77d0/le_groupactor.png)

A Group Actor in the World Outliner.

For more information about Actor selection, refer to the [Selecting Actors](/documentation/en-us/unreal-engine/selecting-actors-in-unreal-engine) documentation.

## Working with Actor Groups

Actor group options are located in the **Group** section of the **context menu** that opens when you right-click a selection of Actors or an Actor group, in the **Viewport** or in the **World Outliner**.

The sections below describe the options for working with groups in Unreal Engine.

### Regrouping

When a selection contains at least one group and other ungrouped Actors, the **Regroup** option becomes available in the context menu.

Regrouping removes all selected Actors from any existing groups, then creates a new group from all selected Actors. Use this option to quickly create a new group out of a selection without needing to manually disband other groups.

You can also use the **Ctrl + G** keyboard shortcut to regroup Actors. This shortcut behaves differently depending on whether you have selected:

-   **No Actor groups:** Ctrl + G creates a new group that contains all of the selected Actors.
    
-   **At least one Actor group:** Ctrl + G performs a regroup, as described above.
    

### Ungrouping

The **Ungroup** option removes all Actors from the selected groups and deletes the groups.

For groups that are unlocked, the ungroup operation will remove the selected Actors from the group without attempting to keep them within any existing group hierarchy.

You can also use the **Shift + G** keyboard shortcut to ungroup Actors and / or nested groups.

### Lock and Unlock Group

The **Lock** and **Unlock** options are available when you are working with an existing group.

By default, newly created groups are in a **locked** state. When a group is in a locked state:

-   If you select any Actor in a locked group, the entire group will be selected.
    
-   Transformations will affect all Actors in the group.
    

If a group is **unlocked**, you can:

-   Select and transform individual Actors that are part of that group.
    
-   Remove Actors from the group.
    

The brackets surrounding a group indicate whether it is currently locked or unlocked. Green brackets signify that the group is locked. Red brackets mean that the group is unlocked.

![Locked group](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f3719d3-5e85-4fe2-afd1-4e06dddb03bd/lockedgroup.png)

![Unlocked group](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2047c21d-0dda-4427-a969-aa4a6d078f91/unlockedgroup.png)

Left: A locked Actor group. The brackets around it are green and the pivot point is at the center of the group. Right: An unlocked Actor group. The rightmost cube is currently selected and can be transformed individually.

### Adding and Removing Actors

The **Add to Group** option is only available after you select one group and other ungrouped Actors. This option adds the ungrouped Actors to the existing group.

The **Remove from Group** option is only available after you select one or more Actors in an unlocked group. This option will remove the selected Actors from the group. If a nested group is removed from a larger group, it still remains a group itself.

If a group contains no Actors, it is automatically deleted, and its Group Actor is removed from the **World Outliner**.

### Transforming Actors and Actor Groups

The **pivot point** of an Actor group is automatically set to the center point of that group. When the group is locked, you can only transform *all* actors inside the group around the group's pivot points. To transform individual Actors around their own pivot points, you must unlock the group first.

To set the pivot point of an Actor group, select the group, then hold down the **Alt** key and **middle-click** at the location where you want to set the pivot point. Alternatively, **middle-click and drag** the sphere at the center of the group's transformation gizmo to move the pivot point.

![Changing an Actor group's pivot point.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8911f515-7aa8-4be9-9c79-30a50efa1f6a/changinggrouppivotpoint.gif)

This GIF illustrates how to move the pivot point of an Actor group, and demonstrates how the Actor group rotates around the new pivot point.
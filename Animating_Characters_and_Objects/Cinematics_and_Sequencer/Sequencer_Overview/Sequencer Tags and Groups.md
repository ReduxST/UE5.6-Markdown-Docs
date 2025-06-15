# Sequencer Tags and Groups

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-tags-and-groups-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-tags-and-groups-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:22

---

Sequencer provides the ability to tag tracks with metadata in order to support additional functions and behavior. Actors can have **Tags** assigned to them, and those tags can be referenced in Blueprints, which enables referencing Actors and tracks more generically. Tracks can also be placed into **Groups**, in order to manage their display and selection.

This page provides an overview of the Tags and Groups features in Sequencer.

#### Prerequisites

-   You have an understanding of **[Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine)**, its **[Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine)**, and how to add **[Tracks](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine)**.
-   You have an understanding of **[Blueprints Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine)**.

## Tags

Tags are metadata markers that you can assign to the **[Object Binding Track](/documentation/en-us/unreal-engine/cinematic-actor-tracks-in-unreal-engine)** in Sequencer, and can be referenced by tag-based Blueprint nodes.

![sequencer tag blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49bd9d5a-9374-435d-a971-16b3c4a857ce/tagoverview.png)

The quickest way to add a tag to a track is by right-clicking it, navigating to the **Tags** menu, and typing a name in the **Add Tag** field. Once done you can either press **Enter** or the **Add (+)** button to create the tag.

![create sequencer tag](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5304fed7-73be-410e-9599-dbee39fbe94a/createtag.png)You can have more than one tag assigned to an Actor. ![multiple tags](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4061d76-509f-48bb-af3b-858fa0d34015/twotags.png) 

Once a tag is assigned, the **Tags** context menu will now show the list of tags added to the track. They can be toggled on and off by clicking them.

![enable disable tag menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd224adf-fc31-4830-9225-748534e5aa99/toggletags.gif)

### Binding Tag Manager

To view and manage your tags in Sequencer, you can open the Binding Tag Manager by clicking **Open Binding Tag Manager** in the Tags context menu. You can also open it from the toolbar's [**Actions**](/documentation/en-us/unreal-engine/cinematic-tags-and-groups-in-unreal-engine#actions) menu.

![sequencer binding tag manager](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/430d477a-02af-4ce8-848f-c86e050dd1b3/opentagmanager.png)

The Binding Tag Manager has two main areas:

![binding tag manager](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8be0e7a-0fe5-44c2-abac-b29fd8ce6d42/tagmanager.png)

1.  The first area contains a list of all object bindings in the sequence, including any subsequences. Tags assigned to Actors are displayed next to them, and can be unassigned by clicking **Delete (X)** on the tag. New tags can be added by right-clicking a binding, typing in a name, and pressing **Enter**.
    
    ![tag manager create tag](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d652333e-5388-4189-be07-b979b336efe6/createtag2.png)
    
2.  The second area lists all existing tags for this sequence. Clicking **Delete (X)** will unassign it from all bindings.

### Referencing in Blueprints

Binding Tags can be accessed in Blueprints by calling one of the "by Tag" **Binding** functions from **Level Sequence Actors**. You can use these functions to get the current binding or bindings of Actors with tags, rebinding those Actors, or resetting bindings.

"By Tag" binding functions can be found by right-clicking in the Blueprints graph or by dragging off from a Level Sequence Actor reference and locating them within **Sequencer > Player > Bindings**.

![binding by tag blueprints](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62ca39e3-5ae3-4374-a055-b6d71acc0252/bindingtagnodes.png)

Most of the "by Tag" Blueprint functions have the following input pins:

![add binding by tag](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/594475b0-ce78-4314-8281-6e62c0c6ea79/examplebp.png)

-   **Target**: The reference to the Level Sequence Actor.
-   **Binding Tag**: The Tag name to look for.
-   **Actor**: The Actor to bind, rebind, or add binding to.
-   **Allow Bindings from Asset**: Disabling this will lock the sequence from further binding actions.

## Groups

Tracks in Sequencer can be added into groups, which aid in quick selection and display filtering.

To create new groups and add tracks to them, right-click a single track or multiple tracks, and select **Add to Group > New Group**. This will open the **Sequencer Group Manager** and create the new group and add the tracks to it.

![sequencer add to group new group](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57963ca9-3b3d-4c00-98e1-77083388eb2c/newgroup.png)

With a new group created, new tracks can also be added to that group from the **Add to Group** context menu.

![add to group](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/551922b9-e220-4fe1-9329-7df699b2ab3f/addgroup2.png)

You can also drag tracks from Sequencer's outliner into the Sequencer Group Manager to add tracks to groups.

![add group drag and drop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3e4353c-7794-4e04-9308-bf3f6edd815d/addgroup.gif)

### Group Manager

The Sequencer Group Manager is where you manage your groups and tracks that are assigned to them. If you are not creating a new group, you can open it by clicking **Open Sequencer Group Manager** in the toolbar's [**Actions**](/documentation/en-us/unreal-engine/cinematic-tags-and-groups-in-unreal-engine#actions) menu.

![open sequencer group manager](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98f933ca-767e-4a60-80a0-94819b649039/opengroup.png)

#### Management

Right-clicking in the Group Manager window will show the context menu, where you can create new groups, rename your group, delete groups, or [**Filter Groups**](/documentation/en-us/unreal-engine/cinematic-tags-and-groups-in-unreal-engine#filtering).

![group manager context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c79f3b68-7e81-4f19-b791-4ece92480c81/groupcontext.png)

#### Selection

You can quickly select the contents of a group by clicking the group header, or by clicking each group item individually.

![sequencer group selecting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea559daf-74e0-4ba2-a0b1-1b04bd3fe423/selectgrouptracks.gif)

#### Filtering

Clicking the **Filter** icon will filter all tracks out in the Sequencer outliner except for the tracks (and their children).

![sequencer group track filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5dc3413b-222b-4c8a-8c5b-7f53b1eace06/filter1.png)

Clicking the **Filters** menu in Sequencer's outliner will also display controls for enabling **Group Filters**.

![sequencer group track filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfb33df4-931c-4741-a772-8b9a4f194d27/filtermenu.png)
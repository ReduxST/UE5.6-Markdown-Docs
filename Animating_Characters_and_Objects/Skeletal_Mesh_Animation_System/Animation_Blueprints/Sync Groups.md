# Sync Groups

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-sync-groups-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-sync-groups-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:40

---

To improve blending behavior in **Animation Blueprints**, **Sync Groups** can be used to automatically synchronize the related animation's lengths and playback during the blend. This can be useful when blending between walking and running cycles of different lengths. In such a case, directly blending from one to the other without Sync Groups could cause unnatural results as the feet placement may not be synchronized.

This document provides an overview of the Sync Group system in Animation Blueprints.

#### Prerequisites

-   Sync Groups are created and managed in [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine), therefore you should have a basic knowledge working in this editor.

## Overview

Sync Groups work with the concept of roles, in which one animation is the **leader** while all other animations are **followers**. Leaders provide the master animation length that is used by all followers and have priority for triggering [Animation Notifies](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine). Followers match their animation lengths to leaders and have their notifies suppressed.

By default during the blend, leader and follower assignment can change based on the weight distribution. The animation with the highest blend influence is considered the leader.

| Image | Description |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4a6fb6d-6eda-4c04-9134-c754cf78a211/concept1.png) | As an example, you can compare a walk and run cycle animation. Typically these animations may not match in length. Without Sync Groups, the general body movement cycles of these animations will not align. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/317656e2-1196-46e7-8018-feac58409260/concept2.png) | When using Sync Groups, and with the **run cycle as leader**, this will cause the walk cycle to adjust its playback speed to match the leader. In this case, the walk cycle is being shortened to play faster to match the run cycle. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06a666f7-bdd8-4149-9c3a-a45e85587f63/concept3.png) | When using Sync Groups, and with the **walk cycle as leader**, this will cause the run cycle to adjust its playback speed to match the leader. In this case, the run cycle is being lengthened to play slower to match the walk cycle. |

Due to the nature of synchronizing animations with Sync Groups, there are certain animation restrictions that you should consider when using animations in this way:

-   Ensure that all animations being synchronized have the same general body movement from the start to the end. For walk and run animations, this might mean ensuring that the same feet are being planted at the start and ending frames.
    
    ![synchronize foot placement](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab16adb5-34c1-467c-bb56-9423152b698c/footsync.png)
-   Also ensure that there are no drastic length differences between the animations that are blending. This may result in some animations playing noticeably faster than others, as well as causing noticeable playrate "pops" when leader and follower animations switch.
    

### Sync Settings

When syncing animations in a variety of ways, you can edit the behavior with the following settings found in the **Details** panel.

| Name | Description |
| --- | --- |
| **Group Name** | Defines the name of the Sync Group. Generally, you will want all related animations that are meant to blend together (such as body motions for sneak, walk, run, sprint) to have the same name, causing them to be in the same Sync Group. |
| **Group Role** | 
Specifies certain leader and follower rules for this animation. You can select from the following:

-   **Can be Leader**, which is the default behavior, and when selected causes this animation to be the leader as long as it has the highest blend weight.
-   **Always Follower**, which causes this animation to always follow the Sync Group leader. If all animations are set to this, then the first animation evaluated will be set to the leader.
-   **Always Leader**, which causes this animation to always be the leader. If more than one animation in the group is set to this option, then the last one evaluated will be set to the leader.
-   **Transition Leader**, which causes this animation to be excluded from syncing while blending in. Once blended in it will become the Sync Group leader until blended out.
-   **Transition Follower**, which causes this animation to be excluded from syncing while blending in. Once blended in it will become a follower until blended out.



 |
| **Method** | 

Defines how syncing is determined. You can select from the following:

-   **Do Not Sync**, which is the default setting and causes no animation syncing to occur.
-   **Sync Group**, which will enable [Group-Based Syncing](/documentation/en-us/unreal-engine/animation-sync-groups-in-unreal-engine#group-basedsyncing).
-   **Graph**, which will enable [Graph-Based Syncing](/documentation/en-us/unreal-engine/animation-sync-groups-in-unreal-engine#graph-basedsyncing).



 |

## Sync Group Types

There are several ways to set up Sync Groups, you can choose from the following types.

### Group-Based Syncing

**Group-Based Syncing** groups animations together by name. To create a group-based Sync Group, select the animation nodes to sync in the **AnimGraph** and locate the **Sync** category in the **Details** panel. Set the following properties:

-   Set **Method** to **Sync Group**.
    
-   Type a name in **Group Name**. The **Group Name** must match for all animations you want to sync.
    

![sync group name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fed3c2a-2099-4da7-abc3-a0345f0939b9/syncgroup1.png)

Your animations now sync when blending. You can preview this behavior by connecting them to a **Blend** node and setting the **Alpha** to 0.5.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74698710-d904-4e0d-8ed9-e5bc7693eb56/syncoff.gif) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ea31945-f647-4779-aa96-234c72b594db/syncon.gif) |
| Group Sync Off | Group Sync On |

When using Sync Groups with Animation Nodes, the node will display a text watermark for the sync method, and the group name.

![sync group watermark](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c12dea05-1e65-4ba7-8e3b-781f73e240ce/syncgroup2.png)

### Marker-Based Syncing

In addition to Sync Groups, animations can be synchronized using **Sync Markers** within Animation Sequences. This causes the playback of animations to synchronize based on the relative position of playback between markers placed along the timeline of animations.

This can be useful for a variety of blending conditions:

-   When general body movement does not have a matching number of steps. For example, when blending a run cycle that has the right foot touching the ground four times, and the walk cycle's foot only touches the ground two times.
-   When the stride lengths are not the same. For example, when blending a time-rigid marching walk animation to a time-loose scramble running animation.
-   When blending with non-looping animations, such as run and walk starts and stops. Additionally with this case, the start and stop animations should be set to **Always Leader**.

![sync markers](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad8001da-c9c9-460b-a373-3e4b37252ff4/markers1.png)

To add a Sync Marker, right-click within an [Animation Notify](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine) timeline and select **Add Sync Marker...** > **New Sync Marker…**. Next, type in the name of the Sync Markers and press **Enter**.

![create sync marker](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a3c4442-487d-4c2d-b098-3babe9be83e4/markers2.png)

Once a Sync Marker has been added, it will be saved to the Skeleton. Once added, you can easily reuse Sync Marker names on different animations, ensuring that the same names are being used and standardized. Saved Sync Markers can be added by right-clicking in the notify timeline and selecting **Add Sync Marker...** > **Existing Sync Markers**, then selecting a Sync Marker from the list.

![add existing sync marker](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67331a97-4899-4ed3-a238-188e71d03c06/markers3.png)

Sync Markers will only synchronize with other markers if the animations are in the same [Sync Group](/documentation/en-us/unreal-engine/animation-sync-groups-in-unreal-engine#group-basedsyncing). This means you must ensure that both Sync Marker and Sync Group names match.

[Animation Montages](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine) also support marker-based syncing while blending out, so you can transition back to other animations seamlessly. In the Animation Montage Editor, navigate to the **Sync Group** properties in the **Asset Details Panel** to edit the relevant sync properties.

![animation montage sync settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/239f5f76-52ad-4921-8cd1-39c41a256ee1/markers4.png)

Other elements to consider when using Sync Markers are:

-   Only markers common to all animations within a group are synced. For example, if one animation is missing "Right Foot Down" markers, then those markers will be ignored for all animations when determining that frame's position.
-   Marker-based syncing is used automatically when animations in a Sync Group have matching markers. Otherwise, the system will fall back to normal length syncing behavior.

### Graph-Based Syncing

When building complex Animation Blueprints, it can become tedious to manage name-based sync groups. You can instead use **Graph-Based Syncing** to propagate a single Sync Group to various sub-graphs and child nodes. Graph-Based Syncing requires children nodes and graphs that have their **Method** property set to **Graph**.

![graph method](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acc4d2e5-b27a-4cfa-b77d-c1563028125a/graph1.png)

The first method of using Graph-Based Syncing is by creating the **Sync** node. This node propagates sync behavior to all incoming pose nodes that have their **Method** property set to **Graph**. To add a Sync node to your graph, right-click and select **Sync** from the **Misc.** category.

![create sync node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d07d6d3-a186-42b0-a4d3-afa90ce15cd2/graph2.png)

Typically, you may want to place this node after your pose logic, so that it can synchronize all incoming animation data.

![synchronize incoming pose](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09408e11-9b0f-453f-8f0e-c710c5f831b0/graph3.png)

#### Blend Space Graphs

In addition to the Sync node, [Blend Space Graphs](/documentation/en-us/unreal-engine/blend-spaces-in-animation-blueprints-in-unreal-engine#blendspacegraph) also provide graph syncing functionality. This will cause the sync behavior to propagate to all children samples within the graph.

Similar to the Sync node, Blend Space Graphs require a **Group Name** in order for the sync behavior to propagate.

![blend space graph sync](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2ead372-e7b1-401a-9a67-86aa62e302d9/graph4.png)

By default, **Sequence Players** generated in Blend Space Graph samples will default to using the **Graph** sync method, to accept synchronization from the Blend Space Graph node.

![blend space graph sync](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e81a3b2-16e3-4601-9482-78be646b9d21/graph5.png)
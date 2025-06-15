# Animation Blueprints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:51

---

**Animation Blueprints** are specialized **Blueprints** that control the animation of a **Skeletal Mesh** during simulation or gameplay. **Graphs** are edited inside of the **Animation Blueprint Editor**, where you can blend animation, control the bones of a Skeleton, or create logic that will define the final animation pose for a Skeletal Mesh to use per frame.

This document provides an overview of how to create an Animation Blueprint, its editor, and its primary features.

#### Prerequisites

-   Your project contains a [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-actors-in-unreal-engine).

## Animation Blueprint Creation

You can create Animation Blueprints in the following ways:

In the **Content Browser**, click **Add (+)**, then select **Animation > Animation Blueprint**. You will then be prompted to specify which **Skeleton** to target for the Animation Blueprint. Select one and click **Create**.

![create animation blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6368083b-2787-4801-bf9f-2a60bc1e6952/create1.png)

For this creation method, you can optionally specify a **Template Animation Blueprint**, and **Parent Class**, if you are wanting to create a child Blueprint. For more information about templates, visit the [Animation Blueprint Linking](/documentation/en-us/unreal-engine/animation-blueprint-linking-in-unreal-engine) page.

Animation Blueprints can also be created by right-clicking on a **Skeletal Mesh Asset** in the **Content Browser** and selecting **Create > Anim Blueprint**.

![create animation blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce31777e-98db-405a-a926-be56ff72fc98/create2.png)

Once created, double-click your new **Animation Blueprint** to open it in the **Animation Blueprint Editor**. To learn more about the interface, toolbar, and sections of this editor, refer to the [Animation Blueprint Editor](/documentation/en-us/unreal-engine/animation-blueprint-editor-in-unreal-engine) page.

### Assigning to Characters

Animation Blueprints on their own will not affect your characters until you assign them. Typically this is done on the Skeletal Mesh of your character, regardless if it is referenced in a level or as a component in Blueprints.

To assign your Animation Blueprint, select your Skeletal Mesh and set the following properties:

-   Set **Animation Mode** to **Use Animation Blueprint**.
-   Set **Anim Class** to your Animation Blueprint asset.

![assign animation blueprint to character](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7db83be-d012-4836-820b-154ba35fd181/assign1.png)

## Working with Animation Blueprints

There are several features and workflows available to you when using Animation Blueprints. From creating animation logic using the **AnimGraph**, to using **Linked Anim Instances**, Animation Blueprints provide a powerful suite of tools for you.

Reference the following pages to learn how to create robust Animation Blueprint logic for your characters.
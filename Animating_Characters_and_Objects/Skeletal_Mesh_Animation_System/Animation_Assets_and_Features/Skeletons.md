# Skeletons

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletons-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletons-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:53

---

A **Skeleton** is a hierarchy that is used to define **Bones** (sometimes called **joints**) in a [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-actors-in-unreal-engine). In some ways, these Bones mimic a real biological skeleton due to their position and control over how characters deform.

In Unreal Engine, Skeletons are used to store and associate animation data, the overall skeletal hierarchy, and [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine). Skeleton Assets can also be shared through a variety of methods, enabling for additional animations and data to be shared between different Skeletons.

This document provides an overview of how to create and use Skeletons.

#### Prerequisites

-   Your project contains a [Skeletal Mesh Actor](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine), or you have a skinned FBX character to import into Unreal Engine.

## Creating Skeletons

The primary way to create a Skeleton is to [import](/documentation/en-us/unreal-engine/importing-skeletal-meshes-using-fbx-in-unreal-engine) a skinned character FBX, which then converts to a **Skeletal Mesh** in Unreal Engine. When importing a Skeletal Mesh, in the [FBX Import Options](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine#skeletalmeshoptions) window, leaving the **Skeleton** field empty will automatically create a Skeleton Asset based on the skinned character being imported.

![import skeletal mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/101eee60-2819-46a9-8b5f-0dbace2b031c/create1.png)

After importing your character, the **Skeleton Asset** will be created along with other Skeletal Mesh Assets.

![skeleton asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f196ffb6-2015-4f20-9108-b8603baf4950/create2.png)

You can also create a copy of a Skeleton from any Skeletal Mesh by right-clicking on it in the **Content Browser** and selecting **Skeleton > Create Skeleton**. This creates a new Skeleton associated with an existing mesh. If that mesh had another Skeleton associated with it, it will re-link to the new Skeleton and any animations will then link to the new Skeleton.

![create skeleton copy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a8a3fe5-e37b-43e4-8a87-c10e1d183d77/create4.png)

Double-click the Skeleton Asset to open the [Skeleton Editor](/documentation/en-us/unreal-engine/skeleton-editor-in-unreal-engine).

![skeleton editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02632093-d6bd-4931-b41c-fad7b6919fc7/create3.png)

## Skeleton Tree Information

Bones and other items displayed in the [Skeleton Tree](/documentation/en-us/unreal-engine/skeleton-editor-in-unreal-engine#skeletontree) can appear different depending on several factors.

| Icon | Description |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d1ceac6-7230-4bd6-803d-dd66b9a429d0/iconbone1.png) | A normal Bone that influences vertices on the Skeletal Mesh. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8464629f-e39c-446f-a866-07f8ee6457f5/iconbone2.png) | A Bone in the current Skeleton that doesn't influence vertices on the Skeletal Mesh. These Bones are typically used in an auxiliary manner, such as for attaching weapons or props, while still being animatable as a Bone. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3114f51f-0a57-40a8-936d-93ecdbd045fd/iconsocket.png) | A [Socket](/documentation/en-us/unreal-engine/skeletal-mesh-sockets-in-unreal-engine), which is a static point that acts as an offset attachment point for Bones. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/995c20c0-4ebd-43d0-bc5b-ab9f0c5a37a2/iconvirtual.png) | A [Virtual Bone](/documentation/en-us/unreal-engine/virtual-bones-in-unreal-engine), which is a Bone that follows the transforms of another Bone, but in a different Bone space. These are useful for locking down unwanted joint movements, and are used in conjunction with [IK](/documentation/en-us/unreal-engine/animation-blueprint-two-bone-ik-in-unreal-engine). |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac91c5ff-644c-405c-b5cd-a101215ffd72/iconnobone.png) | A Bone that exists in the Skeleton, but is not used by the current Skeletal Mesh. This can happen if you have [merged](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine#mergingduringimporting) Skeletons, or are previewing different LODs on this Skeleton that are not using certain Bones. |

## Animation Data Storage

In addition to controlling animation, Skeletons in Unreal Engine also store animation-specific data. When data is created from those sources, such as creating an [Animation Notify](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine) in an Animation Sequence, it gets added to the Skeleton as shared data.

Skeletons store the following types of animation data:

-   [Animation Notifies](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine).
-   [Animation Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine).
-   [Slots](/documentation/en-us/unreal-engine/animation-slots-in-unreal-engine).
-   [Retarget Sources](/documentation/en-us/unreal-engine/retarget-manager-in-unreal-engine).
-   [Blend Profiles and Blend Masks](/documentation/en-us/unreal-engine/blend-masks-and-blend-profiles-in-unreal-engine).

This data can be viewed in dedicated tool panels by clicking **Window** in the Skeleton Editor menu, then enabling one or more of these panels.

![animation data panels](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bc67964-27ad-4147-8492-4f4017c0b7b7/data1.png)

## Sharing Skeletons

An important feature of Skeleton Assets is that a single Skeleton Asset can be used by multiple Skeletal Meshes, so long as the Skeletal Meshes use the same general rig hierarchy. This means that the names and hierarchical order of your Bones must be consistent in order for sharing to work correctly.

For example, consider a limb with three Bones in a Skeletal Mesh. The bones are named **1**, **2**, and **3**:

![sharing skeleton example 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5346f4e2-90a1-4a85-8cb2-0e4ee0936c17/shareexample1.png)

If you want to share this Skeleton with another Skeletal Mesh, you will need to keep these Bones in the same order and with the same names. The second Skeletal Mesh, however, can contain Bones that are additions or peripheral to the hierarchy. Any time animation data is received for a Bone that is not included in the Skeletal Mesh, that animation data will be ignored.

In that case, your new hierarchy could look like the image below. Here, the second Skeletal Mesh has extra Bones, while still retaining and not interfering with the original hierarchy from the first Skeletal Mesh.

![sharing skeleton example 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68cd3554-c706-4a78-928b-f784da752737/shareexample2.png)

However, in order for both Skeletal Meshes to use the same Skeleton Asset, you cannot change the hierarchy order or rename the Bones. If a second Skeletal Mesh uses a different Bone hierarchy and naming structure, you will need to create a new Skeleton Asset.

![sharing skeleton example 3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7523b3d6-bac7-44fe-98cc-87bcc6c16fd1/shareexample3.png)

If you insert a bone into the hierarchy without changing the order, you will be able to share successfully. However in most cases the extra bone may cause unintended transform offsets in your skeleton. It is recommended that you avoid this if possible.

![sharing skeleton example 4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df64b287-d751-43de-8cde-88fe4a0fca25/shareexample4.png)

Taking these sharing rules into account, there are several ways you can share Skeletons between Skeletal Meshes in Unreal Engine. These are detailed below.

### Merging during Import

The first method for sharing Skeletons is done during the FBX import process. When importing your new Skeletal Mesh (with additional and peripheral Bones compliant with the rules above), you can select a Skeleton from a Skeletal Mesh that already exists in your project. Unreal Engine will then merge the Skeletons, appending any new Bones into the hierarchy. Additionally, your Skeleton's proportions will be defined by the original Skeletal Mesh from which it was created.

![merge sharing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5294fb2a-d242-420f-9410-2da638aa16b8/share1.png)

If you are importing a Skeleton that is vastly different from the Skeleton you are attempting to merge to and breaks any sharing rules, you will see an error message:

![failed to merge bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f716072-e26f-4cdb-b1ca-e7f0097a37c3/share2.png)

In this case, you may need to create a new Skeleton Asset for the Skeletal Mesh you are importing, rather than merge into an existing one.

When viewing your merged Skeleton, you will see these additional Bones listed in your hierarchy, but they will only be visible and active for the Skeletal Mesh they are intended for.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecbe6152-00e4-4769-b6f9-3e76ca974bbc/sharevar1.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb0530cc-7c3d-49ab-bc08-16b825e9e7ce/sharevar2.png) |
| Skeletal Mesh Variant 1 | Skeletal Mesh Variant 2 |

### Compatible Skeletons

Additionally, skeletons can non-destructively share animation assets by defining other skeletons as compatible. Compatible skeletons can share [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine), [Montages](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine), [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine), and more.

To define another skeleton as compatible for a character, open the character's skeleton asset in the [Skeleton Editor](/documentation/en-us/unreal-engine/skeleton-editor-in-unreal-engine), and then open the **Retarget Manager** by clicking the button in the **Toolbar**.

![compatible skeletons](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3a226d6-cdf6-4d5e-b2e6-43338d9b127b/retargetman.png)

In the **Retarget Manager**, locate the **Manage Compatible Skeletons** section of the **Retarget Sources** panel and click **Add Skeleton** to select another skeleton asset in your project using the context menu.

![add compatible skeleton](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6226667a-f33e-4767-af6c-51501a03293e/selectcompatibleskel.png)

Now, animations can be shared from the Skeleton that was added to the **Manage Compatible Sources** list.

![compatible skeletons](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a87c578-64ab-450b-bd45-ee2857e4c5f7/compat3.gif)

Skeleton compatibility is bi-directional. If you set Skeleton 1 to be compatible with Skeleton 2, that also means that Skeleton 2 is now compatible with Skeleton 1.

Creating and managing a system of compatible skeletons can be an effective way to optimize the number of animation assets your project requires to animate multiple characters. However, in order to utilize the Compatible Skeletons system, all characters must have nearly identical skeleton hierarchy structures and naming conventions. Additionally, all characters must have similar mesh proportions to achieve ideal results.

To share animations across characters with the same skeleton structure but with different proportions see the [Animation Retargeting](/documentation/en-us/unreal-engine/animation-retargeting-in-unreal-engine) documentation.

To rebuild animation sequences to work across characters with radically different skeleton structures, see the [IK Rig Retargeting](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine) documentation.

## Skeleton Features

Skeletons in Unreal Engine support a variety of features for attaching, blending, and other settings. Refer to the following pages to learn more about these features:
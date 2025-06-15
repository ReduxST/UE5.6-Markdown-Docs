# Animation Modifiers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-modifiers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-modifiers-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:14

---

**Animation Modifiers (Anim Modifier)** are a type of native or [Blueprint Class](/documentation/en-us/unreal-engine/blueprint-class-assets-in-unreal-engine) that enable users to apply a sequence of actions to an [Animation Sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) or [Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) asset. An example of this includes (but is not limited to) creating automatic foot sync markers by pin-pointing on which frames the right or left foot is place on the ground. Using this information, **Animation Sync Markers** can be added to frames where a foot bone is at its lowest point (or touching the floor).

Above an Anim Modifier is used to generate auto foot sync markers.

Accessing and applying Anim Modifiers is performed in either the **Animation Editor** or **Skeleton Editor** under the **Animation Data** tab. When applying an Anim Modifier to a Skeleton, the modifier is applied to all Animation Sequences that are based on the Skeleton. When applying the modifier to an Animation Sequence, it is only applied to the sequence itself and no other sequences.

## Creating an Anim Modifier

To get started, you will need to create an Anim Modifier Blueprint class:

1.  In your project's **Content Browser**, click the **Add New** button and select **Blueprint Class**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/443791d5-f981-48d3-ac6a-d27daebf7935/create_01.png)
2.  In the **Pick Parent Class** window, expand **All Classes** and search for and select **Animation Modifier**, click **Select** then give it a name.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e46ab06-ba62-413e-8951-a71f97c77703/create_02.png)
3.  Double-click the new Animation Modifier Blueprint to open it up in the Blueprint Editor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0f006e1-fb1a-46bc-af3a-4cc5773eb0fd/create_03.png)

With your Anim Modifier created, you can now use Blueprint Script and functions contained with the **Animation Blueprint Library** to access and manipulate animation data.

### Animation Blueprint Library

Right-click in the graph of the Anim Modifier Blueprint to see the context menu and list of functions available, particularly under the Animation Blueprint Library.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bae6202d-f1a9-4fbe-99e0-ac6d0e114c3d/animbplibrary.png)

In the image above, functions related to Marker Syncing are expanded which enable you to synchronize animations using marker data.

Before working with the various functions available for accessing data, you will want to implement the **OnApply** and **OnRevert** events. The OnApply Event enables the user to change, add or remove data from the animation while the OnRevert enables the user to remove previously applied user changes (or return the sequence to its original state). Each event returns the Animation Sequence in which to feed the Animation Blueprint Library operations.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/114d3407-dcee-4510-985d-8a2420a40b47/eventnodes.png)

In the image above, when the Anim Modifier is applied, a new Notify track is created with the defined name while reverting the Anim Modifier, the track is removed.

## Implementing an Anim Modifier

Implementing an Anim Modifier can be done inside a **Skeleton** asset (to add to the Anim Modifier to all animations associated with the Skeleton) or in a single Animation Sequence.

1.  Inside the **Skeleton Editor** or **Animation Editor**, go to **Window** menu option and select **Animation Data Modifiers**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/916caef4-70b7-4599-ac2c-15f89fa249af/implement_01.png)
2.  In the **Animation Data Modifiers** tab, select **Add Modifier** and select your desired **Anim Modifier Blueprint**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ea153fc-c554-4c85-9bfc-7c22fc953612/implement_02.png)
3.  Right-click on your Anim Modifier Blueprint then click **Apply Modifier** to apply the Anim Modifier and any changes (or **Revert Modifier** to remove changes).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4ed37d2-5688-47dd-a312-f126d22aa9ec/implement_03.png)
    
    Your Anim Modifier will be listed as **Out of Date** until you apply it.
    
    Below is an example of an Anim Modifier that has been applied to a Skeleton asset, indicated by the Skeleton icon.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93c4925a-4658-4274-a592-c122cbc01caf/skeletonmodifier.png)

Any properties that you have set as **Instance Editable** will be available to edit in the **Animation Data Modifiers** tab.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4505d55-3720-4230-ab3e-2a79a6651620/implement_04.png)

In the image above, we define properties that can be used to drive automatic foot syncing.

### Exposing Properties

Inside your Anim Modifier Blueprint, you will want to expose parameters using **Instance Editable** that you can manipulate within the **Animation Tab** in the Animation Tools

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0551057f-6d7c-4ee5-983f-c4554f17f504/instanceeditable.png)

In the image above, we use a structure variable containing information that we can set for the name of a bone as well as provide an offset.

Inside our Animation Sequence when we implement our Anim Modifier and apply it, we can see our exposed parameters.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1a38b79-4d30-411f-a21f-0e11aac074d7/animdatavariables.png)

In the image above, we enter the names of the bones that we want to include in our Anim Modifier in which to gather animation data (such as Bone Transform) from.

## Animation Blueprint Library Reference

While there are several different nodes available within the Animation Blueprint Library, this section lists some of the more commonly used types within Anim Modifiers.

### Add/Remove Notify and Curve Tracks

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3188f19b-31f2-4aeb-a8b3-117133bb1275/notifiesandcurves.png)

These nodes enable you to dynamically add Notify or Curve Tracks to the specified Animation Sequence. Once Notify or Curve Tracks have been added, you can add various types of keys or events to those tracks. For example, you may want to **Add Float Curve Keys** to a Curve Track, **Add Animation Notify Events** or **Add Animation Sync Markers** to a Notify Track.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae80910e-1ef1-4ffe-884c-1f20736fbb99/addmarkers.png)

### Get Bone Pose

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/372ab175-306d-4453-87d6-99d60a3f095f/getpose.png)

To get Bone Transform data you can use the **Get Bone Pose for Frame** or **Get Bone Pose for Time** nodes which will return the Bone Transform for the provided Animation Sequence with the specified Bone Name. Alternatively, you can use the **Get Bone Poses for Frame** or **Get Bone Poses for Time** to collect Bone Transforms for a specified array of Bone Names.

When getting Bone Transforms the transform data will be in local space. If you need it to be in component space, you will need to manually convert the transforms.

### Helper Nodes

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6889b362-7867-4054-8fc7-c2071ad8b8f5/helpernodes.png)

The Animation Blueprint Library nodes include several helper nodes including nodes for converting frame and time information (**Get Time at Frame** or **Get Frame at Time**). Another node that is useful for getting information is the **Find Bone Path to Root** which will take an Animation Sequence and a Bone Name (typically the Root Bone) and output a list of Bone Names in a chain.
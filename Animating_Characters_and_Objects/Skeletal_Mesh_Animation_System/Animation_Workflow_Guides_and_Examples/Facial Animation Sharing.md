# Facial Animation Sharing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/facial-animation-sharing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/facial-animation-sharing-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:12

---

![FacialAnimationSharing.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c3398cd-7f46-4c23-9fb1-5b5079feaded/facialanimsharingbanner.png "FacialAnimationSharing.png")

If you have multiple characters in your project that are similar and share the same Skeleton Asset, you may want to consider using curve driven animations for facial expressions. When doing so, you can share thoseanimation curves and drive them with Pose Assets to produce your desired facial expressions and even share them across multiple Skeletal Meshes. 

One important caveat however is that your animation must not have any bone transform data within it. Any bone transform data, even with one mesh's reference pose, won't work for other meshes so it is important to remove bone transforms (keeping only curves) and start with each mesh's own reference pose if you want to share the curve between different meshes. This enables you to share the facial curves between different faces. 

The following is an example workflow, your workflow may differ based on your assets and desired results.

## Create and Use a Master Skeleton

The first thing you will want to do is to import a base Skeletal Mesh and create a Skeleton Asset that will be considered as your Master Skeleton (which every other Skeletal Mesh that you want to share facial animations with will use). Any additional meshes that you import should have the same bone hierarchy and naming convention in order to share the Skeleton asset.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80d850f7-9c8c-4b56-8a05-c7d60bfdf082/masterskeleton_01.png "MasterSkeleton_01.png")

Please see the [Skeleton Assets](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) documentation pages for more information on Skeletons.

## Create a Pose Asset

The next thing you will want to do is inside your DCC, bake out your poses to an FBX sequence and import the FBX into Unreal Engine. This will give you an Animation Sequence containing each of the curves at their min/max blend values. 

Click image for full view.

Above, our imported animation sequence contains all curves and their max values at a given frame.

Once you have imported your sequence containing all your curve data, you can create a [Pose Asset](/documentation/en-us/unreal-engine/animation-pose-assets-in-unreal-engine) from that animation sequence which can be used to translate the animation curve data into actual facial animation on the character. 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b023261-d93b-4c5e-a952-906dc2ecfcfe/animationsequence_02.png "AnimationSequence_02.png")

You can right-click on an Animation Sequence and create a Pose Asset from it from the context menu.

Inside your Pose Asset, you will need to define the Pose Names by entering in each name manually or by copying and pasting data stored from your clipboard. 

Here we have a list of all the poses identified in our 58 frame animation sequence containing our poses that we imported: 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13d241eb-f4e7-42c5-bb39-37482c9f4ff9/facial_poses.png "Facial_Poses.png")

We can then apply these as the names of our poses in our Pose Asset: 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2e640af-720a-4e31-9628-b7f68faaa605/poseassetblank.png)

You will then see these curves in the **Anim Curves** window which is stored along with the Skeleton Asset. 

Click image for full view.

Every character that uses the Master Skeleton would then have access to these curves and can drive their own facial animation by the different values represented in each curve while the Pose Asset translates all of the curve data to the actual animation pose the character takes. 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47a581dd-1b46-4c8b-b237-ee2e0a853a1d/animationsequence_03.png "AnimationSequence_03.png")

*Above, we changed the default value of the jaw\_open\_pose from 0 to 1 resulting in the character opening its mouth.*

When entering your Pose Names inside the Pose Asset, it is generally a good idea to delete unused curves from the **Anim Curves** window to minimize the amount of unused curves from being displayed.

Below in our Pose Asset we can see all of our Pose Names which are also displayed in the Anim Curves window:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d2b5489-9370-4e73-86ac-a8706c7f222e/poserename1-1.png "PoseRename1-1.png")

When we change **Pose\_0** to **l\_eye**, **Pose\_0** remains as a curve in the Anim Curves which we can delete by right-clicking on it and selecting **Delete Curve.**

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ccbeb58-2b66-4d98-a615-9e19a6646267/poserename2.png)

## Establish Parent/Child Animation Blueprints

Once you have a Pose Asset, you'll want to create an **Animation Blueprint** for your character that utilizes a curve driven animation, and finally, a **Pose Asset** node (assigning your Pose Asset) to correctly translate the curve data into poses the character can use. 

Click image for full view.

If you plug the curve driven animation directly into the Final Animation Pose, the Animation Pose will not now how to translate the curves into pose data. This is where the Pose Asset node comes in and intercepts the animation, properly translating the curves into actual pose data that the character can use. 

When you have additional characters, if you create and assign them Child Animation Blueprints from this Master Animation Blueprint, you can override the Pose Asset with unique Pose Asset data for each character. This allows for the character specific deltas to be achieved, ensuring that a scream for example looks correct on varying proportions. 

Click image for full view.

Above we have an additional character that is using a Child Animation Blueprint based on our Master.

Inside our Child AnimBP, we have overridden the Pose Asset to use one that is specific to this character, enabling us to use the deltas to drive facial poses specific to this character and the animation that is played comes from our parent.

## Bringing In Animations

When you start to bring in facial animations for your characters, typically you'll want some body animation that is driven by bones in the character in addition to the curve driven facial animation. In order to share body animations but drive facial animations through curves, you will need to remove any Bone Tracks from the facial animation leaving only curves or use an Animation Modifier to remove specified Bone Tracks and drive curves for the face. 

How would this work? For example, take the Animation Sequence below: 

![BringInAnimation_01.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0bee62d-1b56-4152-8f63-8a09ecd83ac3/bringinanimation_01-resize885x625.png "BringInAnimation_01.png")

Our Animation Sequence contains all the curves and keyed values for those curves representing varying facial poses. The problem however is that the curves would also be playing on top of any bone driven animations which would result in double transforms and incorrect results. In this case you would want to remove those Bone Transforms, leaving only the curves. 

You can Remove All Bone Tracks from the Asset menu under animation: 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5ce85cd-8697-4136-b050-cee3cc111045/bringinanimation_04.png "BringInAnimation_04.png")

You can also use Animation Modifiers to remove certain bones only if you want to share body animations but drive curves for the face. Typically you'll want to have a bone driven body animation, but curve driven facial animations in which case we opted to use an Animation Modifier. 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a30cab7e-fda1-437a-a802-504ff51788fc/bringinanimation_02.png "BringInAnimation_02.png")

Here the Animation Sequence and specified Bone Track to remove (include its children) are finalized when the modifier is applied.

You can create an Animation Modifier by creating a Blueprint with the [Parent Class](/documentation/en-us/unreal-engine/creating-blueprint-classes-in-unreal-engine) set to Animation Modifier.

On any animation that your import, you can go into the Animation Modifiers section and then apply the Animation Modifier that you have created to remove Bone Transforms. 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0bc3051-32ba-40a9-87b2-03179b1cdfe1/bringinanimation_03.png "BringInAnimation_03.png")

After adding the Animation Modifier, you can then click to Apply the modifier.

With only the curves remaining, you can run the animation through a Pose Asset inside your Animation Blueprint to give you the curve driven pose that can be shared. Below, we connect our curve driven animation directly up to the Final Animation Pose, however the pose is not used as it does not know how to handle the curves. We then connect it to the Pose Asset to drive those curves which results in the character performing our facial expressions. 

Each of our characters since they are using a Child Animation Blueprint and their own assigned Pose Asset can now share the facial animation using their relative deltas. Since we do not have bone transforms and the animation is purely driven by curves, we are not seeing double transforms and can blend this with any additional bone driven animation data (such as full body animation).
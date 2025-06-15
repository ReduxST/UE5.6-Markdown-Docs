# Animation Retargeting

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-retargeting-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-retargeting-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:28

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01fcd552-1c1c-457a-9b51-59388bd57537/retargetingheader.png)

**Animation Retargeting** is a feature that allows animations to be reused between characters that use the same [Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) asset but may have vastly different proportions. Through retargeting, you can prevent your animated skeletons from losing their proportions or becoming unnecessarily deformed when using animations from differently shaped characters. With Animation Retargeting it is also possible to share animations between characters that use **different Skeleton** assets as long as they share a similar Bone Hierarchy and use a shared asset called a **Rig** to pass animation data from one Skeleton to the other.

## Why Use Retargeting?

Suppose you have multiple characters that you would like to share animations between A base character, a short stocky character, and a tall skinny character.

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c56d752d-b385-4cb5-bf1f-3bf0f65afa67/basecharacter.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/730f4f1d-7158-40fe-b325-dc3125a8da7c/shortstocky.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/397c1e31-e55f-4084-8ee2-48bcf480e793/tallskinny.png) |
| Base Character | Short Stocky Character | Tall Skinny Character |

### Results Before Retargeting

Before retargeting is applied, you can already use animations between any Skeletal Meshes that share the same Skeleton asset. However, when you have differing proportions, as shown above, you can get some unsightly results. Notice how the short character gets unnecessarily stretched and the tall character gets compacted, both so that they can fit onto the Base Character's skeletal proportions.

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b929039-d714-4600-bc00-3b0a033da4eb/basecharacterrunning.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b2bb0e3-4d8c-4031-871c-5d43df509795/shortstockyrunning.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea6866c4-dba1-48fc-be82-b19a0df0a75b/tallskinnyrunning.png) |
| Base Character | Short Stocky Character | Tall Skinny Character |

### Results After Retargeting

Once retargeting is applied to the characters, the differences in their proportions are taken out of the equation and the animation plays properly on each character. You can also go to **Show > Non-Retargeted Animation** from the **Viewport** options and see the difference in the original skeleton (shown in beige) and the current skeleton (white). Notice how on the Base Character, the beige non-retargeted bones perfectly match the skeleton.

   |   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bff04ee-7350-488b-9899-545d14dd61a1/basecharacterrunningretargetedbones.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f1d3379-2040-4ff7-98a7-02a7016e7580/shortstockyrunningretargetedbones.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19185435-e6b0-4bbe-b193-0ca60c863608/tallskinnyrunningretargetedbones.png) |
| Base Character | Short Stocky Character | Tall Skinny Character |

## How Does Retargeting Work?

Animations are bound to a [Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) asset. The Skeleton asset is really just a list of bone names and hierarchy data, but it also stores the initial proportions from the original Skeletal Mesh used to define the Skeleton asset. This data is stored as bone translation data. It is important to note that the retargeting system only retargets the bone's translation component. The bone's rotation always comes from the animation data.

Because the original Skeletal Mesh is used to define the proportions of the Skeleton asset, any other Skeletal Meshes using that Skeleton asset that have different proportions (such as a mesh that is much shorter than the original one) will require retargeting to work properly. Without it, the Skeletal Meshes of varied proportions would try to use the translation data of the original mesh, leading to the types of errors seen at the beginning of this document.

To solve this problem, the Skeleton Tree within the **Skeleton Editor** offers a few settings to change how translation retargeting between bones is handled. There are 3 different settings for Bone Translation Retargeting:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/387ae99b-cd14-4941-b760-72af40b9d9d7/retargetingsettings.png)

-   **Animation** - Bone Translation comes from the animation data, unchanged.
-   **Skeleton** - Bone Translation comes from the Target Skeleton's bind pose.
-   **AnimationScaled** - Bone translation comes from the animation data, but is scaled by the Skeleton's proportions. This is the ratio between the bone length of the Target Skeleton (the skeleton the animation is being played on), and the Source Skeleton (the skeleton the animation was authored for).

Also with Animation Retargeting, there is no significant difference in performance between using retargeted and non-retargeted animations. The benefit of using animation retargeting is increasing the number of unique characters without having to create an entirely new set of matching animations which could seriously cut down on your animation memory budget.

### Retargeting Animations for Different Skeletons

The process in which Animation Retargeting is handled for characters that do not share the same Skeleton asset involves assigning a special asset called a **Rig** that processes animation data from one Skeleton to another. The Skeleton assets associated with each character communicate with the shared **Rig** asset to properly pass transform data from a source to its intended target.

The **Rig** can be assigned inside the **Skeleton Editor** under the [Retarget Manager](/documentation/en-us/unreal-engine/animation-retargeting-in-unreal-engine#usingtheretargetmanager) and the same Rig will need to be assigned to both Skeleton assets.

Please see [Using Retargeted Animations](/documentation/en-us/unreal-engine/using-retargeted-animations-in-unreal-engine) for a step-by-step guide.

## How Are End Effectors Handled With Retargeting?

Do tall characters run faster, can they still hold the same props - these are questions that may arise when working with retargeting. In short, there is no automatic work happening and it is up to the user to decide what they want it to do.

One method that can be taken regarding the holding of props is to create a separate chain of bones that follow the hands in the original animation, called "Hand IK Bones". Then retarget the body and arms, but not the "Hand IK Bones", so they remain identical after retargeting. This will allow you to have characters of different proportions manipulating the same props (for example, reloading a rifle).

Having a separate chain of bones allows you to switch smoothly between FK and IK easily when you want to (for example, you would want the Hand IK ON when reloading the weapon, and OFF when reaching for a magazine in a pocket).

The system is very flexible and can be customized to fit your needs. Perhaps you only want the left hand to be IK and the right hand to use its FK position, but IK rotation. Feet are sometimes handled this way, sometimes not. When stepping on a very precise prop, you would want to turn on IK; when you are just running around, you would want to use the FK, so you do not end up with a bow-legged character (or the opposite).

## Setting Up Retargeting

As mentioned above under How Retargeting Works, the first thing you will want to do is set up the **Bone Translation Retargeting** mode for the Bones within the Skeleton.

Typically, you will want to use these settings for bipeds:

-   Root Bone, IK Bones, weapon bones, and any kind of markers will use the Animation mode.
-   The pelvis will use AnimationScaled so it sits at the right height and is still animated.
    -   Any other bone you want translation to be animated and retargeted should also use AnimationScaled.
-   All other bones will use Skeleton. They will use the static translation from the target skeleton.

This means that a fast workflow would be:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c589f9fd-4d75-4296-8c6e-bc0519f77959/recursivelyset.png)

1.  **Right-click** on your root bone and **Recursively Set Translation Retargeting Skeleton** so all bones are set to Skeleton.
2.  Find the Pelvis or equivalent bone and set that to **AnimationScaled**.
3.  Find the Root bone, any IK bones, any weapon bones, or other marker-style bones and set them to use **Animation**.

If you are retargeting animations for characters that share the same Skeleton asset, those animations will now be affected by animation retargeting. If you want to retarget animations for characters that do not share the same Skeleton asset, there a couple extra steps you will need to take to ensure the animations are properly retargeted. Please see [Using Retargeted Animations](/documentation/en-us/unreal-engine/using-retargeted-animations-in-unreal-engine) for more information.

## Using the Retarget Manager

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67ab2c4d-e419-4916-8a9c-a6f52589c20d/baseposemanager.png)

Another tool you can use as part of your Animation Retargeting efforts is the **Retarget Manager** which allows you to:

-   **Manage Retarget Source** assets - useful for when you have different proportional meshes per skeleton, you can use this setting to indicate if a particular animation is from a different source.
-   **Set up Rig** - which allows you to retarget animations to different skeletons that use the same rig.
-   **Manage Retarget Base Pose** - which is used when retargeting assets to a different skeleton and allows you to alter the base pose of the target so it lines up with the source's base pose and provides a more accurate retargeted animation.

Please see the [Retarget Manager](/documentation/en-us/unreal-engine/retarget-manager-in-unreal-engine) page for more information.
# Using Retargeted Animations

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-retargeted-animations-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-retargeted-animations-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:49

---

**Animation Retargeting** is the process of repurposing existing animations for use between multiple characters, eliminating the need to create entirely new animations as you can instead share your animation assets between characters.

There are two forms of Animation Retargeting, one in which the Skeleton of the character you wish to share animations with is using the **Same Skeleton** as the character that the animations were originally created for. The other involves an intermediary object called a **Rig** which allows you to retarget animations from one character's Skeleton and pass that Skeleton's Bone information to a **Different Skeleton** using the Rig which both Skeleton's share.

Refer to the two links below for the type of Animation Retargeting you are looking to achieve:

## Retargeting Using the Same Skeleton

This section will show you how to set up a **Skeleton** to use retargeted animations for all biped characters that use the Skeleton.

### Steps

1.  Inside the **Content Browser**, open the **Skeleton** asset that is being used for each of your characters.
    
2.  In the **Skeleton Tree** window of the **Skeleton Editor**, check the **Show Retargeting Options** checkbox.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4698769-a484-481e-b64d-44b43847b93b/howto1.png)
3.  **Right-click** on your **Root** bone in the **Skeleton Tree** and select **Recursively Set Translation Retargeting Skeleton**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccbf8300-6e70-484e-a483-96c0ca2b05aa/howto2.png)
    
    This will ensure that all bones use the skeleton's static translation (we will modify certain bones for retargeting in a moment).
    
4.  Locate the **Pelvis** bone (or its equivalent bone) and click the drop-down box and select **AnimationScaled**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b695e0c0-9ca3-4822-9010-0ee87c68ed73/howto3.png)
    
    This will make sure that the bone sits at the right height and is still animated. Any other bone you want translation to be animated and retargeted should also use this setting.
    
5.  Find the **Root** bone, any **IK** bones, any **Weapon** bones you may be using or other marker-style bones and set them to **Animation**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e917afbe-f4a9-4c29-b916-9639ed76af86/howto4.png)
    
    By using **Animation** as the Bone Translation Retargeting Mode, the bone's translation comes from the animation data itself and is unchanged.
    
    You may have to experiment with the different methods for different bones to produce your desired results.
    
6.  Click the **Scene Setup** button in the Viewport and select a different **Preview Mesh**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29f0014b-caef-4a3f-bfb2-3542cbdd9e28/howto5.png)
    
    Try out different animations on different **Skeletal Meshes** to ensure that your Skeleton is set up properly for each of your animations.
    
7.  Inside the Viewport, click **Show** and check **NonRetarget Animation** and under **Bone**, choose **All Hierarchy** to display all Bones.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8b01015-aae0-4db9-b3b8-98cfce0919b7/howto6.png)

### End Result

You should now see something similar to below on your Skeleton.

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bff04ee-7350-488b-9899-545d14dd61a1/basecharacterrunningretargetedbones.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f1d3379-2040-4ff7-98a7-02a7016e7580/shortstockyrunningretargetedbones.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19185435-e6b0-4bbe-b193-0ca60c863608/tallskinnyrunningretargetedbones.png) |
| Base Character | Short Stocky Character | Tall Skinny Character |

Shown in beige above is the original Skeleton along with the current, retargeted Skeleton in white. When retargeting is applied to the characters, the differences in their proportions are taken out of the equation and animations applied play properly on each of the different characters and the original Skeleton (beige Skeleton) is depicted in the same position in both the Short and Tall Characters.

## Retargeting Using Different Skeletons

In this section, we will go through the process of retargeting animations from one character to another who both use different Skeleton assets. We are also going to use two asset packs that are available for free via the **Marketplace** that have additional skeletons and animations in it that we can use to retarget. If you have two Skeleton assets ready to use, you can skip the note below and use your assets. If you do not, you can follow along with the steps by adding the two packs outlined in the note below.

In this example, we are using the following assets which are available for download for free from the **Marketplace**.

-   The Source Skeleton we are using is the **UE4\_Mannequin\_Skeleton** that is included in the **Animation Starter Pack**.
-   The Target Skeleton we are using is the **SK\_Mannequin\_Skeleton** that is included in the **Infinity Blade: Warriors** pack.

Once you have installed the packs above, you can add them to a project via the **Add to project** button in the Unreal Launcher.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/265a847c-358e-4fd8-a1d0-4ee58a8ebe31/animstarterpack.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/342cbeff-868f-49b0-b99e-c0ffc7a8d736/infinitybladewarriors.png) 

### Steps

1.  Inside the **Content Browser** under the **Content/AnimStarterPack/UE4\_Mannequin/Mesh** folder, open the **UE4\_Mannequin\_Skeleton** asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b76e45a-6256-461b-9e33-1cf3e70dc628/retarget1.png)
2.  Click the **Retarget Manager** button, then under **Set up Rig**, click the **Select Rig** dropdown and select **Select Humanoid Rig**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6928ad2f-bf60-4bcb-ab9f-61aaeb76dbed/retarget2.png)
3.  In the **Content Browser** under the **Content/InfinityBladeWarriors/Character/CompleteCharacters** folder, open the **SK\_Mannequin\_Skeleton** asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/748c7f78-de6d-4132-b1c6-a2f4291e3c4b/retarget3.png)
4.  Click the **Retarget Manager** button, then under **Set up Rig**, click the **Select Rig** dropdown and select **Select Humanoid Rig**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86c85649-afbd-45bb-8f58-cc747822f07f/retarget4.png)
5.  With the Rig assigned, next you will need to match up the Bones from the Target to the Nodes on the Rig.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0827bd8b-1b1a-4b9d-8941-fe4332f6e100/retarget5.png)
    
    Since the Skeleton in the Infinity Blade: Warriors pack uses the same naming convention and Bone hierarchy, they are automatically detected and applied to the Rig.
    
    If your Bone naming convention differs from the Epic Skeleton, you may see "none" applied to each of the Bones in the Rig:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed67436c-066d-45cb-a07a-627329fb0db1/retarget6.png)
    
    In this case, you will need to use the **Auto Mapping** feature or manually assign each Bone from the Skeleton that best matches the Node on the Rig.
    
    When using the **Auto Mapping** feature, it is a good idea to double check which Bones were assigned to which Nodes on the Rig. Auto Mapping will try to get the best match based on Bone position and (or) Bone Naming Conventions and assign those to ones on the Rig, but they may not the ideal Bone to use in each case.
    
6.  Click the **Show Advanced** button to toggle between Advanced/Base configuration.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c88eeecc-2028-4848-9c69-f2d56c3b2c04/advancedconfig.png)
    
    In this section, you can assign Bones from the Skeleton that corresponds to Nodes on the Rig for digits of fingers, IK Bones or Twist/Roll Bones.
    
    Similar to the Base configuration, the Bones within Advanced may be set to "none" depending on your Skeleton which you will have to set.
    
7.  In the **Content Browser**, under **Content/AnimStarterPack**, select an animation that you want to retarget to the new Skeleton.
    
8.  **Right-click** on the animation and choose **Retarget Anim Assets -> Duplicate Anim Assets and Retarget**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bd0d96c-96ce-4c3c-8885-3b5acd801f1c/retarget7.png)
9.  In the **Select Skeleton** window, you should see your Skeleton in the upper portion of the window, select it and click **Retarget**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0707d15-e1a2-4a5f-ae84-34dfac83e9d4/retarget8.png)
    
    This will copy the animation to the specified folder location. You can assign a New Asset Name in this window as well.
    
    The **Target** Skeleton should have a similar Base pose as the Source to generate the best possible retargeted animation. Above, both Skeletons are in an A-Pose, however, you may have a character that is an A-Pose and one that is in a T-Pose. You can use a [Retargted Base Pose](/documentation/en-us/unreal-engine/retarget-manager-in-unreal-engine) to fix this prior to retargeting animations.
    

### End Result

The new retargeted animation will be available to any Skeletal Meshes that use the Skeleton asset the animation was retargeted for.

While this example illustrates how to retarget an animation, the same **Right-click** method can be used on any animation asset and retargeting can be applied.
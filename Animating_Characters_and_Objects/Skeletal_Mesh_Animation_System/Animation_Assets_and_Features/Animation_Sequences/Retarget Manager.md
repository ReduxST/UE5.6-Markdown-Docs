# Retarget Manager

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/retarget-manager-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/retarget-manager-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:16

---

The **Retarget Manager** within the **Skeleton Editor** can be used to manage your retarget sources, set up rigs and define retargeted base poses for use with [Animation Retargeting](/documentation/en-us/unreal-engine/using-retargeted-animations-in-unreal-engine).

## Manage Retarget Source

Since retargeting uses a [**Skeleton**](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) asset and the Skeleton has its original proportions defined by the Skeletal Mesh for which it was initially created, it follows that one-directional retargeting will work smoothly in most cases. However, there will often come times when you will have special animations that are built just for the variant versions. For example, suppose you have multiple characters that share the same Skeleton asset (a base character, a short character, and a tall character) and you have a special animation that was created just for the tall version of the character.

If you imported this new tall-only animation in, you would still need to use the same Skeleton asset as before, which was created from the base version of the character. This will cause the new animation's proportions to be distorted. The solution is to use the **Manage Retarget Source** option within the **Retarget Manager** which allows you to associate an Animation Sequence with the actual Skeletal Mesh for which it was designed. In this way, any problems of retargeting for special animations will be fixed.

### Adding Retarget Sources

1.  Inside the **Skeleton Editor**, from the **Toolbar** click the **Retarget Source Manager** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a2bf56e-8eb4-4617-b5cb-e15aaad87ddd/retargetmanager.png)
2.  Click the **Add New Retarget Source** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1c9a5b7-939a-4a8a-a60e-86fbdbfe7767/addsource.png)
3.  Choose the **Skeletal Mesh** for which the special animation was created.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8a51cd3-d14e-4659-8356-c80587cce06d/selectskeletalmesh.png)
    
    You will now see that Skeletal Mesh listed in the **Retarget Manager**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb76f9ec-f987-40ce-a01c-18371eff4c57/created.png)
4.  Open the special case **Animation Sequence** intended for your specific **Skeletal Mesh**.
    
5.  In the **Asset Details** panel, locate the **Animation** category and locate the **Retarget Source** property and choose your **Skeletal Mesh** from the drop-down menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c260c09b-a567-40c4-9346-ddf21a356cec/dropdownselection.png)
    
    By choosing this mesh, you are specifying that you want to use the proportions of that mesh to drive this animation.
    

## Set up Rig

The middle section of the Retarget Manager allows you assign a **Rig** to the Skeleton which can be used to pass animation data to a different Skeleton that uses the same Rig.

![Set up Rig-1.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14d7573e-3354-415b-b7eb-f55a7789f1ad/set20up20rig-1.png "Set up Rig-1.png")

This process is needed in order to perform any animation retargeting for characters that use different Skeleton assets.

You can select the Rig to use from the **Select Rig** drop-down option where a **Humanoid** option is available which you will want to select for most characters.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d00ec12a-f298-4129-8887-7a9b6d4c6463/humanoidsetup-1.png "HumanoidSetup-1.png")

Once you assign the Humanoid Rig, you will need to assign Bones from the Skeleton that correspond to the same (or similar) location as the Node on the Rig. You can use the drop-down menu for Node and manually assign the corresponding Bone from your Skeleton, or you can use the **Auto Mapping** feature located at the top of the menu. This will look through your Skeleton and attempt to find the best matching Bone for each Node on the Rig.

If you are working with non-biped characters, or have a hierarchy that is not compatible with the Humanoid Rig asset then you can create your own Rig asset by right-clicking on your Skeleton in the Content Browser and selecting **Create > Create Rig**.

The **Clear Mapping** button will wipe all the currently assigned Bones from their corresponding Node assignment. You can also use the **Save** and **Load** buttons to save the current mapping assignment or load a previously saved mapping assignment from a **Node Mapping Container** asset (shown below).

The **Show Advanced** button will allow you to assign additional Node/Bone correlations for things like finger digits, IK Bones or Twist Bones. Once you set up the Rig for your source Skeleton (or the Skeleton asset that drives the animation that you want to retarget to another character), you will need to go into the Skeleton of the target Skeleton and assign the same Rig and define the Bones in the new Skeleton that best match up with the Nodes on the Rig.

Please see [Using Retargeted Animations](/documentation/en-us/unreal-engine/using-retargeted-animations-in-unreal-engine) for a step-by-step guide on how to retarget animations between characters that use different Skeletons.

## Manage Retarget Base Pose

There may be instances where you want to retarget animations to a Skeleton that is not quite using the same base pose as your Source Skeleton.

Take for example the Skeleton in the image below on the right when attempting to retarget an animation:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccd52dc8-1b3d-425f-8992-d8b92b6718fc/managebasepose1.png)

Our Source Skeleton (left) is in a A-Pose while our Target Skeleton is using an T-Pose. If we were to retarget animations as is now, we may encounter issues:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86e45479-bb72-4141-b0f6-50dceedc1f4d/targetanimation.png)![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb80835e-c489-43b0-9c31-5bc908178f93/badbasepose.png)

Above we have our target animation on the left of a character holding a shotgun, however, when we retarget the animation to our new character on the right (because they are using different base poses) the arm positioning is not correct. We can fix this by Retargeting the Base Pose inside the **Retarget Manager** which allows us to define a Retargeted Base Pose to use for animation retargeting purposes rather than using the characters normal Base Pose.

We can select bones in our character and rotate them (in this case the left and right shoulders) so that our character is in an A-Pose, then we click **Modify Pose**:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/620126fa-4986-48f1-b650-f38c41e995aa/retargetedbasepose.png)

In context menu, select **Use Current Pose**:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d3a41ce-6c19-4625-9b3d-803eae6128a9/usecurrentpose.png)

This will set the pose you define as the Retargeted Base Pose to use when performing any animation retargeting.

Now when we go to retarget an animation, we will see the updated Retargeted Base Pose:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/743bab67-3fc8-41dc-9512-3c2c7509c18b/newbasepose.png)

When we retarget animations for Skeletons that have more similar Base Poses, we get better-looking results:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9696135-d671-4852-9fb5-7f0f8821e14e/holdingshotgun.png)

### Importing Retarget Base Pose from Pose Asset

From the **Modify** context menu, you can also choose to import a pose from an animation [**Pose Asset**](/documentation/en-us/unreal-engine/animation-pose-assets-in-unreal-engine) to use as the Retargeted Base Pose.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00b16744-2bf8-4ca5-8fdb-293f3aab7385/importpose.png)

In the image above, after selecting which Pose Asset to use (1) the available poses will be displayed in the selection drop-down menu (2). After selecting a pose from the Pose Asset to use, clicking the **Import** button (3) will update the mesh in the viewport to use the pose selected as the Retargeted Base Pose. Below (left) our default pose is shown and (right) our Retargeted Base Pose selected from a pose within our Pose Asset is shown.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/618f0f9b-105f-4ac1-a2ed-f7cd7b5a9a6d/defaultpose.png)![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c7f681a-a71c-4e47-b394-b685199142ef/newretargetpose.png)
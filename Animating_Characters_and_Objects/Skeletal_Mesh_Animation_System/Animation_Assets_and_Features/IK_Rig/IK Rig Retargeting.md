# IK Rig Retargeting

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:42

---

You can use **IK Rigs** to create animation retargeting between different **Skeletal Meshes**. This differs from Unreal Engine's traditional [Animation Retargeting](/documentation/en-us/unreal-engine/animation-retargeting-in-unreal-engine) feature in that you can transfer animation between skeletons with varying numbers of bones, bone names, and orientations, while optionally maintaining precise hand or foot contact points using IK.

Retargeting animations provides a way to share animation data between multiple different skeletons, without needing to create and manage new animations outside of Unreal Engine.

This page provides an overview of the **IK Retargeter**.

For information about using Unreal Engine’s automatic retargeting tools, see the [Auto Retargeting](/documentation/en-us/unreal-engine/auto-retargeting-in-unreal-engine) documentation.

#### Prerequisites

-   Your project has two different Skeletal Meshes to evaluate the retargeting process.
-   IK Rig Assets have already been created and retargeting chains defined within them. Refer to the [Retargeting Bipeds with IK Rig](/documentation/en-us/unreal-engine/retargeting-bipeds-with-ik-rig-in-unreal-engine) page for how to do this.

## Creation and Overview

To create an IK Retargeter, click **Add (+)** in the Content Browser, then select **Animation > IK Rig > IK Retargeter**. A dialog window appears where you must select the IK Rig that you want to retarget animation from. Once selected, name and open the **IK Retargeter Asset**.

![create ik retargeter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8572d5f3-40df-4340-b621-632ffbc67a70/create1.png)

The IK Retargeter contains the following tools and options:

![ik retargeter editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d786479-3bdf-449e-adbc-acb80be05d2f/create2.png)

1.  [Retarget Pose](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#poseediting), where you can edit, save, and import the base retarget poses on either the source or target character.
2.  **Viewport**, where you preview and debug the source and target characters being retargeted.
3.  The [Details panel](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#headername), which displays properties for your selected item or when other modes are active.
4.  [Hierarchy](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#hierarchydisplay), which displays a filterable list of bones and their assigned chains on either character.
5.  **Retarget Output Log**, which displays debug information, warnings, and errors indicating the current status of your IK Retargeter.
6.  [Chain Mapping](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#retarget%20chains), which is used to map target chains to source chains. The **Asset Browser** is used to [preview and export](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#previewanimationandexport) retargeted animations.

## Retarget Chains

Limbs and other appendages you want to transfer in the retarget process must be defined on both the source and target IK Rigs. This is a process similar to "characterizing" your rig as seen in other applications like Autodesk MotionBuilder or Maya. The main difference is you define it by joint chains, rather than by individual **Bones**. This provides flexibility in retargeting characters with vastly different bone structures.

For example, if your target character contains more arm joints than your source, the retargeting behavior will still work correctly because you are defining the entire arm chain, no matter the number of bones.

![retarget chains example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ee80c9b-8b79-4fd3-8a96-cc0ed7c44ff9/chains1.png)

1.  Source arm chain.
2.  Target arm chain.

### Chain Creation

Retargeting chains are created in the [IK Rig Editor](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine). To create a chain, open the IK Rig Asset for both characters, navigate to the IK Retargeting panel, then do the following:

1.  Click **Add New Chain (+)**.
    
    ![add new chain](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a7c4f2f-4978-4490-9799-6e457a6d5877/chains2.png)
    
2.  In the **Add New Retarget Chain** dialog window, ensure **Chain Name** is set correctly, then click **OK**. In most cases, IK Rig automatically assigns this value from its list of [common chain names](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#chainpropertiesandnames).
    
    ![chain name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7f87af4-ca79-4b3d-b41b-e7b94be1df45/chains3.png)
    
3.  In the **Add Goal to New Chain** dialog window, select **No Goal**. Typically you do not need to add [IK Goals](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#ikgoals) unless your retargeting requires additional IK adjustments, such as [Speed Planting](/documentation/en-us/unreal-engine/fix-foot-sliding-with-ik-retargeter-in-unreal-engine), [Stride Warping](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#globalsettings), or **Blend to Source**.
    
    ![add goal to new chain](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2d48fd5-cc50-4b96-9ecc-2d49bca72e20/chains4.png)
    

You can also create chains by selecting every **bone** in the intended chain, right-clicking on them in the **Hierarchy** panel, and selecting **New Retarget Chain from Selected Bones**.

![new retarget chain from selected bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ae87304-ef4e-458c-b696-db1dbb7efd8a/chain3.png)

### Chain Properties and Names

Chains require the following parameters to be set:

| Name | Description |
| --- | --- |
| **Chain Name** | 
The name of this chain. This name can be arbitrary, but it should match with the intended retarget chain in the other IK Rig.

The matching chain name process is determined by a [Fuzzy](https://en.wikipedia.org/wiki/Approximate_string_matching) string match. Therefore, while your **Chain Names** in each IK Rig do not have to match perfectly, you should still try to match them. For example, a Chain Name of `ArmLeft` can match to `left_arm` as long as there isn't a name that might be more accurate.



 |
| **Start Bone** | The starting Bone of the retarget chain. If you are retargeting an arm, then typically you would select the upper arm bone here. |
| **End Bone** | The ending Bone of the retarget chain. If you are retargeting an arm, then typically you would select the hand bone here. |
| **IK Goal** | You can optionally select an [IK Goal](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#ikgoals) here in order to [stabilize limbs or chains](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#retargetingwithikgoals) which may not be retargeting with good accuracy. This means you will also need to create [Solvers](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine) for those goals, which will execute their solve after the retargeting process. |

The **Chain Name** property automatically fills in itself depending on the name of the selected bones used when creating the chain. The system looks for common bone names used, and then picks a name that best matches the selected bones. This mapping list is as follows:

| Chain Name Mapping | Bone Names to Search For |
| --- | --- |
| **Head** | `head` |
| **Neck** | `neck` |
| **Leg** | `leg` `hip` `thigh` `calf` `knee` `foot` `ankle` `toe` |
| **Arm** | `arm` `clavicle` `shoulder` `elbow` `wrist` `hand` |
| **Spine** | `spine` |
| **Jaw** | `jaw` |
| **Tail** | `tail` `tentacle` |
| **Thumb** | `thumb` |
| **Index** | `index` |
| **Middle** | `middle` |
| **Ring** | `ring` |
| **Pinky** | `pinky` |
| **Root** | `root` |

For symmetrical chains, such as arms and legs, the auto-naming feature is determined by comparing the average location of the bones in the chain, and then assigning a prefix of **Left** or **Right**. If the selected bones are mostly located on the negative X side, they are "Left", positive X is "Right", and if they are relatively centered on the X axis, then they are considered "Center" and no prefix is applied.

If multiple chains are created for bones with similar names, a numerical suffix will apply for each subsequent chain. For example, if you were retargeting a creature with multiple heads, then the resulting chains would read as **Head\_1**, **Head\_2**, and **Head\_3**. You can manually name your chains however you like, but this convention is helpful to establish standard naming conventions and retarget quickly using other IK Rigs.

### Chain Display and Mapping

The **Chain Mapping** panel displays the source and target chains, and their mapping relationships. Using the dropdown menus under **Source Chain**, you can specify different chain mappings or correct mismatches.

![change source chain](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/109edfd2-dfda-4856-a556-d84eedfbf6b5/retargeter4.png)

Chains are drawn by default in the viewport and can be selected, which highlights the chain in the Chain Mapping panel. You can edit chain debug visualization in the [Details](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#editorsettings) panel.

![select chains](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba97e583-329a-4d59-8bd9-8e89a3788b1d/chains5.gif)

### Retarget Root

In addition to defining chains, you must also define the **Retarget Root**, which is typically the **pelvis** or **hip** bone. This is done so the character's root motion can be defined and transferred in a proportional way.

Like chains, the Retarget Root is defined in the IK Rig Editor. To do this, open the **IK Rig Asset** for both characters, navigate to the **Hierarchy** panel, right-click the bone and select **Set Retarget Root**.

![set retarget root](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c77429c9-c2c3-4fbd-b762-33a81a07a5ff/retargetroot1.png)

Once done, the Retarget Root indicates with the selected bone in the **Hierarchy** and the **IK Retargeting** panels.

![retarget root indication](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3711bb33-04d9-402a-8569-84bed90402ab/retargetroot2.png)

## Retarget Pose

Depending on the reference poses of the characters being retargeted, it may be necessary to edit this pose in the form of a base **Retarget Pose**. Typically you need to do this if your target character's reference pose is different from the source, such as being in a T-pose, rather than an A-pose. Matching these retarget poses will increase the accuracy of the retargeting.

![retarget pose comparison](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86d96b8c-b0e9-4991-becc-f2de3e8adb1c/pose1.png)

1.  Source character's reference pose is an A-Pose.
2.  Target character's reference pose is a T-Pose.

You can resolve reference pose discrepancies by editing, importing, or exporting different poses using the **Retarget Pose** tools in the **Hierarchy** panel.

![retarget pose tools](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0f6b62a-8d4d-4b83-a823-05b490a20ee9/poseedit1.png)

Clicking **Source** or **Target** will change the focus of the Retarget Pose tools and Hierarchy panel to either the source or target character. If bone drawing is enabled in the viewport, then the skeletons will indicate which rig is currently focussed by highlighting in color.

![change source or target focus](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3295e11-b252-4822-b303-2c8b014de642/poseedit2.gif)

### Create and Edit Pose

Although you can edit the **Default Pose** for any of your retargeted characters, we recommend creating **new** Retarget Poses if you need to make adjustments. To do this, click **Create (+) > Create New**, name the new Retarget Pose, then click **Ok**.

![create new retarget pose](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37c662eb-7f0b-45f5-a86a-a97e792e7bb9/poseedit3.png)

Next, ensure **Current Retarget Pose** is set to your new pose, then **enable Edit Mode**. You can now select and modify bones in the viewport and match the poses. When finished, **disable** Edit Mode.

![edit retarget pose](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d7de99e-c9aa-48b3-804b-69e7dcdbad6e/poseedit4.gif)

For extra precision, you can numerically modify retarget poses in the **Details** panel where a rotation value of 0, 0, 0 returns the bone to its reference pose.

### Importing and Exporting Poses

Rather than manually creating new Retarget Poses, you can also import them from [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) or [Pose Assets](/documentation/en-us/unreal-engine/animation-pose-assets-in-unreal-engine).

To import from an **Animation Sequence**, click **Create (+) > Import from Animation Sequence**. In the dialog window, select the sequence to import from and set the following parameters:

-   **Sequence Frame** defines a specific frame of the Animation Sequence to base the imported pose on. By default this will be set to **0**, which will use the first frame of the animation.
-   **Pose Name** defines the name of the Retarget Pose upon importing.

![import pose from animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efe1ec12-a898-432f-a7bf-bbb3bbb2828c/poseedit5.png)

To import from a **Pose Asset**, click **Create (+) > Import from Pose Asset**. In the dialog window, select the pose to import from, click the dropdown menu to set the specific pose name to use, then select **Import Retarget Pose**.

![import pose from pose asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/afbdff2d-1c25-4993-b7bd-45c45411971f/poseedit6.png)

You can also export Retarget Poses as a **Pose Asset** to share with other IK Retargeting assets in your project. To do this, click **Create (+) > Export Pose Asset**, give your asset a name, then click **Save**.

![export retarget pose](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7e595fa-8a42-4a9d-9e96-7b011c0cf890/poseedit7.png)

### Miscellaneous Workflows

The Retarget Pose area also contains the following miscellaneous tools to assist with creating and editing your Retarget Pose:

| Name | Description |
| --- | --- |
| **Current Retarget Pose** | 
Displays the current Retarget Pose used by either the Source or Target character. Initially this will only list **Default Pose**, and populates when you create new poses. You can click the dropdown menu to select different poses.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a80c6739-1368-4bbe-bfc8-34dd1ca7843a/posemisc1.png)

 |
| **Run Retargeter / Show Retarget Pose** | 

When enabled, this engages the retargeter so you can preview the results of the current Retarget Pose using Animation Sequences. Disabling this switches back to Retarget Pose mode, where you can continue to make further refinements if necessary.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/edb044ff-8c1b-4b19-ae91-50b05bbfcffa/posemisc2.gif)

The viewport will highlight in a blue outline to indicate that the Retarget Pose mode is enabled.



 |
| **Retarget Pose Blend** | 

When making several edits to a Retarget Pose, it may be helpful to preview what changes have occurred on which bones. To help this, you can edit the Retarget Pose Blend slider. Setting it to **0** changes the pose back to the Skeletal Meshes default reference pose. Setting it to **1** changes the pose to the current Retarget Pose.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab05d2e1-d5d9-4d46-af42-08142a3d7113/posemisc3.gif)

 |
| **Reset** | 

You can use the **Reset** menu to reset the Retarget Pose back to the Skeletal Meshes default reference pose. You can select the following options:

-   **Reset Selected Bones**, which resets only the bones you have selected in the viewport or Hierarchy.
-   **Reset Selected and Children Bones**, which resets only the bones you have selected and their children in the viewport or Hierarchy.
-   **Reset All**, which resets all bones.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14e93c67-280e-4d7a-9760-b09d762e2ba1/posemisc4.gif)

 |
| **Duplicate** | 

You can duplicate the current Retarget Pose by clicking **Create (+) > Duplicate Current**, then naming the new pose.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42dfb024-68e2-46c5-9e31-f91bbeeb3e00/posemisc5.png)

 |
| **Rename** | 

Rename the current Retarget Pose by clicking **Rename**, entering a new name, then clicking **Ok**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c620d615-1a52-4a2d-ab03-c23d1967b7fa/posemisc6.png)

 |

## Hierarchy Display

The Hierarchy panel displays the skeletal hierarchy of either the Source or Target character, depending on which is enabled. Bone names indicate if they are used in [Retarget Chains](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#retargetchains) by highlighting in addition to the Retarget Chain column displaying the name of the chain being used.

![hierarchy panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc63cb58-f439-42eb-8806-dd8bf321f89d/hierarchy1.png)

You can search to locate and filter specific Bone Names or Retarget Chains.

![hierarchy search](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/057867df-9d1e-4dfd-a92c-3423b1add03e/hierarchy2.png)

You can also click the filter dropdown menu to set the following filters:

-   **Hide Bones Not in a Chain**, which hides bones not used within a chain, regardless if the IK Retargeter is using the chain.
-   **Hide Bones Not Retargeted**, which hides all bones not used by the IK Retargeter.
-   **Hide Retargeted Bones**, which hides bones used by the IK Retargeter

![hierarchy filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98d82e0a-b7d2-4c6c-bd80-db2a013f9b42/hierarchy3.png)

## Preview Animation and Export

The **Asset Browser** panel is used to preview and export the retargeting effect on different assets. Double-click an asset to play it.

![preview animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a63bc54b-535f-4be9-b89d-7e7eb29f95db/retargeter3.gif)

Once you are satisfied with your retargeting results on the target character, you can export the animations to compatible [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) for that character's Skeleton. To do this, select the animations you want to export in the **Asset Browser** panel, then click **Export Selected Animations**.

![export selected animations](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb1de478-812d-4d47-859a-1935bf879259/export1.png)

In the export dialog window, choose the export folder, then optionally specify the following rename properties:

-   **Add Prefix**, which adds text before the new asset name.
-   **Add Suffix**, which adds text after the new asset name.
-   **Search for** and **Replace with**, which searches for existing names in the file name and replaces it with the name specified. Search and replace is not case sensitive.

Click **Export** to save your retargeted Animation Sequences.

![export retargeted animations](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab8efdda-5a30-4fc7-ad4b-7633406c81af/export2.png)

## Batch Retargeting

Most [animation assets](/documentation/en-us/unreal-engine/animation-assets-and-features-in-unreal-engine), such as Animation Sequences, Blend Spaces, or Animation Blueprints can be retargeted quickly from the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) using **batch retargeting**.

In the **Content Browser**, select the animation assets you want to retarget, then right-click them and select **Retarget Animation Assets > Duplicate and Retarget Animation Assets**.

![batch retarget animations](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1cdd4a5-912d-4363-a845-baee322eb763/batch1.png)

A batch retargeter window appears where you can customize the retargeting behavior and results before starting the batch process.

![batch retarget overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1c6bc1f-f779-47a6-852b-885ed25e4c3d/batch2.png)

1.  Source and Target Skeletal Mesh preview. These panels will not be active until you specify an **IK Retargeter**. Once active, you can change the Target Skeletal Mesh if you want to change the character being retargeted to.
    
    Changing the Target to a completely different skeleton from the one defined in the IK Retargter may produce incorrect results.
    
2.  The IK Retargeter Asset to inform the Source and Target Skeletal Meshes and retargeting batch process.
3.  Text fields where you can specify new Prefix and Suffix modifiers to the output asset names, as well as search and replacing text. **Old Name** and **New Name** will display a preview of your text entries.
4.  The output folder where the retargeted assets will be saved.
5.  Remap References Assets will enable any assets that have references to other retargeted assets (such as a Blend Space referencing an Animation Sequence) to remap to the newly created retargeted results.
    
    -   Disabling this will maintain the original references and may cause issues with assets referencing animations that are no longer compatible with the new Skeleton.
    -   Enabling this may cause reference issues if you are not retargeting all assets referenced.
    

Click **Retarget** to start the batch retargeting process.

![export batch assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e293211b-3065-42d8-a760-b3a6347f1da1/batch3.png)

## Retargeter Properties and Settings

### Editor Settings

The IK Retargeter **Details** panel contains the following properties when nothing is selected.

![editor settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39a81044-3042-4dac-b1df-2064cf34d6ac/details1.png)

| Name | Description |
| --- | --- |
| **Source IKRig Asset** | The source IK Rig to copy animation from. |
| **Source Preview Mesh** | The source Skeletal Mesh. You can change this, and the IK Retargeting system will use name matching to attempt to make the IK Rig compatible with a different mesh and skeleton. |
| **Target IKRig Asset** | The target IK Rig to copy animation to. |
| **Target Preview Mesh** | The target Skeletal Mesh. You can change this, and the IK Retargeting system will use name matching to attempt to adapt the IK Rig to the provided skeleton and proportions. Incompatibilities are printed as warnings or errors in the **Retarget Output Log**. |
| **Target Mesh Offset** | 
A positional offset that can be applied to the target Skeletal Mesh to offset it from the source. This is useful to help with previewing both characters, or if the target character is very large, requiring a larger offset.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70495970-dbbb-4bf2-9a4b-f2cb740036bc/details2.gif)

 |
| **Target Mesh Scale** | 

A preview scale modifier which you can use to increase or decrease the target character's scale. This is useful if your target is very small or large relative to the source, where changing this value can align their sizes more closely for convenience.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1e73445-8673-4996-adb6-70f1c33c4631/details3.gif)

 |
| **Source Mesh Offset** | Similar to **Target Mesh Offset**, this is a positional offset you can apply to the source Skeletal Mesh to offset it from the target. |
| **Debug Draw** | 

Enables drawing chain and root debug visuals in the viewport for the target character.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee61e860-9cea-48e9-a684-b15d905eedee/details4.gif)

 |
| **Draw Final Goals** | 

Enables drawing IK Goals used by chains for the target character.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a611fd31-51c0-461f-be9a-e3f6489638e7/details5.gif)

 |
| **Draw Source Locations** | Enables drawing IK Goals used by the source character. |
| **Chain Draw Size** | Controls the size of chains and IK Goals drawn in the viewport. |
| **Chain Draw Thickness** | Controls the line thickness of chains and IK Goals drawn in the viewport. |

### Global Settings

Clicking **Global Settings** in the **Chain Mapping** panel reveals additional settings for the IK Retargeter, including **Stride Warping** features.

![global settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5cdc8a7d-7fe4-4512-93aa-bd49c0d81e96/globalsettings1.png)

| Name | Description |
| --- | --- |
| **Enable Root** | Enables the translation movement of the root bone defined in the target IK Rig. Do not disable this unless you are debugging root retargeting behavior. |
| **Enable FK** | Enables the retargeting of all bone chains. Do not disable this unless you are debugging bone chain retargeting behavior. |
| **Enable IK** | Enables the IK retargeting pass if you are using IK Goals in the retarget chains. Do not disable this unless you are debugging IK retargeting behavior. |
| **Stride Warping** | Enables **Stride Warping** functionality, which allows manipulation of the stride length, width, and splay of the retargeted animations. Stride Warping requires your character to be set up using IK Goals for retargeting. |
| **Forward Direction** | The world space facing direction of your character. In most cases this is **Y**. |
| **Direction Source** | 
The source to use to determine a "best fit" global rotation that approximates the facing direction of the character over time. You can select from the following:

-   **Goals**: Uses the positions of IK Goals to approximate the facing direction. This option is best used on characters with a vertical spine, like bipeds.
-   **Chain**: Uses the positions of the bones in Retarget Chains to approximate the facing direction. This is best used for characters with a horizontal spine, like quadrupeds.



 |
| **Direction Chain** | If you set **Direction Source** to **Chain**, this property is used to specify which chain to use to help define the forward direction of the character. |
| **Warp Forwards** | 

Warps the IK goals along the forward direction. Values lower than **1** creates smaller strides, which values higher than **1** increase the stride length.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a09f0bf-3a62-4442-9f1b-7f8b8d46b34c/globalsettings2.gif)

 |
| **Warp Splay** | 

Warps the overall stance of the character. Values below **1** pulls the IK Goals together to an average location, and higher than **1** pushes them apart.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69079a85-45b5-4dd0-a768-ca3ca0097477/globalsettings3.gif)

 |
| **Sideways Offset** | 

Warps the sideways stance of the character. Values below **0** pulls the IK Goals together perpendicularly to the forward direction, and higher than **0** pushes them apart.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a587c395-70d1-4c28-8de0-0e0a335e1c24/globalsettings4.gif)

 |

### Root Settings

Clicking **Root Settings** in the Chain Mapping panel, or selecting the root in the viewport reveals [Retarget Root](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#retargetroot) settings for the IK Retargeter.

![root settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82666f4e-52bf-4c0f-a4f2-65e8fb5e6676/rootsettings1.png)

| Name | Description |
| --- | --- |
| **Rotation / Translation Alpha** | Blends the animation on the retarget root between the Retarget Pose (**0**) and the incoming retarget source (**1**). |
| **Translation Offset** | Applies a component-space translation offset to the retarget root. |
| **Rotation Offset** | Applies a local-space rotation offset to the retarget root. |
| **Scale Horizontal / Vertical** | 
Scales the motion of the retarget root in either the horizontal or vertical directions. You can use this in conjunction with **IK Goals** and **Translation Offset** to create embellished or diminished movements on your retargeted characters.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54b95448-61ed-4efe-b90e-de175f454d5a/rootsettings2.gif)

 |
| **Blend to Source** | Blends the retarget root's translation between its retargeted location (**0**) and the exact source location (**1**). This property is similar to "reach" as seen in other retargeting tools. |
| **Blend to Source Weights** | Per-axis blending control multipliers for **Blend to Source**. |
| **Affect IK Horizontal / Vertical** | If you are using **IK Goals**, these sliders control whether all IK Goals should move along with the root if the root is modified along the horizontal or vertical axes. At **0** the IK Goals remain at their retargeted position, and at **1** they move relative to the modified root transform. |

### Chain Settings

Selecting **IK Goals** or **Chains** reveals chain-specific properties in the Details panel:

![chain settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c505d650-6a84-4c5a-b890-3aed78d2e08c/chainsettings.png)

| Name | Description |
| --- | --- |
| **Source Chain** | The source chain assigned to this IK Goal. Changing this is the same as changing **Source Chain** in the **Chain Mapping** panel. |
| **FK** | Enables copying the shape of the chain from the source character using rotation and translation. |
| **Rotation Mode** | 
Determines how rotation is copied from the source chain to the target chain. You can select from the following:

-   **Interpolated**: The source and target chains are normalized by their length, then each target bone rotation is generated by finding the rotation at the same normalized distance on the source chain and then applying that normalized rotation to the target. This typically provides the best result for targets with a different amount of bones in the chain, or different proportions.
-   **One to One**: Each bone in the source chain is copied to the equivalent bone in the target chain, based on the bone order starting from the root chain bone. If the target chain has more bones than the source, the extra bones will remain at their reference pose. This option is best chosen when the amount of bones in a chain match between the target and source, and typically is the best choice for **finger chains**.
-   **One to One Reversed**: This operates similarly to **One to One**, but the copying order is started from the end bone in the chain instead of the root.
-   **None**: No rotation copying occurs, causing bone rotations to remain at their reference pose.



 |
| **Rotation Alpha** | Blends the amount of FK rotation copying. |
| **Translation Mode** | 

Determines how translation is copied from the source chain to all bones in the target chain. You can select from the following:

-   **None**: No translation copying occurs, causing bone translations to remain at their reference pose. In most cases this is the best option to choose.
-   **Globally Scaled**: The target bone translations are set to the source bone, multiplied by the relative global scale of the target skeleton.
-   **Absolute**: The target bone translations are set to the absolute positions of the source bones.



 |
| **Translation Alpha** | Blends the amount of FK translation copying. |
| **Pole Vector Matching** | Blends the rotation angle of the target chain to the source chain by twisting the chain along its length. This does not alter the location of the end bone. |
| **Pole Vector Offset** | When **Pole Vector Offset** is set to **1**, you can use this property to apply an angular offset (in degrees) to the rotation angle of the chain, essentially controlling the twist of the chain. |
| **IK** | Enables using an [IK Goal](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#ikgoals) to modify this chain. To enable this, you must associate an IK Goal with the chain in the IK Rig asset. |
| **Blend to Source** | Blends the IK Goal's translation between its retargeted location (**0**) and the exact source location (**1**). This property is similar to "reach" as seen in other retargeting tools. |
| **Blend to Source Weights** | Per-axis blending multipliers for **Blend to Source**. |
| **Static Offset** | Applies a world-space translation offset to the IK Goal. |
| **Static Local Offset** | Applies a local-space translation offset to the IK Goal. |
| **Static Rotation Offset** | Applies a local-space rotation offset to the IK Goal. |
| **Extension** | Moves the IK Goal along the direction of the chain. Higher values increase the distance, and lower values move it closer to the root bone in the chain. |
| **Affected by IK Warping** | Enables this IK Goal to be affected by [Stride Warping properties](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#globalsettings). Typically this should be enabled for IK Goals used for leg chains, and disabled for all others. |
| **Speed Planting** | Enables this IK Goal to use [Speed Planting](/documentation/en-us/unreal-engine/fix-foot-sliding-with-ik-retargeter-in-unreal-engine) properties. |
| **Speed Curve Name** | The name of the [Animation Curve](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) that contains the speed curve data. |
| **Speed Threshold** | The maximum speed a source bone is allowed to move for the Speed Planting system to determine it is not moving. This causes the target IK Goal to not move whenever the source bone speed drops below this threshold. |
| **Unplant Stiffness** | How stiff the spring model is that smoothly pulls the IK position after unplanting. Increasing this means increasing the speed that the IK Goal reaches the target value. |
| **Unplant Critical Damping** | How much damping to apply to the spring. A value of **0** means no damping, and a value of **1** means critically damped, causing no oscillation. |

Chains with adjusted settings will indicate in the Chain Mapping panel.

![chain edit indication](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78410797-f28a-4329-b09c-6c3f984db74f/chainsetting2.png)
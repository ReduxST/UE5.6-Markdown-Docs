# Creating Dynamic Animations

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-dynamic-animations-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-dynamic-animations-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:28

---

One way you can improve the realism in your character's movement is to provide dynamic animations for items that they may be carrying or wearing. With [**AnimDynamics**](/documentation/en-us/unreal-engine/animation-blueprint-skeletal-controls-in-unreal-engine) those pieces that you would expect to move around as you move in real life (hair, necklaces, bracelets, swords, pouches, etc.) will bounce around and move while your character moves.

In this How-to we will apply AnimDynamics to a character to achieve the effect seen below:

Above, the character has AnimDynamics applied to the harness and furnace that is being carried around the character's neck. As the character moves, the harness shifts slightly while the furnace has a bit more movement forwards/backwards. The amount of movement can be adjusted via the **Details** panel of the AnimDynamics node to achieve the effect you are looking for. Additional constraints can be added as well to manipulate just how the bones move.

If you already have a character with an AnimBlueprint and bones ready to drive with AnimDynamics, you can proceed to step 2.

## 1 - Required Setup

Before we get started with applying dynamic animations to our character we need to set up the character we wish to use. The template characters do not have any dynamic bones we can use so we will retarget animations from the template character over to an Infinity Blade character who has bones that we can influence with AnimDynamics.

For this guide, we created a New Project using the **Blueprint Third Person** template.

We then added the **Infinity Blade: Adversaries** pack which is available for free on the Marketplace to the project.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/435a9e4d-4c7f-45f9-9f02-05c5bbc02b6e/adversariespack.png "AdversariesPack.png")

With your **Blueprint Third Person** based template project open and the **Infinity Blade** assets added:

1.  In the **Content Browser** under **Content/Mannequin/Character/Mesh**, open the **UE4\_Mannequin\_Skeleton** asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4eae5a6-9410-444f-b5fd-835403897b8a/1_openmesh-2.png "1_OpenMesh-2.png")
2.  Click the **Retarget Manager** button, then under **Select Rig** assign the **Humanoid** rig.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a801a582-51e4-4be0-94ef-8b952ec4f273/2_setrig-2.png "2_SetRig-2.png")
    
    We are going to [retarget](/documentation/en-us/unreal-engine/using-retargeted-animations-in-unreal-engine) this character's AnimBlueprint and Animations to an Infinity Blade character.
    
3.  In the **Content Browser** navigate to and open the **SK\_Master\_Grunt\_Skeleton** in the Infinity Blade Adversaries folder.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b5fff6f-45b4-4d44-8d75-cbfaf4b9117b/3_opengrunt-1.png "3_OpenGrunt-1.png")
4.  Click the **Retarget Manager** button, then select **Humanoid** under the **Select Rig** option.
    
5.  For each node on the Rig, assign a Bone from the Skeleton.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/239d0145-e92b-45df-9acd-82df8dd1a31a/4_assignbones-1.png "4_AssignBones-1.png")
    
    The full assignment is shown in the table below.
    
    | Node (Rig) | Bone (Skeleton) |
    | --- | --- |
    | **Root** | b\_MF\_Root |
    | **Pelvis** | b\_MF\_Pelvis |
    | **spine\_01** | b\_MF\_Spine\_01 |
    | **spine\_02** | b\_MF\_Spine\_02 |
    | **spine\_03** | b\_MF\_Spine\_03 |
    | **clavicle\_l** | b\_MF\_Clavicle\_L |
    | **upperarm\_l** | b\_MF\_UpperArm\_L |
    | **lowerarm\_l** | b\_MF\_Forearm\_L |
    | **hand\_l** | b\_MF\_Hand\_L |
    | **clavicle\_r** | b\_MF\_Clavicle\_R |
    | **upperarm\_r** | b\_MF\_UpperArm\_R |
    | **lowerarm\_r** | b\_MF\_Forearm\_R |
    | **hand\_r** | b\_MF\_Hand\_R |
    | **neck\_01** | b\_MF\_Neck |
    | **head** | b\_MF\_Head |
    | **thigh\_l** | b\_MF\_Thigh\_L |
    | **calf\_l** | b\_MF\_Calf\_L |
    | **foot\_l** | b\_MF\_Foot\_L |
    | **thigh\_r** | b\_MF\_Thigh\_R |
    | **calf\_r** | b\_MF\_Calf\_R |
    | **foot\_r** | b\_MF\_Foot\_R |
    
    Before we proceed with retargeting, we will adjust the Translation Retargeting to ensure that our animations play correctly.
    
6.  In the **Skeleton Tree**, click the **Show Advanced Options** button.
    
7.  **Right-click** on the **b\_MF\_Root** bone and select **Recursively Set Translation Retargeting Skeleton**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/917340fd-cdce-4a5c-8ea9-39d502c6edd8/5_translationretargetinga-1.png "5_TranslationRetargetingA-1.png")
8.  Under **Translation Retargeting**, set **b\_MF\_Root** to Animation and **b\_MF\_Pelvis** to **Animation Scaled**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0796fa01-bdb8-42a7-a871-2a12b13f0008/5_translationretargetingb-1.png "5_TranslationRetargetingB-1.png")
    
    Our Skeleton is set up and we can now retarget the AnimBluperint and Aniamtions from the template character.
    
9.  Navigate to the **ThirdPersonAnimBP** and **Right-click** on it and select **Duplicate Anim Blueprints and Retarget**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e91e961d-5544-4ad6-88ad-7ee22a02b03f/6_retargetanimbp-1.png "6_RetargetAnimBP-1.png")
10.  In the **Select Skeleton** window, select the **SK\_Master\_Grunt\_Skeleton** asset then choose **Retarget**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa4c5a69-47fe-4c37-bfee-27272517b8cf/7_settarget-1.png "7_SetTarget-1.png")
    
    You can click the **Change...** button to assign where the retargeted assets are copied to if you like.
    
11.  Navigate to the duplicated assets and rename the new AnimBlueprint to **GruntAnimBP**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5743027-35d6-4c40-9e1c-2b8a428bea79/8_renameanimbp-1.png "8_RenameAnimBP-1.png")
12.  Navigate to and open the **ThirdPersonCharacter** Blueprint.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/936fd2b6-47f6-4e37-9f25-fb715ea02153/9_openthirdbp-1.png "9_OpenThirdBP-1.png")
13.  Click the **Mesh** in the **Components** window, then assign the **SK\_Master\_Grunt** and **GruntAnimBP\_C** in the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6309d12-0f62-404e-990c-8f6336860d77/10_assignnewcharacter-1.png "10_AssignNewCharacter-1.png")
14.  **Compile** and **Save**, then close the Blueprint.
    

At this point if you play in the Editor, you should be controlling the Grunt Character who can run and jump with **WASD** and **Spacebar**.

Notice the limited movement of the harness and furnace around the characters neck. It appears relatively static and our character would look more natural if these objects moved along with the character's movement.

In the next step we will use the AnimDynamics node to animate the harness and furnace so it reacts to character movement.

## 2 - Applying AnimDynamics

Now that our character is set up with an **Animation Blueprint** and has bones that we want to dynamically animate, we can do so from the **AnimGraph** of our **Animation Blueprint** with the **AnimDynamics** node.

In our example, the character is carrying a large furnace around their neck that we want to be animated based on character movement. If you are using your own character, you can follow the steps below and assign the bone(s) you want to drive with AnimDynamics and adjust the settings as desired.

### Steps

1.  In the **Content Browser**, open the character's **Animation Blueprint** (**GruntAnimBP**).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23796a89-3ad1-4f1d-b34d-72e126ee496c/1_openanimbp.png)
2.  Click **MyBlueprint**, then **AnimGraph** to open the Animation Graph.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67f8c3f0-7207-4b8f-803c-38ab296ec7e1/2_animgraph.png)
3.  **Right-click** in the graph and search for and add the **AnimDynamics** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ffd5290-9862-49b5-b4d5-3e1669d8c260/3_addnode.png)
    
    The AnimDynamics node takes in an **External Force** value which is additional force to apply to all bodies in the simulation (this is optional, but may be something to consider). It also takes in the **Component Pose** which is the reference pose data as well as an **Alpha** value (the strength with which to apply the skeletal control, where 0 is no strength and 1 is full strength).
    
4.  **Copy** and **Paste** the node, then connect the nodes as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d447bc70-ed5e-419b-a478-43a6cb45b0a8/4_connectnodes.png)
    
    The Local to Component and Component to Local will be automatically created when connecting pose pins.
    
    In our example we are using two AnimDynamics nodes (one to affect the Harness and another to affect the Furnace).
    
5.  Select the first **AnimDynamics** node in the sequence, then in the **Details** panel assign the settings shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6d7d5d4-0a97-4ac1-b05f-4b9981f6e7bc/5_furnance1.png)
    
    The **Preview** section is all about visualization, which helps to indicate the current limits applied to the movement in the viewport. You can also see Collision Spheres if you are using **Planar Limits** and **CoM** (Center of Mass) is not enabled. This is outside the scope of this example but you can experiement with this setting.
    
    The last thing we set is the **Bound Bone** or bone we are affecting which we set to the **furnace** bone on our character (this bone affects the Harness).
    
6.  With the node still selected, set the **Setup** and **Constraint** sections as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c17f0475-c1b8-4e0c-8d34-9babfbc21bea/6_furnance1.png)
    
    The **Setup** and **Constraint** sections are where you define the movement and range of movement for the bone driven by AnimDynamics. The **Box Extent** provides the inertia, the **Local Joint Offset** defines the pivot point, and **Angular Limits** provide the rotational range of movement (which is indicated by the preview visualization options when enabled).
    
    Please see [**AnimDynamics**](/documentation/en-us/unreal-engine/animation-blueprint-skeletal-controls-in-unreal-engine) section of Skeletal Controls for more information on Setup and Constraint settings.
    
7.  Click **Compile** and notice how the harness object tilts to the side.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25ed991e-74f8-427a-8c27-e61b33f2d7db/6_furnance1b.png)
    
    The Angular Limits for the **Y** axis is quite large right now indicated by the green cone in the picture above. Let's reduce this range.
    
8.  With the node still selected, in the **Constraints** section, adjust the **Angular Limits** for **Min/Max** as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8de4e52a-89e0-47c7-a006-62a4ba5ec1f2/6_furnance1c.png)
    
    When you **Compile** this time, the harness should not shift as much to either side (even if you adjust the **Speed** or **IsInAir?** settings).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dfd0695-7e6f-4989-bdbb-85baf8efbd20/6_furnanced.png)
9.  Select the second **AnimDynamics** node in the sequence and use the following settings.
    
    *Click for full view.*
    
    With the settings above, we changed the **Bound Bone** to now target the **Furnace\_Pivot** bone in our character which affects the furnace object. We also adjusted the **Twist Axis** so that it twists on the **Y** axis providing back-and-forth movement instead of side-to-side. The Angular Limits are set to **\-50** and **50** as the range in which to move.
    
10.  **Compile** and **Save** then play in the editor.
    

### End Result

You should now see that the furnace for our example character bounces around as the character moves based on our constraint settings.

Feel free to experiment with the **Box Extent** and **Local Joint Offset** values in the **Setup** section as well as the **Linear** and **Angular Limits** in the **Constraints** section to see how it alters the movement of our bones affected by AnimDynamics.
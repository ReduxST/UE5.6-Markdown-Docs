# Creating an Aim Offset

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-an-aim-offset-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-an-aim-offset-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:04

---

In this guide, we will create an [Aim Offset](/documentation/en-us/unreal-engine/creating-an-aim-offset-in-unreal-engine), which is an asset that stores a blendable series of poses to help a character aim a weapon. We will take an animation sequence and chop it up into usable poses for an Aim Offset, get the player's pitch/yaw location of the mouse and use that to determine which blended pose to use so that the character moves and aims in the location of the mouse (with some restrictions) as seen in the example below.

Completing the following steps will result in a similar character as depicted above:

## 1 - Creating Aim Poses

In this step, we update our default playable character and create all the poses that will be needed for the Aim Offset.

For this guide we are using the **Blueprint Third Person Template** project and have added the **Animation Starter Pack** to the project:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71496090-fd53-48ce-a9fb-6c3114577017/animationassetpack.png)

You can download the Animation Starter Pack for free through the **Marketplace** from the Epic Launcher.

### Steps

1.  In the **Content Browser** under the **Content/ThirdPersonBP/Blueprints** folder, open the **ThirdPersonGameMode**.
    
2.  Under **Default Pawn Class**, click the drop-down menu and select the **Ue4ASP\_Character** then **Save** and close the Blueprint.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a77826c4-e0cf-4f10-b592-27696b40fb4b/animations1.png)
    
    We are changing the default playable character to use the one provided with the Animation Starter Pack.
    
3.  In the **Content Browser** open the **Content/AnimStarterPack** folder, then click **Add New** and create a folder called **AimPoses**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/881a0441-4b0e-4283-be87-94a6c74c05f9/aimoffset1.png)
4.  Drag the **Aim\_Space\_Hip** asset onto the **AimPoses** folder and select **Copy**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/261e6346-089b-4390-84d7-83b96fee9358/aimoffset2.png)
    
    This is the animation sequence that contains a range of motions for aiming a weapon that we will chop up into poses.
    
5.  Inside the **AimPoses** folder, with **Aim\_Space\_Hip** selected, press **Ctrl+W** to duplicate it and name it **Aim\_Center**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/877391a1-2f67-4d0d-b8b2-14d43ae08b01/aimoffset3.png)
6.  Open the **Aim\_Center** asset, click the **Pause** button from the playback controls, then click the **ToFront** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4669582c-a23f-42c6-b46e-1c1b70995ae3/aimoffset4.png)
7.  **Right-click** on the scrub bar in the timeline, then choose the **Remove from frame 1 to frame 87** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5735e337-ecc2-4bb1-9fb2-473d6661dcb1/aimoffset5.png)
    
    With this, we now have a single frame containing a pose we can use in our Aim Offset.
    
8.  In the **AimPoses** folder with **Aim\_Space\_Hip** selected, press **Ctrl+W** to duplicate it and name it **Aim\_Center\_Down**.
    
9.  Open **Aim\_Center\_Down**, make sure it is on frame **0**, then click the **ToNext** button and go to frame **20**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c30a86ed-88e2-4902-a00f-71c6e389fa0e/aimoffset9.png)
    
    The character will now be aiming downward in the viewport, which is the pose we want to use for aiming down.
    
10.  **Right-click** on the scrub bar in the timeline, then choose the **Remove frame 0 to frame 20** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fde885d-1a66-4e3d-b4c8-4bcb73957d3b/aimoffset10.png)
    
    Depending on where you **Right-click** on the scrub bar, the frame range may be off by a frame or two, just make sure the character is aiming down.
    
11.  **Right-click** on the scrub bar in the timeline again, then choose the **Remove from frame 1 to frame 68** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/433073f9-4501-4068-81f5-6bdc7038d048/aimoffset11.png)
12.  In the **AimPoses** folder with **Aim\_Space\_Hip** selected, press **Ctrl+W** to duplicate it and name it **Aim\_Center\_Up**.
    
13.  Open **Aim\_Center\_Up**, make sure it is on frame **0**, then click the **ToNext** button and go to frame **10**.
    
14.  **Right-click** on the scrub bar in the timeline, then choose the **Remove frame 0 to frame 10** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f3ccc7d-d075-44a2-8f7e-a13ed864018b/aimoffset14.png)
15.  **Right-click** on the scrub bar in the timeline again, then choose the **Remove from frame 1 to frame 78** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8c083f7-25a9-4dcc-8dad-5f027d718433/aimoffset15.png)
16.  **Duplicate** the **Aim\_Space\_Hip** asset each time and create each of the remaining poses based on the table below.
    
    | Anim Name | Start At Keyframe | Remove Frames 1 | Remove Frames 2 |
    | --- | --- | --- | --- |
    | **Aim\_Left\_Center** | 30 | 0 - 30 | 1 - 57 |
    | **Aim\_Left\_Up** | 40 | 0 - 40 | 1 - 48 |
    | **Aim\_Left\_Down** | 50 | 0 - 50 | 1 - 37 |
    | **Aim\_Right\_Center** | 60 | 0 - 60 | 1 - 27 |
    | **Aim\_Right\_Up** | 70 | 0 - 70 | 1 - 17 |
    | **Aim\_Right\_Down** | 80 | 0 - 80 | 1 - 8 |
    
    For each animation, be sure to start at the suggested **Start At Keyframe** frame, then **Right-click** on the scrub bar and **Remove Frames 1**, **Right-click** on the scrub bar again and **Remove Frames 2**. Each of your animations should be a single frame with the character aiming in the direction of its corresponding name. When you have created each, your **AimPoses** folder should have several poses in it for each aiming direction.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07d42d0f-5b9f-4e83-b0b1-7a3f6f63c82a/aimoffset17.png)
17.  In the **Content Browser**, **Shift** and select each of the aim poses.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca572529-e0ab-436f-a5f7-0d42e6ace991/aimoffset18.png)
18.  **Right-click** and under **Asset Actions**, select the **Bulk Edit via Property Matrix** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96462983-5658-4dd5-90ab-4f86ed522ea6/aimoffset19.png)
19.  In the **Property Matrix**, under **Additive Settings**, change the **Additive Anim Type** to **Mesh Space**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d6e365c-26cf-4580-a2b5-6f87c0c11b3f/aimoffset20.png)
    
    For an animation to be compatible with an Aim Offset, it must be set to use an Additive Anim Type of **Mesh Space**.
    
20.  Change the **Base Pose Type** to **Selected animation frame**, then under **Base Pose Animation**, click the pick asset icon and choose **Idle\_Rifle\_Hip**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2800ccfd-78e7-4af5-b222-5670652b8296/add_01.png)
    
    This Base Pose Type will define how the additive delta is to be calculated.
    
21.  Once you have done so, return to the **Content Browser** and click the **Save All** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5da556d7-b729-4bf6-bce8-d14b2fea9245/aimoffset22.png)

With each of our pose assets created, in the next step, we will the poses to create our Aim Offset.

## 2 - Creating the Aim Offset

In this step, we take each of our aim poses and create our Aim Offset which will blend between each of the poses.

### Steps

1.  In the **Content/AnimStarterPack/UE4\_Mannequin/Mesh** folder, **Right-click** on the **UE4\_Mannequin** and select **Create Aim Offset**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50929599-b045-4f0b-9e83-b823bf5c2b17/aimoffset23.png)
    
    This will create the Aim Offset asset based on this Skeleton.
    
2.  In the Aim Offset window (center window), under **Parameters**, enter the parameters shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58463794-b750-4f34-8336-fbb3b1e84eb3/aimoffset26.png)
    
    Set the **X Axis Label** to **Yaw** and **Y Axis Label** to **Pitch**, then set both Axis Ranges to **\-90 to 90** and click **Apply Parameter Changes**.
    
    Aim Offsets work very similar to [Blend Spaces](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine) and will allow us to blend between our poses based on our parameters.
    
3.  In the **Asset Browser**, search for **Aim**, then drag the **Aim\_Center** animation onto the graph in the center position as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03c033b6-17b7-4bf1-9c6c-7f28a0d36c8a/aimoffset27.png)
4.  Drag the **Aim\_Center\_Up** to position **1** and **Aim\_Center\_Down** to position **2** as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/268487e4-cc01-4868-8e83-5798e51f83a2/aimoffset28.png)
    
    Optionally, you can turn off the tooltip in the grid by unchecking the **Enable Tooltip Display** option.
    
5.  Drag the **Aim\_Left\_Center** to position **1** and **Aim\_Right\_Center** to position **2** as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d56f134-0505-4fb8-910e-164273ce3519/aimoffset29.png)
6.  Add the **Aim\_Left\_Up** (1), **Aim\_Right\_Up** (2), **Aim\_Left\_Down** (3) and **Aim\_Right\_Down** (4) poses to finish the Aim Offset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59a1b144-715d-41c2-8579-0bea7d48ae25/aimoffset30.png)
7.  In the **Asset Details** panel, set the **Preview Base Pose** option under **Additive Settings** to **Idle\_Rifle\_Hip**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d3d25a9-cd5a-4228-b01e-248eb18391aa/add01.png)
    
    You can preview the blending of poses by moving your mouse within the grid, the viewport mesh will update its pose based on your mouse position.
    

The Aim Offset is now setup, in the next step we will hook it up for use within our **Animation Blueprint** so that gameplay can drive the blending.

## 3 - Implementing the Aim Offset

In this step, we add the Aim Offset to our Animation Blueprint and hook it up to our existing Anim Graph.

### Steps

1.  In the **Content/AnimStarterPack** folder, open the **UE4ASP\_HeroTPP\_AnimBlueprint** and **Double-click** the **AnimGraph** in the **MyBlueprint** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2902bc6-aba7-4475-9c9d-df0864ab45d2/step3_01.png)
2.  From the **Asset Browser** tab, drag in your Aim Offset asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d2306aa-8fde-4f11-94a5-a671f5ef97b0/step3_02.png)
3.  Connect the Aim Offset as shown below, then **Right-click** on the **Yaw** and **Pitch** pins and **Promote to Variable** and name them **Aim Yaw** and **Aim Pitch**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/071379e4-890a-4c97-890d-4086059d0084/step3_03.png)
    
    These two variables will be populated by where the player is aiming using their mouse and will drive the pose in our Aim Offset.
    
4.  In the **MyBlueprint** panel, jump over to the **EventGraph**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4fa03ed0-6973-4fb8-a588-a8552101a10e/step3_04.png)
5.  In the **EventGraph**, locate the **Sequence** node within the Movement portion of the script.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b81abbf2-fda7-4c68-a225-498bfd1f2509/step3_05.png)
    
    Click the **Add pin** button on the **Sequence** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e59abb5-94c7-4382-ac62-818cd647659b/step3_05b.png)
6.  From the **MyBlueprint** panel, hold down **Alt** and drag in both the **Aim Yaw** and **Aim Pitch** and connect to **Sequence** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/713a29a2-1eda-4877-9480-f93820e4b7f5/step3_06.png)
7.  Drag off the **Cast To Ue4ASP\_Character** node and add the **Get Control Rotation** and **Get Actor Rotation** nodes.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99d032fc-e3a5-4530-b694-b0acd33a464a/step3_07.png)
8.  Drag off the **Get Control Rotation** node and add a **Delta(Rotator)** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b877a207-f278-4289-930f-98ec36e90944/step3_08.png)
9.  Connect the **Get Actor Rotation** to the **Delta(Rotator) B Pin**, then off the **Return Value** add an **RInterp To** node (and swap the connection from Current to Target).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2fb0398d-7b64-4ce7-b14a-1b696e2e03b7/step3_09.png)
    
    You can hold **Ctrl** and **Left-click** on the **Current** pin to drag its connection to the **Target** pin.
    
10.  Drag off the **Current** pin of the **RInterp To** node and select **Make Rotator**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6c7e0ea-f9b0-43ac-a880-df4a3b1a1b90/step3_10.png)
11.  From the **MyBlueprint** panel, hold **Ctrl** and drag in the **Aim Pitch** and **Aim Yaw** variables and connect them to the **Make Rotator** node's **Pitch** and **Yaw**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8308ecc2-b794-463c-a3eb-92a4289a44cc/step3_11.png)
12.  At the start of the **Movement** script, find the **Event Blueprint Update Animation** node and promote **Delta Time X** to a variable called **Time** and connect as shown.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45c27987-a8c3-4875-aa51-7a20ee209d64/step3_12.png)
13.  Back on the **RInterp To** node, connect the new **Time** variable and set the **Interp Speed** to **15**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5c67f61-2e40-4359-bbc5-bc8103d7dab1/step3_13.png)
    
    We are going to use the rotation of the character and the rotation of the player's input to create a new rotator that will limit how much the character can turn in a direction.
    
14.  Off the **RInterp To** node, add a **Break Rotator** and **Clamp Angle** of **Pitch** and **Yaw** with min/max angles set to **\-90** and **90** respectively.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62bf658a-830b-41fe-b51f-9dc12d1986c4/step3_14.png)
15.  Connect the **Clamp Angle** from the **Pitch** to **Aim Pitch** and the **Yaw** to **Aim Yaw**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6b07904-91b3-4ad6-a894-4513721a66f1/step3_15.png)
    
    The Aim Yaw and Aim Pitch values that drive our Aim Offset now take into account the character's rotation, the player's current controller rotation and are clamped to prevent the character from turning too far in one direction. Without clamping the angle degrees, the character's legs could be pointed forwards while the character turns all the way around and points in the opposite direction which is probably something we want to avoid.
    

We are just about done with our setup, in the next step, we will tie everything together and test out our character's ability to aim.

## 4 - Finishing Up

In this final section, we will update our Character Blueprint to change how controller rotation is handled as well as fix some minor issues before testing.

### Steps

1.  In the **Content/AnimStarterPack** folder, open the **Ue4ASP\_Character** Blueprint.
    
2.  Cick on **Ue4ASP\_Character** in the **Components** window, then in the **Details** uncheck **Use Controller Rotation Yaw**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52f41519-1a17-4768-b716-74175bdda0c7/step4_04.png)
    
    This will prevent the character from automatically turning to the location of the Controller's yaw.
    
3.  Cick on **CapsuleComponent** in the **Components** window, then in the **Details** check the **Hidden in Game** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/873ff36e-aeb6-4215-90de-c741a974a11c/hidecapsule.png)
    
    This will hide the debug collision display during gameplay.
    
4.  Click the **EventGraph** in **MyBlueprint**, then find the **Crouching** section and replace the **InputAction Crouch** node with a **C** Key Event.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91888b1c-a174-432c-a482-d50579b0f035/step4_05.png)
    
    This will remove the yellow warning sign on the compile button in the upper left corner of the window since the project does not have an Action Mapping for Crouch by default, we are going to use the **C** button to crouch (you can use any Key Event you wish for this).
    
5.  **Compile** and **Save**, then close the Blueprint.
    
6.  Remove the **ThirdPersonCharacter** from the level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5722d3ab-9ae6-460c-8dac-28d5d23a0e49/deletecharacter.png)
    
    This will make sure that we use the character assigned to Game Mode and not the one placed in the level.
    
7.  Click the **Play** button to play in the editor.
    

### End Result

When you play in the editor, the character will now aim while stationary and will react to mouse movement, pointing in the direction of your mouse. There are some restrictions in place that prevent the character from turning and facing backward while the mouse is behind them as well and while the character is jogging, moving the mouse also turns the character's torso in the direction you are pointing.

You can take this a few steps further by allowing the character to aim in a direction and play a shooting animation in that direction and (or) allow the character to play a shooting animation while moving in a direction or crouching by [layering animations](/documentation/en-us/unreal-engine/using-layered-animations-in-unreal-engine) over the existing animations. Or, you can take a look at [Skeletal Mesh Sockets](/documentation/en-us/unreal-engine/skeletal-mesh-sockets-in-unreal-engine) for examples on how to attach a weapon to the character's hands now that they can aim.
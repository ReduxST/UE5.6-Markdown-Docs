# Locomotion Based Blending

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/locomotion-based-blending-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/locomotion-based-blending-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:17

---

[Blend Spaces](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine) are special assets which can be sampled in **AnimGraphs** that allow for blending of animations based on the values of two inputs. Simple blending between two animations based on a single input can be performed using one of the standard [Blend Nodes](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine) available in Animation Blueprints. Blend Spaces provide a means of doing more complex blending between multiple animations based on multiple values (currently limited to two).

In this How-to, we use a Blend Space to blend between walking and jogging animations based on the character's movement speed and movement direction.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60563328-e8a7-4525-9c3f-68996ee936a7/endresultimage.png)

## Steps

For this guide, we are using the **Blueprint Third Person Template** project and have added the **Animation Starter Pack** to the project.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84b55282-84fe-4eee-99e5-80eafca019bf/animationassetpack.png)

You can download the Animation Starter pack for free through the **Marketplace** from the Epic Launcher.

1.  In your project in the **Content/ThirdPersonBP/Blueprints** folder, open the **ThirdPersonGameMode** and set the **Default Pawn Class** to **Ue4ASP\_Character**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80f55a50-3f76-4b1d-bc25-7a0ec9a23bab/blendspace1.png)
    
    This will allow us to use the playable character that was created along with the Animation Starter Pack project.
    
2.  In the Level, select the **ThirdPersonCharacter** and delete it from the level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1470e6eb-75bc-4bf8-a010-8ac55c227dd3/blendspace2.png)
    
    We need to delete this character from the level in order to spawn in as the character from the previous step.
    
3.  In the **Content/AnimStarterPack/UE4\_Mannequin/Mesh** folder, right-click on the **UE4\_Mannequin** and under **Create**, select **Blend Space** and give it a name.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb07d81c-a9a2-4d76-b8b5-efe970955f43/blendspace3.png)
    
    Blend Space assets need a Skeleton asset to reference, here we are using a shortcut to create a Blend Space from this Skeleton asset which we called **MyBlendSpace**.
    
4.  Inside the Blend Space, in the **Asset Details** panel under **Axis Settings**, add the following values:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce404723-85ed-478f-99ed-2396f957698d/blendspace4.png)
    
    The Horizontal Axis will determine the **Direction** we are moving in degrees:
    
    | Horizontal Axis Settings | Value |
    | --- | --- |
    | **Name** | Direction |
    | **Minimum Axis Value** | \-180 |
    | **Maximum Axis Value** | 180 |
    | **Number of Grid Divisions** | 4 |
    | **Interpolation Time** | 0 |
    | **Interpolation Type** | Averaged Interpolation |
    
    The Vertical Axis will determine the **Speed** in which our character is moving:
    
    | Vertical Axis Settings | Value |
    | --- | --- |
    | **Name** | Speed |
    | **Minimum Axis Value** | 0 |
    | **Maximum Axis Value** | 250 |
    | **Number of Grid Divisions** | 4 |
    | **Interpolation Time** | 0 |
    | **Interpolation Type** | Averaged Interpolation |
    
5.  In the **Asset Browser**, drag the **Walk\_Fwd\_Rifle\_Ironsights** animation to the center-bottom position on the grid.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a09b4cc-85a9-4525-80c5-e887e8f2b31d/blendspace5.png)
    
    This will be are starting position when we enter this Blend Space.
    
6.  Drag the **Walk\_Lt\_Rifle\_Ironsights** animation to location **1** and **Walk\_Rt\_Rifle\_Ironsights** animation to location **2** below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8bce00a-c5fa-4381-a14f-061165dfd996/blendspace6.png)
    
    Here we place the animations to use when moving left or right.
    
7.  Drag the **Walk\_Bwd\_Rifle\_Ironsights** animation to locations **1** and **2** below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6141103-d1a0-4f94-b2f0-94400c6ff209/blendspace7.png)
    
    Here we place the animation to use when moving backward.
    
8.  From the **Asset Browser**, drag the **Jog\_Fwd\_Rifle** animation to the top-center position on the grid.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84911f69-8c8f-4c33-9ff6-90b79afa9546/blendspace8.png)
    
    This allows us to use a different animation when our speed is at max 250 and we are not moving left or right, we are jogging forward.
    
9.  Drag the **Jog\_Lt\_Rifle** animation to location **1** and **Jog\_Rt\_Rifle** animation to location **2** below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a558ece0-08e4-4b26-a6d5-d3760857e74d/blendspace9.png)
10.  Drag the **Jog\_Bwd\_Rifle** animation to locations **1** and **2** below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f554b85-8eb9-444a-b94e-4ea566ab216f/blendspace10.png)
11.  In the **Content/AnimStarterPack** folder, open the **UE4ASP\_HeroTPP\_AnimBlueprint** then in the **My Blueprint** panel, **Double-click** the **Locomotion** graph.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fce2003-c98e-4de9-b75e-20a320669c1f/blendspace11.png)
12.  **Double-click** the **Jog** State to open its graph.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47d2a952-60c2-4bf3-8515-301a427c2a38/blendspace12.png)
    
    This [State Machine](/documentation/en-us/unreal-engine/state-machines-in-unreal-engine) already has a Jog State and in it, a Blend Space for different Jogging motions.
    
13.  From the **Asset Browser**, drag the **MyBlendSpace** asset into the graph and replace the **BS\_Jog** Blend Space as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc297be9-e558-41e1-b21a-523c8f7a0f2b/blendspace13.png)
    
    The default Blend Space does not include Walking states which our Blend Space does, so let's replace it with ours!
    
14.  In the **Content/AnimStarterPack** folder, open the **Ue4ASP\_Character**.
    
15.  Locate the section marked **Crouch** in the graph and delete it to remove the warning error.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bba6cf58-7706-4f52-89e4-dd61f48b76de/blendspace14.png)
    
    By default, the Animation Starter Pack has bindings created for crouch which our project does not. For this example, we will remove the ability to crouch walk.
    
16.  Right-click in the graph and add a **Left Shift** Key Event, then drag the **CharacterMovement** into the graph from the **Components** tab.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0153bd0-d3b4-4858-9868-2f937ff0d0cf/blendspace15.png)
    
    When we press and hold the Left Shift button, that will toggle us from walking into a jog.
    
17.  Drag off the **CharacterMovement** node and **Set Max Walk Speed** for **Pressed** and **Released** with the values **250** and **100** respectively.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87303353-73b7-48a3-bc40-bbf31bd68643/blendspace17.png)
    
    We are changing our movement speed based on if Left Shift is held and will alter our character's movement speed in-game.
    
18.  Click the **CharacterMovement** component, then in the **Details** panel set the **Max Walk Speed** to **100**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62abe5af-01b4-443a-8ca2-7c4eec207fc6/blendspace20.png)
    
    We need to update our character's default movement speed so they start out walking.
    
19.  Click the **CapsuleComponent** in the **Components** tab and in the **Details** panel, check the **Hidden in Game** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba1adfa3-746e-4665-a1df-e8d38f1a2809/blendspace18.png)
    
    This will turn off the collision capsule debug display in-game.
    
20.  Click **Compile** then click the **Play** in editor button from the Toolbar.
    

## End Result

When playing in the Editor, using **WASD** to move around, the character will now walk by default and blend between walking animations when changing directions. While standing, pressing and holding **Left Shift** while using WASD will cause the character to blend from the walk/aim animation to a lowered/aim jog animation, essentially creating a sprint for the character.
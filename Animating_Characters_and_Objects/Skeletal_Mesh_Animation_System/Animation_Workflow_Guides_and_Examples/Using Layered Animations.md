# Using Layered Animations

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-layered-animations-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-layered-animations-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:27

---

Animation blending, as a concept, simply means making a smooth transition between two or more animations on a single character or Skeletal Mesh. In Unreal Engine, there are various ways in which such blending can be applied either through [Blend Spaces](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine), through additive methods by literally combining two animations based on a weighted bias or alpha value, or even applying direct overrides of the existing pose.

You can also send animation directly to specific bones within the Skeleton and all of its children. For instance, you can start with an animation in which the character is running, but then selectively apply a shooting animation to the upper body of the character. The final result would be a character that can run around and shoot at the same time, similar to the video below.

## 1 - Setting up the Animation to Blend

In this step, we change our default player character and create an AnimMontage for the animation we want to layer in on top of our movement animations.

For this guide we are using the **Blueprint Third Person Template** project and have added the **Animation Starter Pack** to the project:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55cb5e81-5902-4064-b2d0-2769f6ad84a8/animationassetpack.png)

You can download the Animation Starter Pack for free through the **Marketplace** from the Epic Launcher.

1.  With your project open, inside the **Content Browser** under the **Content/ThirdPersonBP/Blueprints** folder, open the **ThirdPersonGameMode** Blueprint.
    
2.  Under **Default Pawn Class**, click the drop-down menu and select the **Ue4ASP\_Character**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a77759bf-506e-4d2a-9ecf-ae5ff38011e0/animations1.png)
3.  **Compile** and **Save** then close the Blueprint.
    
4.  In the **Content Browser**, open the **Content/AnimStarterPack** folder.
    
5.  **Right-click** on the **Fire\_Shotgun\_Ironsights** animation, select **Create** then **Create AnimMontage**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d5d6bf3-029c-4e67-84cf-bcb55d05632a/animations2.png)
    
    You can filter the window by typing "Fire" inside the search window as shown above.
    
6.  Open the new AnimMontage and click the magnifying glass icon.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fea44bd-ed09-467e-ac49-825769542681/animations3.png)
    
    This will open the **Anim Slot Manager** which we will use to create a **Slot** that we can use to blend to when calling the Slot by name.
    
7.  Click the **Add Slot** button, then name the slot **UpperBody** then click **Save**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6d04075-e895-4145-b389-199e02b52f52/animations4.png)
    
    Although we chose the name "UpperBody" here, we are not targeting the upperbody just yet but have assigned the name so we know where we are targeting.
    
8.  Click the drop-down menu inside the **Montage Group** section and change it to **DefaultGroup.UpperBody**, then close the window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1fd2636-1671-418c-a8c2-69ead62ba1f6/animations5.png)
    
    We have now associated this Montage with the **DefaultGroup.UpperBody**, allowing it to play when the Slot is called.
    

In the next section, we will change our default player character and make some adjustments to determine when we are firing a weapon.

## 2 - Updating the Character Blueprint

In this step, we create some script inside our Character Blueprint to allow us to signal our Animation Blueprint that we are firing a weapon.

1.  Inside the **Content Browser** under **Content/AnimStarterPack**, open the **Ue4ASP\_Character** Blueprint.
    
2.  Locate the **Crouching** section, and delete the **InputAction Crouch** Event (with the Warning!) sign.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e69aea4-5326-4413-9498-cfad04c70349/animations6.png)
    
    There is a warning on this node because our project is not set up to use the InputAction event "Crouch".
    
3.  **Right-click** in the graph and add a **C** Key Event and connect as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ad7ef85-bb03-4f01-ac58-f0a4912c8ba0/animations7.png)
    
    We have just associated crouch now with the **C** key press, you can change this input to whatever you would like.
    
4.  In the **MyBlueprint** window, click the **Add Variable** button to create a **Boolean** variable and call it **Fire Button Down**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da8ed662-8591-4402-bf5c-6cd133e0421a/animations8.png)
5.  **Right-click** in the graph and add the **Left Mouse Button** Key Event.
    
6.  Holding **Alt**, drag the **Fire Button Down** variable in the graph to create a **Set** node.
    
7.  Repeat the previous step (or copy the **Set** node) and connect as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63d6c48e-0051-4a3f-a407-65b4fe71b19b/animations9.png)
    
    Make sure that **Fire Button Down** is **True** when **Left Mouse Button** is **Pressed** and **False** when **Released**.
    
8.  Select **CapsuleComponent** in the **Components** window, then in the **Details** panel check the **Hidden in Game** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f22cfc41-9042-4f4e-95a7-dff86df7dfd7/hidecapsule.png)
    
    This will turn off the debug display of capsule's collision.
    
9.  **Compile** and **Save** then close the Blueprint.
    

Our character is now set up to send signals to our Animation Blueprint when we are crouching or firing a weapon. In the next step, we will set up our Animation Graph inside our Animation Blueprint to handle the blending of our Anim Montage with our normal movement animations so that we can blend between the two.

## 3 - Setting up the Anim Graph

In this step, we set up our AnimGraph to handle the blending of our AnimMontage and the movement pose from our State Machine.

1.  In the **Content/AnimStarterPack**, open the **UE4ASP\_HeroTPP\_AnimBlueprint** Animation Blueprint.
    
2.  Inside the **MyBlueprint** window, open the **AnimGraph**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6950071b-346b-41be-b96d-fba7c6734085/animations9b.png)
3.  Drag off the **Locomotion** State Machine and search for and add **New Save cached pose**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01d5692c-0d54-4304-b175-a908ffe26d58/animations10.png)
    
    Here we are getting the resulting pose from our Locomotion State Machine and storing it in a cached pose that we can use elsewhere.
    
4.  Give the cached pose a name by pressing **F2** on the node such as **LocomotionCache**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d4a98d1-7d6a-4562-a507-5061bede5fc5/animations11.png)
5.  **Right-click** in the graph and add the **Use cached pose 'LocomotionCache'** (or whatever you named the cached pose).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17fd5bce-488c-421f-a6ad-0a88b143ad5d/animations12.png)
6.  Drag off the **Use cached pose** node and search for and add the **Layered blend per bone** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbc0c1ed-4e06-4a99-935d-9a3f78dae5e0/animations13.png)
    
    The **Layered Blend Per Bone** node will allow us to blend animations together from a specified bone on the Skeleton.
    
7.  Copy/Paste the **Use cached pose 'LocomotionCache'** node, then drag off it and add the **Slot 'DefaultSlot'** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1b0326a-f471-4f06-b192-6a6ef4fc3f6a/animations14.png)
8.  In the **Settings** for the **Slot** node, click the dropdown menu and select **DefaultGroup.UpperBody**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36f16572-63c7-436f-8140-d68242f66c4c/animations15.png)
    
    When an Animation Montage that uses this slot is called to play, it will now be called inside our AnimGraph.
    
9.  Connect the **Slot** to the **Blend Poses 0** pin on the **Layered blend per bone** node, then connect the out to the **Result** and **Compile**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aac61855-927b-4d42-9c48-14a6ac176914/animations16.png)

Our AnimGraph is complete, but we still need to modify some settings on the **Layered blend per bone** node to finish up which we will do next.

## 4 - Finalizing the Blend Settings

In this final step, we define the method in which to layer our blended animation and which bone to start the blend from.

1.  Inside the **AnimGraph** of **UE4ASP\_HeroTPP\_AnimBlueprint**, click on the **Layered blend per bone** node, then expand the **Layer Setup** section and click the **+** sign.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a37b959-a1b4-47d4-b4a5-bcce1eadcc34/animations17.png)
2.  Under **Bone Name** enter **spine\_01**, then set **Blend Depth** to **1** and check **Mesh Space Rotation Blend**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/faf375b9-7817-4e83-977c-0c6d0509d4af/animations18.png)
    
    With these settings, we can blend the shooting AnimMontage onto our Skeleton starting from the **spine\_01** bone.
    
3.  Inside the **MyBlueprint** window, open the **EventGraph**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4362dad1-456f-496e-9c3b-4b2da9ed9940/animations18b.png)
4.  Drag off the **As Ue4ASP Character** pin of the **Cast To Ue4ASP\_Character** node and add the **Get Fire Button Down** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e802dd6b-a873-4eb4-a2f6-288b4023b3a8/animations19.png)
    
    This will tell us if the player is pressing the fire button or not.
    
5.  Hold **B** and **Left-click** in the graph to create a **Branch** node and connect it following **Set Crouching**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4fdd7e2c-8d05-4c25-aa76-26b15e5e12b4/animations20.png)
    
    For the **Condition**, plug in the **FireButtonDown** pin.
    
6.  **Right-click** in the graph and add the **Montage Is Playing** node and assign **Fire\_Shotgun\_Ironsights\_Montage**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a21cc8b8-9f3a-4b9f-a12d-308081d60deb/animations22.png)
7.  Off the **Return Value** of the **Montage Is Playing** node, add a **Branch**.
    
8.  Connect the **Branch** from Step 5 to the new **Branch** as shown below and add a **Montage Play** node with **Montage to Play** set to your Montage.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04695aaa-3bbb-4a45-abad-d5b66c6c0a55/animations23.png)
    
    This will check now if the Montage is currently playing and if it is, do not play it (and if it is not, play the Montage).
    
9.  **Compile** and **Save**, close the **Blueprint** and delete the existing **ThirdPersonCharacter** in the level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05d39393-a6a5-48fc-bc35-86b64b1dd12a/animations24.png)
    
    This will allow us to use our selected character defined in our Game Mode and not the one placed in the level.
    
10.  **Play** in the editor.
    

### End Result

You will see that when you hold the **Left Mouse Button** down, the character will play the shooting AnimMontage. You can walk around while shooting, you can even crouch (by holding **C**) and shoot as well. You could use this same guide to play a melee attack, reload animation or any other animation that you want to be able to do while moving around.

The **UpperBody** slot that we created and assigned in our Animation Montage can be assigned in other Animation Montages as well. Since our AnimGraph has the Slot node assigned, whenever we call to play an Animation Montage that has that slot assigned, it will get played with our defined settings.
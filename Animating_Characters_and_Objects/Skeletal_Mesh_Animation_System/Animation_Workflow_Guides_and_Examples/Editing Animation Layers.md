# Editing Animation Layers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/editing-animation-layers](https://dev.epicgames.com/documentation/en-us/unreal-engine/editing-animation-layers)  
**Processed:** 2025-06-14 16:21:38

---

Animation Layer Editing allows you to modify any existing [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) inside Unreal Engine as part of **Additive Layer Tracks**. With Animation Layer Editing you can take an existing animation and adjust it to produce a different take on that animation, or you can create a separate, new animation with its own motion you provide based off the original.

This page will show you how to use the Animation Layer Editing tools to take an Idle animation and repurpose it into a Reload animation.

For this guide, we created a New Project using the **Blueprint First Person** template with **Starter Content** enabled.

## Steps

1.  Inside the **Content/FirstPerson/Animation** folder, duplicate the **FirstPerson\_Idle** animation and name it **FirstPerson\_Reload**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ce517ff-4779-4fde-a668-268f340d4d5f/layeranimation_01.png)
2.  Inside **FirstPerson\_Reload**, pause the animation at frame 0, click the **upperarm\_l** bone in the **Skeleton Tree**, then click the **Key** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3be3f72b-7a32-4771-9b07-a388468ef2b8/layeranimation_02.png)
    
    This will add **Transform**, **Rotation** and **Scale** keys for the current position of the upperarm\_l to the **Additive Layer Tracks** section.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60de526a-f939-4bf1-b4fb-1937bd8f46f9/layeranimation_03.png)
3.  Move the timeline ahead to frame **15**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e29d64bd-3730-4b7b-b625-90331ddeb098/layeranimation_04.png)
4.  Rotate the **upperarm\_l** bone **\-70** degrees, then press the **Key** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44b48c8f-7918-4663-b85e-0a472badde49/layeranimation_05.png)
    
    This will add a key for the bone's rotation when the animation is at frame 15.
    
5.  Move the timeline ahead to frame **20**, rotate the **upperarm\_l** bone **70** degrees to its default position and press the **Key** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08888b4b-7d6f-4578-816e-be54d7c144dd/layeranimation_06.png)
    
    Over the course of 20 frames, the arm will move down then back up to its default position.
    
6.  **Right-click** on the timeline marker and **Remove from frame 20 to frame 92**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7caae97-cb20-4d0b-b2a9-b43621d6355e/layeranimation_07.png)
    
    This will remove the rest of the frames from the animation, keeping only our reloading motion.
    
7.  In the **Content Browser**, **Right-click** on the **FirstPerson\_Reload** animation and select **Create AnimMontage**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/435aa1fa-8d62-401f-9bfd-99cac664b9a1/layeranimation_08.png)
    
    We are going to use this to play our new reload animation when the player presses the designated key during gameplay.
    
8.  Open the new AnimMontage, then change the slot to use the **DefaultGroup.Arms** slot.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4e87f21-20da-498f-9fba-f357423fddc6/layeranimation_09.png)
    
    Below, the Animation Blueprint assigned to the template character is set up to use a [Slot Node](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#slot) to play any Anim Montages assigned to the "Arms" slot.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31ee0bd2-a217-4c81-857a-437b499b6be3/layeranimation_13.png)
    
    This is currently being used to handle the playing of the firing weapon animation which we will also use for our reload motion.
    
9.  Inside the **Content/FirstPersonBP/Blueprints** folder, open the **FirstPersonCharacter** Blueprint.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46dc7a9d-543c-41fb-a7d8-86b0868be6d0/layeranimation_10.png)
    
    This is the Character Blueprint assigned to the template and is our playable character.
    
10.  Locate the **Spawn Projectile** script and **Ctrl** select the **Mesh2P**, **Get Anim Instance** and **Montage Play** nodes shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f566d551-bc6b-4d52-bb68-7d51283016ef/layeranimation_11.png)
    
    These nodes get the animation instance assigned to the Skeletal Mesh and signals the playing of an Animation Montage, in this case, the fire weapon montage. We are going to use this same script but instead call our reload Animation Montage when the key we specify is pressed.
    
11.  **Right-click** and copy the selected nodes, then paste them in an empty space in the graph.
    
12.  **Right-click** and add a **R** Key Event and connect them as shown to the pasted nodes, setting **Montage to Play** to your reload montage.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55bd207f-f6bc-47ba-9942-eab0dcb57fc4/layeranimation_12.png)
13.  **Compile** and **Play in the Editor**.
    

## End Result

When playing in the editor, pressing the **R** key will drop the character's hand off screen before bringing it back up to the gun, simulating a reload motion.

You can continue to modify this animation by moving to a frame on the timeline and selecting the Bone you want to modify and keying it, then moving the timeline forward some and moving the Bone to a new location and keying it again. The Bone will move from your first key to your second key along the curve created as the timeline progresses. You can modify as many Bones as you wish for more precision than our example, but the process of keying is the same.

### FAQ

**What happens if you export the animation?**

-   When you export, it will be whichever baked version of the animation is available. If you apply all the curves, it will export with curves.

**What happens if you re-import the animation?**

-   Reimporting the animation, it will overwrite the source data and apply the curves. If you do not want the curves, you can remove them.

**Can I temporarily disable or remove tracks?**

-   Yes, you can do both from the **Track Options** menu located in the upper right corner of the track window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/262b51bf-d1e4-4543-9de9-4cb783851ff3/animedit25.png)

**Is there a way to see the difference of my edited animation versus its source?**

-   Inside the **Show** menu options, you can enable the **Source Animation** and (or) **Baked Animation** for display in the viewport. The Source Animation can be seen as a white skeleton, while the Baked Animation can be seen as a blue skeleton as shown in the image below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4a25971-389f-4561-acf4-2b8ec196d437/le_sourcebakedanim.png)
    
    Just make sure that you have enabled the display of **Bones** from the **Show -> Bone Hiearchy** menu.
    

**Can Animation Layer Editing be used to create root motion?**

-   Yes. Select your Root Bone and key it, then scrub the timeline forward and move the Root Bone and re-key it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24cf797c-8732-4685-bc48-695d4ce443d7/le_thirdpersonanim.png)
    
    Above we have enabled the Source and Baked Animation preview where the white skeleton is the source animation.
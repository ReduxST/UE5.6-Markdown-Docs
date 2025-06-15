# Blending Animation Blueprints with Sequencer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blending-animation-blueprints-with-sequencer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blending-animation-blueprints-with-sequencer-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:15

---

If you want to blend an animation assigned within Sequencer with an animation defined from a Character's Animation Blueprint, you can do so using a **Slot** node and the **Weight** property of an Animation Track in Sequencer. 

In this example, we take the idle pose from our Animation Blueprint and blend in a running animation defined from Sequencer. 

## Steps

For this how-to guide, we are using the **Blueprint Third Person Template** project.

1.  In the **Content/Mannequin/Character/Mesh** folder, right-click the **SK\_Mannequin** then under **Create**, select **Anim Blueprint.**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b480891-8233-41e2-944b-c8e9d31e5417/animbpweight_01.png "AnimBPWeight_01.png")
    
    Give the Animation Blueprint any name and save location. 
    
2.  Inside the **Anim Blueprint**, drag in the **ThirdPersonIdle** and connect to a **Slot** node, then connect to the **Final Animation Pose** node. 
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c348b63e-efe3-4bd5-b761-f8731bd4e782/animbpweight_02-1.png "AnimBPWeight_02-1.png")
    
    Notice the Slot node is given the name **DefaultSlot** by default and is the name we will refer to inside our Level Sequence later in this guide. 
    
3.  Drag the **Anim Blueprint** into the Level, then from the Main Toolbar, select **Cinematics** and select **Add Level Sequence**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db08d21f-7218-4223-be44-cc778b6c7b95/animbpweight_03-3.png "AnimBPWeight_03-3.png")
    
    Give the Level Sequence any name and save location. 
    
4.  Add the **Anim Blueprint** character to the Sequence, then add/loop the **ThirdPersonRun** animation to fill the Sequence. 
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9aa1a44c-93bf-4d35-a3c7-ddb54efe43cb/animbpweight_04.png "AnimBPWeight_04.png")
5.  Expand the Animation track, then change the **Weight** value to **0.0** and add a key to the Sequence. 
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a177093-5713-4d51-b649-bbd03900bb84/animbpweight_05.png "AnimBPWeight_05.png")
    
    By setting the Weight to 0.0, we are stating that we want to use no part of this Animation until we increase the Weight value. 
    
6.  Add a key for **Weight** with the value **1.0** at frame **75**, and another key with a value of **0.0** at frame **150**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83e16715-e4d6-425e-b84e-cd3f9c69f68a/animbpweight_06.png "AnimBPWeight_06.png")
    
    This will blend from 0.0 to to 1.0 (full effect of the animation) back down to 0.0. 
    
7.  Right-click on the **ThirdPersonRun** track, then under **Properties**, notice the **Slot Name**, and the three **Keys** we added.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b8acb32-6588-4886-9fd7-71275471ab62/animbpweight_07.png "AnimBPWeight_07.png")
    
    Slot Name is the name referring to the Slot Node added inside the Animation Blueprint. These names must match in order for Sequencer to know which Slot you are referring to and to pass through the Weight values. 
    
8.  Select the Level Sequence, then in the **Details** panel, enable **Auto Play** and set **Loop** to **Loop Indefinitely**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4f0951e-94a8-408a-ad9c-f04c6a53d1b3/animbpweight_08.png "AnimBPWeight_08.png")
9.  From the Main Toolbar, select to Play in the Editor. 
    

## End Result

When you play in the Editor, the character will starting idle (which is the state inside our Animation Blueprint) and will blend to the animation we assigned (running) inside our Level Sequence, then back to idle. 

While our example uses an idle animation as our Final Animation Pose, using this method you can generate an entire State Machine to produce the Final Animation Pose inside your Animation Blueprint based on any number of factors, then blend to an animation defined inside a Level Sequence. 

As an example, an NPC could have some logic defined that governs what pose they are in and the player could approach that NPC triggering a cutscene where you override the animation logic with an animation defined within Sequencer.
# Controlling Anim Instances with Sequencer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/control-animation-blueprint-parameters-from-sequencer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-animation-blueprint-parameters-from-sequencer-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:32

---

Within Sequencer, it is possible to animate variables on Anim Instances through Possessables, enabling you direct control of Anim Blueprint variables, functions and other content. By adding a Skeletal Mesh Component Track, you can gain access to the Anim Instance Track where any variables that are exposed to cinematics will be shown and available to keyframe.

In this how-to, we blend between multiple animation poses that are defined within an Animation Blueprint by keyframing those changes inside Sequencer.

## Steps

For this guide we are using a new **Blueprint Third Person** template project.

1.  In the **Content/Mannequin/Character/Mesh** folder, right-click the **SK\_Mannequin** then select **Anim Blueprint** under **Create** and give it any name.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/516c1c63-0e56-4023-91a6-57c90e412153/image_1.png)
2.  Right-click in the **Content Browser** and under **Blueprints**, select **Enumeration** and call it **MoveType**.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c910ef26-36da-4893-baf5-c8b1dddf56ab/image_2.png)
3.  Create three enumerators called, **Idle, Walk** and **Run** by clicking the **New** button.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/625b7e44-2236-45fe-b549-70057a8c6186/image_3.png)
4.  Open the **Animation Blueprint** created in step 1 and create a variable of the **MoveType** type called **MoveType** and enable **Expose to Cinematics**.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31302b8f-cdb4-498f-b583-6f60f56c362b/image_4.png)
5.  On the **Anim Graph**, add the **ThirdPersonIdle, ThirdPersonWalk** and **ThirdPersonRun** animations and a **Blend Poses by Move Type** node.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca3d872c-d1d0-445b-bd3b-10b3e533975b/image_5.png)
6.  Right-click on the **Blend Poses** node then add a pin for **Idle, Walk** and **Run**.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ee5fff0-aafd-468f-958b-0528b4fcd173/image_6.png)
7.  Add the **Move Type** variable to the graph and connect each of the nodes to the **Final Animation Pose** as shown below.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f2080d9-e6f5-4bf2-8c1e-915a417e2f4f/image_7.png)
8.  Drag the **Animation Blueprint** into the Level, then create a new **Level Sequence** (give it any name) and add the Anim Blueprint to the Sequence.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c78a1ee8-7c6d-44ea-84b0-1a978fc8b92f/image_8.png)
9.  Click the **\+ Track** button on the Anim Blueprint and add an **SkeletalMeshComponent0** track.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa4e6c05-c83b-4c3c-ac85-7fa299bc174e/image_9.png)
10.  Click the **\+ Track** button on the SkeletalMeshComponent and add the **Anim Instance** track.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a48e4255-363b-40cc-8dab-c646a148b94b/image_10.png)
11.  Click the **\+ Track** button on the Anim Instance and add the **Move Type** property.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4d254e9-d2ac-4ea6-bf67-2f0a3e865954/image_11.png)
12.  Scrub the Timeline to frame **45** and change the **Move Type** drop-down to **Walk,** adding a key.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19a86ec9-610d-485e-aa04-c39aeb4bddf6/image_12.png)
13.  Scrub the Timeline to frame **90** and change the **Move Type** drop-down to **Run**, adding another key.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14531325-cb52-443f-8100-989fb4c9c0d7/image_13.png)
14.  Add a key for **Move Type** at frame **120** set to **Walk** and another key at frame **150** set to **Idle.**
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/841390bd-70e7-46d8-a554-43b235073792/image_14.png)
15.  Set the Level Sequence to **Auto Play** in the **Details** panel, then click the **Play** or **Simulate** button to play/simulate in the Editor.
    

## End Result

When you Play or Simulate, the Level Sequence will play back and change the character's state based on the key framed property **Move Type** defined in the Sequence. Animating variable properties is useful in the event that you have characters that have Animation Blueprints that drive their animation logic, however you want to control what animation the character enters through a Sequence.
# Keeping or Restoring Changes Made by Sequencer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/what-happens-when-my-cinematic-ends-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/what-happens-when-my-cinematic-ends-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:14

---

When working in Sequencer, you may make changes to the properties of your Actors that you want to persist after the cinematic finishes. For example, you might create a cinematic where a player unlocks and opens a door, and the door remains in the open state afterward. In a film production environment, however, you may want animated values in a shot to return to their pre-animated state so they don't bleed into the next shot. With the **When Finished** property, you can determine on a per-track basis whether tracks should return to their pre-animated state or keep changes when the sequence finishes.

In this how-to guide, you will use the When Finished property to restore the color change of a light but keep the changes made to the movement of a door.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/525bb5f4-0fa7-48eb-914c-85950d1893fb/heroimage.png)

## Steps

For this how-to guide, we are using the **Blueprint Third Person Template** with **Starter Content** enabled.

1.  From the **Content/StarterContent/Props** folder, drag an **SM\_Door** and **SM\_DoorFrame** into the **Level Viewport** and position the door inside the frame.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eead49cf-a074-45d6-91b4-7e6ac2bda295/whenfinished_01.png)
    
    Press the **W** key to enter translation mode and, if needed, disable grid snapping (pictured below) to fine tune the position of the door in the frame.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83b8abbe-f77b-486c-83eb-ca7c4ae223d1/whenfinished_02.png)
2.  From the **Place Actors** panel in the **Lights** tab, drag a **Point Light** into the **Level Viewport** and position it in front of the door.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/499c2ffc-b86e-4389-878f-e5f98fd55d29/whenfinished_03.png)
3.  Position the **ThirdPersonCharacter** in the **Level Viewport** in front of the door.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36512f19-7f12-4a39-b88f-483a7c141e07/whenfinished_04.png)
4.  From the **Main Toolbar**, click the **Cinematics** button and select **Add Level Sequence**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1745999e-4799-4d30-b812-8dabf47d9868/whenfinished_05.png)
5.  In the **Save Asset As** window, select a **Name** and save location, then click **Save**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b69f9bc7-9da7-4ecb-9cf0-22a5d535792c/whenfinished_06.png)
6.  In the **Sequencer** window, click the **Add** button and select **Shot Track**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d801310-4631-4a56-bf31-a6653153f870/whenfinished_07.png)
    
    This will create a [Shot Track](/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine) which enables you to section off parts of your cinematic into self-contained "shots" that you can arrange and re-arrange.
    
7.  On the **Shot Track**, click the **\+ Shot** button and **Insert Shot** and use the default naming convention when prompted.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/782abdc1-f719-4f36-973a-8dadda7340bb/whenfinished_08.png)
8.  Grab the end of the shot and pull it back to **Frame 75** so the shot is half the length of the entire sequence.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2973c1a-8633-4cd2-a304-4431a37bd3f9/whenfinished_09.png)
    
    We are going to use the shot to affect the light in our scene, but restore those changes once the shot is over.
    
9.  With the **Timeline** at **Frame 0** and the **SM\_Door** selected in the level, add the **Actor To Sequencer** from the **\+ Add** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/270ae457-4b5e-459c-95c7-03d2023ec1db/whenfinished_10.png)
    
    We will affect the door on the master level and keep the state of the changes we are going to apply.
    
10.  Click the **Add (+)** button on the **Transform** track of **SM\_Door**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6c6a497-e730-4a08-ab9d-ec181c032fc1/whenfinished_11.png)
11.  Move the **Timeline** marker to **Frame 150**, then rotate the door (**E** key) in the level so it is open and press the **S** key to add its transform while open.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bdb835c7-a062-4895-8e24-40fa69c5b59a/whenfinished_12.png)
    
    This will cause the door to go from closed to open once we reach the end of the cinematic.
    
12.  Double-click on the shot in the **Shot Track** to open it, then in the level select the **Point Light** and add it to the shot.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc618d38-ca56-4c1c-8834-f76537c47fea/whenfinished_13.png)
13.  On the **Light Color** track, click the **+** sign to assign the default color to use at **Frame 0** of the shot.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f41db3c4-16b6-4cf7-a70e-303c7993a5dd/whenfinished_14.png)
14.  Move the **Timeline** marker to **Frame 75** and change the **Light Color** to **Green** (or any color you desire) adding keys for the new values.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a95bc44c-7dea-40b1-8135-89ef91aa6e7b/whenfinished_15.png)
15.  Right-click on the **Light Color** track in the tracks window and select **Properties** to view the **When Finished** state.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3fd1d6ad-baa9-41e9-99c9-d6a831ecb69e/whenfinished_16.png)
    
    By default, **When Finished** states that this track will **Restore State** (return to its original state) when the section is completed.
    
16.  Exit the **Shot** and return to the **Master Sequence** level by clicking the breadcrumb buttons in the upper-right of the **Sequencer** window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a94a35e-de71-4be2-a9a5-e3f6f67407da/whenfinished_17.png)
17.  Right-click on the **Transform** track of the **SM\_Door** and select **Properties**, then change the **When Finished** property to **Keep State**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c9f219a-e706-49d9-b46a-261656c1b91b/whenfinished_18.png)
    
    We are now stating that we want to **Keep State**, meaning we want to keep the changes that we apply through Sequencer when the cinematic is complete.
    
18.  Select the **Level Sequence** Actor in the level, then, in the **Details** panel, set the **Auto Play** option to **True**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fc1d502-3004-4575-9674-de0a2f1deb32/whenfinished_19.png)
19.  From the **Main Toolbar**, click the **Build** button and select **Build Lighting Only**, then (after lighting has built) click the **Play** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/458ae629-697c-4f0c-86b0-53a4826e7102/whenfinished_20.png)

## End Result

When you play in the level, the light will change colors before returning to white. Our door, however, will remain in the opened state.

For the light inside our shot, we used the default **When Finished** property value of **Restore State**, which will restore it back to its original state when the shot is finished. For the door, however, we changed the When Finished property to **Keep State** preserving our changes and keeping the door in the open state when the cinematic completes.

One thing to consider is that, while Keep State has a local effect, there is a global **Restore State** option contained within the **Level Sequence** actor:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae031f5b-2c9f-482a-9f61-bcb076a94450/whenfinished_21.png)

The Restore State option in the **Details** panel of a Level Sequence actor will restore all states when the Level Sequence stops. If you want to keep the state of a track after the sequence has completely finished, you will need to make sure both that your section is set to Keep State, and the Level Sequence actor is **not** set to Restore State, otherwise the global value will override your local settings.
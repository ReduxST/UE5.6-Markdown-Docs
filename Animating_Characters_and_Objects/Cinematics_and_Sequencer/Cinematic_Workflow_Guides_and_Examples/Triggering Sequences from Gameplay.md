# Triggering Sequences from Gameplay

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/play-cinematics-from-blueprints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/play-cinematics-from-blueprints-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:34

---

Once you have created your cinematic sequence, you may want to have it called and played during gameplay as part of a cutscene. For example, maybe the player walks into a room and you want to have the camera zoom in on an object. Or perhaps you want to trigger an ending cinematic after the player kills an enemy. By getting a reference to your Level Sequence, you can use [Blueprint](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) or C++ code to tell your sequence to start playing.

In this How-to, we create a sample cinematic that turns on a light when the player enters a Trigger Box. When the cinematic finishes playing, we'll instruct Sequencer to apply the changes to the light in the Level so it persists after the cinematic has finished playing. We also allow the player to skip the cinematic while it is playing but still instruct Sequencer to turn and leave the light on after skipping the scene.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9e2424e-22bc-4ca8-9fd1-8f4ca8636628/heroimage.png)

## Steps

For this How-to, we are using the **Blueprint Third Person Template** project.

1.  From the **Place Actors** panel in the **Basic** tab, drag a **Box Trigger** into the Level and resize and position as desired.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad0bd677-2517-4416-96de-9b224f2e8bba/trigger01.png)
    
    When the player enters our trigger, we will instruct our cinematic to start playing through Blueprint.
    
2.  From the Main Toolbar, click the **Cinematics** button then select **Add Level Sequence** and give your cinematic a name.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7624922f-b7fc-4f35-b085-82a4f2689edd/trigger02.png)
3.  From the **Place Actors** panel in the **Basic** tab, drag a **Point Light** into the Level and place the light in the position shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7e6454d-53c9-43f2-a698-e4753ee06e15/trigger03.png)
4.  With the **Point Light** selected, in the **Details** panel, change the **Intensity** value to **0.0** and click the **Keyframe** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/749e0dcb-a425-40c8-a9f4-77c53b911831/trigger04.png)
    
    This will add the Point Light to Sequencer and keyframe its initial value at the start of the sequence.
    
5.  In Sequencer, move the timeline to frame **150** and set the **Intensity** value of your light to **5000**\* and keyframe it.
    
    Click image for full view.
    
    Your Point Light will now start in the off position and get brighter as the Sequence plays out.
    
6.  Click the **Add Camera** Button, then move the Camera in the Level to a position near the Character and keyframe it.
    
    Click image for full view.
    
7.  Move the Timeline to frame **75**, then in the Level, move the Camera to a new position overlooking the Character and the light and keyframe it.
    
    Click image for full view.
    
8.  Move the Timeline to frame **150**, then in the Level, move the Camera to a position focused on the light and keyframe it.
    
    Click image for full view.
    
    Our cinematic now has a camera fly-through animation that will show the player where the light is in the Level.
    
9.  Select the **Trigger Box** in the Level, then from the Main Toolbar, click the **Blueprints** button and select **Open Level Blueprint**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2ff1a85-30dd-4628-9bdf-b55d02f6a544/trigger09.png)
10.  Right-click inside the graph, then select the **Add On Actor Begin Overlap** for the **Trigger Box**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cffc3373-a75e-451e-8e89-ddfb64743c8b/trigger10.png)
11.  Return to the Level and select your Level Sequence, then back inside the **Level Blueprint**, right-click and **Create a Reference** to your Level Sequence.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99bc4ca4-5300-4a9d-add1-3ec8319eabc8/trigger11.png)
12.  Drag off the Level Sequence reference and select **Play (SequencePlayer)**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10712277-55f5-405e-95dd-00fea5e9eda4/trigger12.png)
13.  Connect the **OnActorBeginOverlap** node to the **Play** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b328802-eb9b-4d13-ac6f-67b35dbe7d5c/trigger13.png)
    
    When entering the Trigger Box, the **Play** node will be executed and will play your Level Sequence.
    
    You will notice if you play in the Editor that the sequence plays when entering the Trigger Box, however, it will only play once. If you want to play the sequence again, you will need to start the sequence over using the **Set Playback Position** node with the Playback Position set to **0** (or the start of the sequence) before telling the sequence to play.
    
14.  In the **Level Blueprint**, drag off the **Sequence Player** node and use the **Set Playback Position** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbb8bdf7-fff9-416b-8007-18ea519b3d23/trigger14.png)
15.  Connect the **Set Playback Position** node between the **OnActorBeginOverlap** and **Play** nodes.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4650bca-064d-4ecc-9ead-90c63ced3e36/trigger15.png)
    
    This will set the Level Sequence back to the beginning prior to playing it.
    
16.  Inside **Sequencer**, right-click on the **Intensity** track, then under **Properties** set **When Finished** to **Keep State**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5e3cfa5-c78b-4f59-bd8f-c42b7d04c8b2/trigger16.png)
    
    Using the **Keep State** option enables our light Intensity setting to remain after the sequence has ended. This is useful for situations where you want effects or settings you make in Sequencer to remain after the Sequence has ended. For example, your cinematic opens a door and you want the door to remain open once the cinematic ends.
    
17.  In the **Level Blueprint**, add an **F** keyboard event connected to a **Branch** (with condition **Is Playing**) that is connected to the **Go to End and Stop** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14be747e-49f5-4ddb-8a17-e514b9603a14/trigger17.png)
    
    When pressing the **F** key, if the Level Sequence is currently playing, it will immediately jump to the end and stop playing. The **Go to End and Stop** node is useful for situations when you want to allow your player to skip your cinematic but continue with any changes that Sequencer would have applied if the Sequence continued playing.
    
    For example, in our cinematic, Sequencer turns on a light in the Level. If the player skips the cutscene of the light being turned on, we still want the light to be on after the cutscene is skipped. If we were to simply use the **Stop** node to stop playing our cinematic, it would not complete the cinematic and would stop at whatever point in the cinematic we chose to stop (meaning the light would not be fully on or not on at all depending on where we stopped).
    
18.  Return to the Main Editor, then from the Main Toolbar, click the **Play** button to play in the Editor.
    

## End Result

When you play in the Editor, you will notice that the light is not on by default. When entering the Trigger Box, the cinematic will start playing and the light will turn on and stay on when the cinematic completes. You can re-trigger the cinematic by entering the Trigger Box again, which will play the sequence from the beginning. You can also enter the Trigger Box and press the **F** key to skip the cinematic, which will result in the light automatically turning on.
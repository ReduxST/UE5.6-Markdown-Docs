# Actor Rebinding in Blueprints with Sequencer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/change-cinematic-track-bindings-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/change-cinematic-track-bindings-in-unreal-engine)  
**Processed:** 2025-06-14 16:12:21

---

When creating cinematics for gameplay purposes, there may be times when you want to animate an object in Sequencer that is dynamically spawned at runtime. For example, you can create and animate an object that moves along a path within Sequencer but that object is something which can be defined by the player that is spawned during gameplay. With the help of [Blueprints Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine), you can expose binding identifiers from a Level Sequence using the **Get Sequence Bindings** node and override any of those bindings with your own settings.

In this example, we animate and move an Empty Actor along a path, allowing the player to change the object to different effects with the press of a button.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19f6ec05-3feb-4bcf-978a-e503c5698bba/endresult.png)

For this how-to guide, we are using the **Blueprint Third Person Template** project with **Starter Content** enabled.

## Steps

1.  From the **Place Actors** panel in the **Basic** tab, drag an **Empty Actor** into the Level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b908090-34ac-41cd-b2dc-3ff172142f7e/dynamicanim_01.png)
    
    We will animate this Empty Actor inside Sequencer and override the Sequence Bindings to change the Actor to different particle effects.
    
2.  From the Main Toolbar, click the **Cinematics** button, then select **Add Level Sequence** and give the Sequence any name.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f81af1f1-20f0-43ce-a57b-ae529a0f1b00/dynamicanim_02.png)
3.  Select the Empty Actor in the Level, then add the Empty Actor to Sequencer.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7cd7f9d5-e526-4137-99cc-ab759cdc69fe/dynamicanim_03.png)
4.  Click the **Track** button on the Empty Actor and select **Transform**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56a7ccb3-76e9-4a62-b943-54c970661e09/dynamicanim_04.png)
5.  Add a keyframe for the **Transform** track to initialize the Empty Actors current location in the Level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/628850b6-0038-49bb-91ed-64aaf44341c8/dynamicanim_05.png)
6.  Scrub the Timeline ahead to frame **75**, then move the Empty Actor up in the Level and add a keyframe for the new position.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/beba8255-13fa-40c4-9a0d-0c8712571787/dynamicanim_06.png)
7.  Right-click and copy the first keyframe in Sequencer, then move to frame **150** and right-click and **Paste** the **Transform** key.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8d7f090-6170-4f97-b803-fb3ce56a7789/dynamicanim_07.png)
    
    Copying the first key and pasting it at the end will give us a smooth sequence that we can loop.
    
8.  In the **Details** panel for the Level Sequence, enable **Auto Play** and set **Loop** to **Loop Indefinitely**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e11ccea-4495-4acb-b310-38a90c1d04eb/dynamicanim_08.png)
9.  From the Main Toolbar, click the **Blueprints** button then select **Open Level Blueprint**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b876c141-1009-4d69-a302-7c96d0b67e92/dynamicanim_09.png)
10.  In the **Level Blueprint**, right-click and add an **F** keyboard event connected to a **Flip Flop** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61d1a397-3030-481c-96f0-f6bc2f4a2b85/dynamicanim_10.png)
11.  Add two **Spawn Actor from Class** nodes (one using **Blueprint Effect Fire** and the other using **Blueprint Effect Sparks**) and connect to a **Make Transform** node as shown.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71034076-f9f3-4718-90b2-c081fcf9e0b1/dynamicanim_11.png)
12.  Right-click on the **SpawnActor Blueprint Effect Fire** node's **Return Value** and select **Promote to Variable** and call it **Fire BP**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11a5fc1f-78a5-4bb4-92d6-e727cca19a89/dynamicanim_12.png)
13.  Promote the **Return Value** for the **SpawnActor Blueprint Effect Sparks** to **Sparks BP**.
    
14.  Add a reference to your Level Sequence, then off it, use the **Add Binding** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2167e0be-12cb-47be-bee1-a53169421e51/dynamicanim_13.png)
15.  Create another **Add Binding** node and connect each as shown below, feeding the **Fire BP** and **Sparks BP** as the **Actor**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d9f01e8-79f8-472d-836f-97793469a235/dynamicanim_14.png)
16.  Right-click and use the **Get Sequence Binding** node (setting the options highlighted below) and connect to both **Add Binding** nodes.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ad5bdc2-1043-400c-8060-655ec99c2dc7/dynamicanim_15.png)
    
    On the **Get Sequence Binding** node, you can specify the Level Sequence you want to target and the **Binding** you want to override. In our example, we only have one track listed in our Level Sequence (our Empty Actor) that we can override. Objects that are added to your Level Sequence that can be overridden will be displayed in the drop-down menu.
    
17.  Bring in the **Sparks BP** and **Fire BP** variables and use an **IsValid** node and **Destroy Actor** if the object is valid.
    
    Click image for full view.
    
    Our script is complete and will spawn either the fire or sparks effect, override the Empty Actor in our Level Sequence then destroy the other particle effect (if it is valid).
    
18.  Play in the Editor, then press the **F** key to cycle between our spawned Actors.
    

## End Result

When we play in the Editor and press the **F** key, our Empty Actor is replaced by our spawned fire or spark effect and continues to use the animation we applied to the Empty Actor.

Not only can you add bindings, you can:

-   **Remove Binding** to remove the specified Actor from the specified binding.
-   **Reset Binding** to reset the specified binding back to its default settings.
-   **Reset Bindings** to reset all overridden bindings back to the default settings.
-   **Set Binding** to override the specified binding with the specified Actors.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1cb6eb75-d2b0-423b-8de4-a1c6ba323594/additionalfunctions.png)
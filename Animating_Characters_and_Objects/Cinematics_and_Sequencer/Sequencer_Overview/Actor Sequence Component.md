# Actor Sequence Component

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-blueprint-component-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-blueprint-component-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:20

---

This is an experimental feature that is currently undergoing development. Some aspects may not work as expected or may change in future revisions.

When working with and creating [Sequences](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview), there may be situations where you want to reuse the functionality of a Sequence in other places or instances. With the **Actor Sequence Plugin** and **Actor Sequence Component**, it is possible to embed Sequences directly into an Actor [Blueprint](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine). This enables reuse of Sequences by binding the animations to the Blueprint instance and triggering them automatically or through the **Event Graph** of the Blueprint. Additionally, you can add an Actor Sequence Component to any Actor in the world to add animations to a single instance of an Actor.

In this how-to guide, you'll create a Blueprint with an embedded Sequence that animates and changes the color of a Spot Light over time.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73aa4bbc-c926-4e99-a823-ab449fae3d7d/endresult.png)

The Blueprint can then be placed in any level or duplicated and the embedded Sequence will play automatically when called.

## Steps

For this how-to guide, we are using the **Blueprint Third Person Template** with **Starter Content** enabled.

1.  With your project open, from the **Edit** menu select **Plugins**.
    
2.  From the **Plugins** menu, under **Built-in**, enable the **Actor Sequence Editor** option and restart the editor when prompted.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed902a74-8344-4975-84da-5b1df513be97/actorsequence02.png)
    
    You may see the **Experimental** confirmation dialog window when enabling the Actor Sequence Editor, click **Yes** to proceed.
    
3.  Create a new **Blueprint** of the **Actor** type can call it **Light\_BP**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a648dc86-527f-40d8-aa10-7c147b87eeb1/actorsequence03.png)
4.  Inside the **Light\_BP**, click **Add Component** and add a **Spot Light**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66bee7d1-7f33-4c16-9a35-f5c385fa1d53/actorsequence04.png)
5.  In the **Details** panel for the **Spot Light**, change the **Rotation** value for **Y** to **\-60**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43cfda98-7e46-4dcb-a43c-5c466fb8de79/actorsequence05.png)
    
    This will rotate and angle the light slightly downward in the viewport.
    
6.  Add another **Component** of the **Static Mesh** type, then in the **Details** panel set the mesh to **Floor\_400x400** with its **Location** set to **\-180 (X), -180 (Y), -100 (Z)**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab0d585e-16d3-4d22-8bc9-62174bd1c777/actorsequence06.png)
    
    We will use this Floor Mesh to shine our Lights on and to see the effects of Sequencer driving the parameter changes.
    
7.  Add another **Component** of the **Actor Sequence** type.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/696dda01-80da-4547-a5b7-cf9583b9e813/actorsequence07.png)
8.  In the **Details** panel for the **Actor Sequence**, set **Loop Indefinitely**, **Random Start Time** and **Auto Play**, then click **Open in Tab**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35a345d9-91d1-4f6a-bd79-81ce91e487f4/actorsequence08.png)
    
    After clicking **Open in Tab**, the **Sequencer Editor** will open within the Blueprint.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3294e5cd-831c-481c-9094-1087ae0ebcac/sequencerwindow.png)
    
    For this example we will automatically trigger and play the Sequence, however, you can also call this to play from the **Event Graph**.
    
9.  In the **Sequencer** tab, click **Add** then under **Component** select **SpotLight**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/671e19a2-1699-4bcb-a81d-67948cecca6a/actorsequence09.png)
10.  On the **SpotLight** track, click the **Track** button and select **Transform**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36906914-25ff-4728-a349-4006925d73a6/actorsequence10.png)
11.  Click the **Track** button again for the **SpotLight** track and add the **Light Color** track.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9f1e3e9-a219-4c2b-8f51-2aaf60015ce9/actorsequence11.png)
12.  For the **Transform** track under **Rotation**, click the **+** icon for the **Z** value to add a key of **0** at frame **0**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db8eb385-9e2c-4052-89cb-2bd631dbb63f/actorsequence12.png)
13.  Select the key that was added, then press the **4** key to change the interpolation type to **Linear**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a5be34c-b86f-45bb-96e3-4bb6c138098a/actorsequence13.png)
    
    You can change the type of interpolation with the number keys or by right-clicking on the keyframe and selecting your interpolation method.
    
14.  Add a key at **2.00** for the **Z** value of **Rotation** set to **\-180.0** and change the interpolation to **Linear** by pressing **4** on the key.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98d3f858-ac33-414a-99cf-5a4babea02a4/actorsequence14.png)
15.  Add a key at **4.00** for the **Z** value of **Rotation** set to **\-360.0** and change the interpolation to **Linear** by pressing **4** on the key.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/462c8c31-61d3-4bbe-b85d-2a4a73d11827/actorsequence15.png)
    
    You can also move the red **End Marker** back to **4.00** so the Sequence ends where it began.
    
16.  For the **Light Color** track, click the **Add (+)** button to add a key at frame **0**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8cd94155-b8f0-4ac3-81b4-26014a64502d/actorsequence16.png)
17.  Add a key at **1.00** for **Red** with a value of **0.0**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d62ee75c-78b7-42f5-8e59-de8fc17855b5/actorsequence17.png)
18.  Add a key at **2.00** for **Green** with a value of **0.0**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/983dda6b-d1e0-438e-a67f-90c9b7c7464b/actorsequence18.png)
19.  Add keys at **3.00** for **Blue** with a value of **0.0**, and both **Red** and **Green** at **1.0**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8b2ac43-546a-4937-80f4-88d3512b81b0/actorsequence19.png)
20.  Add a key at **4.00** for **Blue** with a value of **1.0**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf0d086b-a56c-4334-9b71-1d6591ecec91/actorsequence20.png)
    
    This will cause the light to go from white to various colors before returning back to white at the end of the Sequence.
    
21.  In the **Components** window, select and **Delete** the **StaticMesh** floor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6346b427-14c0-4a02-88ad-388776e8b2dd/actorsequence21.png)
    
    Now that our light is set up, we no longer need this mesh as a way to preview the light in the viewport.
    
22.  In the Main Level Editor Viewport, select the floor, then while holding **Alt** drag up a copy of the floor to create a roof encapsulating the level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dccf5165-5db7-4f1d-9bdb-4e5e4f41f1a8/actorsequence22.png)
23.  From the **Content Browser**, drag and place instances of the **Light\_BP** in the level (you can also press **E** and rotate them if desired).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be409a4a-1973-4c77-a982-8cd1fc2af10e/actorsequence23.png)
24.  From the **Build** drop-down menu, select **Build Lighting Only** to rebuild the lighting in the level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/008ab500-c6e3-404a-b392-6d3c27dae138/actorsequence24.png)
25.  Click the **Play** button to play in the editor.
    

## End Result

When you play in the level, you will see that the lights you placed start rotating and changing colors playing the embedded Sequence.

Since the Sequence is embedded within the Actor Blueprint, it has no dependencies and can play in any level or can be duplicated without any issues.

In our example we've set the Sequence to **Auto Play**, however, you can also use the **Event Graph** to script when the Sequence should Play.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c312f878-ecf2-4498-8314-f6aa94f11a0b/eventgraphplayscript.png)

Above, upon **Event BeginPlay** we have allowed the Actor to receive input from a **Player Controller**. When the **P** key is pressed, we take the **Actor Sequence Component** and get the **Sequence Player** which allows us to make a call to the function **Play** to start playing the Sequence. You can use any method you desire to make the call to the Play function if you prefer not to have the Sequence Auto Play upon level load.
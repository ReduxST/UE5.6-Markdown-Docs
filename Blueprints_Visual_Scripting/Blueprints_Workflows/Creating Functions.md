# Creating Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:30

---

**Functions** are node graphs belonging to a particular **Blueprint** that can be executed, or called, from another graph within the Blueprint. Functions have a single entry point designated by a node with the name of the Function containing a single exec output pin. When the Function is called from another graph, the output exec pin is activated causing the connected network to execute.

The steps below will guide you through creating a Function which will print text to the screen when a button is pressed.

1.  Inside the **Content Browser**, click the **New** Button then select **Blueprint Class**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4ebaee7-2421-48c5-8162-8e6dd978b6ac/newblueprint.png)
2.  In the **Pick Parent Class** window, select **Actor**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/822b06da-383d-44bd-bedf-8a38d418c337/actorblueprint.png)
3.  Name the Blueprint, then **Double-click** on it to open it up in the Blueprint Editor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71b6f46c-9e55-4abc-9e48-4d65753b4c8a/functionblueprint.png)
4.  **Right-click** in the graph and search for and add the **Event Begin Play** Event.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72ed5907-a319-4879-87d6-d388516cd435/eventbeginplay.png)
    
    This node will execute once when the game is launched, along with any script that follows it.
    
5.  **Right-click** in the graph and search for and add the **Get Player Controller** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b71d0ac-cbdd-43fc-8789-bebac16e1ed5/getplayercontroller.png)
    
    This will get the currently assigned player controller and allow us to Enable Input for this Blueprint.
    
6.  **Right-click** in the graph and search for and add the **Enable Input** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65eb53c4-6b28-4fef-a843-5bf999d0d996/enableinput.png)
    
    This is the node which will allow input to be received for this Blueprint.
    
7.  Connect the nodes as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7718fa6-6bb9-4414-920a-082d60d6eb70/connectnodes.png)
    
    When the game is launched, we get the player controller and enable input from it in this Blueprint.
    
8.  In the **MyBlueprint** window, click the **Add New Function** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e652fc5-d08a-4bda-93f3-b4098bfe6d8c/addfunctionbutton.png)
9.  Select the new function in the **My Blueprint** window and press **F2** to rename it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/670b4fee-c797-4bec-aa6e-10c0ad43db95/renamefunction.png)
    
    Give the Function a name such as "Print Text".
    
10.  In the Function's graph, drag off the **Print Text** pin and search for and add a **Print String** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0c8e645-7d5e-4954-a014-526cbab3c41d/printstringfunction.png)
11.  In the **In String** box, you can leave or change the text to the text you want to display in-game.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3458bac6-5d4e-4393-acea-c40489a47ecf/entertext.png)
12.  Click the **Event Graph** tab to return to the Event Graph.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb43458f-304d-4bd8-bf14-b4ef604fd955/eventgraphtab.png)
13.  **Right-click** in the graph and search for and add an **F** Key Event.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55684efe-d8ce-47ed-a167-c23cec47440a/fkeyevent.png)
14.  Drag off the **Pressed** pin and search for and add your **Print Text** function.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c99b523-b856-49e0-9b11-37f6c2546561/callfunction.png)
    
    When **F** is pressed, it will call the Print Text function which is set to print text to the screen using a Print String.
    
    If you do not see your function, try clicking the **Compile** button from the Toolbar then try your search again.
    
15.  Your network should look similar to below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c87571b6-1f30-4466-98cf-cf582b141166/finishedgraph.png)
16.  Click the **Compile** button then close the Blueprint.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e51db14-8d49-4f41-9029-5561b8699b1e/compilebutton.png)
17.  Drag the Blueprint into the level, then click the **Play** button to play in the Editor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e606c4d-55c6-423a-ad3d-e9d0ff539b25/dragintolevel.png)
18.  Press **F** and the Function will be called and print your text to the screen.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7765ffd-854b-4b8e-b354-9d6b44327765/workingfunction.png)

While this example Function only prints text to the screen when a key is pressed, you could add more script to the Function which would be executed by the assigned key press.

For example, your Function could be used to cast a spell when the key is pressed and the script containing the spawning of the spell and its location, the effects associated with the spell and how it affects the world, or if it damages other Actors could all be contained within the function leaving your Event Graph free from all that script which would be contained neatly within the Function.

There are other ways Functions can be used and accessed, for more on Functions please see the **Related Topics** section below.
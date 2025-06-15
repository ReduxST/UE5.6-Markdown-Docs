# Using a Single Line Trace (Raycast) by Channel

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-a-single-line-trace-raycast-by-channel-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-a-single-line-trace-raycast-by-channel-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:07

---

**Line Trace By Channel** will perform a collision trace along a given line and return the first Object that the trace hits. Below, you will find steps for setting up a **Single Line Trace By Channel** Blueprint.

## Steps

1.  Create a new project using the **Blueprint First Person** template with **Include Starter Content** and open the project.
    
2.  In the **FirstPerson/Blueprints** folder, open the **BP\_FirstPersonCharacter** Blueprint.
    
3.  Right-click in the graph, search for and add an **Event Tick** node.
    
    ![Add an Event Tick node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dcd49e7f-84c2-4fa4-a9e5-3baf62d5a2f0/guide-how-to-2b-1.png)
    
    This will cause the trace to run every frame.
    
4.  Drag off the execute pin, then search for the **Line Trace By Channel** node.
    
    ![Search for the Line Trace By Channel node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/243f760d-f655-4247-8c43-a8b6ea39de69/guide-how-to-2b-2.png)
5.  While holding down the **Ctrl** key, drag in the **First Person Camera** component.
    
    ![Drag in the First Person Camera component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e0195ef-467d-43cc-9559-dae19ec84f72/guide-how-to-2b-3.png)
    
    The camera is where we will start our trace from.
    
6.  Drag off the **First Person Camera** node, and add a **Get World Location** node, then connect it to the **Start** of the trace.
    
7.  Drag off the **First Person Camera** node again and add a **Get World Rotation** node.
    
    ![Add a Get World Rotation node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/570621e3-fb36-4dd3-8256-62fea3f17b61/guide-how-to-2b-4.png)
    
    Here, we are starting the trace from the location of the First Person Camera, then we are getting the rotation of the First Person Camera.
    
8.  Drag off the **Get World Rotation** node and add a **Get Forward Vector**, then drag off that and add a **Vector \* Float** node set to **1500**.
    
    ![Drag off the Get World Rotation node and add a Get Forward Vector then drag off that and add a Vector Multiple Float node set to 1500](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a1f9b50-e595-4b3f-afb6-b9ce831dc5fb/guide-how-to-2b-5.png)
    
    We are getting the rotation and the forward vector, extending outward from it by 1500 (this value is the length of the trace).
    
9.  Drag off the **Get World Location** node and add a **Vector + Vector** node, connecting (as shown below) to the **End** of the Line Trace By Channel node.
    
    ![Drag off the Get World Location node and add a Vector Plus Vector node connecting to the End of the Line Trace By Channel node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f64e0a22-515e-41bb-af3a-c93361c5631f/guide-how-to-2b-6.png)
    
    Here, we are taking the location of the First Person Camera and extending out from it, 1500 units based on its rotation and forward vector.
    
10.  On the Line Trace By Channel node, set the **Draw Debug Type** to **For One Frame**.
    
    ![Set the Draw Debug Type to For One Frame on the Line Trace By Channel node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4681952d-418f-4bab-b35d-7a333bf4d1ca/guide-how-to-2b-7.png)
    
    This will allow us to see a debug line while playing in-game to see our line trace.
    
11.  Drag off the execution out pin of the Line Trace By Channel node and add a **Print String** node.
    
    ![Drag off the execution out pin of the Line Trace By Channel node and add a Print String node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed79efc2-4142-48a9-9a8b-18afb66241ee/guide-how-to-2b-8.png)
12.  Drag off the **Out Hit** pin and search for **Break Hit** then add a **Break Hit Result** node.
    
    ![Drag off the Out Hit pin and search for Break Hit then add a Break Hit Result node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4989daba-35b5-4100-9227-7ea749c7f69e/guide-how-to-2b-9.png)
13.  Drag off the **Hit Actor** pin (off of the **Break Hit Result** node), add a **To String (Object)** node, and connect it to the **Print String** node.
    
    Click image for a full view.
    
    This will allow us to debug print the object we hit with our trace.
    
14.  Click the **Compile** button, then play in the Editor and look at the cubes in the level.
    
    ![Play in the Editor and look at the cubes in the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd67ce85-1155-4bfd-9da7-6a7f4c9126d8/guide-how-to-2b-11.png)
    
    Here, we have ejected from the First Person's perspective so that you can see the view angle of the trace.
    
    You should see that when the trace hits a cube, it prints the cube to the screen.
    

## End Result

The example above returns all Objects that are set to respond to the provided Trace Channel, however, there may be instances when you want to only return certain objects. In the example above, you can use the **Actors to Ignore** pin, taking an Array of Actors that should be ignored by the trace (this means that you have to specify each Actor to ignore).

You can also perform a **Line Trace By Object** where only the specified **Object Types** are returned. This will allow you to target a specific set of Objects (only to be included in the trace).
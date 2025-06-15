# Using Sprite Sockets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-sprite-sockets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-sprite-sockets-in-unreal-engine)  
**Processed:** 2025-06-14 16:42:00

---

On this page you will learn how to add sockets to sprites then access those sockets from within a Blueprint which you can attach an object to. You can spawn particle effects from sprite sockets (such as a character on fire), attach a weapon to a character's hand (like a gun or sword) or any number of different items that you want to spawn and attach to a sprite's socket.

For this example we will attach a hat to our character's head.

**To add a socket to a sprite**:

1.  Locate the sprite you wish to add a socket to and open it.
    
2.  In the **Details** panel, click the **+** next to **Sockets** to add a new socket.
    
3.  Enter in a **Socket Name** and move the socket where you would like using the **Local Transform** or widget inside the viewport.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e101c776-cf1a-489b-acee-2060a1e1336f/addingsocket.png)
    
    To move the socket in the viewport, you may need to zoom in and click on the socket first.
    

It is important to note the name you give your socket. Above we have created a new socket called *HatSocket* to which we want to spawn in a 2D hat for our character to wear. The steps above have only covered one sprite, in our idle animation we are using 8 different sprites so we need to add sockets to each of those sprites as well.

A quick way to do this would be to use the **Property Matrix**.

**Add Sockets to Several Sprites**:

1.  In the **Content Browser**, select each of the sprites in your Flipbook animation that you want to apply sockets to.
    
2.  **Right-click** on a sprite, then under **Asset Actions** select **Property Matrix...**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/502b65eb-a5ca-472c-86e1-c920140d47c7/propterymatrix.png)
    
    By opening the **Property Matrix** we can modify each of these sprites at the same time which will save time.
    
    We also selected the sprite which we already added a socket to for reference so all 8 frames are selected.
    
3.  Inside the **Property Matrix**, select each of your sprites (which do not have sockets) then click the **+** to add sockets to them.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8cf7f2a-9260-4a90-b44a-b0e9628783de/addsockets.png)
4.  Expand element 0, then under **Socket Name** name them the same as your first sprite (in our example **HatSocket**).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba85b93a-b159-466a-bc09-3383b67cc077/addsockets2.png)
5.  Expand **Local Transform** then **Translation** and set the XYZ values to the same as your first sprite.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a3aae4c-79b0-4f98-b7d0-e0cfdfe8bf57/addsockets3.png)
6.  Open up each of the sprites in your animation to ensure that a socket has been added to each.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae10d348-fe6a-4a96-b016-818035e06fb8/addsockets4.png)
    
    You may need to adjustment the socket location per sprite to ensure it is at the desired location for that frame.
    

Now that we have a socket attached to each frame of our Flipbook, we can tell our Blueprint to spawn an Actor at the socket location.

**Accessing Sprite Sockets via Blueprint**:

1.  Inside our Character Blueprint, in the **My Blueprint** window click the eye icon and **Show Inherited Variables**.
    
2.  **Left-click** and drag in the **Sprite** component for your character.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09804367-d698-4857-ac26-29897af9941b/blueprint1.png)
3.  Off an **Event Begin Play** node, add a **Spawn Actor from Class** node set to the Actor Class you want.
    
4.  Use a **Make Transform** node for the **Spawn Transform** and off the **Return Value** use an **Attach To** node.
    
5.  Connect your **Sprite** component as the **In Parent** and for the **In Socket Name** enter the Socket you created.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/daa7ff09-9c3e-4a9e-b6d6-62f3f5bf0e54/blueprint2.png)
    
    Your setup should look similar to above. For example we are just spawning a Blueprint called **Hat\_BP** which is a Blueprint containing a Sprite Component of a hat that we are attaching to our character at the **HatSocket** location we've created. The same process we took above for our idle frames, we've done for our run frames so that we end up with a character that wears a hat in our game (as seen below).
    
6.  Once you **Compile** and play in the editor, the Actor Class spawned will spawn at the socket location and become attached.
    

You could add a socket to a sprite and attach any number of different things in that socket, whether or not the sprite is part of a Flipbook and is animated as well as what goes in the socket is entirely up to you.
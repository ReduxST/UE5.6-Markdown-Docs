# Top Down 2D Game Setup

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-example-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-example-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:46

---

On this page you will learn how to modify the existing **Third Person Template** project to create a **Top Down 2D** style game.

You can use your own 2D character with this tutorial or you can download a sample character from the link below:

-   [Sample Assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/174dccf9-78f5-4471-9752-2ff1470627cb/sampleassets.rar)

## Setup Project

Here we will set up our project for this tutorial, you can import your own assets during this section or use the Sample Assets provided.

1.  Create a new **Third Person Blueprint** template project.
    
2.  Inside the project, **Right-click** on the **Content** folder in the **Content Browser** and create a **New Folder**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a743a80-0621-4224-8dc6-98a01c852b6f/topdown1.png)
    
    Give the folder a name such as **TopDown** or whatever you would like.
    
3.  Locate the downloaded Sample Assets and drag the **SoldierSprites.paper2dsprites** asset into **Content Browser**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6103567e-6034-4b3e-9901-d9af4f73cb34/topdown2.png)
    
    This will automatically create a **SolderSprites** Sprite Sheet asset and folders containing **Frames** and **Textures**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/073f498a-754b-4e5a-8640-d45a0e4112c6/topdown3.png)
    
    For more information on how to set up assets for importing, see the [Paper 2D Import Options](/documentation/en-us/unreal-engine/import-sprites-in-unreal-engine) documentation.
    
4.  **Right-click** on the **SoldierSprites** asset and select **create Flipbooks**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c791367-9469-4eda-b3df-2deb9242c18a/topdown4.png)
    
    This will automatically create two Flipbooks based on the sprite sheet for us.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ca19cc6-c52c-434c-b825-519bd85ad7db/topdown5.png)
5.  (Optional) Open the **Idle** Flipbook and in the details panel set **Frames Per Second** to **3.0**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47ffecb1-9da8-49e9-bf6a-2c4a13b4cdab/topdown6.png)
    
    Also set the **Run** Flipbook **Frames Per Second** to **8.0**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7d990d3-9baa-47c9-97f5-fe3a837413a2/topdown7.png)
    
    This will slow down the playback speed of both Flipbook Animations.
    

Our project is now set up and we can begin setting up the Top Down Character.

## Character Setup

Here we will create a new Paper 2D Character Blueprint and set up the character.

1.  **Right-click** in the **Content Browser** and select to create a new **Blueprint Class**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da34f048-2e1c-48b3-8993-5515784ef2eb/topdown8.png)
2.  In the **Pick Parent Class** window, click the **All Classes** drop down and search for and add the **PaperCharacter**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93195742-6b6c-4406-826f-171c12e90881/topdown9.png)
    
    Give the new Blueprint a name such as **TopDownCharacter**.
    
3.  Inside the **TopDownCharacter** Blueprint, in the **Components** window click the **Sprite** component.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2f63070-ab0d-420e-9809-99ecdaa8da71/topdown10.png)
4.  In the **Details** panel under **Sprite** click the **Source Flipbook** drop down and select the **Idle** Flipbook.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/099cdf61-b000-4a8a-9d22-675c7014e099/topdown11.png)
    
    The character will then be added to the **Viewport** inside the Capsule Component.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4dea604-f59f-4f4d-a7c7-956281bb98df/topdown12.png)
5.  Back inside the **Details** panel under **Transform**, set the **Rotation** to **\-90,0,90** and **Scale** to **0.75** for XYZ.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/626ae742-08fe-4017-95fb-eb10f8977f3e/topdown13.png)
    
    This will rotate the Flipbook into position and scale it down so it fits inside the Collision Capsule.
    
6.  In the **Components** window, click the **CapsuleComponent** then in the **Details** panel adjust the **Shape** settings.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5b353ec-a441-413d-8a5d-752c2b1c8045/topdown14.png)
    
    This will vary based on the character you are using, we have set both **Half Height** and **Radius** to **45.0**.
    
7.  In the **Components** window, click **TopDownCharacter(self)** then in the **Details** panel, un-check **Use Controller Rotation Yaw**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7297f16-0a23-4dec-957f-c346b43371ae/topdown15.png)
    
    For this example we are going to automatically orientate our character to the direction they are moving and not use the controller rotation.
    
8.  In the **Components** window, click the **CharacterMovement** component.
    
9.  In the **Details** panel for **CharacterMovement**, update the **Max Walk Speed** to **400** and check **Orient Rotation to Movement**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87231afe-7155-4612-b73a-d8855007f510/topdown16.png)
    
    This will reduce the characters movement speed and automatically rotate the character based on our movement.
    
10.  In the **Components** window, click **Add Component** and search for and add a **Spring Arm** component.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93c6236e-cdbc-4a59-94ff-02c27ddd5b01/topdown17.png)
11.  Click **Add Component** again and add a **Camera** component, then drag the Camera onto the Spring Arm to attach it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66ab701d-a2b3-44f5-8277-ac9c35d7e23d/topdown18.png)
12.  Select the **Camera** component, then in the **Details** panel, zero out the **Location** setting.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bd981b4-7ba0-411a-a148-4d92ac8bc194/zerocamera.png)
13.  Select the **Spring Arm** then make the following updates in the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e77a94e3-8511-4da9-94ce-eef287bcc129/topdown19.png)
    
    Here we are adjusting the **Rotation** of the Spring Arm (and by extension, Camera) to **180, -90, 180** to position the camera directly above the character. We are also adjusting the camera distance away from the character by changing the **Target Arm Length** to **600**. Finally we've unchecked the **Inherit** options for **Pitch, Yaw and Roll** as we do not want to inherit settings from the camera.
    
14.  Click **Compile** and **Save** then minimize the Blueprint (we will come back to it in a moment).
    

The character is setup, however there is no movement script applied to it which we will grab from the **Third Person Character** Blueprint.

## Finishing Up

There is no need to reinvent the wheel here, since this template comes with a character with scripted functionality for movement, we can copy that into our Paper Character to provide movement for it.

For more detailed information on setting up character movement and setting up character movement from a blank project, see the [Setting Up Character Movement in Blueprints](/documentation/en-us/unreal-engine/setting-up-character-movement) documentation.

1.  Inside the **ThirdPersonBP** folder in the **Content Browser**, open the **Blueprints** folder then the **ThirdPersonCharacter** Blueprint.
    
2.  Inside the **Event Graph**, copy the **Movement Input** section by **Left Mouse** dragging a selection box then pressing **Ctrl+C** to copy.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a241bef-604a-4b04-8506-87eba541118e/topdown20.png)
    
    There is other script in here for 3D gameplay such as manipulating the camera, controller input and jumping. For the purposes of this tutorial we are only concerned with general movement.
    
3.  Return to your **Paper Character** Blueprint and press **Ctrl+V** in the **Event Graph** to paste it in.
    
4.  Also inside the **ThirdPersonBP** and **Blueprints** folder, open the **ThirdPersonGameMode** Blueprint.
    
5.  Under **Classes**, change the **Default Pawn Class** to your **Paper Character** (*TopDownCharacter*).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7726c9f3-2293-4992-a449-30a7e1be5984/topdown21.png)
    
    This will set our Paper Character as the default character to use during gameplay.
    
6.  Inside the level delete the Blue Character so you will not take control of it when launching the game.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17a5aacd-9985-4fc9-8d30-a77214bef3ff/deleteme.png)
7.  From the Main Tool bar, click the **Play** button to play in the editor.
    
    Although the 2D character is idle, you can now move around the default map using the **WASD** keys.
    

This tutorial illustrates how to set up the foundation of a top down game by creating a playable 2D character, there are other tutorials you can take a look at to continue to develop this sample such as the **Setting up an Animation State Machine** (to set up different Flipbook Animation states for the character to use) as well as the section on **Paper 2D Tile Maps** to create a 2D map. Want a fixed camera position instead of a follow camera for your top down game? The **How to Use Cameras in Blueprints** page will show you how to set that up and more.
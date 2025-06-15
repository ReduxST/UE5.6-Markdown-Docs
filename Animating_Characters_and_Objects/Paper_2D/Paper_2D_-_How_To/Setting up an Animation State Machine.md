# Setting up an Animation State Machine

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-setting-up-an-animation-state-machine-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-setting-up-an-animation-state-machine-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:52

---

On this page you will learn how to set up an Animation State machine for a 2D character which will allow the character to cycle between different Flipbook animations based on your defined criteria.

This tutorial assumes you have a Paper 2D character that is already set up for movement and have some Flipbook animations that you want the character to switch between. If you do not have a character or Flipbook animations, see the [Paper 2D Top Down Tutorial](/documentation/en-us/unreal-engine/paper-2d-example-in-unreal-engine) for information on setting up a Paper 2D character and applying movement as well as a link to the sample assets used in this tutorial.

With your project open and Paper 2D character ready to go, follow the steps below.

## Variable Setup

1.  Inside your project, open your Paper 2D Character Blueprint (**TopDownCharacter** in our example).
    
2.  In the **My Blueprint** window, click the **Add Variable** button to create a Bool variable and name it **IsMoving?**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/870dca49-b650-4c0c-810b-9de2f77afebe/animation1.png)
3.  Create and name another variable based on one of your Flipbook animations (such as Idle) and set it to a **Paper Flipbook** type.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11253441-7d0a-44cb-b03f-63f80283a772/animation2.png)
    
    Depending upon the type of game you are making, you may have different animations. Most character based games, have a state where the character is idle (or resting and not moving).
    
4.  Click **Compile** then set the default value of the variable to its corresponding Flipbook asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3fc7209c-689e-4b30-934a-0f104abc1fb1/animation3.png)
    
    Above we have assigned our Idle Flipbook animation to our IdleFlipbook variable.
    
    (Optional) For the sake of clarity, you may also want to put the variable in a **Category** called **Animations**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd01325d-80b2-4639-9896-f87069f90367/animation4.png)
    
    You can type in the name of the category you would like and will keep things organized for you.
    
5.  Repeat the previous two steps for each of the animations that you want your character to be able to play.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc5e2581-e01f-4155-9501-d8c376e87f16/animation5.png)
    
    Above we have created another Paper Flipbook variable called **RunFlipbook**, clicked **Compile** then set the **Default Value** for that variable to our corresponding Run Flipbook animation. While our example only has the two animations, you could have one for a death animation, another for reloading a gun (if they have one) or a melee attack, another for picking up or using items, etc.
    
    Once you have added variables for each of our Flipbook animation states, proceed to the next section.
    

## Update Animation Setup

Next we will create some script to handle the updating of our Animation state.

1.  **Right-click** inside the **Event Graph** and search for and add a **Custom Event**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/950d88c0-e184-4668-899a-29676048cf06/animation6.png)
    
    Call the Custom Event something to the effect of **UpdateAnimation**.
    
2.  **Right-click** in the graph again and add a **Get Velocity** node, then drag off the return value and add the **Vector Length** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0bcda9d4-6e9d-45d6-a554-c50f18c46c9d/animation7.png)
    
    We can use the Vector Length of Velocity to determine if our character is moving or not.
    
3.  Off the return value of the Vector Length, add a **\>** node then drag-and-drop the **IsMoving?** variable onto the Bool return to set it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f3d62d7-184c-4081-bd67-2a7a1818fe50/animation8.png)

## Animation State Machine Function

Here we will create a function that will handle the checking of which state we are in and output a corresponding Flipbook animation to use.

1.  In the **My Blueprint** window, create a new **Function** called **Anim State Machine**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5d8c12b-614a-4b11-bf73-99d6d445f2f9/animation9.png)
2.  In the **Details** panel of the function, add an **Input** Boolean called **IsMoving?** and an **Output** Paper Flipbook called **Output Flipbook**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1fefe771-e477-4a98-979c-dca8c19e21b1/animation10.png)
    
    Our function will take in the value of our variable also called IsMoving? to check if we are moving and use that as a test case to determine what state we are in (moving or not). Our function will then output an *Output Flipbook* which we will set our sprite to use in a moment.
    
3.  Connect a **Branch** node off the input executable pin of the function.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3cf2fe30-8d80-47bd-83d5-da1c93d36a73/animation11.png)
    
    The first thing that occurs when this function is called is run a True/False check against our **IsMoving?** variable.
    
4.  Back inside the **Content Browser**, **Right-click** and under **Blueprints** create an **Enumeration** and call it **Animation State**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffa3cafb-bc97-4092-9ee8-c6315dab85a7/animation12.png)
    
    We are using an Enumeration to create a list of all our animation states that our character can be in which we can then select from.
    
5.  Open the Enumeration, then add a state for each of the animations that your character will enter.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8b3adc5-1741-4087-b860-7e143d9723ca/animation13.png)
    
    For example, we only have Idle and Run however you may have many more depending upon the animations you plan to use.
    
6.  Return to your Paper 2D Character Blueprint and create a new variable called **AnimationState** set to the Enum *Animation State*.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf0b4df4-ebd8-41df-b1a9-674b59ab40ed/animation14.png)
7.  Inside the **Anim State Machine** function, hold **Alt** and drag in the **AnimationState** variable to set it.
    
8.  Drag in another **AnimationState** variable and connect each to the **True** and **False** pins of the **Branch** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/143f7053-681e-4a34-9936-424eccc6b924/animation15.png)
    
    For the Enum connected to True, set the state to **Run** and set the other Enum to **Idle**. We are saying if IsMoving? is true set our Enum state to Run and if we are not moving set it to Idle. While our example only checks whether we are moving or not, you could add different Branch nodes to check different criteria based on your needs.
    
    One thing to note is that the order in which you process your checking is important and you'll want to prioritize certain states over others. For example, if we had a death Flipbook animation for our character would probably want to process that first and check if the character is dead and if so, we would want to play the death animation and kill the character. If they are not dead, then we can proceed on to the next series of checks (if the character is moving, attacking, using an item, etc. with the final check being if the character is not doing anything at all resulting in the Idle pose.
    
9.  Hold **Ctrl** and drag in the **IdleFlipbook**, **RunFlipbook** and **Animation State** variables, then **Right-click** and add a **Select** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0570d4fa-0f2f-44cb-ae7e-d7db4d627cd4/animation16.png)
    
    For this section, you will need to drag in each of your animation variables into the graph.
    
10.  Connect each of the nodes so the function is complete and looks similar to below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cab2340d-7c3b-46ca-8e8e-e8662310ef52/animation17.png)
    
    Our function now checks if we are moving and if so, sets our Enum state to Run (Idle if we are not moving). We then use a Select node to get our Animation State from our Enum and based on the state assigns the corresponding Flipbook as the *Output Flipbook* to use.
    

## Finishing Update Animation Event

Now that our function is complete, we will call it as part of our Update Animation Event and finish off the remaining script.

1.  On the **Event Graph** in the **My Blueprint** window, choose to **Show Inherited Variables** then hold **Ctrl** and drag in your **Sprite**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c5bc59f-ebb7-475d-a129-ac17e5737985/animation18.png)
2.  Drag in the **Anim State Machine** function and connect it to the **Set Is Moving?** node, then off your **Sprite** add a **Set Flipbook** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27f94a5d-aa47-410d-bd1b-8f369d5f1731/animation19.png)
3.  Connect all of your nodes together for the **UpdateAnimation** custom event as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70333e54-5267-4cb5-9f27-209e93e668ac/animation20.png)
4.  Following the **Add Movement Input** node from your MoveForward Event, call the **Update Animation** custom event.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19bf8225-7ae2-411c-829f-743921cc80bf/animation21.png)
5.  **Compile** and **Save** then play in the editor.
    
    You will now have a character that cycles between the two states based on your condition of whether or not the character is moving.
    

As mentioned, in order to add additional animation states to this setup you would need to:

-   Have Flipbook Animations for each of the animation states you want your character to enter.
-   Add and set them as Flipbook variables inside your Paper 2D Character Blueprint.
-   Add each of the states to the **Animation State** Enumeration we created.
-   Create conditions that determine when the character can enter each state and add it to the **Anim State Machine** function.
-   Connect each of your Flipbook variables to the **Select** node inside the **Anim State Machine** function.
# Calling Events through Sequencer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fire-blueprint-events-during-cinematics-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/fire-blueprint-events-during-cinematics-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:44

---

When playing a cinematic through **Sequencer**, there may be instances when you want to trigger an **Event** that initiates some scripted functionality. Perhaps at a certain point in your cinematic you want a door to open, or have a particle effect to spawn and effect the Player in some way. With the **Event Track** you can key the exact frame in the cinematic where you want to call the Event.

You can add Events through a Sequencer track without needing to access the Blueprint. You can add multiple Events to an object, or add multiple object bindings to a single Event. If you open the Blueprint, you can also add multiple Parameters to one Event. For more detailed information, refer to [Event Track Overview](/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine).

In this guide, we use several Event Tracks to print text to the screen indicating our character is dead. At the same time, we disable player movement and simulate physics on the character.

For this guide we are using the **Blueprint Third Person Template** project.

## Setting up the Character

First, we need to set up the Third Person Character.

1.  From the Main Toolbar, click the **Cinematics** button and select **Add Level Sequence** with any name and save location.
    
2.  In the **Details** panel for the Level Sequence, enable the **Auto Play** option.
    
3.  Select the **ThirdPersonCharacter** in the Level, then add it to Sequencer from the **\+ Track** button.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bbe7fe0b-6eac-4d4a-896e-57b5a49c76a4/neweventtrack_03.png "NewEventTrack_03.png")
    
4.  Right-click on the **ThirdPersonCharacter** in the Level, then select **Edit ThirdPersonCharacter**.
    
5.  Right-click in the **Event Graph** and search for then add a **Custom Event**.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4783e690-4fc1-4745-84d0-2869da3bc675/neweventtrack_05.png "NewEventTrack_05.png")
    
6.  Call the Custom Event **KillPlayerText** and connect a **Print String** node with custom text as the String.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a78118f5-6f59-45f5-b484-134035e69133/killplayer_text.png)
7.  Select the KillPlayerText node, and on the Details panel, go to **Inputs**. Select **+Add Parameter** to add a new parameter to the node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed76f220-2e35-415d-8d38-672f375b4a2b/add_parameter.png)
8.  Choose the **String** parameter from the dropdown and update the parameter name to **In String**. Then, connect the In String input from the Custom Event to the Print String.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbac9646-e62b-43c9-8e70-a774bc0fbb37/string_parameter.png)

## Adding Event Tracks

With the character set up, we can add Events so the character becomes disabled and prints the text from the Character Blueprint.

1.  In **Sequencer**, click the **\+ Track** button on the **ThirdPersonCharacter** track and select **Event**.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a555801-359b-45b9-848c-ccc53b4a3d4d/neweventtrack_07.png "NewEventTrack_07.png")
    
2.  Move the Timeline to frame **149**, then add a key to the Events track.
    
3.  Right-click on the new keyframe, and under **Properties**, select the **Unbound** dropdown to add **Create a Quick Binding**.
    
4.  In the Quick Bind, search for **Set All Bodies to Simulate Physics**. Make sure to check **New Simulate** under Payload.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ff1ca7b-e5e0-4292-a2d1-da193f158d0f/simulate_binding.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c50621c5-b638-4580-8241-51af3439dd75/payload1.png)
5.  Add a second Event Track and add a Quick Bind for **Disable Movement**.
    
6.  Add a third Event Track and add a Quick Bind to call the **Kill Player Text** we set up earlier. Under **Payload**, enter **GAME OVER!** in the **In String** textbox.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/804795ec-07e4-4bc7-b6a3-6a12573b4e99/payload_string1.png)
7.  **ALT+Drag** the string key to three other locations on the timeline. Update the first key's string text with **3**, the second key with **2**, and the third key with **1**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d30f7f34-a4b3-4468-a52f-d6bfd62574f1/payload_string2.png)
    
    Essentially, we are counting down to the GAME OVER! string text.
    
8.  From any key's **Event Properties**, double-click the **magnifying glass** icon to open the **Sequence Director Blueprint**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db0c11ee-ac96-44ad-af74-3b98249dffca/openbp.png)
    
    You can also open the Blueprint by double-clicking the event key or by navigating to **General Options > Open Director Blueprint**.
    
9.  Add a **SetCollisionEnabled** node to **Set All Bodies Simulate Physics**, and set the type to **Collision Enabled**. Connect the Target pin to the **Mesh** pin.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d136b472-fe8b-47e3-85e2-bc796b180e42/eventbp.png)
    
    This setting causes the character to collide into objects rather than fall through them. Even though we don't need to access the Blueprint to create Events, we do need the Blueprint to add onto Events, such as in this case.
    
10.  When you press **Play** you can run around in the viewport until the 150 second mark where the character dies and the text prints to the upper left corner of the viewport.
    

If the **Mouse Control** label appears in the upper left corner, you will not be able to see the text easily. To toggle this off, go to *Editor Preferences* > *Level Editor* > *Play*, and uncheck **Show Mouse Control Label**.

## End Result

When you play in the Editor, after a few moments, text will appear in the upper-left corner of the window and the character will fall to the ground with your ability to move disabled.

Adding an Event Track to an Object within Sequencer creates an Object Binding where you can call Events, Functions or access properties of the Object that you are bound to. Event Tracks can also be used to execute script within the Level Blueprint, UI Widget Blueprints, or communicate with multiple Blueprints through a Blueprint Interface.
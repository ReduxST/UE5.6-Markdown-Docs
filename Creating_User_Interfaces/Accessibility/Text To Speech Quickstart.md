# Text To Speech Quickstart

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/text-to-speech-quickstart-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/text-to-speech-quickstart-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:58

---

This guide describes how to create and enable a simple **Text To Speech** widget with two buttons. Each button vocalizes a text string when a user clicks it.

## Required Knowledge and Setup

Before you can complete the steps outlined on this page:

1.  Make sure you're familiar with the basic principles of the Unreal Motion Graphics (UMG) UI Editor.
    
2.  Create a new Unreal Engine project. You can use any template you like.
    
3.  Enable the Text To Speech plugin for your project. If you need more help with completing this step, refer to the [Working with Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) page.
    

## Create a New Widget Blueprint

In this step, you will create a widget that displays on-screen.

1.  In the **Content Browser** or **Content Drawer**, right-click an empty area. In the **context menu**, select **User Interface > Widget Blueprint**.
    
    ![Create a new Widget Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e2b79b9-0623-4d90-82d3-6514170f26b0/1-create-widget-blueprint.png)
2.  Select the **User Widget** class, then click **Select** to create your widget.
    
    ![Select widget class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/620235e1-0c3c-4dfe-b106-742d5cc2db75/2-select-widget-class.png)
3.  Name your new widget **MyWidget**.
    
4.  Double-click the **Widget Blueprint** to open it in the **Widget Editor**, then create a simple layout with two buttons, as shown below. The size and placement of the buttons is not important for the purpose of this tutorial, as long as you can click them easily.
    
    ![An example widget layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/475a646e-8099-4501-a31c-3e774ca056f2/3-example-widget-layout.png)
5.  **Compile** and **Save** your Widget, then minimize the Widget Editor.
    

## Add Your Widget to the Level Blueprint

Next, add your widget to the Level Blueprint so that it will be drawn on-screen when the game starts.

1.  From the **Main Toolbar**, open the **Level Blueprint**.
    
    ![Open the Level Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0024538e-5f18-4249-8d77-9ba7e5c75274/4-open-the-level-blueprint.png)
2.  In the **Level Blueprint**, drag from the **Event BeginPlay** node's execute pin. Search for and select **Create Widget**, then press the **Enter** key to create the node.
    
    ![Create a new widget node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92ef3c77-d2bb-4e2d-a947-101eaf8c1d6d/4-create-widget-node-1.png) ![Create a new widget node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/756e7498-ffde-4d42-9250-70cb9d611607/5-create-widget-node-2.png)
3.  Drag from the **Create Widget** node's execute pin and create an **Add to Viewport** node.
    
    ![Create a new Add to Viewport node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c4c71e3-72bc-4791-9f51-c45b19cc1cbf/6-add-to-viewport.png)
4.  Drag from the **Add to Viewport** node's execute pin and create a **Set Input Mode UI Only** node.
    
    ![Create a Set Input Mode UI Only node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/907e1d57-d129-4396-ba8e-9d6e306a6d34/7-set-input-mode-ui-only.png)
    
    This node tells your Widget the only game element that responds to player input is the UI. Any other input from the user will not translate to gameplay actions, even if an action is bound to that control.
    
5.  Right-click in a free area of the **Blueprint Editor** and create a **Get Player Controller** node.
    
    ![Create a Get Player Controller node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14da65bf-179c-4c2e-8933-716c052b8c8c/8-create-get-player-controller-node.png)
6.  Connect the **Return Value** pin of the **Construct Widget** node you created in step 2 to the following pins:
    
    -   **Target** on the **Add to Viewport** node.
    -   **In Widget to Focus** on the **Set Input Mode UI Only** node.
7.  Connect the **Return Value** pin of the **Get Player Controller** node you created in step 5 to the **Player Controller** pin on the **Set Input Mode UI Only** node.
    
    At this stage, your Level Blueprint should look like the image below.
    
    ![Partial Level Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e9a412b-74e1-42b3-8043-5d345cd1bf3f/9-partial-level-blueprint.png)
8.  Drag from the **Return Value** pin of the **Get Player Controller** node and create a **Set Show Mouse Cursor** node. Enable the **Show Mouse Cursor** checkbox for this node.
    
9.  Connect the **Set Input Mode UI Only** node output pin to the **Set Show Mouse Cursor** node input pin.
    
    ![Connect the Set Show Mouse Cursor node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b9db6d8-693f-4bda-815c-6779dd9b99b0/10-set-show-mouse-cursor-node.png)
10.  Set the **Class** value of the **Create Widget** node to the **MyWidget** widget you created in the previous section.
    
    ![Set widget class to MyWidget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e38720a-7c81-4a8c-aa09-3116bfb22c8d/11-set-widget-class.png)
11.  **Compile** and **Save** your Blueprint.
    

Your finished Level Blueprint should look like this:

Click the image for full size.

You can now close the Level Blueprint.

## Add Text to Speech Strings

Next, create a channel for each button to "speak" on, and enter the text strings that will be vocalized.

1.  Return to the **Widget Editor** for your widget. If you closed it, double-click the **MyWidget** widget in the **Content Browser** to open it again.
    
2.  Click one of the buttons you created. Then, in the **Details** panel on the right, scroll down to **Events** and click **(+) plus** to add a new **On Clicked** event.
    
    ![Add OnClicked event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aee0e96f-d1d3-4fbb-8d8f-cbb9fe297b25/13-add-on-clicked-event.png)
    
    This action will open the Widget's **Graph** and create a new **On Clicked** node for this button.
    
3.  Right-click in the graph and create a new **Get TextToSpeechEngineSubsystem** node.
    
    ![Create a Get Text To Speech Engine Subsystem node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/faed9bdb-bc5a-4040-b4b5-23b9afc1a580/14-create-get-tts-subsystem-node.png)
    
    If you can't see this node, make sure that the **Text To Speech** plugin is enabled for your project.
    
4.  Drag from the **Text to Speech Engine Subsystem** node and create a new **Add Default Channel** node. Connect the **On Clicked** event to the **Add Default Channel** node **input** pin.
    
    ![Create an Add Default Channel node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/242e86d9-c772-492f-80ab-cafe45ff2c5c/15-create-add-default-channel-node.png)
5.  In the **Add Default Channel** node, right-click the **New Channel ID** property and select **Promote to Variable** from the context menu.
    
    ![Promote the New Channel ID property to a variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/078a00b0-14e4-4757-b452-47cc17fcc48c/16-promote-to-variable.png)
6.  In the **Details** panel on the right, using the **Variable Name** property, name the variable **Channel One**.
    
    ![Rename the variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ffd2182-1873-43b0-9305-ae8f3bd25bc3/17-rename-variable.png)
7.  Drag again from the **Text to Speech Engine Subsystem** node and create a new **Activate Channel** node. Connect the **Add Default Channel** node output pin to the **Activate Channel** node input pin.
    
    ![Create an Activate Channel node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ca75948-e1f4-4b07-a231-efa30f4ff876/18-create-activate-channel-node.png)
8.  Connect the **Channel One** variable you created in step 4 to the **Channel ID** pin on the **Activate Channel** node.
    
    At this stage, your Blueprint should look like this:
    
    Click the image for full size.
    
9.  Drag again from the **Text to Speech Engine Subsystem** node and create a new **Speak on Channel** node. Connect the **Activate Channel** node output pin to the **Speak on Channel** node input pin.
    
    ![Create a Speak on Channel node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79d4ccfb-6d66-4d03-9094-1ae658c6bc7a/20-create-speak-on-channel-node.png)
10.  Connect the **Channel One** variable you created in step 4 to the **Channel ID** pin on the **Activate Channel** node.
    
11.  Drag from the **String to Speak** pin on the **Speak on Channel** node and create a new **To String (Text)** node.
    
    ![Create a String to Speak node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5349893-0e4b-44e7-9dbc-c0f4b10778d5/21-string-to-speak.png)
12.  Drag from the input pin of the **to String (Text)** node you created in the previous step and create a new **Format Text** node.
    
    ![Create a Format Text node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c7bd57f-01f2-444a-9952-94022b4fc6ef/22-format-text-node.png)
13.  In the **Format** box of the **Format Text** node, enter the text you want to be spoken.
    
    ![Enter the string to be spoken](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6b8ae78-89af-4a9f-9b0d-bbfeb54535c8/23-enter-string-to-speak.png)
14.  Repeat steps 1-12 above for the second button you created, changing Channel One to Channel Two where appropriate.
    
    You can click and drag to select multiple Blueprint nodes, then copy and paste them. This reduces the need for manual step duplication.
    
15.  **Compile** and **Save** the Blueprint.
    

Your finished Widget Blueprint should now look like this:

Click the image for full size.

## Test your Widget

Now, it's time to test your widget.

In the **Level Viewport**, on the **Main toolbar**, click the **Play** button to enter **Play in Editor** mode.

![Play button on the Main Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2727ed0a-eca4-4ed6-ae7e-557b98d49395/25-play-in-editor.png)

You should now see your widget drawn inside the viewport. Click a button to hear its string vocalized.

![Completed widget in the Level Viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e9c6093-ec0c-4d3c-8293-e09ed8989ed3/26-finished-widget.png)
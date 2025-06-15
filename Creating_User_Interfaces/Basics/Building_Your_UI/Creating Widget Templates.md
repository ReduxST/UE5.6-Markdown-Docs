# Creating Widget Templates

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-umg-widget-templates-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-umg-widget-templates-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:51

---

Every **Widget Blueprint** that you create with UMG is considered a **User Widget** that can be reused and placed within other Widget Blueprints. Both visual and scripted functionality will be carried over into the Blueprint.

With some Blueprint Scripting, you can create variables for how your UI widget functions or looks that can be overwritten on a per-instance basis. In this How-to, we will create and stylize a Button and set it up in such a way that we can override the style when we place it in other Widget Blueprints. Lastly, we will customize what happens when the Button is clicked on a per-instance basis. This is useful if you have a series of Buttons in a menu that you want to look and act the same but produce different results when pressed.

## 1 - Setting Up the Button Widget

First, we need to create a Button and set up the script for what happens when we click the Button.

For this how-to, we are using the **Blueprint Third Person Template** with **Starter Content** enabled.

1.  Click the **Add** in the **Content Browser**, then select **User Interface > Widget Blueprint**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68589b82-5a71-4198-9c5f-27b27a711bbe/01_newwidgetblueprint.png)
    
    You can also add a Widget Blueprint by right-clicking into **Content Browser**, then **User Interface > Widget Blueprint**.
    
2.  You should create two **Widget Blueprints** with names **CustomButton** and **HUD**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77a06ca2-9ba3-406f-9caf-159d1caae289/02_widgetsyouneed.png)
    
    The **CustomButton** is the User Widget that we will add into the **HUD** Widget Blueprint.
    
3.  Add a **Button** by dragging from the **Palette** panel into **Hirerchy** panel. Right-click **Button** you added and select **Wrap With > Size Box**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc4b7855-5d4f-4ed7-b886-9ba40f7264d1/03_wrapwithsetbutton.png)
4.  In the **Size Box** **Details** panel, change the **Width Override** to **300** and **Height Override** to **100**. You can also change the graph layout to **Desired on Screen** to get an idea of the actual size of the button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46698ab4-62d0-432b-aecd-48ddae3bbb61/04_sizeboxdetails.png)
5.  In the Event Graph, hold **Ctrl** and drag the **Button** from the **My Blueprint** panel. Then, drag off the pin and add a **Set Style** node. Make sure to select the **Variable Apperance** node and not the Button Function node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a54e0a2e-9007-4036-ac34-5a9e727191a6/05_addsetstylenode.png)
6.  Connect the **Event Construct** node to the **Set Widget Style** node, and then Right-click on **Widget Style** and select **Promote to Variable**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d65bd383-1090-451b-9677-77a983e66573/06_setstylepromtovar.png)
7.  Name the new variable **ButtonStyle** and then **Compile** the Blueprint. Then, set the **Normal > Image** style to any texture.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa25a854-7b13-4d3a-9b11-a1ee17295359/07_vardetailpanel.png)
8.  Right-click on the **Normal** section and select **Copy**. Then, paste the image settings to the **Hovered** and **Pressed** values. All three of these values should now have the same image texture.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1d636dc-2b39-45c3-92b3-baf128e0923f/08_copybuttonstyle.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eac81e6b-4e65-4b48-97c2-3a9a1cbc0c0b/09_setbuttonstyle.png)
    
9.  Expand **Hovered** and change the **Tint** color to any color (such as yellow).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f361dfce-c2a0-4559-9491-ec3a1c43cde2/10_sethovered.png)
10.  In the **ButtonStyle**, check **Instance Editable** and **Expose on Spawn**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5ef7462-94c6-4132-8e15-d48bbb5464c0/11_buttonstylevardetails.png)
    
    This enables us to modify the values of this variable from other Widget Blueprints when we use this Widget Blueprint elsewhere.
    
11.  Select the **Button** variable, and click the **+** sign to add an **OnClicked** node to the graph.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87997bb4-bd1f-4180-95ba-25b17b719210/12_addonclickevent.png)
12.  In the **MyBlueprint** panel, select **\+ Event Dispatcher** to create a new **Event Dispatcher** and call it **ButtonClicked**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/929ca94a-d2b9-48a3-bf1e-bcb0d0d962ff/13_addeventdispatchers.png)
13.  Drag the **ButtonClicked** event into the graph, select **Call**, and connect the node to the **OnClicked** event.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb80463a-ff19-44a2-81c7-145a61a58e2d/14_onclickbuttonscript.png)
    
    This creates a unique script functionality when we click the button. If we had multiple instances of this button and only used the **OnClicked** event, each instance would respond and execute the same functionality. However, by creating an **Event Dispatcher**, we can implement events on a per-instance basis and have only the button that was actually clicked on fire off an additional script.
    

## 2 - Adding the Button Widget to the HUD Widget

With our Button widget created and scripted, we can now add the Button to the HUD Widget, add the HUD to the viewport, and see the buttons in-game.

1.  Open the **HUD** Widget Blueprint, and add a **Vertical Box** to the **Canvas Panel**. Resize the box to a smaller size.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34d3f217-1732-4d82-864e-57306811416f/15_addvertboxtocanpan.png)
2.  From the **Palette** under **User Created**, add three **Custom Buttons** to the **Vertical Box**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecdea01a-3146-4cf9-9f2a-f67d93a83268/16_vertboxhierarchy.png)
3.  In the Event Graph, select each **CustomButton** and click **+** to add the **Button Clicked** event to the graph. You should have three events, one for each button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/242181ec-8cdc-4c63-a52c-d78ac7552cd6/17_addbuttonclickedevent.png)
    
    This is the **Event Dispatcher** that we created inside our **CustomButton** Widget Blueprint and will respond whenever this particular button is clicked.
    
4.  For each **ButtonClicked** event, drag off the pins and connect **Print String** nodes up to each event. Add different text to the **In String** text boxes.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c22c06ee-6f41-488b-a373-f87b213035b0/18_addprintstringscript.png)
    
    In this example, we are printing different text to the screen depending on which button we click. In a real-world example, you can have each button open up a different menu, change different game settings, or make modifications to a player character.
    
5.  From the Level Editor Main Toolbar, go to **Blueprints** and select **Open Level Blueprint**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6738e3ed-beca-4aa9-9099-5415b613d56d/19_openlevelbp.png)
6.  Right-click in the Event Graph and add an **Event BeginPlay** node. Connect the node to a **Create Widget** node with the **Class** set to **HUD**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87d1f3c5-1e5a-4a75-a52c-ecfb87a63b60/20_createhudwidget.png)
7.  Add an **Add to Viewport** node and connect it to the **Create HUD Widget** node. Then, add a **Get Player Controller** function to a **Set Show Mouse Cursor** node and check the box (set it to True).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00a8ca7d-b7cf-498f-bba7-c0d83cd1e307/21_eventbeginplayscript.png)
8.  **Compile**, **Save**, close the **Level Blueprint**, and click **Play** in the editor to interact with your button in-game.
    

## End Result

When playing in the editor, each Button is automatically styled based on the defined **ButtonStyle** variable, and they execute a different portion of the script as the **Event Dispatcher** is called and the corresponding **ButtonClicked** Event is called. Since our **ButtonStyle** variable is exposed and editable on spawn, we can override the style of the button in whatever Widget Blueprint we place it in. This is useful if you have some kind of animation or other complex scripted logic that you don't want to re-create in each Blueprint. By creating your button as a User Widget, you can reuse it in any other Widget Blueprints without additional work.
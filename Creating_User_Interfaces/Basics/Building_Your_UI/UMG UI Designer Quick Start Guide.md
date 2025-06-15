# UMG UI Designer Quick Start Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-ui-designer-quick-start-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-ui-designer-quick-start-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:55:37

---

This **Quick Start Guide** shows you how to implement some basic in-game HUD elements using **Unreal Motion Graphics UI Designer (UMG)**. Get familiar with example of the process of creating dynamic elements: health bar, energy bar, and counter of ammo. Also learn how to add them to the **Viewport**.

All actions are described step by step and in detail. However, if you have never worked with **Unreal Engine**, then it is recommended that you first familiarize yourself with the [Level Designer Quick Start](/documentation/en-us/unreal-engine/level-designer-quick-start-in-unreal-engine). Here you will find basic knowledge and terminology for working with UE. Also, this course contains links to more detailed information. Check them out if necessary.

## 1 - Required Project Setup

For this tutorial, use the **Blueprint First Person** template with **Starter Content** enabled.

Character appears unarmed at the start of game process. Ammo indication should appear in case Character take a weapon. For this reason, use two Widgets: HUD and HUD\_AmmoCount. You should adjust HUD Widget to display health and energy of the Character from the start of game process, and HUD\_AmmoCount Widget to display ammo in case taking a weapon.

1.  Create **Widget Blueprint**. Click the **Add New** in the **Content Browser**, then select **User Interface > Widget Blueprint**. Name this widget **HUD**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf146350-4103-4b5a-a33d-23b00ca8bc63/01-01_createwidgetblueprint.png)
    
    Use a Widget Blueprint to create and set up UI elements (HUD, Menus, and so on). With the help of this, you can visually layout UI elements and provide scripted functionality for it.
    
    For more information on Widget Blueprints see [Widget Blueprints in UMG](/documentation/en-us/unreal-engine/level-designer-quick-start-in-unreal-engine).
    
2.  Create three more Widget Blueprints, name it **HUD\_AmmoCount**, **MainMenu**, **PauseMenu**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9537bf4e-5ee1-4eeb-8920-5a1119850e26/01-02_widgetsyouneed.png)
3.  Create new **Level**. **Right-click** in the **Content Browser** select **Level**. Name it **Main**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58d81da3-cc2d-4ab3-976e-4cd105ea5f0b/01-03_createlevel.png)
    
    You will use this later in the guide for Main Menu setup.
    

### Adjusting BP\_FirstPersonCharacter Blueprint

1.  In the **Content Browser**, open the **BP\_FirstPersonCharacter** Blueprint located under the **Content/FirstPerson/Blueprints** folder.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50a46169-556d-4f62-83a7-f52d4b629a68/01-11_firstperbp.png)
    
    This is the **Character Blueprint** you control in the game. You should adjust it to construct HUD Widget and display it in a viewport.
    
2.  In the **Blueprint Editor** window, click the **Add Variable** Button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aeb46af8-7b5b-4542-b2dc-45f8483c9348/01-12_addvariable.png)
3.  In the **Details** panel of this variable, select a **Float** variable type and input the name **Health**. Set the **Default Value** to **1.0**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd1c2922-0651-437f-bda8-7e3de143a301/01-13_healthdetail.png)
    
    You will use this variable for adjusting Health Bar of the character in the the HUD Widget.
    
4.  Create another variable with **Float** type and name it **Energy**. Set the **Default Value** to **1.0**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/225a6f17-f193-415b-913b-12c30c437aba/01-14_energydetail.png)
    
    You will use this variable for adjusting Energy Bar of the character in the the HUD Widget.
    
    You should compile Blueprint by clicking the **Compile** button from the Tool Bar before input a Default Value.
    
5.  Create another variable with **Integer** type and name it **Ammo**. Set the **Default Value** to **25**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b75d4f52-e976-48ed-afb1-cf9a764e41d6/01-15_ammodetail.png)
6.  Create one more variable with **Integer** type and name it **MaxAmmo**. Set the **Default Value** to **25**.
    
7.  **Right-click** inside the **Graph** window, add the **Event Begin Play** node, then add a **Create Widget** node. Set the **Class** to **HUD** Widget.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aff4595d-c2d0-4d43-a13c-d4093da8339b/01-16_createhudwidget.png)
8.  For the **Return Value** of the **Create HUD Widget**, select **Promote to Variable** and name it **HUD Reference**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/718d2be1-244d-4399-aae0-628b5389823c/01-17_hudtovar.png)
    
    With the help of this, you create HUD Widget, when the game is started, and set it as a variable for later calls. This is usefull in case you need call some functions or set properties of the HUD Widget via Blueprint. For example, if you need hide the HUD, while the game is paused, you can access the HUD through this variable.
    
9.  Add the **Add to Viewport** node to the out pin of the **Set** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79856c5e-fe2e-4653-9092-081396b85652/01-18_beginplay.png)
    
    With the help of this, you've added the HUD Widget to the viewport from start of game process.
    
10.  **Compile** and **Save** the **BP\_FirstPersonCharacter** Blueprint and close it.
    

### Adjusting BP\_Rifle Blueprint

The process of adjusting BP\_Rifle Blueprint is similar to adjusting BP\_FirstPersonCharacter Blueprint. In case you need more detail see section above [Adjusting BP\_FirstPersonCharacter Blueprint](/documentation/en-us/unreal-engine/umg-ui-designer-quick-start-guide-in-unreal-engine#adjustingbp_firstpersoncharacterblueprint).

1.  In the **Content Browser**, open the **BP\_Rifle** Blueprint located under the **Content/FirstPerson/Blueprints** folder.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62c63e6d-a68b-4e71-9be3-8a9b44f04653/01-21_riflebp.png)
2.  Find the **On Component Begin Overlap (SphereCollision)** node. **Right-click** on the execution pin and select **Break All Pin Link(s)**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77effd7c-f29a-4f23-b5f7-47815ac1474a/01-22_breakalllinks1.png)
3.  Drag the execution pin of the **On Component Begin Overlap (SphereCollision)** node and add a **Create Widget** node. Set the **Class** to **HUD\_AmmoCount** Widget.
    
4.  For the **Return Value** of the **Create HUD Widget**, select **Promote to Variable** and name it **HUD Ammo Count Ref**.
    
5.  Add the **Add to Viewport** node to the out pin of the **Set** node.
    
6.  Connect the execution pin of the **Add to Viewport** node with the execution pin of the **Cast to BP\_FirstPersonCharacter** node. Your script should look as following.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d79f611-a98b-4a3e-aabd-bbab86fd894d/01-23_oncompevent.png)
    
    With the help of this, you've added the HUD\_AmmoCount Widget to the viewport in case Character take a weapon.
    
7.  **Compile** and **Save** the **BP\_Rifle** Blueprint and close it.
    

### Adjusting Character Variables in BP\_FirstPersonCharacter Blueprint

In this chapter you can find information about the adjusting declaired variables and adding them to the Blueprint.

1.  In the Blueprint Editor of the **BP\_FirstPersonCharacter**, hold **Alt** and drag the **Energy** variable into **Graph** window and place it next to the Jump script.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c310fda-d908-4951-9d04-87c887fa7bca/01-31_dragenergy.png)
2.  Hold **Ctrl** and drag a copy of the **Energy** variable into **Graph** window. Add **Substruct** operator node, connect and set to **0.25** as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02f609d8-f57a-4fdd-a55d-fb0eb463da0a/01-32_jump.png)
    
    With the help of this script, every time the Character jumps, the Energy is reduced by 0.25 from current Energy value.
    
3.  Set up the same script for the **Health** variable but use an **F** Key Event (or any other key press event) for testing.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b1449ee-87b7-4ae0-bd84-b110f0b21ccd/01-33_testhealth.png)
    
    With the help of this script, you will be able to test if Health is reduced by 0.25 from current value, every time you press **F**.
    
4.  **Compile** and **Save** the **BP\_FirstPersonCharacter** Blueprint and close it.
    
    To add the ability to reload ammo do the following. Add the **R Key Event**. Hold **Alt** and drag the **Ammo** variable. Hold **Ctrl** and drag the **Max Ammo** variable. Connect it as shown in the image below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46b4b10b-c3d6-402e-9926-0beecb2d8e25/01-46_reloadammo.png)

### Adjusting Character Variables in BP\_Rifle Blueprint

1.  Open **BP\_Rifle** Blueprint. Find the **OnFireProjectile Custom Event**. **Right-click** on the execution pin and select **Break All Pin Link(s)**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f9cf86b-18fc-4a5e-abe7-4154a4306aa4/01-41_breakalllinks2.png)
2.  Near this node, **Right-click** and add a **Branch** node.
    
3.  Hold **Ctrl** and drag a copy of the **FirstPersonCharacterReference** variable into **Graph** window. Drag the pin and select **Get Ammo**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27bf853d-2c33-4099-b006-373363bddf05/01-42_addammo.png)
4.  Add **Greater** operator node, set to **0** and connect as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e362077-5d37-4966-a9be-235adf72f872/01-43_onfirecondit.png)
    
    Character you play can fire if their ammo is greater than zero, due to this script.
    
5.  At the end of the **OnFireProjectile Custom Event** script following the **Montage Play** node, hold **Ctrl** and drag a copy of the **FirstPersonCharacterReference** variable into **Graph** window. Drag the pin and select **Get Ammo**. Drag the pin again and select **Set Ammo**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/326756d6-1b08-417b-ad7b-fe3e3d15e323/01-44_setammo.png)
6.  Add **Substruct** operator and set **Ammo** to equal **Ammo - 1**. Your script should look as following.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbe5fe3c-b301-4bae-a5a5-1f8f8642cdcd/01-45_ammocountscript.png)
    
    Every time Character you play fires it decreases ammo by one, due to this script.
    
7.  **Compile** and **Save** the **BP\_Rifle** Blueprint and close it.
    

## 2 - Displaying Health, Energy & Ammo

At this step you should set up the visualization of Health, Energy and Ammo variables in the Widgets and adjust connection with game process.

### Visual: Health and Energy

To set up the visualization of HUD Widget do the following.

1.  Open **HUD** Widget Blueprint to access the **Widget Blueprint Editor**. With the help of this, you can create the visual layout and scripted functionality of HUD Widget.
    
    For more information on the different facets of the Widget Blueprint Editor, see [Widget Blueprints in UMG](/documentation/en-us/unreal-engine/widget-blueprints-in-umg-for-unreal-engine).
    
2.  Find the **Horizontal Box** in the **Palette** panel under **Panel** and drag it onto the **Canvas Panel** in the **Hierarchy** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e12ed45-1181-4d6e-b4f5-ebea7b1f6938/02-02_horboxwidget1.png)
    
    **Panel** Widgets are like containers for other widgets. You can provide additional functionality for the widgets that are inside it.
    
3.  Also under **Panel**, drag two **Vertical Boxes** onto the **Horizontal Box**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d346b0d-9a15-460b-9cda-64d960630067/02-03_widgetstructure1.png)
4.  Under **Common**, drag two **Text** widgets onto the first Vertical Box and two **Progress Bars** onto the second Vertical Box.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3885089-2e23-4ba4-b1ac-7dd39d9a402e/02-04_widgetstructure2.png)
5.  Select the **Horizontal Box**, find it in the **Graph**, resize the box and place it in the upper left corner of the window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdfb8410-1eaa-49e0-a8ad-1266c4dc6ade/02-05_widgetlocation.png)
6.  Select both **Progress Bars**, then in the **Details** panel set both to **Fill** under **Size**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf9970fb-b691-4e9f-a815-6f7df22841af/02-06_progbardetails.png)
7.  Select the **Vertical Box** containing the Progress Bars, then in the **Details** panel set both to **Fill** under **Size** as well.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/22acc9a7-fb20-4464-a94c-6c1779b3f813/02-07_vertboxdetails.png)
8.  Select the **Horizontal Box** again and resize it so the bars line up with the text.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8e20dd2-d696-4463-ace7-3989d2c3a5d2/02-08_horboxwidget2.png)
9.  Select the top-most **Text** widget in the **Hierarchy** panel, then in the **Details** panel under **Content** enter **Health:**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a13e4c1b-ec2f-4c00-a9d7-6dbffa039db5/02-09_texthealth.png)
10.  Do the same for the other **Text** widget, but enter **Energy:**. It should look as following.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b053d9e-8528-4145-be9c-c97c8947ae00/02-10_healthenergybar.png)
    
    By default, UMG text widgets use a font from Unreal Engine. It allows you get started work in Unreal Engine quickly. However, this built-in font has some limitations. For example, it only supports a small set of languages. In most cases, it is necessary import custom fonts into Assets. For more details about setting up text widgets to use custom fonts see [Creating and Assigning Fonts in Unreal Engine User Interface](/documentation/en-us/unreal-engine/creating-and-assigning-fonts-in-unreal-engine-user-interface).
    
11.  Select the **Progress Bar** next to **Health**, then in the **Details** panel set the **Fill Color and Opacity** to green color.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/289c2fcf-f766-443b-a016-4ccf3fb96c51/02-11_healthcolor.png)
    
    Progress Bar does not change color when assigning a color. This is because the **Percent** value to fill the bar is set to 0.0. You can change this to test out different colors. Later you will link this to the Health variable value of the Character.
    
12.  Also set a Fill Color and Opacity for the **Energy** bar (For example, an orange color).
    
13.  Your HUD Widget layout should look as following.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccc3bc02-5fd5-433d-b5a9-3fb4eae719e2/02-12_hudlayout.png)
14.  **Compile** and **Save** the **HUD** Widget Blueprint and close it.
    

### Visual: Ammo

To set up the visualization of HUD\_AmmoCount Widget do the following.

1.  Open **HUD\_AmmoCount** Widget Blueprint to access the **Widget Blueprint Editor**.
    
2.  Use the same way to add widgets to the **Hierarchy** panel. Your structure of layout should look as following.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2f47f98-b377-41ef-af49-af6a6ee19112/02-13_widgetstructure3.png)
3.  Select the **Horizontal Box** in the **Graph**, resize the box and place it in the upper right corner of the window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c4b61d4-28f9-47e3-8bf7-e139d36458f1/02-14_widgetammolocation.png)
4.  Select the **Horizontal Box**, then in the **Details** panel click **Anchors** and select the upper-right Anchor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48d16b02-717f-476f-a54c-b9d8f5d7418d/02-15_widgetammoanchors.png)
    
    With the help of this, you place the **Anchor Medallion** to the upper right corner of your screen.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ef9bd93-935e-442e-a2d5-9d5f2f5ee137/02-16_hudammofinal.png)
    
    You fix the Horizontal Box position regardless of screen size, due to the Anchors settings. The Widget stays the same distance from the Anchor Medallion when the screen is resized.
    
    You can test different screen sizes by clicking and changing the **Preview Size** option inside the graph.
    
5.  **Compile** and **Save** the **HUD\_AmmoCount** Widget Blueprint and close it.
    

### Script: Health and Energy

The next step is provide functionality for the **HUD** Widget elements.

1.  Open **HUD** Widget Blueprint to access the **Widget Blueprint Editor**.
    
2.  Click the **Graph** button in the upper right corner of the Widget Blueprint Editor window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3efed24-4e3b-4c20-94a6-b54cdfe69653/02-17_grapheditingmode.png)
3.  In the **Graph** under the **Event Construct** node, **Right-click** and add **Get Player Character** node.
    
4.  Drag the **Return Value** pin of **Get Player Character** node and select **Cast to BP\_FirstPersonCharacter**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fab50649-7d71-40eb-86e5-a14a9bfdd2a9/02-18_casttohud.png)
5.  Drag the **As BP First Person Character** pin and select **Promote to Variable** (name it **My Character**), then connect as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d61baa9-c96f-48d3-87f7-816192419e0b/02-19_eventconstruct.png)
    
    With the help of this, you will be able to access the variables from **BP\_FirstPersonCharacter** Blueprint.
    
6.  Click **Compile** in the toolbar to compile the script.
    
7.  Return to the **Designer** and select the **Progress Bar** next to **Health**.
    
8.  In the **Details** panel under **Progress**, click the **Bind** option next to **Percent** and click **Create Binding**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63191eef-1abc-4830-9348-b8353a4ee070/02-20_createbinding.png)
    
    With the help of this, you can create custom bindings by adjusting function script in opened window.
    
9.  Hold **Ctrl** and drag the copy of **MyCharacter** variable into the **Graph**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f65afc3d-b0b0-4e02-852d-7f40537302c3/02-21_dragmycharacter.png)
10.  Drag the pin **MyCharacter** and select **Get Health**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e54cf30-1fc8-4263-9be1-a31147b66fdb/02-22_gethealth.png)
11.  Connect the **Health** pin to the **Return Value** of the **Return Node**. It should look as following.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ba289a3-0be9-427d-b3a3-67e345192e17/02-23_healthscript.png)
12.  Do the same procedure to adjust **Progress Bar** next to **Energy**. It should look as following.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69847c9c-034c-4be9-a58f-40c61bf9fbf8/02-24_energyscript.png)
13.  **Compile** and **Save** the **HUD** Widget Blueprint and close it.
    

### Script: Ammo and AmmoMax

Procedure of setting up Ammo variable is similar to setting Health and Energy variables. For more detailed information see section above [Script: Health and Energy](/documentation/en-us/unreal-engine/umg-ui-designer-quick-start-guide-in-unreal-engine#script:healthandenergy).

1.  Open **HUD\_AmmoCount** Widget Blueprint and go to **Graph** tab.
    
2.  Create script for connection **HUD\_AmmoCount** Widget Blueprint to **BP\_FirstPersonCharacter** Blueprint as described before. This should look as following.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/363ac821-8296-448b-976c-321e12162b18/02-19_eventconstruct.png)
3.  Click **Compile** in the toolbar to compile the script.
    
4.  Return to the **Designer** and select the **25** text following the **Ammo** text. In the **Details** panel for **Text**, click **Bind** and **Create Binding**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f686a87a-fb6a-4f9e-80b1-c82b697b1d23/02-25_createbindingtext.png)
5.  In opened window, hold **Ctrl** and drag the copy of **MyCharacter** variable into the **Graph**. Drag the pin **MyCharacter** and select **Get Ammo**. Connect the **Ammo** pin to the **Return Value** of the **Return Node**. It should look as following.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5cedbf0-bcad-4815-8d20-ac86c19829de/02-26_ammoscript.png)
    
    A conversion node **To Text** will be created automatically after connecting **Ammo** node to the **Returned Node**.
    
6.  Repeat the process above for other **25** text and creating a binding for the "AmmoMax" text.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4852c529-5daf-4b87-8b06-1cba3fd3065a/02-27_ammomaxscript.png)
    
    It is not necessary to do this if your max ammo is constant. However, with the help of this **AmmoMax** variable setting, you will be able to change it by creating a script in **BP\_FirstPersonCharacter**.
    
7.  Click **Compile** and **Save**, then click the **Play** button to play in the Editor.
    

With the help of this quide, you have adjusted displaying Health and Energy Bars via HUD Widget, and displaying Ammo via HUD\_AmmoCount Widget. All these Widgets display current values from your Character Blueprint. In game process, the pressing **Space** cause the jump Character, reducing Energy; pressing **F** cause the reducing of the Health; the pressing **Left Mouse Button** cause fire the weapon, reducing Ammo.

In the next section, you will find the information on creating a Main Menu, which you can use to load into game you set up. Also, there is additional information on working with **Unreal Motion Graphics** and **Blueprints**.

## 3 - Further Reading

Further reading related to the topics in this guide:

-   For more information on Unreal Motion Graphics, see: [UMG UI Designer](/documentation/en-us/unreal-engine/umg-editor-reference-for-unreal-engine).
-   For more information on Blueprints, see: [Blueprints Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine).
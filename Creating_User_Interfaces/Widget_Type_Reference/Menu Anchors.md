# Menu Anchors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-menu-anchors-in-umg-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-menu-anchors-in-umg-for-unreal-engine)  
**Processed:** 2025-06-14 16:59:57

---

**Menu Anchor** is a widget you can add to the UI layout. With the help of **Menu Anchor**, you can adjust location of the pop-up menus on the screen.

This page gives basic information about using and adjustment the Anchor Menu Widget in the UI layout. Also, get familiar with example of using and adjustment the Anchor Menu Widget below using **Unreal Motion Graphics UI Designer (UMG)**.

## Menu Anchor Properties

### Details Panel Options

In the **Details** panel for a placed **Menu Anchor**, there are a couple of specific options that can be set that pertain to the Widget:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92ba482c-8f9c-41bf-a145-34417ad9ddd5/detailspanel.png)

| Option | Description |
| --- | --- |
| **Menu Class** | The Widget Blueprint (pop-up) to spawn when the menu is called. Creates the widget freshly each time. |
| **Placement** | Several placement options use to determine the location of the created widget. |
| **Fit in Window** | If sets true, the Menu Anchor attempt to fit the menu inside the window. |
| **Should Defer Painting After Window** | Sets ability to defer painting after window content. |
| **Use Aplication Menu Stack** | If sets false, you can control the menu's lifetime yourself. |
| **OnGetMenuContent** | Allows for the customization of the pop-up by binding a function or property to the **OnGetMenuContent** Event which is called when the pop-up is summoned (see below). |
| **OnGetUserMenuContent** | Allows for the customization of the pop-up by binding a function or property to the **OnGetUserMenuContent** Event which is called when the menu content is requested. |
| **OnMenuOpenChanged** | Allows for the customization of the pop-up by binding a function or property to the **OnMenuOpenChanged** Event which is called when the opened state of the menu changes. |

For the **OnGetMenuContent** Event and **OnGetUserMenuContent** Event, you can create and bind a function directly from the **Details** panel which will be called whenever the Menu Anchor is called. This allows you to provide extra functionality to the creation of your pop-up menu. For example, below we've run a check to determine if the player is "In Battle" and if not, we allow them to access the pop-up menu. If they are we do not allow them to access the pop-up menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0fa35d9-32df-4156-a854-cc989736075e/examplegetmenu.png)

### Blueprint Functions

The Menu Anchor widget has some widget specific functions that can be called through script which are described below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20580a41-3b18-46e8-96df-d8a31d255eca/menuanchornodes.png)

| Option | Description |
| --- | --- |
| **Close** | Closes the menu if it is currently open. |
| **Fit in Window** | Sets the fitting of the Anchor Menu in window. |
| **Get Menu Position** | Returns the menu's position in world space. |
| **Has Open Sub Menus** | Returns wether the menu has open sub menus or not. |
| **Is Open** | Checks to see if the Target Menu Anchor is currently open and returns a Boolean. |
| **Open** | Opens the menu if it is currently closed. |
| **Set Placement** | Sets placement options use to determine the location of the created widget. |
| **Should Open Due to Click** | Returns wether the menu should be openable by clicking or not. |
| **Toggle Open** | This toggles the open state for the menu and can be used instead of opening/closing. |

## Usage Example

Say you wanted to create an Inventory Menu and have a pop-up appear when the player clicks on a item, as seen in the example below.

The first thing you would want to do is create what your pop-up menu looks like.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76e12664-dbb7-4a3a-9876-2854b420c96d/popupdesigner.png)

Above we created a simple **Widget Blueprint** called **MenuPopUp** that is comprised of three Buttons inside a Vertical Box.

Next you would need to create another Widget Blueprint for your Inventory Menu, which we called **HUD** below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e1905aa-3ac6-4d6d-b8d2-9bd15c4164eb/makeinventorymenu.png)

After you have created your Inventory Menu, you would also add the **Menu Anchor** Widget (located under **Primitive**).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68d30cf4-5004-4369-83ea-6bead2b2be08/addmenuanchor.png)

You would then position the Menu Anchor where you want it to appear, we positioned and Anchored it to the right/center position.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17b6f863-338f-4240-8548-12a9f7c9ddbd/placedanchor.png)

In the **Details** panel for the Menu Anchor, you would set the **Menu Class** (or Widget Blueprint to spawn) as well as its placement options.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff680c7c-a8a1-4c46-a7ec-b76b7de42487/menuanchordetails.png)

On the Graph tab, you would add **OnClick** Events for each of your Buttons and drag in the Menu Anchor widget.

Dragging off the Menu Anchor, you can call the **Open** function to open and display your specified Menu Class.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb859908-f768-44ac-8756-1c61d4988d36/hud_graph.png)

Check the **Focus Menu** option on the **Open** node to apply focus to the Menu Anchor Widget. In this case, the Menu Anchor Widget automatically closes when focus leaves the menu (which happens when you click anywhere else). This is a way of making the menu close when the user interacts with other areas of the screen.

After you have created the Inventory Menu, you would need to call that menu in-game somehow.

This could be through the **Level Blueprint** or (in our case) through the Default Pawn Class (which is set to use the **MyCharacter** Blueprint).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76d0a6aa-3561-426d-a681-50bcbf78e40f/displayinginventorymenu.png)

Above in our **MyCharacter** Blueprint, when the game is started we create the HUD Widget and store it as a variable called **HUDWidget** so we can access it later. We then set **I** to toggle between **Add to Viewport** and **Remove from Parent** to Display or Remove the Inventory Menu. We also set **Show Mouse Cursor** to enabled or disabled based on whether or not the Inventory Menu is open or not.

And finally inside the **MenuPopUp** Blueprint (your pop-up menu), adding some script to **Close** the Menu Anchor when the player presses a Button in the pop-up menu. Below when the pop-up is constructed, we get a reference to the **MyCharacter** Blueprint by **Casting** to it then promoting it to a variable called **MyCharacterReference**. With this reference we can then access the HUD

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/943a0a7a-2e7a-40b4-a163-79c90cc4d262/popupmenunetwork.png)

You would probably want to add some functionality for each of the buttons for your pop-up (instead of printing to the screen) that when pressed, does something. For example, perhaps the first button "uses" the item from the Inventory, while the second "drops" the item and the third "cancels" and returns the player to the Inventory Menu.

This is just one example, you could also change what causes the Menu Anchor to open. Instead of a button press, perhaps using the **IsHovered** function to determine if an object is being hovered over then opening the Menu Anchor and pop-up window to display a tool-tip or some other form of notification. In either case, this should get you started with using the Menu Anchor to display/remove pop-up widgets through script.
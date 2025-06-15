# Creating Drag and Drop UI

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-drag-and-drop-ui-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-drag-and-drop-ui-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:27

---

There may be instances in your project where you want your players to be able to interact with UI elements by dragging and dropping them onscreen. This could be to customize interface layouts (positioning health bars or unit frames) or interacting with gameplay systems like inventory screens (adding/removing items around). With UMG you can create these types of interactions with the **DragAndDropOperation** node and override some of the inherited Blueprint Functions based on your method of interaction.

In this example, we take a look at how a player can drag and reposition a health bar on screen with the Left Mouse Button. At the end of this guide, you will have a UI widget that you can drag around inside the viewport and drop at a new location.

## 1 - Project Setup

Before we get started, there are a couple assets that we need to create as part of our project setup. In this example, the element in our HUD that we want to drag and drop is the **HealthBar**. To do this, we will create a **DragWidget** in the same shape as our Health Bar rather than dragging the actual Health Bar around. This separates the Health Bar programming from the drag and drop function.

For this how-to guide, we are using the **Blueprint Third Person** template project.

1.  In the **Content Browser**, create three **Widget Blueprints** called: **DragWidget**, **HealthBar**, and **HUD**.
    
    ![Create three Widget Blueprints called: DragWidget, HealthBar, and HUD](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1225f1d-3183-405a-a1f4-690c6d8baca0/ue5_1-01-creat-widget-blueprints.png "Create three Widget Blueprints called: DragWidget, HealthBar, and HUD")
2.  Right-click in the **Content Browser**, create a new **Blueprint Class**.
    
    ![Create a new Blueprint Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/672bb322-e225-4931-9f81-7f3d926bc4fa/ue5_1-02-create-blueprint-class.png "Create a new Blueprint Class")
3.  Select the **DragDropOperation** class as a parent class, and name created Blueprint Class **WidgetDrag**.
    
    ![Select the DragDropOperation class as a parent class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fa9eb66-7a55-43dd-b2a6-be98aeb9df1e/ue5_1-03-select-parent-class.png "Select the DragDropOperation class as a parent class")
    
    This specialized Blueprint Class enables us to pass through information as part of our drag and drop action.
    
4.  Open the **WidgetDrag** Blueprint, and create a **User Widget** variable called **WidgetReference**. Check the boxes for **Instance Editable** and **Expose on Spawn**.
    
    ![Create and set WidgetReference variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bc1e516-9716-4c03-a32c-0a5806d0edef/ue5_1-04-create-widget-reference-variable.png "Create and set WidgetReference variable")
    
    This will be used to hold the UMG Widget that we want to drag around on screen.
    
5.  Create a **Vector 2D** variable called **DragOffset**. Check the boxes for **Instance Editable** and **Expose on Spawn**.
    
    ![Create and set DragOffset variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aede48c3-bdfb-454b-b8f2-40034d2bf5f0/ue5_1-05-create-drag-offset-variable.png "Create and set DragOffset variable")
    
    This offsets the location from where we start dragging and dropping the widget.
    
6.  **Compile** and **Save** the **WidgetDrag** Blueprint.
    
    ![Compile and save the WidgetDrag Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/033cc1da-fd70-442a-97cd-c77ed32e989a/ue5_1-06-compile-save-widget-drag.png "Compile and save the WidgetDrag Blueprint")
7.  Navigate to UI folder and open the **Drag Widget** Blueprint.
    
    ![Open the Drag Widget Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c003d7e0-3556-4c1e-a24e-6a692dbc1012/ue5_1-07-open-drag-widget.png "Open the Drag Widget Blueprint")
8.  Select **Graph** Tab in the **Blueprint Editor**.
    
    ![Select Graph Tab in the Blueprint Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e7a3056-0976-466e-b812-f6786295101d/ue5_1-08-select-graph-tab.png "Select Graph Tab in the Blueprint Editor")
9.  Under **My Blueprint** tab create a **User Widget** variable called **WidgetReference**. Check the boxes for **Instance Editable** and **Expose on Spawn**.
    
    ![Create and set WidgetReference variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30cf6573-f33f-4b46-8260-264d6d8105b2/ue5_1-04-create-widget-reference-variable.png "WidgetReference")
10.  **Compile** and **Save** the **DragWidget** Blueprint.
    
    ![Compile and save the DragWidget Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2f545d1-a5ba-461d-9294-d79cee4f083e/ue5_1-09-compile-save-drag-widget.png)

With our project setup done, next we will start working on the HealthBar Widget Blueprint which is the piece of UI that we want to be draggable.

## 2 - Setting Up the Health Bar Widget

In this step, we determine when the Left Mouse Button is pressed and store the location where it was pressed in screen space. We also use the **DetectDragIfPressed** node to determine if the player is dragging with a specified key.

1.  Open the **HealthBar** Widget Blueprint, and navigate to the **Hierarchy** Panel.
    
    ![Open the HealthBar Widget Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c934666b-0b72-4cb6-9929-801725322af9/ue5_1-10-open-health-bar-widget.png "Open the HealthBar Widget Blueprint")
2.  Add a **Size Box** and add a **Progress Bar** to the box. In the **Details** Panel for the **Size Box**, set the **Width** to **500** and **Height Override** to **50**.
    
    ![Add and set a Size Box and add a Progress Bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d82d538-9c73-40a8-88e5-0d9a230615b4/ue5_1-11-set-size-box-overrides.png "Add and set a Size Box and add a Progress Bar")
    
    You can also stylize the **Progress Bar**. Select the **Progress Bar** in the **Hierarchy** Panel, change the color under **Fill Color and Opacity** and set the **Percent** to **1.0** in the **Details** Panel so the progress bar is filled and can changes color.
    
    ![Stylize the Progress Bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eab9bb9b-66b7-4c40-a243-4d31fd34f021/ue5_1-12-set-color-and-percent.png "Stylize the Progress Bar")
3.  Set the preview to **Desired on Screen**.
    
    ![Set the preview to Desired on Screen](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f4f35bd-0389-42c9-8b5e-d113424bf3db/ue5_1-13-set-desired-on-screen.png "Set the preview to Desired on Screen")

### 2.1 - Scripting the On Mouse Button Down Function

This step enables us to determine if the player is dragging the Left Mouse Button.

1.  Select **Graph** Tab in the **Blueprint Editor**.
    
    ![Select Graph Tab in the Blueprint Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12d93e98-a424-4437-9460-a7098e47307a/ue5_1-08-select-graph-tab.png "Select Graph Tab in the Blueprint Editor")
2.  In the **My Blueprint** Panel, add the **OnMouseButtonDown** and **OnDragDetected** overrides. This creates tabs for each of the overrides in the **Event Graph**.
    
    ![Add the OnMouseButtonDown and OnDragDetected overrides](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4ef9a2b-4261-411b-a498-b8177286cf65/ue5_1-14-create-overrides.png "Add the OnMouseButtonDown and OnDragDetected overrides")
    
    There are several functions that you can override to call your own custom script. Here we will perform some checking when the Mouse Button is pressed and what happens when a widget drag is detected.
    
3.  Select the **OnMouseButtonDown** tab. From the **OnMouseButtonDown** node, drag off the **My Geometry** pin and add the **Absolute to Local** node.
    
4.  Drag off the **Mouse Event** pin and add the **Get Screen Space Position** node and connect the Return Value to the **Absolute Coordinate** pin.
    
    ![BP script of the OnMouseButtonDown override](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89f9c3ec-80d1-4c10-894a-5d01b6671a12/ue5_1-15-onmousebuttondown-bp-script-1.png "BP script of the OnMouseButtonDown override")
    
    This converts the absolute coordinates of the Health Bar widget to local space by getting the screen position where the mouse button registered a button down key press. This stores the location as a variable so we can determine where on the widget the player actually clicked and where it gets dropped.
    
5.  Right-click the **Return Value** of the **Absolute to Local** node, and select **Promote to Variable**. Name the variable **Drag Offset**.
    
    *Click for full view.*
    
    Don't worry if you see an error on the On Mouse Button Down node. Once we complete the function it will go away.
    
6.  Right-click in the graph and add a **Detect Drag if Pressed** node. Set the **Drag Key** to **Left Mouse Button**.
    
7.  Finish connecting the remaining pins.
    
    -   Connect **Mouse Event** to **Pointer Event**.
    -   Connect the **Return Value** pins from **Detect Drag if Pressed** to **Return Node**
    -   Connect the **Exec** pins across the four nodes.
    
    *Click for full view.*
    
    This determines if the player is dragging the Left Mouse Button, which will start the **On Drag Detected** script.
    
8.  **Compile** and **Save** the **HealthBar** Blueprint.
    
    ![Compile and Save the HealthBar Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ef0354a-a7d2-464c-8a98-1db24218c51d/ue5_1-18-compile-save-healthbar-widget.png "Compile and Save the HealthBar Blueprint")

### 2.2 - Scripting the On Drag Detect Function

In this step, we determine what happens when the player is, in fact, dragging the HealthBar around on the screen.

1.  Select the **OnDragDetected** tab. From the **OnDragDetected** node, Right-click and add a **Create Widget** node. Set the **Class** to **Drag Widget**.
    
    ![BP script of the OnDragDetected override](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee467624-e1c8-456c-867c-46475657a0d3/ue5_1-19-ondragdetected-bp-script-1.png "BP script of the OnDragDetected override")
2.  From the **Widget Reference** pin, connect a **Self** node. **Promote** the Return Value to a variable called **Dragged Widget** and connect the pins.
    
    ![BP script of the OnDragDetected override](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da075b5f-3a18-4388-9287-83f32c00bf1b/ue5_1-20-ondragdetected-bp-script-2.png "BP script of the OnDragDetected override")
    
    Now when we create the drag widget, it will have a reference to the existing Health Bar widget. We also promote the dummy drag widget to a variable so that we have access to it later and can remove it from the display when we choose to drop the widget.
    
3.  Right-click and create a **Drag & Drop Operation** node. Set the **Class** to **Widget Drag**, and set **Pivot** to **Mouse Down**.
    
    ![Create a Drag & Drop Operation node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bfe97d8b-6108-42b5-857f-9821c342eb91/ue5_1-21-create-widget-drag-node.png "Create a Drag & Drop Operation node")
    
    Pivot determines where the Drag Widget Visual appears while being dragged relative to the pointer performing the drag operation.
    
4.  Connect the following nodes to the **DragAndDropOperation** node pins.
    
    -   **Exec** line from the **Dragged Widget Set** through to the **Return Node**
    -   **Self** to **Widget Reference**
    -   **Dragged Widget** to **Default Drag Visual**
    -   **Drag Offset** to **Drag Offset**
        
    
    *Click for full view.*
    
    Above we indicated what Widget Blueprint is our reference and what the drag visual should be and provided an offset in which to start dragging. There is an offset pin on the node by default; however, we are using our own calculation to determine the position in which to start dragging when Mouse Button Down is pressed.
    
5.  **Compile** and **Save** the **HealthBar** Blueprint.
    
    ![Compile and Save the HealthBar Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c391ff9c-8e84-4bb0-82da-791bb0c38fb2/ue5_1-18-compile-save-healthbar-widget.png "Compile and Save the HealthBar Blueprint")

Next, we need to do is to determine what happens when the player releases the Left Mouse Button and performs the OnDrop function.

## 3 - Setting up the On Drop Function

Here we set up our main **HUD** Widget Blueprint and override what happens when we perform the **OnDrop** function.

1.  Open the **HUD** Widget Blueprint.
    
    ![Open the HUD Widget Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/447f155e-c5dd-4ab4-89aa-582104adf8d3/ue5_1-23-open-hud-widget.png "Open the HUD Widget Blueprint")
2.  Drag the **Canvas Panel** from the **Palette** Panel to the **Hierarchy** Panel. Select the **Canvas Panel** and in the **Details** Panel set the **Visibility** to **Visible**.
    
    ![Add and set Canvas Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e8f3503-dba5-46b1-9622-5080757b2aab/ue5_1-24-drag-canvas-panel-set-visibility.png "Add and set Canvas Panel")
    
    We scripted the drag detection inside the Health Bar widget; however, when we release the Left Mouse Button we want to drop the bar in our HUD Widget Blueprint. In order for our HUD to receive the hit detection, we need to make the panel Visible.
    
3.  From the **Palette** Panel, add the **Health Bar** widget to the **Canvas Panel**.
    
    ![Add the Health Bar widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/003f100a-f5f3-4a24-81e0-303214775d47/ue5_1-25-drag-health-bar.png "Add the Health Bar widget")
4.  In the **Event Graph**, add an **OnDrop** function override from the **My Blueprint** panel.
    
    ![Add an OnDrop override](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53e2658f-286a-4b8b-8f54-b5f15a29f4d5/ue5_1-26-create-ondrop-override.png "Add an OnDrop override")
5.  From the **OnDrop** node, drag off **Operation** and add a **Cast to WidgetDrag** node. Then, add a **Get Widget Reference** and connect the **As Widget Drag** pin to a **Widget Reference** and **Drag Offset** nodes.
    
    ![BP script of the OnDrop override](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ad44c5c-419d-4edb-9e66-6bb271efdd9b/ue5_1-27-ondrop-bp-script-1.png "BP script of the OnDrop override")
    
    This checks which type of operation is being performed as part of the **OnDrop** function. If it is **Widget Drag** we get the **WidgetReference** (which we passed through as the widget being dragged), as well as the **DragOffset** (or position in which we started the drag from).
    
6.  From the **My Geometry** pin, add an **Absolute to Local** node. From the **Pointer Event** pin, add a **GetScreenSpacePosition** node.
    
    *Click for full view.*
    
    This will tell us the position in 2D space where we released the Left Mouse Button to drop the widget. We will use this minus the **DragOffset** to determine where we should place the widget when it is dropped.
    
7.  Add a **Subtract** node and subtract the **DragOffset** from the the **Return Value** of **Absolute to Local**.
    
    *Click for full view.*
    
8.  Right-click and add **Remove from Parent**, **Add to Viewport**, and **Set Position in Viewport** nodes. Connect the **Exec** pins across all 3 modes in the order listed above, and connect the **Set Position in Viewport** node to the **Return Node**.
    
9.  Make the following connections and adjustments:
    
    -   **Widget Reference** pin to **Target** pin on all 3 nodes.
    -   **Return Value** pin from the **Vector2D - Vector 2D** node to the **Position** pin.
    -   Uncheck **Remove DPIScale**
    -   Check **Return Value**
    
    *Click for full view.*
    
    We uncheck **Remove DPIScale** and check the **Return Value** because we do not need to remove the [DPI Scaling](/documentation/en-us/unreal-engine/dpi-scaling-in-unreal-engine). We already handled this function, so we return as true. With this script, we first remove the existing Health Bar widget before re-adding it to the screen in the new location relative to our Drag Offset.
    
10.  **Compile** and **Save** the **HUD** Widget Blueprint.
    
    ![Compile and Save the HUD Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b81834c-33e3-4921-ba03-cd9fb45aec8e/ue5_1-31-compile-save-hud-widget.png)

Our HUD is set up to handle dropping our dragged widget and it displays our Health Bar. Next, we set up our Dragged Widget to mimic the shape of our Health Bar as well as instruct our Character Blueprint to add the HUD to the viewport.

## 4 - Scripting the Drag Widget

In this step, we configure the **DragWidget**, which is the visual widget we will be dragging in the viewport.

1.  Open the **DragWidget** Widget Blueprint.
    
    ![Open the DragWidget Widget Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09daede7-0437-49a5-a9d9-64a5ce7dfd6a/ue5_1-32-open-drag-widget.png "Open the DragWidget Widget Blueprint")
2.  Add **Size Box** and **Border** widgets to the **Hierarchy** panel. Rename the **SizeBox** to **WidgetSize**, and set **isVariable** to true. Check both **Width Override** and **Height Override**.
    
    ![Add and set Size Box and Border widgets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56873b22-9340-4fca-b8f8-a0489d818188/ue5_1-33-set-size-box.png "Add **Size Box** and **Border** widgets")
    
    We are going to set the Width and Height of the Size Box to reflect the size of our Health Bar widget.
    
3.  Select **Border**, and set the **Brush Color** to **Black** with an **Alpha** of **0.5** for some transparency.
    
    ![Set Brush Color for Border](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c371f01a-7a8b-4195-a7f7-b5458295a204/ue5_1-34-set-border-brush-color.png)
    
    In this example, we will have a silhouette of our Health Bar as the drag visual while keeping the actual Health Bar in the same location.
    
4.  Select **Graph** Tab in the **Blueprint Editor**.
    
    ![Select Graph Tab in the Blueprint Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed3b96f5-5f42-4b97-8015-0e3710ad0c3a/ue5_1-35-select-graph-tab.png)
5.  In the **Event Graph**, off of **Event Construct**, add a **Cast to HealthBar** node. Drag in the **Widget Reference** and connect it to the **Object** pin.
    
6.  From the **As Health Bar** pin, add a **Get Desired Size** node. Connect the Return Value pin to a **Break Vector 2D** node.
    
    *Click for full view.*
    
    This gives us the size of our Health Bar and we can set the Size Box to the same size. We could have manually entered the overrides; however, if we change the size of our Health Bar we would then also have to change it here.
    
7.  Right-click and add **Set Height Override** and **Set Widget Override** nodes and connect them respectively to the **Cast to HealthBar** node. Then, drag in the **Widget Size** node.
    
8.  Connect the following pins:
    
    -   **Widget Size** to both **Target** pins
    -   Break Vector 2D **X** to **In Height Override**
    -   Break Vector 2D **Y** to **In Width Override**
        
    
    *Click for full view.*
    
9.  **Compile** and **Save** the **DragWidget** Blueprint.
    
    ![Compile and Save the DragWidget Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/673b82ca-ece8-424c-84e1-b6bd833786d4/ue5_1-09-compile-save-drag-widget.png "Compile and Save the DragWidget Blueprint")

## 5 - Adding the HUD Widget to the Viewport

Lastly, we need to add the **HUD** Widget Blueprint to the viewpoint in the **Character** Blueprint and enable the Mouse Cursor so we can see where we are dragging.

1.  In the **Content Browser** under **Content/ThirdPerson/Blueprints**, open the **BP-ThirdPersonCharacter** Blueprint.
    
2.  Off the **Event Begin Play** node, add a **Create Widget** node and set the **Class** to **HUD**. Create an **Add to Viewport** node connect it to **SET Show Mouse Cursor**. Add a **Get Player Controller** node and connect the **Return Value** to the **SET Target**.
    
    *Click for full view.*
    
3.  **Compile** and **Save** the **BP\_ThirdPersonCharacter** Blueprint.
    
    ![Compile and save the BP_ThirdPersonCharacter Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9123c26a-929e-40f5-8b23-af53542eaa07/ue5_1-39-compile-save-character-bp.png "Compile and save the BP_ThirdPersonCharacter Blueprint")
4.  Click the **Play** button to play with the drag and drop widget.
    
    ![Click the Play button to play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0b12d39-90af-470f-82c5-87c1ba1cce11/ue5_1-40-click-play-button.png "Click the Play button to play")

### End Result

When you play in the Editor, you can left-click and drag the health bar on screen then drop it in a new location.

This is just an example of the elements you will need to start the Drag and Drop process. Additional checking may be needed to ensure that players do not drag the widget outside of Safe Zones or potentially on top of other widgets.
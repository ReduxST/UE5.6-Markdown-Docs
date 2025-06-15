# Gameplay Camera System Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-camera-system-quick-start](https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-camera-system-quick-start)  
**Processed:** 2025-06-14 16:24:53

---

This quick start guide will teach you how to create three different camera rigs by using the **Gameplay Camera System**. These camera rigs will replicate the following camera setups from the templates that come with Unreal Engine:

-   Third Person
-   First Person
-   Top Down

To learn more about the system, read the [Gameplay Camera System Overview](/documentation/en-us/unreal-engine/gameplay-camera-system-overview) documentation.

## Required Setup

1.  Create a new project and select the **Games** category and the **Third Person** template.
    
    -   Enter your project's **Location** and **name**.
    -   Click **Create**.
    
    ![Create a new project and select the Third Person template](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02fb31df-cb54-46e3-ba63-97aab3802162/gameplay-cameras-quickstart-1.png)
2.  Click **Settings > Plugins** to open the **Plugins** window.
    
    -   Search for and **enable** the **Gameplay Cameras** plugin. Restart the editor, if necessary.
    
    ![Click Settings - Plugins to open the Plugins window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67ce8687-34c0-4612-8f22-413faf48baa7/gameplay-cameras-quickstart-2.png) ![Search for and enable the Gameplay Cameras plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3240c3ce-50e5-4006-ac6b-c2e2fdd74d0b/gameplay-cameras-quickstart-3.png)
3.  In the editor, click **File > New Level**.
    
    -   Select the **Basic** template and click **Create**.
    
    ![Select the Basic template and click Create](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c54bb0c-fae3-4c29-ac48-30b8a30e0b63/gameplay-cameras-quickstart-4.png)

### Section Results

In this section, you created a new project and set it up so you can use the Gameplay Camera System to create several camera setups for the player.

## Creating the Camera Asset

The **Camera Asset** contains information about one or more **Camera Rigs**, **transitions**, and the **Camera Director** used to determine the active Camera Rig during gameplay.

To create a Camera Asset, follow these steps:

1.  Right click in the **Content Browser** and select **Gameplay > Camera Asset**.
    
    ![Right click in the Content Browser and select Gameplay - Camera Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e79c189-cbf1-4492-aa12-551fa2e8fa08/gameplay-cameras-quickstart-5.png)
2.  In the **Pick Camera Director Type** window, select the **Blueprint Camera Director** and click **Select**.
    
    ![Select the Blueprint Camera Director and click Select](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf021e9c-558c-40a4-947f-035298ded9c8/gameplay-cameras-quickstart-6.png)
3.  Name the asset **CA\_PlayerCameras**.
    

### First-Person Camera Rig

1.  Open **CA\_PlayerCameras** and click **Rigs** in the toolbar to see the available Camera Rigs.
    
2.  Rename the default rig to **FirstPerson**.
    
    ![Open CA_PlayerCameras, click Rigs and rename the default rig to FirstPerson](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30d87c5e-57b8-49ef-a8f3-90630cbaa4a7/gameplay-cameras-quickstart-7.png)
3.  Click the **Toolbox** panel to see the available nodes.
    
    ![Click the Toolbox panel to see the available nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7817f3bc-ceb9-4ab7-a62f-3a5e4189545a/gameplay-cameras-quickstart-8.png)
4.  Add a **Sequence** node and a **Boom Arm** node as seen below.
    
5.  With the **Boom Arm** node selected, go to the **Details** panel and set the **Boom Offset** to **50**, **0**, **50** for X, Y, Z, respectively.
    
    ![Add a Sequence node and a Boom Arm node and set the Boom Offset to 50, 0, 50](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a54db53-04b5-4f61-913e-b4f6c0fd73df/gameplay-cameras-quickstart-9.png)
6.  Add a **Field of View** node and go to the **Details** panel and set the **Field of View** to **100**.
    
    ![Add a Field of View node and set the Field of View to 100](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f51cc020-a094-481f-9d99-4b3b63f215ff/gameplay-cameras-quickstart-10.png)

### Third-Person Camera Rig

1.  Create a new **Camera Rig** and name it **ThirdPerson**.
    
    ![Create a new Camera Rig and name it ThirdPerson](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72c7a1db-40b6-4e7f-be9f-9fec4ab82753/gameplay-cameras-quickstart-11.png)
2.  Add a **Sequence** node and a **Boom Arm** node as seen below.
    
3.  With the **Boom Arm** node selected, go to the **Details** panel and set the **Boom Offset** to **\-500**, **0**, **50** for X, Y, Z, respectively.
    
    ![Add a Sequence node and a Boom Arm node and set the Boom Offset to -500, 0, 50](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a167fd34-3cde-458c-8f4d-b31b7ee688d8/gameplay-cameras-quickstart-12.png)
4.  Drag from the **Input Slot** pin and select **Input Axis Binding 2D**. This exposes the InputSlot to Blueprints, which you will modify later.
    
    ![Drag from the Input Slot pin and select Input Axis Binding 2D](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ad730f8-fc6a-4eeb-8dd6-497b59aecfec/gameplay-cameras-quickstart-13.png)
5.  Go to the **Details** panel and add the **IA\_Look** Axis Action.
    -   **Enable** the **Clamp Y Min** and **Max** checkboxes and enter **\-80** and **10** for the **Min Value** and **Max Value**, respectively.
    -   **Enable** the **Revert Axis Y** checkbox.
        
        ![Add the IA_Look Axis Action, enter -80 and 10 to the Clamp Y Min and Max checkboxes, and Enable the Revert Axis Y checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1af7a43-7d27-4535-926e-d3ca45e45b66/gameplay-cameras-quickstart-14.png)
6.  Drag from the **BoomOffset** pin and click **Camera Rig Parameter** to expose this variable to Blueprints.
    
    ![Drag from the BoomOffset pin and click Camera Rig Parameter to expose this variable to Blueprints](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb4e3134-f6c0-437f-a333-a030c3062ab7/gameplay-cameras-quickstart-35.png)
7.  Add a **Field of View** node and a **Dampen Position** node. Then with the **Dampen Position** node selected, go to the **Details** panel and enter **5** for the **Forward Damping Factor**.
    
    ![Add a Field of View node and a Dampen Position node and enter 5 for the Forward Damping Factor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1539326d-824c-44aa-b0a8-ae0f85ce2038/gameplay-cameras-quickstart-15.png)
8.  Add an **Occlusion Material** node and go to the **Details** panel and select a material from the **Occlusion Transparency Material** dropdown. In the example below, you can see the translucent material used for this example.
    
    ![Add an Occlusion Material node and select a material from the Occlusion Transparency Material dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc5a61f5-b69b-451b-91d8-103b3658bed6/gameplay-cameras-quickstart-16.png) ![Translucent material used for this example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b802265-9643-48e7-9f9b-398d9913e427/gameplay-cameras-quickstart-17.png)

### Top-Down Camera Rig

1.  Create a new **Camera Rig** and name it **TopDown**.
    
    ![Create a new Camera Rig and name it TopDown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa9bdd70-20c8-458b-a2cb-0d3eae08b559/gameplay-cameras-quickstart-18.png)
2.  Add a **Sequence** node and a **Boom Arm** node as seen below. With the **Boom Arm** node selected, go to the **Details** panel and set the **Boom Offset** to **\-1000**, **0**, **0** for X, Y, Z, respectively.
    
    ![Add a Sequence node and a Boom Arm node and set the Boom Offset to -1000, 0, 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/668b0857-4e79-40c0-a0c4-0169f84a3f02/gameplay-cameras-quickstart-19.png)
3.  Add a **Field of View** and a **Dampen Position** nodes. Then with the **Dampen Position** node selected, go to the **Details** panel and enter **5** for the **Forward Damping Factor**.
    
    ![Add a Field of View and a Dampen Position nodes and enter 5 for the Forward Damping Factor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fc26bb1-d076-4a62-94a4-57af25505883/gameplay-cameras-quickstart-21.png)
4.  Add an **Occlusion Material** node and go to the **Details** panel and select a material from the **Occlusion Transparency Material** dropdown. Use the same material you used for the **Third Person Camera Rig**.
    
    ![Add an Occlusion Material node and select a material from the Occlusion Transparency Material dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/015ce4c1-a356-4118-b02c-4ae4a4d13aa6/gameplay-cameras-quickstart-22.png)

### Camera Director

1.  Click the **Director** button to navigate to the **Director** tab.
    
2.  Click **+** to create a new **Director Blueprint**.
    
    ![Click the Director button and click + to create a new Director Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4bbf6fb7-de98-49d3-bbbc-464222a299e6/gameplay-cameras-quickstart-32.png)
3.  Select the **destination folder**, enter the name **CDE\_PlayerCameras** and click **Save**.
    
    ![Select the destination folder, enter the name CDE_PlayerCameras and click Save](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d47d8432-3a42-4f06-b50a-2d196af15ba0/gameplay-cameras-quickstart-33.png)
4.  Click **Build**.
    
    ![Click Build](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20139a54-8d1e-45a6-ad46-eb8b41e951fe/gameplay-cameras-quickstart-34.png)

### Section Results

In this section, you created three Camera Rigs that will be used by the player character Blueprint.

## Creating the Camera Transitions

In this section you will create transitions for the Camera Rigs you created in the previous section.

Follow these steps to create Camera Rig transitions:

1.  Open the **First Person Camera Rig** and click **Transitions**.
    
    -   Drag from **Exit Transitions 0** pin and select **Exit Transition**.
    -   Drag from the **Blend** pin of the **Camera Rig Transition** node and select **Smooth Blend**.
    
    ![Open the First Person Camera Rig and click Transitions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29e3dec0-f35c-49ad-93c3-f7dceab7e921/gameplay-cameras-quickstart-45.png) ![Drag from Exit Transitions 0 pin and select Exit Transition, then drag from the Blend pin and select Smooth Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f1c9dbf-299a-49df-b524-2df59c7a3a9c/gameplay-cameras-quickstart-46.png)
2.  Repeat the steps above for the **Third Person** and **Top Down** Camera Rigs.
    
    ![Repeat the steps above for the Third Person Rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ba1ed56-0ef1-4240-b877-32550c828854/gameplay-cameras-quickstart-47.png) ![Repeat the steps above for the Top Down Camera Rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a63e22f-5291-44a1-b07b-41c72170f648/gameplay-cameras-quickstart-48.png)

### Section Results

In this section, you created transitions for the Camera Rigs.

In the next section, you will modify the player Blueprint so it can use the Camera Rigs during gameplay.

## Adding the Gameplay Camera Component to the Player

To add the **Gameplay Camera component** to the player Blueprint, follow these steps:

1.  In the **Content Browser**, go to **ThirdPerson > Blueprints** and double click **BP\_ThirdPersonCharacter** to open the Blueprint.
    
    ![Open the BP_ThirdPersonCharacter Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08b5f95c-cd0d-465b-bd0d-1db0a112baf0/gameplay-cameras-quickstart-23.png)
2.  Go to the **Components** window and delete the **CameraBoom** and **FollowCamera** components.
    
    ![Delete the CameraBoom and FollowCamera components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76728d3d-3b54-443d-9dbd-1c68fcadc721/gameplay-cameras-quickstart-24.png)
3.  Click **+Add** and select **GameplayCamera** to add the component.
    
    -   Go to the **Details** panel and scroll down to the **Camera** section and add **CA\_PlayerCameras** to the **Camera** dropdown.
    -   Go to the **Activation** section and **enable** the **Auto Activate** checkbox. Then select **Player 0** from the **Auto Activate for Player** dropdown.
    
    ![Click +Add and search for then select GameplayCamera to add the component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c152cbca-4e69-4e4c-b519-eb6728d1daa1/gameplay-cameras-quickstart-25.png) ![Add CA_PlayerCameras to the Camera dropdown and enable the Auto Activate checkbox, then select Player 0 from the Auto Activate for Player dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4beeae1e-1f9b-4d93-9f69-808d62110030/gameplay-cameras-quickstart-26.png)
4.  Go to the **Event Graph** and add **three input events** for the numbers **1**, **2**, and **3** on your keyboard.
    
    -   Create a new **Integer variable** and call it **ActiveCameraRig**.
    -   Drag the variable to the **Event Graph**, select **Set Active Camera Rig** and connect it to the first keyboard event.
    -   Repeat this for the other two events and set their values to **0**, **1**, and **2**, as shown below.
    
    ![Go to the Event Graph and add three input events for the numbers 1, 2, and 3 on your keyboard, then select Set Active Camera Rig and connect it to the keyboard events](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06cf205d-f685-4fbe-86cf-6fe4910d8a4d/gameplay-cameras-quickstart-27.png)
    
    The value of this variable will be used later to determine which Camera Rig is active during gameplay.
    
5.  Add a **Mouse Wheel Up** and **Mouse Wheel Down** input events in the **Event Graph**.
    
    -   Create a Float variable named **BoomLength** and set its **default value** to **\-500**.
    -   Create a Float variable named **BoomZoomStep** and set its **default value** to **25**.
    
    ![Add a Mouse Wheel Up and Mouse Wheel Down input events in the Event Graph and create Float variables named BoomLength and BoomZoomStep](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f23499e2-c513-49c2-a34c-f428548e17ba/gameplay-cameras-quickstart-28.png)
6.  Add the **BoomLength** and **BoomZoomStep** nodes to the **Event Graph** as shown below.
    
    -   On **Mouse Wheel Up** **add** the **Boom Zoom Step** to the **Boom Length**.
    -   Conversely, on **Mouse Wheel Down** subtract the **Boom Zoom Step** to the **Boom Length**.
    
    This will zoom in the camera on mouse wheel up and zoom out the camera on mouse wheel down.
    
    ![Set the BoomLength by adding and subtracting the BoomZoomStep](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f2e6117-bb7f-44b4-8293-8963a9b6e11b/gameplay-cameras-quickstart-29.png)
7.  Drag the **GameplayCamera component** to the **Event Graph** to create a node.
    
    -   Drag from the **GameplayCamera** node and search for then select **Get Initial Variable Table**.
    
    ![Drag the GameplayCamera component to the Event Graph and drag from the GameplayCamera node and select Get Initial Variable Table](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec008502-7658-444b-be76-f65eadf50113/gameplay-cameras-quickstart-30.png)
8.  Drag from the **Return Value** pin of the **Get Initial Variable Table** node and search for then select **Set Camera Rig Parameters**.
    
    -   Select **CA\_PlayerCameras** and click the **ThirdPerson** rig.
    -   Connect the **Set BoomLength** node to the **Set Camera Rig Parameters** node.
    
    ![Drag from the Get Initial Variable Table node and search for then select Set Camera Rig Parameters, then select CA_PlayerCameras and click the ThirdPerson rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4207ea23-7902-4915-9f4b-60607e64b81d/gameplay-cameras-quickstart-31.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d2b383d-6d4f-4591-9372-697734dae6c4/gameplay-cameras-quickstart-36.png)
9.  Right click the **Boom Offset** pin and select **Split Struct Pin**, then connect the **Boom Length** variable to the **Boom Offset X** pin.
    
    ![Connect the Set BoomLength node to the Set Camera Rig Parameters node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b6a8167-2b17-4beb-99af-5e65d5a1c47d/gameplay-cameras-quickstart-37.png)
10.  Repeat the steps above for the **Mouse Wheel Down** input event. You can see the final Blueprint code below.
    
    ![Repeat the steps above for the Mouse Wheel Down input event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1b93a65-3e76-46c8-88f6-e718e1f27f7e/gameplay-cameras-quickstart-38.png)

### Section Results

In this section, you added the Gameplay Camera component to the player Blueprint. You also added scripting to switch between Camera Rigs and zoom in and out of the Third Person Camera Rig.

In the next section, you will configure the Camera Director Blueprint so it can switch between Camera Rigs when the player presses the 1 - 3 keys.

## Configuring the Camera Director

In this section you will modify the Camera Director Evaluator Blueprint so the player can switch between Camera Rigs during gameplay.

Follow these steps to configure the Camera Director:

1.  Open **CDE\_PlayerCameras** and right click in the **Event Graph**.
    
    -   Search for then select **Find Evaluation Context Owner Actor**.
    -   Click the dropdown and select **BP\_ThirdPersonCharacter**.
    
    ![Search for then select Find Evaluation Context Owner Actor and click the dropdown and select BP_ThirdPersonCharacter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c43a1fc-4b2c-417b-b1a1-33b3b9767df3/gameplay-cameras-quickstart-39.png)
2.  Drag from the **Return Value** pin of the **Find Evaluation Context Owner Actor** node and search for then select **Get Active Camera Rig**.
    
    -   Drag from the **Active Camera Rig** node and search for then select **Switch on Int**.
    -   Click **Add Pin +** three times to add pins **0**, **1**, and **2**.
    
    ![Drag from the Find Evaluation Context Owner Actor node and select get Active Camera Rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86209c1b-899e-405d-9b97-b354c2aa1fb6/gameplay-cameras-quickstart-40.png) ![Drag from the Active Camera Rig node and select Switch on Int](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1210599b-880d-40f1-8449-dd8a27823829/gameplay-cameras-quickstart-41.png)
3.  Drag from the **0** pin of the **Switch on Int** node and search for then select **Activate Camera Rig**.
    
    -   Click the **Camera Rig** dropdown and select **ThirdPerson**.
    
    ![Drag from the 0 pin of the Switch on Int node and select Activate Camera Rig, then click the Camera Rig dropdown and select ThirdPerson](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/109b5185-4406-443e-9979-2d667db9f466/gameplay-cameras-quickstart-42.png)
4.  Add two more **Activate Camera Rig** nodes and connect them to the **1** and **2** pins of the **Switch on Int** node.
    
    -   Set the **Camera Rig** dropdowns to **FirstPerson** and **TopDown**, as shown below.
    
    ![Add two more Activate Camera Rig nodes and connect them to the 1 and 2 pins of the Switch on Int node, then set the Camera Rig dropdowns to FirstPerson and TopDown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3902535d-fe55-4d8f-9edd-c35ddafe7d20/gameplay-cameras-quickstart-43.png)
5.  Drag from the **Find Evaluation Context Owner Actor** node and search for then select **Get Controller**.
    
    -   Drag from the **Get Controller** node and search for then select **Set Control Rotation**.
    -   Right click the **Rotation** pin of the **Set Control Rotation** node and select **Split Struct Pin**.
    -   Set the **New Rotation Y (Pitch)** to **\-50**.
    -   Connect the **Activate Camera Rig** node to the **Set Control Rotation** node, as seen below.
    
    ![Drag from the Find Evaluation Context Owner Actor node and select Get Controller, then drag from the Get Controller node and select Set Control Rotation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23bee084-a96b-40db-aed5-e87abeb4c0b1/gameplay-cameras-quickstart-44.png)
6.  Press **Play** and test the Gameplay Camera System. Press the **1 - 3 keys** to switch between **Camera Rigs** and use the **mouse wheel** to zoom in and out when using the **Third Person** Camera Rig.
    

### Section Results

In this section you learned how to configure the Camera Director so it can switch between Camera Rigs during gameplay.

## 6 - On Your Own!

Now that you learned how to use the Gameplay Camera System, try experimenting by creating new Camera Rigs with different behaviors.
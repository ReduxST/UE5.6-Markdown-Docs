# Aligning the LED Wall to Camera Tracking using ArUcos

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/aligning-the-led-wall-to-camera-tracking-using-arucos-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/aligning-the-led-wall-to-camera-tracking-using-arucos-in-unreal-engine)  
**Processed:** 2025-06-14 16:05:30

---

## Goals

In this Quick Start guide, you will go through the steps to align an LED wall to your camera tracking with ArUco markers.

## Objectives

-   Generate ArUco markers for your LED wall.
    
-   Preview the ArUco markers in the editor Viewport and the stage LED screens.
    
-   Use the ArUco markers to calibrate your LED wall.
    

## 1 - Required Setup

For this guide, you will use a production camera, an optical camera tracking system, and an AJA Kona 5 for source video input. In addition, you will need an existing LED wall configuration and a nDisplay Blueprint that matches your stage LED wall configuration. Follow the [Rendering to Multiple Displays with nDisplay](/documentation/en-us/unreal-engine/rendering-to-multiple-displays-with-ndisplay-in-unreal-engine) documentation to learn how to create your nDisplay Blueprint.

Before proceeding, follow the [Camera Calibration for Production](/documentation/en-us/unreal-engine/camera-lens-calibration-quick-start-for-unreal-engine) guide to make sure the lens distortion and nodal point offset of your camera are calibrated. This will create a Lens File Asset that will be used as part of the LED wall alignment with camera tracking.

The example in this guide is based on the Epic LA RnD stage LED wall setup.

Click image to expand.

## 2 - Generating the ArUco markers

1.  Click **Settings > Plugins** to open the **Plugins Menu**.
    
    ![Open the Plugins Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0bbe524a-cb9a-4da4-a322-e3e70764fc8b/ue5_01-open-plugins-menu.png "Open the Plugins Menu")
2.  Search for the **LED Wall Calibration** and the **Live Link Over nDisplay** plugins and enable them. Restart the editor.
    
    ![Enable the LED Wall Calibration plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16426dfa-744a-412c-b01e-608de8412b4b/ue5_02-enable-led-wall-plugin.png "Enable the LED Wall Calibration plugin") ![Enable the Live Link Over nDisplay plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e41296d7-fa5f-4831-8669-4c7b68c46402/ue5_03-enable-live-link-over-plugin.png "Enable the Live Link Over nDisplay plugin")
3.  In the **Content Browser**, search for your **nDisplay stage** actor Blueprint and double-click it to open it.
    
    ![Double-click the nDisplay stage actor Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83280fc3-5bd6-4287-a0fe-805b05d4aa4e/ue5_04-open-ndisplay-stage.png "Double-click the nDisplay stage actor Blueprint")
    
    Click image to expand.
    
4.  Select your first **wall mesh** from the **Components** panel and double-click the corresponding **cluster** from the **Cluster** panel. This will give you the selected display's resolution.
    
    ![Double-click the corresponding cluster from the Cluster panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03c73087-1787-4405-83f1-088737bf89dc/ue5_06-click-corresponding-cluster.png)
5.  With the wall mesh selected, click **\+ Add Component** and search for and select **Calibration Point**. This will add a Calibration Point component as a child of your wall mesh.
    
    ![Click Add Component and select Calibration Point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b06462ae-cb27-48fd-9eb5-ef8533d076c9/ue5_07-add-calibration-point.png "Click Add Component and select Calibration Point")
6.  Rename the Calibration point to **ArUcoW1**.
    
    ![Rename the Calibration point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a333008-44f8-4d89-a3e1-b6d8fbf27251/ue5_08-rename-calibration-point.png "Rename the Calibration point")
7.  With the Calibration Point selected, go to the **Details** panel and scroll down to the **Calibration** section. Click **Create ArUcos**.
    
    ![Add a Calibration Point component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a208131-d7ce-4ee2-aac8-2b7d2753b2d1/ue5_09-create-arucos.png "Add a Calibration Point component")
8.  The **ArUco Generation Options** window will open.
    
    1.  Enter the **Texture Width** and **Texture Height** values that correspond to the wall viewport that ArUcos are being applied to.
        
    2.  Select the appropriate **ArUco Dictionary** from the list. In this example, the **DICT\_6x6\_1000** dictionary is selected, which has 1000 unique ArUco symbols.
        
    3.  Enter the **Marker ID** that will be used as the starting ID for the ArUco markers that will be generated.
        
    4.  Enter the **Place Modulus** value. This value represents the number of LED panels that will be skipped when placing the ArUco markers. This is useful for working on a large LED wall, where you would use over 1000 unique ArUco symbols if they were to be placed on every LED panel. The default value is 2. Change this to 1 for smaller LED walls where one ArUco can be displayed on every panel. Using the default value of 2 will place an ArUco symbol on every second LED panel.
        
    5.  Click **OK** to generate the ArUco markers.
        
        ![Enter the ArUco generation options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/561c33a0-adf8-4013-ae03-2f035058cde4/ue5_10-generate-aruco-markers.png "Enter the ArUco generation options")
9.  Select a location to save the texture and click **OK**. A confirmation window will appear that tells you which **marker Id** to start from for the next viewport. This will be remembered by UE, but can be adjusted in case you need to change the order. Click **OK** to confirm.
    
    ![Select a save destination for the texture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c6fa1da-2da6-42f0-9463-6ed2bb660a1e/ue5_11-select-save-destination.png "Select a save destination for the texture") ![Confirmation message after saving the texture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eeec043e-fc83-42ad-a3c0-892923c3ca73/ue5_12-confirmation-message.png)
10.  Select the **Viewport** to which the calibration point was applied in the **Cluster** tab.
    
    ![Select the Viewport where the calibration point was applied to in the Cluster tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94b91e46-19e5-4510-abd2-a6e68f395eb4/ue5_13-select-viewport.png)
11.  Go to the **Details** panel on the right. Scroll down to the **Texture Replacement** section and select the generated texture as the **Source Texture**. Enable the **Enable Viewport Texture Replacement** checkbox.
    
    ![Add the generated texture as the Source Texture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52650749-2e54-44f9-994f-9cf67ebe82c5/ue5_14-enable-viewport-texture-replacement.png "Add the generated texture as the Source Texture")
12.  Repeat steps 5 to 10 to add the ArUco markers to the remaining LED viewports.
    
13.  In the **Content Browser**, double-click the **nDisplay Blueprint** to open it.
    
    ![Double-click the nDisplay stage actor Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf40cb95-6817-4c6d-8b54-2279871316c2/ue5_15-click-ndisplay-stage-actor.png "Double-click the nDisplay stage actor Blueprint")
14.  Click **\+ Variable** to create a new **boolean** variable and name it **Replace\_Viewport\_Textures**. Go to the **Details** panel and enable the **Instance Editable** checkbox.
    
    ![Create a new variable and call it Replace_Viewport_Textures](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1890558d-5f0b-4d89-9f25-3f77ace1376d/ue5_16-reate-new-variable.png "Create a new variable and call it Replace_Viewport_Textures") ![Enable the Instance Editable checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23cce998-5bb1-470e-9f51-c09bc9b6c637/ue5_17-enable-instance-editable.png "Enable the Instance Editable checkbox")
15.  Drag **Replace\_Viewport\_Textures** to the **Event Graph** and select **Get Replace\_Viewport\_Textures** to create a node.
    
16.  Right-click in the **Event Graph** and search for and select **Set Replace Texture Flag for All Viewports**.
    
17.  Connect the **Event Tick** node to the **Set Replace Texture Flag for All Viewports** node. Connect the **Replace Viewport Textures** node to the **Replace** pin of the **Set Replace Texture Flag for All Viewports** node.
    
    ![Connect the Event Tick node to the Set Replace Texture Flag for All Viewports node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d3659ac-b4fc-4f65-a4cc-5d2d871214de/ue5_18-connect-event-tick-node.png "Connect the Event Tick node to the Set Replace Texture Flag for All Viewports node")
18.  **Compile** and **Save** the Blueprint.
    
19.  To see the changes in the **Preview Pane** of the nDisplay Blueprint, select the nDisplay Blueprint and go to the **Details** panel. Scroll down to the **Editor Preview** section and enable the **Replace Viewport Textures** and **Enable Editor Preview** checkboxes. This will show the ArUco markers.
    
    ![Select the nDisplay Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d1777e0-5699-4a41-a936-02adfd61e742/ue5_19-select-ndisplay-blueprint.png "Select the nDisplay Blueprint") ![Enable the Replace Viewport Textures and Enable Editor Preview checkboxes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ea76555-e3eb-493d-9b6a-783f1c2b9f1d/ue5_20-enable-replace-viewport-textures.png "Enable the Replace Viewport Textures and Enable Editor Preview checkboxes")
    
    Click image to expand.
    
20.  If you are using multiple render nodes, sync the project to the other computers now.
    
21.  In the **Outliner**, select the **nDisplay Blueprint** and go to the **Details** panel. Scroll down to the **Default** tab and enable the **Replace Viewport Textures** checkbox. The ArUco markers will now appear on the LED wall.
    
    ![Enable the Replace Viewport Textures checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b619ae9-dc07-4175-9ae6-3f97f2e87614/ue5_22-replace-viewport-textures-checkbox.png "Enable the Replace Viewport Textures checkbox")
    
    Click image to expand.
    
22.  To see the ArUco markers in the Editor Viewport, scroll down to the **Editor Preview** section and enable the **Enable Editor Preview** checkbox.
    
    ![Enable Editor Preview checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bdd9be45-22a1-48cc-b208-ed75544b66cb/ue5_24-enable-editor-preview.png "Enable Editor Preview checkbox")
    
    Click image to expand.
    
23.  To check the alignment of the LED wall, it is helpful to see the points at the corners of the ArUco markers.
    
    1.  Select a **Calibration Point** that was created when the ArUcos were added.
        
    2.  Go to the **Details** panel and scroll down to the **Calibration** section. Enable the **Visualize Points in Editor** checkbox.
        
    3.  The **Point Visualization Scale** adjusts the scale of the markers on the mesh. The **Visualization Shape** dropdown changes the marker shapes between **Cubes** and **Pyramids**. Adjust these values to suit your needs.
        
        ![Enable the Visualize Points in Editor checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f7e88f2-d946-48b5-af9e-a050b30f728b/ue5_26-visualize-points-editor-checkbox.png "Enable the Visualize Points in Editor checkbox")
24.  **Compile** and **Save** the Blueprint.
    
    ![You can now see the corner markers for each ArUco Marker](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2eae49bf-6685-4cd8-b8f5-8f004a6ea147/lwc-visualizepoints2.png)
25.  In the **Outliner** window, select the **nDisplay Blueprint** and go to the **Details** panel. Scroll down to the **Editor Preview section** and enable the **Enable Editor Preview** checkbox.
    
    This will allow the CG ArUcos to be displayed on the viewport mesh in the Lens file. Once the LED calibration is applied, the CG ArUcos will be overlaid on the live video feed from the camera that shows the ArUcos on the LED wall.
    
    ![Enable Editor Preview checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59feb4ea-97e9-4528-9ce3-d1c10fe962a6/ue5_32-enable-editor-preview.png)
26.  Place the tracked production camera and any other tracked objects under a **Tracking Node**. Parent the **Tracking Node** to the **nDisplay Blueprint**.
    

### Section Results

You generated the ArUco markers and are now ready to use them as part of your Lens file to calibrate your LED wall.

## 3 - Calibrating your LED wall with the ArUco markers

1.  In the **Content Browser**, double-click the **Lens File** that was created in the [Camera Calibration for Production](/documentation/en-us/unreal-engine/camera-lens-calibration-quick-start-for-unreal-engine) guide to open it. The Lens File should be attached to the camera under the LiveLinkController streaming the FIZ data.
    
    1.  Click the **Nodal Offset** tab.
        
        Click image to expand.
        
    2.  Go to the **Viewport Settings** and set the **Transparency** to **0**. This will turn off the CG overlay of the ArUco markers that are displayed in the Editor.
        
        ![Set the Transparency to 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2eb40f47-13bb-4ce2-87e5-256d4b4c96b4/ue5_30-set-transparency-0.png "Set the Transparency to 0")
    3.  Go to the **Nodal Offset** section and set the **Nodal Offset Algo** to **Nodal Offset ArUco markers**
        
    4.  Set the **Calibrator** to the **nDisplay Blueprint**.
        
    5.  Enable the **Show Detection** checkbox**.** This will capture an image each time the **Viewport** is clicked and will be used to gather calibration points of the ArUco Markers.
        
        ![Adjust the Nodal Offset settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e349a46-fe41-4791-a63e-1ef1cce108fc/ue5_31-nodal-offset-settings.png "Adjust the Nodal Offset settings")
2.  Point the production camera at the LED wall that is displaying the ArUcos markers. You will now collect images of the ArUco markers across the LED wall. Click the mouse inside the viewport to capture an image. A preview of the captured image will be displayed. Click the **OK** button.
    
    Click image to expand.
    
3.  Repeat the previous step multiple times to capture several images across the LED wall. You will see the captured images displayed under the **Nodal Offset** section.
    
4.  Once you have captured enough samples across the LED wall, click on **Apply to Camera Parent** button. This will offset the Tracking Origin previously created and the tracked production camera below it.
    
5.  To check the alignment of the LED wall, set the **Transparency** to **0.5.** This will show the CG ArUcos applied to the LED wall mesh overlaying the ArUcos on the physical LED wall. Both sets of ArUco markers should now be right on top of each other. If not, the virtual LED mesh does not match the physical LED mesh.
    

### Section Results

You calibrated your stage LED wall using the ArUco markers.
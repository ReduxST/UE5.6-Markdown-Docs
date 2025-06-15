# Audio Modulation Quick Start Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-modulation-quick-start-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-modulation-quick-start-guide)  
**Processed:** 2025-06-14 16:08:56

---

## Overview

The **Audio Modulation** system provides control over common floating-point audio parameters from the **Blueprint** and **Component** systems. The system includes a better, more intuitive and dynamic subset of features for mixing audio sources, and for dynamically controlling and parameterizing audio properties than Unreal Engine had in prior versions.

In this guide, you will learn how to build a basic volume-based **Control Bus** structure for your game audio.

## Goals

Use the **Audio Modulation Plugin** to build a basic volume-based Control Bus structure for your game audio.

## Objectives

-   Create a collection of Control Buses and Control Bus **Mix objects** to apply volume mixing to sound assets .
    
-   Assign Control Buses to **MetaSound Sources** and **Sound Classes**.
    
-   Use the **Mix Matrix Debugger** to see the current values of the Control Bus.
    
-   Adjust a Control Bus from Blueprints.
    

## 1 - Required Setup

1.  Create a new project and select the **Games** category and the **Third Person** template. Enter your project's location and name. Click **Create**.
    
    ![Create a new First Person project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf963468-bcef-4900-9582-c62fe43f25b1/audio-modulation-qs-1.png)
2.  Click **Settings > Plugins** to open the **Plugins** window.
    
    ![Open the Plugins window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acc9e918-2aa3-406b-b50d-310f2d4ec6a1/audio-modulation-qs-2.png)
3.  Search for and **enable** the **Audio Modulation** and **MetaSound** plugins. Restart Unreal Engine.
    
    ![Open the Plugins window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/048bb23c-f266-4f1b-8f4e-2dcac0323143/audio-modulation-qs-3.png)

### Section Results

In this section, you created a new project and enabled the Audio Modulation and MetaSound plugins. You are now ready to create the Control Buses.

## 2 - Create the Control Buses

1.  In the **Content Browser**, right click and select **Audio > Modulation > Control Bus**. Name the asset `CB_Main`.
    
    ![Name the asset CB_Main](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/781b70d6-041c-435f-8796-79be615ed890/audio-modulation-qs-5.png)
2.  Open `CB_Main` and click the **Parameter** dropdown. Click the **Gear** icon and enable the **Show Plugin Content** checkbox. You may have to select **Show Engine Content,** as the Modulation plugin is an Engine plugin.
    
    ![Click the Gear icon and enable the Show Plugin Content checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4aa97e5f-3b19-43ae-9c06-0853ee799ca6/audio-modulation-qs-6.png)
3.  Search for and select the **Volume** parameter.
    
    ![Search for and select the Volume parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8f9a881-0f3d-4b82-b03e-3210de150b82/audio-modulation-qs-7.png)
    
    You can create a custom parameter by right clicking in the Content Browser and selecting **Audio > Modulation > Modulation Parameter**. Then, select the SoundModulationParameterVolume class from the list.
    
4.  Create two folders in the **Content Browser** that will contain several Control Buses meant for designers and users. In the example below, the folders are named `Buses_Designer` and `Buses_User`.
    
    ![Create two folders in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4710f142-b03f-4608-965b-d65c7cd8f895/audio-modulation-qs-8.png)
5.  Right-click on `CB_Main` and select **Duplicate**. Name the new asset `CB_Ambience`.
    
    ![Right-click on CB_Main and select Duplicate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5b94f57-5b4b-4120-a516-5208818f3def/audio-modulation-qs-9.png)
6.  Repeat this process two more times and create `CB_Foley` and `CB_Footsteps`. Select all three assets and move them to the `Buses_Designer` folder.
    
    ![Repeat this process two more times and create CB_Foley and CB_Footsteps](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b59709b-b12c-46e9-84de-2407d1a6bd94/audio-modulation-qs-10.png)
7.  Repeat the previous step and create `CB_Dialogue`, `CB_Music`, and `CB_SFX`. Move them to the `Buses_User` folder.
    
    ![Repeat the previous step and create CB_Dialogue, CB_Music, and CB_SFX](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03530945-1c97-4f1a-af61-f15939fbed8e/audio-modulation-qs-11.png)

### Section Results

In this section, you created the main Control Bus that will modulate the volume for all assigned audio in your project. In addition, you created several Control Buses meant for the user and designer. You are now ready to assign the main Control Bus to the Master sound class in your project.

## 3 - Assign the Control Buses to Sound Assets

1.  Click **Settings > Project Settings** to open the **Project Settings**.
    
    ![Click Settings - Project Settings to open the Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfdd8448-7121-45ac-82db-49d850912680/audio-modulation-qs-12.png)
2.  Scroll down to the **Engine** section and select the **Audio** category. Go to the **Audio** section and double click the **Master Default Sound Class** to open it.
    
    ![Scroll down to the Engine section and select the Audio category](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77221f10-6b49-45de-bac5-773ec0b63b74/audio-modulation-qs-13.png) ![Double click the Master Default Sound Class to open it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3be1f096-4933-4b13-8f1e-e4dbd7b16668/audio-modulation-qs-14.png)
3.  In the **Details** panel, go to the **Modulation** section and enable the **Modulate** checkbox next to **Volume**.
    
    1.  Click **+** next to **Volume Modulators** and add `CB_Main` to **Index\[0\]**.
    
    ![Go to the Modulation section and enable the Modulate checkbox next to Volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46c6e0cb-9a4a-4abc-990c-8c44b17e2759/audio-modulation-qs-15.png) ![Click + next to Volume Modulators and add CB_Main to Index[0]](audio-modulation-qs-16.png)
    
    Add the `CB_Main` Control Bus to any additional sound classes in your project, so all sounds are mixed using the same Control Bus. The Sound Class reference hierarchy is not observed by modulation and the mix structure. Each Sound Class must list all Control Buses that are to be applied to Sound Assets referencing said Sound Class.
    

### Section Results

In this section, you assigned the `CB_Main` Control Bus to the Master sound class. You are now ready to create a sample MetaSound to test the mix during gameplay.

## 4 - Create a Sample MetaSound

1.  In the **Content Browser**, right-click and select **Audio > MetaSound Source**. Name the asset `MS_Sample`.
    
    ![Name the asset MS_Sample](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5957e8ce-5abe-408b-9ba6-e8f9ebe4be4f/audio-modulation-qs-18.png)
2.  Open `MS_Sample` by double-clicking it in the **Content Browser**.
    
    1.  Go to the **Interfaces** panel on the left and click the **remove** icon next to **UE.Source.OneShot** to remove it.
        
    2.  Right-click in the **Event Graph** and search for then select **Wave Player (Mono)**.
        
    3.  Connect the **Input** node to the **Play** pin of the **Wave Player** node.
        
    4.  Connect the **Out Mono** pin of the **Wave Player** node to the **Output** node.
        
    
    ![Click the remove icon next to UE.Source.OneShot)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/494bbf6d-60ac-4b67-af87-6500de079192/audio-modulation-qs-19a.png) ![Right-click in the Event Graph and search for then select Wave Player (Mono)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4ad87dd-0ff3-402e-84db-ef687b750528/audio-modulation-qs-19.png) ![Connect the Out Mono pin of the Wave Player node to the Output node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/adf2d066-54fc-47e4-854e-bbb9629d3039/audio-modulation-qs-20.png)
3.  Click the **Wave Asset** dropdown and select a sound asset. In this example, **EndPlayInEditor** was selected.
    
    1.  Enable the **Loop** checkbox.
    
    ![Click the Wave Asset dropdown and select a sound asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09f14adb-5dea-4a8a-b417-fc7159fda3cf/audio-modulation-qs-21.png)
4.  Click **Source** on the toolbar and scroll down to the **Details** panel.
    
    1.  Expand the **Modulation** category.
        
    2.  Click the **Volume Routing** dropdown and select **Union**.
        
    3.  Enable the **Modulate** checkbox next to **Volume**.
        
    4.  Click **+** next to **Volume Modulators** and add `CB_SFX` to **Index\[0\]**.
        
    
    ![Click Source on the toolbar and scroll down to the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e50cc2b-f053-4794-9bcc-b949c8267d24/audio-modulation-qs-22.png) ![Click the Volume Routing dropdown and select Union](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb7be63e-1653-495a-9e7e-348f9a68eee3/audio-modulation-qs-23.png) ![Click + next to Volume Modulators and add CB_SFX to Index[0]](audio-modulation-qs-24.png)
5.  Drag `MS_Sample` to your level.
    
    ![Drag MS_Sample to your level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7ce7748-d0d8-4ca5-86cc-abe4d243b8b5/audio-modulation-qs-25.png)

### Section Results

In this section, you create a simple MetaSound that will play a sound asset continuously. You are now ready to apply the Control Bus Mix to the Control Buses.

## 5 - Apply a Mix

In this section, you will create a **Control Bus Mix** and apply it to all **Control Buses** in the `Buses_User` folder. You can follow these steps to create a Control Bus Mix for all Control Buses in the `Buses_Designer` folder as well. In addition, there is no strict rule as to what can be included in a mix.

Multiple mixes can be activated and applied to a single or group of Control Buses. However, only a single instance of a given mix can be active at a time.

1.  In the **Content Browser**, right-click and select **Audio > Modulation > Control Bus Mix**. Name the asset `CM_User`.
    
    ![Name the asset CM_User](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d49c4d0e-3a7c-401d-b32c-d04dec8d76ac/audio-modulation-qs-27.png)
2.  Open CM\_User and go to the Mix Stages section.
    
    1.  Click **+** next to **Mix Stages** to add a new mix.
        
    2.  Click the **Bus** dropdown and select `CB_Dialogue`.
        
    
    ![Click the Bus dropdown and select CB_Dialogue](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25ecbcd7-6b31-45e6-b9ef-fe293d58d685/audio-modulation-qs-28.png)
3.  Repeat the previous step and add `CB_Music` and `CB_SFX` to the **Mix Stages**.
    
    ![Repeat the previous step and add CB_Music and CB_SFX to the Mix Stages](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42b38c85-41ef-4113-b606-6639b6ee3546/audio-modulation-qs-29.png)
4.  Press **Play** to enter runtime.
    
    1.  Press **Shift-F1** to regain control of your mouse.
        
    2.  Go to `CM_User` and click **Activate Mix**.
        
    3.  Change the value of `CB_SFX` to see the changes applied in real time.
        
    
    ![Go to CM_User and click Activate Mix](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2290a76-c261-4e32-b11f-6a34afb92bee/audio-modulation-qs-30.png) ![Change the value of CB_SFX to see the changes applied in real time](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd2219d2-f587-4aae-a610-59498a1610fb/audio-modulation-qs-31.png)

### Section Results

In this section, you created and applied the `CM_User` **Control Mix** to the Control Buses in your project. You also activated the mix during gameplay and changed the volume of sounds using the `CB_SFX` Control Bus.

## 6 - Debug a Mix

1.  During gameplay, press **~** to open the **console** window.
    
    1.  Enter the following command: `au.Debug.Modulation.Enable.Matrix 1` to enable Sound Modulation debugging.
    
    ![Enter the following command: au.Debug.Modulation.Enable.Matrix 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24e0e68d-fe48-4a4e-9043-a23e0ff44412/audio-modulation-qs-32.png)
2.  You can filter the list of Control Buses and Control Mixes displayed by entering the commands: `au.Debug.Modulation.Filter.Buses [substring]` and `au.Debug.Modulation.Filter.Mixes [substring]`.
    
    ![You can filter the list of Control Buses and Control Mixes displayed by entering the appropriate commands](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3c32b9f-6b7a-4505-8418-bcdfef3b5041/audio-modulation-qs-33.png) ![The Bus Mix Matrix is showing CB_SFX](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/662c03b4-f8f0-4435-ac08-bac4f42660fa/audio-modulation-qs-34.png)

### Section Results

In this section, you activated the Sound Modulation debugger and filtered the matrix to only show the `CB_SFX` Control Bus.

## 7 - Adjust Control Buses from Blueprints

In this section, you will activate a Control Mix from Blueprints at runtime.

1.  Click the **Blueprint** button in the **Level Editor** toolbar and select **Open Level Blueprint**.
    
    ![Select Open Level Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52c7c98f-7d6d-4b71-ab3b-80d615a42100/audio-modulation-qs-35.png)
2.  In the **Event Graph**, right-click and search for then select **Event Begin Play**.
    
    ![Right-click and search for then select Event Begin Play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c247e42-a312-405e-aacb-673529096c83/audio-modulation-qs-36.png)
3.  Drag from the **Event Begin Play** node and search for then select **Activate Control Bus Mix**.
    
    1.  Click the **Mix** dropdown and select `CM_User`.
    
    ![Drag from the Event Begin Play node and search for then select Activate Control Bus Mix](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58b3eb8b-aa4e-4aa9-94d6-1ff581bd2536/audio-modulation-qs-37.png)
4.  Drag from the **Activate Control Bus Mix** node and search for then select **Delay**.
    
    1.  Set the **Duration** to **3.0**.
    
    ![Drag from the Activate Control Bus Mix node and search for then select Delay](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f700fbc6-66c5-45c8-aa75-2777004bd048/audio-modulation-qs-38.png)
5.  Drag from the **Delay** node and search for then select **Set Control Bus Mix By Filter**.
    
    1.  Click the **Mix** dropdown and select `CM_User`.
        
    2.  Add `CB_SFX` to the **Address Filter**.
        
    3.  Enter a **Value** of **0.25**.
        
    
    ![Drag from the Delay node and search for then select Set Control Bus Mix By Filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/200b3998-22c0-4a4b-afbb-75c51e4406de/audio-modulation-qs-39.png)
6.  Press **Play** and verify that the `CM_User` **Control Bus** is activated and the volume of `MS_Sample` is lowered after 3 seconds.
    

### Section Results

In this section, you activated the `CM_User` Control Bus and changed the volume of audio using the `CB_SFX` Control Bus.
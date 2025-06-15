# Setting Up a New AR Project

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-new-ar-project-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-new-ar-project-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:03

---

This guide shows how to create a new empty project in Unreal Engine and add the necessary Blueprints and configurations to turn it into an AR experience.

If you want to start with an AR project that is set up already, see the following AR templates:

-   [Handheld AR Template for iOS and Android](/documentation/en-us/unreal-engine/handheld-ar-template-quickstart-in-unreal-engine)

## Setting Up a Blank Project

Follow these steps to create a new Unreal Engine project and level with minimal rendering features enabled. Blank projects open with the default level, which includes a Sky Sphere and Atmosphere Fog objects. These objects will persistently overlay everything in AR, so it's useful to start with an empty level when creating an AR experience to control what will be displayed.

1.  Launch **Unreal Engine** from the [Epic Games Launcher](https://www.epicgames.com/store/en-US/download).
    
2.  In the **Unreal Project Browser** window, choose **Games** .
    
    Click image to expand.
    
3.  Select the **Blank Template**.
    
    Click image to expand.
    
4.  For the **Project Defaults**, choose the following:
    
    -   Blueprint
        
    -   Scalable
        
    -   Raytracing Disabled
        
    -   Mobile
        
    -   No Start Content
        
        Click image to expand.
        
    -   From the Editor Choose **File > New Level…** and choose **Empty Level**. Make sure to name and save your level. In this example, the level is named **Main**.
        
        ![Adding an empty level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f8f3280-1879-4854-b4c3-0429c4d9be4e/04-select-empty-level_ue5.png)
    -   In the main navigation, choose **Edit > Project Settings**.
        
    -   In the Project Settings window, select **Maps & Modes** under the **Project** section. Set the **Editor Startup Map** and the **Game Default Map** to the new level **Main**.
        
        Click image to expand.
        

## Adding a Pawn and Game Mode

In Unreal Engine, a [pawn](/documentation/en-us/unreal-engine/pawn-in-unreal-engine) is the physical representation of the user and defines how the user interacts with the world. The [Game Mode](/documentation/en-us/unreal-engine/game-mode-and-game-state-in-unreal-engine) object defines the rules of the experience, such as which pawn object to use. In order to build a new AR project, you need to set up the pawn so you can interact with the environment when you run your app.

Follow the steps below to create a Pawn and Game Mode for your AR project.

1.  Right-click in the **Content Drawer** and choose Blueprint Class from the list. In the **Pick Parent Class** window, select **Pawn**. Name the asset **ARPawn**.
    
    ![Create Blueprint class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/374c351e-a711-400a-ba5d-d3bc1dec3bad/06-create-blueprint-class_ue5.png) ![Pick Parent class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4288e548-1d92-478d-abd4-bbf7a0236a29/07-actor-parent-class_ue5.png)
2.  Double-click the **ARPawn** object in the **Content Drawer** to open it in the **Blueprint Editor**. In the Blueprint Editor, choose **Add Component** and search for **Camera**.
    
    ![Adding camera component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/233577d5-bb2a-405a-8301-d2ac5b5209b2/08-add-new-component_ue5.png)
3.  Make sure the **Camera** component's parent is **DefaultSceneRoot**.
    
    ![Camera default scene root](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d0fc6ed-42db-4091-978c-688a347103dc/09-camera-component_ue5.png)
4.  Right-click in the **Content Drawer** and choose **Blueprint Class** from the list. In the **Pick Parent Class** window, select **Game Mode Base**. Name the asset **ARGameMode**.
    
    ![Add game mode class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3a1c185-6339-4720-9c75-a9feade56d9b/10-game-mode-base-class_ue5.png)
5.  Double-click **ARGameMode** to edit the settings. Set **Default Pawn Class** to **ARPawn**.
    
    Click image to expand.
    
6.  In the main navigation, choose **Edit > Project Settings** to open the **Project Settings** window.
    
7.  In the **Project Settings** window under the **Project** section on the left, select **Maps & Modes**.
    
    1.  Set **Default GameMode** to **ARGameMode**
        
    2.  Set **Default Pawn Class** to **ARPawn**.
        
    
    Click image to expand.
    

## Creating an AR Session

The function **Start AR Session** requires an ARSessionConfig object, which defines all the AR-specific capabilities for the project. See [UARSessionConfig](/documentation/en-us/unreal-engine/API/Runtime/AugmentedReality/UARSessionConfig) for more information on what each setting is.

Follow the steps below to add the AR session logic to your project.

1.  Right-click in the **Content Drawer**. Choose **Miscellaneous > Data Asset** to open the **Pick Data Asset Class** window.
    
    ![Adding a data asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dcd7c52d-e7d5-4a9f-ad06-c51ec400e346/13-create-data-asset_ue5.png)
2.  In the **Pick Data Asset Class** window, choose **ARSessionConfig**. Name the data asset **ARSessionConfig**. Open the asset and select **Save** to confirm the default AR options.
    
    ![Opening AR session config](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06486238-35d0-4408-8670-547ddc5cdf07/14-ar-session-config_ue5.png)
3.  Double-click the **ARPawn** asset to open it in the **Blueprint Editor**. Add the function **Set Tracking Origin**. Set the **Origin value** to **Floor Level**.
    
    ![Blueprint set tracking origing to floor level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d3fd30c-f200-4399-bbc7-c769824fdffb/15-origin-floor-level_ue5.png)
4.  Add the function **Start AR Session**. Set **Session Config** asset to **ARSessionConfig**.
    
    ![Blueprint adding start AR session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/129b4c62-abea-451e-b083-fd47255becad/16-session-config-ar-session_ue5.png)
5.  Add the function **Stop AR Session**.
    
    ![Blueprint adding stop AR session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/271e7c50-106d-4302-b188-9a5f56d9fdb8/17-stop-ar-session_ue5.png)

When you launch your project on your device, you will now be able to navigate your AR environment. See the documentation for your AR platform for detailed steps on how to launch your Unreal project on your device.

## Step 4 - On Your Own

In this guide, you learned how to create a new AR project, and add the necessary Blueprints to get started building an AR app.
# Setting up your Project

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-your-project-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-your-project-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:09

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac94fbbe-93c6-4bba-a466-dec53cab5a26/22-fps-settingup-section-result.png)

This is what you will see at the end of this section.

## Goals

The purpose of this section is to show you how to set up your First Person Shooter project.

## Objectives

By the end of this section of the tutorial, you will be able to:

-   Set Up a New Project
-   Set the Editor Startup Map
-   Open Your Project in Visual Studio
-   Add Log Messaging to Your Project
-   Compile Your First C++ Class
-   Set the Default Game Mode

## Steps

-   1.1 - Project Setup
-   1.2 - Opening the Project in Visual Studio
-   1.3 - Adding Log Messaging
-   1.4 - Compiling the Project
-   1.5 - Setting the Default Game Mode
-   1.6 - Section One Summary

## 1.1 - Project Setup

During this step, you are going to create a starting point for our First Person Shooter (FPS) game by using the Unreal Engine.

1.  Open **Unreal Engine** from the Epic Launcher and [create a New Project](/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine).
    
2.  Select the **Games** project category.
    
3.  Select the **Blank** template.
    
4.  Select the **C++** project type (instead of **Blueprint**).
    
5.  Disable the **Starter Content**.
    
6.  Name your project **FPSProject**.
    
7.  After you have named your project, go ahead and click the **Create** button. Project should automatically open in the Unreal Editor.
    
    Click image to expand.
    
    Some of the code samples in this tutorial will need to be updated if you name your project differently.
    
8.  Navigate to the **Content Browser** and go to the **Engine > Content > Maps > Templates**, double-click the **Template\_Default** Level to open this.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4265da7-34e0-41da-bc8f-a6abc538cc3f/02-fps-settingup-open-default-level.png)
9.  Click the **Play** button in the **Level Editor Toolbar** to start **Play in Editor** (PIE) mode.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04c0b29a-61a2-43ec-b216-8f071fe43c54/03-fps-settingup-play-button.png)
    
    Use the WASD keys to move around the Level while using your mouse to aim the camera.
    
10.  Press the **Shift + Escape** or click **Stop** in the **Level Editor Toolbar** to exit PIE mode.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4362da6c-08d7-4844-9ae5-c250959ab0fd/04-fps-settingup-stop-button.png)
11.  Now that you are done exploring the Level, navigate to the **Content Browser** and create a **Maps** folder under the **Content** folder (Select the **Content** folder, right-click in the file window of the **Content Browser**, and select **New Folder**).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03e7c3a9-677e-4a76-8de3-cf4c1b9f11ed/05-fps-settingup-maps-folder.png)
12.  Click the **File** in the **Main** menu panel, select **Save Current Level as...**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab3608ad-88e8-4ad9-9d35-fdd2e53084bb/06-fps-settingup-save-level-as.png)
13.  Select the **Maps** folder in the **Save Level As** window, name your new map **FPSMap** and click **Save**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bdd80bd4-6776-4499-9622-d77f8c382d63/07-fps-settingup-save-level-settings.png)
14.  Click the **Edit** in the **Main** menu panel and select **Project Settings**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7b9ee64-6dff-43c9-986b-b403a935c2fe/08-fps-settingup-open-project-settings.png)
15.  Navigate to the **Project** section on the left side of the **Project Settings** tab, click on **Maps & Modes**. Expand the **Editor Startup Map** dropdown menu, and select **FPSMap**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c79579c3-c6c1-4768-bc2d-bc223779a1cf/09-fps-settingup-editor-default-map.png)
    
    With this setings, the Editor will automatically load FPSMap as the default map.
    
16.  Finally, close the **Project Settings** menu and save your project before moving onto the next step.
    

## 1.2 - Opening the Project in Visual Studio

When you set up your **Basic Code** project in the previous step, Unreal Engine created a **Game Mode** for you. Game Modes define a game's rules and win conditions. The Game Mode also sets default classes that will be used for some basic gameplay framework types, including Pawn, PlayerController, and HUD. During this section, you are going to use the Editor to open your project as a solution in **Visual Studio** so that you can view your project's Game Mode class.

1.  Click the **Tools** in the **Main** menu panel and select **Open Visual Studio** to open your C++ code in Visual Studio.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c722bc2a-d21c-417f-a80c-42919967055e/10-fps-settingup-tools-menu-open-vs.png)
2.  After Visual Studio launches your project, you should see the `.cpp` and `.h` files inside of Visual Studio's **Solution Explorer**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e51795fd-f878-4fe4-bf5e-495b8fd614da/11-fps-settingup-vs-solution-explorer.png)
    
    Do not be alarmed if Visual Studio in the example images looks a little different than yours, in this examples Dark Mode are used. You can enable this by going to: **Tools > Options > Environment > General > Color Theme**.
    
3.  Expand **Source** and then **FPSProject** to view the main files for your new game.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9a88789-38b7-4a3d-be85-adb06d2422f3/12-fps-settingup-vs-expand-source.png)
4.  Open `FPSProjectGameModeBase.cpp`. It should look like the following:
    
    FPSProjectGameModeBase.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.           #include "FPSProjectGameModeBase.h"`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSProjectGameModeBase.h"
5.  Now open `FPSProjectGameModeBase.h`. It should look like the following:
    
    FPSProjectGameModeBase.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.               #pragma once               #include "CoreMinimal.h"     #include "GameFramework/GameModeBase.h"     #include "FPSProjectGameModeBase.generated.h"               /**      *       */     UCLASS()     class FPSPROJECT_API AFPSProjectGameModeBase : public AGameModeBase     {         GENERATED_BODY()     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/GameModeBase.h" #include "FPSProjectGameModeBase.generated.h" /\*\* \* \*/ UCLASS() class FPSPROJECT\_API AFPSProjectGameModeBase : public AGameModeBase { GENERATED\_BODY() };
6.  Now that you have opened your C++ project in Visual Studio, you are ready to start adding code to the project.
    

## 1.3 - Adding Log Messaging

A great way to start adding code to your project is by adding a log message to **FPSGameMode**. Log messages are really useful for verifying and debugging code during development. During this step, you will use a log message to verify that you are actually using **FPSGameMode** rather than the default Game Mode provided by Unreal Engine.

### FPSProjectGameMode Header File

1.  In the **Solution Explorer**, go to **FPSProject > Source > FPSProject**.
    
2.  Double-click `FPSProjectGameModeBase.h` to open the header file for your **FPSGameMode** class.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a25542c0-a052-45fd-850e-bcce99713f51/13-fps-settingup-header-file.png)
3.  Your class declaration should look like the following:
    
    FPSProjectGameModeBase.h
    
    ```
        `UCLASS()     class FPSPROJECT_API AFPSProjectGameModeBase : public AGameModeBase     {         GENERATED_BODY()              };`
    Copy full snippet
    ```
    UCLASS() class FPSPROJECT\_API AFPSProjectGameModeBase : public AGameModeBase { GENERATED\_BODY() };
4.  Add the following function declaration under the `AFPSProjectGameMode` constructor declaration:
    
    FPSProjectGameModeBase.h
    
    ```
       `virtual void StartPlay() override;`
    Copy full snippet
    ```
    virtual void StartPlay() override;  
    
    This function declaration allows you to override [StartPlay](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AGameModeBase/StartPlay) so that you can print a log message to the screen when gameplay begins.
    
5.  `FPSProjectGameMode.h` should now look like the following:
    
    FPSProjectGameModeBase.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.           #pragma once           #include "CoreMinimal.h"     #include "GameFramework/GameModeBase.h"     #include "FPSProjectGameModeBase.generated.h"           /**      *       */     UCLASS()     class FPSPROJECT_API AFPSProjectGameModeBase : public AGameModeBase     {         GENERATED_BODY() 		          virtual void StartPlay() override;     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/GameModeBase.h" #include "FPSProjectGameModeBase.generated.h" /\*\* \* \*/ UCLASS() class FPSPROJECT\_API AFPSProjectGameModeBase : public AGameModeBase { GENERATED\_BODY() virtual void StartPlay() override; };
6.  Save your `FPSProjectGameMode.h` header file in Visual Studio.
    

### FPSProjectGameMode CPP File

1.  In the **Solution Explorer**, go to **FPSProject > Source > FPSProject**.
    
2.  Double-click `FPSProjectGameModeBase.cpp` to open the implementation file for your **FPSGameModeBase** class.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5893e461-1fc3-472f-9825-0c4700f3f655/14-fps-settingup-cpp-file.png)
3.  Now add the following lines of code to the file:
    
    FPSProjectGameModeBase.cpp
    
    ```
        `void AFPSProjectGameModeBase::StartPlay()     {         Super::StartPlay(); 	          check(GEngine != nullptr); 		         // Display a debug message for five seconds.          // The -1 "Key" value argument prevents the message from being updated or refreshed.         GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Hello World, this is FPSGameMode!"));     }`
    Copy full snippet
    ```
    void AFPSProjectGameModeBase::StartPlay() { Super::StartPlay(); check(GEngine != nullptr); // Display a debug message for five seconds. // The -1 "Key" value argument prevents the message from being updated or refreshed. GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Hello World, this is FPSGameMode!")); }
    
    `StartPlay()` will print a new debug message ("Hello World, this is FPSGameModeBase!") to the screen in yellow text for five seconds when gameplay begins.
    
4.  `FPSProjectGameModeBase.cpp` should now look like the following:
    
    FPSProjectGameModeBase.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.        #include "FPSProjectGameMode.h"       void AFPSProjectGameModeBase::StartPlay()     {         Super::StartPlay(); 	          check(GEngine != nullptr); 		         // Display a debug message for five seconds.          // The -1 "Key" value argument prevents the message from being updated or refreshed.         GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Hello World, this is FPSGameModeBase!"));     }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSProjectGameMode.h" void AFPSProjectGameModeBase::StartPlay() { Super::StartPlay(); check(GEngine != nullptr); // Display a debug message for five seconds. // The -1 "Key" value argument prevents the message from being updated or refreshed. GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Hello World, this is FPSGameModeBase!")); }
5.  Save your `FPSProjectGameModeBase.cpp` implementation file in Visual Studio.
    

## 1.4 - Compiling the Project

Now is a good time to compile your project so that you can see your code changes reflected in-game.

1.  Going back to the Editor, click the **Compile** button to compile your code.
    
    Since you started developing your project as a C++ project, you are able to compile your C++ code directly from Unreal Editor. Click for full image.
    
2.  Click the **Play** button in the **Level Editor Toolbar** to start Play in Editor (PIE) mode.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60f279cc-52b3-4128-83b4-6059289d35a3/16-fps-settingup-pie-game-mode.png)
    
    You might be wondering why your log message is not being displayed on screen when you are in PIE mode. The reason you are not seeing your log message is because the Editor is still using the default Game Mode at this stage in development.
    
3.  Press the **Shift + Escape** or click **Stop** in the **Level Editor Toolbar** to exit PIE mode..
    

### Extending your C++ Game Mode Class to Blueprints

Now is a good time to extend the C++ Game Mode class to Blueprints. Please feel free to go to the [C++ and Blueprints](/documentation/en-us/unreal-engine/cpp-and-blueprints-example) reference page to learn more about extending C++ classes to Blueprints.

1.  Create a **Blueprints** folder inside of the **Content** folder.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e28d9612-6fda-403d-8924-8f0a8af503e9/17-fps-settingup-blueprints-folder.png)
2.  Right-click the **FPSProjectGameModeBase** class (in **C++ Classes > FPSProject**) to open the **C++ Class Actions** menu.
    
3.  Click **Create Blueprint class based on FPSProjectGameModeBase** to open the **Add Blueprint Class** dialog menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ca69a09-1271-4abe-b95e-c5b5ba3bcdd8/18-fps-settingup-create-derived-bp-class.png)
4.  Name your new Blueprint Class **BP\_FPSProjectGameModeBase** and choose the **Blueprints** folder, click the **Create Blueprint Class** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe45babb-381f-4396-a7f9-b29ae0668bb2/19-fps-settingup-add-bp-class.png)
5.  As a result, you should have a newly created **BP\_FPSProjectGameModeBase** Blueprint Class located inside of the **Blueprints** folder.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0b9c0e9-5be4-4b9f-9f0c-a7c1acf03604/20-fps-settingup-created-bp-class.png)
6.  Make sure to save your **BP\_FPSProjectGameModeBase** Blueprint before closing the **Blueprint Editor**.
    

## 1.5 - Setting the Default Game Mode

Now that you have successfully extended your newly modified Game Mode to Blueprints, you will need to set your project to use **BP\_FPSProjectGameModeBase** as the default **Game Mode** in this step.

1.  Click the **Edit** in the **Main** menu panel and select **Project Settings**.
    
2.  Navigate to the **Project** section on the left side of the **Project Settings** tab, click on **Maps & Modes**. Expand the **Default GameMode** dropdown menu, and select **BP\_FPSGameModeBase**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f55f7fb6-cb96-41f4-a07a-1b150bb90b7d/21-fps-settingup-setting-default-gamemode.png)
3.  Close the **Project Settings** menu.
    
4.  Click the **Play** button in the **Level Editor Toolbar**. "Hello World, this is FPSGameMode!" should now be displayed in yellow text for five seconds in the upper left hand corner of your viewport.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/791657e6-b9c9-43f6-88f7-1cc86ed3bff8/22-fps-settingup-section-result.png)
5.  Press the **Shift + Escape** or click **Stop** in the **Level Editor Toolbar** to exit PIE mode.
    

## 1.6 Section One Summary

FPSProjectGameModeBase.h

```
`// Copyright Epic Games, Inc. All Rights Reserved.   #pragma once   #include "CoreMinimal.h" #include "GameFramework/GameModeBase.h" #include "FPSProjectGameModeBase.generated.h"   /**  *   */ UCLASS() class FPSPROJECT_API AFPSProjectGameModeBase : public AGameModeBase {     GENERATED_BODY()       virtual void StartPlay() override; };`
Copy full snippet
```
// Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/GameModeBase.h" #include "FPSProjectGameModeBase.generated.h" /\*\* \* \*/ UCLASS() class FPSPROJECT\_API AFPSProjectGameModeBase : public AGameModeBase { GENERATED\_BODY() virtual void StartPlay() override; };

FPSProjectGameModeBase.cpp

```
`// Copyright Epic Games, Inc. All Rights Reserved.            #include "FPSProjectGameMode.h"   void AFPSProjectGameMode::StartPlay() {     Super::StartPlay();       checkGEngine != nullptr);            // Display a debug message for five seconds.        // The -1 "Key" value argument prevents the message from being updated or refreshed.       GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Hello World, this is FPSGameModeBase!")); }`
Copy full snippet
```
// Copyright Epic Games, Inc. All Rights Reserved. #include "FPSProjectGameMode.h" void AFPSProjectGameMode::StartPlay() { Super::StartPlay(); checkGEngine != nullptr); // Display a debug message for five seconds. // The -1 "Key" value argument prevents the message from being updated or refreshed. GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Yellow, TEXT("Hello World, this is FPSGameModeBase!")); }

Congratulations! You've learned how to:

✓ Set up a New Project  
✓ Open your Project in Visual Studio  
✓ Add Log Messaging to your Project  
✓ Compile your First C++ Class  
✓ Set the Default Game Mode

You're now ready to learn how to implement your character in the next section.
# Building Unreal Engine from Source

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/building-unreal-engine-from-source](https://dev.epicgames.com/documentation/en-us/unreal-engine/building-unreal-engine-from-source)  
**Processed:** 2025-06-14 16:11:38

---

Windows macOS Linux

## Building Unreal Engine from Source

Read about [](/documentation/404), and make sure that **Microsoft Visual Studio** is installed prior to building **Unreal Engine (UE)** from source. Also, depending on your system's specifications, it may take between 10 and 40 minutes to compile the Engine.

1.  Inside the root directory, where you [downloaded and adjusted the UE Source Code](/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine#downloadingthesourcecode) run `GenerateProjectFiles.bat` to set-up your project files.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc1490a3-9467-4668-8b33-1a2d771928eb/01_generateprojectfiles.png)
    
    All project files are intermediate (`[UERoot]\Engine\Intermediate\ProjectFiles`). You must generate project files each time you sync a new build to ensure they are up to date. If you delete your `Intermediate` folder, you must regenerate project files using the `GenerateProjectFiles` batch file.
    
2.  Load the project into Visual Studio by double-clicking `UE5.sln`.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f059211-12b7-4b26-9b15-9b4a3043556b/02_launchue5vs.png)
3.  Set your solution configuration to **Development Editor**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4a8bbcb-a479-4401-890f-3fa94f465c22/03_solutionconfig.png)
4.  Set your solution platform to **Win64**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2ac340b-117f-4e2c-8327-677796987bae/04_solutionplatform.png)
5.  Right-click the **UE5** target and select **Build**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58494b6c-b8fd-4bd6-bb80-afa3bae1563e/05_buildue.png)

Read about [](/documentation/404), and make sure that **XCode** is installed prior to building **Unreal Engine (UE)** from source. Also, depending on your system's specifications, it may take between 10 and 40 minutes to compile the Engine.

1.  Inside the root directory, run `GenerateProjectFiles.command` to set up your project files.
    
2.  Load the project into XCode by double-clicking `UE5.xcodeproj`.
    
3.  To set your build target, select **UnrealEditor - Mac** for **My Mac** in the title bar.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b083a3cc-306b-4393-b012-6765f1391b4e/settingmactarget.png)
4.  To build the project, select **Product > Build**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11757f83-cb36-4ccb-bcf8-f6bd9c679a29/buildingmaceditor.png)

**Unreal Engine (UE)** development and support teams currently use the latest version of **Ubuntu**; as a result, we may not be able to provide support for other Linux distributions (including other versions of Ubuntu). Additionally, read about [](/documentation/404), and make sure your system has at least one hundred (100) gigabytes of disk space before performing the following steps.

1.  Inside the root directory, run `Setup.sh` from the terminal to setup the files needed to generate the project files.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86b4caef-ec58-407a-b07b-47b88651f23e/runsetupshellscript_linux.png)
2.  Now, run `GenerateProjectFiles.sh` from the terminal to generate your project files.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cacfc3b6-ec4d-4ec4-872a-8628ce28fed0/rungenprjfilesshellscript_linux.png)
3.  To build the project, run **make** from the terminal.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88b8325b-5661-44a2-a24e-2117732e0e94/runmakefile_linux.png)

Depending on your system's specifications, it may take anywhere from ten minutes to over an hour to compile the Engine. If you want to shorten the time it takes to compile the Engine from source, we recommend compiling the source code on a machine that has at least eight (8) gigabytes of RAM, with a multi-core processor having at least eight (8) cores (including hyperthreading).

## Running the Editor

1.  Set your startup project by right-clicking the **UE5** target and selecting **Set as StartUp Project**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1aea8a2f-0e58-4091-9cfb-dd9b687d7100/06_setstartupproj.png)
2.  Right-click the **UE5** project, then select **Debug > Start New Instance** to launch the Editor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fb6382a-2f95-4cbc-8606-4ce06a14d4ef/07_startnewinstance.png)
    
    Alternatively, you can **press the F5 key** on your keyboard to start a new instance of the Editor.
    
3.  Congratulations! You've compiled and launched the Engine from source.
    

1.  Select **Product > Run** to launch the Editor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81d9071b-06ab-40c4-9040-0a24367d26c9/runningmaceditor.png)
2.  Congratulations! You've compiled and launched the Engine from source.
    

1.  Navigate to the Editor's binary path by entering `cd Engine/Binaries/Linux/` into the terminal.
    
2.  Run **UnrealEditor** to launch the editor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5d86e81-34ff-49e2-aa83-f82e4808829f/runue4editor_linux.png)
3.  Congratulations! You've compiled and launched the Engine from source.
    

## Getting Started with Unreal Engine

Learn how to use Unreal Engine by referring to the [Understanding the Basics](/documentation/en-us/unreal-engine/understanding-the-basics-of-unreal-engine) documentation!

If you're looking to quickly get started with UE, refer to the following tutorials:

-   [Programming Quick Start](/documentation/en-us/unreal-engine/unreal-engine-cpp-quick-start)
-   [Level Designer Quick Start](/documentation/en-us/unreal-engine/level-designer-quick-start-in-unreal-engine)

UE's in-editor help features are a great way to get your questions answered.
# Creating a New Project

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine)  
**Processed:** 2025-06-14 16:16:57

---

When you launch **Unreal Engine**, the **Unreal Project Browser** opens automatically. This is where you can:

-   Create a new project.
    
-   Open an existing project.
    
-   Manage existing projects.
    

The diagram below illustrates the steps to create a new project in Unreal Engine.

![Creating a new project in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70b8eb57-6f94-4214-aec5-93178378c19d/creating-new-project.png)

Creating a new project in Unreal Engine from the Project Browser window.

To create a new project, follow these steps:

1.  Select the **development category** (1) that best matches your industry and project goals.
    
    You can select from the following categories:
    
    -   Games
    -   Film, Television, and Live Events
    -   Architecture, Engineering, and Construction (AEC)
    -   Automotive, Product Design, and Manufacturing (APM)
2.  Select a **template** (2) for your project. The templates you can choose from are based on the category you selected in step 1.
    
    Unreal Engine contains a number of **project templates** you can use as a starting point for your own projects. To learn more about the different project templates available, refer to the [Templates Reference](/documentation/en-us/unreal-engine/unreal-engine-templates-reference) page.
    
3.  Configure the **Project Defaults** (3). In this section, you can select your target platform (that is, the hardware where your game or application will run, like a computer or a mobile device), configure quality and ray tracing settings, and more.
    
    Some of the settings below may not be available for certain templates. For example, the Handheld AR template can only use Blueprint implementation.
    
    You can configure the following settings:
    
    | Setting | Description |
    | --- | --- |
    | **Implementation** | 
    Select how you want to implement your project's logic, such as character movement, level transitions, and so on.
    
    You can choose from the following options:
    
    -   **Blueprint**, if you want to build your project in the Unreal Editor, and use the Blueprint Visual Scripting system to create interactions and behavior.
        
    -   **C++**, if you want to build your project by programming with C++ in Visual Studio.
        
    
    For more information about these implementation methods, refer to the following pages:
    
    -   [Blueprint Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine)
    -   [Programming with C++](/documentation/en-us/unreal-engine/programming-with-cpp-in-unreal-engine)
    
    
    
     |
    | **Target Platform** | 
    
    Select the kind of platform your project is intended for:
    
    -   **Desktop**
    -   **Mobile**
    
    
    
     |
    | **Quality Preset** | 
    
    Select the maximum quality level, based on which platform your project targets. We recommend that you choose:
    
    -   **Maximum**, if you are developing your project for a computer or game console.
    -   **Scalable**, if you are developing your project for mobile devices.
    
    
    
     |
    | **Starter Content** | 
    
    Select whether you want your new project to include **starter content**. Starter content includes some simple Static Meshes with basic textures and Materials. It is useful if you want to start learning and experimenting straight away, without worrying about sourcing and importing custom content.
    
    
    
     |
    | **Ray Tracing** | 
    
    Select whether to enable or disable **ray tracing** for your project.
    
    For more information about ray tracing in Unreal Engine, refer to the [Hardware Ray Tracing and Path Tracing Features](/documentation/en-us/unreal-engine/ray-tracing-and-path-tracing-features-in-unreal-engine) page.
    
    
    
     |
    
4.  Select where you want to store your project, and give your project a name (4).
    
5.  Click **Create** (5) to finish creating your new project.
    

## Result

Unreal Engine creates a new project with the settings you configured, and then automatically opens the project.
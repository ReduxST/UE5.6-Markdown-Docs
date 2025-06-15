# Creating Custom Templates

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/converting-a-project-to-an-unreal-engine-template](https://dev.epicgames.com/documentation/en-us/unreal-engine/converting-a-project-to-an-unreal-engine-template)  
**Processed:** 2025-06-14 16:16:05

---

Unreal Engine's templates offer a powerful starting point for your projects. You can use them to quickly start developing for a specific platform or to create a specialized project, such as a multi-display experience.

With Unreal Engine, you can also create **custom templates** from existing projects to meet your specific needs.

A custom template is an Unreal Engine project configured such that the engine includes it in the list of templates that appears when you create a new project.

Custom templates can include content, settings, and code, and can have specific plugins enabled or disabled by default.

## Steps

In the instructions below, \[ProjectName\] refers to your Unreal Engine project's name (for example, `MyProjectName.uproject`). This is different from the **ProjectName** variable (without square brackets) in the `DefaultGame.ini` file.

To convert an existing project into a template:

1.  Copy the **entire** project's folder into the `Templates` folder of your Unreal Engine installation. If you installed Unreal Engine from the Epic Games Launcher, the `Templates` folder will be located at:
    
    -   `C:\Program Files\Epic Games\UE_[version]\Templates` on Windows
        
    -   `/Users/Shared/Epic Games/UE_[version]/Templates` on Mac
        
    
    If you compiled Unreal Engine from source, the `Templates` folder will be located at `[ForkLocation]\UE4\Templates`.
    
2.  Open the `[ProjectName]\Config\DefaultGame.ini file`. Then, add or update the **ProjectName** variable. This is the name that will display in the template selection screen when you create a new Unreal Engine project.
    
    Example:
    
    ```
         `[/Script/EngineSettings.GeneralProjectSettings]      ProjectID=E6468D0243A591234122E38F92DB28F4      ProjectName=MyTestTemplate`
    
    Copy full snippet
    ```
    \[/Script/EngineSettings.GeneralProjectSettings\] ProjectID=E6468D0243A591234122E38F92DB28F4 ProjectName=MyTestTemplate
    
    Note that the **ProjectID** variable is a unique ID generated for each project.
    
3.  From your Unreal Engine installation folder, go to `Templates\TP_FirstPerson\Config\`. Copy the `TemplateDefs.ini` file to the `[ProjectName]\Config` folder.
    
    You can use any existing template folder instead of `TP_FirstPerson`, as long as it has a `TemplateDefs.ini` file.
    
4.  Open the `TemplateDefs.ini` file you copied in the previous step and update the **LocalizedDisplayNames** and **LocalizedDescriptions** variables. There are four sets of variables, one for each language Unreal Engine supports: English (en), Korean (ko), Japanese (ja), and Simplified Chinese (zh-Hans).
    
    Example:
    
    ```
             `[/Script/GameProjectGeneration.TemplateProjectDefs]          LocalizedDisplayNames=(Language="en",Text="My Test Template")          LocalizedDescriptions=(Language="en",Text="This is a custom template that includes a first-person character and uses Blueprint.")`
    
    Copy full snippet
    ```
    \[/Script/GameProjectGeneration.TemplateProjectDefs\] LocalizedDisplayNames=(Language="en",Text="My Test Template") LocalizedDescriptions=(Language="en",Text="This is a custom template that includes a first-person character and uses Blueprint.")
5.  When you create a new project, your template will appear in the category specified in the `TemplateDefs.ini` file. This is controlled by the **Categories** variable. Despite the variable name, a template can only have **one** category assigned to it.
    
    The possible options are:
    
    -   **Games** - Games
    -   **ME** - Film, Television, and Live Events
    -   **AEC** - Architecture, Engineering, and Construction
    -   **MFG** - Automotive, Product Design, and Manufacturing
    
    For more information, open the `TemplateCategories.ini` file in the `[UE installation path]\UE_[Version]\Templates` folder.
    
6.  You can add an icon and a preview image in the `[ProjectName]\Media` folder. These images must use the PNG format and follow the naming conventions below:
    
    -   Icon: `[ProjectName].png`.
    -   Preview: `[ProjectName]_Preview.png`.

## End Result

You should now see the new template in the New Project dialog.

![A new custom template called My Test Template can be seen in this instance of the Unreal Project Browser.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/290512ab-8b40-47a6-b215-8d317bd46455/custom-template.png)

*A new custom template called My Test Template can be seen in this instance of the Unreal Project Browser.*

To see new templates, you only need to close and open the New Project window. However, if you make any changes to an existing template (for example, if you change its name or description), you must restart Unreal Engine before the changes are displayed in this window.
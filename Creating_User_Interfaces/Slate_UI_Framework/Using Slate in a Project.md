# Using Slate in a Project

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-slate-in-a-project-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-slate-in-a-project-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:53

---

In order to use the Slate User Interface (UI) Framework, your project must be set up properly so that it is aware of the framework. This allows you to include the Slate.h header and reference the various elements of the framework necessary for building a UI with slate.

## Module Dependencies

The Slate framework is stored in a few modules. In order to make your project aware of these, some dependencies must be set up in the \*.build.cs file for your project.

The modules your project needs access to are:

| Module | Dependency Type |
| --- | --- |
| InputCore | Public |
| Slate | Private |
| SlateCore | Private |

**To set up the Slate module dependencies:**

1.  Open the \[ProjectName\].build.cs file for your project. It is located in the \[ProjectDir\]/\[ProjectName\]/Source/\[ProjectName\] directory.
2.  Add the InputCore public dependency by adding `"InputCore"` to the `PublicDependencyModuleNames`.
    
    ```
         `PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore" });`
    		
    Copy full snippet
    ```
    PublicDependencyModuleNames.AddRange(new string\[\] { "Core", "CoreUObject", "Engine", "InputCore" });
    
    The InputCore module is set as a public dependency by default when code projects are created.
    
3.  Add Slate and SlateCore private dependencies. A line exists in the \*.build.cs file for adding private dependencies:
    
    ```
         `PrivateDependencyModuleNames.AddRange(new string[] {  });`
    		
    Copy full snippet
    ```
    PrivateDependencyModuleNames.AddRange(new string\[\] { });
    
    Add the SlateCore and Slate modules to that line:
    
    ```
         `PrivateDependencyModuleNames.AddRange(new string[] { "Slate", "SlateCore" });`
    
    Copy full snippet
    ```
    PrivateDependencyModuleNames.AddRange(new string\[\] { "Slate", "SlateCore" });
    
    Depending on when you created your project, and with what version of the engine, it may already have the Slate dependencies set up in the \*.build.cs files but commented out. You can uncomment the appropriate lines to set up the dependencies.
    
    ```
         `// Uncomment if you are using Slate UI      // PrivateDependencyModuleNames.AddRange(new string[] { "Slate", "SlateCore" });`
    Copy full snippet
    ```
    // Uncomment if you are using Slate UI // PrivateDependencyModuleNames.AddRange(new string\[\] { "Slate", "SlateCore" });
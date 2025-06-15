# Project Files for IDEs

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-generate-unreal-engine-project-files-for-your-ide](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-generate-unreal-engine-project-files-for-your-ide)  
**Processed:** 2025-06-14 16:29:05

---

The following guide is meant for users who have downloaded and built Unreal Engine from its source code, which we have made available on GitHub. For more information, see [Downloading Unreal Engine Source Code](programming-and-scripting/development-environment-setup/downloading-unreal-engine-source-code)

If you download the latest **Unreal Engine (UE)** code, you might notice that there are no **Visual Studio (VS)** or **Xcode** project files included for compiling and running the engine or example games. You will need to run a script that generates project files for you to load:

-   Run the `GenerateProjectFiles.bat` file which is located in the UE root directory.
    
-   The project generator tool will analyze the module and target build files and generate new project files. This may take some time to complete.
    

For VS developers, this will generate a `UE5.sln` file in the same directory. You will use this solution file to build and run UE games and programs. For your first time compiling, we recommend building using the Development configuration with Win64 platform.

By default, we generate buildable projects for all available platforms that we detected SDKs for, so that you will be able to build and debug console and mobile platforms as well. If you want to generate projects only for the current platform you are running on (for example, Windows.), run the `GenerateProjectFiles.bat` with the `-CurrentPlatform` argument. The project files will be a little lighter.

Remember to re-run `GenerateProjectFiles.bat` after syncing new code changes from source control. If you forget to do this, you will most likely run into problems when compiling or running your game.

If you make local changes to modules such as adding or removing source files, you should re-run `GenerateProjectFiles.bat`. We do not recommend manually making changes to project files.

## Command-line Options

The project generator has some optional command-line arguments that you can use if you want to customize your generated project files to suit your needs more closely. Typically these options are not required or recommended.

| Option | Description |
| --- | --- |
| 
`-CurrentPlatform`

 | 

Generates buildable projects for only the current desktop platform (Windows or Mac), instead of all detected available target platforms.

 |
| 

`-2022`

 | 

Generates projects in a format native to VS 2022. The Visual C++ 2022 compiler will be used to compile when this option is set.

 |
| 

`-ThirdParty`

 | 

Adds headers and other files from third-party libraries to the project. This could be useful if you like to see symbols and files in Visual Assist for PhysX, Steamworks or Bink for example. However, it will make the project files take longer to load.

 |
| 

`GAME_NAME -Game`

 | 

Tells the project generator to generate projects that only include code and content for the specified project name, excluding all other discovered projects. Make sure to specify a project name as well. For example `GenerateProjectFiles.bat ShooterGame.uproject -Game` would generate projects that only have source and targets for ShooterGame.

 |
| 

`-NoIntelliSense`

 | 

Skips generation of IntelliSense data used for auto-completion and error squiggles in the IDE.

 |
| 

`-AllLanguages`

 | 

Includes engine documentation for all languages. By default, we only include files in the project for English.

 |
| 

`-OnlyPublic`

 | 

When specified, only public header files will be included in the generated projects for Engine modules. By default, all source files are included for Engine modules. This can give you faster project load times, but it might be more difficult to navigate engine code.

 |
| 

`-NoShippingConfigs`

 | 

Omits the `Shipping` and `Test` build configurations from the generated projects. This will reduce the number of target configurations you need to deal with.

 |
| 

`-Platforms=PLATFORM_1+PLATFORM_2+...`

 | 

Overrides the default set of platforms to generate buildable projects for, and instead generates projects for the platform or platforms that you specify. You can specify multiple platforms by separating them with a '+' character. This also causes the generated solution file to be named with a suffix that includes the platform name or names.

 |

## Additional Information

The `GenerateProjectFiles.bat` script is a simple wrapper around Unreal Build Tool, which is launched in a special mode that builds project files instead of building program executables. It invokes Unreal Build Tool with the `-ProjectFiles` command-line option.

The UE build system does not actually require project files to compile the code. Unreal Build Tool always locates source files using module and target build files. For this reason, if you add a new source file and trigger a compile, the new source file may be included in the build even though the project files have not been refreshed yet.

For VS projects, the generated solution file is `UE5.sln` and is saved to the root UE directory. However, the project files are saved to the `UNREAL_ENGINE_ROOT/Engine/Intermediate/ProjectFiles/` directory. It is safe to delete these files at any time and regenerate projects, however, you may lose certain project-specific preferences such as command-line argument strings if you delete these files.

### Advantages of Generate Project Files

There are certainly both pros and cons, but here are some important reasons why we decided to generate project files for UE:

-   UE is designed to work with many platforms, but different teams may only be working with a few specific platforms at any time. By generating project files, we can omit platform-specific files and build configurations that are not relevant.
    
-   UE programming methodology incorporates many sub-modules, and it was very important that we made it as easy as possible for programmers to add new modules.
    
-   The project generator emits highly-accurate definitions and includes paths which are used by VS IntelliSense while you are working on UE code.
    
-   Setting up a new project is much easier when project files are automatically generated.
    
-   We want to support multiple platforms and development environments (for example, VS and Xcode). Maintaining multiple sets of project files manually is error-prone and tedious.
    
-   We want to enable programmers to generate highly customized project files.
    
-   The directory structure of source files is automatically mirrored in the project file solution hierarchy. This is really convenient when browsing source files, but was difficult to maintain with manually authored projects.
    
-   UE build configurations are very complex and are difficult to maintain manually. The project generator makes this nearly transparent to developers.
    

### Other Files Added with Generate Project Files

Along with source code for C++ modules, we automatically add several other files to the generated projects. This is just to make it easy to locate these files when doing searches. Some examples of other files that are added to the generated projects:

-   Shader source code (`*.usf` files)
    
-   Engine documentation files (`*.udn` files)
    
-   Program configuration files (`*.ini` files)
    
-   Localization files (`*.int` files)
    
-   Program resource files and manifests (`*.rc`, .manifest)
    
-   Certain external (non-generated) project files (for example, UnrealBuildTool and Clean)
    

### Project Files and Source Control

Project files are not checked in to source control. Merging source control conflicts to project files was tedious and highly error-prone. The new system avoids this entirely by treating project files as pure intermediates. Plus, solution files will be different for each team that is working on different game projects. Chances are that the project files that we use at Epic will not be useful to other teams without modifications.

### Debugging Project Generator Code

Here are some useful tips to help you debug changes that you have made to project generator code:

-   Change your startup project to UnrealBuildTool.
    
-   Set the command-line parameters for debugging to `-ProjectFiles`.
    
-   Set the working directory to your local path for `UNREAL_ENGINE_ROOT/Engine/Source/`.
    
-   Compile and debug as normal.
    

Be aware that the project generator may delete the project files you are using in VS as you are working. For this reason, it is sometimes useful to load the Unreal Build Tool project directly into VS instead of debugging through the regular UE solution file.

### Build Multiple Configurations

You can use the **Batch Build** feature in VS. You can find this under the **Build** menu. Simply select all of the configurations that you want to compile and click **Build**.

### Integration With UnrealVS Extension

The [UnrealVS Extension](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-unrealvs-extension-for-unreal-engine-cplusplus-projects) for VS includes a tool-bar button that you can click to re-generate project files for the currently loaded solution.

You can also bind a shortcut key to this feature. In VS, open **Tools > Options > Environment > Keyboard**, then search for UnrealVS.RefreshProjects.

Note that this feature is only enabled after you have a solution loaded (because the tool needs to know which code branch to generate projects for). If you have no `UE5.sln` file generated yet, you will need to run the `GenerateProjectFiles.bat` script directly first.
# Running Unreal Engine

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/running-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/running-unreal-engine)  
**Processed:** 2025-06-14 16:47:35

---

Operating System

×Windows

Select an option from the dropdown to see content relevant to it.

[![](https://dev.epicgames.com/community/api/documentation/image/ecb60063-5331-4ba0-a7ae-f6ab4fad510f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ecb60063-5331-4ba0-a7ae-f6ab4fad510f?resizing_type=fit)

The instructions on this page are for running the engine with projects compiled in a **Development** build configuration. You can substitute the `UEEditor-_.exe` or `UE-_.exe` that you need for opening projects built in other configurations. More information on the binary naming convention can be found on the [Building Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/building-unreal-engine-from-source) page.

## Running the Editor

The process of running the editor requires passing the name of the project to run as an argument to the executable.

You can add the `-debug` switch to force the executable to load the debug version of the modules for your project, which contain all of the debugging symbols. This is necessary even when debugging through Visual Studio with the configuration set to **Debug** because the main executable is always compiled using the **Development** configuration. Of course, you must first compile your modules using the Debug configuration so they exist for the executable to load.

### Running the Editor from the Command Line

1.  From a command prompt, navigate to your `[LauncherInstall][VersionNumber]\Engine\Binaries\Win64` directory.
    
2.  Run the `UEEditor.exe`, passing it the path to your project.
    
    Shell
    
    `UEEditor.exe "[ProjectPath][ProjectName].uproject"`
    
    UEEditor.exe &quot;\[ProjectPath\]\[ProjectName\].uproject&quot;
    
    Copy full snippet(1 line long)
    

### Running the Editor from the Executable

1.  Navigate to your `[LauncherInstall][VersionNumber]\Engine\Binaries\Win64` directory.
    
2.  Right-click on the `UEEditor.exe` executable and choose **Create shortcut**.
    
3.  Rename the shortcut to something like **MyProject - Editor.exe** as this reflects that this shortcut runs the MyProject game editor.
    
4.  Right-click on the newly created shortcut and choose **Properties**.
    
5.  Add the name of the game to run as an argument at the end of the **Target** property:
    
    Shell
    
    `[LauncherInstall][VersionNumber]\Engine\Binaries\Win64\UEEditor.exe "[ProjectPath][ProjectName].uproject"`
    
    \[LauncherInstall\]\[VersionNumber\]\\Engine\\Binaries\\Win64\\UEEditor.exe &quot;\[ProjectPath\]\[ProjectName\].uproject&quot;
    
    Copy full snippet(1 line long)
    
6.  Press **OK** to save the changes.
    
7.  Double-click the shortcut to launch the editor.
    

### Running the Editor with No Arguments (Stand-alone)

If the editor is not set to open the most recent project at startup, running the editor executable without any arguments will launch the Project Browser. From here, you can [create a new project](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine) , [open your existing projects](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine) , or open [content examples and sample games](https://dev.epicgames.com/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine) .

## Running an Uncooked Game

Once a project is loaded in Unreal Editor, you can [test your gameplay](https://dev.epicgames.com/documentation/en-us/unreal-engine/in-editor-testing-play-and-simulate-in-unreal-engine) in Uncooked Game mode from the **Play In** menu. To play the uncooked game in its own window, select the [New Window At > Default Player Start mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/in-editor-testing-play-and-simulate-in-unreal-engine) using the [Play In dropdown menu](https://dev.epicgames.com/documentation/en-us/unreal-engine/in-editor-testing-play-and-simulate-in-unreal-engine) in the Level Editor toolbar.

[![](https://dev.epicgames.com/community/api/documentation/image/675380d5-2cdd-48b3-8a37-bfa47aa78206?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/675380d5-2cdd-48b3-8a37-bfa47aa78206?resizing_type=fit)

*Click to see full-size image:*

Running the uncooked game version of the engine executable using either of the below methods will result in the same behavior.

### Running an Uncooked Game from the Command Line

When running from the command line, you must pass the name of the project you want to run along with the `-game` switch as arguments.

1.  From a command prompt, navigate to your `[LauncherInstall][VersionNumber]\Engine\Binaries\Win64` directory.
    
2.  Run the **UEEditor.exe** passing it the path to the project to run, along with the `-game` parameter.
    
    C++
    
    `UEEditor.exe "[ProjectPath][ProjectName].uproject" -game`
    
    UEEditor.exe &quot;\[ProjectPath\]\[ProjectName\].uproject&quot; -game
    
    Copy full snippet(1 line long)
    

### Running an Uncooked Game from the Executable

When running from the executable, you must specify the path to the project you want to run along with the `-game` switch as arguments to the executable via the **Target** property of a shortcut.

1.  Navigate to your `[LauncherInstall][VersionNumber]\Engine\Binaries\Win64` directory.
    
2.  **Right-click** on the **UEEditor.exe** executable and choose **Create shortcut**.
    
3.  Rename the shortcut to reflect the game it will run, i.e. **MyProject.exe**.
    
4.  **Right-click** on the newly created shortcut and choose **Properties** to display the properties of the shortcut.
    
5.  Add the full path to the project to run as an argument at the end of the **Target** property, and specify the `-game` argument to run as a game:
    
    C++
    
    `[LauncherInstall][VersionNumber]\Engine\Binaries\Win64\UEEditor.exe "[ProjectPath][ProjectName].uproject" -game`
    
    \[LauncherInstall\]\[VersionNumber\]\\Engine\\Binaries\\Win64\\UEEditor.exe &quot;\[ProjectPath\]\[ProjectName\].uproject&quot; -game
    
    Copy full snippet(1 line long)
    
6.  Press **OK** to save the changes.
    
7.  **Double-click** the shortcut to run the game.
    

## Running a Cooked Game

See [Packaging Projects](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project?application_version=5.5) for information on how to package and run cooked game builds

## Useful In-Game Commands

When you are running the game, there are a multitude of **console commands** you can use in the console inside the game. The console can be summoned by pressing the **~ (tilde)** or **Tab** keys. Some of the most useful commands are listed below.

-   `EXIT/QUIT`
    
-   `DISCONNECT`
    
-   `OPEN [MapURL]`
    
-   `TRAVEL [MapURL]`
    
-   `VIEWMODE [Mode]`
    

## Loading Maps

It is possible to specify a particular map to load when running the engine or editor or load a new map while running the engine. This can be useful for testing by quickly jumping into the map you want to test without needing to make your way through a series of menus.

### Loading Maps at Startup

The engine will always attempt to load a default map when it is run. This map is specified in the `DefaultEngine.ini` config file located in the `Config` folder of your game project. The map to run by default is set using the **Map** property in the `[URL]` section of the .ini file. As an example, when you create a project with a map file named "MyMap", the following is set automatically in its `DefaultEngine.ini` file:

C++

`GameDefaultMap=/Game/Maps/MyMap`

GameDefaultMap=/Game/Maps/MyMap

Copy full snippet(1 line long)

This will cause the `MyMap.umap` (located in `(UE4Directory)/(YourProjectName)/Content/Maps`) to load at startup unless it is overridden. Generally, you will want to specify the map that loads or is used as the background for your main menu as the default map.

To override the default map, you can pass in a map name (without the file extension) as a command line argument. It was mentioned previously that you must specify the project name on the command line. Following these, you can also specify a map name to force the engine to load a map other than the default. For instance, the following command line could be used to load the engine running the `ExampleMap` map:

C++

`UEEditor.exe "[ProjectPath][ProjectName].uproject" ExampleMap -game`

UEEditor.exe &quot;\[ProjectPath\]\[ProjectName\].uproject&quot; ExampleMap -game

Copy full snippet(1 line long)

The same concept works when running the editor. Specifying the name of the map to load will load that map when the editor opens instead of the default or blank map. To load the editor with the `ExampleMap` map loaded, the following command line can be used:

`UE4Editor.exe "[ProjectPath][ProjectName].uproject" ExampleMap -game`

The map name can also be a full map URL specifying additional settings such as the GameMode. Settings are appended to the map name as key-value pairs separated by a `?`. For example:

C++

`DM-Deck?Game=CaptureTheFlag`

DM-Deck?Game=CaptureTheFlag

Copy full snippet(1 line long)

### Loading New Maps

If you want to load a new map during play, in order to test during development or even to switch maps during gameplay, this can be done using the `OPEN` or `TRAVEL` console commands followed by the name of the map (without the file extension) to load.

The difference between the `OPEN` and `TRAVEL` commands is described above in the [Useful In-Game Commands](https://dev.epicgames.com/documentation/en-us/unreal-engine/running-unreal-engine) section.

The commands below load the DM-Deck map during play with the same settings or settings reset, respectively:

C++

`open DM-Deck`

open DM-Deck

Copy full snippet(1 line long)

Or

C++

`travel DM-Deck`

travel DM-Deck

Copy full snippet(1 line long)
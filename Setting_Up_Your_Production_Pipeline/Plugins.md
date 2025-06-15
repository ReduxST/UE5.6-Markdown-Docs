# Plugins

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/plugins-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/plugins-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:47

---

This page describes the development and management of **Plugins** for use with **Unreal Engine (UE)** tools and runtime.

In Unreal Engine, Plugins are collections of code and data that developers can easily enable or disable within the Editor on a per-project basis. Plugins can add runtime gameplay functionality, modify built-in Engine features (or add new ones), create new file types, and extend the capabilities of the Editor with new menus, tool bar commands, and sub-modes. Many existing Unreal Engine subsystems were designed to be extensible using Plugins.

If you want to jump right in and create a Plugin now, please see the [Creating New Plugins](/documentation/en-us/unreal-engine/plugins-in-unreal-engine#creatingnewplugins) section.

## Plugin UI in the Editor

You can see which Plugins are currently installed by opening the Plugin editing interface from the **Edit** menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d52f2f6-0d63-4a80-8e28-abe75dccbbf1/pluginseditor.png)

The Plugin Editor is accessible from the main 'Window' menu. This interface displays all of the Plugins that are currently installed and can enable or disable Plugins individually.

You can browse categories of Plugins using the tree interface on the left. Selecting a category will show all Plugins in that category as well as Plugins in any sub-category. As you navigate through categories, a bread crumb trail displayed at the top of the UI will enable you to jump quickly to higher-level categories. The number displayed next to a category indicates how many Plugins are available in that category.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ef6e573-edf6-48b5-815b-16a8ef6b737f/plugincategories.png)

Plugins are displayed in the main list, along with each Plugin's name, icon, current version, text description, author (and optional web hyperlink), as well as whether or not the plugin is currently enabled.

The search control at the top will enable you to search Plugins displayed in the list by name.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c88c13a-bb6f-4e90-a5ab-2c439875eb1f/searchingplugins.png)

You can enable or disable a Plugin for use with your active project by toggling the **Enabled** check box under the Plugin's description. You may need to restart the Editor for the change to take effect.

## Anatomy of a Plugin

Plugins with code will have a Source folder. This folder will contain one or more directories with module source code for the Plugin. Note that, although Plugins often contain code, this is not actually a requirement. See the [Code in Plugins](/documentation/en-us/unreal-engine/plugins-in-unreal-engine#codeinplugins) section for more information.

Plugins with code will have a `Binaries` folder that contains compiled code for that Plugin, and temporary build product files will be stored in a separate `Intermediate` folder under the Plugin's directory.

Plugins can have their own Content folder that contains Asset files specific to that Plugin. See the [Content in Plugins](/documentation/en-us/unreal-engine/plugins-in-unreal-engine#contentinplugins) section for more information. Plugin configuration files should be placed using the same convention as other configuration files:

-   Engine plugins: `[PluginName]/Config/Base[PluginName].ini`
-   Game plugins: `[PluginName]/Config/Default[PluginName].ini`

Plugins do not support their own Derived Data Cache distribution.

## Plugin Folders

In order for Plugins to be found, they must be located in one of the search paths for Plugins, either in your project, or in the Engine itself.

| Plugin Type | Search Path |
| --- | --- |
| Engine | `[Unreal Engine Root Directory]/Engine/Plugins/[Plugin Name]/` |
| Game | `[Project Root Directory]/Plugins/[Plugin Name]/` |

You can also organize Plugins into subdirectories under the base Plugins folder. The engine will scan all of your sub-folders under the base Plugins folder for Plugins to load, but it will never scan subdirectories beneath a Plugin that has already been found.

Unreal Engine finds your Plugin by searching for `.uplugin` files on disk. We call these files **Plugin Descriptors**. They are text files that provide basic information about your Plugin. Plugin Descriptors are discovered and loaded automatically by the Engine, Editor, and **UnrealBuildTool** (UBT), whenever those programs are run. See the section on [Plugin Descriptors](/documentation/en-us/unreal-engine/plugins-in-unreal-engine#plugindescriptorfiles) to learn about creating and customizing these files.

## Code in Plugins

When generating project files for Visual Studio or Xcode, any Plugins that have `Source` folders (containing `.Build.cs` files) will be added to your project files to make it easier to navigate to their source code. These Plugins will automatically be compiled by UBT when compiling your game project.

Plugins are allowed to have any number of Module source directories. Most Plugins will only have one Module, but it is possible to create multiple, for example, if a Plugin contains some Editor-only functionality, and other code that is intended to run during the game.

For the most part, Plugin source file layout is the same as any other C++ Module in the Engine.

Plugins are able to declare new reflected types (`UCLASS`, `USTRUCT`, etc.) in header files within a Module's `Source` directory (or one of its subdirectories). The Engine's build system will detect these files and generate code as needed to support the new types. You will need to follow the normal rules for using `UObjects` within C++ modules, such as including the generated header file and the Module's `generated.inl` file in one of your Module's source files.

Unreal Engine supports interdependent Modules and Plugins. Project Modules can depend on Plugins by enabling the Plugins in its `.uproject` file. Similarly, Plugins indicate dependency by enabling other Plugins within their own .uplugin files. There is one important restriction, however, which is that Plugins and Modules are broken into hierarchical levels, and can only depend on other Plugins or Modules at the same level or higher. For example, although a Project Module can depend on an Engine Module, an Engine Module cannot depend on a Project Module. This is because the Engine (and all of its Plugins and Modules) is higher-level than any Project, as it must be able to build without a Project. The following diagram indicates the hierarchy of dependency levels between Projects and Modules:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54c51526-241d-47a5-a17b-41649eafdeea/pluginandmoduledependency.png)

Arrows indicate possible dependency. Each Plugin or Module type can depend on others at its own level or higher.

### Engine Plugins

Unreal Engine has some built-in Plugins included under the `Engine` directory. Engine Plugins are just like project Plugins, except that they are available for all projects. Typically, these plugins are created by engine and tools programmers to provide baseline functionality that can be used in multiple projects while being maintained in a single place. This can enable the user to add or override engine features without modifying engine code.

## Content in Plugins

Unreal Engine supports plugins that contain game content as well as binary code. In order to use Content in a Plugin, the "CanContainContent" setting within the Plugin's descriptor must be set to "true".

## Plugins in Projects

Plugins reside under the `Plugins` subfolder within your project's directory, and will be detected and loaded at Engine or Editor start-up time.

If the Plugin contains modules that have `Source` folders (and `.Build.cs` files), Plugin code will automatically be added to generated C++ project files, so that you can work on developing the Plugin alongside your project. Whenever you compile your project, any Plugins that have source available will also be compiled as a dependency of your game.

Plugins that do not have a `Source` folder are ignored by the project generator and will not appear in your C++ project files, but they will still be loaded at start-up as long as binary files exist.

At present, Plugin configuration files are not packaged with projects. This may be supported in the future, but currently requires manually copying the files to the project's `Config` folder.

## Distributing a Plugin on the Epic Marketplace

To package your Plugin, click the **Package...** link to package your Plugin into a folder for distribution.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ee0b664-2949-4b05-a57d-9b13e0630086/packageplugin.png)

### Precompiling Plugins

If you are precompiling a plugin for UE 5.2, compile your plugin with Visual Studio 2019 — the minimum supported version of Visual Studio for UE 5.2. Compiling with Visual Studio 2019 ensures that the resulting libraries are compatible with UE 5.2 for all users. For more information about Visual Studio and Unreal Engine version compatability, see [Setting Up Visual Studio](/documentation/404) for more information.

## Plugin Descriptor Files

Plugin descriptors are files that end with `.uplugin`. The first part of the file name is always the name of your Plugin. Plugin descriptor files are always located in your Plugin's directory, where the Engine will discover them at start-up time.

Plugin descriptors are in the Json ([JavaScript Object Notation](http://www.json.org/)) file format.

### Descriptor File Example

This example plugin descriptor is from the Engine's `UObjectPlugin`.

```
`{     "FileVersion" : 3,     "Version" : 1,     "VersionName" : "1.0",     "FriendlyName" : "UObject Example Plugin",     "Description" : "An example of a plugin which declares its own UObject type.  This can be used as a starting point when creating your own plugin.",     "Category" : "Examples",     "CreatedBy" : "Epic Games, Inc.",     "CreatedByURL" : "http://epicgames.com",     "DocsURL" : "",     "MarketplaceURL" : "",     "SupportURL" : "",     "EnabledByDefault" : true,     "CanContainContent" : false,     "IsBetaVersion" : false,     "Installed" : false,     "Modules" :     [         {             "Name" : "UObjectPlugin",             "Type" : "Developer",             "LoadingPhase" : "Default"         }     ] }`
Copy full snippet
```
{ "FileVersion" : 3, "Version" : 1, "VersionName" : "1.0", "FriendlyName" : "UObject Example Plugin", "Description" : "An example of a plugin which declares its own UObject type. This can be used as a starting point when creating your own plugin.", "Category" : "Examples", "CreatedBy" : "Epic Games, Inc.", "CreatedByURL" : "http://epicgames.com", "DocsURL" : "", "MarketplaceURL" : "", "SupportURL" : "", "EnabledByDefault" : true, "CanContainContent" : false, "IsBetaVersion" : false, "Installed" : false, "Modules" : \[ { "Name" : "UObjectPlugin", "Type" : "Developer", "LoadingPhase" : "Default" } \] }

### Descriptor File Format

The descriptor file is a JSON-formatted list of variables from the `FPluginDescriptor` type. There is one additional field, "FileVersion", which is the only required field in the structure. "FileVersion" gives the version of the Plugin descriptor file, and should usually set to the highest version that is allowed by the Engine (currently, this is "3"). Because this version applies to the format of the Plugin Descriptor File, and not the Plugin itself, we do not expect that it will change very frequently, and it should not change with subsequent releases of your Plugin. For maximum compatibility with older versions of the Engine, you can use an older version number, but this is not recommended.

For details about the other supported fields, see the [](/documentation/404)API reference page.

Field names for Boolean variables lose the initial "b" in the variable name. For example the variable `bEnabledByDefault` corresponds to the "EnabledByDefault" field.

#### Module Descriptors

For Plugins that contain code, the "Modules" field in the descriptor file will contain at least one entry. An example entry follows:

```
`{     "Name" : "UObjectPlugin",     "Type" : "Developer"     "LoadingPhase" : "Default" }`
Copy full snippet
```
{ "Name" : "UObjectPlugin", "Type" : "Developer" "LoadingPhase" : "Default" }

Each entry requires the "Name" and "Type" fields. "Name" is the unique name of the Plugin Module that will be loaded with the Plugin. At runtime, the Engine will expect appropriate Plugin binaries to exist in the Plugin's "Binaries" folder with the specified Module name. For Modules that have a Source directory, a matching ".Build.cs" file much exist within the Module's subfolder tree. "Type" sets the type of Module. Valid options are **Runtime**, **RuntimeNoCommandlet**, **Developer**, **Editor**, **EditorNoCommandlet**, and **Program**. This type determines which types of applications can load the Module. For example, some plugins may include modules that should only load when the Editor is running. Runtime modules will be loaded in all cases, even in shipped games. Developer modules will only be loaded in development runtime or Editor builds, but never in shipping builds. Editor modules will only be loaded when the editor is starting up. Your Plugin can use a combination of modules of different types.

For details about the other supported fields, see the [](/documentation/404)API reference page.

## Icons

Along with the descriptor file, Plugins need an icon to display in the Editor's Plugin Browser. The image should be a 128x128 .png file called "Icon128.png" and kept in the Plugin's "/Resources/" directory.

## Creating New Plugins

To create a new Plugin, use the **New Plugin** button in the Editor's Plugin Browser.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f43f4c4-8df1-4214-9b1f-c44280d80e45/createplugin.png)

From there, you can select which type of Plugin you wish to create, enter a name, and set some basic parameters.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/296a16d2-cffa-4192-a962-bda9958dd4dc/plugintypes.png)

Your new Plugin will now appear in the Plugin Browser, and will be enabled in your current project.
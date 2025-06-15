# Configuration Files

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:45

---

**Configuration Files** or **Config Files** provide the initial settings for **Unreal Engine (UE)**. At their most basic level, they contain lists of key-value pairs organized into sections. These files are used to set default values for objects and properties that are loaded upon startup of Unreal Engine for all builds and platforms. Configuration files use the `.ini` file extension.

## Syntax

Configuration files are structured as follows:

```
`[SECTION1] <KEY1>=<VALUE1> <KEY2>=<VALUE2>  [SECTION2] <KEY3>=<VALUE3>`
Copy full snippet
```
\[SECTION1\] <KEY1>=<VALUE1> <KEY2>=<VALUE2> \[SECTION2\] <KEY3>=<VALUE3>

Every config variable must belong to a `[SECTION]` and consist of a `KEY` followed by the `=` symbol. For example, in `BaseEngine.ini`:

```
`[Core.Log] LogTemp=warning`
Copy full snippet
```
\[Core.Log\] LogTemp=warning

The `VALUE` can be empty in a config variable, so it is possible to have:

```
`[Core.Log] LogTemp=`
Copy full snippet
```
\[Core.Log\] LogTemp=

### Section Names

Section names are alphabetic strings you can set to any value. The config system loads all declarations in configuration files whether a config variable exists in your project code or not.

#### Modules

Section headings for configurable objects contained in modules use the syntax:

```
`[/Script/ModuleName.ClassName]`
Copy full snippet
```
\[/Script/ModuleName.ClassName\]

where:

-   `ModuleName`: the name of the module containing the configurable object.
-   `ClassName`: the name of the class within the module `ModuleName` containing the configurable object.

#### Plugins

Section headings for configurable objects contained in plugins use the syntax:

```
`[/Script/PluginName.ClassName]`
Copy full snippet
```
\[/Script/PluginName.ClassName\]

where:

-   `PluginName`: the name of the plugin containing the configurable object.
-   `ClassName`: the name of the class within the plugin `PluginName` containing the configurable object.

#### Blueprints

Section headings for configurable assets contained in blueprints use the syntax:

```
`[/PathToUAsset/UAssetName.UAssetName_C]`
Copy full snippet
```
\[/PathToUAsset/UAssetName.UAssetName\_C\]

where:

-   `PathToUAsset`: the path to your asset.
-   `UAssetName`: the name of the asset in `PathToUAsset` containing the configurable object.

#### Custom Section Names

Any alphabetic string can be used as a custom category name. For example, if you want a category named "MyConfigSection", write

```
`[MyConfigSection]`
Copy full snippet
```
\[MyConfigSection\]

When you use custom section names, you must manually query the config variables contained in the section. See the [Manually Apply Configuration Settings to Variables](/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine#manually) section for more information.

### Comments

Prepend a semicolon ( `;` ) to any line to create a comment in your configuration file. This also works for commenting out key-value pairs as opposed to deleting them from a file.

```
`[Core.Log] ; This section can be used in DefaultEngine.ini to override the display level for different log categories, using lines like the following: ; LogTemp=warning`
Copy full snippet
```
\[Core.Log\] ; This section can be used in DefaultEngine.ini to override the display level for different log categories, using lines like the following: ; LogTemp=warning

### Key-Value Pairs

Configuration keys can represent a variety of different types of information:

-   Strings
-   Numerics
-   Arrays
-   Structs

#### Array

Array structures in configuration files provide a mechanism for you to combine, accumulate, or override information across multiple configuration files in the configuration file hierarchy. For example, you can add multiple entries to a single configuration array object across multiple files in the hierarchy, such as `BaseEngine.ini` and `DefaultEngine.ini` in your engine directory, and `DefaultEngine.ini` in your project directory.

Configuration files support the following array operations:

| **Name** | **Operator** | **Description** | **Example** |
| --- | --- | --- | --- |
| Empty | `!` | Empty the contents of an array. Any value after `=` is ignored. For clarity, we recommend you put something descriptive after `=` such as `!MyVar=ClearArray`. | `!MyArray=ClearArray` |
| Append | `+` | Append the value to the array if it does not yet exist in the array already. Does nothing if the value already exists in the array. | `+MyArray=Value` |
| Remove | `-` | Remove the value from the array. Must be an exact match. | `-MyArray=Value` |
| Append Duplicate | `.` | Append the value to the array, even if the value already exists in the array. | `.MyArray=Value` |

##### Array Example

```
`MyConfigArray=7 !MyConfigArray=ClearArray +MyConfigArray=2 +MyConfigArray=3 +MyConfigArray=4 .MyConfigArray=2 -MyConfigArray=4`
Copy full snippet
```
MyConfigArray=7 !MyConfigArray=ClearArray +MyConfigArray=2 +MyConfigArray=3 +MyConfigArray=4 .MyConfigArray=2 -MyConfigArray=4

The lines in this example perform the following operations:

-   `MyConfigArray=7`: remove everything from array then append 7
-   `!MyConfigArray=ClearArray`: clear the array of all entries
-   `+MyConfigArray=2`: append 2 to the array
-   `+MyConfigArray=3`: append 3 to the array
-   `+MyConfigArray=4`: append 4 to the array
-   `.MyConfigArray=2`: append potential duplicate 2 to the array
-   `-MyConfigArray=4`: remove 4 from the array

In the end, `MyConfigArray` contains `[2,3,2]`.

#### Structs

Configuration files support changing struct properties in a config object. The syntax for setting a struct is

```
`[/Script/MyModule.MyClass] MyStruct=(MyStructProperty1=Value1,MyStructProperty2=Value2,...)`
Copy full snippet
```
\[/Script/MyModule.MyClass\] MyStruct=(MyStructProperty1=Value1,MyStructProperty2=Value2,...)

#### Strings

Quotes support the use of specially escaped characters, hexadecimal, and UTF sequences. This is helpful for localization and internationalization. For example, the following section is contained in `BaseEngine.ini`:

```
`[Internationalization] ; These are the paths for localizing the core engine itself, the localized game content settings are in *Game.ini +LocalizationPaths=../../../Engine/Content/Localization/Engine +CultureDisplayNameSubstitutes="ja;\u53f0\u6e7e;\u30c1\u30e3\u30a4\u30cb\u30fc\u30ba\u30bf\u30a4\u30da\u30a4" +CultureDisplayNameSubstitutes="\u53f0\u6e7e;\u4e2d\u534e\u53f0\u5317"`
Copy full snippet
```
\[Internationalization\] ; These are the paths for localizing the core engine itself, the localized game content settings are in \*Game.ini +LocalizationPaths=../../../Engine/Content/Localization/Engine +CultureDisplayNameSubstitutes="ja;\\u53f0\\u6e7e;\\u30c1\\u30e3\\u30a4\\u30cb\\u30fc\\u30ba\\u30bf\\u30a4\\u30da\\u30a4" +CultureDisplayNameSubstitutes="\\u53f0\\u6e7e;\\u4e2d\\u534e\\u53f0\\u5317"

## Configuration Files in Your Project

There are a few important considerations when using configuration files in your project. These include:

-   What categories of configuration files does Unreal Engine recognize?
-   How do files within the same category interact with one another?

### Configuration File Categories

Unreal Engine recognizes several typical "known" categories of configuration files.

#### General

-   `Engine`
-   `Game`
-   `Input`
-   `DeviceProfiles`
-   `GameUserSettings`
-   `Scalability`
-   `RuntimeOptions`
-   `InstallBundle`
-   `Hardware`
-   `GameplayTags`

#### Editor-Only

-   `Editor`
-   `EditorPerProjectUserSettings`
-   `EditorSettings`
-   `EditorKeyBindings`
-   `EditorLayout`

#### Desktop-Only

-   `Compat`
-   `Lightmass`

### Configuration File Hierarchy

There can be multiple different configuration files within each category. For example, the `Engine` directory contains:

-   `Engine\Config\BaseGame.ini`
-   `Engine\Config\Windows\WindowsGame.ini`

These files are part of the `Game` configuration file category. Each provides an additional layer of customization.

Configuration files within the same category are organized into a hierarchical structure. If there are duplicate key-value pairs among files in the same category, key-value assignments in latter files override those from files earlier in the hierarchy. Configuration files stored in the `Engine` directory apply to all projects using this Engine distribution. Configuration files located in the `<PROJECT_DIRECTORY>` apply only to that particular project. Similarly, configuration files located in `<PLATFORM>` directories apply only to that particular platform.

Category configuration files are loaded in the following order:

1.  `Engine/Config/Base.ini`
2.  `Engine/Config/Base<CATEGORY>.ini`
3.  `Engine/Config/<PLATFORM>/Base<PLATFORM><CATEGORY>.ini`
4.  `Engine/Platforms/<PLATFORM>/Config/Base<PLATFORM><CATEGORY>.ini`
5.  `<PROJECT_DIRECTORY>/Config/Default<CATEGORY>.ini`
6.  `Engine/Config/<PLATFORM>/<PLATFORM><CATEGORY>.ini`
7.  `Engine/Platforms/<PLATFORM>/Config/<PLATFORM><CATEGORY>.ini`
8.  `<PROJECT_DIRECTORY>/Config/<PLATFORM>/<PLATFORM><CATEGORY>.ini`
9.  `<PROJECT_DIRECTORY>/Platforms/<PLATFORM>/Config/<PLATFORM><CATEGORY>.ini`
10.  `<LOCAL_APP_DATA>/Unreal Engine/Engine/Config/User<CATEGORY>.ini`
11.  `<MY_DOCUMENTS>/Unreal Engine/Engine/Config/User<CATEGORY>.ini`
12.  `<PROJECT_DIRECTORY>/Config/User<CATEGORY>.ini`

Configuration set in the Engine directory applies to all projects that use this engine distribution. If possible, use the configuration files located in your project directory for finer control over configuration changes.

For more information about the configuration file hierarchy, see the header file `ConfigHierarchy.h` located in `Engine/Source/Runtime/Core/Public/Misc`.

#### Hierarchy Example

To illustrate how the hierarchy works, suppose that you have a project named `MyExampleProject` and in the `Engine/Config/BaseEngine.ini` configuration file, you have:

```
`[/Script/EngineSettings.GameMapsSettings] GameDefaultMap=/Engine/Maps/Templates/OpenWorld`
Copy full snippet
```
\[/Script/EngineSettings.GameMapsSettings\] GameDefaultMap=/Engine/Maps/Templates/OpenWorld

Suppose that you have the following config setting in `MyExampleProject/Config/DefaultEngine.ini`:

```
`[/Script/EngineSettings.GameMapsSettings] GameDefaultMap=/Game/ThirdPerson/Maps/ThirdPersonMap.ThirdPersonMap`
Copy full snippet
```
\[/Script/EngineSettings.GameMapsSettings\] GameDefaultMap=/Game/ThirdPerson/Maps/ThirdPersonMap.ThirdPersonMap

Since the `DefaultEngine.ini` file in your project directory supersedes the `BaseEngine.ini` file in your engine directory, the value of `GameDefaultMap` when your project starts up is `/Game/ThirdPerson/Maps/ThirdPersonMap.ThirdPersonMap`.

## Use Configuration Variables in Code

You can automatically apply config variables to `UPROPERTIES` and `USTRUCTS` or manually read them from the config manager.

### Apply Configuration Settings to Variables

#### Automatically

You can define a class to automatically load values from within the config file hierarchy.

##### Section Format

To automatically load a config setting in your module code, format `[Section]` as:

```
`[/Script/ModuleName.ClassName]`
Copy full snippet
```
\[/Script/ModuleName.ClassName\]

where

-   `ModuleName` is the name of the module where the class `ClassName` is defined.
-   `ClassName` is the name of the class where the variable in question is defined.

`ClassName` is the name of the class without the `U` or `A` prefix.

##### Steps to Automatically Load Config Variables

Suppose that you have a module named `MyGameModule` that has a class named `AMyConfigActor`, and that `AMyConfigActor` contains a member variable you want to be able to change in configuration files named `MyConfigVariable`.

1.  Configure which config file category to read in the `UCLASS` declaration. This example uses the `Game` category:
    
    ```
         `UCLASS(config=Game)      class AMyConfigActor : public UObject`
    Copy full snippet
    ```
    UCLASS(config=Game) class AMyConfigActor : public UObject
2.  Mark any member variable in the class that you want to be configurable as `Config`:
    
    ```
         `UPROPERTY(Config)      int32 MyConfigVariable;`
    Copy full snippet
    ```
    UPROPERTY(Config) int32 MyConfigVariable;
3.  Set the preceding variables anywhere in the hierarchy of your chosen config file category. For example, since this example uses the `Game` category, the following configuration can be set within `DefaultGame.ini` in the project directory:
    
    ```
         `[/Script/MyGameModule.MyConfigActor]      MyConfigVariable=3`
    Copy full snippet
    ```
    \[/Script/MyGameModule.MyConfigActor\] MyConfigVariable=3

Your class should look something like this:

```
`UCLASS(config=Game) class AMyConfigActor : public UObject { 	GENERATED_BODY()  	UPROPERTY(Config) 	int32 MyConfigVariable; }`
Copy full snippet
```
UCLASS(config=Game) class AMyConfigActor : public UObject { GENERATED\_BODY() UPROPERTY(Config) int32 MyConfigVariable; }

#### Manually

As previously mentioned, the config system loads all declarations in configuration files whether an actual config variable exists in your C++ code or not. This means that you can query a config variable in any section. For example, say you have the following config in `DefaultGame.ini`:

```
`[MyCategoryName] MyVariable=2`
Copy full snippet
```
\[MyCategoryName\] MyVariable=2

You can read this value into any file you want using the following code:

```
`int MyConfigVariable; GConfig->GetInt(TEXT("MyCategoryName"), TEXT("MyVariable"), MyConfigVariable, GGameIni);`
Copy full snippet
```
int MyConfigVariable; GConfig->GetInt(TEXT("MyCategoryName"), TEXT("MyVariable"), MyConfigVariable, GGameIni);

The value of `MyConfigVariable` in your game code is now 2.

##### Manual Read Options

There are several options for functions to retrieve a variable as well as the configuration file category to retrieve said variable from.

###### Functions

The following functions can be found in `ConfigCacheIni.h` located in `Engine/Source/Runtime/Core/Public/Misc`.

-   `GetBool`
-   `GetInt`
-   `GetInt64`
-   `GetFloat`
-   `GetDouble`
-   `GetString`
-   `GetText`
-   `GetArray`

###### Configuration Categories

The configuration category is identified as `G<CATEGORY>Ini`. For example, the `Engine` category is referenced as `GEngineIni`. The values can be found in `CoreGlobals.h` located in `Engine/Source/Runtime/Core/Public`.

## Edit Configuration Settings

You can change your configuration settings by either:

-   Editing configuration values in an appropriate `.ini` file.
-   Editing configuration values exposed in the **Project Settings** within **Unreal Editor**.

Not all configuration settings are exposed in the **Project Settings** within **Unreal Editor**.

### Save Configuration Settings in Code

You can save your configuration settings from your game code with `SaveConfig`.

#### Save Configuration Example

Suppose that you have the same code as in the example in the section [Steps to Automatically Load Config Variables](/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine#stepstoautomaticallyloadconfigvariables):

```
`UCLASS(config=Game) class AMyConfigActor : public UObject { 	GENERATED_BODY()  	UPROPERTY(Config) 	int32 MyConfigVariable; }`
Copy full snippet
```
UCLASS(config=Game) class AMyConfigActor : public UObject { GENERATED\_BODY() UPROPERTY(Config) int32 MyConfigVariable; }

Somewhere in your code, suppose that you edit this configurable variable:

```
`AMyConfigActor *Settings = GetMutableDefault<AMyConfigActor>(); Settings->MyConfigVariable = 42;`
Copy full snippet
```
AMyConfigActor \*Settings = GetMutableDefault<AMyConfigActor>(); Settings->MyConfigVariable = 42;

You can save this new config value to the config file with absolute path `PathToConfigFile` as:

```
`FString PathToConfigFile; Settings->SaveConfig(CPF_Config, *PathToConfigFile);`
Copy full snippet
```
FString PathToConfigFile; Settings->SaveConfig(CPF\_Config, \*PathToConfigFile);

## Related Console Commands

You can see the value of any configuration setting with the `GetIni` console command. This command helps you to view the value of any configuration setting, including settings for platforms other than the one you are currently using. This command only searches loaded configuration files, so if the setting is in a configuration file that is not loaded, your query might fail.

### Command

```
`GetIni [Platform@]IniFile:Section Key`
Copy full snippet
```
GetIni \[Platform@\]IniFile:Section Key

The `Platform@` argument is optional. If this is not supplied, `Platform` defaults to the platform you are currently using.

### Example

To find the value of the `Protocol` key in the `URL` section of the `Engine` hierarchy on Windows, run:

```
`GetIni Windows@Engine:URL Protocol`
Copy full snippet
```
GetIni Windows@Engine:URL Protocol

## Override Configuration from the Command-line

Unreal Engine provides a mechanism by which you can override configuration settings through command-line arguments.

Command-line overrides do not work with arrays.

### Specific Config File Properties

#### Command

```
`-ini:<CATEGORY>:[SECTION_1]:<KEY_1>=<VALUE_1>,[SECTION_2]:<KEY_2>=<VALUE_2>,...`
Copy full snippet
```
\-ini:<CATEGORY>:\[SECTION\_1\]:<KEY\_1>=<VALUE\_1>,\[SECTION\_2\]:<KEY\_2>=<VALUE\_2>,...

#### Description

Override the specified `KEY` with the provided `VALUE` contained in the given `SECTION` of the configuration file `CATEGORY`. For a full list of available configuration file categories, see the [Configuration File Categories](/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine#configurationfilecategories) section of this page.

#### Example

```
`-ini:Engine:[/Script/Engine.Engine]:bSmoothFrameRate=False,[TextureStreaming]:PoolSize=100`
Copy full snippet
```
\-ini:Engine:\[/Script/Engine.Engine\]:bSmoothFrameRate=False,\[TextureStreaming\]:PoolSize=100

Override the value of `bSmoothFrameRate` contained in the `[/Script/Engine.Engine]` section of the `Engine` category hierarchy, no matter the previous value. Same for the `PoolSize`.

### Default File in Category

#### Command

```
`-Def<CATEGORY>Ini=<FILE_NAME>`
Copy full snippet
```
\-Def<CATEGORY>Ini=<FILE\_NAME>

#### Description

Override the `Default<CATEGORY>.ini` file with the file `<FILE_NAME>` where `CATEGORY` is the specific configuration file type you wish to override. For a full list of available configuration file categories, see the [Configuration File Categories](/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine#configurationfilecategories) section of this page.

#### Example

```
`-DefGameIni=FooGame.ini`
Copy full snippet
```
\-DefGameIni=FooGame.ini

`FooGame.ini` overrides the `DefaultGame.ini` configuration file. For a full list of available configuration file categories, see the [Configuration File Categories](/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine#configurationfilecategories) section of this page.

### All Files in a Category

#### Command

```
`-<CATEGORY>Ini=<FILE_NAME>`
Copy full snippet
```
\-<CATEGORY>Ini=<FILE\_NAME>

#### Description

Override all configuration files in the given `CATEGORY`. For a full list of available configuration file categories, see the [Configuration File Categories](/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine#configurationfilecategories) section of this page.

#### Example

```
`-EngineIni=FooEngine.ini`
Copy full snippet
```
\-EngineIni=FooEngine.ini

`FooEngine.ini` overrides all other `*Engine.ini` files. For a full list of available configuration file categories, see the [Configuration File Categories](/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine#configurationfilecategories) section of this page.

### Config File with Matching Suffix

#### Command

```
`-iniFile=<PATH/TO/FILE_NAME>`
Copy full snippet
```
\-iniFile=<PATH/TO/FILE\_NAME>

#### Description

Override the config file with the matching suffix path.

This command requires that your path's suffix directory structure match the engine directory structure for configuration files.

#### Example

```
`-iniFile=C:/MyAdditionalConfigFiles/Engine/Config/BaseEngine.ini`
Copy full snippet
```
\-iniFile=C:/MyAdditionalConfigFiles/Engine/Config/BaseEngine.ini

`C:/MyAdditionalConfigFiles/Engine/Config/BaseEngine.ini` overrides the configuration file `<PROJECT_DIRECTORY>/Engine/Config/BaseEngine.ini`. For a full list of available configuration file categories, see the [Configuration File Categories](/documentation/en-us/unreal-engine/configuration-files-in-unreal-engine#configurationfilecategories) section of this page.

### All Config Files

#### Command

```
`-IniBootstrap=<FILE_NAME>`
Copy full snippet
```
\-IniBootstrap=<FILE\_NAME>

#### Description

Override all config files being loaded and parsed. Read-only.

#### Example

```
`-IniBootstrap=Foo.ini`
Copy full snippet
```
\-IniBootstrap=Foo.ini

`Foo.ini` is the only configuration file loaded, nothing else.

## Set Console Variables in Configuration Files

Configuration Files provide another mechanism for specifying console variables. Some console variables can be set in general configuration categories whereas others should be set in specific configuration categories. Generally, console variables are set in the `[ConsoleVariables]` section in `DefaultEngine.ini` within your project directory.

### Specific Categories

The following table describes the specific categories of console variables that should be set in particular sections:

| **Type** | **Section** | **Description** |
| --- | --- | --- |
| Rendering | `[/Script/Engine.RendererSettings]` | Any console variable starting with `r.` |
| Rendering Override | `[/Script/Engine.RendererOverrideSettings]` | Specifically for the console variable `r.SupportAllShaderPermutations` |
| Streaming | `[/Script/Engine.StreamingSettings]` | Any console variable starting with `s.` |
| Garbage Collection | `[/Script/Engine.GarbageCollectionSettings]` | Any console variable starting with `gc.` |
| Network Settings | `[/Script/Engine.NetworkSettings]` | Only for the console variables `n.VerifyPeer`, `p.EnableMultiplayerWorldOriginRebasing`, and `NetworkEmulationProfiles`. |
| Cooker Settings | `[/Script/UnrealEd.CookerSettings]` | Any console variable starting with `cook.` |

## Useful Source Files for More Information

The following engine files provide more information about the config system and its components:

-   ConfigCacheIni
-   CoreGlobals
-   ConfigHierarchy
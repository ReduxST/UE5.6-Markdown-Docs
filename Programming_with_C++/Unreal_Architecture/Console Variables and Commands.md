# Console Variables and Commands

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/console-variables-cplusplus-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/console-variables-cplusplus-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:08

---

A **Console Command** is a string sent to the engine, often typed in by the user at the in-game console, that the engine recognizes and can react to in some way. For example, a console commands can trigger a console / log response, change a variables internal state, and so on. A **Console Variable** can be used to store state information that can be viewed or changed through the console. The in-game console supports auto-completion and enumeration for console commands and console variables that have been registered with the **Console Manager**. The console manager also provides a registry for you to see all registered console commands and console variables as well as information about their purpose. For these reasons, you should avoid the old `Exec` interface and instead define and register your console variables and console commands through the console manager.

## What is a Console Variable?

A Console Variable is a variable of a simple data type (for example, `float`, `int32`, `FString`) that has an engine-wide state. The user can read and write to the state. The Console Variable is identified by a unique name, and the in-game console will assist the user with auto-completion while typing into the console. Some examples:

| **User console input** | **Console output** | **Description** |
| --- | --- | --- |
| `MyConsoleVar` | `MyConsoleVar = 0` | The current state of the variable is printed into the console. |
| `MyConsoleVar 123` | `MyConsoleVar = 123 LastSetBy: Constructor` | The state of the variable is changed and the new state printed into the console. |
| `MyConsoleVar ?` | `Possibly multi line help text.` | Print the console variable help text into the console. |

## Console Variable and Console Command Reference

For a list of available console variables, see the [Console Variable Reference](/documentation/en-us/unreal-engine/unreal-engine-console-variables-reference) page.

For a list of available console commands, see the [Console Command Reference](/documentation/en-us/unreal-engine/unreal-engine-console-commands-reference) page.

## Creating / Registering a Console Variable

All Console Variables are registered when the engine is created. The following example has been taken from engine code:

```
	`static TAutoConsoleVariable<int32> CVarRefractionQuality( 		TEXT("r.RefractionQuality"), 		2, 		TEXT("Defines the distortion/refraction quality, adjust for quality or performance.\n") 		TEXT("<=0: off (fastest)\n") 		TEXT("  1: low quality (not yet implemented)\n") 		TEXT("  2: normal quality (default)\n") 		TEXT("  3: high quality (e.g. color fringe, not yet implemented)"), 		ECVF_Scalability | ECVF_RenderThreadSafe 	);`
Copy full snippet
```
static TAutoConsoleVariable<int32> CVarRefractionQuality( TEXT("r.RefractionQuality"), 2, TEXT("Defines the distortion/refraction quality, adjust for quality or performance.\\n") TEXT("<=0: off (fastest)\\n") TEXT(" 1: low quality (not yet implemented)\\n") TEXT(" 2: normal quality (default)\\n") TEXT(" 3: high quality (e.g. color fringe, not yet implemented)"), ECVF\_Scalability | ECVF\_RenderThreadSafe );

Here we register a Console Variable of the type `int32`, with the name `r.RefractionQuality`, the default value of `2` and some multi-line help text and flags. The help text is shown when the user types "?" after the Console Variable's name. The names and descriptions of flags available (from the `EConsoleVariableFlags` enumerated type) can be found on the [`EConsoleVariableFlags` API Reference page.](/documentation/en-us/unreal-engine/API/Runtime/Core/HAL/EConsoleVariableFlags).

There are other entries in the `EConsoleVariableFlags` enumerated type, but all other flags are intended for internal use only.

If needed, you also can generate a console variable inside a function:

```
	`IConsoleManager::Get().RegisterConsoleVariable( 		TEXT("r.RefractionQuality"), 		2, 		TEXT("Defines the distortion/refraction quality, adjust for quality or performance.\n") 		TEXT("<=0: off (fastest)\n") 		TEXT("  1: low quality (not yet implemented)\n") 		TEXT("  2: normal quality (default)\n") 		TEXT("  3: high quality (e.g. color fringe, not yet implemented)"), 		ECVF_Scalability | ECVF_RenderThreadSafe 	);`
Copy full snippet
```
IConsoleManager::Get().RegisterConsoleVariable( TEXT("r.RefractionQuality"), 2, TEXT("Defines the distortion/refraction quality, adjust for quality or performance.\\n") TEXT("<=0: off (fastest)\\n") TEXT(" 1: low quality (not yet implemented)\\n") TEXT(" 2: normal quality (default)\\n") TEXT(" 3: high quality (e.g. color fringe, not yet implemented)"), ECVF\_Scalability | ECVF\_RenderThreadSafe );

`IConsoleManager::Get()` is the global access point. There you can register a Console Variable or find an existing one. The first parameter is the name of the Console Variable. The second parameter is the default value, and depending on the type of this constant, a different Console Variable type is created: int, float, or string (!FString). The next parameter defines the Console Variable help text.

It is also possible to register a reference to an existing variable. This is convenient and fast but bypasses multiple features (for example, thread safety, callback, sink, cheat) so we suggest to avoiding this method. Here is an example:

```
	`FAutoConsoleVariableRef CVarVisualizeGPUSimulation( 		TEXT("FX.VisualizeGPUSimulation"), 		VisualizeGPUSimulation, 		TEXT("Visualize the current state of GPU simulation.\n") 		TEXT("0 = off\n") 		TEXT("1 = visualize particle state\n") 		TEXT("2 = visualize curve texture"), 		ECVF_Cheat 		);`
Copy full snippet
```
FAutoConsoleVariableRef CVarVisualizeGPUSimulation( TEXT("FX.VisualizeGPUSimulation"), VisualizeGPUSimulation, TEXT("Visualize the current state of GPU simulation.\\n") TEXT("0 = off\\n") TEXT("1 = visualize particle state\\n") TEXT("2 = visualize curve texture"), ECVF\_Cheat );

Here they type is deducted from the variable type.

## Getting the State of a Console Variable

Getting the state of a Console Variables created with **RegisterConsoleVariableRef** can be done efficiently by using the variable that it was registered with. For example:

```
	`// only needed if you are not in the same cpp file 	extern TAutoConsoleVariable<int32> CVarRefractionQuality;  	// get the value on the game thread 	int32 MyVar = CVarRefractionQuality.GetValueOnGameThread();`
Copy full snippet
```
// only needed if you are not in the same cpp file extern TAutoConsoleVariable<int32> CVarRefractionQuality; // get the value on the game thread int32 MyVar = CVarRefractionQuality.GetValueOnGameThread();

Using Getter functions (that is,!GetInt(), !GetFloat(), !GetString()) to determine a Console Variable's state results in a slightly slower implementation (virtual function call, possibly cache miss, and so on). For best performance you should use same type the variable was registered with. To get the pointer to the variable, you can either store the return argument of the register function or call **FindConsoleVariable** just before you need the variable. For example:

```
	`static const auto CVar = IConsoleManager::Get().FindConsoleVariable(TEXT("TonemapperType")); 	int32 Value = CVar->GetInt();`
Copy full snippet
```
static const auto CVar = IConsoleManager::Get().FindConsoleVariable(TEXT("TonemapperType")); int32 Value = CVar->GetInt();

The static there ensures the name search (implemented as map) is only done the first time this code is called. This is correct as the variable will never move and only gets destructed on engine shutdown.

## How to Track Console Variable Changes

If you want to execute some custom code if a Console Variable changes, you have 3 methods you can choose from.

Often the simplest method is the best: You can store the old state in your subsystem and check each frame if they differ. Here you control when this happens very freely; for example, on the render thread, game thread, or streaming thread, before / after tick or rendering. When you detect the difference, you copy the console variable state and do your custom code. For example:

```
	`void MyFunc() 	{ 		int GBufferFormat = CVarGBufferFormat.GetValueOnRenderThread();  		if(CurrentGBufferFormat != GBufferFormat) 		{ 			CurrentGBufferFormat = GBufferFormat;  			// custom code 		} 	}`
Copy full snippet
```
void MyFunc() { int GBufferFormat = CVarGBufferFormat.GetValueOnRenderThread(); if(CurrentGBufferFormat != GBufferFormat) { CurrentGBufferFormat = GBufferFormat; // custom code } }

You also can register a console variable sink. For example:

```
	`static void MySinkFunction() 	{ 		bool bNewAtmosphere = CVarAtmosphereRender.GetValueOnGameThread() != 0;  		// by default we assume the state is true 		static bool GAtmosphere = true;  		if (GAtmosphere != bNewAtmosphere) 		{ 			GAtmosphere = bNewAtmosphere;  			// custom code 		} 	}  	FAutoConsoleVariableSink CMyVarSink(FConsoleCommandDelegate::CreateStatic(&MySinkFunction));`
Copy full snippet
```
static void MySinkFunction() { bool bNewAtmosphere = CVarAtmosphereRender.GetValueOnGameThread() != 0; // by default we assume the state is true static bool GAtmosphere = true; if (GAtmosphere != bNewAtmosphere) { GAtmosphere = bNewAtmosphere; // custom code } } FAutoConsoleVariableSink CMyVarSink(FConsoleCommandDelegate::CreateStatic(&MySinkFunction));

The sink is called at a specific point on the main thread before rendering. The function does not get the console variable name/pointer as this often would lead to the wrong behavior. If multiple console variables (for example, r.SceneColorFormat, r.GBufferFormat) should all trigger the change, it is best to call the code after all have been changed, not one after another.

The last method, using the callback, you should avoid as it can cause problems if not used carefully:

-   A cycle can cause a deadlock (we could prevent the deadlock but which callback to favour is not clear).
-   The callback can come back at any point in time whenever **!Set()** is getting called. You code has to work in all cases (during init, during serialization). You can assume it is always on the main thread side.

We do not recommend using this method unless you cannot solve it with the other methods mentioned.

For example:

```
	`void OnChangeResQuality(IConsoleVariable* Var) 	{ 		SetResQualityLevel(Var->GetInt()); 	}  	CVarResQuality.AsVariable() 		->SetOnChangedCallback(FConsoleVariableDelegate::CreateStatic(&OnChangeResQuality));`
Copy full snippet
```
void OnChangeResQuality(IConsoleVariable\* Var) { SetResQualityLevel(Var->GetInt()); } CVarResQuality.AsVariable() ->SetOnChangedCallback(FConsoleVariableDelegate::CreateStatic(&OnChangeResQuality));

## Intended Console Variable Behavior and Style

-   Console variable should reflect the user input, not necessarily the state of the system (e.g. !MotionBlur 0/1, some platforms might not support it). The variable state should not be changed by code. Otherwise the user might wonder if they mistyped because the variable does not have the state they specified or they might not be able to change a console variable because of the state of some other variable.
-   Always provide a good help explaining what the variable is used for and what values make sense to specify.
-   Most console variables are intended for development only so specifying the `ECVF_Cheat` flag early would be a good idea. Even better might be to compile out the feature using defines (for example, #if !(UE\_BUILD\_SHIPPING || UE\_BUILD\_TEST)).
-   The variable name should be as minimal as possible while being descriptive, negating meaning should be avoided (for example, bad names would be !EnableMotionBlur, !MotionBlurDisable, MBlur, !HideMotionBlur). Use upper and lower case to make the name easier to read and consistent (for example, !MotionBlur).
-   For indentation, you can assume fixed width font (non proportional) output.
-   It is important to register the variable during engine initialization so that auto completion and !DumpConsoleCommands and !Help can work.

Please read `IConsoleManager.h` for find more details on this.

## Loading Console Variables

On engine startup, the state of Console Variables can be loaded from the file **Engine/Config/ConsoleVariables.ini**. This place is reserved for the local developer - it should not be used for project settings. More details can be found in the file itself:

```
	`; This file allows you to set console variables on engine startup (In undefined order). 	; Currently there is no other file overriding this one. 	; This file should be in the source control database (for the comments and to know where to find it) 	; but kept empty from variables. 	; A developer can change it locally to save time not having to type repetitive 	; console variable settings. The variables need to be in the section called [Startup]. 	; Later on we might have multiple named sections referenced by the section name. 	; This would allow platform specific or level specific overrides. 	; The name comparison is not case sensitive and if the variable does not exist, it is ignored. 	; 	; Example file content: 	; 	; [Startup] 	; FogDensity = 0.9 	; ImageGrain = 0.5 	; FreezeAtPosition = 2819.5520 416.2633 75.1500 65378 -25879 0  	[Startup]`
Copy full snippet
```
; This file allows you to set console variables on engine startup (In undefined order). ; Currently there is no other file overriding this one. ; This file should be in the source control database (for the comments and to know where to find it) ; but kept empty from variables. ; A developer can change it locally to save time not having to type repetitive ; console variable settings. The variables need to be in the section called \[Startup\]. ; Later on we might have multiple named sections referenced by the section name. ; This would allow platform specific or level specific overrides. ; The name comparison is not case sensitive and if the variable does not exist, it is ignored. ; ; Example file content: ; ; \[Startup\] ; FogDensity = 0.9 ; ImageGrain = 0.5 ; FreezeAtPosition = 2819.5520 416.2633 75.1500 65378 -25879 0 \[Startup\]

You also can put the settings in **Engine/Config/BasEngine.ini**, for example:

```
	`[SystemSettings] 	r.MyCvar = 2  	[SystemSettingsEditor] 	r.MyCvar = 3`
Copy full snippet
```
\[SystemSettings\] r.MyCvar = 2 \[SystemSettingsEditor\] r.MyCvar = 3

Setting can also come from **Script/Engine.RendererSettings**. These project settings are exposed like this:

```
	`UPROPERTY(config, EditAnywhere, Category=Optimizations, meta=( 		ConsoleVariable="r.EarlyZPassMovable",DisplayName="Movables in early Z-pass", 		ToolTip="Whether to render movable objects in the early Z pass. Need to reload the level!")) 		uint32 bEarlyZPassMovable:1;`
Copy full snippet
```
UPROPERTY(config, EditAnywhere, Category=Optimizations, meta=( ConsoleVariable="r.EarlyZPassMovable",DisplayName="Movables in early Z-pass", ToolTip="Whether to render movable objects in the early Z pass. Need to reload the level!")) uint32 bEarlyZPassMovable:1;

Those settings can be changed in the editor UI. Project settings should not intermix with scalability settings (to prevent priority issues).

Other settings can come from the Scalability feature. Look at **Config/BaseScalability.ini** or the Scalability documentation for more info.

## Command line

The command line allows to set console variables, call console commands or exec commands. For example:

```
	`UE4Editor.exe GAMENAME -ExecCmds="r.BloomQuality 12,vis 21,Quit"`
Copy full snippet
```
UE4Editor.exe GAMENAME -ExecCmds="r.BloomQuality 12,vis 21,Quit"

Here we execute 3 commands. Note that setting a console variable this way requires you to omit the '=' you would need in an ini file.

## Priority

Console variables can be overridden from various sources, for example user / editor / project settings, command line, consolevariables.ini, and so on. To be able to reapply some settings (for example, project settings can be changed in the editor UI) while keeping the specified overrides (for example, from the command line), we introduced a priority. Now all settings can be applied in any order.

see IConsoleManager.h:

```
	`// lowest priority (default after console variable creation) 	ECVF_SetByConstructor =			0x00000000, 	// from Scalability.ini 	ECVF_SetByScalability =			0x01000000, 	// (in game UI or from file) 	ECVF_SetByGameSetting =			0x02000000, 	// project settings 	ECVF_SetByProjectSetting =		0x03000000, 	// per device setting 	ECVF_SetByDeviceProfile =		0x04000000, 	// per project setting 	ECVF_SetBySystemSettingsIni =	0x05000000, 	// consolevariables.ini (for multiple projects) 	ECVF_SetByConsoleVariablesIni = 0x06000000, 	// a minus command e.g. -VSync 	ECVF_SetByCommandline =			0x07000000, 	// least useful, likely a hack, maybe better to find the correct SetBy... 	ECVF_SetByCode =				0x08000000, 	// editor UI or console in game or editor 	ECVF_SetByConsole =				0x09000000,`
Copy full snippet
```
// lowest priority (default after console variable creation) ECVF\_SetByConstructor = 0x00000000, // from Scalability.ini ECVF\_SetByScalability = 0x01000000, // (in game UI or from file) ECVF\_SetByGameSetting = 0x02000000, // project settings ECVF\_SetByProjectSetting = 0x03000000, // per device setting ECVF\_SetByDeviceProfile = 0x04000000, // per project setting ECVF\_SetBySystemSettingsIni = 0x05000000, // consolevariables.ini (for multiple projects) ECVF\_SetByConsoleVariablesIni = 0x06000000, // a minus command e.g. -VSync ECVF\_SetByCommandline = 0x07000000, // least useful, likely a hack, maybe better to find the correct SetBy... ECVF\_SetByCode = 0x08000000, // editor UI or console in game or editor ECVF\_SetByConsole = 0x09000000,

In some cases, you might see this log printout:

```
	`Console variable 'r.MyVar' wasn't set (Priority SetByDeviceProfile < SetByCommandline)`
Copy full snippet
```
Console variable 'r.MyVar' wasn't set (Priority SetByDeviceProfile < SetByCommandline)

It might be intended (for example, the command line forces a user setting) or caused by some code issue. The priority is also helpful to see who set the variable the last time. You can get this information when getting the console variable state. e.g.

```
	`> r.GBuffer  	r.GBuffer = "1"      LastSetBy: Constructor`
Copy full snippet
```
\> r.GBuffer r.GBuffer = "1" LastSetBy: Constructor

## Unregistering Console Variables

The **UnregisterConsoleVariable** method allows you to remove the Console Variable. At least, this is what is happening from the user's perspective. The variable is still kept (with the unregistered flags) to not crash when pointers access the data. If a new variable is registered with the same name, the old variable is restored and flags get copied from the new variable. This way DLL loading and unloading can work even without losing the variable state. This will not work for console variable references.
# Upgrading the Lyra Starter Game to the Latest Engine Release

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/upgrading-the-lyra-starter-game-to-the-latest-engine-release-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/upgrading-the-lyra-starter-game-to-the-latest-engine-release-in-unreal-engine)  
**Processed:** 2025-06-14 16:57:48

---

We update the **Lyra Starter Game** with each major release of the **Unreal Engine (UE)**. These updates take advantage of the newest features of the engine and fix issues specific to Lyra. This page documents Lyra's major changes for each engine version and includes information that can help you upgrade existing games to the newest release of Unreal Engine.

## Upgrading To the Latest Engine Release

Games that include C++ code, including Lyra, need manual updates to work correctly with new major releases of the Unreal engine. For example, major engine upgrades from 5.0.x to 5.1.x may deprecate older features or settings, and may change existing functions and variables used by your project. Therefore, some game-specific code and data needs to be updated to work correctly after the upgrade. Using Lyra as an example, follow the steps below to update a game:

1.  Read the **release notes** for the new engine version, ensuring you keep track of any major changes and upgrade notes that may affect your game.
    
2.  Download and [install the new version of the engine](/documentation/404) You can install this to a different directory than your current engine version to compare the older and newer versions of the game.
    
3.  Download and install the new version of the [Lyra Starter Game sample](https://www.fab.com/listings/93faede1-4434-47c0-85f1-bf27c0820ad0) that matches the new version of the engine so you can see how it was updated. If you install this to a different directory, you can compare it to the old version.
    
4.  Refer to the [Unreal Engine 5 migration guide](/documentation/en-us/unreal-engine/unreal-engine-5-migration-guide) to check compatibility with the newest version of the engine.
    
5.  Load your project in your C++ code editor and attempt to compile it. This will likely fail.
    
6.  Fix any deprecation warnings by using the instructions included in the deprecation message.
    
7.  For any errors about invalid or missing classes or structs, you will need to add a new `#include` line to the top of the file. If you are using Visual Studio, you can navigate to **Edit** > **Find and Replace** > **Find In Files** then search for the missing type name. Look for the header file that defines that type and add a new `#include`.
    
8.  For errors about virtual function overrides, you will need to update the parameters of your overridden function in both the header and `.cpp` file.
    
9.  For any errors about invalid variables on a class or struct, you will need to use a different method of accessing that variable. This is usually solved by calling an accessor function like `Get()` or `GetVariableName(`) that will return the actual value.
    
10.  If you are unsure about how to fix an error, search the **release notes** or reach out to the [community forums](https://forums.unrealengine.com/) for more information.
    

By comparing the older and newer versions of the Lyra Starter Game, you can see how to handle complex changes to the source code. The version-specific information below will help you upgrade your game if it includes any code or content from Lyra.

## Unreal Engine 5.3

In Unreal Engine 5.3, the Lyra Sample Game continued to receive support. It now takes advantage of the newest features and fixes added to the engine.

### Upgrade Notes for 5.3:

-   Some object pointer variables were changed to use `TObjectPtr`.
    
-   Several C++ lambdas were updated to fix warnings about unsafe usage.
    
-   Some header includes were updated to remove unnecessary paths.
    

### Improvements in 5.3:

-   Lyra now includes experimental Client Replay Support. On the platforms that support them, Saving replays can be enabled in the settings menu and then played back from the main menu. Saved replays are currently missing some visual and sound effects. Some platforms may not support Client Replay Support.
    
-   The shared gameplay settings now inherit from the new engine `LocalPlayerSaveGame` class and will not be loaded until platform login has completed successfully.
    
-   The ShooterExplorer game feature plugin includes some in-progress experimental content that tests open world and AI systems.
    
-   The Lyra-specific input settings were updated to handle improvements to enhanced input.
    

### Bug Fixes in 5.3:

-   Fixed issues with Gameplay Abilities and customized character parts for NPC characters that are placed directly in a map.
    
-   The SyncMarker, FootFX and FootstepEffectTag anim modifiers have been updated.
    
-   Fixed bug where touch-based joysticks affected input while hidden.
    
-   Fixed several networking bugs that were discovered during replay testing.
    
-   The health change callbacks on the LyraHealthComponent now include the instigator when it is available.
    

## Unreal Engine 5.2

In Unreal Engine 5.2, the Lyra Sample Game continued to receive support. It now takes advantage of the newest features and fixes added to the engine.

### Upgrade Notes for 5.2

-   The engine headers were reorganized to improve compile time. This improvement revealed cases of missing headers in Lyra. For example, `CommonUserSubsystem.h` needed to be changed to include `OnlineError.h`
    
-   The 5.1 version of Lyra had optional support for the **Iris** networking system, which is now compiled into the engine by default. Compiling an older version of Lyra in 5.2 will cause networking linker errors, which can be fixed by adding `"SetupIrisSupport(Target);"` to the `LyraGame.build.cs`
    

### Improvements in 5.2

-   The `LyraGame` gameplay tags were changed to use the tags located inside the `LyraGameplayTags` namespace. This makes it possible to use those tags during object initialization.
    
-   The map transfer at the end of a match (or when using the PlayNextGame console command cheat) now uses Seamless Travel.
    
-   Lyra now has experimental support for local multiplayer. To activate local multiplayer, press the start button on a second connected controller of the same type or click the **Add Player** button on the main menu.
    
-   Improved support for dedicated servers. A packaged LyraServer or editor game run with the command `-server` will start hosting a default map using the code in `ALyraGameMode::TryDedicatedServerLogin`.
    
-   Added networking support for Replication Graph, Iris, and packet encryption. This is disabled by default.
    
-   Changed haptic feedback to include Input Device properties such as trigger resistance and controller colors on some platforms.
    
    *Your controller color will match your team color (red or blue).* Weapon instances can have device properties added to them when they are equipped. For example, the shotgun will have heavy trigger resistance on the PlayStation DualSense controller while it is equipped.
    
-   Packaging Lyra will now create multiple `.pak` files. This is setup by using Primary Asset Labels inside the game feature plugins.
    

### Bug Fixes in 5.2

-   Many networking and UI issues were fixed while supporting seamless travel and local multiplayer.
    
-   Animation stutter during character movement has been fixed. This was originally fixed for 5.1.1.
    
-   Fixed several issues with the LyraClient build target. It can now join dedicated servers
    
-   Fixed the default game target for build scripts to be the LyraGame.
    
-   Reduced frequency of `EditorValidator_SourceControl` warnings about assets with unknown version control status.
    

## Unreal Engine 5.1

In Unreal Engine 5.1, the Lyra Sample Game was updated to fix issues with the sample and take advantage of the newest features added to the engine.

### Upgrade Notes for 5.1

-   Several engine headers were reorganized to improve compile times. This exposed some issues with the Lyra source files. These issues can be fixed by adding a `#pragma once` line to the headers missing them and adding lines like `#include EditorStyle.h` to source files that have errors about missing types.
    
-   Several raw pointer properties in the gameplay framework classes were changed to use `TObjectPtr` or `TWeakObjectPtr`. Any code that needs a raw pointer can be fixed by adding a call to the `Get()` function.
    
-   The `ENSURE_ABILITY_IS_INSTANTIATED_OR_RETURN` macro was removed from `GameplayAbility.h`. This macro can be copied from `GameplayAbility.cpp` to other ability source code files.
    
-   Several virtual functions related to game feature plugins were modified to add new parameters. Overridden functions in classes like `ULyraGameFeaturePolicy` will need to be updated.
    
-   The geometry mesh Blueprint `Tools/BakedGeneratedMeshSystem/BaseClasses/BakedGeneratedMeshActor` was updated for 5.1. Although the 5.0 asset will continue to function, Nanite settings will not be configured properly unless the 5.1 version is used.
    

### Improvements in 5.1

-   The pawn initialization flow in the `LyraHeroComponent` and `LyraPawnExtensionComponent` was rewritten to use the new `IGameFrameworkInitStateInterface` and the Init State system on the `GameFrameworkComponentManager`. This fixes several race conditions in network replication and is easier to extend with new feature-specific components.
    
-   Added Android device profiles for devices with different capabilities, and adjusted other platform settings.
-   Added UI for loading common maps to the editor toolbar.
-   Added basic handling for multiplayer game invites using Epic Online Services.
-   Added prototype and test content into the new ShooterExplorer and ShooterTest plugins.
-   Improved the keybinding screen with a warning screen when binding a key that is already assigned.

### Bug Fixes in 5.1

-   The `ShouldEnableAllGameFeaturePlugins` function in `LyraGame.Target.cs` was changed to return `false`, which means that game feature plugins are now enabled like normal plugins. This fixes plugins to work the same for both custom-compiled and launcher-installed versions of the engine.
-   Fixed an issue where running Lyra would change the keybind for exiting Play In Editor in other projects.
-   Changed abilities to properly use the Healing and Damage attributes instead of applying a negative modifier to Health.
-   Updated code and Blueprints to use the new PlatformUser and InputDeviceId types instead of deprecated controller ids.

## Unreal Engine 5.0

The 5.0 version of Lyra Sample Game was updated along with 5.0.2 to fix several bugs in the original release. These fixes are included in all later releases of the sample.

### Bug Fixes in 5.0.2

-   Fixed automation scripts to handle different installation directories.
-   Fixed the inverted mouse setting.
-   Updated mannequin retargeting and control rig assets.
-   Updated antialiasing settings in mobile device profiles.
-   Added missing editor icons.
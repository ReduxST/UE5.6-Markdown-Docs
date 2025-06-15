# Frequently Asked Questions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unity-to-unreal-engine-frequently-asked-questions-faq](https://dev.epicgames.com/documentation/en-us/unreal-engine/unity-to-unreal-engine-frequently-asked-questions-faq)  
**Processed:** 2025-06-14 16:55:52

---

### How do I load my last project automatically?

You can configure Unreal Engine to load the last project you were working on automatically on startup. When you open a project from the Epic Launcher, enable the **Always Load Last Project on Startup** option on the Unreal Engine start screen.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4b09e8e-21c1-467c-9156-2c7c1290df01/always-load-last-project-at-startup.png)

### Where do I set input bindings for my game?

In Unity, you used the Input Manager settings for your project to set up default bindings.

In Unreal Engine, you configure input bindings from the **Project Settings** window, in the **Input** category. In this window, you can add various buttons (actions) and analog controls (axes). Give each control a name and default binding. Once you do that, you can get callbacks to your game's Pawn when input events are triggered.

To learn more about how to set up input for your Unreal Engine project, refer to the [Input](/documentation/en-us/unreal-engine/input-in-unreal-engine) page.

If your project requires more advanced input features, like complex input handling or runtime control remapping, consider using the **Enhanced Input** plugin. For more information, see [Enhanced Input](/documentation/en-us/unreal-engine/enhanced-input-in-unreal-engine).

### How do I change the starting scene of my project?

By default, Unreal Engine loads the default Level of your project when you open it. You can change this behavior in the **Editor Preferences** window (main menu: **Edit > Editor Preferences**), in the **General > Loading & Saving** category.

### How do I run my game?

There are several ways to play-test (run) your game:

-   Directly in the Unreal Editor, by clicking the **Play** button on the **Main Toolbar**.
    
-   As a standalone process, by clicking the **Platforms** button on the **Main Toolbar**, then selecting your machine from the drop-down list. Note that this will first build an executable for your platform; for example, if you are working on a Windows machine, this will build a Windows executable.
    
-   On a different platform (for example, a mobile device or web browser), by clicking the **Platforms** button on the **Main Toolbar**, then selecting the platform you want to run your game on. Note that you will need to install all required dependencies first.
    

To learn more about running your Unreal Engine game on different platforms, refer to the following pages:

-   [Playing and Simulating](/documentation/en-us/unreal-engine/playing-and-simulating-in-unreal-engine)
    
-   [Managing Platforms in Unreal Editor](/documentation/en-us/unreal-engine/using-the-platforms-dropdown-in-unreal-editor)
    

### What units are these?

In Unity, the primary unit of measurement is one meter. In Unreal Engine, the primary unit of measurement is one centimeter.

So, if you move something 1 unit (meter) in Unity, that is equivalent to moving something 100 units (centimeters) in Unreal Engine.

If you want to move something 2 feet in Unity, that would be 0.61units (meters). In Unreal Engine, the equivalent is 61 units (centimeters).

### Which way is up in Unreal Engine's coordinate system?

Both Unity and Unreal Engine use a left-handed coordinate system, but the axes are named differently. In Unreal Engine, positive X is "forward", positive Y is "right" and positive Z is "up".

For more information, see [Coordinate System and Spaces](/documentation/en-us/unreal-engine/coordinate-system-and-spaces-in-unreal-engine).

### How do I see Log Output from my game?

Click the **Output Log** button in the **bottom toolbar**.

### How do I throw exceptions?

Unlike Unity, Unreal Engine does not use exception handling. Instead, use the `check()` function to trigger a critical assertion error. You can pass in an error message. If you want to report an error but not halt the program, use `ensure()` instead. This will log an error with a full call stack, but program execution will continue. If you had a debugger attached, both functions will break into the debugger.

### Where is the .NET Framework?

Unlike Unity, Unreal Engine does not use the .NET framework. Unreal Engine has its own set of container classes and libraries. Below is a list of common container comparisons:

| .Net Framework | Unreal Engine |
| --- | --- |
| String | [FString](https://docs.unrealengine.com/latest/INT/API/API/Runtime/Core/Containers/FString), [FText](https://docs.unrealengine.com/latest/INT/API/API/Runtime/Core/Internationalization/FText) |
| List | [TArray](https://docs.unrealengine.com/latest/INT/API/API/Runtime/Core/Containers/TArray) |
| Dictionary | [TMap](https://docs.unrealengine.com/latest/INT/API/API/Runtime/Core/Containers/TMap) |
| HashSet | [TSet](https://docs.unrealengine.com/latest/INT/API/API/Runtime/Core/Containers/TSet) |

You can learn more about other Unreal Engine containers [here](/documentation/en-us/unreal-engine/API/Runtime/Core/Containers).

### Does Unreal Engine automatically reload code changes?

Yes! You can leave the editor open while you write code. Start a compile from Visual Studio after you have finished editing code, and the editor will "hot reload" your changes automatically.
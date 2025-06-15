# Writing Code in Unreal Engine

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/writing-code-in-unreal-engine-for-unity-developers](https://dev.epicgames.com/documentation/en-us/unreal-engine/writing-code-in-unreal-engine-for-unity-developers)  
**Processed:** 2025-06-14 17:05:19

---

## Setup

### C++

To write C++ code in Unreal Engine (UE), download [Visual Studio](https://visualstudio.microsoft.com/downloads/) on Windows, or [install Xcode](https://itunes.apple.com/us/app/xcode/id497799835?mt=12) on macOS. When you create a new C++ project, UE will automatically create Visual Studio project files for you.

There are two ways to access Visual Studio from your UE project:

-   In the **Content Browser**, **double-click** a C++ class to open it in Visual Studio.
-   From the main menu, go to **Tools** **\>** **Open Visual Studio**. This option only appears if your project contains at least one C++ class.

A critical difference in UE: You will sometimes have to manually refresh your Visual Studio project files (for example, after downloading a new version of UE, or when manually making changes to source file locations on disk.) You can do this in two ways:

-   From UE's main menu, go to **Tools > Refresh Visual Studio Project**.
-   **Right-click** the **.uproject** file in your project's directory and select **Generate Visual Studio project files**.

See [Development Setup](/documentation/en-us/unreal-engine/setting-up-your-development-environment-for-cplusplus-in-unreal-engine) for more detailed information.

### Blueprint

You only need UE to use Blueprint scripting. All the features you need are built into Unreal Editor.

## Writing Event Functions

If you previously worked with MonoBehaviors, you are familiar with the `Start`, `Update`, and `OnDestroy` methods. Below is a comparison between a Unity behavior and its equivalent for UE: Actors and Components.

In Unity, you might have a simple component that looks like this:

```
`public class MyComponent : MonoBehaviour { 	void Start() {} 	void OnDestroy() {} 	void Update() {} }`
Copy full snippet
```
public class MyComponent : MonoBehaviour { void Start() {} void OnDestroy() {} void Update() {} }

### AActor

In UE, you can write code on the Actor itself rather than only coding new component types.

Additionally, Actors have similar methods to Unity's `Start`, `OnDestroy`, and `Update` methods.

#### C++

```
`UCLASS() class AMyActor : public AActor { 	GENERATED_BODY()  	// Called at start of game. 	void BeginPlay();  	// Called when destroyed. 	void EndPlay(const EEndPlayReason::Type EndPlayReason);  	// Called every frame to update this actor. 	void Tick(float DeltaSeconds); };`
Copy full snippet
```
UCLASS() class AMyActor : public AActor { GENERATED\_BODY() // Called at start of game. void BeginPlay(); // Called when destroyed. void EndPlay(const EEndPlayReason::Type EndPlayReason); // Called every frame to update this actor. void Tick(float DeltaSeconds); };

#### Blueprint

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a44c755a-8b89-491c-9afe-14c58128e43a/image_29.png)

### UActorComponent

Components in UE are conceptually similar to MonoBehaviors but contain different methods.

#### C++

```
`UCLASS() class UMyComponent : public UActorComponent { 	GENERATED_BODY()  	// Called after the owning Actor was created 	void InitializeComponent();  	// Called when the component or the owning Actor is being destroyed 	void UninitializeComponent();  	// Component version of Tick 	void TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction* ThisTickFunction); };`
Copy full snippet
```
UCLASS() class UMyComponent : public UActorComponent { GENERATED\_BODY() // Called after the owning Actor was created void InitializeComponent(); // Called when the component or the owning Actor is being destroyed void UninitializeComponent(); // Component version of Tick void TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction\* ThisTickFunction); };

#### Blueprint

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da6169ba-5ffe-4926-9091-7dbd3b95d68f/image_30.png)

## Additional Notes

-   In UE, you must explicitly call the parent's method within a child's method. For example, in Unity C# this would be `base.Update()`, but in UE C++ you will use `Super::Tick()` for Actors or `Super::TickComponent()` for Components.
-   In UE C++, classes use various prefixes, such as `U` for `UObject` subclasses and `A` for Actor subclasses. See [Coding Standard](/documentation/en-us/unreal-engine/epic-cplusplus-coding-standard-for-unreal-engine) for more detailed information.
-   For gameplay coding examples, see [Creating Gameplay in Unreal Engine](/documentation/en-us/unreal-engine/creating-gameplay-in-unreal-engine-for-unity-developers).
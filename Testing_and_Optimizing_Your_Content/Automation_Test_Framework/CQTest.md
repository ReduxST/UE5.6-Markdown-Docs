# CQTest

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cqtest-test-framework-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cqtest-test-framework-for-unreal-engine)  
**Processed:** 2025-06-14 16:16:31

---

**CQTest**, or **Code Quality Test**, is an extension of the \*\*Unreal Engine (UE)`** FAutomationTestBase` providing test fixtures and common automation testing commands. CQTest's goal is to simplify writing new tests compared with previous testing frameworks in UE, and support *before* and *after* test actions to automatically reset state between tests.

## Setup

CQTest is included in UE as a C++ Module that you can add to your project. UE also has several plugins with tests you can look at to see how it works. This section walks through setting up the CQTest Module and using the test plugins.

### Adding the CQTest Module to Your Project

To use the CQTest module in your project, follow these steps:

1.  Open your project in your IDE of choice (for example, Visual Studio, Xcode, or Rider).
    
2.  Open your project's `.Build.cs` file and add `CQTest` to your project module's `PrivateDependencyModuleNames`:
    
    Project Build.cs
    
    ```
         `PrivateDependencyModuleNames.AddRange      (          new string[]           {              "Core",              "CoreUObject",              "Engine",              "CQTest"          }      );`
    Copy full snippet
    ```
    PrivateDependencyModuleNames.AddRange ( new string\[\] { "Core", "CoreUObject", "Engine", "CQTest" } );
3.  Compile your project. Once compilation is complete, CQTest should now be available to use in your project.
    

### Test Plugins

Unreal Engine includes two plugins providing a set of tests to validate and demonstrate CQTest's behavior:

-   **Code Quality Tests Unreal Test Plugin**
-   **Enhanced Input Code Quality Unreal Test Plugin**

#### Enabling the Plugins

To enable the test plugins, follow these steps:

1.  Open **Unreal Editor**.
    
2.  Open **Edit** \> **Plugins**.
    
3.  Search for **Code Quality Unreal Test Plugin**.
    
4.  Enable either of the above plugins.
    
5.  Restart Unreal Editor when prompted.
    

![The CQ Test example plugins in the Edit > Plugins menu.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a529ea70-33ac-4fc9-8504-5149e648904d/cqtestplugins.png)

After enabling these plugins, their respective tests are available for your project.

#### Run Plugin Tests

To run tests provided by the plugins within the Unreal Editor, follow these steps:

1.  Launch Unreal Editor with your project.
    
2.  Navigate to the **Tools** drop-down menu and select **Sessions Frontend**.
    
3.  By default, the tests should be listed first under **Product.Plugins.CQTest**.
    
4.  Select the tests you want to run and press **Start Tests**.
    

## Test Macros

CQTest provides several test macros:

| **Macro** | **Description** |
| --- | --- |
| `TEST` | Basic test object. |
| `TEST_CLASS` | Test object with setup, teardown, common state, and grouping. See [Latent Actions](/documentation/en-us/unreal-engine/cqtest-test-framework-for-unreal-engine#latentactions) below for information on the available actions for this macro. |
| `TEST_CLASS_WITH_ASSERTS` | Test object with custom asserter. |
| `TEST_CLASS_WITH_BASE` | Test object that can inherit from a different test object. |
| `TEST_CLASS_WITH_FLAGS` | Test object that can use different automation test flags. |
| `TEST_CLASS_WITH_BASE_AND_FLAGS` | Test object that can inherit from a different test object and use different custom automation test flags. |
| `TEST_CLASS_IMPL` | Base macro used by the above macros to specify a custom asserter, a test object to inherit from a different test object, or allow for custom automation test flags. |

## Extending the Framework

The CQTest framework is designed to use extensions in a couple areas. See *CQTestTests/Private/ExtensionTests.cpp* for in-code examples.

## Test Components

The CQTest framework embraces composition over inheritance. Creating new components is the intended default mechanism for extending the framework. Some of the components available to you are:

| **Component** | **Description** |
| --- | --- |
| `SpawnHelper` | Eases the ability to spawn actors and other objects. Implemented by `ActorTestSpawner` and `MapTestSpawner`. |
| `ActorTestSpawner` | Creates a minimal `UWorld` for a test to spawn actors, and manages their despawning. |
| `MapTestSpawner` | Creates a temporary map or opens a specified level. You can use this to spawn actors in the aforementioned test world. |
| `CQTestBlueprintHelper` **(Depricated)** | 
Eases the ability for a test to spawn Blueprint objects, intended to be used with `MapTestSpawner`. Loading Blueprint assets is only intended to work within the Editor context. Tests that make use of the `CQTestBlueprintHelper` should specify the `EAutomationTestFlags::EditorContext` flag.

This is deprecated in favor of using CQTestAssetHelper -- see below in [Helper Objects and Methods](/documentation/en-us/unreal-engine/cqtest-test-framework-for-unreal-engine#helperobjectsandmethods).



 |
| `PIENetworkComponent` | Creates a server and a collection of clients. Good for testing replication. The `PIENetworkComponent` sets up a Server and Client PIE instance which is only usable within the Editor context. Tests that make use of the `PIENetworkComponent` should specify the `EAutomationTestFlags::EditorContext` flag. |
| `InputTestActions` | Injects `InputActions` to the `Pawn`. |
| `CQTestSlateComponent` | Notifies the current test when the UI has been updated. |

## Helper Objects and Methods

This testing framework provides the following helper objects and methods:

| **Helper Object** | **Description** |
| --- | --- |
| `FAssetBuilder` | Creates an asset filter you can use with either the `CQTestAssetHelper` namespace methods or when searching through the `AssetRegistry` directly. |
| `CQTestAssetHelper` | 
Namespace containing helper methods you can use to:

-   Search for asset package paths
-   Search for Blueprints by name
-   Build a filter from the `FAssetFilterBuilder`



 |

## Handling Exceptions

Not all platforms support exceptions, and so the assertions are unable to rely on them.

Here are a few options for running tests on platforms that do not support exceptions:

-   Just throw exceptions, and only run tests on platforms which support exceptions.
    
-   Return a `[[nodiscard]]` bool to encourage checking each assertion and returning if it fails.
    
-   Return a normal bool and rely on people to check it when it's important.
    

Exceptions have the advantage of working in helper functions and lambdas, as well as not depending on human diligence.

A normal bool is less noisy, and allows developers to use [IntelliSense](https://learn.microsoft.com/en-us/visualstudio/ide/using-intellisense), but is more error prone.

The default implementation used is `[[nodiscard]]` bool, with a helper macro `ASSERT_THAT` which does the early return check for you. You can use your own types within the `Assert.AreEqual` and `Assert.AreNotEqual` methods, assuming you have the `==` and `!=` operators defined as needed.

In addition, the error message will print out the string version of your type, assuming you have a `ToString` method defined as well. The framework will complain if it doesn't know how to print your value.

You can find examples of providing a string to the framework in *CQTestTests/Private/Assert/CQTestConvertTests.cpp*, but below is a simple example:

Example C++

```
	`struct MyCustomType 	{ 		int32 Value;  		bool operator==(const MyCustomType& other) const  		{ 			return Value == other.Value; 		}  		bool operator!=(const MyCustomType& other) const  		{ 			return !(*this == other); 		}  		FString ToString() const  		{ 			//your to string logic 			return FString(); 		}  	};  	enum struct MyCustomEnum 	{ 		Red, Green, Blue 	};  	template<>  	FString CQTestConvert::ToString(const MyCustomEnum&) 	{ 		//your to string logic 		return FString(); 	}`
Copy full snippet
```
struct MyCustomType { int32 Value; bool operator==(const MyCustomType& other) const { return Value == other.Value; } bool operator!=(const MyCustomType& other) const { return !(\*this == other); } FString ToString() const { //your to string logic return FString(); } }; enum struct MyCustomEnum { Red, Green, Blue }; template<> FString CQTestConvert::ToString(const MyCustomEnum&) { //your to string logic return FString(); }

## Latent Actions

CQTest supports latent actions through the `TEST_CLASS` macro. Each step completes all latent actions before moving to the next. If an assertion is raised during a latent action, then no further latent actions will be processed, but the `AFTER_EACH` method will still be invoked.

Example C++

```
    `TEST_CLASS(LatentActionTest, "Game.Test")  	{ 		uint32 calls = 0;  		BEFORE_EACH()  		{ 			AddCommand(new FExecute([&]() { calls++; })); 		}  		AFTER_EACH()  		{ 			AddCommand(new FExecute([&]() { calls++; })); // executed after the next line, as it is a latent action 			ASSERT_THAT(AreEqual(2, calls)); 		}  		TEST_METHOD(PerformLatentAction)  		{ 			ASSERT_THAT(AreEqual(1, calls)); 			AddCommand(new FExecute([&]() { calls++; })); 		} 	};`
Copy full snippet
```
TEST\_CLASS(LatentActionTest, "Game.Test") { uint32 calls = 0; BEFORE\_EACH() { AddCommand(new FExecute(\[&\]() { calls++; })); } AFTER\_EACH() { AddCommand(new FExecute(\[&\]() { calls++; })); // executed after the next line, as it is a latent action ASSERT\_THAT(AreEqual(2, calls)); } TEST\_METHOD(PerformLatentAction) { ASSERT\_THAT(AreEqual(1, calls)); AddCommand(new FExecute(\[&\]() { calls++; })); } };

CQTest provides the following additional latent actions:

| **Latent Action Type** | **Description** |
| --- | --- |
| `FExecute` | Action that executes only once. |
| `FWaitUntil` | Action that executes over multiple ticks until either completion or the duration exceeds the timeout. Action fails if the condition cannot be satisfied before timing out. |
| `FWaitDelay` | Action that waits a specified duration. **Warning:** Using a timed-wait can introduce unreliability due to variable runtimes. We recommend using the above `FWaitUntil` action instead. |
| `FRunSequence` | Action that ensures a collection of latent actions occur in order, and only after all previous actions have finished. |

### Command-Builder

Also available for commands is a fluent command builder.

Example C++

```
	`TEST_METHOD(SomeTest)  	{ 		TestCommandBuilder 			.Do([&]() { StepOne(); }) 			.Then([&]() { StepTwo(); }) 			.Until([&]() { return StepThreeComplete(); }) 			.Then([&]() { ASSERT_THAT(IsTrue(SomethingImportant)); }); 	}`
Copy full snippet
```
TEST\_METHOD(SomeTest) { TestCommandBuilder .Do(\[&\]() { StepOne(); }) .Then(\[&\]() { StepTwo(); }) .Until(\[&\]() { return StepThreeComplete(); }) .Then(\[&\]() { ASSERT\_THAT(IsTrue(SomethingImportant)); }); }

The command builder provides commands which wrap around the above mentioned latent actions. The following commands are made available:

| **Command** | **Description** |
| --- | --- |
| `Do`/`Then` | Commands which add the `FExecute` latent action with the provided lambda to be executed. |
| `StartWhen`/`Until` | Commands which add the `FWaitUntil` latent action with the provided lambda to be evaluated. |
| `WaitDelay` | 
Command which waits a specified duration before continuing.

Using a timed-wait can introduce flakiness due to variable runtimes and the above `StartWhen`/`Until` commands should be used instead.



 |
| `OnTearDown`/`CleanUpWith` | Commands which add the `FExecute` latent action with the provided lambda to be executed after the test. Can be called multiple times to add multiple clean up latent actions. Actions using OnTearDown or CleanUpWith run in reverse order to help avoid confusion. |

The framework does not currently support adding latent actions from within latent actions. Instead, add the actions as a series of self-contained steps.

## CQTest Examples

You can write a test as simple as:

Example C++

```
	`#include "CQTest.h"  	TEST(MinimalTest, "Game.MyGame") 	{ 		ASSERT_THAT(IsTrue(true)); 	}`
Copy full snippet
```
#include "CQTest.h" TEST(MinimalTest, "Game.MyGame") { ASSERT\_THAT(IsTrue(true)); }

Use the `TEST_CLASS` macro for test objects with:

-   Setup
    
-   Teardown
    
-   Common state between multiple tests
    
-   Grouping related tests
    

The `TEST_CLASS` macro can be used as follows:

Example C++

```
	`#include "CQTest.h" 	 	TEST_CLASS(MyTest, "Game.MyGame") 	{ 		bool SetupCalled = false; 		uint32 SomeNumber = 0; 		Thing* Thing = nullptr;  		// Optional static method executed before all tests of this TEST_CLASS 		// Remove if unused 		BEFORE_ALL() 		{ 			//Perform logic shared with all tests, such as loading a level 		}  		BEFORE_EACH() 		{ 			//Perform logic that is called before each test of this TEST_CLASS	 			SetupCalled = true; 			SomeNumber++; 			Thing = new Thing(); 		}  		AFTER_EACH() 		{ 			//Perform logic that is called after each test of this TEST_CLASS 			delete Thing; 		}  		// Optional static method executed after all tests of this TEST_CLASS 		// Remove if unused 		AFTER_ALL() 		{ 			//Perform cleanup of any resources allocated in BEFORE_ALL 		}  	protected:  		bool HelperMethod() const 		{ 			return true; 		}  		TEST_METHOD(BeforeRunTest_CallsSetup) 		{ 			ASSERT_THAT(IsTrue(SetupCalled)); 		}  		TEST_METHOD(ProtectedMembers_AreAccessible) 		{ 			ASSERT_THAT(IsTrue(HelperMethod())); 		}  		TEST_METHOD(DataMembers_BetweenTestRuns_AreReset) 		{ 			ASSERT_THAT(AreEqual(1, SomeNumber)); 		} 	};`

Copy full snippet
```
#include "CQTest.h" TEST\_CLASS(MyTest, "Game.MyGame") { bool SetupCalled = false; uint32 SomeNumber = 0; Thing\* Thing = nullptr; // Optional static method executed before all tests of this TEST\_CLASS // Remove if unused BEFORE\_ALL() { //Perform logic shared with all tests, such as loading a level } BEFORE\_EACH() { //Perform logic that is called before each test of this TEST\_CLASS SetupCalled = true; SomeNumber++; Thing = new Thing(); } AFTER\_EACH() { //Perform logic that is called after each test of this TEST\_CLASS delete Thing; } // Optional static method executed after all tests of this TEST\_CLASS // Remove if unused AFTER\_ALL() { //Perform cleanup of any resources allocated in BEFORE\_ALL } protected: bool HelperMethod() const { return true; } TEST\_METHOD(BeforeRunTest\_CallsSetup) { ASSERT\_THAT(IsTrue(SetupCalled)); } TEST\_METHOD(ProtectedMembers\_AreAccessible) { ASSERT\_THAT(IsTrue(HelperMethod())); } TEST\_METHOD(DataMembers\_BetweenTestRuns\_AreReset) { ASSERT\_THAT(AreEqual(1, SomeNumber)); } };
# Write C++ Tests

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/write-cplusplus-tests-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/write-cplusplus-tests-in-unreal-engine)  
**Processed:** 2025-06-14 17:05:13

---

## Automation Testing

**Automation Testing** is the lowest level of automated testing, and is best suited for low-level tests of the core functionality of **Unreal Engine**. This system exists outside of the `UObject` ecosystem, so it is not visible to **Blueprints** or the Engine's **Reflection System**. These tests are built in code and can be run from the **Console Command Line**, either in the **Editor** or with **Command-Line Parameters** from your operating system. Automation Tests can be broken into two types: **Simple** and **Complex**. Both types are implemented as derived classes based on `FAutomationTestBase`.

### Creating a New Automation Test

Automation Tests are declared by macros, and implemented by overriding virtual functions from the `FAutomationTestBase` class. Simple Tests are declared using the `IMPLEMENT_SIMPLE_AUTOMATION_TEST` macro, while Complex Tests require the `IMPLEMENT_COMPLEX_AUTOMATION_TEST` macro. Both macros feature the same three parameters, in the following order:

| Parameter | Description |
| --- | --- |
| `TClass` | The desired class name of the test. The macro will create a class of this name, e.g. `FPlaceholderTest`, in which your test can be implemented. |
| `PrettyName` | A string specifying the hierarchical test name that will appear in the UI. For example, "TestGroup.TestSubgroup.Placeholder Test" in our minimal example (below). |
| `TFlags` | A combination of `EAutomationTestFlags` values, used for specifying Automation Test requirements and behaviors. See [`EAutomationTestFlags`](/documentation/en-us/unreal-engine/API/Runtime/Core/Misc/EAutomationTestFlags) for details. |

Once the new Automation Test class has been declared by one of the two macros, its functionality can be implemented. The following functions must be written:

| Function | Parameter | Description |
| --- | --- | --- |
| `RunTest` |   | This function performs the actual test, returning `true` to indicate that the test passed, or `false` to indicate that it failed. |
|   | `Parameters` | This parameter can be parsed or passed through to other functions as appropriate for the specific Functional Test. |
| \-- |   |   |
| `GetTests` |   | This function must be overridden for Complex Tests only; Simple Tests have an auto-generated version of this function built into their declaration macro. |
|   | `OutBeautifiedNames` | This array of strings must be populated with the UI-visible `PrettyName` of each individual Test. |
|   | `OutTestCommands` | This array of strings is expected to be parallel to `OutBeautifiedNames` and must be populated with the `Parameters` to be passed into `RunTest`. |

#### Source File Locations

The current convention is to put all Automation Tests into the `Private\Tests` directory within the relevant module. When an Automation Test matches one-to-one with a particular class, please name the test file `[ClassFilename]Test.cpp`, e.g. a test that applies only to `FText` would be written in `TextTest.cpp`.

#### Minimal Example

The smallest and simplest test possible would be a Simple Test that automatically succeeds (or fails). Building a test like this can be useful as a first step to ensuring that your testing setup is correct before building more meaningful tests.

```
	`IMPLEMENT_SIMPLE_AUTOMATION_TEST(FPlaceholderTest, "TestGroup.TestSubgroup.Placeholder Test", EAutomationTestFlags::EditorContext | EAutomationTestFlags::EngineFilter)  	bool FPlaceholderTest::RunTest(const FString& Parameters) 	{ 		// Make the test pass by returning true, or fail by returning false. 		return true; 	}`
Copy full snippet
```
IMPLEMENT\_SIMPLE\_AUTOMATION\_TEST(FPlaceholderTest, "TestGroup.TestSubgroup.Placeholder Test", EAutomationTestFlags::EditorContext | EAutomationTestFlags::EngineFilter) bool FPlaceholderTest::RunTest(const FString& Parameters) { // Make the test pass by returning true, or fail by returning false. return true; }

### Simple Tests

**Simple Tests** are used to describe single atomic tests, and are useful as unit or feature tests. For example, simple tests can be used to test if the current map loads in Play In Editor or whether text wrapping is working properly in Slate. The following example tests the functionality of the `SetRes` command:

```
	`IMPLEMENT_SIMPLE_AUTOMATION_TEST( FSetResTest, "Windows.SetResolution", ATF_Game )  	bool FSetResTest::RunTest(const FString& Parameters) 	{ 		FString MapName = TEXT("AutomationTest"); 		FEngineAutomationTestUtilities::LoadMap(MapName);  		int32 ResX = GSystemSettings.ResX; 		int32 ResY = GSystemSettings.ResY; 		FString RestoreResolutionString = FString::Printf(TEXT("setres %dx%d"), ResX, ResY);  		ADD_LATENT_AUTOMATION_COMMAND(FEngineWaitLatentCommand(2.0f)); 		ADD_LATENT_AUTOMATION_COMMAND(FExecStringLatentCommand(TEXT("setres 640x480"))); 		ADD_LATENT_AUTOMATION_COMMAND(FEngineWaitLatentCommand(2.0f)); 		ADD_LATENT_AUTOMATION_COMMAND(FExecStringLatentCommand(RestoreResolutionString));  		return true; 	}`
Copy full snippet
```
IMPLEMENT\_SIMPLE\_AUTOMATION\_TEST( FSetResTest, "Windows.SetResolution", ATF\_Game ) bool FSetResTest::RunTest(const FString& Parameters) { FString MapName = TEXT("AutomationTest"); FEngineAutomationTestUtilities::LoadMap(MapName); int32 ResX = GSystemSettings.ResX; int32 ResY = GSystemSettings.ResY; FString RestoreResolutionString = FString::Printf(TEXT("setres %dx%d"), ResX, ResY); ADD\_LATENT\_AUTOMATION\_COMMAND(FEngineWaitLatentCommand(2.0f)); ADD\_LATENT\_AUTOMATION\_COMMAND(FExecStringLatentCommand(TEXT("setres 640x480"))); ADD\_LATENT\_AUTOMATION\_COMMAND(FEngineWaitLatentCommand(2.0f)); ADD\_LATENT\_AUTOMATION\_COMMAND(FExecStringLatentCommand(RestoreResolutionString)); return true; }

### Complex Tests

**Complex Tests** are used to run the same code on a number of inputs. These are generally content stress tests. For instance, loading all maps or compiling all Blueprints would be good fits for complex automation tests. Note that both the `RunTest` and `GetTests` functions must be overridden. The following example tests the loading all of a project's maps:

```
	`IMPLEMENT_COMPLEX_AUTOMATION_TEST(FLoadAllMapsInGameTest, "Maps.LoadAllInGame", ATF_Game)  	void FLoadAllMapsInGameTest::GetTests(TArray<FString>& OutBeautifiedNames, TArray <FString>& OutTestCommands) const 	{ 		FEngineAutomationTestUtilities Utils; 		TArray<FString> FileList; 		FileList = GPackageFileCache->GetPackageFileList();  		// Iterate over all files, adding the ones with the map extension.. 		for( int32 FileIndex=0; FileIndex< FileList.Num(); FileIndex++ ) 		{ 			const FString& Filename = FileList[FileIndex];  			// Disregard filenames that don't have the map extension if we're in MAPSONLY mode. 			if ( FPaths::GetExtension(Filename, true) == FPackageName::GetMapPackageExtension() ) 			{ 				if (!Utils.ShouldExcludeDueToPath(Filename)) 				{ 					OutBeautifiedNames.Add(FPaths::GetBaseFilename(Filename)); 					OutTestCommands.Add(Filename); 				} 			} 		} 	}  	bool FLoadAllMapsInGameTest::RunTest(const FString& Parameters) 	{ 		FString MapName = Parameters;  		FEngineAutomationTestUtilities::LoadMap(MapName); 		ADD_LATENT_AUTOMATION_COMMAND(FEnqueuePerformanceCaptureCommands());  		return true; 	}`
Copy full snippet
```
IMPLEMENT\_COMPLEX\_AUTOMATION\_TEST(FLoadAllMapsInGameTest, "Maps.LoadAllInGame", ATF\_Game) void FLoadAllMapsInGameTest::GetTests(TArray<FString>& OutBeautifiedNames, TArray <FString>& OutTestCommands) const { FEngineAutomationTestUtilities Utils; TArray<FString> FileList; FileList = GPackageFileCache->GetPackageFileList(); // Iterate over all files, adding the ones with the map extension.. for( int32 FileIndex=0; FileIndex< FileList.Num(); FileIndex++ ) { const FString& Filename = FileList\[FileIndex\]; // Disregard filenames that don't have the map extension if we're in MAPSONLY mode. if ( FPaths::GetExtension(Filename, true) == FPackageName::GetMapPackageExtension() ) { if (!Utils.ShouldExcludeDueToPath(Filename)) { OutBeautifiedNames.Add(FPaths::GetBaseFilename(Filename)); OutTestCommands.Add(Filename); } } } } bool FLoadAllMapsInGameTest::RunTest(const FString& Parameters) { FString MapName = Parameters; FEngineAutomationTestUtilities::LoadMap(MapName); ADD\_LATENT\_AUTOMATION\_COMMAND(FEnqueuePerformanceCaptureCommands()); return true; }

The `Parameters` argument can be built and parsed in whatever way is needed for a specific testing situation. For Complex Tests, this is the intended way to test several data points using the same code.

### Latent Commands

**Latent Commands** can be queued up during `RunTest`, causing sections of the code to run across multiple frames. To create a Latent Action, it must be defined via the `DEFINE_LATENT_AUTOMATION_COMMAND` macro. This macro takes one parameter, known as `CommandName`, which defines the class name that will be created for this type of Latent Command. To finish creating the Latent Command, the new class will require a function body for its `Update` function. Here is an example of a simple Latent Command which runs until the **Unit Test Manager** is finished running tests:

```
	`DEFINE_LATENT_AUTOMATION_COMMAND(FNUTWaitForUnitTests);  	bool FNUTWaitForUnitTests::Update() 	{ 		return GUnitTestManager == NULL || !GUnitTestManager->IsRunningUnitTests(); 	}`
Copy full snippet
```
DEFINE\_LATENT\_AUTOMATION\_COMMAND(FNUTWaitForUnitTests); bool FNUTWaitForUnitTests::Update() { return GUnitTestManager == NULL || !GUnitTestManager->IsRunningUnitTests(); }

If the Latent Command you wish to create requires an argument, such as a parameter string, the `DEFINE_LATENT_AUTOMATION_COMMAND` macro can be used. This macro takes two additional parameters, known as `ParamType` and `ParamName`, which define the type and name of the parameter to be passed in. In this example, a Latent Command is used to start connecting to a source control provider and then wait until the connection attempt finishes:

```
	`DEFINE_LATENT_AUTOMATION_COMMAND_ONE_PARAMETER(FConnectLatentCommand, SourceControlAutomationCommon::FAsyncCommandHelper, AsyncHelper);  	bool FConnectLatentCommand::Update() 	{ 		// Attempt a login and wait for the result. 		if(!AsyncHelper.IsDispatched()) 		{ 			if(ISourceControlModule::Get().GetProvider().Login( FString(), EConcurrency::Asynchronous, FSourceControlOperationComplete::CreateRaw( &AsyncHelper, &SourceControlAutomationCommon::FAsyncCommandHelper::SourceControlOperationComplete ) ) != ECommandResult::Succeeded) 			{ 				return false; 			} 			AsyncHelper.SetDispatched(); 		}  		return AsyncHelper.IsDone(); 	}`
Copy full snippet
```
DEFINE\_LATENT\_AUTOMATION\_COMMAND\_ONE\_PARAMETER(FConnectLatentCommand, SourceControlAutomationCommon::FAsyncCommandHelper, AsyncHelper); bool FConnectLatentCommand::Update() { // Attempt a login and wait for the result. if(!AsyncHelper.IsDispatched()) { if(ISourceControlModule::Get().GetProvider().Login( FString(), EConcurrency::Asynchronous, FSourceControlOperationComplete::CreateRaw( &AsyncHelper, &SourceControlAutomationCommon::FAsyncCommandHelper::SourceControlOperationComplete ) ) != ECommandResult::Succeeded) { return false; } AsyncHelper.SetDispatched(); } return AsyncHelper.IsDone(); }

When the `Update` function returns `true`, the Latent Command is considered complete. A return value of `false` indicates that the Automation Test should stop executing immediately and try again next frame. To use a Latent Command in your test code, invoke the `ADD_LATENT_AUTOMATION_COMMAND` with the constructor of the Latent Command you wish to run. If the Latent Command was established with a parameter, pass in the value that the parameter should take as a constructor argument. In your `RunTest` function, the following code will wait for all Unit Tests to finish, then attempt to connect to a previously-named source control provider:

```
	`ADD_LATENT_AUTOMATION_COMMAND(FNUTWaitForUnitTests()); 	ADD_LATENT_AUTOMATION_COMMAND(FConnectLatentCommand(SourceControlAutomationCommon::FAsyncCommandHelper()));`
Copy full snippet
```
ADD\_LATENT\_AUTOMATION\_COMMAND(FNUTWaitForUnitTests()); ADD\_LATENT\_AUTOMATION\_COMMAND(FConnectLatentCommand(SourceControlAutomationCommon::FAsyncCommandHelper()));

Activities related to loading or streaming data, or anything else that isn't guaranteed to run in a single frame, are candidates for Latent Command usage. For example, in the Editor, loading a map happens immediately, but in game, loading a map happens on the next frame, so Latent Commands must be used to ensure consistent behavior when an Automation Test needs to load a map.